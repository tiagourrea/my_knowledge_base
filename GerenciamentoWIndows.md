WINRM

Como configurar

winrm quickconfig -transport:https

Disabling the WinRM Service and Listener:

**Stop the WinRM Service**

`Stop-Service -Name winrm -Force`

**Disable the WinRM Service from starting automatically**

`Set-Service -Name winrm -StartupType Disabled`

Delete WinRM Listeners.

winrm delete winrm/config/listener?Address=*+Transport=HTTP

winrm delete winrm/config/listener?Address=*+Transport=HTTPS

Troca Certificado do Listener

````
param([Parameter(Mandatory=$true)]
$certThumb)

Set-WSManInstance -ResourceURI winrm/config/Listener -SelectorSet @{Address="*"; Transport="HTTPS"} -ValueSet @{CertificateThumbprint=$certThumb}
````

winrm create winrm/config/Listener?Address=*+Transport=HTTPS '@{Hostname="<YOUR_SERVER_HOSTNAME>";CertificateThumbprint="<CERTIFICATE_THUMBPRINT_WITHOUT_SPACES>";Port="5986"}'
