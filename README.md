# ev-userManagement

This add-on is a great thing that allows you to reset passwords for users who forgot owns password without contacting Administrator.

  Features :-
	
    1. Limiting the number of users - you can limit the number of users.

    2. Forgot password - User can now reset their password from the login page. They need to enter their username after which a mail will be shot to the user's registered email id which contains the link to reset the password. This feature will only work when two things are there in the system.
	A template that is required for the email. This template will be copied automatically when a new tenant is created through self-server tenant account but for tenants created manually these needs to be copied manually.
	A workflow definition - When a user initiate a reset password request a workflow is initiated. This workflow requires a definition which is not deployed in the existing tenants but is deployed when a new tenant is created. So this also needs to be done manually for the existing tenants.

    3. Password autogeneration - admin doesn't need to provide a password while creating user. User will get an autogenerated password in email notification.

    4. Email for new user creation - Earlier creating a new user would shoot mail only if the user is getting generated through bulk upload but now even a manual creation of user will shoot a mail and more so the admin doesn't need to provide password as that will be autogenerated.

    5. Mail when the password is changed - Mail will be delivered to the user if the user changes the password or admin changes the password.

    6. New password policy - password policy is "password must have at least 8 characters, one uppercase, one lowercase, one integer number and one special character(~!@#$%*-_)."

    7. Reset password link will be expired after 24 hours.

    8. It works fine even if multitenancy feature is enabled.

	
  Build steps :-

    1. Clone project

	$ git clone https://github.com/monicakumari/ev-OpenSource-AddOn.git

    2. Compile repo amp

	$ cd project-code/ev-resetPassword-repo/

	$ mvn clean package

    3. Compile share amp

	$ cd ../ev-resetPassword-share/

	$ mvn clean package


   How to deploy add-on :-

    1. Compile AMPs for alfresco and share how described above.
    2. Stop Alfresco.
    3. Add the following property in alfresco-global.properties file. which resides in ${Alfresco_HOME}/tomcat/shared/classes/
	
	### Default number of users allowed ###
	max.number.of.users=5,yyy.com=6,zzz.com=7
       
       default number of users is 5. you can set any number. 6 and 7 are the default number of users are set for the tenants.

    3. Copy file project-code/ev-resetPassword-repo/target/reset-password-repo.amp into ${Alfresco_HOME}/amps folder
    4. Copy file project-code/ev-resetPassword-share/target/reset-password-share.amp into ${Alfresco_HOME}/amps_share folder
    5. Apply AMPs by executing command from command line :

	$ cd ${Alfresco_HOME}/bin
	$ apply_amps.sh -force

    6. Start Alfresco.


reference : https://github.com/FlexSolution/AlfrescoResetPassword
