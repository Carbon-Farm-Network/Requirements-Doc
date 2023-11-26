# Recipe CRUD

This needs full stack implementation, backend, graphql, UI.

## hREA

This needs to be added to hREA, including the graphql api.  Figure out the technical part.  Probably its own zome, maybe also DNA?

Here is the model (blue is new).  

**NEW Nov26** One new relationship on the model:  Add another relationship called recipeReciprocalClauseOf in RecipeFlow, referencing RecipeExchange.  It should look just like recipeClauseOf.

![recipes](https://github.com/Carbon-Farm-Network/Requirements-Doc/assets/3776081/13212e0f-5ccb-4b87-91be-55d43523759d)

For CFN, I think they will have only one-process recipes, with that process's inputs and outputs.  (Other use cases will probably require multiple processes per recipe, but we don't have to worry about that now in terms of the UI.  And the data model is basically the same too.)

1. Add `substitutable` to ResourceSpecification. 
2. Two new classes: `RecipeProcess` and `RecipeFlow`.  And their relationships.  They have basically the same structure as `Process` and `Commitment`; or `Process` and `EconomicEvent`; or `Process` and `Intent`.  A process with it's input and output flows.  The main way the relationships work is from `RecipeFlow` to `Process`.  (We'll eventually want queries that go the other direction.)  You can find the same properties and copy them from those existing classes, should be the same datatypes. We won't need the RecipeProcess.hasDuration in the UI, so you can put it in the backend or leave it for later, whichever seems to make the most sense.
3. Add graphql api for the new classes.  Need Create, Update, Delete.  Deleting a `RecipeProcess` should cascade to its `RecipeFlow`s.  To save time, we could skip Update for now if we want.  Again, you can copy from `Process` and `Commitment` (or `Intent` or `EconomicEvent`) and adjust the naming.
4. I kept `RecipeExchange` in the picture, because if you use the schema generation, it will be there, and is a new class.  I don't think we need it for CFN, so you can just comment or stub it out.

## UI

This will be a new menu item on the "config" menu from the upper right person icon.  "Recipes".  

### List

Like the other lists, with an Add Recipe button.  In each list item: Inputs, Process, Outputs.  See if we can fit that on one line across the page.

* Inputs: list of resourceConformsTo (resource specification) names of all the inputs
* Process: the process name
* Outputs: list of  resourceConformsTo (resource specification) names of all the outputs
![recipe-list](https://github.com/Carbon-Farm-Network/Requirements-Doc/assets/3776081/5ba68f21-4b40-4614-9526-ac15fadbd880)


### Recipe page

Process with it's inputs and outputs on one page.

Process:
* Name - RecipeProcess.name - required
* Description - RecipeProcess.note - optional
* Process specification - RecipeProcess.processConformsTo.name (a drop down of all ProcessSpecifications) - required
* (leaving out the hasDuration on the UI)

Input (for each one):
* Action - RecipeFlow.action (drop down of Actions, only the ones where Action.inputOutput is input) - required
* Quantity, Unit (like on Offers) - RecipeFlow.resourceQuantity (drop down on units) - required
* Resource Specification - RecipeFlow.resourceConformsTo (drop down of all RSs) - required
* Stage - RecipeFlow.stage (drop down of ProcessSpecification.name), text something like "choose if this resource must come from a specific process specification" - optional
* Description - RecipeFlow.note - optional

Output (for each one):
* Action - RecipeFlow.action (drop down of Actions, only the ones where Action.inputOutput is output or outputInput) - required
* Quantity, Unit (like on Offers) - RecipeFlow.resourceQuantity (drop down on units) - required
* Resource Specification - RecipeFlow.resourceConformsTo (drop down of all RSs) - required
* Description - RecipeFlow.note - optional
![recipe](https://github.com/Carbon-Farm-Network/Requirements-Doc/assets/3776081/2f89a398-c98e-4d90-a2a3-415487faeb12)
  If this page comes up from Add Recipe, then it automatically brings up this first modal in add mode.)
![recipe-process-modal](https://github.com/Carbon-Farm-Network/Requirements-Doc/assets/3776081/2904df4a-64d7-42e7-a681-fa65b90a55b3)
![recipe-input-modal](https://github.com/Carbon-Farm-Network/Requirements-Doc/assets/3776081/cde24923-a7f9-4165-b883-873c265f1e8b)
![recipe-output-modal](https://github.com/Carbon-Farm-Network/Requirements-Doc/assets/3776081/728f8276-b7c9-4cc6-adf2-4cf61277456f)

### New field:  

Add "substitutable" to the ResourceSpecification modal - true, false, or null.  Some text would be good, like "Any item of this specification can be substituted for any other".  Could default in the list to true.

## Data

Here's a way to think about the recipes.  In this diagram, each process is a recipe.  So, for example, the Ship processes are one process with multiple inputs and outputs; but the Spin processes are one process per output.  This is so tracing the input-process-output graph will work correctly. Together these recipes should be able to create the plan that is mocked up (actually a more complex plan, but that idea).  The data knows how to hook itself together to make the graph, by matching the `resourceConformsTo` (ResourceSpecification) and sometimes the `stage` (ProcessSpecification), between output of one process and input to another process. (This diagram needs some work at the beginning and end as it connects to offers and requests; but should be good in the middle.)

![cfn-recipes-use](https://github.com/Carbon-Farm-Network/Requirements-Doc/assets/3776081/596a40eb-6d61-4e98-b3df-520023ab7a40)

Also, [putting here](https://github.com/Carbon-Farm-Network/app-carbon-farm-network/blob/main/ui/src/lib/data/recipes.json) is a start at some recipe json for test data, in case it is helpful in understanding the data.
