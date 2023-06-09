# Facets

[Faceted classification](https://en.wikipedia.org/wiki/Faceted_classification) will be used for both Agents and ResourceSpecifications. This will be all user defined. Approximate examples:
* Agents: facet: Carbon Beneficial Certified, facet values: Certified, In progress, Not Certified.
* Resource Specifications: facet: Color, facet values: White, Black, Gray, Ivory.

## hREA

This needs to be added to hREA, noting that ResourceSpecification and Agent exist.

![facets(1)(1)(2)(1)](https://github.com/Carbon-Farm-Network/Requirements-Doc/assets/3776081/e2dd2c78-3161-4586-8d4d-9a0370062dfc)

Note that [a separate repo](https://github.com/Carbon-Farm-Network/holochain-facets) has been set up, so that the facets can be used for other holochain applications. See that doc also, in the README of the repo.

I don't see putting it into VF until we try it out here.

For us, the FacetGroup will be "hard-coded data", name will be Agent or ResourceSpecification (the class name, which will let our app know which facets to display as choices in the 2 situations).

**Tentative Definitions**

* Facet: A clearly defined aspect of a subject, a semantically cohesive category, if possible mutually exclusive from the other defined facets.
* FacetValue: A possible value of a facet, mutually exclusive from other values for that facet.
* FacetGroup: A set of facets relevant to one subject area or part of an application.

## UI

### Configuration for the network

This is the Facets and FacetValues within each Facet, for each FacetGroup. These are screen shots of the first draft of the UI, before hooking up to the backend. 

![facet-list](https://user-images.githubusercontent.com/3776081/236702038-9e7b5a7b-5bd1-49ad-b826-bec293adb0fa.png)

![add-facet](https://user-images.githubusercontent.com/3776081/236702046-aff7675e-c309-4aa1-8812-1eaf534b58e2.png)

![facet-values](https://user-images.githubusercontent.com/3776081/236702049-47c07f88-7c93-4b50-ba20-6111f95b27bc.png)

### Hook up UI and hREA

Example graphql (**NOT TESTED!!**)

```
mutation CreateFacetGroup {
  createFacetGroup(
    facetGroup: {
      name: "Agent"
      note: "the agent group"
    } 
  ) {
    facetGroup {
      id
      name
      note
    }
  }
}

mutation CreateFacet {
  createFacet(
    facet: {
      name: "Carbon Beneficial Certification"
      note: "USDA program for farms"
    } 
  ) {
    facet {
      id
      name
      note
    }
  }
}

mutation CreateFacetValue {
  createFacetValue(
    facetValue: {
      name: "Pending"
      note: "Organization has applied"
    } 
  ) {
    facetValue {
      id
      name
      note
    }
  }
}

query GetFacetGroups {
  facetGroups {
    edges {
      node {
        id
        name
        note
        facets {
          id
          name
          note
          facetValues {
            id
            name
            note
          }
        }
      }
    }
  }
}
```

### Add FacetValue choices

Agent: Add to the Agent CRUD form a way to pick zero or one FacetValue for each Facet in the Agent FacetGroup, store the data.

ResourceSpecification: Include it when we get to that, which will be needed for offers.

Note: May 7, The first draft of the UI is done.

### Add to the map

Both Agent and ResourceSpecification facet values will be useful filters, once offers are done.  Let's get some direction from the users on this.

Note: May 7, First step here is to test once everything is hooked up and see how the filtering works.

