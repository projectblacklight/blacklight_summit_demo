# Add your own tasks in files placed in lib/tasks ending in .rake,
# for example lib/tasks/capistrano.rake, and they will automatically be available to Rake.

require File.expand_path('../config/application', __FILE__)
task default: [:ci]


Rails.application.load_tasks

require 'solr_wrapper/rake_task' unless Rails.env.production?

desc 'Run test suite'
task :ci do
  solr_config_dir = File.join(File.dirname(__FILE__), 'solr', 'conf')

  SolrWrapper.wrap(port: '8983') do |solr|
    solr.with_collection(name: 'blacklight-core',
                         dir: solr_config_dir) do
      Rake::Task['spec'].invoke
    end
  end
end
