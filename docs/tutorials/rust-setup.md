# Setting up a dev container for Rust

* Primary author: [Ezra Heinberg](https://github.com/ezra45)

* Reviewer: Lixin Yang (https://github.com/lixiny1)

!!! note

    Certain steps in this tutorial will be directly quoted from the [COMP 423 MkDocs tutorial page](https://comp423-25s.github.io/resources/MkDocs/tutorial/)

==Hello and welcome!== This tutorial will teach you how to set up a basic Rust project in a development container. Just follow along with the steps, and enjoy the process!

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

(4) Create a ==README== file:

```shell
echo "# Basic Program in Rust" > README.md
git add README.md
git commit -m "Initial commit with README"
```

### Step 2. Create a Remote Repository on GitHub

(1) Log in to your GitHub account and go to the [Create a New Repository](https://github.com/new) page.

(2) Fill in these details:

* **Repository Name:** ```rust-tutorial```
* **Description:** "A short program written in Rust!"
* **Visibility:** Public

(3) Do not worry about a README, .gitignore, or license for now.

(4) Click Create Repository.

### Step 3. Link your Local Repository to GitHub
(1) Add the GitHub repository as a remote:

```shell
git remote add origin https://github.com/<your-username>/rust-tutorial.git
```
Replace ```<your-username>``` with your GitHub username.

(2) Check your default branch name with the subcommand ```git branch```. If it's not ```main```, rename it to ```main``` with the following command: ```git branch -M main```.

//-m instead of -M (small issue!)

(3) Push your local commits to the GitHub repo:

```shell
git push --set-upstream origin main
```
!!! info
    What is ```--set-upstream```?

    ```git push --set-upstream origin main``` pushes the main branch to the remote repository origin. The ```--set-upstream``` flag sets up the main branch to track the remote branch, meaning future pushes and pulls can be done without specifying the branch name and just writing ```git push origin``` when working on your local ```main``` branch. The corresponding short flag is ```-u```.

(4) In your web browser, refresh your GitHub repository to see that the same commit you made locally has now been pushed to remote. You can use ```git log``` locally to see the commit ID and message which should match the ID of the most recent commit on GitHub.

## Part 2: Setting up a Dev Container

A development container is useful to ensure that your development environment is consistent across different machines. Follow the steps below to configure and create one. 

### Step 1: Add Dev Container Configuration

(1) Open the ```rust-tutorial``` folder in VSCode via File > Open Folder.

(2) Press ```Ctrl-Shift-P``` (```Cmd-Shift-P``` on Mac) and search for **Dev Containers: Add Dev Container Configuration Files**.

(3) Select **Add configuration to workspace**.

(4) Search for and click **Rust**.

(5) Select **bullseye**.

(6) Click **OK** (top right corner) until your ```.json``` file is created.

(4) A ```devcontainer.json``` file is now added to your folder.

### Step 2: Customizing Dev Container for Your Project

When you create the ```.json``` file, it should look like this: 

```json
// For format details, see https://aka.ms/devcontainer.json. For config options, see the
// README at: https://github.com/devcontainers/templates/tree/main/src/rust
{
	"name": "Rust",
	// Or use a Dockerfile or Docker Compose file. More info: https://containers.dev/guide/dockerfile
	"image": "mcr.microsoft.com/devcontainers/rust:1-1-bullseye",

	// Use 'mounts' to make the cargo cache persistent in a Docker Volume.
	// "mounts": [
	// 	{
	// 		"source": "devcontainer-cargo-cache-${devcontainerId}",
	// 		"target": "/usr/local/cargo",
	// 		"type": "volume"
	// 	}
	// ]

	// Features to add to the dev container. More info: https://containers.dev/features.
	// "features": {},

	// Use 'forwardPorts' to make a list of ports inside the container available locally.
	// "forwardPorts": [],

	// Use 'postCreateCommand' to run commands after the container is created.
	// "postCreateCommand": "rustc --version",

	// Configure tool-specific properties.
	// "customizations": {},

	// Uncomment to connect as root instead. More info: https://aka.ms/dev-containers-non-root.
	// "remoteUser": "root"
}
```

We are going to add some things to the file.

(1) Uncomment out the ```customizations``` section and edit it to look like this: 

```json
"customizations": {
	"vscode": {
		"extensions": [
			"rust-lang.rust-analyzer"
		]
	}
}
```

(2) Uncomment out the line that says ```"postCreateCommand": "rustc --version",```

(3) Now, press ```Ctrl-Shift-P``` (```Cmd-Shift-P``` on Mac), search for **Dev Containers: Reopen In Container** and click on it.

## Part 3: Your first Rust program

Congratulations on making it this far! We will now create our first program in Rust.

### Step 1: Create a ```main.rs``` file

(1) Open a new terminal in VSCode and run this command:

```shell
cargo new . --bin --vcs none
```

!!! info
    What does this mean?

    The command ```cargo new . --bin --vcs none``` creates a new Rust project using the Cargo package manager. ```.``` refers to the name of the current directory, which is the one that the project will go in. The ```--bin``` flag specifies that the project being created is a binary crate, which means it will compile into an executable program. The ```--vcs none``` flag disables version control system (VCS) initialization.

(2) Navigate to the ```main.rs``` file (```rust-tutorial``` folder > ```src``` folder > ```main.rs```).

You will notice the file already has some prewritten code in it. This is a simple function that prints **"Hello, World!"** to standard output.

(3) Simply change the text within the ```println!();``` function to ```"Hello COMP423"```, save the file, and you're done with this part!

### Step 2: Compiling and running the program

Now that your program is ready to be run, we will look at two different ways of accomplishing that. 

#### (1) The ```cargo build``` command

The ```cargo build``` command compiles your project but does not run the executable that results.

This is useful if you want to check that your code compiles correctly without executing it.

This is equivalent to running ```gcc``` to compile a program and stopping after the ```a.out``` executable is created.

To try it out, run ```cargo build``` in your terminal in VSCode.

You will see output that looks like this: 

```shell
Compiling rust-tutorial v0.1.0 (/workspaces/rust-tutorial/rust-tutorial)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 1.83s
```

To run it, type this command: ```./target/debug/rust-tutorial```.

#### (2) The ```cargo run``` command

The ```cargo run``` command compiles and builds your Rust program in one step.

This is equivalent to running ```gcc``` to compile a program and subsequently running ```./a.out```.

To try it out, run ```cargo run``` in your terminal in VSCode.

**Congratulations on finishing this tutorial! You should now have a familiarity with some important coding concepts.**