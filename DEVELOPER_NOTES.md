



## Table of contents

- [Introduction](#1-introduction)
    - [What is Bittensor?](#what-is-bittensor)
    - [What is the purpose of Bittensor?](#what-is-the-purpose-of-bittensor)
- [Architecture](#2-architecture)
    - [Overview of Bittensor's architecture](#overview-of-bittensors-architecture)
    - [How the different components interact?](#how-the-different-components-interact)
- [Main Components](#3-main-components)
    - [Wallet](#wallet)
    - [Neurons](#neurons)
    - [Subtensor](#subtensor)
    - [Metagraph](#metagraph)
- [Developer Notes](#4-developer-notes)
    - [Coding Standards](#coding-standards)
        - [Coding Style](#coding-style)
        - [Git Commit style](#git-commit-style)
            - [1. Atomic Commits](#1-atomic-commits)
            - [2. Separate subject from body with a blank line](#2-separate-subject-from-body-with-a-blank-line)
            - [3. Limit the subject line to 50 characters](#3-limit-the-subject-line-to-50-characters)
            - [4. Use the imprative mood in the subject line](#4-use-the-imperative-mood-in-the-subject-line)
            - [5. Wrap the body at 72 characters](#5-wrap-the-body-at-72-characters)
            - [6. Use the body to explain what and why vs. how](#6-use-the-body-to-explain-what-and-why-vs-how)
    - [Debug](#debug)
        - [Installation](#installation)
        - [Wallets](#wallets)
        - [Querying the Network](#querying-the-network)
        - [Debugging Miners](#debugging-miners)
        - [Debugging Validators](#debugging-validators)
        - [Debugging with the Bittensor package](#debugging-with-the-bittensor-package)
    - [Testing](#testing)
        - [Running Tests](#running-tests)
        - [Writing Tests](#writing-tests)
        - [Mocking](#mocking)
        - [Test Coverage](#test-coverage)
        - [Continuous Integration](#continuous-integration)
    - [Development Workflow](#development-workflow)
        - [Main branches](#main-branches)
        - [Development model](#development-model)
            - [Feature branches](#feature-branches)
            - [Release branches](#release-branches)
            - [Hotfix branches](#hotfix-branches)
            - [Git operations](#git-operations)
            - [Create a feature branch](#create-a-feature-branch)
            - [Merge feature branch into staging](#merge-feature-branch-into-staging)
            - [Create release branch](#create-release-branch)
            - [Finish a release branch](#finish-a-release-branch)
            - [Create the hotfix branch](#create-the-hotfix-branch)
            - [Finishing a hotfix branch](#finishing-a-hotfix-branch)

# 1. Introduction
What is Bittensor?
----------------------
Bittensor is an open-source project that aims to create a decentralized network for AI model training. It allows AI models to learn from each other in a decentralized manner, improving their performance and capabilities.

What is the purpose of Bittensor?
----------------------
The purpose of Bittensor is to democratize AI model training. By creating a decentralized network, it allows anyone to contribute to the training of AI models and benefit from their use.

# 2. Architecture
Overview of Bittensor's architecture
---------------
Bittensor's architecture consists of several key components, including the Bittensor protocol, the wallet, neurons, subtensor, and the Metagraph. These components work together to create a decentralized network for AI model training.

How the different components interact?
------
Neurons in the Bittensor network interact with the Metagraph, a decentralized ledger that keeps track of the state of the network. The wallet is used to manage the tokens that are used for incentives in the network. The subtensor is a lower-level protocol that handles communication between neurons.

# 3. Main Components
Bittensor Protocol
--------------------------
The Bittensor protocol is the backbone of the network. It defines how neurons communicate with each other and with the Metagraph.

Wallet
-----------------
The wallet is used to manage the Bittensor tokens that are used as incentives in the network. It allows users to earn tokens for contributing to the training of AI models and spend tokens to use trained models.

Neurons
------------------
Neurons are the nodes in the Bittensor network. They represent AI models that are learning from the network.

Subtensor
--------------------
Subtensor is a lower-level protocol that handles communication between neurons. It ensures that data is transfered securely and efficiently across the network.

Metagraph
-------------------
The Metagraph is a decentralized ledger that keeps track of the state of the Bittensor network. It records which neurons are part of the network and how they are connected.

# 4. Developer Notes


Coding Standards
------------------

### Coding Style
Use `black` to format your python code before commiting for consistency across such a large pool of contributors. Black's code [style](https://black.readthedocs.io/en/stable/the_black_code_style/current_style.html#code-style) ensures consistent and opinionated code formatting. It automatically formats your Python code according to the Black style guide, enhancing code readability and maintainability.

Key Features of Black:

    Consistency: Black enforces a single, consistent coding style across your project, eliminating style debates and allowing developers to focus on code logic.

    Readability: By applying a standard formatting style, Black improves code readability, making it easier to understand and collaborate on projects.

    Automation: Black automates the code formatting process, saving time and effort. It eliminates the need for manual formatting and reduces the likelihood of inconsistencies.

### Git Commit Style

Here’s a model Git commit message when contributing:
```
Summarize changes in around 50 characters or less
More detailed explanatory text, if necessary. Wrap it to about 72
characters or so. In some contexts, the first line is treated as the
subject of the commit and the rest of the text as the body. The
blank line separating the summary from the body is critical (unless
you omit the body entirely); various tools like `log`, `shortlog`
and `rebase` can get confused if you run the two together.
Explain the problem that this commit is solving. Focus on why you
are making this change as opposed to how (the code explains that).
Are there side effects or other unintuitive consequences of this
change? Here's the place to explain them.
Further paragraphs come after blank lines.
 - Bullet points are okay, too
 - Typically a hyphen or asterisk is used for the bullet, preceded
   by a single space, with blank lines in between, but conventions
   vary here
If you use an issue tracker, put references to them at the bottom,
like this:
Resolves: #123
See also: #456, #789
```
#### 1. Atomic Commits
An “atomic” change revolves around one task or one fix.

Atomic Approach
 - Commit each fix or task as a separate change
 - Only commit when a block of work is complete
 - Commit each layout change separately
 - Joint commit for layout file, code behind file, and additional resources

Benefits

- Easy to roll back without affecting other changes
- Easy to make other changes on the fly
- Easy to merge features to other branches

*Caveat*: When working with new features, an atomic commit will often consist of multiple files, since a layout file, code behind file, and additional resources may have been added/modified. You don’t want to commit all of these separately, because if you had to roll back the application to a state before the feature was added, it would involve multiple commit entries, and that can get confusing.

#### 2. Separate subject from body with a blank line

Not every commit requires both a subject and a body. Sometimes a single line is fine, especially when the change is so simple that no further context is necessary. 

For example:

    Fix typo in introduction to user guide

Nothing more need be said; if the reader wonders what the typo was, she can simply take a look at the change itself, i.e. use     git show or git diff or git log -p.

If you’re committing something like this at the command line, it’s easy to use the -m option to git commit:

    $ git commit -m"Fix typo in introduction to user guide"

However, when a commit merits a bit of explanation and context, you need to write a body. For example:

    Derezz the master control program

    MCP turned out to be evil and had become intent on world domination.
    This commit throws Tron's disc into MCP (causing its deresolution)
    and turns it back into a chess game.

Commit messages with bodies are not so easy to write with the -m option. You’re better off writing the message in a proper text editor. [See Pro Git](https://git-scm.com/book/en/v2/Customizing-Git-Git-Configuration).

In any case, the separation of subject from body pays off when browsing the log. Here’s the full log entry:

    $ git log
    commit 42e769bdf4894310333942ffc5a15151222a87be
    Author: Kevin Flynn <kevin@flynnsarcade.com>
    Date:   Fri Jan 01 00:00:00 1982 -0200

     Derezz the master control program

     MCP turned out to be evil and had become intent on world domination.
     This commit throws Tron's disc into MCP (causing its deresolution)
     and turns it back into a chess game.


#### 3. Limit the subject line to 50 characters
50 characters is not a hard limit, just a rule of thumb. Keeping subject lines at this length ensures that they are readable, and forces the author to think for a moment about the most concise way to explain what’s going on.

GitHub’s UI is fully aware of these conventions. It will warn you if you go past the 50 character limit. Git will truncate any subject line longer than 72 characters with an ellipsis, thus keeping it to 50 is best practice.

#### 4. Use the imperative mood in the subject line
Imperative mood just means “spoken or written as if giving a command or instruction”. A few examples:

    Clean your room
    Close the door
    Take out the trash

Each of the seven rules you’re reading about right now are written in the imperative (“Wrap the body at 72 characters”, etc.).

The imperative can sound a little rude; that’s why we don’t often use it. But it’s perfect for Git commit subject lines. One reason for this is that Git itself uses the imperative whenever it creates a commit on your behalf.

For example, the default message created when using git merge reads:

    Merge branch 'myfeature'

And when using git revert:

    Revert "Add the thing with the stuff"

    This reverts commit cc87791524aedd593cff5a74532befe7ab69ce9d.

Or when clicking the “Merge” button on a GitHub pull request:

    Merge pull request #123 from someuser/somebranch

So when you write your commit messages in the imperative, you’re following Git’s own built-in conventions. For example:

    Refactor subsystem X for readability
    Update getting started documentation
    Remove deprecated methods
    Release version 1.0.0

Writing this way can be a little awkward at first. We’re more used to speaking in the indicative mood, which is all about reporting facts. That’s why commit messages often end up reading like this:

    Fixed bug with Y
    Changing behavior of X

And sometimes commit messages get written as a description of their contents:

    More fixes for broken stuff
    Sweet new API methods

To remove any confusion, here’s a simple rule to get it right every time.

**A properly formed Git commit subject line should always be able to complete the following sentence:**

    If applied, this commit will <your subject line here>

For example:

    If applied, this commit will refactor subsystem X for readability
    If applied, this commit will update getting started documentation
    If applied, this commit will remove deprecated methods
    If applied, this commit will release version 1.0.0
    If applied, this commit will merge pull request #123 from user/branch

#### 5. Wrap the body at 72 characters
Git never wraps text automatically. When you write the body of a commit message, you must mind its right margin, and wrap text manually.

The recommendation is to do this at 72 characters, so that Git has plenty of room to indent text while still keeping everything under 80 characters overall.

A good text editor can help here. It’s easy to configure Vim, for example, to wrap text at 72 characters when you’re writing a Git commit.

#### 6. Use the body to explain what and why vs. how
This [commit](https://github.com/bitcoin/bitcoin/commit/eb0b56b19017ab5c16c745e6da39c53126924ed6) from Bitcoin Core is a great example of explaining what changed and why:

```
commit eb0b56b19017ab5c16c745e6da39c53126924ed6
Author: Pieter Wuille <pieter.wuille@gmail.com>
Date:   Fri Aug 1 22:57:55 2014 +0200
   Simplify serialize.h's exception handling
   Remove the 'state' and 'exceptmask' from serialize.h's stream
   implementations, as well as related methods.
   As exceptmask always included 'failbit', and setstate was always
   called with bits = failbit, all it did was immediately raise an
   exception. Get rid of those variables, and replace the setstate
   with direct exception throwing (which also removes some dead
   code).
   As a result, good() is never reached after a failure (there are
   only 2 calls, one of which is in tests), and can just be replaced
   by !eof().
   fail(), clear(n) and exceptions() are just never called. Delete
   them.
```

Take a look at the [full diff](https://github.com/bitcoin/bitcoin/commit/eb0b56b19017ab5c16c745e6da39c53126924ed6) and just think how much time the author is saving fellow and future committers by taking the time to provide this context here and now. If he didn’t, it would probably be lost forever.

In most cases, you can leave out details about how a change has been made. Code is generally self-explanatory in this regard (and if the code is so complex that it needs to be explained in prose, that’s what source comments are for). Just focus on making clear the reasons why you made the change in the first place—the way things worked before the change (and what was wrong with that), the way they work now, and why you decided to solve it the way you did.


Debug
-------------------

### Installation

First, make sure you have Bittensor installed correctly. There are three ways to install Bittensor:

1. Through the installer:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/opentensor/bittensor/master/scripts/install.sh)"
```

2. With pip:

```bash
pip install bittensor
```

3. From source:

```bash
git clone https://github.com/opentensor/bittensor.git
python3 -m pip install -e bittensor/
```

You can test your installation by running:

```bash
python3 -c "import bittensor; print(bittensor.__version__)"
```
### Wallets

Bittensor uses wallets for identity and ownership. Wallets consist of a coldkey and hotkey. Coldkeys store funds securely and operate functions such as transfers and staking, while hotkeys are used for all online operations such as signing queries, running miners, and validating.

Here's how to create a wallet using the Python API:

```python
import bittensor as bt
wallet = bt.wallet()
wallet.create_new_coldkey()
wallet.create_new_hotkey()
print(wallet)
```

### Querying the Network

You can query the Bittensor network using the Python API. Here's an example of how to do this:

```python
import bittensor as bt

# Query through the foundation endpoint.
print(bt.prompt("Heraclitus was a "))
```

### Debugging Miners

Miners in Bittensor are incentivized to contribute distinct forms of value determined by the verification mechanism that that subnetwork’s Validators are running. 

Here's an example of how to register a miner:

```bash
btcli register --netuid <subnetwork uid>
```

Once registered, the miner attains a slot specified by their UID. To view your slot after registration, run the overview command:

```bash
btcli overview --netuid <subnetwork uid>
```

Registered miners can select from a variety of pre-written miners or write their own using the Python API. Here's an example of how to run a miner:

```bash
python3 bittensor/neurons/text_prompting/miners/GPT4ALL/neuron.py --netuid 1
```

### Debugging Validators

Validators in Bittensor are participants who hold TAO. They use a dual proof-of-stake, proof-of-work mechanism called Yuma Consensus. Here's how to stake funds:

```bash
btcli stake --help
```

And here's how to become a delegate available for delegated stake:

```bash
btcli nominate --help
```

### Using the CLI

Bittensor comes with a command-line interface (CLI) called `btcli` that you can use to interact with the network. Here's how to get help on the available commands:

```bash
btcli --help
```

### Debugging with the Bittensor Package

The Bittensor package contains data structures for interacting with the Bittensor ecosystem, writing miners, validators, and querying the network. Here's an example of how to use the Bittensor package to create a wallet, connect to the axon running on slot 10, and send a prompt to this endpoint:

```python
import bittensor as bt

# Bittensor's wallet maintenance class.
wallet = bt.wallet()

# Bittensor's chain interface.
subtensor = bt.subtensor()

# Bittensor's chain state object.
metagraph = bt.metagraph(netuid=1)

# Instantiate a Bittensor endpoint.
axon = bt.axon(wallet=wallet, metagraph=metagraph)

# Start servicing messages on the wire.
axon.start()

# Register this axon on a subnetwork
subtensor.serve_axon(netuid=1, axon=axon)

# Connect to the axon running on slot 10, use the wallet to sign messages.
dendrite = bt.text_prompting(keypair=wallet.hotkey, axon=metagraph.axons[10])

# Send a prompt to this endpoint
dendrite.forward(roles=['user'], messages=['what are you?'])
```

Remember, debugging involves a lot of trial and error. Don't be discouraged if things don't work right away. Keep trying different things, and don't hesitate to ask for help if you need it.

Testing
-------------------------------

### Running Tests

Bittensor uses `pytest` for running its tests. To run all tests, navigate to the root directory of the Bittensor repository and run:

```bash
pytest
```

This will automatically discover all test files (those that start with `test_`) and run them.

If you want to run a specific test file, you can specify it directly. For example, to run the tests in `test_wallet.py`, you would use:

```bash
pytest tests/test_wallet.py
```

Similarly, you can run a specific test within a file by appending `::` and the test name. For example:

```bash
pytest tests/test_wallet.py::test_create_new_coldkey
```

### Writing Tests

When writing tests for Bittensor, you should aim to cover both the "happy path" (where everything works as expected) and any potential error conditions. Here's a basic structure for a test file:

```python
import pytest
import bittensor

def test_some_functionality():
    # Setup any necessary objects or state.
    wallet = bittensor.wallet()

    # Call the function you're testing.
    result = wallet.create_new_coldkey()

    # Assert that the function behaved as expected.
    assert result is not None
```

In this example, we're testing the `create_new_coldkey` function of the `wallet` object. We assert that the result is not `None`, which is the expected behavior.

### Mocking

In some cases, you may need to mock certain functions or objects to isolate the functionality you're testing. Bittensor uses the `unittest.mock` library for this. Here's an example:

```python
from unittest.mock import MagicMock

def test_some_functionality():
    # Create a mock object.
    mock_wallet = MagicMock()

    # Set the return value for a specific function.
    mock_wallet.create_new_coldkey.return_value = "mocked_key"

    # Call the function you're testing.
    result = mock_wallet.create_new_coldkey()

    # Assert that the function behaved as expected.
    assert result == "mocked_key"
```
In this example, we're mocking the `create_new_coldkey` function to return a specific value. This allows us to test how our code behaves when `create_new_coldkey` is called, without actually calling the real function.

### Test Coverage

It's important to ensure that your tests cover as much of your code as possible. You can use the `pytest-cov` plugin to measure your test coverage. To use it, first install it with pip:

```bash
pip install pytest-cov
```

Then, you can run your tests with coverage like this:

```bash
pytest --cov=bittensor
```

This will output a coverage report showing the percentage of your code that's covered by tests.

Remember, while high test coverage is a good goal, it's also important to write meaningful tests. A test isn't very useful if it doesn't accurately represent the conditions under which your code will run.

### Continuous Integration

Bittensor uses GitHub Actions for continuous integration. This means that every time you push changes to the repository, all tests are automatically run. If any tests fail, you'll be notified so you can fix the issue before merging your changes.

You can view the results of these tests in the "Actions" tab of the Bittensor GitHub repository.

Remember, tests are an important part of maintaining the health of a codebase. They help catch issues early and make it easier to add new features or refactor existing code. Happy testing!



Development Workflow
---------
### Main branches
----------------------

Bittensor is composed of TWO main branches, **master** and **staging**

**master**
- master Bittensor's live production branch. This branch should only be touched and merged into by the core develpment team. This branch is protected, but you should make no attempt to push or merge into it reguardless. 

**staging**
- staging is Bittensor's development branch. This branch is being continuously updated and merged into. This is the branch where you will propose and merge changes.

### Development model
---------------------------

#### Feature branches

- May branch off from: `staging`
- Must merge back into: `staging`
- Branch naming convention:
    - Anything except master, staging, finney, release/* or hotfix/*
    - Suggested: `feature/<ticket>/<descriptive-sentence>`

When implementing new features, hotfixes, bugfixes, or upgrades, it is wise to adhere to a strict naming and merging convention, whenever possible.

**Branch naming and merging convention:**


Feature branches are used to develop new features for the upcoming or a distant future release. When starting development of a feature, the target release in which this feature will be incorporated may well be unknown at that point. 

The essence of a feature branch is that it exists as long as the feature is in development, but will eventually be merged into `staging` (to definitely add the new feature to the upcoming release) or discarded (in case of a disappointing experiment).

Generally, you should try to minimize the lifespan of feature branches. As soon as you merge a feature into 'staging', you should immidiately delete the feature branch. This will be strictly enforced. Excess branches creates tech debt and confusion between development teams and parties.

#### Release branches

- Please branch off from: `staging`
- Please merge back into: `staging` then into: `master`
- Branch naming convention:
    - STRONGLY suggested format `release/5.1.0/descriptive-message/creator's-name`

Release branches support preparation of a new production release. Furthermore, they allow for minor bug fixes and preparing meta-data for a release (e.g.: version number, configuration, etc.). By doing all of this work on a release branch, the `staging` branch is cleared to receive features for the next big release.

This new branch may exist there for a while, until the release may be rolled out definitely. During that time, bug fixes may be applied in this branch, rather than on the `staging` branch. Adding large new features here is strictly prohibited. They must be merged into `staging`, and therefore, wait for the next big release.

#### Hotfix branches

- Please branch off from: `master` or `staging`
- Please merge back into: `staging` then into: `master`
- Branch naming convention:
    - REQUIRED format: `hotfix/3.3.4/descriptive-message/creator's-name` 

Hotfix branches are very much like release branches in that they are also meant to prepare for a new production release, albeit unplanned. They arise from the necessity to act immediately upon an undesired state of a live production version. When a critical bug in a production version must be resolved immediately, a hotfix branch may be branched off from the corresponding tag on the master branch that marks the production version.

The essence is that work of team members, on the `staging` branch, can continue, while another person is preparing a quick production fix.

### Git operations

#### Create a feature branch

1. Branch from the **staging** branch.
    1. Command: `git checkout -b feature/my-feature staging`

> Rebase frequently with the updated staging branch so you do not face big conflicts before submitting your pull request. Remember, syncing your changes with other developers could also help you avoid big conflicts.

#### Merge feature branch into staging

In other words, integrate your changes into a branch that will be tested and prepared for release.

- Switch branch to staging: `git checkout staging`
- Merging feature branch into staging: `git merge --no-ff feature/my-feature`
- Pushing changes to staging: `git push origin staging`
- Delete feature branch: `git branch -d feature/my-feature` (alternatively, this can be navigated on the GitHub web UI)

This operation is done by Github when merging a PR.

So, what you have to keep in mind is:
- Open the PR against the `staging` branch.
- After merging a PR you should delete your feature branch. This will be strictly enforced.

#### Create release branch

- Create branch from staging: `git checkout -b release/3.4.0/descriptive-message/creator's_name staging`
- Updating version with major or minor: `./scripts/update_version.sh major|minor`
- Commit file changes with new version: `git commit -a -m "Updated version to 3.4.0"`

#### Finish a release branch

In other words, releasing stable code and generating a new version for bittensor.

- Switch branch to master: `git checkout master`
- Merging release branch into master: `git merge --no-ff release/3.4.0/optional-descriptive-message`
- Tag changeset: `git tag -a v3.4.0 -m "Releasing v3.4.0: some comment about it"`
- Pushing changes to master: `git push origin master`
- Pushing tags to origin: `git push origin --tags`

To keep the changes made in the __release__ branch, we need to merge those back into `staging`:

- Switch branch to staging: `git checkout staging`.
- Merging release branch into staging: `git merge --no-ff release/3.4.0/optional-descriptive-message`

This step may well lead to a merge conflict (probably even, since we have changed the version number). If so, fix it and commit.

After this the release branch may be removed, since we don’t need it anymore:

- `git branch -d release/3.4.0/descriptive-message/creator's-name`

#### Create the hotfix branch

- Create branch from master:`git checkout -b hotfix/3.3.4/descriptive-message/creator's-name master`
- Update patch version: `./scripts/update_version.sh patch`
- Commit file changes with new version: `git commit -a -m "Updated version to 3.3.4"`

Then, fix the bug and commit the fix in one or more separate commits:
- `git commit -m "Fixed critical production issue"`

#### Finishing a hotfix branch

When finished, the bugfix needs to be merged back into `master`, but also needs to be merged back into `staging`, in order to safeguard that the bugfix is included in the next release as well. This is completely similar to how release branches are finished.

First, update master and tag the release.

- Switch branch to master: `git checkout master`
- Merge changes into master: `git merge --no-ff hotfix/3.3.4/optional-descriptive-message`
- Tag new version: `git tag -a v3.3.4 -m "Releasing v3.3.4: descriptive comment about the hotfix"`
- Pushing changes to master: `git push origin master`
- Pushing tags to origin: `git push origin --tags`

Next, include the bugfix in `staging`, too:

- Switch branch to staging: `git checkout staging`
- Merge changes into staging: `git merge --no-ff hotfix/3.3.4/descriptive-message/creator's-name`
- Pushing changes to origin/staging: `git push origin staging`

The one exception to the rule here is that, **when a release branch currently exists, the hotfix changes need to be merged into that release branch, instead of** `staging`. Back-merging the bugfix into the __release__ branch will eventually result in the bugfix being merged into `develop` too, when the release branch is finished. (If work in develop immediately requires this bugfix and cannot wait for the release branch to be finished, you may safely merge the bugfix into develop now already as well.)

Finally, we remove the temporary branch:

- `git branch -d hotfix/3.3.4/optional-descriptive-message`

