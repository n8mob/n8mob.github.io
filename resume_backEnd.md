---
layout: resume
title: Nate Grigg - Expert Skills
---

<h2 class='subtitle'>nate@nategrigg.com<br />+1 801 599 NATE</h2>
I have 20 years of development experience, and an intuitive creativity that is hard to come by in engineers. Combining my creativity with an uncanny knack for abstraction leads me to ingenious technical solutions. Mixing in my natural aversion to inefficiency brings us to truly elegant designs.

# Skills/Technologies
- **Digital**/**Mobile** Strategy (See [Mobile Projects](#mobile-projects) below)
- **Design** and **Implementation** of **Applications** and **Web Services**
- **microservices**
- **REST Web Services**
- **Java**
- **JAX-RS**
- **Spring**
- **Python**
- **Django**
- **Flask**
- **.NET**
- **ASP.NET MVC**
- **.NET Core**
- **Lean Development**
- **SQLite3**
- **PostgreSQL**
- **MySQL**
- **JetBrains IDE's** (**PyCharm**, **IntelliJ IDEA**, **Rider**, **Android Studio**)
- **SwiftUI**
- **Go**
- **Kafka**
- **Docker**
- **AWS**
- **Elastic Beanstalk**
- **RDS**

# Work History

## Senior Software Engineer, Merit International Inc.
### May 2022&ndash;August 2022
**Go**, **Kafka**, **PostgreSQL**, **Google Cloud Platform**

Implementing features in back-end microservices

## Senior Software Engineer, ReliaQuest
### August 2021&ndash;March 2022
**Java** microservices built with **Spring Boot**, **Spring MVC**, and **PostgreSQL** (deployed to **AWS**).

I was the "Squad Lead" for a full-stack team: me and 2 back-end developers, 2 front-end developers, a UX designer, and a product owner.

The project was to port an internal, employee-facing application to be part of ReliaQuest's main customer application, "GreyMatter".

We coordinated with ReliaQuest's Data Engineering team to set up jobs to transfer the data from the active internal app into a **PostgreSQL** database. We also worked with the **DevOps** team to spin up a brand-new **microservice** (developed by the other back-end developers and me) to serve that data to the front end.

The front-end developers on the team built reusable components to display the information to the users of the GreyMatter web app. (Building one of these components for temporary use is my only **REACT** experience.)

We were coordinating beta testing when I left the company.

## Principal Software Engineer, Newfold Digital
### A.K.A. Bluehost
### Dec 2019&ndash;Aug 2021
**Python**, **Django**, **Flask**, **Microservices**, **JSON Web Tokens (JWT)**
I was the Tech Lead on a team with four fellow developers, an engineering manager who coded, and a test engineer.

We built a **Django** microservice from scratch and inherited two **Flask** microservices.

### Content Recommendation System
From scratch, we built a **REST Microservice** in **Django** to recommend helpful links (such as knowledge-base articles) to customers at various page locations in [Bluehost's](https://www.bluehost.com/) web apps.

The service was so helpful, easy to use, and robust, that the marketing team decided to use it to show **Black-Friday Offers** to new and existing customers (in both the U.S. and an international market that represented a lot of growth potential for the company).

### Website Builder Authorization Service
One of the **Flask** microservice that we inherited signed **JSON Web Tokens (JWT)** to authorize users of  Bluehost's new [Website Builder for WordPress](https://www.bluehost.com/help/article/website-builder-getting-started) sites. The service was already running in beta and production; we continued implementing and enhancing it.

### Website Builder API Gateway
We also inherited another **Flask** microservice that routed calls from the new builder back to [Bluehost's](https://www.bluehost.com/) monolithic Hosting Platform.


## Developer, Personal Project: MAGiE
### Nov 2018&ndash;Oct 2019, Ongoing

I released a mobile game, built using the [**Unity**](https://unity3d.com/unity) game engine with **C#** scripting. While implementing it, I built a [small library](https://github.com/n8mob/alpha) for the underlying bit manipulation and used [**NuGet**](https://www.nuget.org/packages/com.corporealabstract.alpha.lib/) to manage that dependency in the **Unity** project. Working on my Mac, I learned about [**dotnet core**](https://docs.microsoft.com/en-us/dotnet/core/about) and the **JetBrains Rider** IDE to make life easier.

While managing beta tests and releases, I earned a new respect for continuous delivery and release management!

The game is called MAGiE, short for MAGnetic Interactive Explorer. The premise is that you have this device that reads binary data from a mag-stripe like on a credit card. The game then presents you with puzzles where you have to decode the bits to read a message, or encode bits to answer a puzzle.

It's lots of fun, you should try it!

[https://magiegame.com/magie/](https://magiegame.com/magie/)

More recently, I have implemented a **Django** app to (1) make creating and modifying puzzles easier and (2) to serve new puzzles to the game without having to redeploy the app to the app store or even upload a new JSON file to a web site.

## Senior Software Engineer, Ancestry, Inc. 
### 2015&ndash;2018
**Java 8**, **JAX-RS**, **REST**, **Microservices**, **Spring Dependency Injection**, **Maven**

### 2016&ndash;2018 Monolith BreakUp and conversion to Microservices
### Commerce department at Ancestry

The whole department was working on replacing a suite of monolithic **.NET** services with **Java 8** "**mini**&zwnj;services". Aiming to build **micro**&zwnj;services, the team ended up building services that were a little larger than intended.

So, while the larger team worked on implementing new features and breaking up the **monolith**, a smaller team (including me) also worked on breaking the **mini**&zwnj;services into **micro**&zwnj;services. The department also spent the last year "lifting and shifting" all of these services (**micro**, **mini**, and **monolithic**) to the **AWS** cloud.

All this while implementing new features and helping the team raise their standards for software excellence. I have written up some case studies about some of this work - *ask me for details!*

### 2015&ndash;2016 Cross-cut Solutions Team
I audited Ancestry's services catalog and assisted teams to integrate their services with the proprietary **Application Performance Monitoring (APM)** solution.

Converted a **.NET Microservice** to **Java 8**

## Senior Software Engineer, Intermountain Healthcare
### 2014&ndash;2015
Non-Profit Healthcare Provider, regional hospital network.

One of two back-end developers on the web team implementing the company's main user-facing web site.

See [REST endpoint...](#rest-endpoint-to-provide-mobile-app-with-content-from-sitecore-content-management-system) in [Mobile Projects](#mobile-projects) below.

**Sitecore** **Content Management System (CMS)**


## Senior Software Engineer, RedBell Real Estate
### 2013&ndash;2014
Added new features to an existing web application for a real-estate services company

**ASP.NET** **Web Forms**, **Microsoft SQL Server**, **Stored Procedures**


## Senior Consultant, Application Development, Avanade Inc.
### 2006&ndash;2013
IT Consulting joint venture from Accenture and Microsoft

### 2013 National Retail Pharmacy
I worked with a national retail pharmacy to integrate what they thought was an abandoned scheduling tool into their new consumer web application. The developers who had built the appointment-scheduling application had all left the company, and the appointment-scheduling in the new app wasn't ready.

I was able to assess the old appointment tool and modify it so it could be shown as an *iframe* in the new web app.

### 2006&ndash;2013 Navitaire Professional Services
I spent many years working with many airline clients with Navitaire's Professional Services group.

Most of the work was advising web developers at the various airlines how to implement custom features in Navitaire's ASP.NET web application.

See: [Mobile Web Application for booking flights](#mobile-web-application-for-booking-flights) and [US Patent 8942991B2](#us-patent-8942991b2-agent-side-traveler-application-for-mobile-computing-devices) below.


## Software Developer in Test, Control4
### 2004&ndash;2006
Home-automation startup, paid internship

I was the first to run Control4's main dashboard application, "Media Controller", on Control4 hardware. We had been running the controller on commodity PC's when the first batch of prototype hardware arrived. I saw that stack of machines and said, "might as well give it a go!"

So I grabbed one of the machines off the pallet and installed the OS and applications.

I also built an application to help a subject-matter-expert test our database of remote-control codes.

### Embedded Linux, C, C++, Custom Test Automation Software in C\#


## Software Engineer, ThoughtLab
### 2002&ndash;2004
Custom web applications using the Lean Development methodology

I immensely enjoyed an on-site visit to one of our customers: a furniture-manufacturing company. Visiting with the people at the company taught us so much about their business and their needs. We really gave them the best features within the project schedule.

### ASP.NET 1.0, 1.1

# Education

## Bachelor of Science, Computer Science<br />University of Utah
### 2002&ndash;2006
