### Welcome to Conference Central, a web app for managing conferences. ###

This app allows you to view, create, and modify conferences and conference
sessions.

### To use this app, point your web browser to: ###

bigconference2.appspot.com


### Design notes: ###

The Session class contains the fields specified in the problem description
plus the websafe key of the session and its parent conference.  Inclusion
of these keys simplifies some of the queries.

The SessionForm class contains the same fields as Session, but all in
string format.

The speaker is represented as a string inside the Session class.  That's
because for this particular use case the only thing a Session object
needs to know about the speaker is their name.  We may want to maintain
more detailed info about the speaker.  For example we may want to let the
users look at a speaker's background and qualifications.  That will help
the user decide if they want to attend a session with that speaker.
In cases like that we could introduce a separate data class called Speaker.


### Task notes: ###

For Task 3, the following additional queries are implemented:
GetSessionsByDate - shows all the sessions happening on a specific day
GetSessionsByTime - shows all the sessions that begin at a specified time.

For the query problem: the issue is that the Datastore does not allow
inequality filters on more than one property in a single query.

To get around this, I first do a query for Sessions starting before 7pm
and store the results.  I then use a for loop to go through the query
results, choosing the ones that are non-workshop and storing them in
a separate list.  When the loop terminates, the list containing the
non-workshops is returned.

This is implemented in the method GetSessionsBefore7NotWorkshop.
