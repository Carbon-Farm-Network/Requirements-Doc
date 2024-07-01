# Updates post Phase 2

These handle the requirements for being able to create a cost commitment for a different quantity than the offer, handling inputs that show up in the middle of the plan sequence, both at planning and after planning as the season progresses, recording events that weren't planned, showing existing inventory on the plan.

## Planning page: provide more input fields when creating or updating the "cost" agreement

### Commitment

In addition to the Save cost checkbox (or instead of it??), create a separate section in the modal for data for the reciprocal commitment.  This should include:
* Payment quantity (default from the offer if there is one) - amount, unit (format like the others, if no offer default USD or whatever we are doing in offers, but we should not allow blank unit if there is a quantity) - required
* Description - optional

If entered, save the agreement and reciprocal commitment as currently done.

### Event

On add event in the plan page, if the commitment is also part of an agreement (i.e. is showing the cost $), then also allow more info for an event for that reciprocal commitment.  Create a separate section in the create event modal.  This should include:
* Payment quantity (default from the commitment if it exists) - amount, unit (ormat like the others, if no offer default USD or whatever we are doing in offers, but we should not allow blank unit if there is a quantity) - required
* Tracking identifier (for check numbers, etc.) - optional
* Description - optional

If entered, save the reciprocal event and fulfilment for the reciprocal commitment. (No need for another agreement.)

## Add a non-process commitment to a plan

From Laura: "We have 400lbs of clean white wool at the spinning mill (Kraemer) and we are also marrying up the fiber we are delivering to the scouring mill (Bainton) with 150lbs of Brown alpaca, 270 white alpaca and 40 lbs of black alpaca that is already at Bainton.  We'll probably leave the extra wool and alpaca at Kraemer to add to our batch next year."

For now, let's see if we can do this with the stage, and not bring location into the picture unless we need to.  Also we can limit it to this requirement, not knowing what else might fit in later.  I don't know of a way to use an implied transfer in this case, because the quantity will be different, and shouldn't be split up between different process inputs.

Steps:
1. Add an Add icon (+ with circle) below each column, below the output side.
2. When clicked, bring up a modal to add a commitment.


