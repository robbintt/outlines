### Squarespace Patterns

A collection of concepts for developing bespoke web applications in the squarespace managed hosting framework.


View a page's available JSON by appending `?format=json-pretty` to the url.


#### Avoid putting in credentials every git push

Manage local git config in the project directory. From [this squarespace answer](https://answers.squarespace.com/questions/4565/how-can-i-avoid-credentials-typing-on-every-git-push-pull.html).

- `git config credential.helper 'cache --timeout=3600'


#### Managing LESS and CSS

- `styles/reset.css` - override squarespace default styles
- `styles/base.css` - seems to go on each site either before or after site


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
