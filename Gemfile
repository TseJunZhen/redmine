source 'https://rubygems.org'

if Gem::Version.new(Bundler::VERSION) < Gem::Version.new('1.5.0')
  abort "Redmine requires Bundler 1.5.0 or higher (you're using #{Bundler::VERSION}).\nPlease update with 'gem update bundler'."
end

gem "rails", "5.2.2"
gem "rouge", "~> 3.3.0"
gem "request_store", "1.0.5"
gem "mini_mime", "~> 1.0.1"
gem "actionpack-xml_parser"
gem "roadie-rails", "~> 1.3.0"
gem "mimemagic"
gem "mail", "~> 2.7.1"
gem "csv", "~> 3.0.1" if RUBY_VERSION >= "2.3" && RUBY_VERSION < "2.6"

gem "nokogiri", "~> 1.8.0"
gem "i18n", "~> 0.7.0"

# Windows does not include zoneinfo files, so bundle the tzinfo-data gem
gem 'tzinfo-data', platforms: [:mingw, :x64_mingw, :mswin]
gem "rbpdf", "~> 1.19.6"

# Optional gem for LDAP authentication
group :ldap do
  gem "net-ldap", "~> 0.16.0"
end

# Optional gem for OpenID authentication
group :openid do
  gem "ruby-openid", "~> 2.3.0", :require => "openid"
  gem "rack-openid"
end

platforms :mri, :mingw, :x64_mingw do
  # Optional gem for exporting the gantt to a PNG file, not supported with jruby
  group :rmagick do
    gem "rmagick", ">= 2.14.0"
  end

  # Optional Markdown support, not for JRuby
  group :markdown do
    gem "redcarpet", "~> 3.4.0"
  end
end

# Include database gems for the adapters found in the database
# configuration file
require 'erb'
require 'yaml'

group :development do
  gem "rdoc"
  gem "yard"
  gem 'sqlite3'
end

group :test do
  gem "rails-dom-testing"
  gem "mocha"
  gem "simplecov", "~> 0.14.1", :require => false
  # For running system tests
  gem 'puma', '~> 3.7'
  gem "capybara", '~> 2.13'
  gem "selenium-webdriver"
end

local_gemfile = File.join(File.dirname(__FILE__), "Gemfile.local")
if File.exists?(local_gemfile)
  eval_gemfile local_gemfile
end

# Load plugins' Gemfiles
Dir.glob File.expand_path("../plugins/*/{Gemfile,PluginGemfile}", __FILE__) do |file|
  eval_gemfile file
end

group :production do
  gem 'pg', '~> 1.1.3'
  gem 'rails_12factor'
  gem 'thin' # change this if you want to use other rack web server
end

group :heroku do
  gem "pg", "~> 1.1.3"
end