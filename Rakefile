require 'rake/testtask'

VERSION = '0.0.1'

def compile_coffee(name, append = false)
  `node_modules/.bin/coffee -p -c src/js/#{name}.coffee #{append ? '>>' : '>'} lib/#{name}.js`
end

task :build do
  File.open('lib/hover.js', 'w') { |f| f.write "// hover.js v#{VERSION} https://github.com/lihanli/hover.js\n" }
  compile_coffee 'hover', true
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