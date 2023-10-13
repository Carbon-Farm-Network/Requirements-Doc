# Carbon Farm Network: User doc for Release 1

## Installation

1. Install the latest stable Holochain Launcher, https://github.com/holochain/launcher/releases/
2. Download the latest stable Carbon Farm Network release, https://github.com/Carbon-Farm-Network/app-carbon-farm-network/releases
3. Install into the launcher, setting a network seed for yourself or your network
   ![launcher-install-cfn](https://github.com/Carbon-Farm-Network/Requirements-Doc/assets/3776081/b6f35444-7ef6-476d-abfb-9558cac664e3)

## Run it
1. Choose from the launcher, wait for it to come up, it is slow the first time.
2. If you are the first in your network, select to create initial data, and wait for that to be created.
3. It should come up with the map.

### Configuration
You need to configure some things first.
1. Click on the person icon on the upper right to get the configuration menu.
2. Set up some Facets and Facet Values, if you like (optional).  These are classifications for Agents or Resource Specifications.
![cfn-facetvalues](https://github.com/Carbon-Farm-Network/Requirements-Doc/assets/3776081/9a5b1495-3a6d-4d9c-8c05-6f8e9b4031d3)

3. Set up some Resource Specifications.  These are types of resources the nework will use (goods, services, currencies, types of work, ...).
![cfn-resourcespecs](https://github.com/Carbon-Farm-Network/Requirements-Doc/assets/3776081/240b76b6-0044-41e0-bf98-0716703c42f2)
![cfn-resourcespec](https://github.com/Carbon-Farm-Network/Requirements-Doc/assets/3776081/18a600bd-90d6-4e7b-b676-0a3426e0898a)

4. Set up some Agents.  These are organizations that form the network.  (The Agent feature will be developed further in later releases.)
![cfn-agents](https://github.com/Carbon-Farm-Network/Requirements-Doc/assets/3776081/5fb70dcb-d087-4d55-b73a-c079e0602b0e)
![cfn-agent](https://github.com/Carbon-Farm-Network/Requirements-Doc/assets/3776081/74592178-1e28-4d83-ab81-bd2cc4034125)

### Offers
1. Choose Offers from the top menu.
2. Create offers of resources for agents within the network (in this case, farmers, processing mills, transporters).
![cfn-offers](https://github.com/Carbon-Farm-Network/Requirements-Doc/assets/3776081/16314484-7f44-4d30-8f6d-eb97fdf45f05)
![cfn-offer1](https://github.com/Carbon-Farm-Network/Requirements-Doc/assets/3776081/9795d4d9-ccbe-4864-95e8-6d02c65db4d7)

### Requests
1. Choose Requests from the top menu.
2. Create requests of produced resources for agents within the network (in this case, designers). (This works basically like offers.)

### Map
1. Choose Map from the top menu.
2. You should see the Agents you set up (if the latitude/longitude fits on the map scope).
3. You can search for specific agents. (In the future, this will include roles, resource offers, etc.)
4. If you click on an agent, you will see the agent info, their facet values, and their offers on a popup.
![cfn-map-popup](https://github.com/Carbon-Farm-Network/Requirements-Doc/assets/3776081/59a621b5-3d08-4124-a323-7cec42f0f39e)

### Planning
This is a mockup of a page for seasonal planning for the whole network.  (It does *not* work now, but will be worked on next.)
Based on the offers, requests, and recipes for the network's operational work, an initial plan will be created. There will be ways to tweak the plan during the process of firming up the plan with the network participants.  When it is what is ready, commitments will be created between the agents in the network, including the network itself.  The progress will be entered and followed throughout the season, including changes to the plan.
![planning-screenshot](https://github.com/Carbon-Farm-Network/Requirements-Doc/assets/3776081/153f7963-3f30-4055-b309-9363ca197e5c)
