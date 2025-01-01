Notes about website development for this template.

For syntax in .html files that look like this:

{% assign post = site.posts 
  | where_exp: "post", "post.slug == include.lookup"
  | first
  | default: include
%}

Look up Liquid syntax for references on functions you can use to edit them.