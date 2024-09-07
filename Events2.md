# Add create, update to Economic Events page

The page currently lists all events, sorted descending.  Next step, allow edit to certain fields on existing events.  Also allow adding new events, which will be used for events that can't be added on the planning page.  (Events cannot be deleted.)  

## Add columns

What is the easiest?  I'm thinking to add columns for 1) reference to Commitment and 2) reference to Agreement and/or Process, also 3) tracking identifier.  The references we don't have a useful human readable field, so maybe like github commits, take a piece of the hash?  (Trying to keep it as simple as possible.  Alternative could be to structure the page with existing agreements, processes, commitments?)

**9/7/24 edit**: Th commitment and agreement references could be put off until later, if you haven't done it.  If you have, suggest instead of the hash, just say Agreement or Commitment on the link.  Unless you disagree.  Would bring up a read-only view.

## Edit event

Put an edit icon (like the one on commitments on the planning page) on the right of each economic event.  It brings up a modal.  Fields that can be edited: description (note), tracking identifier.  (Will ask about the best way to name that on the UI.)

## Correct event

Put an icon (find one?) .... or do this in edit and if qty is changed, do a - and a + ????  Let's discuss, and I'll ask the CFN.  This is a **lower priority** for now.

## Add event

**Edit: This is only for lone events, without a commitment or agreement or process**

Put a button similar to other "adds" on the page.  Bring up a modal.  Same fields as adding an event elsewhere, plus `trackingIdentifier`, ~~optional reference to the Commitment, optional reference to the Agreement, reciprocal or not.  If we have time, we can autofill from a Commitment; or figure out how to put Commitments on the page~~.

## Add unplanned process-related event

**Edit: Let's do that on the planning pag, not here**

~~Also, we'll want to let them add a process-related event that doesn't have a commitment (wasn't planned).  This is low priority.  If we can add that to the planning page, with an event icon not related to a commitment, but related to a process in a clear way, then we can eliminate this from the event page.~~
