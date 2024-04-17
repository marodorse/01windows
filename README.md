# WINDOWS 101

## In the beginning there was ...

The ISO image to start the process of installing windows 10 Pro from [here](https://info.microsoft.com/ww-landing-windows-10-enterprise.html)


with alocated virtual harddrive details : 
 30 GB of storage space   
 2048MB of RAM  
 2 CPUS 

--------------------------------
Once the VM is started there are the following steps to do :
1. choose time zone/ currency, keyboard layout and language to install
2. accept the license terms 
3. custom install -> okay 
4. select region
5. keyboard
6. sign in with setting up a local account called admin and password admin
7. create security questions we picked the first 3 questions and put admin as answers. 
8. follow the rest of the installation. 

To create User Alice and Bob from powershell : 
start with making a password and saving it into a variable called Password.
```
$Password = Read-Host -AsSecureString
```	
enter the password  and press enter. Then Let's add the user.

```
New-LocalUser "UserName" -Password $Password -fullname "UserFullName" -Description "account description"
```	
No lets add the User to its corresponding group :

```
Add-LocalGroupMember -Group "GroupName" -member "UserName"
```

to grant access for Bob user to `/Users/Bob` 

```
$ACL = Get-ACL -Path "\Users\Bob"
$AccessRule = New-Object System.Security.AccessControl.FileSystemAccessRule("Bob","FullControl","Allow")
$ACL.SetAccessRule($AccessRule)
$ACL | Set-Acl -Path "\Users\Bob"
(Get-ACL -Path "\Users\Bob").Access | Format-Table IdentityReference,FileSystemRights,AccessControlType,IsInherited,InheritanceFlags -AutoSize
```

**To forbid User Bob from accessing any other file other than his folder do:**  

from the admin account right click and Local Disk (C:) and go to _Property_ then go to _Edit_ Click on Bob and click on _Remove_ And tada Bob will be totally unable to access any other file of Local Disk (C:) other than his own path.


## windows defender set up (Built-in Antivirus software)
settings -> update & security -> windows security -> virus threat protection -> manage settings -> turn on real time protection if its not already the case.    
To make this permanent type in search bar `registry Editor` open HKEY LOCAL MACHINE then software then policy options -> microsoft -> windows defender -> right click below default and option new. DWORD 32-bit value option -> Name it DisableAntiSpyware -> in Value data put 0. Which turns on windows defender then restart machine.

---
## Firewall configuration
follow same step as for defedender except go to Firewall & network protection check if all is on. 

Go to advance