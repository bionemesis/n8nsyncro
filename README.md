# n8nsyncro
n8n workflows that integrate with Syncro

These are workflows that we created for our MSP to work with Syncro's API. They are provided as is without any support. When working with the Syncro API, you need to use Authorization type "Header Auth" and use "Authorization" for the Name and "Bearer <token>" for the Value (chaning <token> to your API key).

[dialpad_to_syncro.json](https://github.com/bionemesis/n8nsyncro/blob/main/dialpad_to_syncro.json)

This workflow takes Dialpad call information for an answered call and pushes it into Syncro as either a ticket or an update to an existing ticket. You will need to have a workflow for each technician at this time. It also saves call/ticket information to a Google Sheet to be queried by the dialpad_to_syncro_timer.json workflow.

dialpad_to_syncro_timer.json

This workflow takes Dialpad call information after a call is disconnected and pushes it into Syncro as a ticket timer update, matching the start time and end time provided by Dialpad and a note that containing the contact or customer name and number.

syncro_to_clockify_project.json

This workflow creates a project in Clockify that any user can track time against. Syncro should be setup with a webhook via Notification Set for Ticket - created (for anyone).

syncro_status_update_clockify.json

This workflow will either archive or unarchive a project in Clockify based on a Syncro status change. Syncro should be setup with a webhook via Notification Set for Ticket - Status was changed.