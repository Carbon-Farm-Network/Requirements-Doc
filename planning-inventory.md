# Planning - Take into account Inventory

In 2025 CFN will have some inventory from 2024 (clean white wool).  The plan-from-recipe and all subsequent "automatic" planning, like the supply-driven re-planning, will need to take into account existing inventory (resources that are part of the production plan with >0 quantity).

## Logic backwards

Add to the logic for each time an input commitment looks for a recipe that creates the resource spec + stage (if it exists in the input commitment) that the input commitment (the demand) wants.  Something like this, but probably you can structure it better:
```
Add up all the input commitment quantities (demands) in that column, for all processes in the stage, for that resource spec + stage (if stage exists in the input commitments, otherwise just resource spec).  This is the "demand" quantity.  (This is probably already done. Or if you want to do it one at a time, that would be fine, as long as you can take into account what you just did, like by including the commitments just in memory.)

Add up all the inventory items and unfinished `produce` or `transfer` into network commitments (i.e. all the existing or already planned inventory), subtract any unfinished `consume` or `transfer` out of network commitments (i.e. all the other commitments that will want to use that same inventory), for that resource spec + stage (if stage exists in the input commitment, otherwise just resource spec).  This is the "available" quantity.

If available quantity > 0 then
    If the available quantity < the demand quantity then
        Calc the demand quantity minus the available quantity, use that instead of the demand quantity in the logic
        Existing logic....
    Else you are done with this input demand, no need to find a recipe or proceed further for that res spec + stage if applicable
Else
    Existing logic....
```
Note for the future: We should be taking into account substitutability (if not substitutable, then inventory is not relevant).  We should also be taking into account dates, so that if planned increases to inventory occur after the current commitment demand, then they are not included.  These shouldn't matter for CFN, at least yet.

## Logic forwards

The following logic is for just before the season starts.  It will be more complex after there are new economic events that have created new inventory as part of the new season.  More thought needed on that, but can wait until the next milestone that includes events.

Input to output (same stage): 
```
If pickup or accept then
    Don't consider inventory
Else
    Add matching available inventory (see rules above) to the input quantity when figuring out the proportional output(s)
```
Output to input (next stage):
```
For all actions (I think), add matching available inventory (see rules above) to the output quantity when figuring out what the next input quantity should be.
```

## UI

I think the inventory should show up in the column before it is needed, which would be an output column. It can be below the gray stage backgrounds, like the existing transfer in commitments we have now. Let's use a different shape, a rectangle is good.  It should be green, since it is already there.  Fields: resource specification name, quantity/unit.  We'll want to figure out how to not show this year's inventory, vs last year's, once the season starts.  At least I think that would be confusing.  But I'm not sure of a good way.  It might mostly work to check the last event year for the resource, although that is a hack specific to ag-based supply chain.

I think we should also change the transfer-in commitments to the output columns before use (the + icon and the shape).

And if the transfer-in commitments are not being used as part of the supply-forward calculations, we should add that.  Should work similar to the inventory I think, except using the commitment quantity.


