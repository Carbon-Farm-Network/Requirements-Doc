# Updates post Phase 2

These handle the requirements for being able to create a cost commitment for a different quantity than the offer, handling inputs that show up in the middle of the plan sequence, both at planning and after planning as the season progresses, recording events that weren't planned, showing existing inventory on the plan.

Since we don't have validations for required fields, we can leave these all open, and catch that along with all the required fields as a separate issue later.

## Planning page: provide more input fields when creating or updating the "cost"

### Commitment

In addition to the Save cost checkbox (or instead of it??), create a separate section in the modal for data for the reciprocal commitment.  This should include:
* Payment quantity (default from the offer if there is one) - amount (total), unit (format like the others, if no offer default USD or whatever we are doing in offers, but we should not allow blank unit if there is a quantity)
* Description

If entered, save the agreement and reciprocal commitment as currently done.  Could be update or create on the agreement and/or the reciprocal commitment, depending on what is already there.

### Event

On add event in the plan page, if the commitment is also part of an agreement (i.e. is showing the cost $), then also allow more info for an event for that reciprocal commitment.  Create a separate section in the create event modal.  This should include:
* Payment quantity (default from the commitment if it exists) - amount (total), unit (format like the others, if no offer default USD or whatever we are doing in offers in the PER section, but we should not allow blank unit if there is a quantity)
* Tracking identifier (for check numbers, etc.)
* Description

If entered, save the reciprocal event and fulfilment for the reciprocal commitment. Both events should also reference the agreement. (I think these aren't currently being saved, at least they are not on the event list.)  We don't have to worry about creating or updating resources for now, until we get to maintaining a bank account(s).

## Add a non-process commitment to a plan

From Laura: "We have 400lbs of clean white wool at the spinning mill (Kraemer) and we are also marrying up the fiber we are delivering to the scouring mill (Bainton) with 150lbs of Brown alpaca, 270 white alpaca and 40 lbs of black alpaca that is already at Bainton.  We'll probably leave the extra wool and alpaca at Kraemer to add to our batch next year."

For now, let's see if we can do this with the stage, and not bring location into the picture unless we need to.  Also we can limit it to this requirement, not knowing what else might fit in later.  I don't know of a way to use an implied transfer in this case, because the quantity will be different, and shouldn't be split up between different process inputs.  So we'll need a real transfer.

To do:
1. Add an Add icon (+ with circle) below each process spec column, below the output side.
   ![add-commitment](https://github.com/Carbon-Farm-Network/Requirements-Doc/assets/3776081/a1479580-b1fe-48e9-8e96-5032464a7a8d)

2. When clicked, bring up a modal to add a commitment.  For now, let's just make it a transfer.  It can be just like the Add Satisfy Request modal, with the addition of the cost information as above.
![Screenshot from 2024-07-01 14-35-00](https://github.com/Carbon-Farm-Network/Requirements-Doc/assets/3776081/4f9ac265-fb88-4da5-9759-a3614f1e022d)

3. Save it.  If the cost info is included, create an agreement, commitment and reciprocal commitment, like what is done now for commitments part of the original plan.  Include Commitment.plannedWithin (the Plan), since there is no process.  Include the Commitment.stage (the ProcessSpecification of the column), as this will help us get it back to the same spot in the UI.  (If you have other ideas, or think this won't work, let me know.)  Include the cost info in the total cost.

4. When it gets displayed, let's try just putting the commitment shape under the new add icon, without any background color.  It doesn't need the up/down arrows to change the order, but can have the others afaict.

5. I think the event icon can work the same as it does on any commitment.  Let me know if I missed something there.

## Upgrade format of event list

There will be events that are part of an agreement, and events without an agreement.  Let's figure out how to best display this.  I'm thinking that we keep the events part of the same agreement together, even could be just without the space that is between events now.

## Ability to add events on event list page

1. Add a button for Add, similar to other pages.

2. Bring up a modal to add an event, similar t
