# crev-proofs

This repository exists to support auditing our dependencies. The basic idea is that this repository will link to individual developers' own `crev-proofs` repositories, which will 

## Setup

This is a simplification of the 

### Setup a Repository

The first thing to do when setting up a personal repository is to create a new repository on your own GitHub account named `crev-proofs`. To do this, you can run:

```bash
gh repo create crev-proofs \
    --add-readme \
    --description "Crev Proofs Repository" \
    --disable-issues \
    --disable-wiki \
    --license Apache-2.0 \
    --public
```

You don't need to maintain a local clone of this repository in order to use crev, the utility will handle that for you.

### Install Crev

Next, you'll need to install and setup crev (this assumes rustup and the stable toolchain are installed). You'll want to keep your password manager handy for this:

```bash
# Install crev
cargo +stable install cargo-crev

# Create a new "ID" for yourself that's linked to your github repository.
# This will prompt for a password, and you should use a secure random
# password (e.g. 20+ characters) that is saved in a password manager.
cargo crev id new --github-username $GITHUB_USERNAME


# Trust the upstream MobileCoin Foundation repository
cargo crev id trust --level high https://github.com/mobilecoinfoundation/crev-proofs

# Publish the changes to your repository to github.
cargo crev publish
```

At this point, you should [open an issue](https://github.com/mobilecoinfoundation/crev-proofs/issues/new) against this repository asking to have your repository marked as trusted. Once it's been completed, your reviews will be included in the foundation's review set.

## Reviewing a New Crate

In order to review a crate, you'll want to go into a repository that contains the dependency you want to review, and then review it. For example, to review the `tempfile` dependency for the first time:

```bash
cd sgx
cargo crev open tempfile --cmd 'clion dontReopenProjects nosplash --wait' --cmd-save
```

<details>
  <summary>VScode</summary>

```bash
cargo crev open tempfile --cmd "code --wait -n" --cmd-save
```
</details>

<details>
  <summary>VIM</summary>

VIM users can browse the source directory and examine files as they like via:

```bash
cargo crev open
```
</details>

Once you've gone through all the code in the crate, you can write a review.

### Writing a Review

You can start writing a review using the review sub-command:

```bash
cargo crev review tempfile
```

This will give a "review proof document" that will describe your review. The most important thing is to be honest in your assessment of your own review, in particular the `thoroughness` and `understanding` elements:

```yaml
# Package Review of default 0.1.2
review:
  thoroughness: low
  understanding: medium
  rating: positive
comment: ""


# # Creating Package Review Proof
#
# A Package Review Proof records results of your review of a version/release
# of a software package.
#
# ## Responsibility
#
# It is important that your review is truthful. At very least, make sure
# to adjust the `thoroughness` and `understanding` correctly.
#
# Other users might use information you provide, to judge software quality
# and trustworthiness.
#
# Your Proofs are cryptographically signed and will circulate in the ecosystem.
# While there is no explicit or implicity legal responsibiltity attached to
# using `crev` system, other people will most probably use it to judge you,
# your other work, etc.
#
#
# ## Data fields
#
(...)
```

## Reviewing an Updated Crate

TODO: Fill this in once we have a diff to review ;-)
