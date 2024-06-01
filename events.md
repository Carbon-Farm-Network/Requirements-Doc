# Economic Events on Planning Page

This will support adding economic events that are based on the planned commitments.

## UI

### Adding an event

Each commitment should have a symbol added (beside the update and delete symbols) to indicate add/update an event.  Or a button, suggestions welcome.  (To keep things simple for this page, we can for now assume only one event per commitment.  That will be mostly true for the CFN, possibly not as much for other networks.  We will add a place on another page to allow more events per commitment.)

Pressing the symbol/button should bring up a modal.

Fields to include:

* Provider - default from commitment
* Receiver - default from commitment
* Resource specification (name) - default from commitment
* Resource quantity (numeric value + unit) - default from commitment
* Date - default current
* Description
* Commitment finished - default true (can be a checkbox)

*Optional, do if there is extra time:* If the commitment is also part of an agreement (i.e. is showing the cost $), then also allow add/update of an event for that reciprocal commitment:

* Payment quantity (numeric value + resource spec name, i.e. "Currency" like in offers modal) - default from reciprocal commitment
* Tracking identifier (for check numbers, etc.)
* Description

On the UI, update the background color of the commitment:  If an event was saved with the Commitment finished not checked, then make it light yellow (started).  If an event was saved with the Commitment finished checked, then make it light green (complete).

### Updating an event

For now, we won't do that, mostly it is not allowed anyhow.  We can always put what is allowed on another page later.  Also, events can't be deleted.

## Saving in hREA

Save the EconomicEvent, save the Fulfillment, using the same quantities as are on the EconomicEvent, and referencing the EconomicEvent and the Commitment.

If the Commitment finished flag is checked, set Commitment.finished to true.

## Affecting EconomicResource

See in VF:

* https://www.valueflo.ws/concepts/resources/#how-resources-relate-to-events
* https://www.valueflo.ws/concepts/resources/#how-resources-relate-to-transfers
* https://www.valueflo.ws/concepts/actions/ especially starting here https://www.valueflo.ws/concepts/actions/#action-behaviors and the chart (this defines what an event should do (or not do) to a resource)

Whenever an EconomicEvent is saved, it should decide if it should also create or update an EconomicResource.  First this depends on the action, not all actions have inventoried/instantiated EconomicResources.  There is generally a user choice if a resource should be created, but I think for CFN, all resources that can be inventoried will be inventoried. So probably, just the deliverService events won't affect a resource.  If we're not keeping track of location (and I don't think we are until we have a real object instead of lat/long), then transportation won't affect the resource either.  Except onhandQuantity, but that doesn't seem very important for CFN, so we can skip onhandQuantity.

If all the action data is up to date in hREA, you can do this as a data-driven thing.  It is probably not, but you could make it so if you like.  You might need to add fields.  If you'd rather not, it's fine to just do it in logic.  And we aren't using that many actions: pickup, dropoff, consume, produce, transfer, deliverService.  Don't ever delete a resource, if it ends up with zero quantity, that's fine.

NOTE: Just found an error in the VF doc.  Because that event has an implied transfer in it, i.e. it will create a resource for CFN. But the other pickups do not. So I need to give this some thought when I have more time.  Maybe that first process should be consume and produce, since they are combining the lots.  I need to double check that they are still doing that.  (I.e. putting all the white alpaca in one pile, etc.)  But in any case, I think that on a pickup, if the provider and receiver agent are different, then the receiver becomes the primaryAccountable (owner in capitalism) on the new resource that is created.  At least that would work for CFN for now.  That is how produce works.  And dropoff is probably the same, and accept/modify, but those won't affect CFN.  Anyway, a todo for me.

When creating an EconomicResource, use the following fields:

* name: use the ResourceSpecification name
* accountingQuantity: use the event resourceQuantity
* stage: if it is output of a Process, use the ProcessSpecification of the Process
* primaryAccountable: the receiver on the event determines that, so it will basically always be CFN (until we get to the last transfer, from CFN to the designers, which is the one in the Satisfy Request column, but we can wait on that until later, I don't think we have the UI for it anyhow)
* conformsTo: the ResourceSpecification on the resoureConformsTo on the event

When updating an EconomicResource, use:

* accountingQuantity: see the action chart; or: if produce, increment the resourceQuantity, if Consume, decrement the resourceQuantity, if transfer, decrement the resourceInventoriedAs.resourceQuantity, increment the toResourceInventoriedAs.resourceQuantity (but we're not worrying about transfer yet, that won't matter until the yarn goes to the designers at the end of season)
* stage: if it is output of a Process, use the ProcessSpecification of the Process
