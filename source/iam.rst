Identity and Access Management
------------------------------

Software/Services Overview
~~~~~~~~~~~~~~~~~~~~~~~~~~

There are a number of software and services that we use for identity and
access management (IAM). They are:

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

First, we utilize three services provided by University Information Technology
Services (UITS):

 1. EDS
 2. Shibboleth
 3. Grouper

Users who login to ReDATA uses their `NetID`_ credentials to login (WebAuth).
To control IAM, we update Grouper group memberships, which are metadata that
is passed into EDS and ultimately Shibboleth and consumed by our Figshare for
Institution instance for account creation (for first login) and update when
users (re-login). This metadata record is called ``ismemberof``.


Software
~~~~~~~~

The two codebases that the ReDATA team build and maintains are
:ual-re:`ReQUIAM <ReQUIAM>` and :ual-re:`ReQUIAM_csv <ReQUIAM_csv>`. The
former is the primary software that manages all ReDATA IAM with a
daily "cronjob" that sets research theme association ("portals") and quotas
through the Grouper API. That information is then propagated into EDS
and Shibboleth with users logging in. Also, ``ReQUIAM`` has a
command-line API to enable other manual IAM changes for the ReDATA team,
such as setting a higher quota from default quota settings, which are:

+-------------------+--------------------------------------------+
| Classification    | Quota                                      |
+===================+============================================+
| Undergraduates    | 0 (initially), 100MB after they contact us |
+-------------------+--------------------------------------------+
| Graduates         | 0.5 GB                                     |
+-------------------+--------------------------------------------+
| Faculty/Staff/DCC | 2 GB                                       |
+-------------------+--------------------------------------------+

The ``ReQUIAM_csv`` software contains the mapping between the groups on
ReDATA's Figshare for Institution instance and UArizona organizational
codes. The spreadsheet is available through `Google Docs`_.

The working mapping is provided as a CSV file to be consumed by
``ReQUIAM``, which are publicly available on GitHub at:

1. `Raw version`_
2. `Rendered version`_


.. _NetID: https://netid.arizona.edu

.. _Google Docs: https://docs.google.com/spreadsheets/d/1f8tNxj96g_4NW6LWAIx8s3AxRoBbwRvFIxUXMAYyVlU/edit#gid=1301862342

.. _raw version: https://raw.githubusercontent.com/UAL-RE/ReQUIAM_csv/master/requiam_csv/data/research_themes.csv

.. _rendered version: https://github.com/UAL-RE/ReQUIAM_csv/blob/master/requiam_csv/data/research_themes.csv
