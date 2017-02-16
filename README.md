1.	Create project cmm in GitLab under comms_niu group.
•	Add a “README.md” file and basic “.gitignore” file that does not track temporary file.
2.	Clone the project in SourceTree.
•	Copy the source path URL from the GitLab project browser window.
•	Specify working directory C:/GIT/comms_niu/cmm, i.e. keep all you git repos in the same place.
•	After the clone is complete, if you check this directory you will see the README.md and .gitignore files.
3.	Initialize Git Flow in SourceTree.
•	Accept default branch names and prefixes.
•	Once the Git Flow structure is initialize you will have 2 identical branches, master and develop. Develop branch will be checked out as your working copy.
4.	Now we have to make a series of updates/commits for the hierarchy of streams for the product in ClearCase:
•	First stream to commit will be NIU122_Support Stream ( Baseline "NIU122_9_27_2016_forGit" )
5.	For each stream identified above perform the following steps:
•	Create a new child stream in ClearCase and configure it to have the required parent integration stream baseline and create an associated snapshot view.
•	Zip the snapshot view and copy to desktop.
•	Start a new release branch using Git flow > Start New Release. Use the version number of the baseline used for child stream which you are migrating.
•	Unzip the snapshot view into working storage after making sure the release branch is checked out.
•	Identify the symbolic links from ClearCase using command "cleartool find -all -kind slink -print" and create symlinks in the working copy.
•	Verify the list of files that are ignored due to setting in .gitignore file using command "git status --ignored" from git bash window.
•	Commit the changes to the release branch (include stream and baseline name in commit message).
•	From Git flow finish the Release with the version number of the baseline in the TAG (this will merge the commit into both develop and master branches and delete the release branch).
6.	Identify any CDs delivered in the ClearCase integration stream or child streams that are not included in the baselines taken but which may need to be applied in the associated GIT repo branch (either develop branch or support/xxx branch). This will require discussion with the patch author - do not just blindly take all undelivered changes in child streams.
7.	Push the changes to Git Lab from SourceTree
•	Now other developers can clone the repo.
8.	Update any formal and informal build procedure doc to reflect the move from clearcase to git and add this doc to the root of the repository. Example docs can be found in the comms_niu repos.
9.	Perform an informal build and a formal build and then execute a smoke/comfort test on the newly built product.


Commands to Creating and Using git symlinks on Windows:

	git add-symlink <src> <dst>

This is the command we need to use to create the symbolic link.

* <src> is a RELATIVE PATH, respective to <dst>.
* <dst> is a RELATIVE PATH, respective to the repository's root dir.
* The command must be run from the repository’s root dir.

	git rm-symlinks

This command will replace all symlink files in checked out branch of the repo with NTFS hard links and junctions, i.e. so a build can be done

* The command must be run from the repository’s root dir.

	git checkout-symlinks

This will restore all symlink files in the checked out branch of the repo, i.e. immediately after the build has been done.

* The command must be run from the repository’s root dir.

Git environment setup and script to add the above commands to GIT bash environment can be downloaded from the following link: http://ustr-erl-7791.na.uis.unisys.com/mediawiki/index.php/GIT_Installation


