

|HTTP Method|Route|Description|Role Required|Request Body (Keys only) - What the app asks of the user. It is opposite to a response.|Expected Response|
|-|-|-|-|-|-|
|POST|/api/createAccount|Allows the participant or organiser to create an account.|Participant, Organiser|{ firstName, lastName, dateOfBirth, gender, phoneNumber,email,password }|201 - Created - The user has successfully created their account.<br />400 - BadRequest -Invalid or missing user data/information<br />409 - Conflict - email already used.|
|POST|/api/logIn|Allows the participant or organiser to log in to their existing account|Participant, organiser|{username or email, password}|200 - OK - Participant/Organiser has successfully logged in. Details are correct.<br />401 - Unauthroised - A user (participant or organiser) has entered invalid personal log in details.|
|GET|/api/events|Fetches a list of events created by the organiser.|Participant, Organiser|none|200 - OK - The list of events exist.|
|GET|/api/events/{eventID}|Fetches an event, filtered by an id|Participant, Organiser|none|200 - OK - event has been found.<br />404 - Not Found - Event has not been found.|
|POST|/api/events|The organiser is adding a new event to the events list.|Organiser|{ eventID, eventName, eventType (FK), eventLocation, eventDistance, eventStartTime, eventEndTime, organiserID }|201 - Created - event created.<br />400 - Bad request - invalid data.<br />401 - Unauthorized - Not signed in.|
|PATCH|/api/events/{eventID}|The organiser updates the existing/previously created event.|Organiser (owner of the event)|-|204 - No content - Event does not exist.<br />403 - Forbidden - Not the event owner.<br />404 - Not Found - Event missing.|
|DELETE|/api/events/{eventID}/|The organiser deletes and event they previously created.|Organiser (owner of the event)|-|204 - No content - Event is deleted.<br />403 - Forbidden - Not the woner of the event.<br />404 - Not Found - Event missing or has since been deleted, or does not exist.|
|GET|/api/events/{eventID}/categories|List categories for an event|Participant, organiser|-|200 - OK - Categories returned<br />404 - Not found - Categories not found.|
|POST|/api/events/{eventID}/categories|Add a category to an owned event|Organiser|{ categoryID, categoryName, categoryDistance (Kilometres), categoryEntryFee, categoryMaxParticipants }|201 - Created - Category created.<br />400 - Bad request - invalid data.<br />403 - Forbidden - Not the oner of the event.<br />404 - Not found - The event is missing.|
|PATCH|/api/categories/{categoryID}|Update a category|Organiser|{ categoryName, categoryDistance (Kilometres), categoryEntryFee, categoryMaxParticipants }|200 - OK - Category updated.<br />403 - Forbidden - Not owner.<br />404 - Not found - Category is not found/ Category does not exist.|
|DELETE|/api/categories/{categoryID}|Remove a category|Organiser|-|204 - No content - Category is deleted.<br />403 - Forbidden - Not the owner.<br />404 - Not found - Category missing.|
|POST|/api/entries|Enter the signed-in participant into a category.|Participant|categoryID|201 - Created - Entry has been created.<br />400 - Bad request - Category full or invalid.<br />409 - Conflict - Already entered.<br />404 - Not found - Category missing.|
|GET|/api/entries/me|List the signed in participant's entries.|Participant|-|200 - OK - Participant's entries returned.|
|GET|/api/entries/{entryID}|View one entry.|Participant, organiser|-|200 - OK - Entry returned.<br />403 - Forbidden - No access.<br />404 - Not found - entry missing.|
|PATCH|/api/entries/{entryID}/cancel|Cancel the participant's entry.|Participant|-|200 - OK - Entry cancelled.<br />403- Forbidden - Not the entry owner.<br />404 - Not found - entry missing.|
|GET|/api/categories/{categoryID}/results|List category results ordered by position.|Participant, organiser|-|200 - OK - Results returned.<br />404 - Not found - Category missing.|
|GET|/api/entries/{entryID}/result|Return the results for an entry.|Participant, organiser|-|200 - OK - Results returned.<br />404 - Not found - entry/result is missing.|
|POST|/api/entries/{entryId}/result|Record the results for an entry.|Organiser (event owner)|{ startTime, endTime, position, averageSpeed, resultStatus }|201 - Created - Result recorded.<br />400 - Bad request - Invalid titming/position.<br />403 - Forbidden - Not owner.<br />409 - Conflict - result already exists.|
|PATCH|/api/results/{resultID}|Correct a recorded result|Organiser (event owner)|{ startTime, endTime, position, averageSpeed, resultStatus }|200 - OK - results updated.<br />403 - Forbidden - Not owner.<br />404 - Not found - results missing.|



