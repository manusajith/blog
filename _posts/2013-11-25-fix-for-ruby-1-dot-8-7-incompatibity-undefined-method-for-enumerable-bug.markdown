---
layout: post
title: "Fix for ruby 1.8.7 incompatibity - undefined method for Enumerable bug"
date: 2013-11-25 13:55:31 +0530
comments: true
categories: Ruby Rails Ruby-1.8.7 Ruby 1.8.6 plugins
---

Recently I was working on a Rails 1.1.2 application which used Ruby version 1.8.6. I was trying to make the application work on Ruby 1.8.7, but I found that my 1.1.2 application developed in ruby 1.8.6 are not working in ruby 1.8.7.


The attachment_fu plugin was throwing a weird error,

    undefined method `[]' for #<Enumerable::Enumerator:0xb70a72d0>

and it was really hard to find what was causing the issue.

<!--more -->


From lot of search on google, I found that its issue with ruby 1.8.7 incomatibility. There is an incompatibility issue between Ruby 1.8.7’s String#chars method and the way ActiveSupport::Multibyte::Chars works.

Then, I started searching fix / solution for this incompatibity.
And, Finally I got solution.

If you use any ActionView helper methods such as truncate and also happen to be running ruby 1.8.7 with Rails > 2.0.2 Insert this into the top of your environment.rb:

    unless '1.9'.respond_to?(:force_encoding)
      String.class_eval do
       begin
        remove_method :chars
       rescue NameError
        # OK
       end
     end
    end
