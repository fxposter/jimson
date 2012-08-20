require 'rubygems'
require 'rake'
require 'rspec/core/rake_task'
require 'bundler/gem_helper'

class GemInABoxTasks < Bundler::GemHelper
  protected
  def rubygem_push(path)
    sh("gem inabox")
    Bundler.ui.confirm "Pushed #{name} #{version} to gems.wixpress.com"
  end
end

GemInABoxTasks.install_tasks

desc "Run all specs"
RSpec::Core::RakeTask.new(:rspec) do |spec|
  spec.pattern = 'spec/**/*_spec.rb'
end

RSpec::Core::RakeTask.new(:rcov) do |spec|
  spec.pattern = 'spec/**/*_spec.rb'
  spec.rcov = true
end

task :default => :rspec

begin
  require 'rdoc/task'
rescue LoadError
  require 'rake/rdoctask'
end

Rake::RDocTask.new do |rdoc|
  version = File.exist?('VERSION') ? File.read('VERSION') : ""

  rdoc.rdoc_dir = 'rdoc'
  rdoc.title = "jimson #{version}"
  rdoc.rdoc_files.include('README*')
  rdoc.rdoc_files.include('lib/**/*.rb')
end
