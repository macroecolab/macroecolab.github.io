---
---

{% include section.html %}

#### At the **Macroecology Lab** at Tohoku University, we conduct research on how biodiversity is distributed across the Earth and predict how it will change in the future.

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
  image="images/photo.jpg"
  link="team"
  flip=true
  text=text
%}

{% include section.html background="images/some-bg-image.jpg" dark=false
size=full %}

# [NEWS](blog)

{% include list.html data="posts" component="post-excerpt" %}