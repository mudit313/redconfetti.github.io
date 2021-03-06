---
layout: post
title: Add a Serialized Hash Attribute to a Factory_Girl Definition
date: '2012-06-11 20:25:13 -0700'
categories:
- Testing
tags:
- factory_girl
- hash
---
I recently declared an ActiveRecord model which stores a serialized Hash inside of a text field. When I tried to setup a factory for this model using FactoryGirl, I received many syntax errors. This is because FactoryGirl attributes expect a single value or a certain form of code block.

``` ruby
factory :post do
    title        "Example Post"
    body         "This is the body of the example post"
    meta         { "version" => 2 }
    created_at   "2012-06-01 17:53:13"
  end
```

To include a hash as an attribute of a factory, declare the Hash separately and then simply assign it directly in the factory definition.

``` ruby
meta_hash = { :version => 2 }
  factory :post do
    title        "Example Post"
    body         "This is the body of the example post"
    meta         meta_hash
    created_at   "2012-06-01 17:53:13"
  end
```

As <a href="https://github.com/joshuaclayton" target="_blank">Joshua Clayton</a> pointed out, one could also do <a href="https://gist.github.com/joshuaclayton/3056591" target="_blank">the following:</a>

``` ruby
factory :post do
  title        "Example Post"
  body         "This is the body of the example post"

  meta         { { version: 2 } }
  # or
  meta({ version: 2 })

  created_at   "2012-06-01 17:53:13"
end
```
