Project Management
~~~~~~~~~~~~~~~~~~

An Overview
-----------

We utilize ``git`` and GitHub extensively for version control and project management. This is crucial since we must
keep track of hundreds of bugs, improvements, and changes for several
repositories.

We use GitHub tools to track and implement changes to the software. First, we
use `GitHub issues`_ to identify and track bugs/issues/features, and
`GitHub pull requests`_ or "PR" so that a developer can suggest a set of
changes to be merged into the ``main``/``master`` branch. Within these
issue and PR tracking, we use labels to indicate what these changes/problems
pertain to. Each repository has a set of labels. Labels are helpful to
understand scope and impact and aids in GitHub search engine optimization.
To understand the scope of any work, we use GitHub milestone tracking.
Finally, we use `GitHub project boards`_ to illustrate and manage issues and
PRs. Each repository has its own project board. These are kanban style boards
with several columns/lists.


DevOps workflow
---------------
The general workflow are as follow when starting any improvement:

1. Create a new GitHub issue if one does not exist. Begin tracking it in the
   project board
2. Create a new branch locally
3. Commit changes to branch and push them to the new branch on the remote
   repository (i.e. GitHub)
4. Create a PR within the repository to merge the new branch into the ``main``/``master`` branch
5. A team member reviews the PR (if enough developers are on staff).
   Self-review are OK if staff is limited.
6. The changes are merged into the ``main``/``master`` branch and any
   associated tags are pushed to the remote repository
7. The software is manually deployed

Note: The default branch name is set to "main" starting Oct 1, 2020, not "master" anymore.
For more info: please see `Github rename master to main`_ . Certain repositories still have default branch as "master".

Branching
---------

It is strongly recommended to use ``git`` branches for software development.
This is because, at any point, multiple features/bugs are being addressed,
and changes pushed directly to the main branch could break the software if
it is *untested or has not been reviewed*. Branching is a common Developer
+ Operations ("DevOps") best practice. To create a new ``git`` branch, use
the following ``git`` commands: ( ``-b`` is to create a new branch)

::

   $ git pull origin main
   $ git checkout -b <new-branch>

To checkout an existing branch:

::

   $ git branch  # To see existing branches
   $ git checkout <branchname>

In terms of branch names, it is strongly recommended to name branches so it
is clear and concise. We strongly recommend including:

1. The GitHub issue number
2. Whether it is a feature/enhancement or a bug fix
3. A short description

The above ensures an easier understanding to the software development team.
Examples include:

1. ``feature/235_preserve_prep`` for :ual-re:`LD-Cool-P#235 <LD-Cool-P/issues/235>`
2. ``hotfix/229_400_error`` for :ual-re:`LD-Cool-P#229 <LD-Cool-P/issues/229>`
3. ``chore/242_gitignore`` for :ual-re:`LD-Cool-P#242 <LD-Cool-P/issues/242>`

Note: Our branching model initially followed a ``git-flow`` workflow with
features, hotfixes, and releases; however, we later moved away from that
model and now use a GitHub flow workflow where all changes are merged into
the ``main``/``master`` branch after review and testing.

Pushing to a remote branch
------------------------
After updating files, we can push the changes to remote branch. It is important to push to a branch (not ``main``) so that a team member can review the changes over a pull request.
use the following ``git`` commands:

::

   $ git add .
   $ git commit -m "<message>"
   $ git branch                    # list all the branches and * is the current branch
   $ git push origin <branchname>  # push to a remote branch

Versioning and tagging
----------------------
Before creating a new tag, we need to make sure all related files updated to reflect the new tag.
These files shall be checked and updated if existing:

1. Update __init__.py
2. Update setup.py
3. Update README.md
4. Update changelog.md

In all of our software, we conduct version tagging.
Here, each new version refers to a change to the codebase that is to
be deployed. We loosely follow `Semantic versioning`_ (SemVer), which
denotes changes as MAJOR, MINOR, and PATCH. There are two differences
with our method of versioning against SemVer:

1. We use the patch denotation for both hotfixes and small enhancements
   to software.
2. We use MINOR denotation for large/larger enhancements (e.g. a completely
   new feature rather than an improvement to an existing feature).

MAJOR remains the same, for incompatible API changes. We try to avoid the
latter as much as possible.

While some open-source software teams may not use version tagging, there are
many advantages. First, this step ensures that we have continuous delivery
of our software. Second, for some of our software, we automatically deploy
them on `PyPI`_, a ``python`` package manager that allows for easy
installation of the software. Finally, our logging tools records version
information for each software, so this allows the team to trace an issue
back to a specific PR. To tag a specific commit:

::

   $ git tag vX.Y.Z -m

A ``vim`` prompt will appear so you can provide a message for the tag. Often
a short message referring to the GitHub issue number will suffice.
You will then push the tag via:

::

   $ git push --tags


Merging code
------------

Direct merges to main/master branches are to be avoided. When working collaboratively, all changes must be made to a branch and a pull request opened. The pull request must be reviewed and approved by another team member before being merged to the main/master branch.


Milestone tracking
------------------

More details needed here.


Status of GitHub repositories
-----------------------------

See :ref:`Repositories status`


.. _`GitHub issues`: https://guides.github.com/features/issues/
.. _`GitHub pull requests`: https://docs.github.com/en/github/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests
.. _`GitHub rename master to main`: https://github.com/github/renaming
.. _`GitHub project boards`: https://docs.github.com/en/issues/organizing-your-work-with-project-boards/managing-project-boards/about-project-boards
.. _`PyPI`: https://pypi.org
.. _`Semantic versioning`: https://semver.org/
