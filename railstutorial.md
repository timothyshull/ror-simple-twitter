# 3. Mostly Static Pages
## App Setup
1. cd into directory

    rails __(version)__ new (name)
    
2. Complete prelim gemfile
    - source 'https://rubygems.org'
    - Basic gems + version - rails, sass-rails, uglifier, coffee-rails, jquery-rails, turbolinks (speeds up link selection by keeping elements of the page alive), jbuilder (methods for creating JSON in ruby), sdoc (wrapper for documentation commands) 
    - Development gems - sqlite3 (or mysql, pg), byebug (debugging), web-console (allows you to create interactive debuggig sessions in the browser), spring (rails app preloader for development) (consider pry)
    - Testing - minitest reporters, mini_backtrace, guard_minitest
    - Production - pg, rails_12factor (for deploying to heroku)
    
3. Install and update the bundle

        bundle install --without production && bundle update

4. Initialize repository
5. Change readme and fill out basics
6. Setup GitHub/Bitbucket, push
7. Deploying - Make sure to use rails_12factor (used by Heroku to serve static assets)
    - Make sure to use --without production to prevent local installation of production gems and run bundle install --without production to update the Gemfile.lock for Heroku
    - Make sure your heroku toolbelt is installed and updated, heroku login, make sure keys are added and run heroku create
    - git push heroku master
    - heroku logs
    - For production use config.force_ssl = true in production environment and puma gem for a heroku production webserver, add config/puma.rb and a Procfile
## Static pages
1. git branch and checkout
2. Generate controller
    
        rails generate controller StaticPages home help

3. git add, commit, push origin to static-pages
4. Rails commands can be undone by replacing the generate with destroy, etc., or rake db:migrate -> rake db:rollback
5. Routes file already has a rule for home and help, maps url requests to a the related controller action, which retrieves the related view, in this case static_pages/home does not follow the standard REST architecture
6. controllers inherit from ApplicationController, and actions are methods that map to real-life actions. Rails is smart and knows to render the associated view from an empty action (because of inheritance from Application Controller).
7. (Remember - views are filtered through their corresponding layout, which gives the boilerplate html and the general structure. This can be overridden using render in action method or for all views in a controller with render template: "products/show")
## Getting started with testing
1. Different views on TDD starting point. Generally write simple tests first. Goals with testing:
    - Protect against regression (loss of functionality of a feature)
    - Aid in refactoring
    - Act as client with a code to help determine design and interface
2. Start with controller tests and model tests and then we will move on to integration tests
3. rails g controller automatically generates a test file to get started
    
        test "should get home" do
          get :home
          assert_response :success
        end

4. Run tests with 

        bundle exec rake test 

5. Goal is to write a failing test first and then get it to work - "Red, green, refactor". Failing test:

          test "should get about" do
            get :about
            assert_response :success
          end

6. Then create the action and correct resource to make it pass, i.e. create about route, create about action in controller, create about view
## Slightly dynamic pages
1. To create dynamic titles starting with testing 
    - Use assert_select method (tests for presence of a particular HTML tag or selector)
    
            assert_select "title", "Home | Ruby on Rails Tutorial Sample App" 
        
    - Add to all three tests in controllers tests, then test for red, then add page titles
2. To make it dynamic, we use erb and DRY out the code. Use:

        <title><%= yield(:title) %> | Ruby on Rails Tutorial Sample App</title>

    In the layout title and for the individual view use:
    
        <% provide(:title, "About") %>



 