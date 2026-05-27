source "https://rubygems.org"

gem "jekyll", "~> 4.3"
gem "minimal-mistakes-jekyll"

# Ruby 3.0+ no longer ships these as default gems
gem "webrick", "~> 1.8"
gem "csv"
gem "base64"
gem "bigdecimal"

group :jekyll_plugins do
  gem "jekyll-include-cache"
  gem "jekyll-feed"
  gem "jekyll-seo-tag"
  gem "jekyll-sitemap"
  gem "jekyll-paginate"
end

# Windows and JRuby do not include zoneinfo files, so bundle the tzinfo-data gem
platforms :mingw, :x64_mingw, :mswin, :jruby do
  gem "tzinfo", ">= 1", "< 3"
  gem "tzinfo-data"
end

# Performance booster for watching directories on Windows
gem "wdm", "~> 0.2.0", :platforms => [:mingw, :x64_mingw, :mswin]
