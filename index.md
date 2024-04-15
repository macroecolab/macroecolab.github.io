---
---

{% include section.html %}

{% capture text %}

We investigate how biodiversity is distributed across the Earth and make predictions of how it will change in the future.

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

Check out our publications to see what we have been working on.


{%
  include button.html
  link="research"
  text="See our publications"
  icon="fa-solid fa-arrow-right"
  flip=true
  style="bare"
%}

{% endcapture %}

{%
  include feature.html
  image="images/photo.jpg"
  link="research"
  title="Published Papers"
  text=text
%}


{% capture text %}

We are a diverse team that is passionate about modeling, mapping, and monitoring.

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
  text=text
%}
