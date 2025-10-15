# 💰 Calculating Family Expenses using ServiceNow

## 📘 Overview
**Calculating Family Expenses using ServiceNow** is a workflow-based project built on the ServiceNow platform to automate family expense tracking and management.  
It enables users to record daily expenses, automatically aggregate totals per day, and view linked records with minimal manual effort.
The project leverages **ServiceNow tables, relationships, and business rules** to provide a seamless and scalable financial tracking solution.
KEY FEATURES
- 🧾 **Automated Expense Calculation:** Automatically sums up daily expenses into total family expenses.  
- 🔗 **Table Relationships:** Establishes linkage between *Daily Expenses* and *Family Expenses* tables.  
- ⚙️ **Business Rules:** Updates and synchronizes records dynamically when new expenses are added.  
- 🧠 **Form Customization:** User-friendly interface with read-only and mandatory fields.  
- 🔢 **Auto-Numbering:** Maintains unique record identifiers using Number Maintenance.  
## 🧰 Tech Stack
| Component | Description |
|------------|-------------|
| **ServiceNow** | Development platform for workflow automation |
| **GlideRecord Scripting** | For querying and updating records |
| **Business Rules** | Automates logic on record creation/update |
| **Form Designer** | Customizes user forms and layouts |
## ⚙️ Implementation Steps

### Setting up ServiceNow Instance
### Create a New Update Set
### Create Tables
### Create Relationship
### Add Business Rules
    (function executeRule(current, previous) {
  var FamilyExpenses = new GlideRecord('u_family_expenses');
  FamilyExpenses.addQuery('u_date', current.u_date);
  FamilyExpenses.query();

  if (FamilyExpenses.next()) {
      FamilyExpenses.u_amount += current.u_expense;
      FamilyExpenses.u_expense_details += " > " + current.u_comments + ": Rs." + current.u_expense + "/-";
      FamilyExpenses.update();
  } else {
      var NewFamilyExpenses = new GlideRecord('u_family_expenses');
      NewFamilyExpenses.u_date = current.u_date;
      NewFamilyExpenses.u_amount = current.u_expense;
      NewFamilyExpenses.u_expense_details = " > " + current.u_comments + ": Rs." + current.u_expense + "/-";
      NewFamilyExpenses.insert();
  }
})(current, previous);

📊 Results
Real-time total expense calculation
Automatic data synchronization
Linked record visibility through related lists
Easy data entry via customized forms

🚀 Future Enhancements

Graphical dashboards for visual analysis
Budget limit alerts and notifications
Multi-user login for family members
Exportable monthly expense reports
