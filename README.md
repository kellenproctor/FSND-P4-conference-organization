#P4: Conference Organization App

Course code for Building Scalable Apps with Google App Engine in Python class

Project 4 additions by Kellen Proctor on 3 March 2016

####INTRODUCTION:
Conference Central contains a first stab at a fully functional full-stack python web app! Let's hope it works! Written using Python and the Google App Engine, and based off of the excellent class taught by Magnus and Karl (super thumbs up!!), we're looking to exceed expectations.

###Task 1 Design Choices
Session, SessionForm, and SessionForms are implemented in models.py as a simple copy of Conference and ConferenceForms. I decided to keep speaker as a string for the sake of simplicity. I may go back to implement speaker as a distinct entity with a "speakerSessions" property. With this, it should be simple to query Speaker for all sessions at which that Speaker is attending. Further, a speaker could also have a user_id, to help a user manage his/her speaking obligations.

For the session methods, I decided to use querystrings instead of path arguments for the parameters. I think this makes the API calls a bit more elegant, and also simplifies the path.


####FILES:
database_setup.py - brief description

####DOWNLOAD:
Please clone to your most convenient directory (folder) via the following
command:


```
git clone https://github.com/kellenproctor/item-catalog.git item-catalog
```

####REQUIREMENTS:
[Vagrant](https://www.vagrantup.com/)

[Virtual Box](https://www.virtualbox.org/)

####RUNNING:
Please open a terminal, navigate to /vagrant inside the /item-catalog
directory, and run the following commands:

```
vagrant up
vagrant ssh
cd /vagrant/catalog
```

This will get you into the item_catalog directory, where you can interact with
the files as listed above. To initiate the item catalog web-app,
run the following command inside the directory containing **application.py**:

```
python database_setup.py
python lotsofitems.py
python application.py
```

Open **http://localhost:8000/** in your browser, and commence interacting with
the platform!


######Enjoy your experience! All feedback is welcome!

A third stab at these, thanks to some help from Udacity and some resources
from coach (unknown). Will check out the Readme class soon, I promise.