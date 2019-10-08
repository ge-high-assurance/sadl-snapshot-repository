# SADL Snapshot Repository

This repository contains snapshot versions of the SADLServer and
Reasoner dependencies since we need these snapshot versions to build
the VERDICT STEM runner and Maven central repositories usually contain
only release versions of dependencies.

We can use this GitHub project as a Maven repository by putting a
repositories section in a pom.xml like this:

**pom.xml**
```xml
<!-- This microrepository has our SADL dependencies -->
<repositories>
    <repository>
        <id>sadl-snapshot-repository</id>
        <url>https://raw.github.com/ge-high-assurance/sadl-snapshot-repository/master/repository</url>
        <snapshots>
            <enabled>true</enabled>
        </snapshots>
        <releases>
            <enabled>false</enabled>
        </releases>
    </repository>
</repositories>
```

I got the idea for using a GitHub project as a Maven repository from
this blog
[article](https://cemerick.com/2010/08/24/hosting-maven-repos-on-github/).

## How to update these SADL snapshot dependencies

- Install Java 8 OpenJDK if needed
- Install Apache Maven if needed
- Check out SADL's AugmentedTypes branch from GitHub
- Start a Maven build in sadl3/com.ge.research.sadl.parent

The first build may take up to one hour since Maven may have to
download many poms and jars into its local repository.  Afterwards,
you will be able to run "git pull" to pull any new SADL changes from
GitHub, run "mvn clean" to delete any old files, and run "mvn install"
to build new files in much less time than the first build will take.

```bash
# clone SADL's GitHub project
git clone git@github.com:crapo/sadlos2.git
# or
git clone https://github.com/crapo/sadlos2.git
# change to the right directory
cd sadlos2/sadl3/com.ge.research.sadl.parent
# change to the right branch
git checkout AugmentedTypes
# delete any old files
mvn clean
# build new files
mvn install
```

- Check out this project from GitHub
- Update the SADL snapshot dependencies
- Commit any new changes back to GitHub

These steps will update the snapshot versions of the SADL 
dependencies in this repository, although any Maven build using
these dependencies will bring in another 10-20 transitive
dependencies as well.  All of these transitive dependencies already
have release versions in the central Maven repositories, so there
is no need to store any of them in this repository too.

```bash
# clone this project
git clone git@github.com:ge-high-assurance/sadl-snapshot-repository.git
# change to this directory
cd sadl-snapshot-repository
# update the SADL snapshot dependencies
mvn install
# add any new files
git add .
# commit any new or changed files
git commit -m "Maven artifacts for 3.2.0-SNAPSHOT"
# push any changes back to GitHub
git push
```
