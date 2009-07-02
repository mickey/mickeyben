require 'rubygems'
require 'git'
require 'net/ssh'
require 'jekyll/lib/jekyll'


require 'rubygems'
require 'git'
require 'net/ssh'
require 'jekyll/lib/jekyll'
 
namespace :publish do
  desc "Publish site content on jtoy.net"
  task :jtoy do
    
    puts "* Publish jtoy.net"
  
    content = 'site-content/'
    remote = 'jtoy.net/'
    branch = 'jtoy.net'
  
    # Use Jekyll to generate site-content
    puts "-- Jekyll process"
    Jekyll.process(content, remote)
  
    # Get last commit message
    puts "-- fetch commit message"
    commit_message = Git.open(content).log.first.message.strip
  
    # Push alexgirard.com
    puts "-- commit and push on #{branch} branch"
    g = Git.open(remote)
    g.add
    g.commit(commit_message)
    g.push("origin", branch)
  
    # Connect to ssh and pull modifications
    puts "-- sync on ssh server"
    Net::SSH.start("jtoy.net") do |ssh|
        ssh.exec! "cd public_html; /home/peeloo/bin/git pull origin #{branch};"
    end
  end
end
 
desc "Publish all content on all sites"
task :publish => ["publish:jtoy] do
  # All happens in sub-task, nthing to be done
end
 


