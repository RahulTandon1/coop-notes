Maven has:

- Conventions on how stuff should work
- POM
- Plugin architecture

Will do the following

- [ ] Artifacts
- [ ] Coordinates
- [ ] Dependencies
- [ ] Elements and uses of pom.xml
- [ ] Maven build lifecycle and plugins

  

Some env var setup

  

-e, -X flags

  

**Basic Maven Concepts**

  

  

  

  

- WAR != JAR

  

POM Outline:

- groupId, artifactId, version -> uniquely define a Maven project
- Packaging - type of artifact e.g. jar, war
- Properties - symbols referenced in POM
- Dependencies
- Build - config of tasks to exec to build the project
- Profiles - customises the pom for different use cases

  

GAV coordinates

- Uses 5 elements (coordinate) to identify Maven artificers
- artifactId : groupID : packaging : version : classifier