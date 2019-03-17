# Ruby
<!-- MarkdownTOC -->

- [Install \(here\)](#install-here)
- [Data Types](#data-types)
- [Database](#database)
    - [Create](#create)
    - [Read](#read)
    - [Update](#update)
    - [Delete](#delete)
- [Tutorials](#tutorials)

<!-- /MarkdownTOC -->

## Install (here)
https://gorails.com/setup/windows/10
http://guides.railsgirls.com/install

```bash
sudo apt update
sudo apt install git-core curl zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev python-software-properties libffi-dev

cd
export $SHEL="/bin/zsh"
git clone https://github.com/rbenv/rbenv.git ~/.rbenv
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.zshrc
echo 'eval "$(rbenv init -)"' >> ~/.zshrc
exec $SHELL

git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build
echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.zshrc
exec $SHELL
rbenv install 2.5.1
rbenv global 2.5.1
ruby -v

sudo gem install bundler
rbenv rehash

curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
sudo apt-get install -y nodejs
gem install rails -v 5.1.4
rbenv rehash

# Create a new app
rails new myapp
cd myapp
# Create the database
rake db:create
# Run the server
rails server
# You can now visit http://localhost:3000 to view your new website!

# If your using Linux (not WSL) make sure postgresql service is running
sudo service postgresql start
service postgresql status
```

## Data Types
```ruby
# Hash
variable = {key: value}
variable[:key]  # => value
variable.key    # => value
```

## Database
Assuming we have a database called `Tweet`

### Create

```ruby
# Create (a new record)
t = Tweet.new
t.data = "My tweet" # OR
t = Tweet.new(data: "My tweet")
t.save
# Create 2
Tweet.create(hash)
```

### Read

```ruby
Tweet.find(1)           # Read (Find one ID in the database)
Tweet.find(3, 4, 5)     # Read (Find multiple IDs)
Tweet.first
Tweet.last
Tweet.all               # Return an array of all tweets
Tweet.count
Tweet.order(:name)      # Return all tweets ordered the name
Tweet.limit(10)         # Return the first 10 tweets
Tweet.where(name: "jon") # Rertun all tweets from Jon
Tweet.where(name: "jon").order(:data).limit(10)
```

### Update

```ruby
t = Tweet.find(1)
t.tweet = "New tweet"   # OR change multiple fields at once
t.attributes = hash
t.save
# We can also update all fields directly
t = Tweet.find(1)
t.update(hash)
```

### Delete

```ruby
t = Tweet.find(1)
t.destroy
Tweet.find(1).destroy
Tweet.destroy_all
```

## Tutorials
* http://railsforzombies.org/
* https://stackoverflow.com/questions/7164484/ruby-on-rails-quickstart
* https://www.tutorialspoint.com/ruby-on-rails/rails-quick-guide.htm
* http://guides.railsgirls.com/app

