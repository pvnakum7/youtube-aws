## Github : https://github.com/pvnakum7/

### Error during command add and solutions:
## ref: https://osxdaily.com/2018/05/24/command-not-found-mac-terminal-error-fix/ and https://docs.brew.sh/Installation
## if commnad not work then ## as per the error you need to allow commnad for permission allow:
### inside output of command:  Then use some output of the above command error you can enable it for command permission


Step1: 
### Connect remote connection from AWS console: or connect SSH connection using pem file:
ssh -i path-of-instance-pem-file.pem ec2-user@instance-ip

## type below command to set ec2-user password:
sudo dscl . -passwd /Users/ec2-user NewMyPassword12


Step2:
### remote enabled command: 
## reference Link: https://www.techrepublic.com/article/how-to-enable-screen-sharing-on-macs-via-terminal/
## and: https://repost.aws/knowledge-center/ec2-mac-instance-gui-access
### for all user remote enable
sudo /System/Library/CoreServices/RemoteManagement/ARDAgent.app/Contents/Resources/kickstart -activate -configure -access -off -restart -agent -privs -all -allowAccessFor -allUsers


sudo defaults write /var/db/launchd.db/com.apple.launchd/overrides.plist com.apple.screensharing -dict Disabled -bool false

sudo launchctl load -w /System/Library/LaunchDaemons/com.apple.screensharing.plist


Step3: 
### Create User using command line:
# Command 1: 
sudo dscl . -create /Users/test UserShell /bin/bash

###  Command 2: 
sudo dscl . -create /Users/test test "nakum test"

### Command 3: add user group id
sudo dscl . -create /Users/test PrimaryGroupID 1000

####  Step 4: create directory
sudo dscl . -create /Users/test NFSHomeDirectory /Local/Users/test

## Command 5: reset password
sudo dscl . -passwd /Users/test MyPassword12

### Command 6: add user into admin group
sudo dscl . -append /Groups/admin GroupMembership test

## Command 7: check user available in group or not
sudo dscl . -read /groups/admin GroupMembership

## Reference link: https://www.alphr.com/create-admin-mac-terminal/

## All steps:
sudo dscl . -create /Users/test1 UserShell /bin/bash

sudo dscl . -create /Users/test1 RealName "My test1"

sudo dscl . -create /Users/test1 PrimaryGroupID 1000

sudo dscl . -create /Users/test1 NFSHomeDirectory /Local/Users/test1

sudo dscl . -passwd /Users/test1 MyPassword12

sudo dscl . -append /Groups/admin GroupMembership test1

sudo dscl . -read /groups/admin GroupMembership


Step4:  
## Again enabled remote login for all user:  
## ref: https://www.techrepublic.com/article/how-to-enable-screen-sharing-on-macs-via-terminal/

sudo /System/Library/CoreServices/RemoteManagement/ARDAgent.app/Contents/Resources/kickstart -activate -configure -access -off -restart -agent -privs -all -allowAccessFor -allUsers


Step 5: 
#### For Remote Connection:
### open screen sharing app:
add ip , username and password to connect:

## If you are not able to login with created new user with command then delete that user using with below command:
## and create new user with step 7.
## For Delete user:
sudo /usr/bin/dscl . -delete /Users/test1


Step6: 
### open screen sharing app with login
# username: your-username (default first time username= ec2-user) and password:
enter Instance IP it enter and add username and password

(For windows: 
-- windows file explorar and type ip 

-- and enter username and password when you have set during create ec2 instance 

-- or created after ssh connection from console or using pem file.
-- after password enter you are able to see the screen
)






Step7: 
## Creating new User with Mac s console interface
### goto setting and general-->sharing option

so now go to setting--> user and group--> create new user and set as admin/standard with set password

After that logout from current user and login with new user( follow the step 6).











