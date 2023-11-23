# Plan from Recipe 

## Additions to hREA and graphql api

1. Add `substitutable` to ResourceSpecification.  It used to be in RecipeResource, which is now gone.  It is a boolean, but should also allow null or whatever is the right thing for this tech, if possible.
2. Add `minimumQuantity` to Intent.  It should look just like `availableQuantity`, and is also optional.

## Attach UI to hREA

### Bring in offers and requests to Planning page

The first column is offers, the last column is requests.  Bring those from hREA, basically the same logic as the offers list and the requests list.  Bring in only if `finished` is false.  (Or if they are being saved without a value, then check not = true.  But hopefully they are saved with the default value false when created.)

### Hook up Plans page

There is a new page with a list of Plans.  Make that show the saved Plans.  (Edit and Delete need to wait until later.)

### Make Save Plan work

There's a button Save Plan on the planning page, with a modal when clicked, including name and note.  If they Save, then:

* create a `Plan` in hREA: `name` and `note` come from the modal. use current timestamp for `created`.
* for each process in memory (`allColumns`), create a `Process` in hREA: Include `name`, `note`, `plannedWithin` (the `Plan` just created), `basedOn` (the `ProcessSpecification` referenced), default `finished` to false unless that is done by hREA already.
* for each `Process` created, for each commitment `inputOf`, and each commitment `outputOf` the `Process`, create a `Commitment`: reference the `Process` `inputOf` or `outputOf`, `action`, optionally `stage` (a `ProcessSpecification`), `resourceConformsTo` (a `ResourceSpecification`), a `resourceQuantity` (includes `hasNumericalValue` and `hasUnit` which is a Unit from the list), default `finished` to false unless that is done by hREA already, optionally `note`,  use current timestamp for `created`, optionally `provider` (an `Agent`), optionally `receiver` (an `Agent`).

Create the data for the commitments in the Satisfy Requests column:

* for each commitment (in `commitments` in memory), create a `Commitment` in hREA: include `action`, optionally `provider`, `receiver`, optionally `stage`, `resourceConformsTo`, `resourceQuantity`, `finished` as false, optionally `note`,  use current timestamp for `created`, and `independentDemandOf` (references the `Plan`).
* also for each commitment, create a `Satisfaction` record that is `satisfiedBy` the `Commitment` and `satisfies` the `Intent` that is on the `Proposal` request from the designer, and has `resourceQuantity`, in this case the same value as the one in the commitment.

## UI Work

### Recipe Exchanges in Memory (before save plan)

This is new in VF, not yet tried in an app.  Be prepared for experimentation. :)

When a Commitment is created, either in Satisfy Requests or the All Columns portion of the plan, whether created by us in the plan-from-recipe logic or by them with a create modal:

* Look up to see if there is an exchange recipe (a `recipeClauseOf` RecipeFlow that is attached to a RecipeExchange, for the `resourceConformsTo` and the `stage` (if there is a stage) matching the data in the Commitment just created.
* If not, nothing to do.
* If so, using the recipe data,
    * create an Agreement (`name` and `note` from RecipeExchange, `created` use current timestamp)
    * create a Commitment (the new Agreement as `reciprocalClauseOf`, `finished` false, `resourceConformsTo` and `stage` and `action` and `resourceConformsTo` and `note` from the RecipeFlow, `created` as current timestamp) 
    * to the Commitment that triggered the exchange, add the new Agreement as `clauseOf`
 
When a Commitment is deleted, whether by the user, or because our plan-from-recipe is re-run, if there is also an Agreement, also delete the Agreement and any other Commitment clauses.
