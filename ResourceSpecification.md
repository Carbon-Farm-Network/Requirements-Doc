# ResourceSpecifications

## hREA

Should be all there.  We'll need to load in some units (there won't be very many).

## UI

### Resource Specification List
Create a list of resource specs, can be just names.

### Resource Specification CRUD
Add popup/modal or separate pane (?) with:

    - Name (ResourceSpecification.name)
    - Image (ResourceSpecification.image)
    - Default Unit of Resource (ResourceSpecification.defaultUnitOfResource)
    - Default Unit of Effort (ResourceSpecification.defaultUnitOfEffort)
    - Description (ResourceSpecification.note)
    - later when we have facets: facets/facet values for the ResourceSpecification
    
(I don't think we need ResourceSpecification.resourceClassifiedAs.)
    
Sample from REA Playspace, just informational, or maybe there is some code that could be re-used.

![](https://i.imgur.com/MPqKQYd.png)
![](https://i.imgur.com/9VaVUA9.png)

### Hook UI to hREA

Sample graphql (note Unit is included because you'll need to make a unit to use in CreateResourceSpecification - Units won't have a CRUD, they can be created from the graphiql interface when hREA is installed and run from the launcher):
```
mutation CreateUnit {
  createUnit(
    unit: {
      label: "pound"
      symbol: "lb"
    }
  ){
    unit {
      id
      label
      symbol
    }
  }
}

query GetUnits {
  units {
    edges {
      node {
        id
        label
        symbol
      }
    }
  }
}

mutation CreateResourceSpecification {
  createResourceSpecification(
    resourceSpecification: {
      name: "White Alpaca Dirty"
      image: "https://example.com/alpaca"
      note: "good stuff"
      defaultUnitOfResource: "lb:uhC0kQ4nL2SS4GBSV6xKDpcLXYQN98Iy3w-PPXeJk7P4OpNYDYwKb"
    } 
  ) {
    resourceSpecification {
      id
      name
      image
      note
      resourceClassifiedAs
      defaultUnitOfResource {
        label
      }
      defaultUnitOfEffort {
        label
      }
    }
  }
}
```
