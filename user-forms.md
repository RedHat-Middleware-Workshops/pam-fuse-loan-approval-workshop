# 9. Creating the User Forms

Next we will create User Forms to interact with the human tasks. We will set up one form to start the process and one for the Loan Manager Approval.

1. For this on the Process editor click on the following option and choose `Generate all Forms`.

   ![Generate all forms]({% image_path forms1.png %})

   This will create a form with all possible values, we will now edit these forms to make sure we have the right fields.

2. Go Back to the Asset Library view and filter by Forms. You should now see 3 forms generated.

   [![image 2020 09 01 16 56 47 564]({% image_path image/image-2020-09-01-16-56-47-564.png %})]

3. Now open up the Form com_myspace_loan_approval_LoanApplicant

   You can see the various fields possible for an `LoanApplicant`. Let us remove the field `Loan Pre Qualification`, `Loan Qualification` and `LoanGroupAssignment` by clicking on the three dots on the right side of the field. You can also rearrange the fields as you see fit.

   ![User Form ]({% image_path forms2.png %})

   Save the changes.

   Finally let us open up the User Task Form - `Task-taskform` and make sure the fields look up. Remove the field name `CustomerClass`, this will come from the service lookup.

4. Now we are ready to build and deploy the changes. Go back to the asset library and click on *Deploy*. (The Deploy action Builds & Deploys the changes).