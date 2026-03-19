# Anti-Patterns: CSV Import Implementation

What NOT to do when generating Draw.io CSV import data, with explanations of why each pattern fails.

---

## AP-01: Missing Label Directive

### WRONG

```csv
# style: rounded=1;whiteSpace=wrap;html=1;
# layout: auto
#
name,role
Alice,Developer
Bob,Designer
```

### RIGHT

```csv
# label: %name%<br><small>%role%</small>
# style: rounded=1;whiteSpace=wrap;html=1;
# layout: auto
#
name,role
Alice,Developer
Bob,Designer
```

### Why It Fails

Without `# label:`, shapes render as empty boxes with no visible text. The CSV import ALWAYS requires an explicit label directive — there is no default label behavior.

---

## AP-02: Invalid JSON in Connect Directive

### WRONG

```csv
# connect: {from: manager, to: name}
```

```csv
# connect: {'from': 'manager', 'to': 'name'}
```

```csv
# connect: {"from": manager, "to": name}
```

### RIGHT

```csv
# connect: {"from": "manager", "to": "name"}
```

### Why It Fails

The `# connect:` value MUST be valid JSON. JSON requires double-quoted keys AND double-quoted string values. Single quotes, unquoted keys, and unquoted values all cause a parse error, and no connections are created. The import silently fails — no error message appears.

---

## AP-03: Directive Lines After CSV Data

### WRONG

```csv
name,role,manager
Alice,CEO,
Bob,CTO,Alice
# label: %name%
# connect: {"from": "manager", "to": "name"}
# layout: auto
```

### RIGHT

```csv
# label: %name%
# connect: {"from": "manager", "to": "name"}
# layout: auto
# ignore: manager
#
name,role,manager
Alice,CEO,
Bob,CTO,Alice
```

### Why It Fails

ALL directive lines MUST appear before the CSV header row. Once the parser encounters a line without a `#` prefix, it treats it as the header and all subsequent lines as data. Directive lines placed after data are treated as data rows, producing malformed shapes with `#` characters in their labels.

---

## AP-04: Column Name Mismatch in Placeholders

### WRONG

```csv
# label: %Name%
# connect: {"from": "Manager", "to": "Name"}
#
name,role,manager
Alice,CEO,
Bob,CTO,Alice
```

### RIGHT

```csv
# label: %name%
# connect: {"from": "manager", "to": "name"}
#
name,role,manager
Alice,CEO,
Bob,CTO,Alice
```

### Why It Fails

Column references are case-sensitive. `%Name%` does NOT match the column header `name`. The placeholder renders as the literal text `%Name%` instead of being replaced with the row value. ALWAYS ensure exact case matching between `%placeholder%` references and CSV column headers.

---

## AP-05: Missing CSV Header Row

### WRONG

```csv
# label: %name%
# layout: auto
#
Alice,CEO
Bob,CTO
```

### RIGHT

```csv
# label: %name%
# layout: auto
#
name,role
Alice,CEO
Bob,CTO
```

### Why It Fails

The first non-directive line is ALWAYS treated as the column header. Without a header, the first data row (`Alice,CEO`) becomes the header, and `%name%` finds no matching column. Shapes render with literal `%name%` text, and one data row is lost.

---

## AP-06: Using Both style and stylename/styles

### WRONG

```csv
# style: rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;
# stylename: type
# styles: {"server": "shape=cylinder3;", "client": "rounded=1;"}
# label: %name%
#
name,type
DB Server,server
Web Client,client
```

### RIGHT (Option A: Static Style)

```csv
# style: rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;
# label: %name%
#
name,type
DB Server,server
Web Client,client
```

### RIGHT (Option B: Conditional Styles)

```csv
# stylename: type
# styles: {"server": "shape=cylinder3;whiteSpace=wrap;html=1;fillColor=#e1d5e7;strokeColor=#9673a6;", \
#   "client": "rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;"}
# label: %name%
# ignore: type
#
name,type
DB Server,server
Web Client,client
```

### Why It Fails

When both `# style:` and `# stylename:`/`# styles:` are present, the behavior is unpredictable. The conditional styles may override the static style, or the static style may take precedence depending on the Draw.io version. NEVER mix both approaches — choose one.

---

## AP-07: Forgetting to Ignore Utility Columns

### WRONG

```csv
# label: %name%
# style: rounded=1;whiteSpace=wrap;html=1;fillColor=%fill%;strokeColor=%stroke%;
# connect: {"from": "parent_id", "to": "id"}
# identity: id
# layout: auto
#
id,name,fill,stroke,parent_id
1,Server,#dae8fc,#6c8ebf,
2,Database,#d5e8d4,#82b366,1
```

### RIGHT

```csv
# label: %name%
# style: rounded=1;whiteSpace=wrap;html=1;fillColor=%fill%;strokeColor=%stroke%;
# connect: {"from": "parent_id", "to": "id"}
# identity: id
# layout: auto
# ignore: id,fill,stroke,parent_id
#
id,name,fill,stroke,parent_id
1,Server,#dae8fc,#6c8ebf,
2,Database,#d5e8d4,#82b366,1
```

### Why It Fails

Non-ignored columns become visible metadata attributes in the shape properties panel. Users see `id: 1`, `fill: #dae8fc`, `stroke: #6c8ebf`, `parent_id:` cluttering the shape data. ALWAYS ignore columns that serve only as identifiers, color inputs, or connection references.

---

## AP-08: Missing Identity with Non-First-Column Connections

### WRONG

```csv
# label: %name%
# connect: {"from": "parent_id", "to": "id"}
# layout: auto
# ignore: parent_id,id
#
name,id,parent_id
Root,100,
Child A,200,100
Child B,300,100
```

### RIGHT

```csv
# label: %name%
# connect: {"from": "parent_id", "to": "id"}
# identity: id
# layout: auto
# ignore: parent_id,id
#
name,id,parent_id
Root,100,
Child A,200,100
Child B,300,100
```

### Why It Fails

Without `# identity: id`, the connect directive matches `parent_id` values against the first column (`name`). Since `100` does not match `Root`, no connections are created. ALWAYS set `# identity:` when the connection target column is not the first column in the CSV.

---

## AP-09: Missing Namespace with Multiple Imports

### WRONG

```csv
## First import
# label: %name%
# layout: auto
#
name
Server A
Server B
```

```csv
## Second import (same diagram)
# label: %name%
# layout: auto
#
name
Router X
Router Y
```

### RIGHT

```csv
## First import
# label: %name%
# namespace: servers-
# layout: auto
#
name
Server A
Server B
```

```csv
## Second import (same diagram)
# label: %name%
# namespace: routers-
# layout: auto
#
name
Router X
Router Y
```

### Why It Fails

Without namespaces, both imports generate cell IDs from the same pool. If both CSVs contain a row with the same identity value, the second import overwrites the first shape instead of creating a new one. ALWAYS use unique `# namespace:` prefixes when importing multiple CSVs into the same diagram.

---

## AP-10: Missing Style Key in Conditional Styles

### WRONG

```csv
# label: %name%
# stylename: status
# styles: {"active": "fillColor=#d5e8d4;whiteSpace=wrap;html=1;", \
#   "inactive": "fillColor=#f5f5f5;whiteSpace=wrap;html=1;"}
# layout: auto
# ignore: status
#
name,status
Server A,active
Server B,inactive
Server C,maintenance
```

### RIGHT

```csv
# label: %name%
# stylename: status
# styles: {"active": "fillColor=#d5e8d4;whiteSpace=wrap;html=1;", \
#   "inactive": "fillColor=#f5f5f5;whiteSpace=wrap;html=1;", \
#   "maintenance": "fillColor=#fff2cc;whiteSpace=wrap;html=1;"}
# layout: auto
# ignore: status
#
name,status
Server A,active
Server B,inactive
Server C,maintenance
```

### Why It Fails

The value `maintenance` has no matching key in the `# styles:` JSON. The shape for "Server C" renders with no style applied — it appears as a default rectangle without colors or formatting. EVERY distinct value in the `stylename` column MUST have a corresponding entry in `# styles:`.
