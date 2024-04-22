---
---

{% include section.html %}

# about us

We use statistical models and geospatial techniques to predict species's
ranges and their relationships with the environment, make estimates of
biodiversity and map its patterns, and predict how biodiversity will
change in the future.

{% include section.html
background="images/forest.png"
size=full dark=false %}

{%capture text%}

#### We investigate how biodiversity is distributed across the Earth and make predictions of how it will change in the future.


{%
  include button.html
  link="projects"
  text="Browse our projects"
  icon="fa-solid fa-arrow-right"
  flip=true
  style="bare"
%}

{% endcapture %}

{%
  include feature.html
  image="images/research.jpg"
  link="projects"
  title="Research Projects"
  flip=true
  style="bare"
  text=text
%}

{% capture text %}

#### Check out our published papers to see what we have been working on.


{%
  include button.html
  link="research"
  text="See our publications"
  icon="fa-solid fa-arrow-left"
  flip=false
  style="bare"
%}

{% endcapture %}

{%
  include feature.html
  image="images/rspb2023.jpg"
  link="research"
  title="Publications"
  text=text
%}


{% capture text %}

#### We are a diverse team that is passionate about modeling, mapping, and monitoring.

{%
  include button.html
  link="team"
  text="Meet our team"
  icon="fa-solid fa-arrow-right"
  flip=true
  style="bare"
%}

{% endcapture %}

{%
  include feature.html
  image="images/photo.jpg"
  link="team"
  title="Our Team"
  flip=true
  text=text
%}

{% include section.html background="images/some-bg-image.jpg" dark=false
size=full %}

# [NEWS](blog)

{% include list.html data="posts" component="post-excerpt" %}