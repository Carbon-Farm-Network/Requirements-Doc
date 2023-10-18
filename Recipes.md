# Recipe CRUD

This will be a new menu item on the "config" menu from the upper right person icon.  "Recipes".  It can probably be a list + CUD modal, like the others, but it is a more complex data structure.

## hREA

This needs to be added to hREA, including the graphql api.  Figure out the technical part.  Probably its own zome, maybe also DNA?

Here is the model (blue is new).

![recipes](https://github.com/Carbon-Farm-Network/Requirements-Doc/assets/3776081/99dff7bc-da76-467e-bbd9-00babcd0344f)

For CFN, I think they will have only one-process recipes, with that process's inputs and outputs.  (Other use cases will probably require multiple processes per recipe, but we don't have to worry about that now in terms of the UI.  And the data model is basically the same too.)

1. Add `substitutable` to ResourceSpecification. (This can also wait until later, I'm not sure we need it for this use case.  In fact, since there is a modeling question involved there, it might be best to wait anyhow.)
2. Two new classes: `RecipeProcess` and `RecipeFlow`.  And their relationships.
3. Add graphql api for the new classes.  Need Create, Edit, Delete for both.  Deleting a `RecipeProcess` should cascade to its `RecipeFlows`.  To save time, we could skip Update for now.
4. 

