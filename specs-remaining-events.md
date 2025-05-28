# Remaining event features for season in process

I think these are in priority order.

## Event fulfilling multiple commitments

This came up around payments for multiple fiber resource specs on pick up.  It will also solve current awkwardness with the services. This is a fairly normal feature, basically line items on an invoice.  This integrates the exchanges better with the production plan.

One possible UX follows, other ideas welcome!!

#### Present modal

User selects create event icon on a commitment.  On the way into the modal, we query to bring up a separate list of unfinished commitments with the the same provider, receiver, resource spec, and action as the one chosen. For each of them, also bring up the resource spec of the other commitment connected (?). Default everything as it is now. If there are other possible commitments that can be included, format them onto the modal (at the top? by the quantity?), a list with a checkbox, something like 
```
Fulfill at the same time:
[ ] 345 USD for White Alpaca Dirty
[ ] 456 USD for Gray Alpaca Dirty
```
(If it is too much to include the resource spec of the opposing commitment, like the fiber, we can leave that off and see if it is enough. I would actually be fine with leaving it off, then the feature is more universal, i.e. not just reciprocal commitments.)

#### Choose commitments

The current parts of the modal work as now.  If they check one of those new checkboxes, add that quantity on to what is in the quantity already.

#### Save

Save the one event, fulfilling all of the chosen commitments.  

If finished is chosen, update the finished flag on all of the chosen commitments and change the color on all to green.  If finished is not chosen, change color of all to yellow. If we are now showing number of events on the reciprocal commitments (can't remember), then show one event on each of the commitments fulfilled. (If that is some work, we can skip for now.)

## Non-production planned events

Minimal implementation to start with.  

On the Exchanges page, add a link to be able to fulfill each of the commitments on an exchange.  Might take a little thought to make it understandable along with the Edit and Delete.  Could be Fulfill or could be the icon I suppose.

I think the modal can be the same as the one on the planning page for adding events.  They can do it multiple times from the list page if they need multiple events.

After saving, the event can just appear on the events list, which I think it automatically would.  Later we can think about how to best show the commitments and events as related.

## Event corrections

On the event list (Activities), add an option for each event "Correct"

**Bring up a modal** to add an event, basically like the existing one except they can't change provider, receiver, action, resource spec.  The title could be something like Correct Economic Event. We need to allow negative quantities on this one.  Or if we are really nice, we could bring up the original quantity and let them just make that the correct quantity, and save the difference in the new event.  If we do that, the label could be "Corrected quantity" or something similar.

**Save the event**. Include the reference to the corrected event in the `corrects` field. (Hopefully that field is in hREA, if not, we'll have to add it.  If it makes sense to add both directions, the other direction would be `correctedBy` and it could be a "many".  I.e. an event can correct 1 event; and event can be corrected by 0 to many events.) Also include  other fields from the original event: inputTo or OutputOf a process, fulfills a commitment(s) or satisfies an intent(s), realizationOf or reciprocalRealizationOf and agreement, resourceInventoriedAs and/or toResourceInventoriedAs.

(At some point, we should figure out how to best display these, at least a way to see that one event corrected another on the event list.  And eventually, where in the app to show as 1 totaled event and where to show as >1 event.  But not critical at this moment, it will just show up on the list.)

## Unplanned production events

Minimal implementation to start with.

On the planning page, next to the + used to create a new input or output commitment on a process, add one of those event icons.  (The arrows for replanning can stay on the outsides of those.)

When they select the new icon, bring up a record event modal, with all fields opened up, no defaults, and without the finish commitment. 

When they save it, connect it to the process with inputOf or outputOf, without any commitment involved.

(Later, we'll want to get it displayed on the plan probably, but it shouldn't matter right now, and it will be infrequently used if ever, for this network.  But we need it just in case.  It will show up on the event list.)
