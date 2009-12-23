desc "deploy site to mickeyben.com"
task :deploy do
  require 'rubygems'
  require 'highline/import'
  require 'net/ssh'
 
  branch = "master"
 
  username = ask("Username: ") { |q| q.echo = true }
  password = ask("Password: ") { |q| q.echo = "*" }
 
  Net::SSH.start('mickeyben.com', username, :password => password) do |ssh|
    commands = <<EOF
cd ~/tmp/mickeyben
git pull
rm -rf _site
jekyll
cp -rf _site/* ~/www/
EOF
    commands = commands.gsub(/\n/, "; ")
    ssh.exec commands
  end
end