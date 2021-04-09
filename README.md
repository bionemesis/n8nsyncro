# n8nsyncro
n8n workflows that integrate with Syncro

These are workflows that we created for our MSP to work with Syncro's API. They are provided as is without any support. When working with the Syncro API, you need to use Authorization type "Header Auth" and use "Authorization" for the Name and "Bearer <token>" for the Value (chaning <token> to your API key).

[dialpad_to_syncro.json](https://github.com/bionemesis/n8nsyncro/blob/main/dialpad_to_syncro.json)

This workflow takes Dialpad call information for an answered call and pushes it into Syncro as either a ticket or an update to an existing ticket. You will need to have a workflow for each technician at this time. It also saves call/ticket information to a Google Sheet to be queried by the dialpad_to_syncro_timer.json workflow. This will match to inbound and outbound calls, so if that's not desired you need to add in an IF to only proceed on either inbound or outbound calls.

[dialpad_to_syncro_timer.json](https://github.com/bionemesis/n8nsyncro/blob/main/dialpad_to_syncro_timer.json)

This workflow takes Dialpad call information after a call is disconnected and pushes it into Syncro as a ticket timer update, matching the start time and end time provided by Dialpad and a note that containing the contact or customer name and number.

[syncro_to_clockify_project.json](https://github.com/bionemesis/n8nsyncro/blob/main/syncro_to_clockify_project.json)

This workflow creates a project in Clockify that any user can track time against. Syncro should be setup with a webhook via Notification Set for Ticket - created (for anyone).

[syncro_status_update_clockify.json](https://github.com/bionemesis/n8nsyncro/blob/main/syncro_status_update_clockify.json)

This workflow will either archive or unarchive a project in Clockify based on a Syncro status change. Syncro should be setup with a webhook via Notification Set for Ticket - Status was changed. This does not handle merging of tickets as Syncro doesn't support a Notification Set for merged tickets, so you should change a ticket to Resolved first before merging it.

[clockify_to_syncro.json](https://github.com/bionemesis/n8nsyncro/blob/main/clockify_to_syncro.json)

This workflow will take a timer entry from Clockify and submit it to a matching ticket in Syncro. It saves the time entry ID from Clockify and the time entry ID from Syncro into a Google Sheets. Then, it will check if a match already exists from a previous update and will update the same time entry if the description or time is changed in Clockify. There is a Set node with the name and Syncro IDs of technicians. If you have multiple technicians with the same name, this won't work for you. Likewise, if the name in Clockify doesn't exactly match what you put in the Set, it won't work.

[syncro_alert_to_opsgenie.json](https://github.com/bionemesis/n8nsyncro/blob/main/clockify_to_syncro.json)

This workflow will take an alert from Syncro, determine if it's an agent_offline_trigger type, then determine if it's a new alert or a close to an existing alert, and then submit it to OpsGenie. New alerts will create a new alert in OpsGenie and resolved alerts will close the alert in OpsGenie. It doesn't require any kind of Google Sheets because OpsGenie allows you to submit a unique ID (known as an alias) along with the alert, which can be referenced later when closing the alert. The trigger type can be changed to suit your needs.