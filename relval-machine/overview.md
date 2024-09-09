# Overview

### Structure and navigation

RelVal machine has five different pages - Home (Initial page), Tickets, RelVals, Dashboard and Editing/Creating new. First four pages can be reached by clicking buttons at the top bar - click RelVal logo to get to the Home page or use other three appropriately named buttons. The Editing/Creating new page depends on the context, i.e. it can be accessed only from Tickets and RelVals pages and allow actions on these objects.

![Top bar with navigation buttons and user info](<../.gitbook/assets/Screenshot from 2021-07-21 13-50-10.png>)

### Users

There are three kinds of user roles in the RelVal machine: User, Manager and Administrator. The role can be determined by looking for a star next to the person's name in the top bar. If there is no star, user is a User, if star is yellow, user is a Manager and if it's blue, user is an Administrator. Role can also be seen in a tooltip when hovering over user's name.

User roles are controlled by E-Groups. Manager role requires membership of "cms-ppd-conveners-pdmv" or "cms-ppd-pdmv-val-admin-pdmv" e-group, Administrator role requires membership of "cms-pdmv-serv" e-group.

* User - can browse RelVal machine, use search, look at tickets and RelVals, cmsDriver commands. Basically users are free to browse, but are not allowed to do any persistent changes.
* Manager - can do same actions as User. Managers can also create, delete and update Tickets and RelVals, submit and reset RelVals. Managers have access to all the RelVal machine function and can perform all actions. Some actions are allowed to the Managers, but buttons are hidden as they should not be needed for normal operation.
* Administrators - can do same actions as Manager. Administrators do not ahve any special powers, they just see more debug output and have a couple of buttons to perform actions that should be done automatically, e.g. force refresh from Stats2.

![User "John Johnson" and a "Manager" star](<../.gitbook/assets/Screenshot from 2021-07-21 13-50-53.png>)
