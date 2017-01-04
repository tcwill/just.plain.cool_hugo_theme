# Just.Plain.Cool Hugo Theme

This is a theme for Hugo that I created for [my website](http://just.plain.cool).

The homepage for the theme [can be found here](http://just.plain.cool/hugo-theme/).

I developed the theme with a problem in mind.  I had several existing
topical blogs that I wanted to fold into a single website.  Each blog
had its own URL that I'd like to keep around and point to different topic
pages in the consolidated site.


## Content Types (sections): Posts and Pages

Sections are a basic Hugo convention.  These two sections will be used
to default to their respective contents types; i.e. the default behavior
in Hugo is Section = Content Type.  The theme is composed of just these
two content types:

- posts - blog posts (point in time).
        - posts are the "featured" content in the theme and are readily visible/accessible throughout
        - list elements of posts render with a trailing date
- pages - continuously maintained content
        - pages are less visible and primarily accessible through Topic Index pages.
        - list elements of pages do not include a date

Another Hugo convention is that the name of the directory under content/
is used as the name of the Section/Content Type. 

```
.
|_ content
   |_ post
   |  |_ post1.md
   |  |_ post2.md
   |  |_ ...
   |_ page
      |_ page1.md
      |_ page2.md
```

FWIW, I dislike the 'section' term. For this theme I think it's 
helpful to simply think of posts and pages as content
types.  In the context of this theme the word 'sections' is confusing.

## Semantics

### Taxonomy 1: Topics

Topics will be used to organize posts and pages into topical subsites
that serve as the primary site navigation. This will let me keep some 
of the groupings that exist from my various blogs.  

Topic is the top-level taxonomy for the theme, so I recommend keeping
your list of topics relatively well-defined and few in number.  This 
way major navigation components of the theme will be effective.

Topics will be implemented in the front matter of the various posts and
pages, e.g.:

```
+++
topics: [ "beekeeping" ] 
+++
```

... of course if a post/page spans multiple topics, you can have multiple
topics and Hugo will take care of cross-posting for you:

```
+++
topics: [ "beekeeping","homebrewing" ]
+++
```

### Taxonomy 2: Tags

The lower-tier taxonomy for the theme is "tags".  Just think of
this as keywords, and use them as liberally as you like.  As with any
taxonomy the more consistency you apply here, the more useful these will
be.  I think of these as a way to call out specific subtopics or just
novel nouns that appear through the site.

```
+++
tags: [ "wildlife","adventure","landscape"  ]
+++
```

When the above is combined with the Topic of "photography" this will help
with navigating your subtopics.


## Configuration

### Theme specific config:

The theme *requires* the following config in your site-level config.toml:

```
baseurl = "http://example.com/"
title = "Your site title"
theme = "just.plain.cool"

[taxonomies]
topic = "topics"
tag = "tags"
```

The theme can use author information if you so choose to include it in your site-level config.toml

```
[params]
 [params.authors]
  [params.authors.tcw]
        "firstName" = "Todd"
        "lastName" = "Williams"
        "displayName" = "Todd C. Williams"
        "img" = "/img/tcw.jpg"
        "Email"  = "tcwill@1dot0.io"
        "website" = "http://1dot0.io"
 [params.authors.goodcitizen]
        "displayName" = "Good Citizen"
	"Email" = "goodcitizen@example.com"
```

With the above author config if you specifiy the following in a piece of content frontmatter:

```
+++
author = "tcw"
+++
```

The theme will insert the Author block that matches the 'tcw' token... so everything under
params.authors.tcw (if it matches the values the template is looking for).

### More theme specific config:

There are a handful of parameters that are entirely theme-specific.  So until Hugo can support overlaying
config files into site config, I've decided to stick a config.toml file in the theme's data/ directory.

```
[ taxonomy.exclude ]
topics = [ "about", "nope" ]

[ navToRender ]
header = 3

[ SummariesToRender ]
homepage = 3
topicIndex = 2
```

`taxonomy.exclude.topics` is a map list of topic values that should be excluded from being rendered in the
navigation links in the top-left of the theme's layout.

`navtorender.header` is an integer value to specify how many nav links to render in the top-topics nav
in the top-left of the theme's layout.  Note: this is *in addition* to an 'about' link.

`summariestorender.homepage` sets the number of post summaries to render on the theme's homepage.  Any posts
beyond that number are rendered in the "older posts" list.

`summariestorender.topicindex` is the same, but for topic index pages.  Again, any posts beyond that render
in the older posts list.

### Theme specific content:

The only assumption the theme makes is that you'll provide an about page in content/pages/about.md and
specify the following in that page's frontmatter:

```
+++
url = "about"
+++
```

## Credits

This theme was built from scratch, but I have to acknowledge the many contributions from the Hugo community
via the Hugo [docs](http://gohugo.io/overview/introduction/) and [forums](https://discuss.gohugo.io/).


That's it for now.

-Todd

