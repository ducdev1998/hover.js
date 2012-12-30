require 'rake/testtask'

def compile_coffee(name, append = false)
  `node_modules/.bin/coffee -p -c src/js/#{name}.coffee #{append ? '>>' : '>'} lib/#{name}.js`
end

task :build do
  compile_coffee 'hover'
  `sass src/css/style.scss lib/style.css`
  puts 'compile done'
end

task watch: [:build] do
  require 'listen'
  Listen.to('src') do |modified, added, removed|
    Rake::Task["build"].execute
  end
end

Rake::TestTask.new('test') do |t|
  t.libs << "test"
  t.test_files = FileList['test/tests/**/*.rb']
end