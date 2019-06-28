# frozen_string_literal: true

source 'https://rubygems.org'

# Make sure all gems are using consistent versions for troubleshooting

gem 'bundler', '~> 1.17.3'
gem 'cocoapods', '~> 1.6.2'
gem 'danger', '~> 6.0.9'
gem 'danger-junit', '~> 0.7.4'
gem 'danger-rubocop', '~> 0.6.1'
gem 'danger-swiftlint', '~> 0.21.1'
gem 'dotenv', '~> 2.7.2'
gem 'fastlane', '~> 2.123.0'
gem 'rubocop', '~> 0.70.0', require: false
gem 'xcode-install', '~> 2.5.0'

plugins_path = File.join(File.dirname(__FILE__), 'fastlane', 'Pluginfile')
eval_gemfile(plugins_path) if File.exist?(plugins_path)
