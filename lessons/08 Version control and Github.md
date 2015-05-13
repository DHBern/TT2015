Version control and Github
==========================

or, never lose your work again.
------------------------------

*Version control* is a system for keeping track of your work - not just what you have now, but also that paragraph you wrote yesterday that you deleted today and now you want it back. (Or, indeed, that Python method.)

There are a lot of version control systems in use, but the one we will look at today is Git. The advantage of Git is that it is backed by a good (and free, up to a point) online service for collaboration - you can make an account, set up teams, and allow anyone you want to work with you.

There are two services that can be used:

* [Github](https://github.com/). This is the most popular and well-known, certainly in the humanities. Accounts are free, making teams is free, public repositories are free, private repositories are not (although they have an education program that might help you out.) Today we will be using Github.
* [Bitbucket](https://bitbucket.org/). This is very much like Github, with a different model: accounts are free, repositories are free (both public and private), free collaboration is limited to teams of up to 5 people.

Getting started: Git on your computer
-------------------------------------

First you will create a repository of your own, then you will contribute to a shared 
repository. A *repository* is a place for all your stuff, or a place for all the stuff
of a group.

1. Choose a directory (folder) on your computer that you want to track. It might be a new (and empty) folder, or it might be one that you have some work in (e.g. your homework for this class.)

2. 
  * (Windows) Open Git Bash and go to your directory.
  * (Mac) Open a Terminal window and go to your directory.

3. Run the following commands. You will only ever have to do this once.

		git config --global user.name "Your Name"
		git config --global user.email "your.name@student.unibe.ch" <-- whatever you just used to sign up
		git config --global push.default simple  <-- make things easier later on

3. Run the command `git init`. Voilà, you are using version control! Everything in this directory, and all changes you make and tell Git about, will be kept track of. This directory is now a Git repository.

4. Run the command `git status`. The output should look like this:

		On branch master
		Initial commit
		nothing to commit (create/copy files and use "git add" to track)
	
	or this:

		On branch master
		Initial commit
		Untracked files:
		   (use "git add <file>..." to include in what will be committed)
			.idea/
			testcypher.txt
			testneo.py
		nothing added to commit but untracked files present (use "git add" to track)

This message gives us some hints about what to do next. If you don't have any files, then make one - open your text editor (or even Word, if you like) and make a new file. Save the result into this directory.

Using your repository
---------------------

Now that you have some files, you can run the command `git add [your_files]`. If you run `git status` again, you will now get a message that looks like this:

	On branch master
	
	Initial commit
	
	Changes to be committed:
	  (use "git rm --cached <file>..." to unstage)
	
		new file:   testcypher.txt
		new file:   testneo.py

But you aren't done yet! Git works in two stages for any repository - first you tell it what changes you want to record with `git add`, and then you tell it "okay, I'm ready, save these changes" with `git commit`.

The idea here is that changes can go together logically. You make some changes to a spreadsheet, which means that a paragraph in your paper needs to be updated. You want to save these things together, because they are related, but meanwhile you have also added an image that has nothing to do with the spreadsheet changes. So you `git add` the spreadsheet and your paper, but not the image! Then you run `git commit` to save their state, with an appropriate message. Once that's done, you can *then* save your image. (Or, indeed, vice versa!)

The `git commit` command always needs a *message*. This is a memo for you, to remind you want this change was about. So let's run the command:

	git commit -m "This is my first Git commit"
	
You'll get output that looks like this:

	[master (root-commit) 111a7f4] testing local commit
 	2 files changed, 61 insertions(+)
 	create mode 100644 testcypher.txt
 	create mode 100644 testneo.py
	
Now if you run `git status` again, this is what you'll see:

	On branch master
	nothing to commit, working directory clean
	
Try making a change to one of your files, and go through the `git add` / `git commit` cycle again, for practice.

Github and collaboration
------------------------

The real value of Git is the ability to have a backup of your repository off on the Internet, to share files across multiple computers, and to collaborate with others! For this you need a *Git server*. You can set up and run your own Git server if you have the resources; if not, this is what Github and Bitbucket provide.

We'll now put the repositories we just made on Github (or Bitbucket, if you are feeling dangerous - but if you choose Bitbucket, make sure your teammates do too!) Here's how.

1. Make a personal repository for yourself: go to https://github.com and log in, then click the green button next to "Your repositories." Give the repository the same name as the directory/repository you have just been working in.

2. When it asks, say that no, you don't want a README or a .gitignore file. (If you didn't already have a repository on your computer that will correspond to this one, then it would be a very good idea to say 'yes' to the README.)

3. Go to the repository you've made and look for its "HTTPS clone URL" in the sidebar on the right. Copy that URL.

4. Go back to your Git Bash / Terminal window and run the command

		git remote add origin [that URL you just copied]
		
	Next, run
	
		git remote -v
		
	and make sure you have a message like this:
	
		origin	https://github.com/tla/dd_repo.git (fetch)
		origin	https://github.com/tla/dd_repo.git (push)
		
	Finally, run
	
		git push --set-upstream origin master
    
5. Now you have the two directories connected, so it's time to bring them into sync. You do this with the `git push` command.
    
6. Now your `git status` message looks a little different!

		On branch master
		Your branch is up-to-date with 'origin/master'.
		nothing to commit, working directory clean

7. Practice again the make change / add / commit / push cycle.

		[make a change to a file or two]
		git add my_file1 my_file2
		git commit -m "This is another practice commit"
		git push
	
7. Now we will see how shared repositories work. Github and Bitbucket (but especially Github) are essentially social networks for collaboration. That means you can all share things! We're going to set up shared project directories for your project groups. First, choose one team member to make a repository on Github. This time, say "Yes" you want a README. (Do you see how the README uses Markdown? Now you know how to edit it!)

8. Now that person should go to 'Settings' -> 'Collaborators' and add his/her team members.
    
8. Now all team members can get the new repository directory onto their computers by running a new command, `git clone`. This uses the same 'clone URL' as we saw above, and will make a new folder on your computer that is your shared repository. **YOU CANNOT RUN GIT CLONE FROM A DIRECTORY THAT IS ALREADY A GIT REPOSITORY!** So before you run this, make sure to `cd ..` (or `cd` somewhere else, at any rate) to leave the repository you have been experimenting with.

		cd ..
		git clone https://github.com/DHBern/our-awesome-project.git
		cd our-awesome-project
    
9. Add a file, or make a change to the README.md file. And then see what happens if you try to push it! Only one of you will succeed...
	
		git commit -m "I made a change to a shared repository"
		git push

10. The rest of you will get a message like this:

		To git@github.com:tla/stemmaweb.git
		 ! [rejected]        master -> master (non-fast-forward)
		error: failed to push some refs to 'git@github.com:tla/stemmaweb.git'
		To prevent you from losing history, non-fast-forward updates were rejected
		Merge the remote changes (e.g. 'git pull') before pushing again.  See the
		'Note about fast-forwards' section of 'git push --help' for details.

11. Scary huh? But it's okay, nothing actually broke! What it says is that someone else already changed the repository since you last got a copy, and you have to update your copy before you are allowed to send changes. (Otherwise whatever was changed by the someone else will be lost, and that isn't very collaborative.) Here is how you do that:

    	git pull
    
12. Now try your `git push` command again. For some of you it will work, and for others you might get a message about a 'conflict'. Raise your hand if that's the case.

13. A conflict means that two of you tried to change the same place in the same file at the same time, and whichever of you wasn't first now has to decide what to do. I'll show an example of a conflict up on the screen and how we *resolve* it. This looks a little intimidating, but do it a few times and it will start to make sense.

14. Now go to the repository page on Github, and you'll be able to see where everyone has made changes!
    
