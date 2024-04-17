# WINDOWS 101

## TO BEGIN WITH

lets get the ISO image to start the process of installing windows 10 Pro from [here](https://info.microsoft.com/ww-landing-windows-10-enterprise.html)

--------------------------------
alocated virtual harddrive details : 
 30 GB of storage space
 2048MB of RAM
 2 CPUS 

--------------------------------

1. choose time zone/ currency, keyboard layout and language to install
2. accept the license terms 
3. custom install -> okay 
4. select region
5. keyboard
6. sign in with setting up a local account called admin and password admin
7. create security questions we picked the first 3 questions and put admin as answers. 
8. follow the rest of the installation. 


to grant access for Bob user to /Users/Bob
```
    $ACL = Get-Acl -Path "C:\Users\Bob
    $User = New-Object System:security:Principal:Ntaccount("Bob") 
    $ACL.SetOwner($User)
    $ACL | Set-Acl -Path "C:\Users\Bob
    Get-ACL -Path "C:\Users\Bob" 
    ```
```
​$ACL = Get-ACL -Path "\Users\Bob"
$AccessRule = New-Object System.Security.AccessControl.FileSystemAccessRule("Bob","FullControl","Allow")
$ACL.SetAccessRule($AccessRule)
$ACL | Set-Acl -Path "\Users\Bob"
(Get-ACL -Path "\Users\Bob").Access | Format-Table IdentityReference,FileSystemRights,AccessControlType,IsInherited,InheritanceFlags -AutoSize```

To forbid User Bob from accessing any other file other than his folder do :
from the admin account right click and Local Disk (C:) and go to _Property_ then go to _Edit_ Click on Bob and click on _Remove_ And tada Bob will be totally unable to access any other file of Local Disk (C:) other than his own path.

---