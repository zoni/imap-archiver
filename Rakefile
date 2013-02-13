require 'erb'

task :default => [:sync, :archive, :rmconfig, :rmmaildir]

task :prepenv do
	if ENV['user'].nil?
		print "Please specify the username of the email account to run with: "
		# Specifically use $stdin.gets to avoid occasional
		# 'No such file or directory - user=...' error
		ENV['user'] = $stdin.gets.strip 
	end
end

desc "Generate a config file for offlineimap"
task :mkconfig => :prepenv do
	# Used for random account number to allow multiple simultanious executions
	random = Random.new.rand 1000000 
	config = ERB.new(File.read 'offlineimaprc.erb')
	File.open('offlineimaprc', 'w') do |f|
		f << config.result(binding)
	end
end

desc "Remove the generated config file for offlineimap"
task :rmconfig do
	if File.exists? 'offlineimaprc'
		File.unlink 'offlineimaprc'
	end
end

desc "Sync an IMAP resource"
task :sync => :mkconfig do
	if !system "which offlineimap > /dev/null 2>&1"
		fail "Couldn't find the offlineimap program in your $PATH"
	else
		sh "offlineimap -c offlineimaprc"
	end
end

desc "Archive local maildir"
task :archive => :prepenv do
	if !File.exists? ENV['user'] 
		fail "Maildir seems to be missing. Did you run `rake sync`?"
	else
		# This looks a bit like magic, but ensures there's no suffix after .tar in case compressor
		# is nil or an empty string. This lets one do compressor= to only make a tar archive, or 
		# compressor=gz|bz2|xz|whichever to compress with that 
		compressor = ENV['compressor'].nil? || ENV['compressor'].strip == '' ? '' : '.' << ENV['compressor']
		sh "tar --auto-compress --create --file #{ENV['user']}.tar#{compressor} #{ENV['user']}"
	end
end

task :rmmaildir => :sync do
	FileUtils.rm_r ENV['user']
end
