# Facets

[Faceted classification](https://en.wikipedia.org/wiki/Faceted_classification) will be used for both Agents and ResourceSpecifications. This will be all user defined. Approximate examples:
* Agents: facet: Carbon Beneficial Certified, facet values: Certified, In progress, Not Certified.
* Resource Specifications: facet: Color, facet values: White, Black, Gray, Ivory.

## hREA

This needs to be added to hREA, noting that ResourceSpecification and Agent exist.  (Discussion welcome to improve this model!)

![](https://i.imgur.com/96aAkH8.png)

Facet.categorizes is there to designate "Agent" or "ResourceSpecification".  If you would rather have separate sets of Facets/FacetValues for each instead, I'll change it.  Maybe the current modularization would indicate that?

We'll need to decide how this fits into the zome/DNA scheme, as well as the graphql scheme.  I don't see putting it into VF until we try it out here, if that is OK.

## UI

### Configuration for the network

This is just the Facets and FacetValues within each Facet.  This is done mostly just at the beginning of the network, so we don't need anything fancy.  We could even consider just loading CFN data in to save time, using graphiql.  That would make sense to me.

### Add FacetValue choices

Agent: Add to the Agent CRUD form a way to pick zero or one FacetValue for each Facet, store the data.

ResourceSpecification: Include it when we get to that, which will be needed for offers.

### Add to the map

Both Agent and ResourceSpecification facet values will be useful filters, once offers are done.  Start with just Agent. Let's get some direction from the users on this.
