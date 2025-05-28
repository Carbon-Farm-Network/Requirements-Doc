# Remaining event features for season in process

## Event fulfilling multiple commitments

This came up around payments for multiple fiber resource specs on pick up.  It will also solve current awkwardness with the services. This is a fairly normal feature, basically line items on an invoice.  This integrates the exchanges better with the production plan.

One possible UX follows, other ideas welcome!!

### Present modal

User selects create event icon on a commitment.  On the way into the modal, we query to bring up a separate list of unfinished commitments with the the same provider, receiver, resource spec, and action as the one chosen. For each of them, also bring up the resource spec of the other commitment connected (?). Default everything as it is now. If there are other possible commitments that can be included, format them onto the modal (at the top? by the quantity?), a list with a checkbox, something like 
```
Fulfill at the same time:
[ ] 345 USD for White Alpaca Dirty
[ ] 456 USD for Gray Alpaca Dirty
```
(If it is too much to include the resource spec of the opposing commitment, like the fiber, we can leave that off and see if it is enough. I would actually be fine with leaving it off, then the feature is more universal, i.e. not just reciprocal commitments.)

### Choose commitments

The current parts of the modal work as now.  If they check one of those new checkboxes, add that quantity on to what is in the quantity already.

### Save

Save the one event, fulfilling all of the chosen commitments.  

If finished is chosen, update the finished flag on all of the chosen commitments and change the color on all to green.  If finished is not chosen, change color of all to yellow.  If we are now showing number of events on the reciprocal commitments (can't remember), then show one event on each of the commitments fulfilled. (If that is some work, we can skip for now.)




