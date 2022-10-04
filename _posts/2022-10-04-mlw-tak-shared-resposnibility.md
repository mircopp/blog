---
layout: post
title:  "Building Trust as a Service - A Shared Responsibility Approach for Data Platforms at CentralNic Group PLC"
author: mirco
categories: ['Data Engineering', 'Conceptual Design', 'Data Governance', 'Data Observability']
tags: [ Observable ]
image: assets/images/paw_industry_40.png
rating: 4.5
comments: true
toc: true
---


> “Where there is data smoke, there is business fire.”
> -- <cite>Thomas Redman</cite>

The famous quote from Thomas Redman aka the data doc shows a well known but still underestimated issue with using data for supporting decision making processes that is becoming more and more important for companies nowadays.
The problem can be easily described as a type of domino effect: If there are issues with the data right at the source, the impact on the business side will become much bigger possibly leading to wrong decisions. On the analytics side, AI systems consume data to recommend or take actions with further impact. Being supplied with "bad" data, these prediction algorithms can easily being tricked by the noise leading to poor performance and, again, wrong decisions in the business context.

This blog post is used as the basis of my talk at the Machine Learning Week Europe 2022 in Berlin. In the coming chapters, I will summarize the most important points around governance of our data platforms. Mor specifically, I will explain how we make use of a shared responsibility concept in order to build a more robust data ecosystem that focusing on detecting and tackling data quality issues in a structured way. The goal of this overall approach is to generate more trust of the data consumers into the information extracted from the data that leads to more transparent and better decision making processes.


# About CentralNic Group
Founded in 1996, over the years CentralNic became one of the most important providers of internet infrastructure tools in the world. What started as a registry operator selling top level domains to a handful of verified registrars, today is managing the end-to-end supply chain for domain names and related web services. The product portfolio of the group is structured in two areas: The Online Presence segment focusses on supporting companies in their overall online appearance (domain names, hosting plans, brand protection, security services and many more) while the Online Marketing segment consists of everything around monetizing traffic on the internet (domain parking, media buying services, search engines etc.).

CentralNic mainly grew this broad offering of different products by acquiring many companies that are experts in their area over the years. Having that said, each of the brands comes with its individual systems and software producing vast amounts of data of various types. Besides the software, the data produced by the services is sitting as well with the brands separately resulting in data silos. On the other hand, most of the business departments are working collaboratively. So for example, finance departments are merged together and reporting requires numbers from every single brand aggregated together. Other departments like marketing, sales or legal have other, but related requirements. This led us to think about a solution to centralize the data somehow to make it available for the business side faster while reducing efforts going to reporting initiatives of the engineering teams sitting with the brands. Our main goal was to break up the data silos to build a **reliable, complete and secure** single source of truth that can be trusted by all its data stakeholders. So let's have a look at the problem at hand and what motivates us to think about how to share responsibility between the parties involved.

TODO: Add picture of the history of acquisitions.

# Motivation
The bottom line of every data platform is that if it is not trusted by its users, it won't be particularly useful for anyone. According to a Gartner survey, “72% of data and analytics leaders [...] are unsure how to build the ‘trusted data foundation’ needed to accelerate their efforts and achieve business goals” [TODO Reference].

To tackle this issue, while building the platform, we also took into consideration how to build a solid data governance structure around it. Basically, there are two famous approaches how to govern a modern data ecosystem:
* **Data Lake**: Centralization of the data in a data lake that is administered and governed by a central data team [TODO 5]
* **Data Mesh**: Distribution of the data across a variety of data producers that are providing information about their products separately [TODO 3,4]

Both approaches have interesting implications. With a data mesh you would basically have the system experts taking care of the reporting probably resulting in higher data quality. On the other hand, data lakes help you to unify data structures across brands resulting in a more consistent reporting allowing for cross-brand aggregations.

However, there are also plenty of disadvantages of both strategies as well. Basically, the advantage of the one is probably the disadvantage of the other. So for example, while a data lake allows you to standardize and centralize reporting activities resulting in more efficient use of software engineering capacities, the data mesh would basically duplicate the whole reporting process for every single brand.

All these concerns motivate us to think further and to ask the following questions first:
* Which are the stakeholders of our data platform, the so-called data stakeholders?
* What are their individual needs?
* How can we make use of the existing approaches to build a solid governance infrastructure that improves trust in the data?

In the following chapters, these questions will be answered. So let's have a look at the data stakeholders first.

# Data Stakeholders

From a top-level perspective, we distiguish three different types of stakeholders that require interaction with the data platform:

*  **Data producers**: In our case, these are mostly software engineering teams working on systems that produce most of the data that is needed. Besides that, there is also IT, sales and product teams producing different data (logs, spreadsheets, project management reports) on a daily basis.
*  **Data keepers**: All data related roles taking care of the information flowing in the organization consisting of data engineers, data analysts and data scientists.
* **Data consumers**: Mainly business departments that require data for their reporting initiatives (finance, sales, marketing) but also different other roles that require to consume data on a regular basis such as data scientists in order to build their models.

Each of them come with different goals that are consistently challenging a central data platform and the governance that comes with it. Let's have a closer look at what they require individually.

## Data producer
* Reduction of work for reporting i.e. ad-hoc requests, monitoring, etc. through automation
* High data quality e.g. accurate numbers
* Transparency to the management board

## Data keeper

* Integration of data sources into the overall data architecture
* Prevention of data downtime (“bad data”)
* Democratization of data in the organization

## Data consumer

* Specific reports to support decision making
* Interactive data exploration
* Data-based process automation (e.g. marketing campaigns)
* Analysis of the data
* Reliability and trust

