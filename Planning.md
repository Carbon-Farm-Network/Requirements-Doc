# DRAFT !!! 
# Do not use this for any development !!!

![planning-screenshot](https://github.com/Carbon-Farm-Network/Requirements-Doc/assets/3776081/0ac31a44-102b-4e8c-93df-50b1463852d3)

Pieces of code:

* CRUD ProcessSpecifications
   * Add image to ProcessSpecification in the backend
   * List and modal create/update/delete ProcessSpecification, under config menu
* CRUD recipes (we are thinking to hard code these to start)
   * Recipes are not in hREA I think, need to be added from scratch on backend
   * Design a UI that will work for one-process recipes; but some people will need multi-process recipes
   * Include stage
* Plan from recipe (works for mfg/assembly and workflow patterns) >> logic in zome? 
   * Create Plan with Processes/Intents, demand-driven, using requests as independent demand, "squashing" or "expanding" as needed
       * Choose all the independent demand intents (all the yarn requests)
       * Should we put something in the recipe to say intent or commitment created?  and create what it says?
   * Add minimumQuantity to Intent in hREA and to Offer UIs
   * We'll need delete Plan fairly soon, so they can experiment, and fine tune the recipes.
   * Do we need anything more?  Or can it figure out all the correct order?
* Planning page display (offers, requests, plan columns with plan)
   * Visually flag issues (not enough or too much of something) >> logic on client?
* (Re)Calculate supply-driven quantities, display on page >> logic in client? (is there a way to make this modular for others?)
* (Re)Calculate demand-driven quantities, display on page >> lobic in client?
* User can play with the numbers, create/edit intent quantities separately from the calculated ones (should we show payments/costs?)
* Lock in plan (create a plan with actual commitments, is this one at a time, or the whole thing, or both? > probably best to allow one at a time;  include payment commitment and agreement)
* Notify suppliers of orders (send to them by email?  list?)

Then, after the plan is done, it can be used for actual operations:

* Enter actual economic events against the commitments
* List of economic events (start of the accounting....)

# Followups to morning discussion:

Lynn suggests recipe for scouring, which then is connected via outputs-of-scouring to inputs of other recipe flows. So requests for various yarn mixtures could use recipes for spinning that accept inputs of different scouring outputs. And designs for knitting could use outputs of spinning processes. So could be different recipes per stage that feed off outputs of recipes for other stages. Knitting recipes would include recipes for previous stages by identifying which recipe they want. A series of such inclusions could constitute a longer recipe. The longer recipe could be used by planFromRecipe for a knitted product.

Does that all make sense?

# Recipe thoughts:

Stashing the visual here (first version for discussion):
![cfn-recipes](https://github.com/Carbon-Farm-Network/Requirements-Doc/assets/3776081/f6caf87f-332f-4d8d-9377-edcc264f5950)

Tentatively thinking this:
![cfn-recipes-use](https://github.com/Carbon-Farm-Network/Requirements-Doc/assets/3776081/48802e81-c2c2-4ab8-ab16-b0e5f597d8c8)

# moving this from the other file


Trying to create pseudocode by mining the Django code.

## Main code components:
* template: https://lab.allmende.io/valueflows/vf-code-experiments/valuenetwork/-/blob/master/valuenetwork/templates/valueaccounting/plan_from_recipe.html
* view: https://lab.allmende.io/valueflows/vf-code-experiments/valuenetwork/-/blob/master/valuenetwork/valueaccounting/views.py
* code modules:

## Spelunking

In the template:
  <input type="submit" name="create-order" id="createOrder" value="{% trans 'Create plan from recipe' %}"
In the view:

## Lynn Spelunking

* EconomicResourceType.generate_mfg_work_order https://lab.allmende.io/valueflows/vf-code-experiments/valuenetwork/-/blob/master/valuenetwork/valueaccounting/models.py#L2981
* Commitment.generate_producing_process https://lab.allmende.io/valueflows/vf-code-experiments/valuenetwork/-/blob/master/valuenetwork/valueaccounting/models.py#L10766
* (same method) https://lab.allmende.io/valueflows/vf-code-experiments/valuenetwork/-/blob/master/valuenetwork/valueaccounting/models.py#L10830
* Process.explode_demands https://lab.allmende.io/valueflows/vf-code-experiments/valuenetwork/-/blob/master/valuenetwork/valueaccounting/models.py#L7910 --> this method has the recursion


