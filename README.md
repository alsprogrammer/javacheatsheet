# My ultimate Java cheatsheet

## The aim

This repository has been created to help me recall programming elements,
concepts, keywords and the other stuff that can be of use when you are using
Java.

The basic idea beneath this all is you tend to forget about the things you are
not using at the moment so anyhow you will forget something. This is the first
place (at least for me) to take a look before start looking somewhere else.

In anyone except me finds it useful, you can use it for your own needs too ;)

## Credits

This all is based on [Programmers cheatsheet, or "We will google for you"](https://habr.com/ru/post/420741/) article or, to be more precise, on the [link](https://cht.sh/java/:learn).

## Prerequisites

I suppose I'm going to use Java8 (if I migrate to a newer version I make some
improvements and notes here) and maven.

## Get started

Any project starts with its template. Because it's strange not to use some
build automation tool these days, I start with maven (though gradle is good too ;)

### Create a skeleton

We'll start with maven:

    mvn archetype:generate
	-DgroupId={project-packaging}
	-DartifactId={project-name}
	-DarchetypeArtifactId={maven-template}
	-DinteractiveMode=false

For a very simple application like typical HelloWorld we can start with

    mvn archetype:generate -DgroupId=org.asaiapin.quickstart -DartifactId=java-quickstart -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false

Note that *-DartifactId=java-quickstart* sets the folder name for your project.

It would create a simple command-line application that does nothing but printing
'Hello, world!'.

### Making the code compilable and runnable

As we use Java8, we have to tell the maven about that specific version. To do that, let's add some special section into our *pom.xml*:

    <properties>
      <maven.compiler.target>1.8</maven.compiler.target>
      <maven.compiler.source>1.8</maven.compiler.source>
    </properties>

This tells the maven we are going to use Java8.

However, if we try to build (or, strictly speaking, *package* the *.jar* file), we won't get a single *.jar* file that includes all we need to start the application. To do that we need to add another section to the *pom.xml* file:

    <build>
      <plugins>
        <plugin>
          <artifactId>maven-assembly-plugin</artifactId>
          <version>3.1.1</version>
          <configuration>
            <descriptorRefs>
              <descriptorRef>jar-with-dependencies</descriptorRef>
            </descriptorRefs>
          </configuration>
          <executions>
            <execution>
              <id>make-assembly</id> <!-- this is used for inheritance merges -->
              <phase>package</phase> <!-- bind to the packaging phase -->
              <goals>
                <goal>single</goal>
              </goals>
            </execution>
          </executions>
        </plugin>
      </plugins>
    </build>

After that, we can package our system and, if there are no errors, we would get a single *.jar* file in the *target* directory that would be named as it is set in *-DartifactId* option.

### Why bring the unneccessary files with you?

Defenitely you do not want to put the executables into the versioning system (for a lot of good reasons), so let's put a *.gitignore* file into the root directory of your repository.

To make the *target* directory "invisible" for your repository, let us put the line

    target/

to the file.

It will let you exclude the whole directory from your repository.

### What about Lombok?

Lombok is a good framework which makes Java as convenient as Kotlin (well... almost as convenient as :)

So if you are going to make Lombok and Micronaut (which is a good framework too) friends, you need to add the Lombok annotation processor to annotation processor paths just like this:

    <annotationProcessorPaths>
      <path>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
        <version>1.18.0</version>
      </path>
      <path>
        <groupId>io.micronaut</groupId>
        <artifactId>inject-java</artifactId>
        <version>${micronaut.version}</version>
      </path>
    </annotationProcessorPaths>
    
### Additional files

Imagine you need a text (or any other) file for you tests only. For me it was an sql file for [MariaBD4j](https://github.com/vorburger/MariaDB4j).

Just create the directory *resources* in the *src/test* directory, and then create the file you need there. That's all! The file woill be avialable in you calsspath.

### How to run

To run the compiled file you can use command

    java -jar target/{artifact-id}-1.0-SNAPSHOT.jar

If you have a few class that cn be run, you have to choose, perfirming the command

    java -cp target/{artifact-id}-1.0-SNAPSHOT.jar {fully qualified class name to run}

for example

    java -cp target/java-quickstart-1.0-SNAPSHOT.jar org.asaiapin.quickstart.App

