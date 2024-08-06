# Rust Project Basics

## Starting a Project

There are two kinds of projects you can make with Rust: binary crates and
library crates. To create a binary crate you would run the following:

```
cargo new [project-name]
```

To create a library crate:

```
cargo new [project-name] --lib
```

&nbsp;

## Linking the Project to a Remote Git Repo

By default, `cargo new` will also initialize the project as a git repo. All
that's left to do before you can commit your work is to link it a remote git
repo, but there are a few steps we need to adhere to if we want to do this
smoothly.


### 1. Create the Remote Repo

On github.com, gitlab.com or wherever, create the remote repository.

### 2. Check the Branch Names

In the last few years, Github changed the name of the default branch of a
repository from "master" to "main". As such, if you create a remote repo on
github.com, it will start with only 1 branch called "main". At the time of
writing, however, the commandline utility `git` names the default branch of a
repo "master". This incompatibility can be a small frustration when attempting
to link your Rust project to your remote repo. Luckily it is easily fixed by
updating your git config to have a different default branch name:

```
git config --global init.defaultBranch [default-branch-name]
# I recommend setting the default branch name to "main":
git config --global init.defaultBranch main
```

### 3. Linking our Local Git Repo to the Remote Repo

First, we need to tell our git repo where the origin is:

```
git remote add origin [ssh-path-to-remote-repo]
# For example:
git remote add origin git@github.com:JSpeedie/g2me.git
```

Then we need to git where the upstream is for pushing and pulling:

```
git push --set-upstream origin main
git pull --set-upstream origin main
```

Finally, we need to pull whatever data it is we have on the remote repo:

```
git pull --allow-unrelated-histories
```

We add the `--allow-unrelated-histories` flag because the remote repo likely
has some files we want in the repo (such as a license and possibly a readme),
and the local repo likely has some files we also want in the repo (source
files), but the 2 repos don't have any common history.

### 4. Commit Some Data!

All that's left to do now is to add the files we want to commit, stage a commit,
and push it.

```
git add Cargo.lock
git add Cargo.toml
git add src/main.rs
git commit -m "Added the main files of the project"
git push
```

&nbsp;

## Adding a Dependency to the Project

```
cargo add assert_float_eq
```

&nbsp;

## Viewing Documentation for a Project

Many Rust projects will be complete with documentation accessible via the
command:

```
cargo doc --open
```

&nbsp;

## Testing a Project

### Adding Tests in a Separate File

```
mkdir tests
vim tests/integration_test.rs
```

### Running the Project Tests

Many Rust projects will make use of Rust's testing facilities. You can run
the testing suite using the following:

```
cargo test
```

&nbsp;

## Installing a New Rust Component

For example, let's say we want to install a component like `clippy` so we can
lint our code with `cargo clippy`. First, let's check if the component is
already installed:

```
rustup component list | grep [component-name]
```

If the output of this command is empty, the component is not installed. We can
install the component with the following commands:

```bash
rustup update
rustup component add [component-name]
```

&nbsp;
