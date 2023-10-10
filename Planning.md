# DRAFT !!! 
# Do not use this for any development !!!

![planning-screenshot](https://github.com/Carbon-Farm-Network/Requirements-Doc/assets/3776081/0ac31a44-102b-4e8c-93df-50b1463852d3

Pieces of code:

* CRUD recipes
* Plan from recipe (creates a plan, or a scenario - works for mfg/assembly and workflow patterns)
* Planning page initial display (offers, requests, plan columns)
* Calculate supply-driven quantities, display on page
* Calculate demand-driven quantities, display on page
* User can play with the numbers, create/edit commitment quantities separately from the calculated ones (is this a Scenario or a Plan? should we show payments/costs?)
* Lock in plan (create actual commitments, is this one at a time, or the whole thing, or both?  include payment commitment)
* Notify suppliers of orders (send to them by email?)

Then, after the plan is done:

* Enter actual economic events against the commitments

# Followups to morning discussion:

Lynn suggests recipe for scouring, which then is connected via outputs-of-scouring to inputs of other recipe flows. So requests for various yarn mixtures could use recipes for spinning that accept inputs of different scouring outputs. And designs for knitting could use outputs of spinning processes. So could be different recipes per stage that feed off outputs of recipes for other stages. Knitting recipes would include recipes for previous stages by identifying which recipe they want. A series of such inclusions could constitute a longer recipe. The longer recipe could be used by planFromRecipe for a knitted product.

Does that all make sense?

