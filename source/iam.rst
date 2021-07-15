Identity and Access Management
------------------------------

IAM Overview
~~~~~~~~~~~~

Our Figshare for Institution has a couple of features to maintain identity
and access management (IAM) settings and to assist in data repository
administration.

First, we have the ability to set a quota of available space for each user.
Our default quotas, applicable to most ReDATA users, are:

+-------------------+--------------------------------------------+
| Classification    | Quota                                      |
+===================+============================================+
| Undergraduates    | 0 (initially), 100MB after they contact us |
+-------------------+--------------------------------------------+
| Graduates         | 0.5 GB                                     |
+-------------------+--------------------------------------------+
| Faculty/Staff/DCC | 2 GB                                       |
+-------------------+--------------------------------------------+

Second, we have the ability to assign each users to groups on Figshare
(a.k.a. "portals"). This allows for the easily exploration of data through
these portals. For our deployment we chose to do it by following common
research themes for our University. To identify researcher's discipline, we
utilize their primary affiliation at the University.


Software/Services Overview
~~~~~~~~~~~~~~~~~~~~~~~~~~

There are a number of software and services that we use for IAM. They are:

+-------------------------------------+---------------+--------------------------------------------------------+
| Software/Services                   | Maintainer(s) | Purpose                                                |
+=====================================+===============+========================================================+
| Enterprise Directory Service (EDS)  | UITS          | UArizona's LDAP directory used to gather metadata      |
|                                     |               | about their users from a central UA datastore in order |
|                                     |               | to make authorization decisions.                       |
+-------------------------------------+---------------+--------------------------------------------------------+
| Grouper                             | UITS          | UArizona's tool to create groups for UA organization.  |
|                                     |               | This is populated into EDS and Shibboleth              |
+-------------------------------------+---------------+--------------------------------------------------------+
| Shibboleth / WebAuth                | UITS          | UArizona's SAML-based access to UA IAM information     |
+-------------------------------------+---------------+--------------------------------------------------------+
| :ual-re:`ReQUIAM <ReQUIAM>`         | ReDATA team   | Python command-line API for IAM                        |
+-------------------------------------+---------------+--------------------------------------------------------+
| :ual-re:`ReQUIAM_csv <ReQUIAM_csv>` | ReDATA team   | Python command-line API and database of groups for IAM |
+-------------------------------------+---------------+--------------------------------------------------------+

Services
~~~~~~~~

First, we utilize three services provided and administered by University
Information Technology Services (UITS):

 1. EDS
 2. Shibboleth
 3. Grouper

Users who login to ReDATA uses their `NetID`_ credentials to login (WebAuth).
A user who is no longer part of the University will not have `NetID`_ and
thus will not be able to log in.


Software
~~~~~~~~

The two codebases that the ReDATA team develops and maintains are
:ual-re:`ReQUIAM <ReQUIAM>` and :ual-re:`ReQUIAM_csv <ReQUIAM_csv>`. The
former is the primary software that manages all ReDATA IAM with a
daily "cronjob" that sets research theme association ("portals") and quotas
through the Grouper API. That information is then propagated into EDS
and Shibboleth with users logging in. Also, ``ReQUIAM`` has a
command-line API to enable other manual IAM changes for the ReDATA team,
such as setting a higher quota from default quota settings
(See :ref:`IAM Overview`)

The ``ReQUIAM_csv`` software contains the mapping between the groups on
ReDATA's Figshare for Institution instance and UArizona organizational
codes. The spreadsheet is available through `Google Docs`_.

The Grouper-to-Figshare-group mapping is provided as a CSV file to be
consumed by ``ReQUIAM``, which are publicly available on GitHub at:

1. `Raw version`_
2. `Rendered version`_


Grouper settings
~~~~~~~~~~~~~~~~

To control IAM, we update Grouper group memberships, which are metadata that
is passed into EDS and ultimately Shibboleth and consumed by our Figshare for
Institution instance for account creation (for first login) and update when
users re-login. This metadata record is called ``ismemberof``.

The three ``ismemberof`` settings that ensures proper IAM are:

+----------------+-------+------------------------------------------------------------------+
| ``ismemberof`` | Type  | Purpose                                                          |
+================+=======+==================================================================+
| active         | Group | This enable login to ReDATA. Non-membership means the individual |
|                |       | is no longer an active member by Libraries privileges            |
+----------------+-------+------------------------------------------------------------------+
| portal         | Stem  | Folder containing various research themes Grouper groups         |
+----------------+-------+------------------------------------------------------------------+
| quota          | Stem  | Folder containing Grouper groups of quotas in bytes              |
+----------------+-------+------------------------------------------------------------------+

The Grouper stem prefix for the above is ``arizona.edu:Dept:LBRY:figshare``.

``ReQUIAM`` maintains direct membership for ``portal`` and ``quota`` groups.
For the ``active`` group, this is done using indirect membership from
other Grouper groups set by the University Libraries patron software,
`patron-groups`_.

Our Figshare instance maps the ``portal`` and ``quota`` settings accordingly
such that:

 1. A quota is set to ensure that a user has enough space for small deposits,
    which is most often the case. The user can request more space, which
    a ReDATA administrator would need to approve. The latter allows for
    the ReDATA team to understand the user's needs and to identify cases where
    there are large deposits requiring more assistance.
 2. A researcher's data deposits are placed in a proper Figshare group/portal.

If a user does not have a ``portal`` set then their data publication will not
appear in any group/portal, but part of the University wide group. If a quota
is not set (for undergraduates logging in for the first time), then the quota
is set to zero.

.. _NetID: https://netid.arizona.edu

.. _patron-groups: https://github.com/ualibraries/patron-groups

.. _Google Docs: https://docs.google.com/spreadsheets/d/1f8tNxj96g_4NW6LWAIx8s3AxRoBbwRvFIxUXMAYyVlU/edit#gid=1301862342

.. _Raw version: https://raw.githubusercontent.com/UAL-RE/ReQUIAM_csv/master/requiam_csv/data/research_themes.csv

.. _Rendered version: https://github.com/UAL-RE/ReQUIAM_csv/blob/master/requiam_csv/data/research_themes.csv
