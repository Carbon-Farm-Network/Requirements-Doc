# Plan from Recipe - In Process!

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
  
