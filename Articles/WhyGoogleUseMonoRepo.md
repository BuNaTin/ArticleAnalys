# In progress...

# Why Google Stores Billions of Lines of Code in a Single Repository
##### [link](https://cacm.acm.org/magazines/2016/7/204032-why-google-stores-billions-of-lines-of-code-in-a-single-repository/fulltext)
Article about managing one of the biggest repository

## Content Overview
  - [Table of view](#table-of-view)
  - [Piper](#piper)
  - [Used articles:](#used-articles)

## Piper and CitC
Google use Piper to store their codebase. Piper contains all repo and is distributed over 10 Google data centers around the world, relying on the [Paxos6](https://en.wikipedia.org/wiki/Paxos_(computer_science)) algorithm to guarantee consistency across replicas. 
Workflow with Piper:
1. Sync user codebase with repo
2. Create local copy of files and change them
3. Push changes to workspace
4. Reviewing changes
5. Commit them to the central repository



## Used articles and resources
 - [What version control system does Google use and why](https://www.quora.com/What-version-control-system-does-Google-use-and-why#:~:text=What%20source%20control%20does%20Google,internally%20developed%20system%20called%20Piper.&text=Google's%20monolithic%20repository%20provides%20a,of%20developers%20around%20the%20world.)
 - [What is google repository like](https://softwareengineering.stackexchange.com/questions/41435/what-is-googles-repository-like)
 - [Paxos in simple words](https://www.researchgate.net/publication/358603298_Understanding_Paxos_and_other_distributed_consensus_algorithms)
 - [Development at Google (video)](https://www.infoq.com/presentations/Development-at-Google/)