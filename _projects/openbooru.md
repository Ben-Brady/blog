---
title: "Openbooru"
date: 2021-10-27 +0000
image: 
  path: /images/openbooru.png
  thumbnail: /images/openbooru.png
  caption: "Openbooru"
---

[Openbooru](https://ptr.openbooru.org) is a modern implementation of a booru written in Sveltekit and Python.

I orinally wanted to create a modern framework for boorus. A booru is a imageboard that can be searched with through tags, this is often used to showcase [Fan-art](https://booru.newblood.games/post/list). In the mid-2000s, the competition in this area was very fierce, however over time the most frameworks are based on old design practices or have become overcome with technical debt.

My implementation was written in two parts, the frontend web-gui and the backend api server with the two parts being entirely seperate. The intention was to make it so that anyone could implement a gui for the booru as long as they wrote it compatible with the API. This meant I could offload the front-end design to the community as this was my first foray into web design.

The front-end was originally written in plain react, then next.js, and I'm currently moving to sveltekit, the however the changes between frameworks weren't that difficult as I the code was designed to be portable. The backend is written in python using FastAPI with the database, this is the part I really hammered away at as I have a lot of experience.
