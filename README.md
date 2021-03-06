# Slackbotsy

Ruby bot for Slack chat, inspired by http://github.com/seejohnrun/botsy.

## Installation

Add this line to your application's Gemfile:

    gem 'slackbotsy'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install slackbotsy

## Example usage

```ruby
require 'slackbotsy'
require 'sinatra'

config = {
  'team'           => 'your_team',
  'channel'        => '#default',
  'name'           => 'botsy',
  'incoming_token' => 'secret',
  'outgoing_token' => 'secret'
}

bot = Slackbotsy::Bot.new(config) do

  hear /echo\s+(.+)/ do |data, mdata|
    "I heard #{data['user_name']} say '#{mdata[1]}' in #{data['channel_name']}"
  end

  hear /flip out/i do
    open('http://tableflipper.com/gif') do |f|
      "<#{f.read}>"
    end
  end

end

post '/' do
  bot.handle_item(params)
end
```
