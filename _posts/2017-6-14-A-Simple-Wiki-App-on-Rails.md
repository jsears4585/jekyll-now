## Getting comfortable with APIs

### Setup

Go ahead and generate a rails application.

Done? Okay cool

### Now for the Actual Part

We're not going to need much for this app, just a controller and a view. And some CSS. In truth, rails is way overkill for this type of application, but since we've already generated our framework with some rails magic, we can focus our efforts more squarely on calling the API, cleaning the results, and passing them to our views.

### Application Programming Interfaces and You, a Love Story

If you aren't already familiar, **A**pplication **P**rogramming **I**nterfaces provide a great medium for obtaining cool data you want in a format you want. APIs naturally come with their own issues, but we'll discuss that later. Suffice to say, if you haven't you had the pleasure of tapping into an API, I can report that you'll be delighted by how quickly you can fly a simple application.

### Code Time

```ruby
require 'rest-client'
require 'json'

class StatsController < ApplicationController

  def index
    results = RestClient.get( "https://en.wikipedia.org/api/rest_v1/feed/onthisday/all/#{current_month}/#{current_day}",
                              headers = { Accept: :'application/json' } )
    json = JSON.parse(results)
    @keep = keep_ary(json)
  end

  private

    def current_month
      m = Time.now.month
      m = "0" + m.to_s if m.to_s.length < 2
      m.to_s
    end

    def current_day
      d = Time.now.day
      d = "0" + d.to_s if d.to_s.length < 2
      d.to_s
    end

    def keep_ary json
      keep = json["events"].select do |event|
        next if event["pages"].empty?
        !event["pages"].first["thumbnail"].nil?
      end
    end
end
```
