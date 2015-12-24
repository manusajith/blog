---
layout: post
title: "identity_map_in_rails"
date: 2013-12-15 04:07:41 +0530
comments: true
categories: Ruby, ActiveRecord, Rails
---

I was recently working on a project that was'nt maintained for some time and the test cases were failing too. I started upgrading the application to the latest version and some of the test cases were still failing.
Looking deeper into the logs I could find that I was getting an wierd error with IdentityMap when using with a Rails4 app. I did some googling and found that identity_map was removed from Rails4.

##What is IdentityMap ?##

Ensures that each object gets loaded only once by keeping every loaded object in a map. Looks up objects using the map when referring to them. More details on the IdentityMap pattern can be found [here]('http://www.martinfowler.com/eaaCatalog/identityMap.html') on a blog post by Martin Fowler

<!--more -->

##Configuration##

In order to enable IdentityMap, set `config.active_record.identity_map = true` in your config/application.rb file.

Identitymap configuration has been removed from Rails4. If you are upgrading Rails 4 from Rails 3, then please be sure to remove/comment the line from config/application.rb

##Issues with IdentityMap##

###Associations###

Active Record Identity Map does not track associations yet. For example:

    comment = @post.comments.first
    comment.post = nil
    @post.comments.include?(comment) #=> true

Ideally, the example above would return false, removing the comment object from the post association when the association is nullified. This may cause side effects, as in the situation below, if Identity Map is enabled:

    Post.has_many :comments, :dependent => :destroy

    comment = @post.comments.first
    comment.post = nil
    comment.save
    Post.destroy(@post.id)

Without using Identity Map, the code above will destroy the @post object leaving the comment object intact. However, once we enable Identity Map, the post loaded by Post.destroy is exactly the same object as the object @post. As the object @post still has the comment object in @post.comments, once Identity Map is enabled, the comment object will be accidently removed.

This inconsistency wasnt fixed and was the main reason for the removal of identitymao from Rails4.

Other two minor problems are:

If you inheriting models, and you want to switch from one typo of object to another, then first you need delete your object from identity map, and after that create a new object. Example:

    class A < ActiveRecord::Base
    end

    class B < ActiveRecord::Base
    end

    a = A.create!
    a.update_attribute :type, 'B'
    b = B.find a.id
    #=> #<A:...>
    ActiveRecord::IdentityMap.remove(a) if ActiveRecord::IdentityMap.enabled?
    b = B.find a.id
    #=> #<B:...>

Another small issue is that the identity map may mees up the thing in the tests. As it do not truncates its repository after each test. To make it to do so one needs to add that into test framework configurations. Rspec example:

    RSpec.configure do |config|
      config.after :each do
        DatabaseCleaner.clean
        ActiveRecord::IdentityMap.clear
      end
    end

My opinion is that identity map may be used, but partially. It is a bad idea to enable it by default for each single object, but it will be a good idea to enable it to specific models. Say, you have a table of languages, which is pretty static data, or may by countries. Why not to load them all in to identity map. But, with dynamic data (like users, or something different, that constantly changes), there is no need to store that in the memory.

The official documentation states clearly that the identitymap is still under development, so no one should really be using it in the wild.