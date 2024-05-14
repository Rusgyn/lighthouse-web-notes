# Rusgyn Magsanay's Notes
Lighthouse Labs - Web Development Bootcamp

## Summary

This repository contains all of the notes taken by [Rusgyn Magsanay](https://github.com/Rusgyn/lighthouse-web-notes) for the Lighthouse Labs Web Development Bootcamp.

## Initializing A New Project

> #### Instruction
> Create a directory in your `/lighthouse` folder called `lighthouse-web-notes`.

```shell
cd /lighthouse
```
```shell
mkdir lighthouse-web-notes
```
This will server as the project directory

> #### Instruction
> Switch into your newly created directory

```shell
cd lighthouse-web-notes
```

> #### Instruction
> Initialize a new repor in this directory.

```shell
git init
```

> #### Instruction
> Create a README.file (called README.md) using the terminal.

```
touch README.md
```

> #### Instruction
> Add the README.md file to the repository

```
git add README.md
```

> #### Instruction
> Commit your changes and push to github

```
git commit -m "Black README.md added"
```

## Pushing to GitHub

> #### Instruction
> Create a new and completely empty repository with the same name on Github
> ###### WARNING
> Make sure to leave the checkbox next to 'Initialize this repository with a README' empty because we will be create our own README file
>
> Add the URL of the new repo as a remote on your local repo

```
git remote add origin <URL>
```
Replace <URL> with the URL of your repo

```
git remote add origin <URL>
```

> #### Instruction
> Push your changes to Github.

```
git push -u origin main
```

## Links
We can create a link with the following Markdown syntax:
```
[Link Text](URL)
```

> #### Instruction
> Add links to the summary
>
> Edit the summary so that [Your Name] is a link to your GitHub profile and the words Lighthouse Labs are a link to the Lighthouse Labs website.

```
...taken by [Joel](https://github.com/JoelCodes) for the...
```
> #### Instruction
> Confirm that your changes are reflected on Github.

## Creating a Table of Contents Using Lists
When we finally add notes to our repository, we want to be able to easily get to a desired folder from the main repository page. For this we can create a table of contents, which will be a list of links to the folders in our repository.

> #### Instruction
> Add an appropriately sized 'Table of Contents' header.
> Create a nested list under the header.

Add the following Markdown below the 'Table of Contents' header

```
- [Week 1](https://github.com/Rusgyn/lighthouse-web-notes/tree/main/Week_1)
  - [Day 1](https://github.com/Rusgyn/lighthouse-web-notes/tree/main/Week_1/Day_1)
```
