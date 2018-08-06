# Strime :video_camera: :fire:

1. [Presentation](#presentation)
    1. [History](#history)
    2. [Team](#team)
    3. [Milestones](#milestones)
    4. [Thanks](#thanks)
2. [Architecture](#architecture)
3. [Installation](#installation)
    1. [Encoding application](#encoding-application)
    2. [API](#api)
    3. [Website](#website)
4. [How to contribute](#how-to-contribute)
    1. [What can be improved](#what-can-be-improved)
    2. [I found a bug](#i-found-a-bug)
    3. [I've got an idea](#ive-got-an-idea)
5. [FAQ](#faq)
6. [Credits](#credits)


## Presentation

Strime is video project management service created to help video producers gather feedback from their client. Instead of sending a file *via* a service like Google Drive, WeTransfer, FromSmash, or Dropbox, and waiting for your client to send you his comments in a fuzzy email, you can upload your video on Strime, share a link with your client, and your client will just have to write down his comments directly on the video.


### Team

Franck Haegeli | Jean-Philippe Cabaroc | Romain Biard
-------------- | --------------------- | ------------
Former war reporter and specialized in animation for more than sixteen years. His experience (sometimes painful) with his clients is the starting point of Strime. | Graphic designer for more than 10 years, Jean-Philippe worked in communication agencies before becoming an independent. He strived to make Strime beautiful and usable. | Fierce and sharp developer, Romain is also a fan of running. He was responsible of making Strime functional and he sweated to make the tool as powerful as possible.
[@larbrenoir](https://twitter.com/larbrenoir) | [@cabaroc](https://twitter.com/cabaroc) | [@rombiard](https://www.twitter.com/rombiard)
[L'arbre noir](www.larbrenoir.fr) | [@cabaroc](https://cabaroc.com/) | [Bobby Digital](https://www.bobbydigital.io/en)<br />[Bobby Photography](https://www.bobby-photography.com/en)


### History

[Strime](https://www.strime.io) was created in 2015 by 3 french people, in Saint-Etienne. The idea came from Franck, who is a video producer and was looking for such a tool to work with his clients. After some research, he realized that a couple of tools existed but all of them were only accessible in english. Nonetheless, the french market is a very language-sensitive market and very little of his client would have been able to use a platform only accessible in english.
Moreover, some of them had a pretty complex interface, designed by video experts for video experts.
He then decided to gather a small team around him to create something that would first be dedicated to the french market, with the goal to be dead simple in order to be widely adopted by the client, because if the client doesn't adopt it, it's pointless.
They won a grant delivered by their region in France and the professional organization [Numelink](http://www.digital-league.org/) for this project, they also integrated [Startup Chile](http://www.startupchile.org/) in february 2017.
In april 2018 they took the decision to take down the company for economical reasons, and to open source the code of the platform, in order for the project to keep living and to offer a solution for those who might be interested in having their own Strime installation.


### Milestones

- February 2015: Idea
- April 2015: Won the Numelink (now Digital League) grant
- July 2015: Incorporation
- January 2016: Launch of the beta
- June 2016: Left the beta and launch of the freemium model
- January 2017: Dropping the freemium model
- February 2017: Integration of the acceleration program Startup Chile
- March 2017: Launch of the english version
- April 2017: Launch of the spanish version
- June 2017: 2nd to the Lab4+ pitch contest in the creative industry category
- April 2018: Decision to take down the service
- July 2018: Open sourcing the code
- September 2018: Closing the website


### Thanks

Some people that helped to the development of Strime have to be thanked:
- Numelink (now [Digital League]((http://www.digital-league.org/))) for their grant and support
- [Saint-Etienne Métropôle](https://www.saint-etienne-metropole.fr) for their support
- [Startup Chile](http://www.startupchile.org/) / [Corfo](https://www.corfo.cl/) for their grant and support
- [iOweb](https://www.ioweb.fr/) / [Datailor](http://www.datailor.fr/) for their advices (and more specifically [Yannis Mazzer](https://github.com/ymazzer))
- Pedro Vargas Ruiz for his work on the spanish translation


## Architecture

### The main principles

Strime is designed in 3 different applications:
- the first one to run the website
- the second one which is the API
- the third one which is an encoding API

We decoupled it into these 3 apps to be able to better handle the resources and split it into different servers to make it scale.

All of them are developed under [Symfony](https://symfony.com/) 2.8, which is a PHP framework.

### Our production architecture

When Strime was running on production, it was first running on 3 different servers: 1 for the website, 1 for the API, and 1 for the encoding API.

This evolved over time, when we began working with [Yannis](https://github.com/ymazzer) to include load balancing, more security with a private network, etc...

### Simplifying the architecture

What you highly advice is you separate the encoding API from the rest on the infrastructure. Indeed, the encoding process, is very demanding in terms of resources, and when you have it running on your server, it occurs that the rest of the applications are inaccessible because of the memory consumed by the encoding API.

2 servers is then the minimal configuration for a stable and efficient infrastructure.

On our side, we used Ubuntu 16.04, PHP7.0, MySQL and [Nginx](https://www.nginx.com/) to make Strime run on our servers. We also used [Let's Encrypt](https://letsencrypt.org/) for the SSL certificates, [PHP-FFMPEG](https://github.com/php-ffmpeg/php-ffmpeg) and therefore [FFMPEG](https://ffmpeg.org/) for the video conversion.

### A word on FFMPEG

In order to work properly, FFMPEG _HAS TO_ [be compiled](https://trac.ffmpeg.org/wiki/CompilationGuide) and not installed through a package installer like APT-GET. This is particularly important to include the support of x265 and other specific codecs.

### Additional services

Strime is also connected to 3rd party services. You will want to create a free [Sendgrid](https://sendgrid.com/) account for handling the emails, a free [Mailchimp](https://mailchimp.com/) account to store the list of subscribers to your mailing list, create a [Slack](https://slack.com/) channel in which we will notify you when some critical actions occurs on your application.

But more importantly, you will need AWS S3 buckets to store your content. You'll need one for the videos, one for the comments (the generated thumbnails), one for the audios and one for the images.

If you want to allow your users to login with Google, you will need to create an API access in the console, and if you want to use Facebook, an app ID.

On our end, we also used Hubspot during some time for marketing purposes, and eventually dropped it, but it can still be configured.

## Installation


### Encoding application


### API


### Website


## How to contribute

You can contribute to each application individually. The best way to proceed is to create pull requests.

Since these applications are no longer maintained by the founding team, you can also fork them, and make them evolve as you see fit, for your own needs, but contributing to a global, open source project, is always nice.


### What can be improved

- [ ] writing unit tests
- [ ] upgrade each app to a newer version of Symfony


### I found a bug


### I've got an idea


## FAQ


### Can I remove Strime's brand and use mine instead?


### ...


## Credits
