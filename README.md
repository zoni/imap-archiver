imap-archiver
-------------

Rake tasks which wrap offlineimap for the purpose of making it quick and easy to archive an IMAP mailbox

Requirements
============

* Ruby
* Rake (Tip: gem install rake)

Usage
=====

Simply run `rake` to backup a GMail mailbox and be prompted interactively for your username and password.

Alternatively, modify `offlineimaprc.erb` to change the remote server or other parameters. Add `user=username` on the command line after the invocation to rake to specify the username on the command line, or add `compressor=gz` to compress the archive with gzip (you can also use xz, bz2 or any other suffix understood by tar's `--auto-compress`).

Demo
====

	$ rake user=n.groenen@am-impact.nl compressor=xz
	offlineimap -c offlineimaprc
	OfflineIMAP 6.5.4
	  Licensed under the GNU GPL v2+ (v2 or any later version)
	Account sync Account1:
	 *** Processing account Account1
	 Establishing connection to imap.gmail.com:993
	Enter password for account 'Remote': 
	 Creating folder [Gmail].Sent Mail[Local]
	 Creating folder [Gmail].All Mail[Local]
	Folder [Gmail]/All Mail [acc: Account1]:
	 Syncing [Gmail]/All Mail: IMAP -> Maildir
	Folder [Gmail]/Sent Mail [acc: Account1]:
	 Syncing [Gmail]/Sent Mail: IMAP -> Maildir
	 Establishing connection to imap.gmail.com:993
	 Copy message 1 (1 of 2336) Remote:[Gmail]/Sent Mail -> Local
	 Copy message 2 (2 of 2336) Remote:[Gmail]/Sent Mail -> Local
	Copy message from Remote:[Gmail]/Sent Mail:
	 Establishing connection to imap.gmail.com:993
	Folder [Gmail]/Sent Mail [acc: Account1]:
	 Copy message 3 (3 of 2336) Remote:[Gmail]/Sent Mail -> Local
	 Copy message 4 (4 of 2336) Remote:[Gmail]/Sent Mail -> Local
	Copy message from Remote:[Gmail]/Sent Mail:
	 Establishing connection to imap.gmail.com:993
	 Establishing connection to imap.gmail.com:993
	Folder [Gmail]/Sent Mail [acc: Account1]:
	 Copy message 5 (5 of 2336) Remote:[Gmail]/Sent Mail -> Local
	 Copy message 6 (6 of 2336) Remote:[Gmail]/Sent Mail -> Local
	 Copy message 7 (7 of 2336) Remote:[Gmail]/Sent Mail -> Local
	 Copy message 8 (8 of 2336) Remote:[Gmail]/Sent Mail -> Local
	Folder [Gmail]/All Mail [acc: Account1]:
	 Copy message 1 (1 of 13746) Remote:[Gmail]/All Mail -> Local
	Folder [Gmail]/Sent Mail [acc: Account1]:
	 Copy message 9 (9 of 2336) Remote:[Gmail]/Sent Mail -> Local
	Folder [Gmail]/All Mail [acc: Account1]:
	 Copy message 2 (2 of 13746) Remote:[Gmail]/All Mail -> Local
	Folder [Gmail]/Sent Mail [acc: Account1]:
	 Copy message 10 (10 of 2336) Remote:[Gmail]/Sent Mail -> Local
	Folder [Gmail]/All Mail [acc: Account1]:
	 Copy message 3 (3 of 13746) Remote:[Gmail]/All Mail -> Local
	Folder [Gmail]/Sent Mail [acc: Account1]:
	 Copy message 11 (11 of 2336) Remote:[Gmail]/Sent Mail -> Local
	[Some time later...]
	Account sync Account1:
	 *** Finished account 'Account1' in 0:00
	tar --auto-compress --create --file n.groenen@am-impact.nl.tar.xz n.groenen@am-impact.nl

	$ ls
	n.groenen@am-impact.nl  n.groenen@am-impact.nl.tar.xz  offlineimaprc.erb  Rakefile  README.md
	$ ls n.groenen@am-impact.nl/
	[Gmail].All Mail  [Gmail].Sent Mail

License
=======

This code is public domain. Do with it as you see fit. :)
