# Cash flow report

Create a new page for a yearly list of economic events that involve cash (USD in this case). Implications:  
* We'll want a filter by year, defaulting to the current year's data.
* We have some choices on the "cash" filter.  If we need to save time, we can just hard-code it to USD like we do in certain places in the modals.  Or while we're at it, we can start making this more configurable, for example, adding a "currency" flag to EconomicResource, using that whenever we just want to show currencies, credits, tokens, etc.  We could also provide a filter for economic resources that are currency accounts, for users who have more than one.  (CFN has only one bank account.)  (This will require some more thought. I think we can use the trackingIdentifier for the bank acct number or wallet id, and use the currency (like USD) ResourceSpecification.  But that may be too simplistic, maybe we'll need a currency resource containedIn an account resource, don't know.)
* We might want to provide some minimal "normal" kind of bank reconciliation features.
* We'll have to figure out how to get a beginning balance.
* We'll want to keep a running balance down the page.

Here is their current spreadsheet:

<img width="1732" height="417" alt="cfn-cash-flow" src="https://github.com/user-attachments/assets/84eeb413-e35c-4b87-a496-c42f18ce921f" />

