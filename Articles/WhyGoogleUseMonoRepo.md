# In progress...

# Why Google Stores Billions of Lines of Code in a Single Repository
##### [link](https://cacm.acm.org/magazines/2016/7/204032-why-google-stores-billions-of-lines-of-code-in-a-single-repository/fulltext)
Article about managing one of the biggest codebase

## Content Overview
  - [Google's tooling and workflows](#googles-tooling-and-workflows)
    - [Tools](#tools)
    - [Google workflow](#google-workflow)
  - [Analys](#analys)
    - [Advantages](#advantages)
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
Of course, custom code analysis [Tricorder] helps create more strong review process.
In the first step of big changes over the codebase, developers create big patches with Rosie (another tool), then split the large ones into smaller patches testing them independently, sending them out for code review, and committing them automatically once they pass tests and a code review.
Fun fact: Rosie creates nearly 7 thousand commits every year (from 2013 to 2015).

## Analys

### Advantages

1. Unified versioning, one source of truth.
   
   Google codebase has only a mainline and every team shouldn't think about others' work and new code.

2. Extensive code sharing and reuse.
   
   The Google codebase includes a wealth of useful libraries and all of them are reused from team to team.

3. Simplified dependency management.
   
   They reduced some problems by static linking and others by having conditional flags on different parts of the repo.

4. Atomic changes.
   
   Strongly checked and reviewed changes into one main line.

5. Large-scale refactoring.
   
   It is easy for testing and benchmarking big changes before they are committed.

6. Team boundaries are fluid.
   
   Collaboration across teams, flexible team boundaries, and code ownership.
   
7. Code visibility and clear tree structure providing implicit team namespacing
   
   Another attribute of a monolithic repository is the layout of the codebase is easily understood, as it is organized in a single tree. Each team has a directory structure within the main tree that effectively serves as a project's namespace. Each source file can be uniquely identified by a single string file path that optionally includes a revision number. 

For example, let's see the advantages of this kind of repository for the compilers team. The monolithic repository provides the team with full visibility of how various languages are used at Google and allows them to do codebase-wide cleanups to prevent changes from breaking builds or creating issues for developers. This greatly simplifies compiler validation, thus reducing compiler release cycles and making it possible for Google to safely do regular compiler releases (typically more than 20 per year for the C++ compilers).

> An important aspect of Google culture that encourages code quality is the expectation that all code is reviewed before being committed to the repository.

## Used articles and resources
 - [What version control system does Google use and why](https://www.quora.com/What-version-control-system-does-Google-use-and-why#:~:text=What%20source%20control%20does%20Google,internally%20developed%20system%20called%20Piper.&text=Google's%20monolithic%20repository%20provides%20a,of%20developers%20around%20the%20world.)
 - [What is google repository like](https://softwareengineering.stackexchange.com/questions/41435/what-is-googles-repository-like)
 - [Paxos in simple words](https://www.researchgate.net/publication/358603298_Understanding_Paxos_and_other_distributed_consensus_algorithms)
 - [Development at Google (video)](https://www.infoq.com/presentations/Development-at-Google/)
 - [Code review](https://abseil.io/resources/swe-book/html/ch09.html#code_review-id00002)
 - [Build in the cloud](https://google-engtools.blogspot.com/2011/08/build-in-cloud-how-build-system-works.html)

[Paxos6]:<https://en.wikipedia.org/wiki/Paxos_(computer_science)>
[Critique]:<https://abseil.io/resources/swe-book/html/ch19.html>
[Tricorder]:<https://static.googleusercontent.com/media/research.google.com/ru//pubs/archive/43322.pdf>
