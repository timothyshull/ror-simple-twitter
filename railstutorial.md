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

    

 