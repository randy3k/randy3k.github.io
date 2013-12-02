require 'rubygems'
require 'optparse'
require 'yaml'

task :post do
  OptionParser.new.parse!
  ARGV.shift
  title = ARGV.join(' ')

  path = "_posts/#{Date.today}-#{title.downcase.gsub(/[^[:alnum:]]+/, '-')}.md"

  if File.exist?(path)
    puts "[WARN] File exists - skipping create"
  else
    File.open(path, "w") do |file|
      file.puts YAML.dump({'layout' => 'post', 'published' => false, 'title' => title, 'tagline'=> "", 'category' => "", 'tags' => [ ]})
      file.puts "---"
    end
  end
  `subl #{path}`

  exit 0
end

desc "Deploy _site/"
task :deploy do
  puts "\n## Building site"
  status = system("jekyll build")
  if status == false then exit 1 end
  puts "\n## Staging modified files"
  status = system("git add -A")
  puts "\n## Committing a site build at #{Time.now.utc}"
  message = "Build site at #{Time.now.utc}"
  status = system("git commit -m \"#{message}\"")
  puts "\n## Deleting master branch"
  status = system("git branch -D master")
  puts "\n## Creating new master branch and switching to it"
  status = system("git checkout -b master")
  puts "\n## Forcing the _site subdirectory to be project root"
  status = system("git filter-branch --subdirectory-filter _site/ -f")
  puts "\n## Switching back to source branch"
  status = system("git checkout source")
  puts "\n## Pushing all branches to origin"
  status = system("git push --all origin")
end
