# Eye::Slack

Sends info about process crashes to Slack channel.

**NOTE** see Changelog.md for changes

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'eye-slack'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install eye-slack

## Usage

this is an example configuration file

````
# Notify example
require 'eye/notify/eye_slack'

Eye.config do
  eye_slack webhook_url: 'url', username: 'eye', color: 'danger'
  contact :dev, :eye_slack, '#test'
  logger '/tmp/eye.log'
end

Eye.application 'test' do
  notify :dev, :debug
  stdall '/tmp/eye-example.log'

  process :some_process do
    notify :dev, :debug
    start_command 'sleep 120'
    daemonize true
    pid_file '/tmp/sleep.pid'
  end

end
````

**NOTE** You need to quit eye and load it back after adding `require`.

# Configuration

* add `eye_slack` line to `Eye.config` section and check following parameters
 * `webhook_url` - *required* - webhook URL
 * `username` - who is reporting to slack, *Eye Bot* as a default
 * `color` - *#f0f0f0* is default. You can choose from RGB or `good`, `warning` and `danger`
 * `icon` - either emoji or URL of the icon, emoji *must* start and end with `:`
 * `title` - title, displayed in bold
 * `message` - message to be sent, default is `*#name#* on #host# *#message#* at #time#.`

* `message` has following variables (variable must be enclosed to ##)
 * `time` - human readable time of the event
 * `host` - hostname
 * `message` - full message
 * `name` - name of process
 * `full_name` - full process name (like group::process)
 * `pid` - process ID
 * `level` - message info level

## Contributing

1. Fork it ( https://github.com/[my-github-username]/eye-slack/fork )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request
