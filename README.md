# Rtsung

TODO: Write a gem description

## Installation

Add this line to your application's Gemfile:

    gem 'rtsung'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install rtsung

## Usage

```ruby
require 'rtsung'

rtsung = RTsung.new do
  client 'localhost', :vm => true

  client 'router', :max_users => 32

  client 'db1', :cpu => 2, :ip => '192.168.2.1', :weight => 1
  client 'db2', :cpu => 2, :ip => ['192.168.2.3', '192.168.2.4'], :weight => 2

  server 'example.com'
  server 'www.example.com', :port => 8080

  phase
  phase 2, :rate => 30
  phase 3, 30, :second, { :interval => 2 }

  user_agents do
    name 'Mozilla/5.0 (X11; U; Linux i686; en-US; rv:1.7.8) Gecko/20050513 Galeon/1.3.21', :probability => 30
    name 'Mozilla/5.0 (Windows; U; Windows NT 5.2; fr-FR; rv:1.7.8) Gecko/20050511 Firefox/1.0.4', :probability => 70
  end

  session :search do
    request '/'

    think_time 1..5

    request '/signin', :params => { :uniq => true }

    think 5

    request '/signin', :method => :POST, :params => { :email => 'test@example.com', :password => 'ov7Feift' }
  end
end

print rtsung.to_xml
```

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
