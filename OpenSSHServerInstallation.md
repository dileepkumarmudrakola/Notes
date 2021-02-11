Download the file from https://github.com/PowerShell/Win32-OpenSSH/releases
Extract to C:\OpenSSH-Win64
Add the path in environment variables

Give permision icacls C:\OpenSSH-Win64\libcrypto.dll /grant Everyone:RX


open cmd as administrator  install-sshd.ps1

Open powershell

PS C:\Windows\system32> install-sshd
[SC] SetServiceObjectSecurity SUCCESS
[SC] ChangeServiceConfig2 SUCCESS
[SC] ChangeServiceConfig2 SUCCESS
sshd and ssh-agent services successfully installed
PS C:\Windows\system32> Set-Service sshd -StartupType Automatic
PS C:\Windows\system32> Set-Service ssh-agent -StartupType Automatic
PS C:\Windows\system32> Start-Service sshd
PS C:\Windows\system32> Start-Service ssh-agent
PS C:\Windows\system32> Get-Service -Name *ssh* | select DisplayName, Status, StartType

DisplayName                   Status StartType
-----------                   ------ ---------
OpenSSH Authentication Agent Running Automatic
OpenSSH SSH Server           Running Automatic


PS C:\Windows\system32> Get-NetFirewallRule -Name *SSH*
PS C:\Windows\system32> New-NetFirewallRule -Name sshd -DisplayName 'OpenSSH Server (sshd)' -Enabled True -Direction Inbound -Protocol TCP -Action Allow -LocalPort 22


Name                  : sshd
DisplayName           : OpenSSH Server (sshd)
Description           :
DisplayGroup          :
Group                 :
Enabled               : True
Profile               : Any
Platform              : {}
Direction             : Inbound
Action                : Allow
EdgeTraversalPolicy   : Block
LooseSourceMapping    : False
LocalOnlyMapping      : False
Owner                 :
PrimaryStatus         : OK
Status                : The rule was parsed successfully from the store. (65536)
EnforcementStatus     : NotApplicable
PolicyStoreSource     : PersistentStore
PolicyStoreSourceType : Local



PS C:\Windows\system32> Get-NetFirewallRule -Name *SSH*


Name                  : sshd
DisplayName           : OpenSSH Server (sshd)
Description           :
DisplayGroup          :
Group                 :
Enabled               : True
Profile               : Any
Platform              : {}
Direction             : Inbound
Action                : Allow
EdgeTraversalPolicy   : Block
LooseSourceMapping    : False
LocalOnlyMapping      : False
Owner                 :
PrimaryStatus         : OK
Status                : The rule was parsed successfully from the store. (65536)
EnforcementStatus     : NotApplicable
PolicyStoreSource     : PersistentStore
PolicyStoreSourceType : Local



PS C:\Windows\system32>

src: https://www.saotn.org/manually-install-openssh-in-windows-server/
