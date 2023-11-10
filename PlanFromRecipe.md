# Plan from Recipe 

## Attach UI to hREA

### Bring in offers and requests to Planning page

The first column is offers, the last column is requests.  Bring those from hREA, basically the same logic as the offers list and the requests list.  Bring in only if `finished` is false.  (Or if they are being saved without a value, then check not = true.  But hopefully they are saved with the default value false when created.)

### Make Save Plan work

There's a button Save Plan on the planning page, with a modal when clicked, including name and note.  If they Save, then create a `Plan` in hREA.  (There will be more later in that save.)

### Hook up Plans page

There is a new page with a list of Plans.  Make that show the saved Plans.  (Edit and Delete need to wait until later.)
