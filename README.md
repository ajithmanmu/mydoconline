# mydoconline
Mobile and backend services for MyDocOnline

## MyDoc Online
### Purpose

To build an app/service to connect doctors with their prospective customers and enable the patients to make appointments online. 

Public: Patients will be able to create/edit/delete appointments from a Calendar based UI. They will be able to see the open slots for a doctor in the calendar.

Note: We might have to bring in some kind of authentication here so that one patient cannot view/edit/delete other patients data - TBD

Admin: Doctor will be able to see the list of appointments, edit/delete (make sure to send notifications). He also will be able to set Out of Office for a period of time where the patients won’t be able to make any appointments during that time frame.


## Technical Documentation (WIP)

### Frontend:

Proposed plan is to build the mobile frontend on React Native. TBD

### Backend:

The backend will run on a node/express API server which will talk to a Mongo database.

#### Public endpoints (authenticated ??):

`POST /appointment`
	Create an appointment
	
`PUT /appointment/<appointmentID>`
	Edit an appointment
	
`DELETE /appointment/<appointmentID>`
	Delete an appointment
	
`GET /appointment (not authenticated)`
	Gets all appointments - This endpoint should accept params to filter the data for different time periods and other search criteria (to discuss further)
	
`GET /appointment/<appointmentID>`
	Get the details of a single appointment
	

#### Admin endpoints (authenticated):

`POST /admin/outofoffice`
	Create a new OOO entry for a specific timeperiod
	
`PUT /admin/outofoffice/<appointmentID>`
	Update an existing OOO entry for a specific timeperiod 
	
`DELETE /admin/outofoffice/<appointmentID>`
	Delete an existing OOO entry
	
`GET  /admin/outofoffice/`
	Gets all OOO entries
	

### Proposed Mongo Schema

Collection: Appointments
```
{
  "_id": Mongo Object, // Auto Generated Unique ID
  "patient": {
    "name": String,
    "reason": String, //reason for appointment
    "details": String //additional details of the appt
    "contact": String //phone/email
  },
  "priority": String, // Critical/High/Moderate/Low enums
  "appointmenttime": Date // in UTC
  "doctorId": ObjectID // UniqueID of a Doctor
  "createdAt": Now(),
  "updatedAt": Now(),
  "status": Bool // false if cancelled
}
```

Collection: Doctors
```
{
 "_id": Mongo Object, // Auto Generated Unique ID
  "name": String,
  "contact": {
    // Address Details
  },
  "status": Bool
}
```

Collection : OutOfOfficeEntries
```
{
  "_id": Mongo Object, // Auto Generated Unique ID
  "doctorId": ObjectID // UniqueID of a Doctor
  "OOOtime": {
    "start": Date, //in UTC
    "end": Date, //in UTC
  },
  "message": String
}
```
..continued..
