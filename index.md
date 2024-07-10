---
---

{% include section.html %}

### At the **Macroecology Lab** at Tohoku University, we conduct research to better understand how biodiversity is distributed across the Earth, how disturbances like land development and climate change affect biodiversity, and how changes to biodiversity can affect human society. 

### To do this, we use **statistical models** and **geospatial analyses** to predict and map species' ranges and biodiversity patterns, including estimates for **future global scenarios**. We also develop **open-source tools** for the research community and science education.

{% include section.html%}

{%capture text%}

#### Our research **projects** focus on themes in biogeography, ecological modeling, conservation, and ecosystem services.


{%
  include button.html
  link="projects"
  text="Browse our research projects"
  icon="fa-solid fa-arrow-right"
  flip=true
  style="bare"
%}

{% endcapture %}

{%
  include feature.html
  image="images/tree_ecosys.png"
  link="projects"
  flip=true
  style="bare"
  text=text
%}

{% capture text %}

#### Check out our **publications** to see what we are working on.


{%
  include button.html
  link="research"
  text="Browse our publications"
  icon="fa-solid fa-arrow-left"
  flip=false
  style="bare"
%}

{% endcapture %}

{%
  include feature.html
  image="images/research.jpg"
  link="research"
  text=text
%}


{% capture text %}

#### We are a diverse **team** passionate about ecological modeling, mapping, and biodiversity monitoring.

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
  image="images/hanami.jpg"
  link="team"
  flip=true
  text=text
%}

{% include section.html background="images/background2.jpg" dark=false
size=full %}

# [Announcements](blog)

{% include list.html data="posts" component="post-excerpt" %}