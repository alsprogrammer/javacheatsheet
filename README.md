# My ultimate Java cheatsheet

## The aim

This repository has been created to help me recall programming elements,
concepts, keywords and the other stuff that can be of use when you are using
Java.

The basic idea beneath this all is you tend to forget about the things you are
not using at the moment so anyhow you will forget something. This is the first
place (at least for me) to take a look before start looking somewhere else.

In anyone except me finds it useful, you can use it for your own needs too ;)

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
