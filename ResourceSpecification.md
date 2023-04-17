# ResourceSpecifications

## hREA

Should be all there.  We'll need to load in some units (there won't be very many).

## UI

### Resource Specification List
Create a list of resource specs, can be just names.

### Resource Specification CRUD
Add agent popup/modal or separate pane (?) with:
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
