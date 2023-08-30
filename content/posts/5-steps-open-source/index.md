---
title: "Getting started with open source contributions in 5 steps"
date: 2023-01-16T09:42:31+01:00
draft: false

showDate : true
showDateUpdated : false
showHeadingAnchors : false
showPagination : false
showReadingTime : false
showTableOfContents : true
showTaxonomies : false 
showWordCount : false
showSummary : false
sharingLinks : false
showEdit: false
showViews: false
showLikes: false
layoutBackgroundHeaderSpace: false

---

## Introduction

Contributing to Open Source Software (OSS) is a daunting task. The sheer number of projects, 
contributors and lines of code can be intimidating. But fear not! I have ventured into the world 
of OSS and come back with a 5 step process that will help you make your first contribution a breeze.

I will be using Github in the examples as it is the place where most open source collaboration happens.

## 1. Shortlist a few projects

While it might seem tempting to just “jump right in”, I recommend taking as much time as needed to first analyze different projects.

If you’ve been using OSS for a while you might already have a list of projects you want to contribute to. If not, a great place to start is to explore different topics on Github [https://github.com/topics](https://github.com/topics)

Here are 2 criteria that can help you decide. The sweet spot lies at the intersection of both.

1. **Based on your interest**. Choosing a project that you find interesting because of the value it adds to the world will bring a lot of satisfaction with each contribution. Even better if you are a user of the project. That will make it easier to understand the source code and you will be the first to reap the benefits of your contribution.
2. **Based on your skills**. Finding a project that uses technologies you are familiar with will make it easier and faster for you to contribute.

{{< alert icon="lightbulb" >}}
Making an open source contribution can be a great opportunity to step outside your comfort zone and try your hand at a new programming language or discover a new framework!
{{< /alert >}}

## 2. A deeper analysis of your project shortlist

Once you have selected a few projects, you will need to look a bit deeper to see which one is the most likely to lead to a successful contribution. Broadly speaking, you will want to choose a project that is not too complex, is welcoming to newcomers and is actively maintained.

Here are a few ways to make this assessment:

→ **Review the CONTRIBUTING.md page**. This page will outline the process that needs to be followed before contributing. Some projects have a very simple contributing process while for others it is more complex. You want to make sure that you will be able to complete all of the tasks outlined.

→ **Check the Pull Request (PR) queue length.** Having a lot of open PRs in the queue is not necessarily a bad thing. It could simply mean that the maintainers have a rigorous process for controlling what goes into the main branch which is a good thing. That being said, the more steps there are the more complicated it will be for you to contribute. A large number of pending PRs could also mean that the maintainers are overwhelmed.

→ **Assess the project complexity**. Complex projects will be harder to contribute to. For example, a distributed software such as Kubernetes will be harder to setup locally than a web app. Look at the project’s documentation for an architecture diagram to get an idea of what it is made up of.

→ **Scan through the open issues**. Are peoples questions answered? Are bug reports addressed? Here you will be able to assess how much the maintainers are engaging with their community versus just sticking to their roadmap. Open issues with the tag “Good first issue” are a sign that the maintainers are encouraging contributions from the community.

## 3. Find an issue to fix.

You will find in the issue tab a list of bug reports and feature requests. Your task here will be to gage how hard it is to solve the issue. While solving issues that are too easy might not be so rewarding, delving into a complex issue that involves many moving parts might be more than you can handle.

{{< alert icon="lightbulb" >}}
Look out for labels “Good first issue”. Also some issues might already outline a possible solution which can steer you in the right direction.
{{< /alert >}}

## 4. Clone, run, reproduce

If you are fixing a bug it is necessary to be able to reproduce it locally. If you are unable to establish the “broken state”, there is no way to establish the “fixed state”. Most projects’ README will have instructions on how to run the project locally.

## 5. Track down the bug

This can be really hard to do if you don’t have a clear process. Even simple web apps will have 1000s of lines of code. It is neither realistic nor useful to attempt to understand every part of the source code. Instead, try to isolate the portion of the source code that holds the logic that you will need to work with. How you do this is highly dependent on the type of project you are working on. For a typical web app, the browser debugger is a good place to start understanding the components that make up the UI and those that are relevant for the work you plan on doing. If you want to contribute to a CLI tool, you will often find that the each CLI command maps to a function or file in the source code.

{{< alert icon="lightbulb" >}}
Write down what you see! I’ve made it a habit that when I start parsing a new project’s source code, I write down all the logical connections between files, functions calls, components,… This is because it is hard to hold all the code logic in your head and easy to get lost in the source code.
{{< /alert >}}


## Wrap up

Making your first open source contribution can be tricky but you will learn so much in the process. Don’t forget that open source software is about collaboration so if you run into difficulties don’t hesitate to ask for help.
While there is much more that goes into completing an open source contribution, I believe these first steps will be very helpful in setting you on the right track. So what are you waiting for? Get coding!