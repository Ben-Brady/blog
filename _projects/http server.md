---
title: "HTTP/1.1 Server"
date: 2022-10-12 +0000
image: 
  path: /images/http.png
  thumbnail: /images/http.png
  caption: "HTTP/1.1 Server"
---

A RFC compliant HTTP/1.1 implementation in python.

After watching James Kettle's amazing research on http desync attacks, I realised how vulnerable over the wire HTTP can be. I decided that if I wanted to fully explore it and find possible areas of attack, I needed to implement it. That way I'd be forced to understand how HTTP/1.1 works and where possible areas of attack would be. It also helped me to gain more understand on how sockets worked.

Originally, I had planned to implement it in Rust as way to learn that more, however the development was too slow
