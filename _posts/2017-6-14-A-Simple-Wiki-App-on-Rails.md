## Getting comfortable with APIs

### Setup

Go ahead and generate a rails application.

Done? Okay cool

### Now for the Actual Part

We're not going to need much for this app, just a controller and a view. And some CSS. In truth, rails is way overkill for this type of application, but since we've already generated our framework with some rails magic, we can focus our efforts more squarely on calling the API, cleaning the results, and passing them to our view.

### Application Programming Interfaces and You, a Love Story

If you aren't already familiar, **A**pplication **P**rogramming **I**nterfaces provide a great medium for obtaining cool data you want in a format you want. APIs naturally come with their own issues, but we'll discuss that later. Suffice to say, if you haven't you had the pleasure of tapping into an API, I can report that you'll be delighted by how quickly you can fly a simple application.

### Code Time (Ruby)

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

The 'onthisday' endpoint from WikiMedia (the group/movement that sustains the Wikipedia project) is suprisingly fun and powerful. When called with the appropriate header, it provides you with a string of JSON that contains a collection of data concerning historical events for a particular day of the year.

By leveraging a few simple methods, we can easily adapt the API call to be dynamic. We just interpolate the month and day strings created with these methods into the API request string, and BAM, we've got the day's historical record we can now break down and feed to our view.

### But Not So Fast

Take notice of the **#keep_ary** method we've created. While this endpoint delivers some great data, there are still errors and inconsistencies we'll have to mitigate before we can provide an instance variable for our view to render.

In this case, occasionally, the JSON string returned from the API provides us with objects that don't hold all of the necessary information we require to render our view in a uniform way. In short, **#keep_ary** enumerates through the full list of events and skips over any unpopulated collections or any collections lacking a thumbnail.

### Code Time (HTML/ERB)

```html
<header>
  <h1 id="that_guy">¯\_(ツ)_/¯</h1>
  <h3 id="sub_head">Historical events for <%= Time.now.strftime("%B %d") %></h3>
</header>

<table cellpadding=0>
  <thead>
    <th>Image</th>
    <th>Description</th>
  </thead>
  <tbody>
    <% @keep.each do |event| %>
      <tr>
        <td>
          <a href='https://en.wikipedia.org/?curid=<%= event["pages"].first["pageid"] %>' target='_blank'>
            <img src='<%= event["pages"].first["thumbnail"]["source"] %>' width='200'>
          </a>
        </td>
        <td class="word_padding"><span class="golden"><%= event["year"] %></span> — <%= event["text"] %></td>
      </tr>
    <% end %>
  </tbody>
</table>
```

Above is the extent of the HTML/ERB we'll need to dynamically create our single-page application. We create a table with headers, then simply inject an each function that iterates over each of the clean collections and pulls out the relevant bits, in this case, the thumbnail link, a link to the article, and a brief set of text describing the historical occurance. 

### Code Time Again (CSS)

```css
table { border-collapse: collapse; border-spacing: 0; }

tbody:before {
  content: "-";
  display: block;
  line-height: 0.1em;
  color: transparent;
}

th {
  font-family: 'Merriweather';
  font-size: 2.3vw;
  padding: 12px 0px;
  background-color: #0e0e75;
  margin-bottom: 20px;
  color: beige;
}

td {
  font-family: 'Raleway';
  font-size: 18px;
}

header {
  color: #606060;
  background: #f0f0f0 image-url("texture.png");
  text-align: center;
  font-family: 'Merriweather';
}

#that_guy {
  font-size: 7vw;
  padding-top: 13px;
  margin: 0px;
}

#sub_head {
  font-size: 2.3vw;
  margin: 0px;
  padding-bottom: 19px;
}

.word_padding {
  padding: 2vw;
}

.golden {
  color: #c7bc32;
  font-weight: 700;
  font-size: 1.2em;
}
```

What's an app without a little style? Above, we've simply spruced up the spacing and font-sizing while providing some general rules for our table to follow.

So what does it all look like now that we're finished?

<h1><a href="http://www.historically.co/" target="_blank">Big Finish</a></h1>
