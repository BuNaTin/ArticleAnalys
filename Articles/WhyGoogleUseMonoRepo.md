# In progress...

# Why Google Stores Billions of Lines of Code in a Single Repository
##### [link](https://cacm.acm.org/magazines/2016/7/204032-why-google-stores-billions-of-lines-of-code-in-a-single-repository/fulltext)
Article about managing one of the biggest codebase

## Content Overview
  - [Google's tooling and workflows](#googles-tooling-and-workflows)
    - [Tools](#tools)
    - [Google workflow](#google-workflow)
  - [Used articles and resources](#used-articles-and-resources)

## Google's tooling and workflows
### Tools
Google uses Piper to store its codebase. Piper contains all repo and is distributed over 10 Google data centers around the world, relying on the [Paxos6] algorithm to guarantee consistency across replicas. 
Workflow with Piper:
1. Sync user codebase with repo
2. Create a local copy of files and change them
3. Push changes to the workspace
4. Reviewing changes
5. Commit them to the central repository

Many people have access to Piper by cloud-based storage system Clients in the Cloud - working this way, you'll have only changed files on your local machine without cloning all repositories.
Google practices trunk-based development on top of the Piper source repository. 
Most engineers work at the "head," or most recent, version of a single copy of the code called "trunk" or "mainline." All changes come to the repo separately in serial ordering.
They also did not have a "developers" branch, cause all changes are saved in new files (and old ones are stored together). These old/new files using configuration are based on conditional flags. They make it possible to exclude new files and changes if something goes wrong or create A/B experiments for users.

### Google workflow

Google uses "pre-submit" infrastructure that provides automated testing and analysis of changes before they are added to the codebase, to reduce bad code in their mono repository.
As well they have interesting politics of accepting changes. Cause their repo has a tree-based structure, every folder has an owner who'll accept or reject every change to files in their scope of view. Owners are usually engineers who work with the project under their directory.
Code Reviews in Google should be written really with a capital letter: they include design, functionality, complexity, testing, naming, comment quality, and code style, as documented by the various language-specific Google style guides.
And yes, they had the specific tool for that - [Critique].

## Used articles and resources
 - [What version control system does Google use and why](https://www.quora.com/What-version-control-system-does-Google-use-and-why#:~:text=What%20source%20control%20does%20Google,internally%20developed%20system%20called%20Piper.&text=Google's%20monolithic%20repository%20provides%20a,of%20developers%20around%20the%20world.)
 - [What is google repository like](https://softwareengineering.stackexchange.com/questions/41435/what-is-googles-repository-like)
 - [Paxos in simple words](https://www.researchgate.net/publication/358603298_Understanding_Paxos_and_other_distributed_consensus_algorithms)
 - [Development at Google (video)](https://www.infoq.com/presentations/Development-at-Google/)

[Paxos6]:<https://en.wikipedia.org/wiki/Paxos_(computer_science)>
[Critique]:<https://abseil.io/resources/swe-book/html/ch19.html>
