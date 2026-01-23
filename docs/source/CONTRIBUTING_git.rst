How To Contribute to NAIRR Community Resources Documentation (Git)
============================================================

#. Login to github
#. Copy ssh key to github (optional)
#. Fork the NAIRRPilot/nairr repository (https://github.com/NAIRRProgram/nairr) and create a working branch.

    #.  Click on the "Fork" button near the top-right of the repository page.

        * You only need to fork the repository once. If already forked during a previous change, skip this step and move on to creating a branch.

#. Clone the fork locally
    #. Navigate to your github fork of the repository
    #. Click Code -> Copy Git clone <fork_url> command.  Use the ssh link if you've uploaded an ssh key, otherwise use http
    #. In your local machine terminal, run git clone with the copied line

#. Setup environment
    #. Create virtual environment
    #. Pip install -r requirements.text

#. Make edits
    #. Use your editor or IDE of choice

#. Preview changes
    #. Make html
    #. cd BUILD 
    #. Navigate in file browser to index.html

#. Repeat edits and preview as until changes are ready

#. Commit changes
    #. git add <files>
    #. git commit -m 'message describing your changes here'

#. Push to fork
    #. set upstream - following github documentation
    #. git push (to your fork)

#. Open Merge Request for main
    #. Navigate to fork on github
    #. Open Merge Request
