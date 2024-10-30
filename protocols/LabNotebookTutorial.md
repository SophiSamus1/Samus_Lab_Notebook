---
layout: protocol
title: "How to: Online Lab Notebook"
author: Sophi Samus
---

### Here are step by step instructions on how to set up your own online lab notebook through GitHub!

**Important Links**
[Sophi's Notebook](https://github.com/SophiSamus1/Samus_Lab_Notebook)
[Hollie's Notebook](https://github.com/hputnam/Putnam_Lab_Notebook)
[Original Jekyll Blog](https://github.com/barryclark/jekyll-now)

First, make sure you can access the command line through your computer's terminal. If you have a Mac, all you have to do is open the Terminal app.
If you have a PC, you will need to install [GitBash](https://git-scm.com/downloads).

You will also need to make a [GitHub](https://github.com/) account and download a text editor of your choice.

### Steps

Terminal:

1. Either in the terminal or through finder/file explorer, create a folder (directory) where you want your Lab Notebook repository to live. For example: `mkdir Desktop/Notebook-Directory` 

2. In the terminal, get into this directory that you made: `cd Notebook-Directory`

3. Make that directory an empty git repository: `git init` Git is a way to do version control, which tracks changes in your files.

_If you get an error here that says invalid active developer path, use: `xcode - select --install`_

Browser:

4. Log into [GitHub](https://github.com/) or make an account if you don't already have one. Then go to [Sophi's Notebook]()

5. In the top right corner, click on the Fork button. This creates a copy of Sophi's repository into your account. Then you can go into the settings and change the name (make sure not to use spaces) to your own.

6. To get back to the home repository, click the <>Code tab on the left. Here, click the green button on the right that says Clone/Download. Copy the link it gives you. 
You will use this link to create a clone of the repository on your personal computer.

Terminal:

7. Back in the terminal, you should still be in your Lab Notebook directory. You can double check using `pwd`

8. Clone your repository with the link you copied: `git clone https://github.com/GitHub-user-name/Your-Notebook-Repo-Name.git`

Browser:

9. Back on GitHub, go to the settings tab and find the Pages section to have your notebook be made into a website. Use the dropdown menu to change the source to master branch and save. A link (something like this: https://meschedl.github.io/Samus_Lab_Notebook/) will show up at the top of the page. You may need to refresh the page for it to show up. Copy this link.

10. Back in the <>Code section, find at the top where it says "Open Lab Notebook" and the link to Sophi's notebook. Click the gear to edit and rename the description to whatever you want and paste your own link you just got from the settings page. 

Computer:

11. In Finder/File Explorer, open the \_config.yml file in your Notebook directory using a text editor. Some options are [Atom](https://atom.io/), [Sublime](https://www.sublimetext.com/download), [BBedit](https://apps.apple.com/us/app/bbedit/id404009241?mt=12) (for Macs).

12. The \_config.yml file is a map to your website. In this file, edit these to personalize your own site:
	-Name
	-Description
	-Social Media links
	-url (should look like https://SophiSamus1.github.io)
	-baseurl (should be the name of your repo: /Samus_Lab_Notebook)

_Do not change anything else in this file, otherwise your site may not publish._

Save your changes.

13. These changes have been made on your computer but now need to be sent to GitHub.

Terminal:

14. In the notebook directory, add the file to Git: `git add _config.yml`. Commit these changes and add a description of what you changed: `git commit -m "adding new config file"`

_Commits always require a message, it is helpful to be descriptive so you can understand changes you made later._

15. To push your changes to GitHub: `git push origin master`

_Since this is probably the first time you've done this, you will have to supply your login information. Your user name is your GitHub username but your password is a passkey that you need to generate._

_To generate a passkey, go to your account settings > developer settings > personal access token > Tokens (classic) > Generate new token > Generate new token (classic)_

_Check the following boxes:_
	_-repo_
	_-workflow_
	_-user_
	_-write:discussion_
	_-admin:enterprise_
	_-admin:gpg-key_

_Copy the token and use this as your password_

_To avoid having to login again: `git config --global user.name "yourusername"` and `git config --global user.email youremail@example.com`_

Computer:

16. Open the \_layouts folder in the Notebook directory and open default.html file. Edit line 45 to be the link to your GitHub notebook (ex: https://github.com/meschedl/MESPutnam_Open_Lab_Notebook/). Save the file and push to GitHub as before: `git add _layouts` `git commit -m "adding new admin link"` `git push origin master`

_add, commit, and push are the steps you will take each time you want to push a change to GitHub_

_Note: make sure there is no .git extension at the end of your link or it will not work_

17. If you want to edit the README.md file to include your name, details about your notebook, etc.: edit the file in your computer and push to GitHub.

18. The last thing you may want to change is the about page. Right now it is set up as Hollie's CV. To change it, edit the about.md file in your computer and push to GitHub.

Browser: 

19. You may have unwanted posts from Sophi's notebook since you copied her version into your account. You can get rid of any of these in GitHub by clicking on the \_posts folder, click on the post and delete. It'll ask you to commit but as long as you are in your own repository, it is fine. Just make sure to not delete the post_template.sh file. 

20. **Remember**, any time you make changes to your repository, either in the browser or on your computer, the two need to communicate to keep them both the same. `git push origin master` is how we push changes from our computer to the browser, ` git pull origin master` is how we get changes from the browser onto our computer.

Computer: 

21. Now, to make a post in your online notebook, open a blank file in your text editor and save it to the \_posts folder in your computer. Use the Jekyll markdown file naming convention: YYYY-MM-DD-Post-Name.md

_Make sure to add the .md extension to your file when you save it, otherwise it will just be a regular text document and won't format the way you want it to!_

22. Every post should have the same header, called a YAML header
`---`  
`layout: post`  
`title: Your title`    
`tags: [ specfic, tags, if, you, want, them]`  
`---`  
Then, write your post in [markdown](https://guides.github.com/features/mastering-markdown/) format ([cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet), [tutorial](https://www.markdowntutorial.com/)), save, commit, and push your post to the online repository and it should post within 10 minutes to the actual site.


### Other resources

To see what your markdown file will look like before you publish it, use [StackEdit](https://stackedit.io/app#)








