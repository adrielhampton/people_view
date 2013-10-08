Contact Resource Description
============================

| name           | accessibility | sample                       | description                                                                 |
| -------------- | ------------- | ---------------------------- | --------------------------------------------------------------------------- |
| type_id        | required      | 5                            | The ID of the contact type. Get this via use of the Contact Types endpoints |
| method         | required      | door_knock                   | The method through which the contact was made                               |
| sender_id      | optional      | 4123                         | ID of the person who made the contact                                       |
| recipient_id   | required      | 8123                         | ID of the person receiving the contact, provide in the URL                  |
| status         |               | not_interested               | How the contact went                                                        |
| broadcaster_id | optional      | 8123                         | ID of the broadcaster on whose behalf the sender made the contact           |
| note           | optional      | He did not support the cause | note about the content of the contact                                       |
