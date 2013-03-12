**Using the web interface**

Navigating the interface:
We hope you can do this without instructions.  Just in case, here's how to upload files and add some metadata.

# Use the "browse data" options (inside the box on the left-hand side) to navigate to your target folder.

# Click "upload file" (at the top of the screen)

# Depending on your browser's settings, the details of this step will vary, but you will probably see a pop-up box asking you to browse for a file on your local computer, which you wish to upload to the website.  Select the file and click "upload."
   * Uploading a single file is straightforward: the file will appear on the screen you are currently viewing in your web interface.  You can now edit the "title" and "description" metadata options to add more information if you like. (note: only the "owner" of a file -- which is the person who originally uploaded -- can edit these fields.  Even in the "Collab" directory, and even if you are the Group Leader, you can't edit somebody else's title and description ("metadata")).
   * You can upload whole directories ("folders").  You must first turn the target directory into a .zip file on your local computer.  When you upload a zipped directory, DataStage will automatically unzip it, and unpack the contents -- if you zipped a series of nested folders into one .zip file, DataStage will create that same filetree.  Note: If your zipped folder contains only folders (with whatever content within), no problem.  If it contains only standalone files (of any type), no problem.  However, if there is a mixture of both directories and standalone files, it won't work.  sorry.).
   * Note: If you use subdirectories (e.g. in the "Collab" area), only the owner of the top-most directory can use the web interface to upload further files within that branch of the file structure.  However, other users can upload sub-files or sub-directories via the mapped drive interface (see below) -- and they ill "own" those sub-files, so can edit their own metadata.

# The “Permissions” file reminds you which permissions go with that particular user and folder.  We recommend you not delete this – it might be a useful reference for you (or other users) in future.  Deleting the file won't harm anything though.

# To delete a file, press "delete" (only the owner of a file may delete it via the web interface -- although if the file is in the "collab" area, other users may delete it using the mapped drive interface). Deleting a file via the web interface seems to have a bug -- file names remain in the list on the web interface, even though they are no longer accessible.  Deleting files via the mapped drive interface does not suffer from this problem -- everything functions as you would expect it should.

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

**Using a mapped drive**