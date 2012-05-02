DataStage -
1/ Queries for Service Documents (GET on SD-IRI, spec section 6.1) 2/ Creates items in the repository with only an atom entry (POST Entry to Col-IRI, spec section 6.3.3) 3/ Queries for Entry Documents (GET on Edit-IRI) 4/ Updates items in the repository by sending the zipped content as a package (PUT Package to EM-IRI, spec section 6.5.1)

Some useful resources:

Client library in python: https://github.com/swordapp/python-client-sword2

Client library in java: https://github.com/swordapp/JavaClient2.0

Client library in PHP: https://github.com/stuartlewis/swordappv2-php-library/

Client library in Ruby: https://github.com/CottageLabs/sword2ruby

Simple Sword Server (python out-of-the-box server environment):
http://sword-app.svn.sourceforge.net/viewvc/sword-app/sss/branches/sss-2/

The SWORDv2 Spec:
http://sword-app.svn.sourceforge.net/viewvc/sword-app/spec/trunk/SWORDProfile.html?revision=510

A DSpace fork with a stabilised SWORDv2 webapp (use this branch, not the master): https://github.com/nye-duo/DSpace/tree/duo
