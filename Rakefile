task :default => [:hey_dummy]

task :hey_dummy do
  puts 'Hey dummy, you need to specify a Rake task!'
  puts 'Try running "rake --describe" for more options.'
end

desc 'Delete generated _site files'
task :clean do
  system 'rm -rf _site'
end

desc 'Compile assets and start the jekyll server'
task :dev do
  pids = [
      spawn('bundle exec jekyll serve --watch'),
      spawn('bundle exec sass --watch assets/css:stylesheets'),
    ]
  
  trap "INT" do
    Process.kill "INT", *pids
    exit 1
  end

  loop do
    sleep 1
  end
end

# TODO: I should be able to not type the post date, i.e. not have 
# to type `rake publish[YYYY-MM-DD-the-post-title]`
desc 'Publish a post from _drafts'
task :publish, :title do |command, args|
  filename = args.title.split( /_drafts\/|_posts\// ).last
  raise RuntimeError.new('no draft specified!') if filename.nil? || filename.empty?
  puts "Removing _posts/#{filename}"
  system("rm _posts/#{filename}")
  puts "Moving #{filename} from _drafts/ to _posts/"
  system("mv _drafts/#{filename} _posts/#{filename}")
end

# Note: all my posts are in the "posts" category, but I may add additional 
# categories in the future. Might add "how-to" as a category, but I 
# could also just add a "how-to" tag to posts.
desc "Given a title as an argument, create a new post file"
task :scaffold, :title do |le_task, args|
  title = args.title
  if title.nil? || title.empty?
    print "Enter post title: "
    title = STDIN.gets.chomp
    raise RuntimeError.new("Title cannot be empty!") if title.nil? || title.empty?
  end
  filename = "#{Time.now.strftime('%Y-%m-%d')}-#{title.gsub(/[\s\W]/, '-').downcase}.md"
  Dir.mkdir("_drafts") unless Dir.exist?("_drafts")
  path = File.join("_drafts", filename)
  if File.exist? path; raise RuntimeError.new("Won't clobber #{path}"); end
  raise RuntimeError.new("Won't clobber #{path}") if File.exist?(path)
  File.open(path, 'w') do |file|
    file.write <<-EOS
---
layout: post
category: posts
title: #{title}
date: #{Time.now.strftime('%Y-%m-%d %k:%M:%S')}
---
EOS
    end
  system("ln #{path} _posts/#{filename}")
  puts "Template post created at: #{path} \nGo forth and blog!"
end
