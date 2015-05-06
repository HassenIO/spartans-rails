# spartans-rails
Actually, there is no specific Rails gem for Spartans, but the [Ruby gem of Spartans](https://github.com/htaidirt/spartans-ruby) was designed to be easily used and customized for Rails.

Here are the simple steps that helps you use spartans-ruby gem inside your Rails projects.

## Step 0. Add Spartans to your Gemfile

Add the following to your `Gemfile`:

    gem 'spartans'
    
Then run `bundle install` in your terminal to install Spartans gem.

## Step 1. Initialize Spartans API Client

Create an initializer file for Spartans. Create the `config/initializers/spartans.rb` file and insert:

    Spartans.init app_id: APP_ID, api_key: API_KEY

Where `APP_ID` is your application ID within Spartans, and `API_KEY` its secret API key (available in your Spartans application dashboard.)

_We highly recommand to use environment variables to store `APP_ID` and `API_KEY`_

## Step 2. Use your model to push items

Once Spartans is initialized, you can use it like you want. We often see developers pushing items to Spartans once they are created. In the model you want to collect as item, the use the following:

    after_save :push_to_spartans

    def push_to_spartans
        Spartans::Item.push id: self.id, name: self.name, properties: {
            property_1: self.property_1,
            ...
            property_n: self.property_n
        }
    end
    
The advantage to create the `push_to_spartans` method, is that you can re-use it (in console, for example.) A frequent use case is when you already have items you want to push to Spartans. In your Rails console, you can do:

    YourModel.all.each { |i| i.push_to_spartans }

Note that, depending on your database volume, this simple operation can take time to complete.

## Step 3. Getting suggestions

We created a Javascript API Client, that is very easy to use and flexible. We highly recommand you to check it out.

## Contribution

Of course, any contribution is welcome. If you have any implementation script that you think can help others, please share it here in this Readme. Fork it, change it and ask for a pull request.

With love,

Spartans team