task :default => [:hey_dummy]

task :hey_dummy do
  puts 'Hey dummy, you need to specify a Rake task!'
  puts 'Try running "rake --describe" for more options.'
end

# "--auto" regenerates the site automatically when files are changed
desc 'Runs Jekyll server locally on port 4000'
task :dev do
  system('jekyll --server --auto')
end

# Note: all my posts are in the "posts" category, but I made add additional 
# categories in the future. Might add "how-to" as a category, but I 
# could also just add a "how-to" tag to posts.
desc "Given a title as an argument, create a new post file"
task :post, :title do |le_task, args|
  filename = "#{Time.now.strftime('%Y-%m-%d')}-#{args.title.gsub(/\s/, '_').downcase}.markdown"
  path = File.join("_posts", filename)
  if File.exist? path; raise RuntimeError.new("Won't clobber #{path}"); end
  File.open(path, 'w') do |file|
    file.write <<-EOS
---
layout: post
category: posts
title: #{args.title}
date: #{Time.now.strftime('%Y-%m-%d %k:%M:%S')}
---
EOS
    end
    puts "Template post created at: #{path} \nGo forth and blog!"
end
