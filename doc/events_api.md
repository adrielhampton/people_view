Events API
==========

Index Endpoint
--------------
Use this endpoint to list the events stored in the nation

GET /api/v1/sites/:site_slug/pages/events

### Attributes
* page - page number
* per_page - number of results to show per page
* tags - tags present on events returned
* starting - earliest start time for events returned (inclusive)
* until - latest end time for events returned (exclusive)

### Example

```
GET https://foobar.nationbuilder.com/api/v1/sites/foobar/pages/events?starting=2013-03-01
```

```json
{
  "page": 1,
  "total_pages": 1,
  "per_page": 10,
  "total": 2,
  "results": [
    {
      "id": 5,
      "slug": "the_event_of_the_year",
      "status": "expired",
      "site_slug": "foobar",
      "name": "The event of the year!",
      "headline": "The event of the year!",
      "title": "The event of the year!",
      "excerpt": null,
      "author_id": 65,
      "published_at": "2013-05-07T14:14:07-07:00",
      "external_id": null,
      "intro": "",
      "calendar_id": 1,
      "contact": {
        "name": "Event Creator",
        "phone": null,
        "show_phone": true,
        "email": "foobarevents@mailinator.com",
        "show_email": true
      },
      "start_time": "2013-05-08T18:00:00-07:00",
      "end_time": "2013-05-08T21:00:00-07:00",
      "rsvp_form": {
        "phone": "hidden",
        "address": "hidden",
        "allow_guests": true,
        "gather_volunteers": false
      },
      "capacity": 15,
      "show_guests": true,
      "venue": {
        "name": "",
        "address": {
          "address1": "",
          "address2": "",
          "city": "Pasadena",
          "state": "CA",
          "country_code": "US",
          "zip": "91101",
          "lat": "34.1427587",
          "lng": "-118.1386005"
        }
      },
      "autoresponse": {
        "broadcaster_id": null,
        "subject": null,
        "body": null
      },
      "shifts": [{
        "id": 1,
        "start_time": "2013-05-17T10:50:17-07:00",
        "end_time": "2013-05-17T11:55:17-07:00",
        "goal": 15,
      }]
    },
    {
      "id": 3,
      "slug": "event",
      "status": "expired",
      "site_slug": "foobar",
      "name": "event",
      "headline": "event",
      "title": "event - Foobar Softwares",
      "excerpt": null,
      "author_id": 9,
      "published_at": "2013-02-28T20:43:36-08:00",
      "external_id": null,
      "intro": null,
      "calendar_id": null,
      "contact": {
        "name": null,
        "phone": null,
        "show_phone": true,
        "email": null,
        "show_email": true
      },
      "start_time": "2013-03-01T18:00:00-08:00",
      "end_time": "2013-03-01T21:00:00-08:00",
      "rsvp_form": {
        "phone": "hidden",
        "address": "hidden",
        "allow_guests": true,
        "gather_volunteers": false
      },
      "capacity": 0,
      "show_guests": true,
      "venue": {
        "name": null,
        "address": null
      },
      "autoresponse": {
        "broadcaster_id": 2,
        "subject": "RSVP confirmation for event",
        "body": null
      },
      "shifts": null
    }
  ]
}
```


Create Endpoint
---------------
Use this endpoint to create an event

POST /api/v1/sites/:site_slug/pages/events

### Parameters

* The standard page parameters -
    * slug - where the page will live on the website - an event with slug 'party' will live at `http://{domain}/party`
    * status - `drafted` or `published`
    * name - a name for the page
    * headline - the headline of the page
    * title - the title of the page
    * excerpt - excerpt of the content to show on search engine results
    * author_id - id of the author of the page
    * external_id - id of the page from another tool
* calendar_id - id of the calendar on which this event should appear
* intro - introductory information about the event
* start_at - starting time of the event
* end_at - ending time of the event
* contact - details about the point of contact for the event
    * person_id - id of the contact
    * contact_phone - the contact's phone number for the purposes of the event
    * show_phone - whether to publically show that phone number
    * contact_email - the contact's email address for the purposes of the event
    * show_email - whether to publically show that email address
* rsvp_form - details about the form users will fill out to (optional, leave out and the event will not accept RSVPs)
    * phone - whether to show the phone input field on the RSVP form.  Possible values are "optional", "required", "hidden"
    * address - whether to show the address input field on the RSVP form.  Possible values are "optional", "required", "hidden"
    * allow_guests - whether to allow the RSVPing person to bring more guests.  Provide true or false.
    * gather_volunteers - whether to ask people if they wish to volunteer on the RSVP form. Provide true or false. Not available for Enterprise and Small Business editions.
* show_guests - whether to show the guest list publically
* capacity - maximum event attendees
* venue - details about the location of the event
    * name - name of the venue (Staples Center, for example)
    * address - address information
* autoresponse - the details of the email to send to a person after they RSVP (optional, leave off to not send RSVP confirmation email)
    * broadcaster_id - id of the broadcaster on whose behalf the response will be sent
    * subject - subject line of autoresponse email
    * body - body of the autoresponse email
* shifts - an array of shifts to offer for volunteering on the RSVP form.  Each shift definition has these attributes:
    * goal - the goal amount of volunteers to gather for the event shift
    * start_time - starting time of the shift
    * end_time - ending time of the shift

### Example

```
POST https://foobar.nationbuilder.com/api/v1/sites/foobar/pages/events
```

```json
{
  "event": {
    "name": "Fasting Day",
    "intro": "Take the 24hr nofoodchallenge!!!",
    "time_zone": "-07:00",
    "start_at": "2013-05-08T17:00:00-07:00",
    "end_at": "2013-05-08T19:00:00-07:00",
    "contact": {
      "name": "Byron Anderson",
      "contact_phone": "1234567890",
      "show_phone": true,
      "contact_email": "contact@venue.com",
      "show_email": true
    },
    "calendar_id": 3,
    "rsvp_form": {
      "phone": "optional",
      "address": "required",
      "allow_guests": true,
      "gather_volunteers": true
    },
    "show_guests": true,
    "capacity": 80,
    "venue": {
      "name": "Ralphs Parking Lot",
      "address": {
        "address1": "123 Foo St",
        "city": "Pasadena",
        "state": "CA"
      }
    },
    shifts: null
  }
}
```

Update Endpoint
---------------
Use the update endpoint to change the details of a pre-existing event page.

Show Endpoint
-------------
Get the details of a specific event.

GET /api/v1/sites/:site_slug/pages/events/:id

### Example

```
GET https://foobar.nationbuilder.com/api/v1/sites/foobar/pages/events/1
```

```json
{
  "event": {
    "id": 1,
    "slug": "foobar",
    "status": "drafted",
    "site_slug": "foobar",
    "name": "foobar",
    "headline": "foobar",
    "title": "foobar - Foobar Softwares",
    "excerpt": null,
    "author_id": 1,
    "published_at": null,
    "external_id": null,
    "intro": null,
    "calendar_id": 1,
    "contact": {
      "name": null,
      "phone": null,
      "show_phone": true,
      "email": null,
      "show_email": true
    },
    "start_time": "2013-02-07T18:00:00-08:00",
    "end_time": "2013-02-07T21:00:00-08:00",
    "rsvp_form": {
      "phone": "hidden",
      "address": "hidden",
      "allow_guests": true,
      "gather_volunteers": false
    },
    "capacity": 0,
    "show_guests": true,
    "venue": {
      "name": null,
      "address": null
    },
    "autoresponse": {
      "broadcaster_id": 2,
      "subject": "RSVP confirmation for foobar",
      "body": null
    },
    shifts: null
  }
}
```

Delete Endpoint
---------------
Remove an event from a site.

DELETE /api/v1/sites/:site_slug/pages/events/:id

RSVP Index Endpoint
-------------------
Use this endpoint to list the RSVPs for an event

GET /api/v1/sites/:site_slug/pages/events/:event_id/rsvps

### Parameters
* page - page number (optional, default 1)
* per_page - number of results to show per page (optional, default 10, max 100)

### Example

Issuing this request:

```
GET https://foobar.nationbuilder.com/api/v1/sites/foobar/pages/events/1/rsvps
```

Should get you a response like this:

```json
{
  "page": 1,
  "total_pages": 1,
  "per_page": 10,
  "total": 1,
  "results": [
    {
      "id": 2,
      "event_id": 13,
      "person_id": 75406,
      "guests_count": 2,
      "volunteer": false,
      "private": true,
      "canceled": false,
      "attended": true
    }
  ]
}
```

RSVP Creation Endpoint
----------------------
Use this endpoint to create an RSVP for an event

POST /api/v1/sites/:site_slug/pages/events/:event_id/rsvps

### Parameters

* rsvp
    * person_id - id of the person RSVPing for the event
    * guests_count - number of guests the person is bringing with them
    * volunteer - whether the person wishes to be volunteer staff for the event
    * private - whether the RSVP should be considered private
    * canceled - whether the person canceled the RSVP
    * attended - whether the person actually attended the event
    * shift_ids - ids of shifts the person wishes to staff

### Example

Issuing a request like this:

```
POST https://foobar.nationbuilder.com/api/v1/sites/foobar/pages/events/1/rsvps
```

With attached body like this:

```json
{
  "rsvp": {
    "person_id": 123,
    "guests_count": 2,
    "volunteer": true,
    "private": true,
    "canceled": false,
    "attended": true,
    "shift_ids": [1, 2, 3]
  }
}
```

Should get you a response like this:

```json
{
  "rsvp": {
    "id": 5,
    "event_id": 1,
    "person_id": 123,
    "guests_count": 2,
    "volunteer": false,
    "private": true,
    "canceled": false,
    "attended": true,
    "shift_ids": [1, 2, 3]
  }
}
```

RSVP Update Endpoint
--------------------
Update the RSVP details, to set whether they cancel or attend, for example.
Acts similarly to creation endpoint.

PUT /api/v1/sites/:site_slug/pages/events/:event_id/rsvps/:id
