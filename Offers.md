# Offers

For now, this will be pretty much offers from the farmers, but eventually could include all roles.  When possible, they will want a page where the farmers (and others eventually) can enter their own agent information, and their own offers to the network.

Getting ResourceSpecification done is somewhat a predescessor, although we could just use graphiql to load a few in if needed.

## hREA

This includes Proposal, ProposedIntent, Intent (one Intent for what is offered, one for the price).  Double check this is all there already.  

## UI

### Offer List

Show all Proposals that have no hasEnd time, or have hasEnd after now.

Fields: 

- provider on main Intent, Agent.name, 
- resourceSpecification.name (pick from existing)
- available quantity (number, unit name dropdown)
- price per unit (number, "USD" or "$") (needs some more thought about units vs resource specs for currency UX)

Edit, End Offer (which will put the current date/time into Proposal.hasEnd)

Filter by provider agent role, resource specification name, eventually facet values


### Offer CRUD

**On the screen:**

- Proposal.hasBeginning (date available, default to today)

(main Intent, ProposedIntent.reciprocal=false)
- Intent.provider (dropdown of agents) - unless we have the agents create the offers **this isn't on the mockup**
- Intent.resourceConformsTo (ResourceSpecification.name, plus all the FacetValues for the ResourceSpecification filter by ... TBD, set up a facet)
- Intent.resourceQuantity (Measure.hasNumericalValue + Measure.hasUnit.label)
- Intent.availableQuantity (Measure.hasNumericalValue + Measure.hasUnit.label)
- Intent.note
- Intent.image

(reciprocal Intent, ProposedIntent.reciprocal=true)
- Intent.resourceQuantity (Measure.hasNumericalValue)
- Intent.resourceConformsTo (ResourceSpecification.name, dropdown filtered by.... TBD, set up a facetValue for currencies, or just hard code it for now)

![](https://i.imgur.com/aE1dK0X.png)

**Fields saved:**

- Proposal.hasBeginning (screen, default date created)
- Proposal.hasEnd (screen, if no longer available is checked, save current date - or just provide this on the list?)
- Proposal.inScopeOf (the network agent - or don't worry for now, since there is just one scope here)
- Proposal.unitBased = true
- Proposal.created (current date when created)

(main Intent)
- Intent.resourceQuantity (screen)
- Intent.availableQuantity (screen)
- Intent.resourceConformsTo (screen)
- Intent.image (screen)
- Intent.inScopeOf (the network agent)
- Intent.finished (false until no longer available is checked, then true)
- Intent.note (screen description)
- Intent.action (always "transfer"??? might also be "deliverService"; maybe even "work", others??? - Lynn think about it)
- Intent.provider (the offering agent)
- ProposedIntent.publishedIn (the proposal)
- ProposedIntent.publishes (the Intent)
- ProposedIntent.reciprocal = false

(reciprocal Intent, the "price")
- Intent.resourceQuantity (screen numeric value, unit = "one")
- Intent.resourceConformsTo (screen)
- Intent.inScopeOf (the network agent)
- Intent.finished (false until no longer available is checked, then true)
- Intent.action (always "transfer")
- Intent.receiver (the offering agent)
- ProposedIntent.publishedIn (the proposal)
- ProposedIntent.publishes (the Intent)
- ProposedIntent.reciprocal = true
