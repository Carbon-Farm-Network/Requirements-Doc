# Offers

For now, this will be pretty much offers from the farmers, but eventually could include all roles.  When possible, they will want a page where the farmers (and other eventually) can enter their own agent information, and their own offers to the network.

## hREA

This includes Proposal, ProposedIntent, Intent (one Intent for what is offered, one for the price).  I think it is all there already?  

As noted above, we'll have to load in a few Units.

## UI

### Offer CRUD

**On the screen:**

Proposal.hasBeginning (date available, default to today)

(main Intent, ProposedIntent.reciprocal=false)
Intent.resourceConformsTo (ResourceSpecification.name, plus all the FacetValues for the ResourceSpecification filter by ... TBD, set up a facet)
Intent.resourceQuantity (Measure.hasNumericalValue + Measure.hasUnit)
Intent.availableQuantity (Measure.hasNumericalValue + Measure.hasUnit)
Intent.note
Intent.image

(reciprocal Intent, ProposedIntent.reciprocal=true)
Intent.resourceQuantity (Measure.hasNumericalValue)
Intent.resourceConformsTo (ResourceSpecification.name, dropdown filtered by.... TBD, set up a facetValue for currencies)

![](https://i.imgur.com/aE1dK0X.png)

**Fields saved:**

Proposal.hasBeginning (screen, default date created)
Proposal.hasEnd (screen, if no longer available checked, save current date)
Proposal.inScopeOf (the network agent)
Proposal.unitBased = true
Proposal.created (current date when created)

(main Intent)
Intent.resourceQuantity (screen, unit="one")
Intent.availableQuantity (screen)
Intent.resourceConformsTo (screen)
Intent.image (screen)
Intent.inScopeOf (the network agent)
Intent.finished (false until no longer available is checked, then true)
Intent.note (screen description)
Intent.action (always "transfer"??? might also be "deliverService"; maybe even "work", others???)
Intent.provider (the offering agent)
ProposedIntent.publishedIn (the proposal)
ProposedIntent.publishes (the Intent)
ProposedIntent.reciprocal = false

(reciprocal Intent, the "price")
Intent.resourceQuantity (screen numeric value, unit = "one")
Intent.resourceConformsTo (screen)
Intent.inScopeOf (the network agent)
Intent.finished (false until no longer available is checked, then true)
Intent.action (always "transfer")
Intent.receiver (the offering agent)
ProposedIntent.publishedIn (the proposal)
ProposedIntent.publishes (the Intent)
ProposedIntent.reciprocal = true
