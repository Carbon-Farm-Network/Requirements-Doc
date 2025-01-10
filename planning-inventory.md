# Planning - Take into account Inventory

In 2025 CFN will have some inventory from 2024 (clean white wool).  The plan-from-recipe and all subsequent "automatic" planning, like the supply-driven re-planning, will need to take into account existing inventory (resources that are part of the production plan with >0 quantity).

## Logic backwards

Add to the logic for each time an input commitment looks for a recipe that creates the resource spec + stage (if it exists in the input commitment) that the input commitment (the demand) wants.  Something like this, but probably you can structure it better:
```
If there is an inventory item for that resource spec + stage (if it exists in the input) then
    If the inventory item quantity < the input quantity then
        Subtract the input quantity - the inventory quantity, use that instead of the input quantity in the logic
        Existing logic....
    Else you are done with this input demand, no need to find a recipe, but keep track that part or all of that inventory is used
Else
    Existing logic....
```
Note: we don't want to use the same inventory item more than once in the plan.  I think it is safe to say that we can't use the same inventory while processing one input column, since if the same resource spec is used in more than one stage, the stage will be noted in the resource and be used in the comparison. There may be a safer way to do this, that would safely cross multiple plans and multiple stages, like figuring out the available inventory quantity by taking the resource quantity and subtracting any existing unfinished commitments, adding any event quantities that fulfill that commmitment.

## Logic forwards

The following logic is for just before the season starts.  It will be more complex after there are new economic events that have created new inventory as part of the new season.  More thought needed on that.

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
