# Planning - Take into account Inventory

In 2025 CFN will have some inventory from 2024 (clean white wool).  The plan-from-recipe and all subsequent "automatic" planning, like the supply-driven re-planning, will need to take into account existing inventory (resources that are part of the production plan with >0 quantity).

## Logic backwards

Add to the logic for each time an input commitment looks for a recipe that creates the resource spec + stage (if it exists in the input commitment) that the input commitment (the demand) wants.  Something like this, but probably you can structure it better:
```
If there is an inventory item for that resource spec + stage (if it exists in the input) then
    If the inventory item quantity < the input quantity then
        Subtract the input quantity - the inventory quantity, use that instead of the input quantity in the logic
        Existing logic....
    Else you are done, no need to find a recipe, but keep track that part or all of the inventory is used
Else
    Existing logic....
```
Note: we don't want to use the same inventory item more than once.  I think it is safe to say that we can't use the same inventory while processing one input column.

## Logic forwards



## UI

I think the inventory should show up in the column before it is needed, which would be an output column. It can be below the gray stage backgrounds, like the existing transfer in commitments we have now. Let's use a different shape, a rectangle is good.  It should be green, since it is already there.  Fields: resource specification name, quantity/unit.  We'll want to figure out how to not show this year's inventory, vs last year's, once the season starts.  At least I think that would be confusing.  But I'm not sure of a good way.  It might mostly work to check the last event year for the resource, although that is a hack specific to ag-based supply chain.

I think we should also change the transfer-in commitments to the output columns before use (the + icon and the shape).
