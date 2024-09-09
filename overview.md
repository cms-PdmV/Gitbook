# Overview

### Structure and navigation

ReReco machine has six different pages - Home (Initial page), Subcampaigns, Tickets, Requests, Dashboard and Editing/Creating new. First five pages can be reached by clicking buttons at the top bar - click ReReco logo to get to Home page or use other four appropriately named buttons. The Editing/Creating new page depends on the context, i.e. it can be accessed only from Subcampaigns, Tickets and Requests pages and allow actions on these objects.

![Top bar with navigation buttons and user info](<.gitbook/assets/topbar (1).png>)

### Users

There are three kinds of user roles in the ReReco machine: User, Manager and Administrator. The role can be determined by looking for a star next to the person's name in the top bar. If there is no star, user is a User, if star is yellow, user is a Manager and if it's blue, user is an Administrator. Role can also be seen in a tooltip when hovering over user's name.

User roles are controlled by E-Groups. Manager role requires membership of "cms-ppd-conveners-pdmv" e-group, Administrator role requires membership of "cms-pdmv-serv" e-group.

* User - can browse ReReco machine, use search, look at subcampaigns, requests and tickets, cmsDriver commands. Basically users are free to browse, but are not allowed to do any persistent changes.
* Manager - can do same actions as User. Managers can also create, delete and update Subcampaigns, Tickets and Requests, submit and reset Requests. Managers have access to all the ReReco machine functions and can perform all actions. Some actions are allowed to the Managers, but buttons are hidden as they should not be needed for normal operation.
* Administrators - can do same actions as Manager. Administrators do not have any special powers, they just see more debug output and have a couple of buttons to perform actions that should be done automatically, e.g. force refresh from Stats2.

![User "John Johnson" and a "Manager" star](<.gitbook/assets/Screenshot from 2021-05-12 18-06-53.png>)

