# 2. Users and Groups

In order to demonstrate the assignment and reassignment features, we will set up 3 sample groups and some users. First, login to Business Central using the credentials provided.On the top right you will see an option for the settings view.

![add asset]({% image_path add_asset.jpg %})


1. Now click on the option for `Users`

2. We will create 4 users. For creating a new user, click on the `New User` option.

   [![new user]({% image_path new-user1.png %})](https://github.com/kmacedovarela/pam-fuse-loan-approval-workshop/blob/master/image/image-2020-08-31-15-59-38-519.png %})

3. Proceed with the wizard. Enter the username as `Mary`, then proceed on to add role to user as below.

   ![New User]({% image_path  new-user2.png %})

   

   ![New Role]({% image_path new-role1.png %})

4. Now choose, the role as `user`.

   ![Associate Role and User]({% image_path associate-role-user.png %})

5. Now click on the `Create` button.

6. Finally set the password `redhatpam1!` for the user.

   ![Set Password]({% image_path set-user-psswd.png %})

7. Let us now repeat the same process to create 3 more users.

   | Username | Password    |
   | -------- | ----------- |
   | Robert   | redhatpam1! |
   | Patricia | redhatpam1! |
   | John     | redhatpam1! |

   Finally you should see the following users.

   ![image 2020 09 01 08 01 51 864]({% image_path all-users.png %})

8. Now let us create 3 groups. For this click on the groups tab as shown in the image.

   ![Add Group]({% image_path add-group.png %})

9. Click on the `New Group` option. Provide a name for the group `seniorUserAgent.

   [![image 2020 09 01 08 04 32 270]({% image_path image-2020-09-01-08-04-32-270.png %})

10. Now you should see the list of users, show up. Choose the user `John` and click on `Add Selected User`.

    ![Add Users to Group]({% image_path add-group2.png %})

11. Repeat the same process to create two more groups.

    | Group Name       | Users        |
    | ---------------- | ------------ |
    | nonResidentGroup | Patricia     |
    | loanAgent        | Mary, Robert |

12. Finally you should see the following groups.

    ![Group list]({% image_path all-groups.png %})

-----

Now that we have the users and groups properly configured, let's start by creating a new project.