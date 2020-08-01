require 'rubygems'
require 'rake'

require 'bundler/setup'

begin
  require 'juwelier'

  Juwelier::Tasks.new do |gem|
    gem.name = "domain_inspector"
    gem.summary = "Domain Name Inspection Library"
    gem.description = "A library to extract information and subdomains from top-level domains and registered name from generic and international domain names"
    gem.email = "ayush@hey.com"
    gem.homepage = "http://github.com/ayushn21/domain_inspector"
    gem.authors = [ 'Scott Tadman', 'Ayush Newatia' ]
  end

  Juwelier::GemcutterTasks.new
rescue LoadError
  puts "Juwelier (or a dependency) not available. Install it with: gem install Juwelier"
end

require 'rake/testtask'

Rake::TestTask.new(:test) do |test|
  test.libs << 'lib' << 'test'
  test.pattern = 'test/**/test_*.rb'
  test.verbose = true
end

namespace :domain_inspector do
  desc "Update the domain information"
  task :update do
    require 'open-uri'
    
    open("https://raw.githubusercontent.com/publicsuffix/list/master/public_suffix_list.dat") do |source|
      open(File.expand_path(File.join('data', 'effective_tld_names.dat'), File.dirname(__FILE__)), 'w') do |dest|
        dest.write(source.read)
      end
    end

    open("https://raw.githubusercontent.com/publicsuffix/list/master/tests/test_psl.txt") do |source|
      open(File.expand_path(File.join('test', 'sample', 'test.txt'), File.dirname(__FILE__)), 'w') do |dest|
        dest.write(source.read)
      end
    end
  end
end

task default: :test
