### How to Collaborate with GitHub (powered by MLH).

The workshop was powered by Major League Hacking - Localhost and sponsored by GitHub.  Participants were given Hands on Tutorials on using GitHub and it’s CLI.

I honestly don't see much of a point in making this document but it can be a good starting point for someone who never used Git or GitHub. If you want a more colorful version of the same, you can refer our [presentation](https://drive.google.com/open?id=1Y_U-h6G3taz1mgI0nSpvMQSfjwGNgty9).

*Let's Get started!*

### Step 1: Make a GitHub account

The fact that you are reading it means you have alreaday opened [GitHub](https://github.com/). The first thing that you are prompted is an option to make an account.

### Step 2: Make a repository

Notice the **+** sign on the top right corner? Click it and click on 'new repository'.
Since you are a noob, I'd recommed to put a tick on the option to initialize with README.

### Step 3: Add something in README

This is going to be the place where we make edits for proof of concepts, soon you'll be able to play around with huge number of files. Make some edit in the README file and commmit it.

*Now let's get some of the confusion out of the way!*

#### Git vs GitHub:

Git is a version control system. It keeps track of changes of files in your local system

GitHub is a platform for code collaboration and uses Git for tracking changes.

### Some terminology:

Suppose you like someone's repository and you want to own a copy of it, you *fork* it.

**fork:** your own copy of someone else's repository.

You own a repository, you love it's current working conditions but you want to have anothewr copy of it to make some changes withougt losing the current state. you *branch* it.

**branch:** a parallel version of the master copy of a repo. Making a branch allows you to edit code without accidentally breaking a working version

You made some changes in some branch. Now you want to save those changes. You *commit* the changes

**commit:** a group of revisions you want to officially add to your branch

There are some more terms, you'll understand them soon.

### Git?

As mentioned earlier, Git is a version control system for your local system. Download and follow the installation intructions from [here](https://git-scm.com/downloads).

Once installed, run the following:

    git config global user.email 'your_github_email'
    git config global user.name 'your_github_username'


### Step 3:

Now let's have a copy of our repository on our local system. This step is called **clone**

Perform this by:

    git clone <reository-URL>.git

Note that if you want to clone a particular branch, you must mention it in the command

### Step 4: 

Make some edits to the files. 

### Step 5:

Now that you've made changes to your repository, it's time to **push** the changes on github. This means that whatever changes you made in your system will now be reflected on GitHub. If you don't want to change the current version on github i.e Master branch, push your changes on a new branch.

    git add.
    git commit -m <Type your message>
    git push

### Bored or not, we're wrapping up.

You have a repository on GitHub and your local system. 

What if contents of it are changed via github or using another system and want the changes to be made in your local system too?

It's time to *pull.*

Just by typing running in the direcotry, you can pull the changes

    git pull




