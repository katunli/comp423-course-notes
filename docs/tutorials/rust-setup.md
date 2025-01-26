# Setting up a dev container for Rust

* Primary author: [Katun Li](https://github.com/katunli)
* Reviewer: [Hamzah Yousuf](https://github.com/hamzahyous)<br>
<br>

Welcome to the Rust Dev Container tutorial! This guide will help you set up a development container for Rust programming in a blank directory. By the end, you'll have a working environment to write, compile, and run a simple Rust program that prints "Hello COMP423."

## __Prerequisites__

Before getting started, make sure you have:

1. __Visual Studio Code (VSCode)__.
2. __Docker__ installed and running.
3. __Git installed__
4. __A Github account__
5. Basic familiarity with Git and the command line.

<br>
# Part 1. Project Setup: Creating the Repository

## __Step 1: Starting a Blank Directory__

1. Open your terminal or command prompt.
2. Create a Local Directory and navigate into it
```bash
mkdir rust-project
cd rust-project
```

3. Initialize a new Git repository:
```bash
git init
```

4. Create a README file:
```bash
echo "# Rust project using dev container" > README.md
git add README.md
git commit -m "Initial commit with README"
```

## __Step 2: Creating a Remote Repository on Github__

1. Log in to your GitHub account and navigate to the [Create a New Repository](https://github.com/new) page.

2. Fill in the details as follows:
    - __Repository Name__:  ```rust-dev-container-guide```
    - __Description__: "A development container for Rust  programming made using a guide"
    - __Visibility__: Public

3. Do not initialize the repository with a README, .gitignore, or license.

4. Click __Create Repository__.

## __Step 3. Link your Local Repository to GitHub__

1.  Add the GitHub repository as a remote:
```bash
git remote add origin https://github.com/<your-username>/rust-dev-container-guide.git
```

Replace ```<your-username>``` with your GitHub username.

2. Check your default branch name with the subcommand ```git branch```. If it's not ```main```, rename it to ```main``` with the following command: ```git branch -M main```.

3. Push your local commits to the Github repository:
```git push --set-upstream origin main```

4. Back in your web browser, refresh your GitHub repository to see that the same commit you made locally has now been pushed to remote. You can use ```git log``` locally to see the commit ID and message which should match the ID of the most recent commit on GitHub. This is the result of pushing your changes to your remote repository.

# Part 2. Setting up the Development Environment

## __Step 1. Add Development Container Configuration__

1. In VS Code, open the ```rust-project``` directory. You can do this via: File > Open Folder.

2. Install the __Dev Containers__ extension for VS Code.

3. Create a __.devcontainer__ directory in the root of your project with the following file inside of this "hidden" configuration directory:

    ```.devcontainer/devcontainer.json```

4. Within ```devcontainer.json``` insert the following:

``` json
{
    "name": "Rust Dev Container",
    "image": "mcr.microsoft.com/devcontainers/rust:latest",
    "customizations": {
        "vscode": {
            "settings": {},
            "extensions": ["rust-lang.rust-analyzer"]
        }
    },
    "postCreateCommand": "rustc --version"
}
```

The ```devcontainer.json```  file defines the configuration for your development environment. Here, we're specifying the following:

- ```name```: A descriptive name for your dev container.

- ```image```: Specifies the base image for Rust from Microsoft's container registry.

- ```customizations```: Adds useful configurations to VS Code, like installing the Rust extension. When you search for VSCode extensions on the marketplace, you will find the string identifier of each extension in its sidebar. Adding extensions here ensures other developers on your project have them installed in their dev containers automatically.

- ```postCreateCommand```: A command to run after the container is created. In our case, it will check the Rust compiler version by running rustc --version.

## __Step 2. Reopen the Project in a VSCode Dev Container__

Reopen the project in the container by pressing Ctrl+Shift+P (or Cmd+Shift+P on Mac), typing "Dev Containers: Reopen in Container," and selecting the option. 

Once your dev container setup completes, close the current terminal tab (trash can), open a new terminal pane within VSCode, and try running ```rustc --version``` to see your dev container is running a recent version of Rust. <br>
<br>

# Part 3. Create and Write the Rust Program

## __Step 1. Create a New Rust Binary Project__

In the terminal inside the container, create a new Rust binary project and navigate into it:

```bash
cargo new hello-comp423 --vcs none
cd hello-comp423
```

!!! Note

    ```--vcs none``` is a flag that specifies that no version control system (VCS) should be initialized with the new project. By default, when you create a new Rust project using Cargo, it may initialize a Git repository (if Git is available and configured on your system). Using the --vcs none option prevents this automatic initialization.

## __Step 2. Write the Simple Program__

Edit ```src/main.rs``` to the following:
```rust
fn main() {
    println!("Hello COMP423");
}
```
<br>

# Part 4. Compile and Run the Program

## __Step 1. Compile the Program__

In the terminal run the following command:
```bash
cargo build
```

!!! Explanation

    This is similar to using gcc to compile a C program, as seen in COMP 211. This command compiles your project and creates an executable file. By default, the executable is placed in the target/debug/ directory for debug builds.

## __Step 2. Run the Program__

To run the executable, you can use the following command from the project root directory:

```bash
./target/debug/hello-comp423
```

## __Alternative to Build__

In the terminal run the following command:

```bash
cargo run
```

- __Difference to build__: ```cargo build``` compiles the program but does not run it, while ```cargo run``` combines both steps for convenience.<br>
<br>

# Conclusion

With this setup, you're ready to dive into Rust development with a fully functional and isolated Dev Container!