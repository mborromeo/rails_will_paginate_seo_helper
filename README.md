# rails_will_paginate_seo_helper

This is standing on the shoulder of a giant: :heart: https://github.com/mislav/will_paginate
and adds some seo-sugar on top.

A simple Rails ViewHelper to display link-tags for will_paginate in header.


Url-Parameter left untouched.

Google suggests to add rel=next and rel=prev link-tags on paged pages: https://webmasters.googleblog.com/2011/09/pagination-with-relnext-and-relprev.html

If you want to have seo link-tags for pages in your rails app without monkey patching will_paginate:

## Setup
simple add to your Gemfile:

```ruby
 # works with rails 4, 5 and 6
 gem 'will_paginate'
 gem 'rails_will_paginate_seo_helper'
```
## Usage

 a will_paginate paged ActiveRecord::Relation
 from your controller:

 ```ruby
 @todos = Todo.all.paginate(page: params[:page])
 ```
now you can use on your templates (expects ```<%= yield :pagination_rel_links %>``` in the header section of your layout)

```html
 <!-- in todos/index.html.erb -->
 <% content_for :pagination_rel_links do %>
  <!-- this will showup in the header section of your html -->
  <%= will_paginate_seo_links(@todos) %>
 <% end %>


```


given we are on page 2 - output will be:
```html
<link href="http://localhost:3000/todos" rel="prev">
<link href="http://localhost:3000/todos?page=3" rel="next">
```

You can also specify a custom page parameter name:
```ruby
will_paginate_seo_links(@todos, param_name: 'p')
```
