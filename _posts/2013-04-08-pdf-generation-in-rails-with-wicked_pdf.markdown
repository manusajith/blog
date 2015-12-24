---
layout: post
title: PDF generation in Rails
tags:
- '2012'
- '2013'
- rails
- ruby
- pdf
- Coding
- coding
- codingarena
- competition
- internet
- manu
- neo
- online
- programming
- Ruby
- web
status: publish
type: post
published: true
---

Recently my friend was working on a project that had a requirement to export the html page to PDF. He had some issues setting this up. So I thought I would write this article, so that it will be helpful for  anyone who faces the same issue. It’s easy getting your pdf in rails as long as you follow the right steps ;) (But unfortunately my good friend doesnt always do that for some reason of his own - No offense intended ;) )

<!--more-->

If you are using Rails, then you have this wonderful <a href="http://rubygems.org">rubygems</a> where you can find a no of gems for pdf generation. The suggested ones are <a href="http://rubygems.org/gems/prawn">prawn</a> and <a href="http://rubygems.org/gems/wicked_pdf">wicked_pdf</a>.

##Which one to chose ?##

For me wicked_pdf is very simple to understand and it gets your job done very quickly if you follow all the right steps, while Prawn restricts you to the old table, grids layout. But ultimately its you who will have to decide which to use depending upon your specific requirements.

I will be using wicked_pdf and ubuntu.

##Wicked_pdf##

Wicked_pdf uses a shell utility <a href="http://code.google.com/p/wkhtmltopdf/">Wkhtmltopdf</a>  to serve a PDF file to a user from a HTML page. In other words, rather than dealing with a PDF generation DSL of some sort, you simply write an HTML view as you would normally, then let Wicked take care of the hard stuff

##Now what is wkhtmltopdf ?##

<a href="http://code.google.com/p/wkhtmltopdf" >Wkhtmltopdf</a> is an c++ executable that <a href="https://github.com/mileszs/wicked_pdf" >wicked_pdf</a><span > gem essentialy wraps. It works great for pdf generation of tables reports etc. The WK in wkhtmltopdf stands for webkit which is the browser engine that is used to render HTML and java-script  Chrome uses this same engine.

Installing it simply via
    sudo apt-get install wkhtmltopdf

on Ubuntu will install a reduced functionality version which is probably not what you want. According to the manual the reduced functionality version does not include the following features.
Printing more then one HTML document into a PDF file. 

Running without an X11 server. 
Adding a document outline to the PDF file. 
Adding headers and footers to the PDF file.
Generating a table of contents. 
Adding links in the generated PDF file. 
Printing using the screen media-type. 
Disabling the smart shrink feature of webkit. 
If you need any of these, then you need to setup the static version of wkhtmltopdf.
First check OS is 32 bit or 64 bit by using following command
Try
		uname -m

Run following command for installing dependencies.
		sudo apt-get install openssl build-essential xorg libssl-dev libxrender-dev

Based on OS download wkhtmltopdf package from following site
<a href=" http://code.google.com/p/wkhtmltopdf/downloads/list">http://code.google.com/p/wkhtmltopdf/downloads/list</a>

Then extract using command

		tar xvjf wkhtmltopdf-0.11.0_rc1-static-amd64.tar.bz2

Then move extracted DIR to usr/local/bin folder

		sudo mv wkhtmltopdf-0.11.0_rc1-static-amd64 /usr/local/bin/wkhtmltopdf

Check wkhtmltopdf is installed or not using following command

		which wkhtmltopdf

##Using wicked_pdf in your Rails app##

Add this to your Gemfile

		gem 'wicked_pdf'

You may also need to add the following to your config/initializers/mime_types.rb</p>

		Mime::Type.register "application/pdf", :pdf


##Basic Usage:##

    class Invoice < ApplicationController
      def show
        respond_to do |format|
          format.html
          format.pdf do
            render :pdf => "invoice"
          end
        end
      end
    end

If you need to include stylesheets and javascript inside the generated document, the wicked_pdf gem has helpers for that

		<%= wicked_pdf_stylesheet_link_tag "pdf_stylesheet" -%>
		<%= wicked_pdf_javascript_include_tag "pdf_javascript" %>

##Some tweaks and tips##

If you need to hide some links in your generated PDF document then you can use a custom stylesheet which defines the properties for print media and can include the same using the above helper method.

Eg: You have a button on your html page and you dont want that to be displayed when you generate the PDF.

If you have the following link with css selector "print_friendly"

		<%= link_to "Print" , "http://example.com/download", :id=>"print_friendly" %>

and have a stylesheet with the css properties for print media as

		@media print {
		  #print_friendly{
		  display:hidden;
		  }
		}

then the link wont be visible inside the generated PDF document

If your page has a lot of javascript and needs longer time for rendering then you can add the following the wicked_pdf

		wkhtmltopdf.exe --javascript-delay 15000 http://example.com/downloads

##Some common Issues##
###1. Runtime Error###
RuntimeError in XxxxController#show

Failed to execute: /usr/bin/wkhtmltopdf --print-media-type -q - - Error: PDF could not be generated!

  	Rails.root: /apps/rails/show

Check the location of your wkhtmltopdf using which wkhtmltopdf and also run a bundle update command as sometimes your gem in gemfile would be configured with the wrong path.
###2. Is wkhtmltopdf-binary necessary to generated PDF files ?###
No

If you have installed the system libraries and have configured the path correctly in your app correctly, you dont need to install he wkhtmltopdf-binary gem seperately.

###3. Wicked_pdf not rendering graphs with HighCharts ###
Wkhtmltopdf doesn't handle transparency/shadows properly and can result in unpredictable results. So the workaround is to add the following options to yo2ur highcharts

			f.options[:plotOptions][:line] = :animation => false, :shadow => false, :enableMouseTracking => false

####As I said earlier it’s easy getting your pdf in rails as long as you follow the right steps ;)####
