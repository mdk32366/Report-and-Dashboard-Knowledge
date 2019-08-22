# Report-and-Dashboard-Knowledge
Capturing bacon-saving ideas that can be leveraged into other bacon-saving ideas

## Basic Report Types, Limitations, and How to Use them

There are 3 kinds of reports in salesforce.com

1) Tabular Reports
2) Summary Reports
3) Matrix Reports

Tabular Reports:- These kind of reports are used when the requirement is just to view the data.
Some of the examples are:-

Show me all Open Opportunities
Show me List of all Accounts which do not have any closed opportunity
Show me top 10 Opportunities by revenue
Dashboards can not be created on Tabular Reports :- Salesforce ADM 201 certification question

Summary Reports:- These reports are used when the requirement is to summarize only X Axis. In short if you need to do the sum or calculate the average on even one parameter then summary report is the answer.
Some of the examples are:-

Show sum of all Open Opportunities
Show opportunities sub total bu my Team
Matrix Reports:- These reports are used when the requirement is to summarize both the Axis i.e. when requirement is to group both Rows as well as Columns.
Some of the examples are:-

Show Accounts grouped as Customer or Prospect depending on the opportunity stage
Show monthly performance of salesteam on closing opportunity by Geography for current year
Note:- Charts can not be made on Tabular Reports as no grouping of data is availableThere are 3 kinds of reports in salesforce.com

1) Tabular Reports
2) Summary Reports
3) Matrix Reports

Tabular Reports:- These kind of reports are used when the requirement is just to view the data.
Some of the examples are:

Show me all Open Opportunities
Show me List of all Accounts which do not have any closed opportunity
Show me top 10 Opportunities by revenue

/*Dashboards can not be created on Tabular Reports :- Salesforce ADM 201 certification question*/

Summary Reports:- These reports are used when the requirement is to summarize only X Axis. In short if you need to do the sum or calculate the average on even one parameter then summary report is the answer.
Some of the examples are:-

Show sum of all Open Opportunities
Show opportunities sub total bu my Team
Matrix Reports:- These reports are used when the requirement is to summarize both the Axis i.e. when requirement is to group both Rows as well as Columns.
Some of the examples are:-

Show Accounts grouped as Customer or Prospect depending on the opportunity stage
Show monthly performance of salesteam on closing opportunity by Geography for current year
Note:- Charts can not be made on Tabular Reports as no grouping of data is available

### Joined Reports in Lightning
+ Only available in Enterprise and Unlimited (and Developer)
+ Exception reporting not allowed.  Example: Accounts WITHOUT Activities, Accounts WITHOUT Contacts.

[Joined Report Limitations](https://help.salesforce.com/articleView?id=reports_unavailable_with_joined_reports.htm&type=5)

[Joined Report Examples (Mostly for Classic, but should work now in Lightning)](https://help.salesforce.com/articleView?id=reports_examples_joined.htm&type=5)

## Report Resources

[Reports Overview](https://help.salesforce.com/articleView?id=rd_reports_overview.htm&type=5)

[Formulas and Operators](https://help.salesforce.com/articleView?id=customize_functions.htm&type=5)

[Formulas: How do I . . . ](https://help.salesforce.com/articleView?id=how_do_i.htm&type=5)

[Cross Object Formulas](https://help.salesforce.com/articleView?id=customize_cross_object.htm&type=5)

[Reporting Snapshots](https://help.salesforce.com/articleView?id=data_defining_analytic_snap.htm&type=5)

[Custom Report Types](https://help.salesforce.com/articleView?id=reports_defining_report_types.htm&type=5)

[Subscribing to Reports and Dashboards](https://help.salesforce.com/articleView?id=reports_subscribe_overview.htm&type=5)

[Joined Reports in Lightning!](https://releasenotes.docs.salesforce.com/en-us/summer18/release-notes/rn_rd_joined_reports.htm)

Up to five blocks available.


### Tracking Object/Field History

[Audit Reports](https://success.salesforce.com/answers?id=90630000000gu0BAAQ)

Click Your Name | Setup | Customize and select the object you want to configure.
Click Fields.
Click Set History Tracking.
For accounts, contacts, leads, and opportunities, select the Enable Account History, Enable Contact History, Enable Lead History, or Enable Opportunity Field History checkbox. Deselect the checkbox if you do not want to track any changes. If you deselect the checkbox, the History related list is automatically removed from associated page layouts.
This checkbox is not available for cases, solutions, or contracts because you cannot disable their history tracking. Certain changes, such as case escalation, are always tracked.

When you choose the fields you want to track, Salesforce begins tracking history from that date and time forward. Changes made before that date and time are not included. Note that some case, solution, and contract fields are preselected for history tracking, so changes to those fields are automatically tracked from the time your organization began using Salesforce.
Choose the fields you want tracked.
Click Save.

## Dashboard Resources

[Dashboards(Lightning)](https://help.salesforce.com/articleView?id=dashboards_create_lex.htm&type=5)

### Report Debugging Tips
1. It does not meet the scope or filter criteria of the Report
2. The User does not have at least Read access to it
3. It does not exist


### Formula Debugging Tips
1.  For long formulas that don't pass validation, start small, validate, add more, validate.  This way you can isolate exactly where the error springs from.

### Dashboard Debugging Tips
+  Are the reports in a folder that the target audience can see?
+  What folder is the dashboard in?  Is it in a folder such that it can be accessed by the right audience and not by the wrong audience?
+  If the information in the report is sensitive, is a running user indicated for the report?
+  Use reports with no filters on them, and add the filters you want to the dashboard you create.
+  Make sure you've included all groups and add any summarizations to any of the columns you want to access in the dashboard.  If they aren't there, then you can't access them in the dashboard.
+  Don't forget to add your filters (stage, probability, close date, age . . )
+  For Date filters, use RELATIVE date types (next month, next quarter, next fiscal quarter, this month, etc.)


### Ultimate Parent Account Field (2/7/18)
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

### Activity Reports (What objects are users logging their activities against.  Standard activity report only allows you to report activities object by object)  (3/20/18)

[Standard Field ID Decoder](https://help.salesforce.com/articleView?id=000325244&language=en_US&type=1&mode=1)

[Standard Object ID Decoder](http://salesforcegenius.com/salesforce-object-id-prefixes-decoder-cereal-box-decoder-ring-salesforce-ids/)

Use Tasks and Events type of report.  Grou

This is placed against the "Related To" record in actvities.  On the Activity Object, create a custom field called 'Related To' (Formula, Text)

Formula: 

    CASE(
       LEFT(WhatId, 3),
       "001","Account",
       "500","Case",
       "006","Opportunity",
       "xxx","Custom Object Here",
       "Other"
       )

Use the Activity by User. and you can sum the activities for each user.  Matrix report with a bar chart makes a nice dashboard.

### Custom Time Slices for Opportunities (Standard report doesn't allow for much flexibility on time slicing.  You can create formulas that will do this for you without creating complex filters) (11/2/18)

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

### Counts of Open & Lost Opportunities (11/2/18)

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

### Custom Buckets (1/22/19)
[Bucket Columns](https://help.salesforce.com/articleView?id=reports_bucketing_overview.htm&type=5)

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
  
### Reporting Snapshots
  
Used for looking at the change in multiple fields over time.

1.  Use a standard report. (Tabular or Summary)
2.  Build a custom object. (Allow reports, and select 'deployed')
  Make sure you include 'snapshot' in the name of the object so that you know what the Custom Object is being used for, and the type of fields in the Custom Object have to match the types in your source report.
3. Map the fields from the report to the fields in the target object.
Note: Use 'Execution Time' mapped to name of the record on custom object

Schedule a reporting interval.

Now this can be accessed as a related list on the Custom Object too.






