---
layout: post
title: sbt Quick Reference
tags: scala
---

## sbt version

This reference is based on sbt 1.3.2. You can check your sbt version with `sbt sbtVersion`.

## Commands

### Official guide

As a good start, you can check the [sbt by example](https://www.scala-sbt.org/1.x/docs/sbt-by-example.html) first. It will give you a glance at how to use the sbt.

### sbt REPL

All the commands below can be run on the sbt REPL, which will speed up the process. You can start the sbt console by entering `sbt` on the terminal under the project folder. When you enter the commands listed below, you should omit the `sbt` in them. For example, `sbt run` just becomes `run` on the REPL.

### Start a new sbt project

```sh
sbt new scala/hello-world.g8
```

This command will create a new sbt project using the hello-world template. [Here](https://github.com/foundweekends/giter8/wiki/giter8-templates) you can find a list of the templates.

### Run the project

```sh
sbt run
```

This command will compile and run the project.

### Compile the project

```sh
sbt compile
```

This command will compile the project only.

### Watch the change of the project and compile

```sh
sbt ~compile
```

### Run the tests

```sh
sbt test
```

## Settings

### Add a new repository for downloading package

Edit the build.sbt file under the project folder. Add the line to the file

```
resolvers +=
  "Sonatype OSS Snapshots" at "https://oss.sonatype.org/content/repositories/snapshots"
```

This will add a new repository named "Sonatype OSS Snapshots" to you sbt project using the URL [https://oss.sonatype.org/content/repositories/snapshots](https://oss.sonatype.org/content/repositories/snapshots). You can add the new repositories using the pattern. When you add the new repository, beware of the conflict of the repository naming.

For more information about the resolvers, please check the [sbt manual on Resolvers](https://www.scala-sbt.org/1.x/docs/Resolvers.html).

## Copyright

This post is written by chryoung. You can copy/paste if you cite the source.
