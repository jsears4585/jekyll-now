## Getting comfortable with APIs

### Setup

Go ahead and generate a rails application.

Done? Okay cool

### Now for the Actual Part

We're not going to need much for this app, just a controller and a view. And some CSS. In truth, rails is way overkill for this type of application, but since we've already generated our framework with some rails magic, we can focus our efforts more squarely on calling the API, cleaning the results, and passing them to our views.

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

