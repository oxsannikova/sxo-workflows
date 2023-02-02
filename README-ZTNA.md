# Applying user Zero Trust policies to Umbrella top blocked identity

## Features
This [workflow](https://github.com/oxsannikova/sxo-workflows/blob/master/sxo-ztna-duo-umbrella/Applying%20user%20ZT%20policies%20to%20Umbrella%20top%20blocked%20identity.json) searches and returns the top 10 identities in Cisco Umbrella with DNS activity blocks for the last 7 days. The data is then parsed and posted in a ServiceNow incident.

**Note:** This workflow is base on the workflow #0041 with added response actions: https://ciscosecurity.github.io/sxo-05-security-workflows/workflows/0041

## Steps

* Get a token for the Umbrella API
* Fetch a list of identities with blocked DNS activity
* Check if the request was successful (if not, end the workflow)
* Extract the result count and check if there were any results (if not, end the workflow)
* Convert the top blocked identities to a table
* For each identity:
  * Fetch blocked domains for the identity provided
  * Format the results for ServiceNow
* Create approval request to block the user
* Create a Webex Message with the list to approve the action
  * If action approved, block the user in Duo
* Create a ServiceNow incident ticket
* Post message to Webex

## Configuration

### Required Targets and Target Groups
**Targets:** ServiceNow, Umbrella API v2 OAuth2, Umbrella API v2, DUO Security

### Required Account Keys
**Accounte Keys**: Umbrella v2

### Required Local Variables
* Update the following local varilables in order to properly authenticate to respective tools.
 
| Variable Name | Value|
|---|:---:|
| Duo Hostname | XXXX.duosecurity.com |
| Duo Integration Key | XXXX |
| Duo Secret Key | ****** |
| ServiceNow Instance URL | XXXX.service-now.com |
| ServiceNow User ID | provide user id here |
| Webex Teams Room ID | XXXXXX |

### Import the workflow

1. In the left pane menu, select **Workflows**. Click on **IMPORT** to import the workflow.

2. Click on **Browse** and copy paste the content of the [Applying user ZT policies to Umbrella top blocked identity](https://github.com/oxsannikova/sxo-workflows/blob/master/sxo-ztna-duo-umbrella/Applying%20user%20ZT%20policies%20to%20Umbrella%20top%20blocked%20identity.json) file inside of the text window.  Select **IMPORT AS A NEW WORKFLOW (CLONE)** and click on **IMPORT**.

3. Go to **My Workflows** and open the workflow **Applying user ZT policies to Umbrella top blocked identity** and validate it. In the properties on the right hand-side, find section **Triggers**. You will see that the status is **Disabled**. Click on the name of the Trigger and change the status to **Enabled**.


## Credits and references

This workflow is base on the workflow #0041 with added response actions: https://ciscosecurity.github.io/sxo-05-security-workflows/workflows/0041

## Notes

Please test this properly before implementing in a production environment. This is a sample workflow!
