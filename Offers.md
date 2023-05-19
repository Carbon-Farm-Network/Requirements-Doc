# Offers

For now, this will be pretty much offers from the farmers, but eventually could include all roles.  When possible, they will want a page where the farmers (and others eventually) can enter their own agent information, and their own offers to the network.

Getting ResourceSpecification done is somewhat a predescessor, although we could just use graphiql to load a few in if needed.

## hREA

This includes Proposal, ProposedIntent, Intent (one Intent for what is offered, one for the price).  Double check this is all there already.  [2023-05-18 I'm not finding createProposedIntent, checking on this.]

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

### Hooking up UI and hREA

Graphql example (**NOT TESTED** can't find createProposedIntent):

```
mutation CreateProposal {
  createProposal(
    proposal: {
      hasBeginning: "2023-06-01T18:51:57.105Z"
      unitBased: true
      note: "shearing end of May"
    } 
  ) {
    proposal {
      id
      hasBeginning
      hasEnd
      unitBased
      note
    }
  }
}


mutation CreateIntent {
  createIntent(
    intent: {
      provider: "uhCEklRIkmI3nhepZi4bWgl2L2Cd2TNZV46oWw11Af-KPZNskLLAF:uhC0kk4XetxTAJxYSsm8Z-RRrgfad7VMrOJN45AxB_cA9rMcTW2zr" 
      action: "transfer"
      resourceConformsTo: "uhCEkAtCeqYLW9TfQinZ3DZRM9Y2pdiqvsTnCAUDH3K-Zg8CDxi1H:uhC0kQ4nL2SS4GBSV6xKDpcLXYQN98Iy3w-PPXeJk7P4OpNYDYwKb"
      availableQuantity: {
        hasNumericalValue: 150
        hasUnit: "lb:uhC0kQ4nL2SS4GBSV6xKDpcLXYQN98Iy3w-PPXeJk7P4OpNYDYwKb"
      }
      resourceQuantity: {
        hasNumericalValue: 1
        hasUnit: "lb:uhC0kQ4nL2SS4GBSV6xKDpcLXYQN98Iy3w-PPXeJk7P4OpNYDYwKb"
      }
      note: "darker gray"
    } 
  ) {
    intent {
      id
      provider {
        name
      }   
      action {
        label
      }
      availableQuantity {
        hasNumericalValue
        hasUnit {
          label
        }
      }
      resourceQuantity {
        hasNumericalValue
        hasUnit {
          label
        }
      }
      note
    }
  }
}
    
mutation ProposeIntent {
  proposeIntent(
      reciprocal: false
      publishedIn: "uhCEkoL69h5kzHKpW5Myr5sGqrVw-5RgUK3YinKR5Mt16s8NVVM77:uhC0kQR4R9RqI_64p9sTSSmVuhWuTBObDDBouNWUd6VkowD2JcN6e"
      publishes: "uhCEkk6ROlMKmW2x30607ApgOraIsRJwBx2jKS-aZAPZuI0lm3yPo:uhC0krhVnZQlEi1GOkBDy7iZarzCTplj-kxSmmXZvw_hja57Ry0gc"
  ) {
    proposedIntent {
      id
      reciprocal
      publishes {
        id
        provider {
          name
        }
      	resourceConformsTo {
          name
        }
      }
      publishedIn {
        id
      }
    }
  }
}
```
