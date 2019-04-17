## Package Push labapp documentation

Brief:
This labapp gets installed in partner's LMA/PBO org and can be used to schedule package push upgrades. This is similar in functionality to package push upgrade functionality that is under Setup. It has following features. 
- Can connect to multiple packaging org and schedule package push upgrades right from LMA 
- USers can create custom List views, with 

![Application in action](/images/pushupgrade-labapp-UI.gif)

### Step 0 - Prerequisite
Enable lightning in your LMA org
Make sure my domain is enabled on LMA org and Packaging org 
In partner portal create support ticket to Enable Push Package feature and Push API feature on the packaging org (if either are not already enabled)
Use Chrome browser for following steps

### Step 1 - Set up Trust between LMA and packaging orgs
Note: Following steps needs to be performed in LMA org. Perform following sub steps i.e. from 1.1 to 1.5 for each packaging org you want to connect to.

### Step 1.1 - Create connected app 
From Setup-> Apps, create a new connected app name reflecting package name e.g “pkg1 Connected App”. (You can give any name). 
![Create connected app](/images/create-connectedapp.png.gif)
For Copy-Paste:
Login URL: https://login.salesforce.com

Go to manage and assign profile permission and Select permitted users 
Make sure Permitted users are as selected as "Admin approved users are pre authorized"

Step 1.2 - Create new Auth. Provider for this “pkg1_auth_Provider”. (You can give any name)
From Setup, create new auth provider as shown below. 
Note: Pick Salesforce as auth provider. Copy Consumer Key and Secret from Step 1.1 here
![Create Auth provider](/images/create-connectedapp.png.gif)
For Copy-Paste:
Authorize endpoint URL: https://login.salesforce.com/services/oauth2/authorize
Token endpoint URL: https://login.salesforce.com/services/oauth2/token

Make sure to wait for 10 minutes for above changes to get deployed and propagated

Step 1.3 - Get Callback URL from Step 1.2 
Go to connected app created in Step 1.1 and update as shown 
![Update connected app](/images/update-connectedapp.gif)

Step 1.4 - Create Named Credentials “packagingOrg” (You can give any name)
![Create named credentials](/images/create-named-credentials.gif)
Note: Make sure to set Scope to “refresh_token full”. Also 
Keep your packaging org user credentials (with Admin profile) handy to establish trust.
For Copy-Paste:
URL: https://{mydomain}.my.salesforce.com (replace mydomain with your packaging org's domain name)
Scope: refresh_token full

On save, it should authentication prompt you to authenticate, use your packaging org you want to connect using login credentials and grant access. If you do not get authentication prompt then edit and click save again

Once authenticated with packaging org, Authentication status in above screen should indicate “Authenticated with ….”

Step 1.5 - Edit Named credentials Auth provider 
Edit Auth provider settings and update Create Named Credentials with URL as shown in {mydomain}.my.salesforce.com format. This mydomain is of packaging org. On Authorize packaging org again


### Step 2 - Create/update lookup mapping records i.e. packaging org named credentials with a package record


