# PackagePushDocs
Package Push labapp documentation

Brief:
This labapp gets installed in partner's LMA/PBO org and can be used to schedule package push upgrades. This is similar in functionality to package push upgrade functionality that is under Setup. It has following features. 
- Can connect to multiple packaging org and schedule package push upgrades right from LMA 
- USers can create custom List views, with 

![Application in action](/images/pushupgrade-labapp-UI.gif)


Step 0 - Prerequisite
Enable lightning in your LMA org
Make sure my domain is enabled on LMA org and Packaging org 
In partner portal create support ticket to Enable Push Package feature and Push API feature on the packaging org (if either are not already enabled)
Use Chrome browser for following steps

Step 1 - Set up Trust between LMA and packaging org
Note: All following steps needs to be done in LMA org

Step 1.1 - Create connected app 
From Setup-> Apps, create new connected app named “SF2SF Package Pusher Connected App”. It can be a different name but prefer to use this name for consistency. 
To Copy-Paste:
Login URL: https://login.salesforce.com



Step 1.2 - Create new Auth. Provider “Package_Pusher_Auth_Provider” 
From Setup, create new auth provider as shown below. 
Note: Pick Salesforce as auth provider. Copy Consumer Key and Secret from Step 1.1 here
To Copy-Paste:
Authorize endpoint URL: https://login.salesforce.com/services/oauth2/authorize
Token endpoint URL: https://login.salesforce.com/services/oauth2/token


Please make sure to wait for 10 minutes for above changes to get deployed and propagated

Step 1.3 - Get Callback URL from Step 1.2 
Go to connected app created in Step 1.1 and update as shown 


Step 1.4 - Create Named Credentials with exact name “packagingOrg”
Note: Make sure to set Scope to “refresh_token full”. Please keep your packaging org user credentials (with Admin profile) to establish trust.
To Copy-Paste:
URL: https://login.salesforce.com
Scope: refresh_token full

When you save make sure to authenticate using your packaging org login and grant access. If you do not get authentication prompt then edit and click save again

Once authenticated with packaging org, Authentication status in above screen should indicate “Authenticated with ….”


Step 1.5 - Edit Auth provider 
Edit Auth provider settings and update Create Named Credentials with URL as shown in {mydomain}.my.salesforce.com format. This mydomain is of packaging org. On Authorize packaging org again


