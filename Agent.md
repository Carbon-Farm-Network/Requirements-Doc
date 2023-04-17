# Agents

*Question:* What have we got now for relating Agents with the holochain pubkey ("holochain agent")?  And do we have a way for more than one holochain agent to have permissions for one organization?  Or even for one holochain agent to have permissions for one organization? (Check the doc.)

## hREA

We should be OK with what is there now.  They said that all nodes are organizations, so we can hack Organization.classifiedAs for role in the network if no objections.  It can be just a string *(or is that validated for URLs?)*

## UI

### Agent List
Create a list of agents, can be just names.

### Agent CRUD
Add agent popup/modal or separate pane *(?)* with:
* Logo (Agent.image)
* Name (Agent.name)
* Display information (Agent.note, will include formatted contact info, will end of lines work?)
* Role (use Organization.classifiedAs)
* Location (Agent.primaryLocation, for now just text: lat, long - specify the exact format expected)
* later when we have facets: facets/facet values for the agent

### Add to the map

Add Role as a filter for the Agents on the map.  Also add facet/facet values as filters. (? double check all of this with Laura/Evan)

Add Agent display for when an agent is clicked.  Include: image, name, contact info (in notes), facets with facet values designated for them.  Leave room for adding offers later.

### Examples
Sample from REA Playspace, just informational, or maybe there is some code that could be re-used.
![](https://i.imgur.com/ahweAso.png)
![](https://i.imgur.com/oc4rCxH.png)

2 ideas which can be combined:

![nytl-agent-popup2](https://user-images.githubusercontent.com/3776081/232624062-cc3fa808-7bac-44e9-b23e-27e36678d430.png)
![nytl-agent-popup](https://user-images.githubusercontent.com/3776081/232624113-bf43cadb-6f07-44b7-89d8-7ef1460795e8.png)


