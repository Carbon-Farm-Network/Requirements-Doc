# Add create, update to Economic Events page

The page currently lists all events, sorted descending.  Next step, allow edit to certain fields on existing events.  Also allow adding new events, which will be used for events that can't be added on the planning page.  (Events cannot be deleted.)  

## Add columns

What is the easiest?  I'm thinking to add columns for 1) reference to Commitment and 2) reference to Agreement and/or Process, also 3) tracking identifier.  The references we don't have a useful human readable field, so maybe like github commits, take a piece of the hash?  (Trying to keep it as simple as possible.  Alternative could be to structure the page with existing agreements, processes, commitments?)

## Edit event

Put an edit icon (like the one on commitments on the planning page) on the right of each economic event.  It brings up a modal.  Fields that can be edited: description (note), tracking identifier.  (Will ask about the best way to name that on the UI.)

## Correct event

Put an icon (find one?) .... or do this in edit and if qty is changed, do a - and a + ????  Let's discuss, and I'll ask the CFN.  This is a lower priority for now.

## Add event

Put a button similar to other "adds" on the page.  Bring up a modal.  Same fields as adding an event elsewhere, plus `trackingIdentifier`, optional reference to the Commitment, optional reference to the Agreement, reciprocal or not.  If we have time, we can autofill from a Commitment; or figure out how to put Commitments on the page.

Also, we'll want to let them add a process-related event that doesn't have a commitment (wasn't planned).  Maybe also an optional reference to a Process, pick input or output?
