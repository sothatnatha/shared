# shared
------------------------------------------ Linux Practice5 ------------------------------------------
# Create group gadmin
	- sudo addgroup gadmin
  
# Create user manager
	- sudo adduser manager

# Give gadmin as group admin
	- sudo vim /etc/sudoers
	- %gadmin ALL=(ALL:ALL) ALL

# Move user manager to group gadmin
	- sudo adduser manager gadmin

# Login user manger and create as below:
+ Directories in root by user manager: 
+ General (both group can full access & manager), 
+ Sale (gacc cannot access), 
+ Accounting (gsale cannot access)
+ Groups: gacc, gsale
+ Users in group gacc: acc1, acc2, acc3
+ Users in group gsale: sale1, sale2, sale3
	- sudo login manager
	- sudo mkdir -p /{General,Sale,Accounting}
	- sudo addgroup gacc
	- sudo addgroup gsale
	
	- sudo adduser acc1
	- sudo adduser acc2
	- sudo adduser acc3

	- sudo adduser sale1
	- sudo adduser sale2
	- sudo adduser sale3

# Add user acc1-3 to group gacc
	- sudo adduser acc1 gacc
	- sudo adduser acc2 gacc	
	- sudo adduser acc3 gacc

# Add user sale1-3 to group gsale
	- sudo adduser sale1 gsale
	- sudo adduser sale2 gsale	
	- sudo adduser sale3 gsale

# Set password change in 20 days on user acc1-3
	- sudo chage -m 20 acc1
	- sudo chage -m 20 acc2
	- sudo chage -m 20 acc3

# Set password change in 40 days on user sale1-3
	- sudo chage -m 40 sale1
	- sudo chage -m 40 sale2
	- sudo chage -m 40 sale3

# Change owner of Accounting, Sale, General
	- sudo chown manager:gacc /Accounting
	- sudo chown manager:gsale /Sale
	- sudo chown manager:manager /General

# Make user manager and group gacc have full access on directory /Accounting
	 - sudo chmod g+w /Accounting

# Make user manager and group gsale have full access on directory /Sale
	 - sudo chmod g+w /Sale

#  Make user manager group gcc, gsale have full access on directory /General
	- sudo chmod g+w /General
	

# Group gsale cannot access /Accounting
	- sudo chmod o-rwx /Accounting

# Group gacc cannot access /Sale
	- sudo chmod o-rwx /Sale

# Other cannot access /General
	- sudo chmod o-rwx /General

## Final Step 

# Add all user in group gacc & gsale to group manager so they're can full access  /General
	- sudo adduser acc1 manager
	- sudo adduser acc2 manager
	- sudo adduser acc3 manager

	- sudo adduser sale1 manager
	- sudo adduser sale2 manager
	- sudo adduser sale3 manager

### Optional (For check directory's permission, owner)
	- ls -l / | grep -E 'Accounting|General|Sale'
------------------------------------------ End Linux Practice 5 ------------------------------------------

----------Password policy------------------
# Password Policy (Strong password)
+ Install: 
	- sudo apt install libpam-pwquality cracklib-runtime
+ Go to configure password:
	- sudo vim /etc/pam.d/common-password
+ Example:
	- password requisite pam_pwquality.so retry=3 minlen=8 lcredit=-1 ucredit=-1 dcredit=-1 ocredit=-1
# Pluggable Authentication Modules (PAM)
	- retry=3: This option will prompt the user 3 times before exiting and returning an error.
	- minlen=8: This specifies that the password cannot be less than 12 characters.
	- ucredit=-1: The option requires at least one uppercase character in the password.
	- lcredit=-1: The option requires at least one lowercase character in the password.
	- dcredit=-1: This implies that the password should have at last a numeric character.
	- ocredit=-1: The option requires at least one special character included in the password.
	- difok=3: This implies that only a maximum of 3 character changes in the new password should be present in the old password.
	- reject_username: The option rejects a password if it consists of the username either in its normal way or in reverse.
	- enforce_for_root: This ensures that the password policies are adhered to even if it’s the root user configuring the passwords.
	- gecoscheck=1  Reject password with account name


----------End Password policy------------------




