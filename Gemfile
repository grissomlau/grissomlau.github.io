source 'https://rubygems.org'

gem "jekyll", "~> 4.3" # installed by `gem jekyll`
# gem "webrick"        # required when using Ruby >= 3 and Jekyll <= 4.2.2

# gem "just-the-docs", "0.5.0" # pinned to the current release
gem "just-the-docs"        # always download the latest release


# Windows and JRuby does not include zoneinfo files, so bundle the tzinfo-data gem
# and associated library.
if RUBY_PLATFORM=~ /win32/ 
    platforms :mswin do
    gem "tzinfo", ">= 1", "< 3"
    gem "tzinfo-data"
    # Performance-booster for watching directories on Windows
    gem "wdm", "~> 0.1.1", :platforms => [:mingw, :x64_mingw, :mswin]

    # Lock `http_parser.rb` gem to `v0.6.x` on JRuby builds since newer versions of the gem
    # do not have a Java counterpart.
    gem "http_parser.rb", "~> 0.6.0", :platforms => [:jruby]

    end
end

