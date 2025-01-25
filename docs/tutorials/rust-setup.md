# Setting up a dev container for Rust

* Primary author: [Ezra Heinberg](https://github.com/ezra45)

hello! - lixin

!!! note

    Certain steps in this tutorial will be directly quoted from the [COMP 423 MkDocs tutorial page](https://comp423-25s.github.io/resources/MkDocs/tutorial/)

Hello and welcome! This tutorial will teach you how to set up a basic Rust project in a development container. Just follow along with the steps, and enjoy the process!

## Prerequisites

Before you start, be sure you have:

1. **An account on GitHub:** If not, sign up for one on [GitHub](https://github.com/)
2. **Git installed:** You can install it [here](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
3. **VSCode installed:** Download [here](https://code.visualstudio.com/)
4. **Docker installed:** Install it [here](https://www.docker.com/products/docker-desktop/)
5. **A general familiarity with the command line:** This will be helpful as you navigate this tutorial.

## Part 1: Creating the Repository

### Step 1. Create a Local Directory and Initialize Git

(1) Open your terminal or command prompt.

(2) Create a new directory for your project.

``` shell
mkdir rust-tutorial
cd rust-tutorial
```

(3) Initialize a new Git repository:

```shell
git init
```

(4) Create a README file:

```shell
echo "# Basic Program in Rust" > README.md
git add README.md
git commit -m "Initial commit with README"
```

### Step 2. Create a Remote Repository on GitHub

(1) Log in to your GitHub account and go to the [Create a New Repository](https://github.com/new) page.

(2) Fill in the details as follows:

* **Repository Name:** ```rust-tutorial```
* **Description:** "Course notes organized as a static website using Material for MkDocs."
* **Visibility:** Public

(3) Do not initialize the repository with a README, .gitignore, or license.

(4) Click Create Repository.

### Step 3. Link your Local Repository to GitHub
(1) Add the GitHub repository as a remote:

```shell
git remote add origin https://github.com/<your-username>/rust-tutorial.git
```
Replace ```<your-username>``` with your GitHub username.

(2) Check your default branch name with the subcommand ```git branch```. If it's not ```main```, rename it to ```main``` with the following command: ```git branch -M main```. Old versions of git choose the name ```master``` for the primary branch, but these days main is the standard primary branch name.

(3) Push your local commits to the GitHub repository:

```shell
git push --set-upstream origin main
```
!!! info
    Understanding the --set-upstream Flag

    ```git push --set-upstream origin main```: This command pushes the main branch to the remote repository origin. The ```--set-upstream``` flag sets up the main branch to track the remote branch, meaning future pushes and pulls can be done without specifying the branch name and just writing ```git push origin``` when working on your local ```main``` branch. This long flag has a corresponding ```-u```short flag.

(4) Back in your web browser, refresh your GitHub repository to see that the same commit you made locally has now been pushed to remote. You can use ```git log``` locally to see the commit ID and message which should match the ID of the most recent commit on GitHub. This is the result of pushing your changes to your remote repository.

