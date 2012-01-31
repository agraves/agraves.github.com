---
layout: post
title: "Debugging redirects"
date: 2012-01-31 01:54
comments: true
categories: [Protips, Rails]
---

Ever had a controller action issuing a redirect, but had no idea why?  Instead of disabling your gems and before\_filters one by one, try this:

``` ruby app/controllers/application_controller.rb

    unless Rails.env.production?
      def redirect_to(options = {}, response_status = {})
        ::Rails.logger.error("Redirected by #{caller(1).first rescue "unknown"}")
        super(options, response_status)
      end
    end
```

Original credit to to [this blog post](http://jkfill.com/2011/05/13/log-which-line-called-redirect_to/).
