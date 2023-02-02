# Applying user Zero Trust policies to Umbrella top blocked identity

This workflow searches and returns the top 10 identities in Cisco Umbrella with DNS activity blocks for the last 7 days. The data is then parsed and posted in a ServiceNow incident.

Targets: ServiceNow, Umbrella API v2 OAuth2, Umbrella API v2

**Steps:**
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

**Note:** This workflow is base on the workflow #0041 with added response actions: https://ciscosecurity.github.io/sxo-05-security-workflows/workflows/0041
