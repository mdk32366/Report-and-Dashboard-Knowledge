# Report-and-Dashboard-Knowledge
Capturing bacon-saving ideas that can be leveraged into other bacon-saving ideas

### Formula Debugging Tips
1.  For long formulas that don't pass validation, start small, validate, add more, validate.  This way you can isolate exactly where the error springs from.

### Ultimate Parent Account Field
You can create a custom field which will place all children accounts no matter how far down under the top-level of account or campaign using the Blankvalue operator.

### Activity Reports (What objects are users logging their activities against.  Standard activity report only allows you to report activities object by object)

[Standard Field ID Decoder](https://help.salesforce.com/articleView?id=000325244&language=en_US&type=1&mode=1)
[Standard Object ID Decoder](http://salesforcegenius.com/salesforce-object-id-prefixes-decoder-cereal-box-decoder-ring-salesforce-ids/)

This is placed against the "Related To" field in actvities:

Formula: CASE(
           LEFT(WhatId, 3),
           "001","Account",
           "500","Case",
           "006","Opportunity",
           "xxx","Custom Object Here",
           "Other"

### Custom Time Slices for Opportunities (Standard report doesn't allow for much flexibility on time slicing.  You can create formulas that will do this for you without creating complex filters)

Formula against CloseDate: You'll need to create custom fields on Opportunity using variations on these Formulas, and then call them up in the standard Opportunity Summary Report.  Use the custom field to group, or as a column.

#### Month by Month (February)

If(
  MONTH(CloseDate) = 2,
  Amount,
  0
  )
  
  #### Quarterly (Q4)
  
  If(
    Month(CloseDate) >= 10,
    Amount,
    0
    )
