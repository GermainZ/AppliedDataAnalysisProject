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

# Research questions
- How many contributors are there, and are there time patterns to when they
  submit their changes?
- Is there a certain roles distribution among contributors to the project?
  For example, do successful projects have people who focus on refactoring
  code, adding features or fixing bugs?
- Are contributors focused around certain parts of the project?
- Are there certain patterns to the commits, such as commit messages length,
  size or frequency of the commits, etc?
- Does the choice of programming language play a role in the success of a
  project?
- Are contributors part of a small community/team (e.g. real-life development
  teams), or are they independent contributors?
- Can we relate the success / popularity to a responsive / helpful community
  (e.g. StackOverflow / Reddit subreddits)?
- Can we gain some insight from GitHub issues for a project? For example,
  the number of open/closed issues or the response time.
- Similarly, can projects' licenses or codes of conduct provide us with some
  insight?
- Could sentimental analysis of commit messages or issue reports be meaningful?

# Dataset
- [Gitential Datasets for Open Source
  Projects](https://github.com/gitential/datasets) will be the main dataset
  we're using. It covers 24 popular open source projects. This provides us with
  information about each commit, including a commit's author and email (which
  we could use to determine if certain authors are part of a small community,
  e.g. they all have "@epfl.ch" emails), changes summary (e.g. number of lines
  added/removed, which might be useful to determine the role of an author --
  for instance, someone who mostly refactors code will probably have more
  removed lines per commit), date and so on.
- We might also make use of the [GitHub API](https://developer.github.com/v3/)
  to retrieve a project's issues/pull requests, or project licenses/codes of
  conduct.

To be able to relate the projects to their community on other websites, we will
use the following datasets:
- [StackOverflow public data dump](https://meta.stackexchange.com/questions/2677/database-schema-documentation-for-the-public-data-dump-and-sede).
  We can search for certain tags or keywords in posts' titles to determine the popularity of a certain project.
- [Reddit comments](http://academictorrents.com/details/85a5bd50e4c365f8df70240ffd4ecc7dec59912b).
  We can search for keywords in posts' titles or the names of subreddits to
  determine the popularity of a certain project.
  We might also make use of the [Reddit API](https://www.reddit.com/dev/api/)
  to retrieve more recent or more specific data (e.g. for certain subreddits,
  such as /r/programming).

# A list of internal milestones up until project milestone 2
- Obtain, explore and clean the data if necessary.
- Build additional datasets using the APIs we listed above.
- Look for efficient ways to answer the research questions listed above.
- Explore possibilities for visualizing our data and answers.
- Figure out how to relate our different datasets for additional insight.

# Questions for TAs
- Is our project idea suitable for the required theme ("Data science for social
  good")?
- Is our goal feasible considering our dataset (~25 popular open source
  projects)? If not, we can expand the dataset ourselves to include even more
  repos.
