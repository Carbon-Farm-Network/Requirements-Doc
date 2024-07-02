# Add a non-process commitment to a plan

From Laura: "We have 400lbs of clean white wool at the spinning mill (Kraemer) and we are also marrying up the fiber we are delivering to the scouring mill (Bainton) with 150lbs of Brown alpaca, 270 white alpaca and 40 lbs of black alpaca that is already at Bainton.  We'll probably leave the extra wool and alpaca at Kraemer to add to our batch next year."

Basically this lets them add a transfer commitment in the stage it is needed.

For now, let's see if we can do this with the stage, and not bring location into the picture unless we need to.  Also we can limit it to this requirement, not knowing what else might fit in later.  I don't know of a way to use an implied transfer in this case, because the quantity will be different, and shouldn't be split up between different process inputs.  So we'll need a real transfer.

To do:
1. Add an Add icon (+ with circle) below each process spec column, below the input side.
![add-commitment(1)](https://github.com/Carbon-Farm-Network/Requirements-Doc/assets/3776081/36abf573-1d48-45a9-a94b-1be9405de90a)

2. When clicked, bring up a modal to add a commitment.  For now, let's just make it a transfer.  It can be just like the Add Satisfy Request modal, with the addition of the stage (dropdown of process specifications) if we can't figure it out ourselves.  The stage is the previous column.
![Screenshot from 2024-07-01 14-35-00](https://github.com/Carbon-Farm-Network/Requirements-Doc/assets/3776081/4f9ac265-fb88-4da5-9759-a3614f1e022d)

3. Save it.  If the cost info is included, create an agreement, commitment and reciprocal commitment, like what is done now for commitments part of the original plan.  Include Commitment.plannedWithin (the Plan) for the primary commitment (non-reciprocal), since there is no process.  Include the Commitment.stage (the ProcessSpecification of the previous column - or make them pick?), as this will help us get it back to the same spot in the UI.  Include the cost info in the total cost.  (If you have other ideas, or think this won't work, let me know.)  

4. When it gets displayed, let's try just putting the commitment shape under the new add icon, without any background color.  It doesn't need the up/down arrows to change the order, but can have the others afaict.

5. I think the event icon can work the same as it does on any commitment.  Let me know if I missed something there.
