# Additions to the planning page

![planning-update(1)](https://github.com/user-attachments/assets/e30b5649-2682-4087-b159-3afe8d67c72f)

## Ability to edit and delete cost

Really, ability to edit the reciprocal commitment, and also add events. 

UI change: If we can fairly easily create a backwards arrow shape for the "cost" payment commitment info, that would be best from a user conceptual point of view.  (Raphael can probably do it if you prefer, Leo.)  It would always show up below the main production commitment, and move with it if they move the main commitment.

Alternative UI change shown also above, except picture it as one big shape, the normal one, just with more lines so it gets fatter.  (Too hard to mock up.)

So one of those choices would replace the "cost" line in the UI.  Then we would add the ability to edit or delete that commitment.  If delete, then delete the agreement too.  To edit, bring up a Edit Commitment modal just like with main commitments.

## Add unplanned event (process-related)

Put an event icon next to the + on the top of each process input and output columns. (no white background) Use that for a modal with all event info we generally have in an add event modal (except the "finish commitment" checkbox), all will need to be editable.  If possible, limit actions to process inputs and outputs [(see chart)](https://www.valueflo.ws/concepts/actions/#behaviors-by-action).  Save the event with the right inputOf or outputOf based on where they selected it.

We'll also need to display it at the bottom of the column after it is saved, more-or-less same format as the commitment.  Make it green.  It will need to be editable and deletable, but they don't need to move it up and down, and it wouldn't have the "add event" icon inside the shape.  For now, we can ignore the "cost" feature, although it does make sense to have it eventually, just really really low priority.
