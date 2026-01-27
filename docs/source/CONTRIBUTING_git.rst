How To Contribute to NAIRR Community Resources Documentation (Git)
==================================================================

Refer to `GitHub's documentation for the Fork & Pull Request workflow <https://docs.github.com/en/get-started/exploring-projects-on-github/contributing-to-a-project>`_ for more information.

#. Login to GitHub
#. Copy SSH key to GitHub (optional)
#. Fork the NAIRRProgram/nairr repository (https://github.com/NAIRRProgram/nairr) and create a working branch.

    #.  Click on the "Fork" button near the top-right of the repository page.

        * You only need to fork the repository once. If already forked during a previous change, skip this step and move on to creating a branch.

#. Clone the fork locally
    #. Navigate to your github fork of the repository
    #. Click Code -> Copy ``git clone <fork_url>`` command.  Use the SSH link if you've uploaded an SSH key, otherwise use http
    #. In your local machine terminal, run `git clone` with the copied line

#. Setup environment
    #. Create and activate a virtual environment
    #. ``pip install -r requirements.txt``

#. Make edits
    #. Use your editor or IDE of choice

#. Preview changes
    #. ``cd docs``
    #. ``make html``
    #. Navigate in file browser to index.html

#. Repeat edits and preview as until changes are ready

#. Commit changes
    #. ``git add <files>``
    #. ``git commit -m 'message describing your changes here'``

#. Push to fork
    #. set upstream - following github documentation
    #. git push (to your fork)

#. Open Pull Request for main
    #. Navigate to fork on GitHub
    #. Open Pull Request
