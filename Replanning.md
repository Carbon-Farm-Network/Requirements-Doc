# Replanning (supply-driven and demand-driven)

This defines the logic for re-planning.  It won't involve the recipe, which should be disconnected after the first save.  It should use the proportions existing in the plan.  [Note this probably won't work for the ones that used formulas from the recipe.  Should we save that in the plan, or lookup the recipe?  Or can we define a simple way to use existing proportions?]

## Demand-driven

This calculates backwards.

## Supply-driven

This calculates forwards.

Logic: 
```
For each Commitment in the column
  If the Commitment is not finished, use that quantity
  Else add up the Economic Event quantities, and use that
  
```
