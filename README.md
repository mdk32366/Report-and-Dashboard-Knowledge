# Report-and-Dashboard-Knowledge
Capturing bacon-saving ideas that can be leveraged into other bacon-saving ideas

[Formulas and Operators](https://help.salesforce.com/articleView?id=customize_functions.htm&type=5)

### Formula Debugging Tips
1.  For long formulas that don't pass validation, start small, validate, add more, validate.  This way you can isolate exactly where the error springs from.

### Ultimate Parent Account Field
You can create a custom field which will place all children accounts no matter how far down under the top-level of account or campaign using the Blankvalue operator.

Standard Parent Account Field or Campaign Field only goes up one level.  You can use this formula to return either a blank value if there is no Parent, or it will nest all the children and subchildren below the 'Ultimate' Parent Account/Campaign.

This is used with the Opportunity Pipeline Report so that all opportunties under the Ultimate Parent end up nested and summarized beneath it.

Create a new custom field, formula type, with the following (up to 10 levels allowed)

Call it "Ultimate Parent Acccount" on the Account (or Campaign) Object which will return the Top Parent Account in the hierarchy no matter where in the hierarchy the current Account/Campaign is, even if there is NO account or campaign hierarchy.

BLANKVALUE is the key.  Determines if an expression has a value and returns a substitute expression if it does not. If the expression has a value, returns the value of the expression.  Usage BLANKVALUE(Department, “Undesignated”) - If Department is blank, it supplies "Undesignated" as the value.

To make sure your formula takes in enough levels of parents, use the 'Insert Field' function to click on 'Parent Account' going up enough levels until you reach the top level account and then use the Insert button to grab that level.

Formula field on Account (or Campaign): "Ulimate Parent Account" (Add it to the Layout)

    BLANKVALUE(Parent.Parent.Parent.Parent.Parent.Parent.Name,
    BLANKVALUE(Parent.Parent.Parent.Parent.Parent.Name,
    BLANKVALUE(Parent.Parent.Parent.Parent.Name,
    BLANKVALUE(Parent.Parent.Parent.Name,
    BLANKVALUE(Parent.Parent.Name,
    BLANKVALUE(Parent.Name,
    Name))))))

Now you can use this field in every standard report.  Use 'Ultimate Parent' as the Grouping field.

### Activity Reports (What objects are users logging their activities against.  Standard activity report only allows you to report activities object by object)

[Standard Field ID Decoder](https://help.salesforce.com/articleView?id=000325244&language=en_US&type=1&mode=1)

[Standard Object ID Decoder](http://salesforcegenius.com/salesforce-object-id-prefixes-decoder-cereal-box-decoder-ring-salesforce-ids/)

This is placed against the "Related To" field in actvities:

Formula: 

    CASE(
       LEFT(WhatId, 3),
       "001","Account",
       "500","Case",
       "006","Opportunity",
       "xxx","Custom Object Here",
       "Other"
       )


### Custom Time Slices for Opportunities (Standard report doesn't allow for much flexibility on time slicing.  You can create formulas that will do this for you without creating complex filters)

Formula against CloseDate: You'll need to create custom fields on Opportunity using variations on these Formulas, and then call them up in the standard Opportunity Summary Report.  Use the custom field to group, or as a column.  Reusable.  You can get a Summary report that looks like a Matrix Report.

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

### Counts of Open & Lost Opportunities

Opportunity Object has fields that count whether an Opp is closed (IsClosed) or won (IsWon), but not 'Open' or 'Lost'.  Open would be Opps that are Not(IsClosed) and Not(IsWon).  Lost would be Opps that are IsClosed and Not(IsWon).  This gives BDMs and Inside sales people an idea of what is open, or what the customer attrition rate is (IsClosed and Not(IsWon)(Use this with Opportunties with Clients).

Use the Opportunity Pipeline Report

Create two formula fields on Opportunity custom fields:

Open Custom Field:
Datatype: Formula
Return Type: Checkbox
Formula:

    IsClosed = FALSE

or

    NOT(IsClosed)

Lost Custom Field:
Datatype: Formula
Return Type: Checkbox
Formula:

    AND(IsClosed = TRUE,
      IsWon = FALSE)
      
 Or

    And(IsClosed,
     NOT(IsWon))
     
Stores a zero or a one in the field.  

Use a SUM column and use these two new fields in the Opportunity Pipeline Reports.  You can also create new ratios for loss percentage, etc  Use a Custom Summary Formula Column in the OPR.  [Custom Summary Formula Field](https://help.salesforce.com/articleView?id=building_custom_summary_formulas.htm&type=5).

### Custom Buckets
[Bucket Fields](https://help.salesforce.com/articleView?id=reports_bucketing_overview.htm&type=5)

Standard Salesforce Buckets: Numeric, Picklist, Text.  No need for a custom formula.
Issue: With C-Level and Sales Manager Level type reporting, when someone new comes in and wants reports differently, you have to change a bunch of reports.

Solution:  Bucket field custom field on the Opportunity Object.  New person, new criteria, just change the formula in the custom field.

    IF(
        Amount > 100000,
        "Large Account"
        IF(
            Amount > 50000,
            "Standard Account"
          )
      )
  
  ### Custom Report Types
  
  Good example is an Activity Report that reports Activities across all Standard Objects.  Standard reports give you an activity report per standard object.
  
  



