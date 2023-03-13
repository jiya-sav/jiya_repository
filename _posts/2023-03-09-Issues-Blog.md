---
layout: post
---
My first issue:

![]({{ site.url }}{{ site.baseurl }}/assets/img/2023-03-09-Issues-Blog/media/image2.png)

Other Error:

![]({{ site.url }}{{ site.baseurl }}/assets/img/2023-03-09-Issues-Blog/media/image3.png)

What help said (not under my control):  
![]({{ site.url }}{{ site.baseurl }}/assets/img/2023-03-09-Issues-Blog/media/image1.png)

To fix the operational error, I tried many methods. I tried to follow the instructions on slack:

  - > Fix \#1: fixing SQLAlchemy upgrade that changed syntax on how to perform db.create\_all(); must be inside an with app.app\_context():

  - > Fix \#2: default location for databases inside an instance folder; changing the impacted docker-compose.yml

Also, I tried removing the db.init\_app(app) lines in each of our api files.

Finally, I got it to work after recoding the entire api files for recipe.py, recipes.py, and main.py. The flask was running smoothly, and I was even able to connect it to postman:

![]({{ site.url }}{{ site.baseurl }}/assets/img/2023-03-09-Issues-Blog/media/image6.png)

Unfortunately, now the flask is not able to run, so I can’t connect it to my front end. However, it is an easy fix to fetch the api, and I even included a section for it in my current code:

![]({{ site.url }}{{ site.baseurl }}/assets/img/2023-03-09-Issues-Blog/media/image5.png)

My current error:

![]({{ site.url }}{{ site.baseurl }}/assets/img/2023-03-09-Issues-Blog/media/image4.png)
