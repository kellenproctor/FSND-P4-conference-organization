#P4: Conference Organization App

Course code for Building Scalable Apps with Google App Engine in Python class

Project 4 additions by Kellen Proctor on 3 March 2016

####INTRODUCTION:
Conference Central contains a first stab at a fully functional full-stack python web app! Let's hope it works! Written using Python and the Google App Engine, and based off of the excellent class taught by Magnus and Karl (super thumbs up!!), we're looking to exceed expectations.

###Task 1 Design Choices
Session, SessionForm, and SessionForms are implemented in models.py as a simple copy of Conference and ConferenceForms. I decided to keep speaker as a string for the sake of simplicity. I may go back to implement speaker as a distinct entity with a "speakerSessions" property. With this, it should be simple to query Speaker for all sessions at which that Speaker is attending. Further, a speaker could also have a user_id, to help a user manage his/her speaking obligations.

For the session methods, I decided to use querystrings instead of path arguments for the parameters. I think this makes the API calls a bit more elegant, and also simplifies the path.

###Task 3: Come up with 2 additional queries
1. A user attending a conference would probably like to see all the sessions they are interested in attending, sorted by start time. So essentially the user is querying Session for all sessions in a specific conference's entity group, then sorting for date and start time. This helps a user to plan which sessions they'll attend, especially if they're interested in two session at the same time.

Code:
```
#Store the conference key in a variable
wsck = request.websafeConferenceKey

#Query for sessions using the websafeConferenceKey as an ancestor
seshs = Session.query(ancestor=ndb.Key(wsck))
seshs.order(Session.date)
seshs.order(Session.startTime)
``` 

2. Similarly, a speaker may be interested in seeing all of the sessions they are obligated to attend. Although my code does not include speaker as a distinct entity (a good addition), this can still be simply determined by simply querying Session, filtering by speaker, and sorting by date and startTime

```
#Assuming speaker is a parameter passed to the request
seshs = Session.query()
seshs.filter(Session.speaker == request.speaker)
seshs.order(Session.date)
seshs.order(Session.startTime)
```

###Task 3: Query Related Problem
So the problem is that an inequality filter can only be used for at most one property (you can't filter for sessions that are not workshops AND sessions before 7pm at the same time). One solution is to use a single filter (not workshops or before 7pm), then return the query results and iterate over the results for the second filter.

For example:
```
seshs = Session.query().filter(session.startTime < "19:00")
results = seshs.fetch()
sessions = []
for sesh in results:
    if sesh.typeOfSession != "workshop":
        sessions.append(sesh)
```

####IMPORTANT FILES:
ConferenceCentral_Complete - Project Directory
app.yaml
index.yaml
main.py - For Task 4
models.py
conference.py - I tried to make it simple to find entries

####DOWNLOAD:
Please clone to your most convenient directory (folder) via the following
command:


```
git clone https://github.com/kellenproctor/conference-organization.git conf_central
```


######Enjoy your experience! All feedback is welcome!

A third stab at these, thanks to some help from Udacity and some resources
from coach (unknown). Will check out the Readme class soon, I promise.