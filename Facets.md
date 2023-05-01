# Facets

[Faceted classification](https://en.wikipedia.org/wiki/Faceted_classification) will be used for both Agents and ResourceSpecifications. This will be all user defined. Approximate examples:
* Agents: facet: Carbon Beneficial Certified, facet values: Certified, In progress, Not Certified.
* Resource Specifications: facet: Color, facet values: White, Black, Gray, Ivory.

## hREA

This needs to be added to hREA, noting that ResourceSpecification and Agent exist.

![facets-vf](https://user-images.githubusercontent.com/3776081/235470953-1a5b9e60-f8cc-4eb1-b4e0-7b0933804fd4.png)

Note that a separate repo has been set up, so that the facets can be used for other holochain applications.  I don't see putting it into VF until we try it out here, if that is OK.

For us, the FacetGroup will be "hard-coded data", name will be Agent or ResourceSpecification (the class name, which will let our app know which facets to display as choices in the 2 situations).

## UI

### Configuration for the network

This is the Facets and FacetValues within each Facet.  This is done mostly just at the beginning of the network, so we don't need anything fancy.  If time, I'd like to create a CRUD UI, to demonstrate the flexibility for other networks.

### Add FacetValue choices

Agent: Add to the Agent CRUD form a way to pick zero or one FacetValue for each Facet, store the data.

ResourceSpecification: Include it when we get to that, which will be needed for offers.

### Add to the map

Both Agent and ResourceSpecification facet values will be useful filters, once offers are done.  Let's get some direction from the users on this.
