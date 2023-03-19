# frozen_string_literal: true

source "https://rubygems.org"
# Old code was pointing to a version which was having layout issues. Currently pointing to a specific tag to make sure UI doesn't break. Revert and point to main branch once the fix is in
# gem "jekyll-theme-chirpy", "~> 5.4", ">= 5.4.0" 
gem "jekyll-theme-chirpy", "= 5.6.0"

group :test do
  gem "html-proofer", "~> 3.18"
end

# Windows and JRuby does not include zoneinfo files, so bundle the tzinfo-data gem
# and associated library.
install_if -> { RUBY_PLATFORM =~ %r!mingw|mswin|java! } do
  gem "tzinfo", "~> 1.2"
  gem "tzinfo-data"
end

# Performance-booster for watching directories on Windows
gem "wdm", "~> 0.1.1", :install_if => Gem.win_platform?
