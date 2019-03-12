<h1 align="center">Git & GitHub Learning Lab Resources</h1>

> &nbsp;  
> Sample repository to be used alongside the [GitHub Learning Lab <span class="arrow">&xrarr;</span>](https://lab.github.com/) 
> tutorial(s), as well as some additional 3rd-party learning resources to help get you up-to-speed with Git.  
> &nbsp;

<br>

## Usage Examples —

_This is an ongoing W.I.P. so be sure to check back later for updated documentation ..._

### Install Homebrew

Install the **Required** Xcode Command Line Tools:
```sh
$ xcode-select --install
```

Install Homebrew using their installation script:
```sh
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Update Homebrew so you've got the latest & greatest index:
```sh
$ brew update
$ brew upgrade

# To diagnose any errors that may have occured, you can debug with the following;
$ brew doctor
```

### Install Git

```sh
# You should ALWAYS run the following prior to installing any packages from Homebrew.
$ brew update

$ brew install git
```

Verify your new Git installation:
```sh
$ which git
# Expected Output
/usr/local/bin/git

$ git --version
# Expected Output
git version 2.21.0
```

### Configure Git

After you [install Git](https://www.linode.com/docs/development/version-control/how-to-install-git-on-mac-and-windows), configure it for first time use using `git config`, a built-in tool that obtains and sets configuration variables. These configuration variables are located in three different places on a GNU/Linux system:

- `/etc/gitconfig` - Stores the configuration information for all system users and their respective repositories.
- `~/.gitconfig` - Stores user-specific configuration files on the system.
- `.git/config` - This is the configuration file of your current working repository.

For a Windows system, the `.gitconfig` file is located in the `$HOME` directory of the user’s profile. The full path is `C:\Document and Settings\$USER` or `C:\Users\$USER`.

After installing Git make sure your username and email address are set correctly. To verify, use the command:
```sh
git config --list
```

If your name and email are not listed in the output, use the following commands to set them manually, replacing `examplename` and `user@example.com`:
```sh
git config --global user.name examplename
git config --global user.email user@example.com
```

Set your default text editor, replacing editor-name with your desired editor:
```sh
git config --global core.editor editor-name
```

The output of git config --list should show echo the information you inputted:
```sh
$ git config --list
user.name=exampleuser
user.email=user@email.com
core.editor=editor-name
```

### Use Git with a Local Repository

A _repository_, or repo, is a collection of files and folders and the history of their changes. Changes are tracked 
through _commits_, which are like snapshots of a file at various points in the file’s history. These commits are not 
automatic, you need to manually stage a commit after each of series of file changes. Commits allow you to refer or revert 
back to a place in the file’s timeline if there are bugs or errors in your code.

If you have an new or existing project and you want to start using Git to keep track of its changes, run `git init` from 
the existing project’s directory:
```sh
git init
```

`git init` creates a new `.git` subdirectory in the current directory. This is where Git stores your configurations. The `git add` 
command tells Git to add a file to the repository and track that file’s changes:
```sh
git add filename
```

After you have added the file, stage a commit and leave a commit message. Commit messages serve as a reminder of the changes that were made to a file:
```sh
git commit -m "Initialized a Git repository for this project. Tracking changes to a file."
```

> &nbsp;  
> **Please Note:**  
> It’s good practice to provide clear and descriptive commit messages for every commit you stage, as 
> this helps collaborators to understand what a commit encompasses.  
> &nbsp;

There may be files or folders in your project directory that you do not wish to include in your Git repository. You can 
include these files in a `.gitignore` file, and Git will ignore them. A sample `.gitignore` file might look like the following:

A sample `.gitignore` file might look something like the following:
```git
1
2
3
.DS_Store
*.zip
__doNotInclude__/
```

### Basic Git Commands

| **Command**   | **Description**                                                                       | **Example**                |
|:--------------|:--------------------------------------------------------------------------------------|:---------------------------|
| `git add`     | Add a file to a repository.                                                           | `git add filename`         |
| `git rm`      | Remove a file from a repository.                                                      | `git rm filename`          |
| `git mv`      | Move or rename a tracked file, directory, or symlink.                                 | `git mv file_from file_to` |
| `git branch`  | List all the local and remote branches.                                               | `git branch branchname`    |
| `git commit`  | Commit all staged objects. Optionally, you can append a message with the `-m` flag.   | `git commit -m "updates"`  |
| `git pull`    | Download all changes from the remote repo and merge them in a specified repo file.    | `git pull repo refspec`    |
| `git push`    | Publish the changes to the remote repo.                                               | `git push repo`            |

### Branches

_Branches_ are used for editing files without disturbing the working portions of a project. The main 
branch is normally named `master` and is usually reserved for clean, working code. When making changes 
to your code, it’s customary to create a new branch and name it after the issue being fixed or the feature 
being implemented. Because Git keep tracks of file changes, you can jump from branch to branch without 
overwriting or interfering with other branches in the repo.

The basic options used with the `git branch` command are:

| **Option** | **Description**                      |
|:-----------|:-------------------------------------|
| `-r`       | List the remote branches.            |
| `-a`       | Show both local and remote branches. |
| `-m`       | Rename an old branch.                |
| `-d`       | Delete a branch.                     |
| `-r -d`    | Delete a remote branch.              |


### Example Usage

Consider an application with a single `master` branch. The author of the application wants to develop a 
new search feature. They would add a new feature branch:
```sh
git branch new-search-feature
```

Then, they would switch to that branch using the checkout command:
```sh
git checkout new-search-feature
```

Now they can safely develop and commit their changes to this feature branch without altering the working 
code of the `master` branch. At any time they could switch back to the `master` branch:
```sh
git checkout master
```

A shortcut for creating a branch and switching to that branch is to use the -b flag with the checkout command:
```sh
git checkout -b new-search-feature
```

Once the new search feature is finalized, the author of the application can merge the new-search-feature 
branch into the `master` branch:
```sh
git checkout master
git merge new-search-feature
```

Now the `master` branch has the new search feature.

### Use Git with a Remote Repository

[GitHub](https://github.com), [GitLab](https://gitlab.com), and [BitBucket](https://bitbucket.com) all provide ways to 
store Git repositories remotely and facilitate collaboration. Many of these services also include a number of other 
features that are vital to content development, including pull requests, continuous integration / continuous delivery 
pipelines (CI/CD), wikis, and webhooks. If you’d rather use a self-hosted solution, GitLab and [Gogs](https://gogs.io/) offer free locally 
hosted versions of their software that can easily be managed on a Linode. Check out our guides on [installing GitLab](https://www.linode.com/docs/development/version-control/install-gitlab-on-ubuntu-18-04/) and 
[installing Gogs](https://www.linode.com/docs/development/version-control/install-gogs-on-debian/) for more information on hosting your own remote repository software. GitHub and Bitbucket also offer paid 
enterprise versions of their software for local hosting. When discussing remote repositories, usually one of the 
aforementioned services is being referenced.

This section provides some basic information on navigating remote Git repositories.

To copy every file from a remote repository to your local system, use `git clone` followed by the remote repo’s URL:
```sh
git clone https://github.com/linode/docs.git
```

You can typically find a remote repository’s URL by clicking on the Clone or Download buttons of a remote 
repository’s user interface.

To check the status of the files within the current branch of your repository, use `status`:
```sh
git status
```

The output of the `status` command will tell you if any tracked files have been modified.

Use `remote` to view which remote servers are configured:
```sh
git remote
```

The `remote` command will display the short names of your remote repositories. If your repository was cloned, you 
will see a repository called origin. The default name `origin` comes from the cloned repository. To view more information 
about the remote repositories, use the command:
```sh
git remote -v
```

### Git Remote Repository Commands

Below are some basic commands for working with remote repositories:

| **Command**                               | **Description**                                                     |
|:------------------------------------------|:--------------------------------------------------------------------|
| `git remote add [remote-name] [url]`      | Add a new remote repository.                                        |
| `git fetch [repository [refspec]]`        | Gather all the data from a remote project that you do not have yet. |
| `git pull`                                | Obtain and merge a remote branch into your current branch.          |
| `git push [remote-name] [branch-name]`    | Move your data from your branch to your server.                     |
| `git remote show [remote-name]`           | Display information about the remote you specified.                 |
| `git remote rename [old-name] [new-name]` | Rename a remote.                                                    |
| `git remote rm [name]`                    | Remove the remote you specified.                                    |

<div class="pagebreak"></div>

## External Resources & Tutorials

These are just some of the articles, resources & tutorials that I've _"Saved For Later"_ throughout the years, 
all of which are geared towards helping you started with Git & GitHub ...

<br>

<table class="tg">
    <thead>
        <tr>
            <th class="tg-3y4y"><strong style="color: rgba(65, 64, 66, 0.54); font-size: 12px; line-height: 24px;">Description</strong></th>
            <th class="tg-3y4y"><strong style="color: rgba(65, 64, 66, 0.54); font-size: 12px; line-height: 24px;">URL</strong></th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td class="tg-ng8p">
                <strong style="color: #039de7; font-size: 14px; font-weight: bold; line-height: 1.4; padding: 0 10px;">GitHub Learning Lab <span class="arrow">&xrarr;</span></strong>
                <br>
                <em style="color: #92999d; font-size: 12px; font-weight: normal; line-height: 1.4; padding: 0 10px;">
                    Learning resources to help you master Git & GitHub by GitHub.com
                </em>
                <br>
            </td>
            <td class="tg-ng8p">
                <a href="https://bbentley.link/2TBHcMo">https://bbentley.link/2TBHcMo</a>
            </td>
        </tr>
        <tr>
            <td class="tg-pd46">
                <strong style="color: #039de7; font-size: 14px; font-weight: bold; line-height: 1.4; padding: 0 10px;">Set Up Git <span class="arrow">&xrarr;</span></strong>
                <br>
                <em style="color: #92999d; font-size: 12px; font-weight: normal; line-height: 1.4; padding: 0 10px;">
                    The absolute starting point when you're ready to get started with Git by GitHub.com
                </em>
                <br>
            </td>
            <td class="tg-pd46">
                <a href="https://bbentley.link/2EQ0p2u">https://bbentley.link/2EQ0p2u</a>
            </td>
        </tr>
        <tr>
            <td class="tg-ng8p">
                <strong style="color: #039de7; font-size: 14px; font-weight: bold; line-height: 1.4; padding: 0 10px;">Resources To Learn Git <span class="arrow">&xrarr;</span></strong>
                <br>
                <em style="color: #92999d; font-size: 12px; font-weight: normal; line-height: 1.4; padding: 0 10px;">
                    List of useful resources to help you learn how to use Git more effectively by GitHub.com
                </em>
                <br>
            </td>
            <td class="tg-ng8p">
                <a href="https://bbentley.link/2TvXIgL">https://bbentley.link/2TvXIgL</a>
            </td>
        </tr>
        <tr>
            <td class="tg-pd46">
                <strong style="color: #039de7; font-size: 14px; font-weight: bold; line-height: 1.4; padding: 0 10px;">Hello World <span class="arrow">&xrarr;</span></strong>
                <br>
                <em style="color: #92999d; font-size: 12px; font-weight: normal; line-height: 1.4; padding: 0 10px;">
                    learning something new, (such as GitHub) by GitHub.com.
                </em>
                <br>
            </td>
            <td class="tg-pd46">
                <a href="https://bbentley.link/2EQrGBW">https://bbentley.link/2EQrGBW</a>
            </td>
        </tr>
        <tr>
            <td class="tg-ng8p">
                <strong style="color: #039de7; font-size: 14px; font-weight: bold; line-height: 1.4; padding: 0 10px;">Getting Started With Git And GitHub: The Complete Beginner’s Guide <span class="arrow">&xrarr;</span></strong>
                <br>
                <em style="color: #92999d; font-size: 12px; font-weight: normal; line-height: 1.4; padding: 0 10px;">
                    Git and GitHub basics for the curious and completely confused by Anne Bonner.
                </em>
                <br>
            </td>
            <td class="tg-ng8p">
                <a href="https://bbentley.link/2EYB6LA">https://bbentley.link/2EYB6LA</a>
            </td>
        </tr>
        <tr>
            <td class="tg-pd46">
                <strong style="color: #039de7; font-size: 14px; font-weight: bold; line-height: 1.4; padding: 0 10px;">Getting Started with Git <span class="arrow">&xrarr;</span></strong>
                <br>
                <em style="color: #92999d; font-size: 12px; font-weight: normal; line-height: 1.4; padding: 0 10px;">
                    An opinionated tutorial of the various aspects of Git & GitHub by Linode.com.
                </em>
                <br>
            </td>
            <td class="tg-pd46">
                <a href="https://bbentley.link/2EVAxSG">https://bbentley.link/2EVAxSG</a>
            </td>
        </tr>
        <tr>
            <td class="tg-ng8p">
                <strong style="color: #039de7; font-size: 14px; font-weight: bold; line-height: 1.4; padding: 0 10px;">Git Guide <span class="arrow">&xrarr;</span></strong>
                <br>
                <em style="color: #92999d; font-size: 12px; font-weight: normal; line-height: 1.4; padding: 0 10px;">
                    Just a simple guide for getting started with Git. no deep shit 😉 by Roger Dudler.
                </em>
                <br>
            </td>
            <td class="tg-ng8p">
                <a href="https://bbentley.link/2TtV9Mg">https://bbentley.link/2TtV9Mg</a>
            </td>
        </tr>
        <tr>
            <td class="tg-pd46">
                <strong style="color: #039de7; font-size: 14px; font-weight: bold; line-height: 1.4; padding: 0 10px;">Getting Started with Git <span class="arrow">&xrarr;</span></strong>
                <br>
                <em style="color: #92999d; font-size: 12px; font-weight: normal; line-height: 1.4; padding: 0 10px;">
                    Things that you should know before getting started with Git by Atisaya Jain.
                </em>
                <br>
            </td>
            <td class="tg-pd46">
                <a href="https://bbentley.link/2TwYb2g">https://bbentley.link/2TwYb2g</a>
            </td>
        </tr>
        <tr>
            <td class="tg-ng8p">
                <strong style="color: #039de7; font-size: 14px; font-weight: bold; line-height: 1.4; padding: 0 10px;">How You Can Learn Git And Github While You’re Learning To Code <span class="arrow">&xrarr;</span></strong>
                <br>
                <em style="color: #92999d; font-size: 12px; font-weight: normal; line-height: 1.4; padding: 0 10px;">
                    An opinionated tutorial of the various aspects of Git & GitHub by Iago Rodrigues.
                </em>
                <br>
            </td>
            <td class="tg-ng8p">
                <a href="https://bbentley.link/2EQTVAp">https://bbentley.link/2EQTVAp</a>
            </td>
        </tr>
        <tr>
            <td class="tg-pd46">
                <strong style="color: #039de7; font-size: 14px; font-weight: bold; line-height: 1.4; padding: 0 10px;">A Full Tutorial On How To Use Github <span class="arrow">&xrarr;</span></strong>
                <br>
                <em style="color: #92999d; font-size: 12px; font-weight: normal; line-height: 1.4; padding: 0 10px;">
                    An opinionated tutorial of the various aspects of Git & GitHub by George Seif.
                </em>
                <br>
            </td>
            <td class="tg-pd46">
                <a href="https://bbentley.link/2ER7akL">https://bbentley.link/2ER7akL</a>
            </td>
        </tr>
        <tr>
            <td class="tg-ng8p">
                <strong style="color: #039de7; font-size: 14px; font-weight: bold; line-height: 1.4; padding: 0 10px;">Results From A Quick Google.com Search <span class="arrow">&xrarr;</span></strong>
                <br>
                <em style="color: #92999d; font-size: 12px; font-weight: normal; line-height: 1.4; padding: 0 10px;">
                    An <strong>UNLIMITED</strong> list of resources available on Google, which is constantly being updated.
                </em>
                <br>Ó
            </td>
            <td class="tg-ng8p">
                <a href="https://bbentley.link/2TtWcvG">https://bbentley.link/2TtWcvG</a>
            </td>
        </tr>
        <tr>
            <td class="tg-pd46">
                <strong style="color: #039de7; font-size: 14px; font-weight: bold; line-height: 1.4; padding: 0 10px;">Results From A Quick Google Search <span class="arrow">&xrarr;</span></strong>
                <br>
                <em style="color: #92999d; font-size: 12px; font-weight: normal; line-height: 1.4; padding: 0 10px;">
                    An <strong>UNLIMITED</strong> list of resources available on Google, which is constantly being updated.
                </em>
                <br>
            </td>
            <td class="tg-pd46">
                <a href="https://bbentley.link/2TtWcvG">https://bbentley.link/2TtWcvG</a>
            </td>
        </tr>
    </tbody>
</table>

## Copyright & License

Copyright &copy; 2019 [Bruce Bentley](https://brucebentley/.io) under the 
[MIT License]([https://github.com/brucebentley/bootstrap/blob/master/LICENSE](https://github.com/brucebentley/github-learning-lab/blob/master/LICENSE)).
