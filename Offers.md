# Offers

For now, this will be pretty much offers from the farmers, but eventually could include all roles.  When it becomes possible, they will want a page where the farmers (and others eventually) can enter their own agent information, and their own offers to the network.  At some point (not needed for this phase), they will need a page for designers to enter their needs.

Getting ResourceSpecification done is somewhat a predescessor, although we could just use graphiql to load a few in if needed.

## hREA

This includes Proposal, ProposedIntent, Intent (one Intent for what is offered, one for the price).

## UI

### Offer List

Show all Proposals that have no hasEnd time, or where the hasEnd is after now. **NOTE: I don't think we have a way to do that now, so just show all Proposals.**

Fields: 

- provider on main Intent, Agent.name 
- offering resourceConformsTo.name on main Intent
- available quantity: hasNumericalValue, hasUnit.label on main Intent
- price per unit: (on reciprocal intent, resourceQuantity.hasNumericalValue, resourceConformsTo.name) + " / " + (on main intent, resourceQuantity.hasNumericalValue, hasUnit.label)

Edit, End Offer (which will put the current date/time into Proposal.hasEnd) - this shows as "Available" on the example, feel free to reverse it if it seems more intuitive to the user.  **OR: We can leave this off for now, it isn't important for the first season.**

Sort by resource specification name, provider name.


### Offer CRUD

**On the screen:**

(main Intent, ProposedIntent.reciprocal=false)
- Intent.provider (dropdown of all agents)
- Intent.resourceConformsTo.name (dropdown of all ResourceSpecifications)
- Intent.availableQuantity.hasNumericalValue + .hasUnit.label (dropdown all units, with the ResourceSpecification chosen pre-selected)
- Intent.resourceQuantity.hasNumericalValue + .hasUnit.label) (after the "PER")
- Intent.note for description

(reciprocal Intent, ProposedIntent.reciprocal=true - Price, before the "PER")
- Intent.resourceQuantity.hasNumericalValue
- Intent.resourceConformsTo.name  (for now, just hard code "US Dollar" there, we might manage this with facets when they are ready, or we might want to add something to the model)

![offer-list](https://github.com/Carbon-Farm-Network/Requirements-Doc/assets/3776081/ff560542-d4d2-43d9-9749-5ac138afcca8)
![offer-popup](https://github.com/Carbon-Farm-Network/Requirements-Doc/assets/3776081/9a6c6d17-6f75-4e40-8e7a-bb879c1c5e9d)


**Fields saved:**

- Proposal.hasBeginning (screen)
- Proposal.unitBased = true
- Proposal.created (current date/time)

(main Intent)
- Intent.resourceQuantity (screen)
- Intent.availableQuantity (screen)
- Intent.resourceConformsTo (screen)
- Intent.finished (false, or maybe it defaults to that already?)
- Intent.note (screen description)
- Intent.action (always "transfer" for now, may want to put it on the screen later)
- Intent.provider (the offering agent)
- ProposedIntent.publishedIn (the proposal)
- ProposedIntent.publishes (the Intent)
- ProposedIntent.reciprocal = false

(reciprocal Intent, the "price")
- Intent.resourceQuantity (screen numeric value, unit = "one")
- Intent.resourceConformsTo (screen)
- Intent.finished (false, or maybe that is the default?)
- Intent.action (always "transfer")
- Intent.receiver (the offering agent)
- ProposedIntent.publishedIn (the Proposal)
- ProposedIntent.publishes (the Intent)
- ProposedIntent.reciprocal = true

### Hooking up UI and hREA

Graphql example:

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

query GetProposals {
  proposals {
    edges {
      node {
        id
        name
        hasEnd
        unitBased
        publishes {
          reciprocal
          publishes {
            resourceConformsTo {
              name
              defaultUnitOfResource {
                label
                symbol
              }
            }
            resourceQuantity {
              hasNumericalValue
              hasUnit {
                label
                symbol
              }
            }
            availableQuantity {
              hasNumericalValue
              hasUnit {
                label
                symbol
              }
            }
            provider {
              id
              name
            }
            receiver {
              id
              name
            }
            finished
            note
          }
        }
      }
    }
  }
}

query GetActions {
  actions {
    id
    label
  }
}

query GetAction {
  action (id:"transfer") {
    id
    label
  }
}
```
