# Order from Offer

This gives a way to create an order (an Agreement with 2 Commitments, one for the resource ordered, one for the payment). It is unclear where this will originate from.  One possibility is a mockup of the planning page.  Another is the offer list.  In either case, it will be a button next to the offer, which will bring up a modal for the order.  When saved (or cancelled), for now it can just go back to the screen where it was clicked.

## hREA

To start with, just a create mutation for each Commitment, and one for the Agreement.  I believe these exist.

## UI

The order will pre-fill some information from the offer.

**On the screen:**



**Fields saved:**


### Hooking up UI and hREA

Graphql example:

```
