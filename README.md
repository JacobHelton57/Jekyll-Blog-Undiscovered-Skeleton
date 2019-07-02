# About

This repository is the starter blog project to be turned into a full-fledged blog using Jekyll.

By following the below instructions, you should produce a product very similar to my finished product found here:

https://github.com/JacobHelton57/Jekyll-Blog-Undiscovered

Before following these instructions, you will need to [install the Jekyll Gem](https://jekyllrb.com/docs/installation/). This process should be pretty straight forward.

# To-Do:

### Create `_config.yml` in root directory:

    markdown: kramdown
    baseurl: /zen-habits
    permalink: pretty
    exclude: ['README.md']

### Create default layout
1. Add `default.html` layout to `_layouts`
1. Copy entire `index.html` into `default.html`
1. Cut `.home-page` from`default.html` and paste in `index.html` in place of everything else
1. Replace gap in `default.html` with `{{content}}` tag

### Make navbar an included file
1. Create `nav.html` file in `_includes` directory
1. Move the navbar section to `nav.html`
1. Insert `{% include nav.html %}` in default template where nav code was
1. Use `{{site.baseurl}}/` in hrefs
1. Logic for active url

    `{% if page.url == '/' %}active{%endif%}`

1. Do the same thing for the about link using `{{site.baseurl}}/about/`

### Make pagination functioning
1. [Download paginator code](https://gist.github.com/JacobHelton57/86e84ad99d59955f8a5c510010144e6e)
1. Move `paginator.html` into `_includes`
1. Include paginator in `index.html`
1. Update YAML with `paginate: 3`
1. Add the [paginator gem](https://gist.github.com/JacobHelton57/a448d7c8ea3b6617f1dd42b847805586) to the root of the project folder

### Get index.html to grab data from posts
1. Change `posts/` directory name to `_posts/`
1. Delete all but one of the cards: we'll only need one
1. Wrap card with `{% for post in paginator.posts%}` and `{% endfor %}`
1. Add `{{post.title}}` and `{{post.excerpt}}` to `.title` and `.text` fields
1. Replace img url with `{{site.baseurl}}/img/{{post.thumbnail}}`
1. Replace post date with `{{post.date | date: "%b %d, %Y"}}`
1. Replace author name with `{{post.author}}`
1. Replace href to read more button with `{{site.baseurl}}{{ post.url }}`

### Create posts layout
1. Add `post.html` layout to `_layouts`
1. Instead of creating a new layout, we are _extending_ the default layout
1. Copy `.post` div from HTML sample post into `post.html`
1. Replace fields with `{{page.title}}`, `{{page.author}}`, and `{{page.date | date: "%b %d, %Y"}}` tags
1. Replace img url with `{{site.baseurl}}/img/{{page.banner_image}}`
1. Add `{{content}}`
1. Make all posts use post layout by default

        defaults:
          -
            scope:
              path: ""
              type: "pages"
            values:
              layout: "default"
          -
            scope:
              path: ""
              type: "posts"
            values:
              layout: "post"
              category: "blog"
              author: "Jacob Helton"
              banner_image: "900x300.png"
              thumbnail: "750x300.png"

### Make sidebar dynamic
1. Create `sidebar.html` include file and add `{% include sidebar.html %}` to default
1. Loop through 5 most recent posts using `{% for post in site.posts limit:5 %}` & `{% endfor %}`
1. Substitute href for `{{site.baseurl}}/{{post.url}}`, title for `{{post.title}}` and date for `{{post.date | date: "%b %d, %Y"}}`

### Make about page use `post` layout
1. Add `layout: post` to about.html

