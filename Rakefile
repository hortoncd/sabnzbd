#!/usr/bin/env rake

namespace :style do
  require 'rubocop/rake_task'
  desc 'Run Ruby style checks'
  RuboCop::RakeTask.new(:ruby)

  desc 'Runs foodcritic linter'
  task :foodcritic do
    if Gem::Version.new('1.9.2') <= Gem::Version.new(RUBY_VERSION.dup)
      sh 'foodcritic --epic-fail any .'
    else
      puts "WARN: foodcritic run is skipped as Ruby #{RUBY_VERSION} is < 1.9.2."
    end
  end
end

desc 'Run all style checks'
task style: %w(style:foodcritic style:ruby)

task default: %w(style)

begin
  require 'kitchen/rake_tasks'
  Kitchen::RakeTasks.new
rescue LoadError
  puts '>>>>> Kitchen gem not loaded, omitting tasks' unless ENV['CI']
end
