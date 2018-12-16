# Analyzing Success

# [Data story](https://ada-how-i-met-your-data.github.io/)

# Abstract
 Open source projects are the backbone of today's technology . We find them in
 programming languages that are at the core of any software (e.g. Luna or
 Rust), frameworks that shape the web (e.g. Laravel, React or Angular),
 toolkits that help scientists handle and analyse data (e.g. numpy, pandas) or
 development tools used by all software teams around the world (e.g. git), to
 name a few examples.

 **Do successful open source projects have common patterns?**

Through this project, we hope to gain some insights into what contributes to
the success of an open source project. This might allow us to identify common
patterns among successful projects, and formulate some guidelines that might
be beneficial to other projects' success.

# Notebooks

- `milestone3.ipynb`: this is the main notebook. It includes our data
  pipeline, methodology and analysis (milestone 3).
- `retrieve_gitential_datasets.ipynb`: this notebook handles the retrieval of
  the Gitential datasets (our main dataset). This is because the Gitential
  dataset is actually organized/split in several directories, with links to
  download the full dataset for each directory. (The dataset on the EPFL
  cluster only contains samples.) (Unchanged from milestone 2.)
- `retrieve_additional_data_github.ipynb`: this notebook handles the retrieval
  and creation of two related datasets (Github issues/pull requests and their
  comments) using the Github API, in order to enrich our main dataset.
  (Unchanged from milestone 2.)

# Data files

We include samples of our data in this git repo. For more info about our
datasets, please refer to `milestone3.ipynb`.

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
    github_comments.csv <- See `milestone3.ipynb` / `retrieve_additional_data_github.ipynb` for details
    github_issues.csv  <- See `milestone3.ipynb` / `retrieve_additional_data_github.ipynb` for details
    reddit_results.txt  <- See `milestone3.ipynb` for more info
```

# Research questions

1. **How many contributors are there for each repository?**

2. **Can we find a pattern that differentiates authors and committers?**

    1. **Are authors and committers the same?**

    2. **If not, how do we explain the difference? Can this be attributed to a specific role such as "Supervising commits"?**

3. **Is the frequency of the commits similar for the projects?**

4. **Are there time patterns to when contributors submit their changes**

5. **Are contributors part of a small community/team (e.g. real-life development teams)?**

6. **Is there a certain roles distribution among contributors to the project? For example, do successful projects have people who focus on refactoring code, adding features or fixing bugs?**

    1. Based on the number of lines removed/added (per author per project).
    2. Based on commit comments.
    3. Based on commit summary messages' length.

7. **Can we gain some insight from GitHub issues for a project?**

    1. Based on the percentage of closed issues per project.
    2. Based on the resolution time of the issues.
    3. Based on which users handle issues.

8. **Can sentiment analysis on the commit messages / issues provide any insights?**

    1. Based on git commit messages for each project.
    2. Based on the body of each project's GitHub issues.
    3. Based on the comments of each GitHub issue per project.

9. **Can we relate the success / popularity to a responsive / helpful community (StackOverflow / Reddit subreddits)?**

    1. **StackOverflow**:
        1. Based on the number of questions related to each project.
        2. Based on the percentage of resolved questions per project.
        3. Based on the resolution time for questions for each project.
    2. **Reddit**:
        1. Based on the number of threads related to a project.
        2. Based on the evolution of the number of threads over time.

**Dropped research questions**:

- **Does the choice of programming language play a role in the success of a project?**

We were planning to check the `patches` Gitential datasets for this at first,
but we decided to drop this idea after futher consideration, as a proper
statistical analysis would probably require thousands of Git projects (24 data
points is not sufficient, since this is a very simple and one-dimensional data
point).

- **Similarly, can projects' licenses or codes of conduct provide us with some insight?**

We were planning to use the Github API to get data for this, but we decided to
drop it as well for similar reasons as above.

# Datasets
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
  to enrich our main dataset, by retrieving each project's issues/pull requests
  and comments.

To be able to relate the projects to their community on other websites, we also
use the following datasets:
- [StackOverflow public data dump](https://meta.stackexchange.com/questions/2677/database-schema-documentation-for-the-public-data-dump-and-sede).
- [Reddit comments](http://academictorrents.com/details/85a5bd50e4c365f8df70240ffd4ecc7dec59912b).
  We search for keywords in posts' titles, comments and the names of subreddits
  to determine the popularity of a certain project.

# Group members' contributions

We all worked on most tasks, except those specifically noted below. We would
each try to solve the question alone, then meet and discuss our different
approaches (in order to get different opinions and perspectives) to reach our
final answer. We will do the same for the final presentation.

The tasks that were handled individually were handled as follows:

- Gaby: handled StackOverflow analysis, design of the data story.
- Germain: building the GitHub dataset and the Reddit dataset, design of the
  data story, and part of the interactive plots for the data story.
- Jennifer: handled the sentiment analysis, design of the data story, and part
  of the interactive plots for the data story.
