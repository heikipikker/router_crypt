begin
  require 'bundler'
  require 'bundler/gem_tasks'
  require 'rspec/core/rake_task'
  Bundler.setup
rescue LoadError
  warn 'missing dependencies'
  exit 42
end


gemspec = eval(File.read(Dir['*.gemspec'].first))

desc 'Validate the gemspec'
task :gemspec do
  gemspec.validate
end

RSpec::Core::RakeTask.new(:spec)

#desc "Build gem locally"
#task :build => %i(spec gemspec) do
#  system "gem build #{gemspec.name}.gemspec"
#  FileUtils.mkdir_p "gems"
#  FileUtils.mv "#{gemspec.name}-#{gemspec.version}.gem", "gems"
#end

##desc "Install gem locally"
##task :install => :build do
##  system "sudo sh -c \'umask 022; gem20 install gems/#{gemspec.name}-#{gemspec.version}\'"
##end

desc "Clean automatically generated files"
task :clean do
  FileUtils.rm_rf "gems"
end

desc 'Tag the release'
task :tag do
  system "git tag #{gemspec.version}"
  end

desc 'Push to rubygems'
task :push => :tag do
    system "gem push pkg/#{file}"
end

task default: :spec
