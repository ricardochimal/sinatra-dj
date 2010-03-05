require 'sinatra-dj'
require File.dirname(__FILE__) + "/vendor/delayed_job/tasks/tasks"

desc "One time task to setup on Heroku"
task :create do
  sh "heroku create"
  sh "git push heroku master"
  sh "heroku rake db:migrate"
  sh "heroku workers +1"
  sh "heroku open"
end

namespace :db do
  task :migrate do
    ActiveRecord::Migrator.migrate(
      'db/migrate', 
      ENV["VERSION"] ? ENV["VERSION"].to_i : nil
    )
  end
end
