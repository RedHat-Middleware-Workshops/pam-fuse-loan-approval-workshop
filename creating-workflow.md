# 8. Creating the Loan Approval Workflow

Now that we have created all necessary pieces, we will now define the process. We will be building the following process flow.

![Workflow]({% image_path complete-workflow.png %})

1. Since, we will be invoking a REST service from our business process, we will first need to enable the corresponding Service task to give us that capability. For this, go to the library view, and open up the option for `Settings`.

   ![Custom Task]({% image_path wf-custom-task.png %})

   Leave the Username/password blank as our service is not secured with authentication.

2. Go back to the asse library and click on the *Add Asset* button and choose the *Business Process* type.

   ![New Process]({% image_path wf-new-process.png %})

3. When the process designer opens, click on the properties pane to open it up.

   ![Process Editor]({% image_path wf-process-editor.png %})

4. Scroll down in the property panel on the right side of the screen, until you see the section *Process Data*.

5. Expand the *Process Data* section and add the following *Process Variable* by clicking on the *+* sign.

   ![Process Variables]({% image_path wf-process-variables.png %})

6. Next let us define the steps one by one. First drag drop the start node from the left side pane.

   ![Start event]({% image_path wf-start-event.png %})

7. We will now create the task to invoke the REST service we created. For this open up the palette from the left.

   ![Rest Task]({% image_path wf-rest-task.png %})

   Drag and drop the component on the canvas. We will now define the properties, for this click on the hidden property pane on the right.

   ![Rest Task 2]({% image_path wf-rest-task2.png %})

   We will define the `Name` as`Lookup Customer Profile`. Click on the `Data Assignments` section to open it up. Click on the pencil icon to open up details.

   ![Rest Task Config]({% image_path wf-rest-task3.png %})

   In the input section, We will define the Method as `GET` and the Url as `http://localhost:8087/camel-rest/lookup/#{loanApplicant.customerId}` We will leave all other input fields blank. We will map the output Result to the `customerClass` variable that we created earlier.

   ![Rest Task Parameteres]({% image_path wf-rest-task4.png %})

8. We will now define an alternate path for PLATINUM customers. We will by pass the approval process. For this we will add a gateway that checks for the customer class and skip execution.

   ![Gateway]({% image_path wf-gateway1.png %})Now let us add a Script task so that we can mark the execution as complete. For this open up the palette from the left and choose the task type as below.

   ![Script Task]({% image_path wf-script.png %})We will name this task `Auto Approve`, open up the Implementation/Execution section and add the Script value as below,

   ```
kcontext.setVariable("loanApplicant.loanQualification",true);
   ```

   [![Script Task 2]({% image_path wf-script2.png %})]
   
   Finally we will define a end node to end this part of the flow.

   [![End Event]({% image_path wf-end-event.png %})]

   Now we will connect all of these nodes using arrows. To connect any node click on the node and choose the context help displayed around the node to choose the arrow.

   [![New association]({% image_path wf-link.png %})]

   The process should look like this.

   [![Workflow First Version]({% image_path wf-v1.png %})]

9. Next we will define the *Loan Pre-Qualification* node. For this we will need to choose the *Business Rule* node. Click on the left side process palette on the Task(Rectangle) option and drag drop the node on to the canvas.

   [![Business Rule Task]({% image_path wf-rules.png %})]

   Now click on the node and edit the properties on the right side pane. We will give it a name and rule flow group as below.

   [![Rules task Properties]({% image_path wf-rules2.png %})]

   Next we will define the Inputs/Ouputs for the Rule. For this scroll down to the *Data Assignments* section and click on the Assignments. We will map the `loanApplicant` as input and the `loanApplicant` as output.

   [![Rules Task Data Assignments]({% image_path wf-rules3.png %})]

   Next connect the nodes as below.

   [![Connect Business Rule Node]({% image_path wf-v2.png %})]

10. Now click on the gateway, and define the default path as below.

    [![Gateway selection]({% image_path wf-gateway3.png %})]

    We will also define the path for the Auto approval. For this click on the arrow that connects the gateway to the Auto Approve task. On the Implementation/Execution section, define the condition for filtering PLATINUM customers.

    [![Gateway conditions]({% image_path wf-gateway4.png %})]

11. Next we need to define a gateway to filter only applicants with succesful Pre Qualification check. Click on the Rhombus from the process palette(on the left) and choose the Exclusive.

    [![Exclusive Gateway]({% image_path wf-gateway5.png %})]

12. Next we will need to invoke the Loan Group Assignment. For this click on the *Task* node from the process palette(on the left) and choose the *Business Rule* node.

    We will edit the name and add the Rule Flow group as below.

    [![Business Rule Group Assignment]({% image_path wf-rules4.png %})]

    We will add the Assignment as we did in the previous step with the following definition.

    [![Business Rule Task inputs and outputs]({% image_path wf-rules5.png %})]

13. We will also choose the Red circle from the process palette(on the left) and choose the *End* event. Now we will connect the arrows between the *Loan PreQualification*, gateway and the *Group Assignment* as below.

    [![End Node]({% image_path wf-end-event2.png %})]

    We will also need to define the logic for the gateway, for this click on the arrow to the *Group Assignment* and expand the *Implementation/Execution* section. Here we will define the logic as below.

    [![Gateway path]({% image_path wf-gateway6.png %})]

    We will define the default path for the gateway as End, as below.

    [![Default route]({% image_path wf-gateway7.png %})]

14. Last we will define a human task for the Loan Manager approval. For this click on the *Task* node from the process palette(on the left) and click on the *User* task. Drag drop the node on to the canvas.

    We will edit the name and add the *Groups*. Add the value as

    ```
    #{loanApplicant.loanGroupAssignment}
    ```

    [![Groups assignment]({% image_path wf-ht1.png %})]

    [![User Task]({% image_path wf-ht2.png %})]

    Next scroll down to the *Assignments* section and add the following assignment.

    [![User Task Data Assignment]({% image_path wf-ht3.png %})]

15. Finally connect the `Loan Approval` task with the end node and connect the arrows.

    [![Worfklow Final]({% image_path wf-v3.png %})]

16. Finally click on *Validate* and it should be succesful.

