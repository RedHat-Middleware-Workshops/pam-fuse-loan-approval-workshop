### 10. Process Management and Tracking

1. After the build is succesful, click top menu option and choose *Process Definition*.

2. We can see the Process Defintion listed, now click on the three dots on the right side of the Process `loan-approval-workflow`. Click on *Start*
 ![Process Definitions]({% image_path mgmt-tracking1.png %})

3. This should open up the Process Start Form. Enter the values for the form and proceed.

   ![New process instance]({% image_path mgmt-tracking2.png %})

4. We can now see the Process Instance View load up automatically.

   ![Process Instance View]({% image_path mgmt-tracking3.png %})

   Inspect the Process Summary

5. Click on the Diagram Tab on the Process Instance View.

   ![Process Diagram]({% image_path mgmt-tracking4.png %})

   You can see that the completed steps show up in grey color and the current task in progress shows up with a Red outline.

6. Let us now quickly explore the admin options on the `Process Instances` tab.

   ![New Process Instance]({% image_path image-2020-09-02-07-04-18-323.png %})

   To start with, you can see that there is a `Filter` section on the left. This section lets us manage the filter criteria for this dashboard. The default filter options based on status, SLAs and Process definition are all mentioned here. This perspective also allows you to create a `New Process Instance`. The table shows the content filtered based on the criteria specified.

7. Let us now explore some complex monitoring options. Assuming that, you will need to track SLAs on the process and alert when they breach. For this go back the designer and open up the Process for authoring again.

   ![Process SLA]({% image_path mgmt-tracking5.png %})

   On the authoring perspective, as shown above, let us set an SLA. Save, build and deploy the changes.

   Let us create a new process instance as we did earlier, with the same input data.

   Now go back to the `Manage` perspective and navigate back to the `Process Instance` section. Since, we set the SLA as 2s it will almost immediately go in to the violated state. Let us verify that here. From the left side filter section, select the SLA violation.

   ![SLA Properties]({% image_path mgmt-tracking8.png %})

   You should see that the SLA violation related results loads up on the right hand side.

8. The `Manage` section also provides for a way to define custom queries on the process data. The following diagram shows how you can setup a custom filter.

   ![Filters]({% image_path mgmt-tracking6.png %})

   Now let us go back process which we last created, The task is assigned to a loan agent group dynamically at runtime based on the rules we configured. Let us see which group this assignment has been done for. For this click on the `Tasks` option from the `Manager` menu option.

   ![Tasks]({% image_path mgmt-tracking7.png %})

   You will now see the task management perspective.

   ![Task list]({% image_path mgmt-tracking9.png %})

   Note: if you cant see the tasks on the Task Management Perspective, it is likely that the user logged in does not have the right role. For this open up the file $JBOSS_HOME/standalone/configuration/application-roles.properties and add `Administrators` as a role to the logged in user.

   Open up the task, and navigate to the `Assignments` tab.

   ![Task Assignments]({% image_path mgmt-tracking10.png %})

9. Let us now try to change the rule logic which governs this assignment. Go back in to the `Design` perspective and open up the guided decision table `AgentGroupAssignment`.

   ![Decision Table Rules]({% image_path mgmt-tracking11.png %})

   Make some changes to the second row, so that we assign RESIDENT cases also to the seniorUserAgent. Now save the business rule, build and deploy the changes.

   We will now create another process instance using the very same input test data.

   Now go in to the `Manage` perspective and open up the `Tasks` section. If we inspect the last task created, we can see it has now been assigned to `seniorAgent` instead of `nonResidentGroup`.

   ![User task assignments]({% image_path mgmt-tracking12.png %})

10. Next let us assume that the group of users are overloaded with work, so we want to make sure the tasks are not in pending state for a long time. For this we want to put some controls in such that, if a tasks is not started by a group until `x` mins/hours we want to ressignment to somebody. Let us now move back to the `Design` Perspective and open up the business process.

    On the Process, click on the `Loan Approval` task. On the right side pane, expand the `Implementation/Execution` section. Here click on the `Reassignments` section.

    Click on the `Add` button and provide the reassingment strategy as below.

    ![Reassignment]({% image_path mgmt-tracking13.png %})

    Click on `Ok`, save changes, build and deploy the project. Now navigate back to the `Manage` perspective and create a process one more time with the same test data.

    The process should be created, let us wait a minute and open up the `Task` section on the management perspective.

    ![Task details]({% image_path mgmt-tracking14.png %})

    You can see that the task has been reassigned. Open up the `Logs` tab to see how the reassignment happened.

    ![Task logs]({% image_path mgmt-tracking15.png %})

11. Next let us look at how an admin can manually delegate tasks. Go back to the `Assignment` section. Now enter the `User` to delegate as `adminUser` and click on delegate.

    ![Delegate]({% image_path mgmt-tracking16.png %})

    You can see the task has been reassigned to `adminUser` now. Also check the `Logs` tab to see the audit log of how the reassignment happened.

12. Next let us go back to the `Task` dashboard by following the breadcrumb.

    ![Task list]({% image_path mgmt-tracking17.png %})

    You can see that because of the assignment, the `Actual Owner` for the task has been changed to `adminUser` and the task is now in the `Reserved` state.

    As you can see, the dashboard provides bulk operations on the tasks. This allows us to claim, suspend, start,release tasks.

    ![Bulk operations ]({% image_path mgmt-tracking18.png %})

