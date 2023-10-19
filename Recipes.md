# Recipe CRUD

This needs full stack implementation, backend, graphql, UI.

## hREA

This needs to be added to hREA, including the graphql api.  Figure out the technical part.  Probably its own zome, maybe also DNA?

Here is the model (blue is new).

![recipes](https://github.com/Carbon-Farm-Network/Requirements-Doc/assets/3776081/99dff7bc-da76-467e-bbd9-00babcd0344f)

For CFN, I think they will have only one-process recipes, with that process's inputs and outputs.  (Other use cases will probably require multiple processes per recipe, but we don't have to worry about that now in terms of the UI.  And the data model is basically the same too.)

1. Add `substitutable` to ResourceSpecification. (This can also wait until later, I'm not sure we need it for this use case.  In fact, since there is an open modeling question involved there, it might be best to wait anyhow.)
2. Two new classes: `RecipeProcess` and `RecipeFlow`.  And their relationships.  They have basically the same structure as `Process` and `Commitment`; or `Process` and `EconomicEvent`; or `Process` and `Intent`.  A process with it's input and output flows.  The main way the relationships work is from `RecipeFlow` to `Process`.  (We'll eventually want queries that go the other direction.)  You can find the same properties and copy them from those existing classes, should be the same datatypes.
3. Add graphql api for the new classes.  Need Create, Update, Delete for both.  Deleting a `RecipeProcess` should cascade to its `RecipeFlow`s.  To save time, we could skip Update for now if we want.  Again, you can copy from `Process` and `Commitment` (or `Intent` or `EconomicEvent`) and adjust the naming.

## UI

This will be a new menu item on the "config" menu from the upper right person icon.  "Recipes".  It can probably be a list + CUD modal, like the others, but it is a more complex data structure.

I'm not sure the best UX for this, will work on something.  The process plus inputs and outputs should be on the same page.  Ideas welcome.

## Data

Here's a way to think about the recipes.  In this diagram, each process is a recipe.  So, for example, the Ship processes are one process with multiple inputs and outputs; but the Spin processes are one process per output.  This is so tracing the input-process-output graph will work correctly. Together these recipes should be able to create the plan that is mocked up (actually a more complex plan, but that idea).  The data knows how to hook itself together to make the graph, by matching the `resourceConformsTo` (ResourceSpecification) and sometimes the `stage` (ProcessSpecification), between output of one process and input to another process. (This diagram needs some work at the beginning and end as it connects to offers and requests; but should be good in the middle.)

![cfn-recipes-use](https://github.com/Carbon-Farm-Network/Requirements-Doc/assets/3776081/596a40eb-6d61-4e98-b3df-520023ab7a40)

Also, [putting here](https://github.com/Carbon-Farm-Network/app-carbon-farm-network/blob/main/ui/src/lib/data/recipes.json) is a start at some recipe json for test data, in case it is helpful in understanding the data.
