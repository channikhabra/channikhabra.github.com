---
title: "Secure Software Teams Trantor"
date: 2019-08-26T16:07:32+05:30
tags: ["security", "trantor"]
---

{{< slidescom "channikhabra/secure-software-teams" >}}

I gave this talk in one of internal sessions at Trantor. Goal was to acquaint
one of our software teams into the world of application security. This was a
basic talk, just to familiarize attendees with basic information security
concepts. I leveraged this opportunity to propose setting up a Red Team in
Trantor.

As practical part of this session, I created a docker based virtual lab with
webgoat set up. During the session we went through some of the exercises, rest
were left for the attendees as homework. Here's the `docker-compose.yml` file
that was used in the session.

```yaml
version: '3'
services:
  webgoat:
    image: webgoat/webgoat-8.0
    environment:
      - WEBWOLF_HOST=webwolf
      - WEBWOLF_PORT=9090
    ports:
      - "8080:8080"
      - "9001:9001"
    volumes:
      - ./docker-volumes/webgoat-home:/home/webgoat/.webgoat
  webwolf:
    image: webgoat/webwolf
    ports:
      - "9090:9090"
    command: --spring.datasource.url=jdbc:hsqldb:hsql://webgoat:9001/webgoat --server.address=0.0.0.0
```

To start the lab, simply create a directory, save above snippet as
`docker-compose.yml`, and run `docker-compose up` in it. You will then be able
to access webgoat on http://localhost:8080/WebGoat