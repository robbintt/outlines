### Squarespace Patterns

A collection of concepts for developing bespoke web applications in the squarespace managed hosting framework.


View a page's available JSON by appending `?format=json-pretty` to the url.


#### Avoid putting in credentials every git push

Manage local git config in the project directory. From [this squarespace answer](https://answers.squarespace.com/questions/4565/how-can-i-avoid-credentials-typing-on-every-git-push-pull.html).

- `git config credential.helper 'cache --timeout=3600'


#### Text blocks merge! How to prevent text blocks from merging.

- Alternate text blocks with empty markdown blocks


#### Managing LESS and CSS

- `styles/reset.css` - override squarespace default styles
- `styles/base.css` - seems to go on each site either before or after site


#### Managing Editable Page Sections (inside a parent page)

Squarespace requires some acrobatics in order to display editable pages inside the main page.

1. Scenario: Bespoke Theme from Designer
    1. The client needs to edit the contents
        - Plan: Use a squarespace `index.conf`. This page contains other pages. The index page will display its own template, `collections/index.list` which will wrap the "main content" from the Squarespace CMS. The json data available to the index.conf, primarily just `title` and `navigation title` and `slug` (all have similar names in the json) can also be called in the template.
    2. The client doesn't need to edit the contents
        - Plan: Embed the content into the page templates


#### Template Management

1. jsont.squarespace.com
    - [json-t basics](http://jsont.squarespace.com/)
    - [json-t advanced](http://jsont.squarespace.com/advanced-jsont/#If-Statements-extensionii)

2. developers.squarespace.com
    - [what is json-t](http://developers.squarespace.com/what-is-json-t/)
    - [json-t system variables](http://developers.squarespace.com/jsont-system-variables/)
    - [json-t predicates](http://developers.squarespace.com/jsont-predicates/)
    - [json-t directive](http://developers.squarespace.com/jsont-directives/)
    - [json-t formatters](http://developers.squarespace.com/jsont-directives/)
    - [json-t helpers](http://developers.squarespace.com/jsont-helpers/)
    - [custom Query tag](http://developers.squarespace.com/squarespace-query/) for collection querying

3. answers.squarespace.com
    - [disambiguating {.if} and {.equal}](https://answers.squarespace.com/questions/100096/access-parent-scope-from-repeated-section.html)
    - [custom layout for individual page](https://answers.squarespace.com/questions/10839/how-do-you-add-custom-layouts-to-individual-pages.html)


#### User-editable sections

In order to allow to clients to edit their pages in a coherent way, it is necessary to use index pages to combine each editable page into one 'main page'.

In order to aggregate pages and collections, use an index at the top level, and use folders at subordinate levels.

- [Folders & Indexes](http://developers.squarespace.com/folders-indexes) are the mechanism for building custom aggregate pages.
- [Custom Index Page](https://support.squarespace.com/hc/en-us/articles/206543817-Using-the-Index-Page)
    

- [Anchor Links in Index Pages](https://support.squarespace.com/hc/en-us/articles/207842357) - may or may not be important

One pattern is to have headers and paragraphs of text interleaved with sections of content, for example project pages with a grid of images or a grid of logos, or a grid of contributors.

An effective pattern for working with this may be to have one collection of paragraphs and titles which are specifically indexed in teh template. These are interleaved with actual collection sections which loop over each item in the collection to populate the segment.

- [Template Partials](http://developers.squarespace.com/template-partials/) break up sections so Squarespace users can edit them.

1. Example: A simple 'blog post' section.
    - Display any number of vertical paragraphs and images in any order.
- [Squarespace Query: Access collection Data from another page](http://developers.squarespace.com/squarespace-query/)
    - A method for giving the user some edit control over a custom template.



#### Managing Templates

- [Layouts & Regions](http://developers.squarespace.com/layouts-regions/) - how to make different page templates for different pages



#### Basic Template, Navigation, and Blocks

- [Beginner Tutorial](http://developers.squarespace.com/beginner-tutorial/) - good intro to nav and code blocks. A little unclear at times.
    - blocks/navigation.block was not being detected. I renamed it to blocks/nav.block and changed the reference to it to 'nav'.
