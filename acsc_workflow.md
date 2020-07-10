# Setup instructions for ACSC Advisory Workflow

In order to successfully run this workflow, several configuration steps need to be accomplished.

## Step 1. Set up Webex Teams Target.

In order to send notifications via Webex Teams, the target needs to be configured to reach it's API. In SecureX Orchestration, go to Targets in the left hand side menu, select New Target, and apply configuration according to the screenshot below.

> **Make sure the display name of the target matches exactly (Webex_Teams_Target).**

![](/assets/webex_teams_target.png)

> If you don't want to use Send Webex Teams Message activity inside the workflow, you can always disable it once you import the workflow. To do that, click on the activity, and choose **Skip activity execution** in the configuration panel on the right.

![](/assets/skip_activity.png)

## Step 2. Create Webex Teams Room for notifications.

> This workflow is meant to be run on regular basis, so it is assumed that Webex Teams Room for notifications will be created in advance.

Create Teams Room and add all necessary people. SXO will need to know the Room ID in order to send notifications. The easiest way to find it out - add `roomid@webex.bot` to your room and it will reply to you with the private message containing the room id.

RoomID bot is developed by Cisco to assist Developers with obtaining Room ID information.

1. Add Bot to your room:

![](/assets/add_roomid_bot.png)

2. The bot will send you the Room ID in a private message:

![](/assets/room_id.png)

## Step 3. Obtain Webex Teams API Token.

In order to send the Webex Teams messages, you have two options:
  - **Option 1 (For tests only):** Use your own Webex Teams API token that will need to be updated manually every 12 hours.
  - **Option 2 (Recommended for production):** Use Webes Teams Bot to send messages.
      - Create Webex Teams Bot following these instructions: [Create a Bot](https://developer.webex.com/docs/bots)
      - Record its API Token
      - Add Bot to the Webex Teams Room so that it can send notifications.

## Step 4. Set up Email Target.

In order to send email notifications, the SMTP endpoint need to be configured. Since SXO is a cloud based solutions, the SMTP server has to be reachable via the internet. In our example, we have created a test Gmail account and configures Gmail SMTP target.

![](/assets/email_target.png)

To allow Apps access to your Gmail accounts, follow the following Google documentation: 
* [Third-party apps with access to your account](https://support.google.com/accounts/answer/3466521?hl=en#)
* [Sign in with App Passwords](https://support.google.com/accounts/answer/185833?p=app_passwords_sa&hl=en&visit_id=637299908343568038-392387523&rd=1)

You may have noticed, that we configured No Accounts Keys - True inside our Email Target. This is because we will configure Email accounts keys inside our workflow.

## Step 5. Set up Email Accounts Keys.

> If you skip this step, you will be asked to provide Email Account Keys during workflow import.

After you have set up your Email target, configure the following Email Account Keys. Make sure that the Display name matches what is on the picture:

![](/assets/email_account_keys.png)

## Step 6. Import the workflow.

SXO workflow is represented by the file in JSON format, that contains definitions and description of all the activities, targets, variables and atomic workflows that are in use.

The workflow json file is located in this repositorys' `acsc-advisory-workflow` folder. You can either clone repository to your workstation using `git clone` command or simply copy and past the content of it into the workflow import dialog box.

1. In SXO, go to My Workflows -> Import -> Browse. You will be presented with the dialog box.

![](/assets/import_dialog.png)

2. Either paste the content, copied from the json file in this repository, or browse your computer to import the file from cloned repository. Choose "IMPORT AS A NEW WORKFLOW (CLONE)" and click IMPORT.

![](/assets/import_filled.png)

3. You will be presented with the following warning:

![](/assets/import_warning.png)

Don't get scared and click "Updated" :)

4. This is where you will provide your Webex Token:

![](/assets/token_request.png)

Copy your personal Webex API Token or your Bots' API Token into the VALUE field. This is Secure String variable and it will be store securely in the SXO.

5. You should see the new workflow being added to the list:

![](/assets/import_in_progress.png)

Click on the workflow even if it still shows as import in progress.

6. If import was successfule, you should see zero warnings at the top of the workflow canvas.


![](/assets/inside_workflow.png)

## Step 5. Run the workflow

1. To execute the workflow, click RUN at the right top corner in the action pane.

![](/assets/action_pane.png)

2. You will be prompted to provide input information.

![](/assets/input_variables.png)

3. Provide necessary information and click `RUN`.

4.  Observe workflow execution.

As the workflow progresses, you should see activities turning green. Don't be alarmed if some activities turn red, it is expected behaviour.

5. Once execution is complete, examine the Webex Teams Room and Email Inbox for notifications and check if Threat Response Casebook has been created/updated in SecureX Ribbon.

## Next Steps.

This is a demonstration workflow. In production, you would want to run it on certain schedule, suitable for your organization. Refer to the following [Tutorial](https://ciscosecurity-sx-00-integration-workflows.readthedocs-hosted.com/en/latest/orchestration/schedules.html) on creating schedules and triggers to automatically run SXO workflows.