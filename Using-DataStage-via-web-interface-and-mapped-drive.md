# Using the web interface

### Web interface
_Note: the web interface can't deal with directories ("folders") or files with spaces [ ] in the title.  Any files with spaces in the title will be safely saved, and are accessible from the other interfaces; better to avoid spaces in your file and directory names._

Navigating the interface:
We hope you can do this without instructions.  Just in case, here's how to upload files and add some metadata.

1. Use the "browse data" options (inside the box on the left-hand side) to navigate to your target folder.

2. Click "upload file" (at the top of the screen)

3. Depending on your browser's settings, the details of this step will vary, but you will probably see a pop-up box asking you to browse for a file on your local computer, which you wish to upload to the website.  Select the file and click "upload."
   * Uploading a single file is straightforward: the file will appear on the screen you are currently viewing in your web interface.  You can now edit the "title" and "description" metadata options to add more information if you like. (note: only the "owner" of a file -- which is the person who originally uploaded -- can edit these fields.  Even in the "Collab" directory, and even if you are the Group Leader, you can't edit somebody else's title and description ("metadata")).
   * You can upload whole directories ("folders").  You must first turn the target directory into a .zip file on your local computer.  When you upload a zipped directory, DataStage will automatically unzip it, and unpack the contents -- if you zipped a series of nested folders into one .zip file, DataStage will create that same filetree.  Note: If your zipped folder contains only folders (with whatever content within), no problem.  If it contains only standalone files (of any type), no problem.  However, if there is a mixture of both directories and standalone files, it won't work.  sorry.).
   * Note: If you use subdirectories (e.g. in the "Collab" area), only the owner of the top-most directory can use the web interface to upload further files within that branch of the file structure.  However, other users can upload sub-files or sub-directories via the mapped drive interface (see below) -- and they ill "own" those sub-files, so can edit their own metadata.

4.  The “Permissions” file reminds you which permissions go with that particular user and folder.  We recommend you not delete this – it might be a useful reference for you (or other users) in future.  Deleting the file won't harm anything though.

5.  To delete a file, press "delete" (only the owner of a file may delete it via the web interface -- although if the file is in the "collab" area, other users may delete it using the mapped drive interface). Deleting a file via the web interface seems to have a bug -- file names remain in the list on the web interface, even though they are no longer accessible.  Deleting files via the mapped drive interface does not suffer from this problem -- everything functions as you would expect it should.

Notes:

When editing the file's metadata (title and description fields): depending on your browser configuration, you may see a button saying "update metadata." If so, you must click this in order for your changes to be kept.  If you do not see this button, then simply clicking your mouse somewhere outside the text box (or pressing the "tab" key) should save your changes.  There is currently a bug related to JavaScript, which can cause the web interface to act strangely.  If you notice that the "title" and "description" fields are not editable, or the changes you make do not seem to stick, this is a JavaScript issue.  Some browsers (especially Internet Explorer) have trouble, while others (Firefox, Chrome) usually work fine.  You can still edit these fields if you turn off JavaScript in your browser, but this may have knock-on consequences for other websites which require JavaScript to be turned on.

**Connect to a repository, to enable submissions**
You can connect to your own instance of DataBank, or to other SWORD-compliant repositories.  Here is how to set it up to connect your DataStage to the “demo” instance of DataBank, running on a VM in the Oxford e-Research Centre.
{note: this can be browsed by the general public, and we routinely delete files to make space.  Don’t put anything important here!}

Name: DataBank {call it what you like}
Type: DataBank {user choice, but easiest to call it DataBank for clarity}
Homepage: http://databank-vm1.oerc.ox.ac.uk/sandbox/ {with the final slash}
Authentication: Basic Authentication
{leave the rest blank}
{save}

**Submit some data to the repository**

In your browser bar, go back to your home DataStage page.
For submission:

Navigate into your target folder/subfile
Click "submit"
Repository: DataBank {or whatever you've set up}
Identifier: {the name that DataStage and DataBank will internally use to talk about this datapackage. keep it compact.}
Title: {title visible to people browsing in DataBank.  Make it human-readable}

DataBank demo system credentials:
Username: admin
Password: test

### Other ways to connect: mapped drives (samba) and SFTP

**Mapped drive**
You can map a connection straight to the data server, which will give you direct access to the files.  This uses a protocol called samba -- it is fantastic for local networks where everybody is using wired connections (using ethernet cables).  But samba is not very secure, and for that reason, most internet service providers (including Eduroam, and Virgin Media) block the ports required to do this -- even if your laptop and the server are set up to enable samba, your wireless internet provider will probably stand in your way.  VPN may help you get around this but it is not reliable.  (don't worry -- there's another solution below).

For Windows users: 

Go to Start -> Computer
Maximise that window
Click "map network drive"

For Mac OS users:
From the Mac OS X Finder, hit Command+K to bring up the ‘Connect to Server’ window
Enter the path to the network drive you want to map, (see below) and click ‘Connect’
The drive is now mounted.  Now go to System Preferences, from the Apple menu
Click on ‘Accounts’
Click on “Login Items”
Click on the + button to add another login item
Locate the network drive you just mounted and click “Add”
Exit System Preferences.  Your mapped drive will now reconnect automatically when you start your computer.


Mapped drive path: 
\\{your server's ip address}\datastage  For example, \\192.135.34.5\datastage 

_or if you have set up an outward-facing server, use your url, as follows:_

\\{your url}\datastage  For example, \\www.daflow.ox.ac.uk\datastage

Then enter your user credentials (short username and password).

That should be it -- talk to your IT support team if it doesn't work.


**An alternative for those not sharing a wired network**

If you have to work off-site, or wireless access won't let you use samba, you can use SFTP over port 22.  You will probably have to install an extra client: [WinSCP](http://winscp.net/eng/index.php) for Windows, or [Cyberduck](http://cyberduck.ch/) for Mac.

It’s not quite as nice as a samba connection, but a lot easier that navigating the web interface.

For WinSCP (sorry -- haven't done instructions for Mac.  The process should be similar though.)

1. Download and install WinSCP
2. Launch WinSCP
3. Set new connection:

Host name: {the root of your web address, e.g. dataflow.ox.ac.uk.  No slashes, no http}
Port: 22
User name: {short username}
Password: {your password}
Private key file: (leave blank)
File protocol: SFTP

Pick a colour if you like. It will become the background of your session (useful if you want to set up multiple SFTP connections to DataStage or other servers).  Default is white.

Click Login

If you get a pop-up box with something about the key not being recognised, say “yes” – OK to proceed.

4. You should see a location on your local computer on the left, and /srv/datastage/private/{username} on the right-hand side (your “private” area on the server).

5. On the right-hand side, navigate to your preferred location (if you want to generally work in another location, eg the "Collab" area, navigate there.  E.g. /srv/datastage/collab/{username}

6. On the left-hand side, navigate to wherever you keep relevant files on your home system.

7. From the “Session” drop-down menu at the top, click “save session.”  Give it a name that makes sense to you (e.g. “groupname_datastage”).

8. WinSCP will remember this setup.  Next time you turn on WinSCP, you can go straight to this location without spending time navigating between areas.

_Note: this approach lets you see a lot more of the "back end" of the data server.  User permissions will prevent unauthorised users from seeing other users' "private" files or accidentally changing system files, but this could give malicious users information about the structure of your system, which may lead to security vulnerabilities._

_We recommend adding extra security: you could install [Denyhosts](http://denyhosts.sourceforge.net/) on the server, which can blacklist any IP address unsuccessfully trying to connect more than (x) times._

9. There are some synchronise/update options just under the drop-down menu (little icons, just hover your mouse over them to see what they do).   You can use this if you like – but please be very careful how you set this up, so you don’t inadvertently roll back changes that others have made on shared/collab areas of the filestore.