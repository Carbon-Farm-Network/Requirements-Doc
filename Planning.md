# DRAFT !!! 
# Do not use this for any development !!!

![planning-screenshot](https://github.com/Carbon-Farm-Network/Requirements-Doc/assets/3776081/0ac31a44-102b-4e8c-93df-50b1463852d3)

Pieces of code:

* CRUD recipes (we are thinking to hard code these to start)
   * Recipes are not in hREA I think, need to be added from scratch on backend
   * Design a UI that will work for one-process recipes; but some people will need multi-process recipes
   * Include stage
* Plan from recipe (works for mfg/assembly and workflow patterns)
   * Create Plan with Intents, demand-driven, using requests as independent demand, "squashing" as needed
   * Do we need anything more?  Or can it figure out all the correct order?
* Planning page initial display (offers, requests, plan columns with plan)
   * Add image to ProcessSpecification in the backend
   * CRUD ProcessSpecification, under config menu
* (Re)Calculate supply-driven quantities, display on page
* (Re)Calculate demand-driven quantities, display on page
* User can play with the numbers, create/edit intent quantities separately from the calculated ones (should we show payments/costs?)
* Lock in plan (create a plan with actual commitments, is this one at a time, or the whole thing, or both? > probably best to allow one at a time;  include payment commitment and agreement)
* Notify suppliers of orders (send to them by email?  list?)

Then, after the plan is done:

* Enter actual economic events against the commitments
* List (start of the accounting....)

# Followups to morning discussion:

Lynn suggests recipe for scouring, which then is connected via outputs-of-scouring to inputs of other recipe flows. So requests for various yarn mixtures could use recipes for spinning that accept inputs of different scouring outputs. And designs for knitting could use outputs of spinning processes. So could be different recipes per stage that feed off outputs of recipes for other stages. Knitting recipes would include recipes for previous stages by identifying which recipe they want. A series of such inclusions could constitute a longer recipe. The longer recipe could be used by planFromRecipe for a knitted product.

Does that all make sense?

