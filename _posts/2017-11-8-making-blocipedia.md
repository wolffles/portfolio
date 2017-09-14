#### This is going to be a blog post about making a rails app called blocipedia, I've decided to make a post about it because I've realized that I don't recall all the steps it takes to make a rails application. With this post I help my future self and anyone else who is in the same predicament.

## the initial setup
  1. cd to folder you want no need to generate a directory
  2. in terminal `$ rails new <name of app goes here>`
  3. create a new README file
  4. create the Development Database. bloc.io => module3 checkpoint10
  5. update gemfile
  6. in terminal `$ bundle install --without production`
  7. in terminal `$ rails db:create`
  8. in terminal `$ bundle install`
  9. set up a git repository.

## the app
<p> It might seem overwhelming when starting a project but you just have to look at the project in little steps and tasks. You don't have to work on your app in this order but this is how I went about making it.</p>

  1. start with a welcome page.
    * you can do the next step manually or use a the generator.
    * in terminal `$ rails generate controller welcome index`.
      - this will create the directories, code the config/route file, and create the view. It also create helper functions.
  2. creating the user model using devise.
    * in gemfile `gem 'devise'`
    * `$ bundle install`
    * `$ rails generate devise:install`
      - follow the instructions that follows the install
    * `$ rails g devise user`
      - will create specs, factory, model, code the route.
    * `$ rails g divise:views`
    * uncommented `confirmable` in the migrate file holding the devise code
    * added in models/user.rb `:confirmable` to devise:
    * run a `$ rake db:migrate`
    * used devises application.html.erb from their wiki for the sign in screen

  3. action_mailer
    * add `config.action_mailer.default_url_options = { host: 'localhost'}` to config/environment/tests and config/environment/development
    * use a third party to send email, included the key and password to the application.yml file
      - you'll need figaro to read yml files
    * in initializers/setup_mail.rb add the smtp(simple mail transfer protocol) info
    * add gem 'figaro' to gem file run a bundle install
    * make sure your user_name: and passwords are protected using yml files
    * to test to see if mailer works run server and check to see if mail is set in console after it is mailed.

  4. CRUD functionality
    * `rails g model <Name> <attributes:string,text,integer>`
    * associate new model to user model via belongs to has many
    * `rails g controller <name>`
      - define controller actions.
    * create routes in config/routes `resources :<model>`
    * add views ie: index, show, new, edit, partials
      - `resources :<model>` creates crud routes, controller controls what those routes actions do, views renders the output.
      - I started with the controller then the view
  5. User authorization using Pundit
    * add to gemfile `gem 'pundit'`
    * run `$bundle install`
    * run `$rails g pundit:install` this will generate some useful defaults for you if its your first time.
      - you can decide to use the default generated file or make your own.
      - pundit is plain ruby the rb file is where the authorization comes into play.
    * need to add a role column to user `$ rails g migration add_role_to_user`
    * in model/user.rb add `enum role:[:<var>]`
      - `after_initilize { self.role||=:standard }`
    * create the policy file for authorization.
    * `include Pundit` to application_controller.rb
      - `rescue_from Pundit::NotAuthorizedError, with: :user_not_authorized`
      - create a private method `user_not_authorized`
    * to activate the policy, in controller method you choose, add `authorize User`
    * `after_action :verify_authorized`
  6. seed using Faker gem
  7. adding payments using Stripe
    * add to gemfile `gem 'stripe'`
    * run `$bundle install`
    * add a config/initializers/stripe.rb
      - add the configuration code
    * add the secret keys to the application.yml file.
    * if you haven't make sure you have the application.yml file in the .gitignore file
    * create the controller charges_controller.rb
      - used a default create method for stripe
      - used a default new method for stripe
    * create a model for the class Amount
    * added charges controller to the routes file
      - `resources :charges, only: [:new,:create]`
    * added the view for the charge views
      - optional: i designed a bit and gave the site a accounts page to manage all account links
  8. Adding on extra features. (for this project ill be adding a feature to make the posts private.)
    * our schema needs to be updated to support a private boolean.
      - `rails g migration AddPrivateToWikis private:boolean`
    * your case might be different but for me I need to add code that will update all the users posts if one chooses to downgrade from private to public again.
    * I'll also have to add the the option to change private or public in view and update the controller to take the parameters
    * when updating accounts remember all dependencies should change with account changes like private wikis should become public again.
  9. allowing people to add markdown syntax to posts
    * add `gem 'redcarpet'` to the gemfile
    * run `$bundle install`
    * in the application helper add code for a markdown function you can call in view, to render markdown syntax.
  10. establishing a 'has many through' relations
    * create model with ids in foreign keys that are indexed related models
      - ie `rails g model collaborator user:references:index wiki:references:index`
    * update the relations in the models via `has_many` or `belongs_to` in our case a wiki has many collaborators, and collaborators belongs to both user and wiki, but wiki doesn't belong to collaborators
    * we adjusted the policy to show what people can and cant see.
    * adjusted the routes accordingly, for this project we just need create and destroy.
    * created a create method/ destroy method and helper functions
