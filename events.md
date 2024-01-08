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
