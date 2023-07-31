# Order from Offer

This gives a way to create an order (an Agreement with 2 Commitments, one for the resource ordered, one for the payment). It is unclear where this will originate from.  One possibility is a mockup of the planning page.  Another is the offer list.  In either case, it will be a button next to the offer, which will bring up a modal for the order.  When saved (or cancelled), for now it can just go back to the screen where it was clicked.

## hREA

To start with, just a create mutation for each Commitment, and one for the Agreement.  I believe these exist.

## UI

**On the screen:**

![cfn-order-spec](https://github.com/Carbon-Farm-Network/Requirements-Doc/assets/3776081/15bc9aa5-9ded-467e-85a6-8605c7e3d4ce)

Pre-filled and not editable, taken from the offer:
* Provider
* Action
* Resource spec
* Unit
* Currency

Pre-filled and editable:
* Ordered quantity (use the offer's available quantity)
* Payment quantity (multiply the ordered quantity by the offer's price)

On the screen, when the ordered quantity is changed, re-multiple by the price and put in a new payment quantity.  They can then override the payment quantity if they want.

**Fields saved:**


### Hooking up UI and hREA

Graphql example:

```
