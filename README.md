# Analyzing Success

# Abstract
Open source projects are the backbone of today's technology. We find them in
programming languages that are at the core of any software (e.g. Luna or Rust),
frameworks that shape the web (e.g. Laravel, React or Angular), toolkits that
help scientists handle and analyse data (e.g. numpy, pandas) or development
tools used by all software teams around the world (e.g. git), to give a few
examples.

Do successful open source projects have common patterns? Through this project,
we hope to gain some insight into what contributes to the success of an open
source project. This might allow us to define what a successful project is,
and formulate some guidelines that might be beneficial to other projects'
success.

# Notebooks

- `data_pipeline.ipynb`: this is the main notebook explaining our data pipeline
  (milestone 2).
- `retrieve_gitential_datasets.ipynb`: this notebook handles the retrieval of
  the Gitential datasets (our main dataset). This is because the Gitential
  dataset is actually organized/split in several directories, with links to
  download the full dataset for each directory. (The dataset on the EPFL
  cluster only contains samples.)
- `retrieve_additional_data_github.ipynb`: this notebook handles the retrieval
  and creation of two related datasets (Github issues/pull requests and their
  comments) using the Github API, in order to enrich our main dataset

# Data files

We include samples of our data in this git repo. For more info about our
datasets, please refer to `data_pipeline.ipynb`.

```
data/
    datasets/ <- See `retrieve_gitential_datasets.ipynb` for details
        project1/
            blames.json.gz
            commits.json.gz
            patches.json.gz
            tags.json.gz
        project2/
            ...
    gitential_datasets_repo/ <- Gitential dataset (original, incomplete)
        project1/
            README.md
            blames.sample.csv
            commits.sample.csv
            patches.sample.csv
            tags.sample.csv
        project2/
            ...
    github_comments.csv <- See `data_pipeline.ipynb` / `retrieve_additional_data_github.ipynb` for details
    github_issues.csv  <- See `data_pipeline.ipynb` / `retrieve_additional_data_github.ipynb` for details
    reddit_results.txt  <- See `data_pipeline.ipynb` for more info
```

# Research questions
- *How many contributors are there, and are there time patterns to when they
  submit their changes?*

**Gitential data**: we plan to look at the number of unique authors
(`author_name` and `author_name_dedup`, whichever is not NaN) for each project,
and analyze the `committer_time` for each person and globally.

---

- *Is there a certain roles distribution among contributors to the project? For
  example, do successful projects have people who focus on refactoring code,
  adding features or fixing bugs?*

**Gitential data**: we plan to answer this by analysing the commits data. For
example, `loc_d`, `loc_i`, `comp_d`, and `comp_i` can be used to detect people
who focus on refactoring code or enforce style guidelines. `nfiles` could
identify people who focus on small or large amounts of files at once, which
could indicate bug fixes/small features versus larger feature
additions/overhauls. Commit messages (`message`) can be parsed to identify
several types of commits. For example: commits that fix issues (e.g. by looking
at keywords such as 'Closes' or 'Fixes'), or commits that merge another
person's pull requests (by looking for 'Merges ...' commits).

---

- *Are there certain patterns to the commits, such as commit messages length,
  size or frequency of the commits, etc?*

**Gitential data**: we can analyse possible patterns in the columns `message`,
`nfiles` (for the size of the commits) and `committer_time` (for the
frequency).

---

- *Are contributors part of a small community/team (e.g. real-life development
  teams), or are they independent contributors?*

**Gitential data**: we plan to analyze this by checking `committer_email` and
`committer_email_dedup` and parsing the domain of the email (e.g. people from
the Microsoft team will have `@microsoft` emails), whereas more diverse people
are more likely to have their unique email hosts or common email hosts (e.g.
`@hotmail` or `@gmail`).

---

- *Can we relate the success / popularity to a responsive / helpful community
  (e.g. StackOverflow / Reddit subreddits)?*

**StackOverflow dataset**: we plan to count the number of questions related to
each of these projects (by making use of `_Tags`), and compute the average
response time (using `_CreationDate` and `_PostTypeId`, to get the difference
between the question and the first answer). We also plan to check the response
time of accepted responses (not just the first answer), by using the
`_AcceptedAnswerId` column. Additionally, `_AnswerCount` can also be used as an
indicator of a thriving community.

**Reddit dataset**: we plan to count the number of posts and comments about
each project, as well as posts in a subreddit for projects that have a
subreddit dedicated to them. We might have to focus on certain
programming-related subreddits to avoid false matches.

---

- *Can we gain some insight from GitHub issues for a project? For example, the
  number of open/closed issues or the response time.*

**GitHub API issues**: we plan to do this by looking at the columns `state`,
`closed_at` and `created_at` (time for resolution), as well as `created_at` /
`parent` for the comments to get the response time.

---

- *Could sentimental analysis of commit messages or issue reports be
  meaningful? (GitHub API comments)*

**Gitential data**: we plan to analyze commit messages (`message`) with an
Python library (NLTK).

**GitHub API comments**: similarly, we plan to analyze issue body texts
(`body`).

---

- *Does the choice of programming language play a role in the success of a
  project?*

We were planning to check the `patches` Gitential datasets for this at first,
but we decided to drop this idea after futher consideration, as a proper
statistical analysis would probably require thousands of Git projects (24 data
points is not sufficient, since this is a very simple and one-dimensional data
point).

---

- *Similarly, can projects' licenses or codes of conduct provide us with some
  insight?*

We were planning to use the Github API to get data for this, but we decided to
drop it as well for similar reasons as above.

---

- *Are contributors focused around certain parts of the project?*

**Gitential data**: we decided to postpone this for now due to potential time
constraints, as we consider the other questions to be more important. If time
allows it, we might be able to explore this at a later stage by checking the
`patches` Gitential datasets.

# Dataset
- [Gitential Datasets for Open Source
  Projects](https://github.com/gitential/datasets) is the main dataset
  we're using. It covers 24 popular open source projects. This provides us with
  information about each commit, including a commit's author and email (which
  we could use to determine if certain authors are part of a small community,
  e.g. they all have "@epfl.ch" emails), changes summary (e.g. number of lines
  added/removed, which might be useful to determine the role of an author --
  for instance, someone who mostly refactors code will probably have more
  removed lines per commit), date and so on.
- We also make use of the [GitHub API](https://developer.github.com/v3/)
  to retrieve a project's issues/pull requests and comments.

To be able to relate the projects to their community on other websites, we also
use the following datasets:
- [StackOverflow public data dump](https://meta.stackexchange.com/questions/2677/database-schema-documentation-for-the-public-data-dump-and-sede).
- [Reddit comments](http://academictorrents.com/details/85a5bd50e4c365f8df70240ffd4ecc7dec59912b).
  We search for keywords in posts' titles, comments and the names of subreddits
  to determine the popularity of a certain project.

# A list of internal milestones up until project milestone 3
- For our presentation, we plan to answer each of our research questions listed
  above, in order to present a story that shows common patterns among
  successful projects.
