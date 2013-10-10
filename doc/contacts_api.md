Contacts API
============

Use the contacts API to log communcation in NationBuilder

Index Endpoint
--------------

View a paginated list of contacts made to a person
GET /api/v1/people/:id/contacts

### Parameters
    * page - (optional) page number
    * per_page - (optional) number of results to show per page (max 100; default 10)

### Example

```
GET https://foobar.nationbuilder.com/api/v1/people/5/contacts
```

Response with code 200:
```json
{
  "page": 1,
  "total_pages": 1,
  "per_page": 10,
  "total": 1,
  "results": [
    {
      "type_id": 6,
      "method": "email",
      "sender_id": 1,
      "recipient_id": 7,
      "status": "left_message",
      "broadcaster_id": null,
      "note": null
    }
  ]
}
```

Create Endpoint
---------------

Create a record of a contact in NationBuilder
POST /api/v1/people/:id/contacts

### Parameters

* `contact` - resource describing the contact you want to create

### Example

Issuing a request like this:
```
POST https://foobar.nationbuilder.com/api/v1/people/4123/contacts
```

With a body like this:
```json
{
  "contact": {
    "sender_id": 1058,
    "broadcaster_id": 10,
    "status": "not_interested",
    "method": "door_knock",
    "type_id": 5,
    "note": "He did not support the cause"
  }
}
```

Then a contact should be created, and you should receive a 200 response with a body like this:

```json
{
  "contact": {
    "id": 8713,
    "recipient_id": 4123,
    "sender_id": 1058,
    "broadcaster_id": 10,
    "status": "not_interested",
    "method": "door_knock",
    "type_id": 5,
    "note": "He did not support the cause"
  }
}
```

Contact Types API
=================
Use this API to list and define contact categories

Index Endpoint
--------------
The index endpoint returns a paginated list of nation-defined contact categories

GET /api/v1/settings/contact_types

### Parameters
    * page - page number
    * per_page - number of results to show per page (default 10; max 100)

### Example
```
GET https://foobar.nationbuilder.com/api/v1/settings/contact_types
```

```json
{
  "page": 1,
  "total_pages": 1,
  "per_page": 10,
  "total": 6,
  "results": [
    {
      "id": 1,
      "name": "Initial outreach"
    },
    {
      "id": 2,
      "name": "Question"
    },
    {
      "id": 3,
      "name": "Invite"
    },
    {
      "id": 4,
      "name": "Fundraising appeal"
    },
    {
      "id": 5,
      "name": "Volunteer recruitment"
    },
    {
      "id": 6,
      "name": "Thank you"
    }
  ]
}
```

Create Endpoint
--------------
The create endpoint makes new contact categories

POST /api/v1/settings/contact_types

### Parameters
    * name - string you want to associate to the contact type

### Example

```
POST https://foobar.nationbuilder.com/api/v1/settings/contact_types
```

```json
{
  "contact_type": {
    "name": "Pledge Drive 2013"
  }
}
```

Should create the contact type, and return a response with status code 200 and a body like this:

```json
{
  "contact_type": {
    "id": 13,
    "name": "Pledge Drive 2013"
  }
}
```

Use the returned id to categorize a contact as this type.

Update Endpoint
--------------
The update endpoint changes pre-existing a contact type.  Use it to rename a contact type, for example.

PUT /api/v1/settings/contact_types/:id

### Parameters
    * name - string you want to associate to the contact type

### Example

```
PUT https://foobar.nationbuilder.com/api/v1/settings/contact_types/13
```

```json
{
  "contact_type": {
    "name": "Pledge Drive Spring 2013"
  }
}
```

Should update the contact type, and return a response with status code 200 and a body like this:

```json
{
  "contact_type": {
    "id": 13,
    "name": "Pledge Drive Spring 2013"
  }
}
```

Destroy Endpoint
--------------
The destroy endpoint removes a contact type from the nation

DELETE /api/v1/settings/contact_types/:id

Contact Methods API
-------------------
This API lists the possible methods of contact

GET /api/v1/settings/contact_methods

### Example

```
GET https://foobar.nationbuilder.com/api/v1/settings/contact_methods
```

```json
{
  "results": [
    {
      "name": "Delivery",
      "api_name": "delivery"
    },
    {
      "name": "Door knock",
      "api_name": "door_knock"
    },
    {
      "name": "Email",
      "api_name": "email"
    },
    {
      "name": "Email blast",
      "api_name": "email_blast"
    },
    {
      "name": "Face to face",
      "api_name": "face_to_face"
    },
    {
      "name": "Facebook",
      "api_name": "facebook"
    },
    {
      "name": "Meeting",
      "api_name": "meeting"
    },
    {
      "name": "Phone call",
      "api_name": "phone_call"
    },
    {
      "name": "Robocall",
      "api_name": "robocall"
    },
    {
      "name": "Snail mail",
      "api_name": "snail_mail"
    },
    {
      "name": "Text",
      "api_name": "text"
    },
    {
      "name": "Text blast",
      "api_name": "text_blast"
    },
    {
      "name": "Tweet",
      "api_name": "tweet"
    },
    {
      "name": "Video call",
      "api_name": "video_call"
    },
    {
      "name": "Webinar",
      "api_name": "webinar"
    },
    {
      "name": "Other",
      "api_name": "other"
    }
  ]
}
```

Contact Statuses API
--------------------
This API lists the possible contact status categories

GET /api/v1/settings/contact_statuses

### Example

```
GET https://foobar.nationbuilder.com/api/v1/settings/contact_statuses
```

```json
{
  "results": [
    {
      "name": "Answered",
      "api_name": "answered"
    },
    {
      "name": "Bad info",
      "api_name": "bad_info"
    },
    {
      "name": "Left message",
      "api_name": "left_message"
    },
    {
      "name": "Meaningful interaction",
      "api_name": "meaningful_interaction"
    },
    {
      "name": "Not interested",
      "api_name": "not_interested"
    },
    {
      "name": "No answer",
      "api_name": "no_answer"
    },
    {
      "name": "Refused",
      "api_name": "refused"
    },
    {
      "name": "Send information",
      "api_name": "send_information"
    },
    {
      "name": "Other",
      "api_name": "other"
    }
  ]
}
```
