# Examples: CSV Import Implementation

Working CSV examples for data-driven diagram generation. Every example is valid Draw.io CSV import format.

---

## 1. Minimal CSV Import (3 Nodes)

The simplest valid CSV import: three shapes with one connection type.

```csv
# label: %name%
# connect: {"from": "parent", "to": "name"}
# layout: auto
# ignore: parent
#
name,parent
Root,
Child A,Root
Child B,Root
```

This produces three shapes connected in a tree: Root at the top, Child A and Child B below.

---

## 2. Org Chart with Images and Styled Hierarchy

A complete organizational chart with images, email links, and color-coded levels.

```csv
## Organizational chart — Acme Corp
# label: %name%<br><i style="color:gray;">%position%</i><br><a href="mailto:%email%">Email</a>
#
# style: label;image=%image%;whiteSpace=wrap;html=1;rounded=1;fillColor=%fill%;strokeColor=%stroke%;
# parentstyle: swimlane;whiteSpace=wrap;html=1;childLayout=stackLayout;horizontal=1;horizontalStack=0;resizeParent=1;resizeLast=0;collapsible=1;
#
# namespace: org-
# identity: name
#
# connect: {"from": "manager", "to": "name", "invert": true, \
#   "label": "manages", "style": "curved=1;endArrow=blockThin;endFill=1;fontSize=11;"}
#
# width: auto
# height: auto
# padding: -12
#
# ignore: image,fill,stroke,manager,email
# link: url
#
# nodespacing: 40
# levelspacing: 100
# edgespacing: 40
#
# layout: verticalTree
#
name,position,manager,email,fill,stroke,url,image
Tessa Miller,CEO,,[email protected],#dae8fc,#6c8ebf,https://example.com,https://example.com/ceo.png
Edward Morrison,CTO,Tessa Miller,[email protected],#d5e8d4,#82b366,https://example.com,https://example.com/cto.png
Sarah Chen,CFO,Tessa Miller,[email protected],#d5e8d4,#82b366,https://example.com,https://example.com/cfo.png
James Park,Lead Dev,Edward Morrison,[email protected],#fff2cc,#d6b656,https://example.com,https://example.com/dev.png
Lisa Wong,DevOps,Edward Morrison,[email protected],#fff2cc,#d6b656,https://example.com,https://example.com/ops.png
```

Key points:
- `invert: true` makes arrows point downward (manager to report) even though the `from` column is on the child row.
- Image URLs in the `image` column render as icons inside each shape.
- `# link: url` makes each shape a clickable hyperlink.

---

## 3. Flowchart with Conditional Styles

A process flow where shape type (decision, process, terminal) determines the shape style.

```csv
## Order processing flowchart
# label: %name%
# stylename: type
# styles: {"decision": "rhombus;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;", \
#   "process": "rounded=0;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;", \
#   "terminal": "rounded=1;whiteSpace=wrap;html=1;arcSize=50;fillColor=#d5e8d4;strokeColor=#82b366;"}
# connect: {"from": "next", "to": "id", "style": "endArrow=classic;html=1;"}
# connect: {"from": "alt_next", "to": "id", "style": "endArrow=classic;html=1;dashed=1;"}
# identity: id
# namespace: flow-
# width: 120
# height: 60
# layout: auto
# ignore: id,next,alt_next,type
#
id,name,type,next,alt_next
start,Receive Order,terminal,validate,
validate,Validate Data,process,check_stock,
check_stock,In Stock?,decision,ship,notify_customer
ship,Ship Order,process,confirm,
notify_customer,Notify Customer,process,end,
confirm,Confirm Delivery,process,end,
end,Done,terminal,,
```

Key points:
- `stylename: type` selects shape style based on the `type` column value.
- Two `# connect:` directives create two edge types: solid for primary flow, dashed for alternate flow.
- Empty `next` or `alt_next` cells produce no connection (terminal nodes).

---

## 4. Network Topology with Organic Layout

A network diagram using device-type icons and undirected connections.

```csv
## Data center network topology
# label: %hostname%<br><small>%ip%</small>
# stylename: device
# styles: {"router": "shape=mxgraph.cisco.routers.router;whiteSpace=wrap;html=1;", \
#   "switch": "shape=mxgraph.cisco.switches.workgroup_switch;whiteSpace=wrap;html=1;", \
#   "server": "shape=mxgraph.cisco.servers.standard_server;whiteSpace=wrap;html=1;", \
#   "firewall": "shape=mxgraph.cisco.firewalls.firewall;whiteSpace=wrap;html=1;"}
# connect: {"from": "uplink", "to": "hostname", \
#   "style": "endArrow=none;strokeWidth=2;strokeColor=#666666;"}
# identity: hostname
# namespace: net-
# width: 80
# height: 80
# layout: organic
# ignore: ip,device,uplink
#
hostname,ip,device,uplink
core-rtr,10.0.0.1,router,
fw-01,10.0.0.2,firewall,core-rtr
sw-access-1,10.0.1.1,switch,fw-01
sw-access-2,10.0.2.1,switch,fw-01
srv-web-01,10.0.1.10,server,sw-access-1
srv-web-02,10.0.1.11,server,sw-access-1
srv-db-01,10.0.2.10,server,sw-access-2
srv-db-02,10.0.2.11,server,sw-access-2
```

Key points:
- `endArrow=none` creates undirected links (no arrowheads).
- `organic` layout arranges nodes using force-directed positioning — ideal for network graphs.
- Cisco shape library references (`shape=mxgraph.cisco.*`) render as network device icons.

---

## 5. Project Task Board with Color-Coded Status

A Kanban-style task list where status drives shape colors.

```csv
## Sprint backlog — color by status
# label: <b>%task%</b><br><small>%assignee% | %points% pts</small>
# stylename: status
# styles: {"todo": "rounded=1;whiteSpace=wrap;html=1;fillColor=#f5f5f5;strokeColor=#666666;", \
#   "in_progress": "rounded=1;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;", \
#   "review": "rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;", \
#   "done": "rounded=1;whiteSpace=wrap;html=1;fillColor=#d5e8d4;strokeColor=#82b366;"}
# connect: {"from": "blocked_by", "to": "id", \
#   "style": "endArrow=block;endFill=1;strokeColor=#b85450;dashed=1;"}
# identity: id
# namespace: sprint-
# width: 200
# height: 60
# layout: horizontalTree
# ignore: id,status,assignee,points,blocked_by
#
id,task,status,assignee,points,blocked_by
T-001,Setup CI Pipeline,done,Alice,3,
T-002,Design API Schema,done,Bob,5,
T-003,Implement Auth,in_progress,Alice,8,T-002
T-004,Build Dashboard,todo,Carol,5,T-003
T-005,Write Tests,in_progress,Bob,3,T-002
T-006,Code Review,review,Dave,2,T-005
T-007,Deploy to Staging,todo,Alice,2,T-003
```

Key points:
- `horizontalTree` arranges tasks left-to-right following dependency chains.
- Blocking relationships use dashed red arrows to visually stand out.
- HTML labels combine bold task names with smaller metadata.

---

## 6. Circular Peer Relationship Diagram

A team communication map with bidirectional relationships.

```csv
## Team communication patterns
# label: %name%<br><small>%role%</small>
# style: ellipse;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;fontSize=12;
# connect: {"from": "communicates_with", "to": "name", \
#   "style": "endArrow=classic;startArrow=classic;strokeWidth=1;curved=1;"}
# identity: name
# namespace: team-
# width: 100
# height: 60
# layout: circle
# ignore: role,communicates_with
#
name,role,communicates_with
Alice,Frontend,Bob
Bob,Backend,Carol
Carol,DevOps,Dave
Dave,QA,Alice
```

Key points:
- `circle` layout arranges all nodes in a ring.
- `startArrow=classic;endArrow=classic;` creates bidirectional arrows.
- The circular communication chain forms a visible ring pattern.

---

## 7. Dynamic Colors from Data Columns

Shapes with per-row colors driven by data instead of conditional styles.

```csv
## Risk register with dynamic colors
# label: <b>%risk%</b><br>Impact: %impact% | Prob: %probability%
# style: rounded=1;whiteSpace=wrap;html=1;fillColor=%fill%;strokeColor=%stroke%;fontSize=11;
# namespace: risk-
# width: 200
# height: 60
# layout: auto
# ignore: fill,stroke
#
risk,impact,probability,fill,stroke
Data Breach,Critical,High,#f8cecc,#b85450
Server Outage,High,Medium,#fff2cc,#d6b656
API Rate Limit,Medium,Low,#d5e8d4,#82b366
DNS Failure,High,Low,#dae8fc,#6c8ebf
```

Key points:
- `fillColor=%fill%` and `strokeColor=%stroke%` pull hex values directly from each row.
- No `# connect:` directive — shapes are standalone (no relationships).
- Each row produces one independently colored shape.
