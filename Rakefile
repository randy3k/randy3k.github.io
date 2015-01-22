require 'rubygems'
require 'optparse'
require 'yaml'
require "stringex"


desc "Draft a post"
task :draft do
  OptionParser.new.parse!
  ARGV.shift
  title = ARGV.join(' ')
  if title.empty?
    print "title: "
    title = $stdin.gets.strip
  end
  path = "_posts/#{Date.today}-#{title.to_url}.md"

  if File.exist?(path)
    puts "[WARN] File exists - skipping create"
  else
    File.open(path, "w") do |file|
      file.puts YAML.dump({'layout' => 'post', 'title' => title, 'tagline'=> nil,
                          'category' => nil, 'tags' => [ ], 'last_modified' => nil})
      file.puts "---"
    end
  end
  `subl #{path}`
  exit 0
end

desc "Draft a post"
task :draft do
  OptionParser.new.parse!
  ARGV.shift
  title = ARGV.join(' ')
  if title.empty?
    print "title: "
    title = $stdin.gets.strip
  end
  path = "_posts/#{Date.today}-#{title.to_url}.md"

  if File.exist?(path)
    puts "[WARN] File exists - skipping create"
  else
    File.open(path, "w") do |file|
      file.puts YAML.dump({'layout' => 'post', 'title' => title, 'tagline'=> nil,
                          'category' => nil, 'tags' => [ ], 'last_modified' => nil})
      file.puts "---"
    end
  end
  `subl #{path}`
  exit 0
end

desc "Deploy _site/"
task :deploy => [:build]
task :deploy do
  puts "## Staging modified files\n"
  status = system("git add -A")
  puts "## Committing a site build at #{Time.now.utc}\n"
  message = "Build site at #{Time.now.utc}"
  status = system("git commit -m \"#{message}\"")
  puts "## Deleting master branch\n"
  status = system("git branch -D master")
  puts "## Creating new master branch and switching to it\n"
  status = system("git checkout -b master")
  puts "## Forcing the _site subdirectory to be project root\n"
  status = system("git filter-branch --subdirectory-filter _site/ -f")
  puts "## Switching back to source branch\n"
  status = system("git checkout source")
  puts "## Pushing all branches to origin\n"
  status = system("git push --all origin")
end

desc "Build site"
task :build => [:knit]
task :build do
  puts "## Building site\n"
  ENV["JEKYLL_ENV"] = "production"
  status = system("jekyll build")
  if status == false then exit 1 end
end


desc "Knit Rmd"
task :knit do
  puts "## Knitting Rmd\n"
  status = system("R --slave -f _plugins/knitpages.R")
  if status == false then exit 1 end
end
