require 'rubygems'
require 'optparse'
require 'yaml'
require 'less'

desc "Draft a post"
task :draft do
  OptionParser.new.parse!
  ARGV.shift
  title = ARGV.join(' ')
  if title.empty?
    print "title: "
    title = $stdin.gets
  end
  path = "_posts/#{Date.today}-#{title.downcase.gsub(/[^[:alnum:]]+/, '-')}.md"

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
task :draftr do
  OptionParser.new.parse!
  ARGV.shift
  title = ARGV.join(' ')
  if title.empty?
    print "title: "
    title = $stdin.gets
  end

  path = "_R/#{Date.today}-#{title.downcase.gsub(/[^[:alnum:]]+/, '-')}.md"

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
  status = system("jekyll build")
  if status == false then exit 1 end
end


CONFIG = Hash.new
CONFIG['less'] = "bootstrap/less"
CONFIG['css'] = File.join("assets", "css")
CONFIG['input'] = "bootstrap.less"
CONFIG['output'] = "bootstrap.css"

desc "Compile Less"
task :lessc do
  less   = CONFIG['less']

  input  = File.join( less, CONFIG['input'] )
  output = File.join( CONFIG['css'], CONFIG['output'] )

  source = File.open( input, "r" ).read
  parser = Less::Parser.new( :paths => [less] )
  tree = parser.parse( source )

  File.open( output, "w+" ) do |f|
    f.puts tree.to_css( :compress => true )
  end
end

desc "Knit Rmd"
task :knit do
  puts "## Knitting Rmd\n"
  status = system("R --slave -f _plugins/knitpages.R")
  if status == false then exit 1 end
end