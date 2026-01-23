How To Contribute to NAIRR Community Resources Documentation
============================================================

#. Fork the NAIRRPilot/nairr repository (https://github.com/NAIRRProgram/nairr) and create a working branch.

    #.  Click on the "Fork" button near the top-right of the repository page.

        * You only need to fork the repository once. If already forked during a previous change, skip this step and move on to creating a branch.

        .. image:: /images/contributing/NAIRR_fork-repo.png
           :alt: The Code page. The 'Fork' button is visible at the top-right of the page.

        .. image:: /images/contributing/NAIRR_fork-repo-closeup.png
           :alt: A close-up of the 'Fork' button. Beneath it is the text 'Fork your own copy of NAIRRProgram/nairr.'

    #.  Double-check that the owner is your account, and if desired modify the repository name and description, then click "Create fork." The page will be redirected to the new fork.

        .. image:: /images/contributing/NAIRR_create-new-fork.png
           :alt: The 'Create a new fork' page.

    #.  Click on the branch drop-down near the top-left of the forked repository and ensure that the branch you want to branch from is selected (typically 'main'). Type in a name for a new branch, then click "Create branch <your-branch-name> from <originating branch>." The page will reload with the new branch name displayed in the drop-down menu.

        .. image:: /images/contributing/NAIRR_main-branch-selected.png
           :alt: The branch selection drop-down on a fork of NAIRRProgram/nairr.

        .. image:: /images/contributing/NAIRR_create-new-branch.png
           :alt: The naming of a new example branch from main.

        .. image:: /images/contributing/NAIRR_example-branch-on-forked-repo.png
           :alt: The 'Code' page on an example branch on a repository forked from NAIRRPilot/nairr.

#.  Make edits in Codespaces

    #.  Click on the green 'Code' dropdown above the project files on the right side.

        .. image:: /images/contributing/NAIRR_code-start.png
           :alt: Top-level NAIRRProgram/nairr code page.

    #.  Click on ‘Codespaces’ tab if to switch from the 'Local' tab if not already selected.

        .. image:: /images/contributing/NAIRR_code-local-tab.png
           :alt: The 'Local' tab in the 'Code' window.
        
        .. image:: /images/contributing/NAIRR_codespaces-already-existing.png
           :alt: Codespaces tab with pre-existing codespace available.

    #.  Click on ‘Create new codespace on main’ if none exist.

        *  If there are any codespaces already available, they will be shown here in place of the button to create a new codespace. In this case, create a new codespace by clicking the plus sign, or use an existing codespace by clicking the three dots across from the name and selecting 'Open in Browser'.

         .. image:: /images/contributing/NAIRR_codespaces-open-in-browser.png
            :alt: Options menu for opening existing codespace.

    #.  If prompted to periodically git Fetch by a notification at the bottom-right of the codespace, click ‘Yes’. 

        .. image:: /images/contributing/NAIRR_notification-periodically-run-git-fetch.png
           :alt: A notification at the bottom-right of the page asking whether the user wants to periodically run "git fetch."

#.  Make changes

    #.  Docs are mostly in /docs/source/ - edit existing files by selecting them in the explorer, or create new files by clicking the 'New File' icon near the top of the file explorer.

        .. image:: /images/contributing/NAIRR_codespaces-file-explorer.png
           :alt: Codespaces file explorer.

    #.  For example, create 'mynewdoc.rst' as a sibling to 'index.rst'

        .. image:: /images/contributing/NAIRR_create-new-file.png
           :alt: Codespaces file explorer with "New File" button shaded in.
        
        .. image:: /images/contributing/NAIRR_name-new-file.png
           :alt: New file being named in the file explorer.

    #.  In table of contents in 'index.rst', add new link to 'mynewdoc'.

        .. image:: /images/contributing/NAIRR_exampledoc-index.png
           :alt: File name of example document being added to the index.

    #.  Add your content in 'mynewdoc.rst'

        .. image:: /images/contributing/NAIRR_blank-new-file.png
           :alt: Blank new file.

        .. image:: /images/contributing/NAIRR_add-content-to-file.png
           :alt: Example text added to a new file.

#.  Preview local build (builds automatically on changes)

    #.  Click on the Codespaces terminal in the bottom pane
    #.  By default, the codespace will probably load the terminal in the /workspaces/nairr directory. Run "cd docs" to move down into the docs directory where the Makefile is.

        .. image:: /images/contributing/NAIRR_cd-to-docs.png
           :alt: cd to docs in the codespaces terminal.
        
        *  If the codespace is already running an http server in the terminal, then to use the terminal either select an unused bash instance to the right of the terminal, create a new instance using the plus sign, or stop the server with Ctrl+C.

           .. image:: /images/contributing/NAIRR_http-server-running.png
              :alt: The codespace terminal running an http server.

           .. image:: /images/contributing/NAIRR_select-bash-instance.png
              :alt: Bash instances already running.

    #.  From the docs directory, run "make html" to build the project.

        .. image:: /images/contributing/NAIRR_make-html.png
           :alt: Building the project with Make.

    #.  Serve the project by running "python -mhttp.server".

        .. image:: /images/contributing/NAIRR_mhttp-server.png
           :alt: Serving the ReadTheDocs build.

        *  The codespace may launch the server automatically when opened, as indicated by the opening of a web browser in the codespace and the presence of a process already running in the terminal. When this is the case, "python -mhttp.server" will fail as the address is already in use. The server will launch automatically after rebuilding the project and refreshing the browser tab viewing the documentation.

    #.  View the build by opening it in a browser tab. This can be done by:

        *  Hovering over the URL in the terminal output (http://0.0.0.0:8000/), clicking "Follow link," and selecting "Open" when prompted,

           .. image:: /images/contributing/NAIRR_mhttp-server-full.png
              :alt: A link to view the documentation which appears when hovering over the output of "python -mhttp.server."

           .. image:: /images/contributing/NAIRR_open-external-website.png
              :alt: A prompt to allow Code to open an external website which it is serving.
         
        *  or by selecting the ports tab and clicking the globe icon.

           .. image:: /images/contributing/NAIRR_ports-tab.png
              :alt: The Codespaces ports tab.

           .. image:: /images/contributing/NAIRR_ports-open-in-browser.png
              :alt: The globe icon used to open the URL in the browser.

    #.  After making additional edits, repeat the "make html" command and refresh the preview browser tab to preview new changes.

        .. image:: /images/contributing/NAIRR_http-example-home.png
           :alt: An early build of the NAIRR Community Learning Resources home page with a link to an example page in the table of contents.

        .. image:: /images/contributing/NAIRR_http-example-page.png
           :alt: An example page of documentation.

#.  Submit Pull Request

    #.  Click on the 'Source Control' icon (Left-hand taskbar, will have the number of changed files overlayed).

        *  https://docs.github.com/en/codespaces/developing-in-a-codespace/using-github-codespaces-for-pull-requests

        .. image:: /images/contributing/NAIRR_codespaces-taskbar.png
           :alt: The left-hand taskbar with a number showing changed files on the Source Control icon.

    #.  Select modified files to stage by clicking the plus icon next to the file name within the "Changes" window, or stage all changes at once by clicking the plus icon at the top of the list.

        .. image:: /images/contributing/NAIRR_stage-files-to-commit.png
           :alt: Source Control view of files with changes.

        .. image:: /images/contributing/NAIRR_stage-files-to-commit-01.png
           :alt: Source Control view of staged changes.

        .. image:: /images/contributing/NAIRR_stage-all-changes.png
           :alt: Source Control view of button to stage all changes.

    #.  Click on the downward-pointing arrow on the green 'Commit' button to open up a drop-down menu and select 'Commit & Create Pull Request.'

        .. image:: /images/contributing/NAIRR_commit-and-create-pull-request.png
           :alt: The Source Control panel with a drop-down menu under the 'Commit' button showing various commit options.

        *  If a window appears with the message 'There are no staged changes to commit. Would you like to stage all your changes and commit them directly?' Select 'Yes.'

           .. image:: /images/contributing/NAIRR_no-staged-changes-to-commit.png
              :alt: A window prompting the user to stage all changes and commit them directly.

    #.  A new tab should open with a text editor titled 'COMMIT_EDITMSG.' Add a commit message, then click the check mark in top right to accept the commit message.

        .. image:: /images/contributing/NAIRR_commit-message-blank.png
           :alt: The COMMIT_EDITMSG editor.

        .. image:: /images/contributing/NAIRR_commit-message-check-mark.png
           :alt: The COMMIT_EDITMSG editor with an example commit message and the checkmark to accept the commit message visible at the top right.

    #.  After accepting the commit message, the left-hand window should change to 'Github Pull Request.' Add a meaningful title and description.

        .. image:: /images/contributing/NAIRR-create-pull-request.png
           :alt: The Github Pull Request window.

        * If the 'Create' button is faded and can't be clicked, it may be because you are trying to merge from 'NAIRRProgram/nairr' which you may not have permission to do. If you have not yet created a branch, you will need to do so.

    #.  Click 'Create.' a tab should open in the codespace to the newly-created pull request.

        .. image:: /images/contributing/NAIRR_sample-title-description.png
           :alt: The 'GitHub Pull Request' window with sample title and description, and with an interactable 'Create' button.

        .. image:: /images/contributing/NAIRR_codespaces-pull-request.png
           :alt: A pull request as seen in the codespace.

#.  (Optional) Final preview in Github (https://github.com/NAIRRProgram/nairr)

    #.  Return to the GitHub page for the base NAIRRPilot/nairr repository and click on 'Pull Requests' at top

        .. image:: /images/contributing/NAIRR_pull-requests.png
           :alt: The Pull Requests page.

    #.  Find your pull request and click on it

        .. image:: /images/contributing/NAIRR_github-pull-requests-00.png
           :alt: The Pull Requests page.

        .. image:: /images/contributing/NAIRR_github-pull-requests-01.png
           :alt: The Pull Requests page, scrolled down to the bottom.
           
    #.  Once checks are successfull, click Show, and Details to see a full preview of ReadTheDocs with your new content.
    #.  Any comments/feedback will be posted here on your pull request.  If your changes are not showing up, you can check status here and comment.

