# Week 1 - Day 1

## Gists and Template Repos

What's a Template Repo?
- Template repositories are regular GitHub repositories that are marked as templates. They allow you to create new repositories with the same directory structure, files, and commits as the original template repository.

What are Gists?
- A gist is just another git repository, except that its interface on GitHub's website is designed specifically for quickly and easily sharing code snippets.
- Gists cannot be given names - instead GitHub automatically assigns them a long, cryptic and unmemorable one.
- Gists come in two flavours: public and secret.
  - Public gists: Like public GitHub repos, these gists are searchable and discoverable by anyone.
  - Secret gists: These are neither searchable nor discoverable, but they're not private. They can be viewed by anyone but only as long as they know the gist's URL. This means that if you'd rather share your code snippets only with a few select people and not with the whole wide web, you should make them secret!

What's a Fork?
- A fork is a GitHub operation (not strictly a git command or feature) by which one GitHub user creates their own copy of another GitHub user's existing repository or gist.

Using Cloning and Template Repos
- While forking is used to create a copy of a repository on GitHub, cloning is used to create a copy of a repository on your local machine for local development.

## Linting and Eslint
Code Linting is one part of the solution towards writing maintainable, consistent code.

From any directory in our terminal, please run:

```shell
npm install -g eslint@8.57.0
```

Running eslint

```shell
eslint <file.name>
```

or

```shell
eslint .
```

## Command Line Args
Command line arguments are strings of text used to pass additional information to a program when an application is run through the command line interface (CLI) of an operating system. Command line arguments typically include information used to set configuration or property values for an application.

syntax:

```
$ [runtime] [script_name] [argument-1 argument-2 argument-3 ... argument-n]
```

Why use Command Line Arguments?

* Advantage
  * You can pass information to an application before it starts. 
  * Command line arguments are passed as strings to your program
  * You can pass an unlimited number of arguments via the command line.
  * Command line arguments are used in conjunction with scripts and batch files, which is particularly useful for automated testing.

* Disadvantage
  * the interface has a steep learning curve, so it's difficult for most people to use unless they have a good deal of experience using CLI tools.
  * an be difficult to use unless you're using a desktop or laptop computer, so they're not typically used on smaller devices like phones or tablets.

To run:
The simplest way of retrieving arguments in Node.js is via the process.argv array.

```
$ node processargv.js tom jack 43
```

Here we are passing three arguments to the processargv.js program. 
2nd index = "tom"
3rd index = "jack"
4th index = "43"

The output should look something like this:

```
$ node processargv.js tom jack 43
0 -> /Users/scott/.nvm/versions/node/v4.8.0/bin/node
1 -> /Users/scott/javascript/processargv.js
2 -> tom
3 -> jack
4 -> 43
```

0 index = path to our node executable
1st index = contains the path to the script file
rest = are arguments
