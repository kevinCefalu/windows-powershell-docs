---
description: Use this topic to help manage Windows and Windows Server technologies with Windows PowerShell.
external help file: Microsoft.DirectoryServices.Deployment.dll-Help.xml
Module Name: ADDSDeployment
ms.date: 12/27/2016
online version: https://learn.microsoft.com/powershell/module/addsdeployment/install-addsdomaincontroller?view=windowsserver2022-ps&wt.mc_id=ps-gethelp
schema: 2.0.0
title: Install-ADDSDomainController
---

# Install-ADDSDomainController

## SYNOPSIS
Installs a new domain controller in an Active Directory domain.

## SYNTAX

### ADDSDomainController (Default)

```
Install-ADDSDomainController [-SkipPreChecks] -DomainName <String>
[-SafeModeAdministratorPassword <SecureString>] [-SiteName <String>]
[-ADPrepCredential <PSCredential>] [-AllowDomainControllerReinstall]
[-ApplicationPartitionsToReplicate <String[]>] [-CreateDnsDelegation]
[-Credential <PSCredential>] [-CriticalReplicationOnly] [-DatabasePath <String>]
[-DnsDelegationCredential <PSCredential>] [-NoDnsOnNetwork] [-NoGlobalCatalog]
[-InstallationMediaPath <String>] [-InstallDns] [-LogPath <String>]
[-MoveInfrastructureOperationMasterRoleIfNecessary] [-NoRebootOnCompletion]
[-ReplicationSourceDC <String>] [-SkipAutoConfigureDns] [-SystemKey <SecureString>]
[-SysvolPath <String>] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]
```

### ADDSDomainControllerReadOnly

```
Install-ADDSDomainController [-SkipPreChecks] -DomainName <String>
 [-SafeModeAdministratorPassword <SecureString>] -SiteName <String> 
 [-ADPrepCredential <PSCredential>] [-AllowDomainControllerReinstall]
 [-AllowPasswordReplicationAccountName <String[]>]
 [-ApplicationPartitionsToReplicate <String[]>] [-Credential <PSCredential>]
 [-CriticalReplicationOnly] [-DatabasePath <String>]
 [-DelegatedAdministratorAccountName <String>]
 [-DenyPasswordReplicationAccountName <String[]>] [-NoDnsOnNetwork] [-NoGlobalCatalog]
 [-InstallationMediaPath <String>] [-InstallDns] [-LogPath <String>]
 [-MoveInfrastructureOperationMasterRoleIfNecessary] [-ReadOnlyReplica]
 [-NoRebootOnCompletion] [-ReplicationSourceDC <String>] [-SkipAutoConfigureDns]
 [-SystemKey <SecureString>] [-SysvolPath <String>] [-Force] [-WhatIf] [-Confirm]
 [<CommonParameters>]
```

### ADDSDomainControllerUseExistingAccount

```
Install-ADDSDomainController [-SkipPreChecks] -DomainName <String>
 [-SafeModeAdministratorPassword <SecureString>] [-ADPrepCredential <PSCredential>]
 [-ApplicationPartitionsToReplicate <String[]>] [-Credential <PSCredential>]
 [-CriticalReplicationOnly] [-DatabasePath <String>] [-NoDnsOnNetwork]
 [-InstallationMediaPath <String>] [-LogPath <String>] [-NoRebootOnCompletion]
 [-ReplicationSourceDC <String>] [-SkipAutoConfigureDns] [-SystemKey <SecureString>]
 [-SysvolPath <String>] [-UseExistingAccount] [-Force] [-WhatIf] [-Confirm]
 [<CommonParameters>]
```

## DESCRIPTION

The `Install-ADDSDomainController` cmdlet installs a domain controller in Active Directory.

## EXAMPLES

### Example 1: Install a domain controller and DNS server

```powershell
Install-ADDSDomainController -InstallDns -DomainName "corp.contoso.com"
```

This command installs a domain controller and DNS server in the `corp.contoso.com` domain using
`CORP\Administrator` credentials and prompts the user to provide and confirm the Directory Services
Restore Mode (DSRM) password.

### Example 2: Install a domain controller and DNS server using administrator credentials

```powershell
$HashArguments = @{
    Credential = (Get-Credential "CORP\Administrator")
    DomainName = "corp.contoso.com"
    InstallDns = $true
}
Install-ADDSDomainController @HashArguments
```

This command installs a domain controller and DNS server in the `corp.contoso.com` domain using
Administrator credentials and prompts the user to provide and confirm the DSRM password.

### Example 3: Install a domain controller and DNS server that uses domain promotion

```powershell
$HashArguments = @{
    Credential = (Get-Credential)
    DomainName = (Read-Host "Domain to promote into")
    InstallDns = $true
}
Install-ADDSDomainController @HashArguments
```

Installs a domain controller and DNS server and prompts for credentials, the name of the domain to
use when installing and promoting the domain controller and to provide and confirm the DSRM
password.

## PARAMETERS

### -ADPrepCredential

Specifies the user name and password that corresponds to the account to be used for running the
Adprep utility, if it is required, to prepare the directory prior to the installation of this domain
controller. Use the `Get-Credential` cmdlet to prompt the user to supply a password.

```yaml
Type: System.Management.Automation.PSCredential
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: NULL
Accept pipeline input: False
Accept wildcard characters: False
```

### -AllowDomainControllerReinstall

Indicates that the cmdlet continues to install this domain controller, despite the fact that another
domain controller account with the same name is detected. By default, the
`Install-ADDSDomainController` cmdlet does not continue the installation if another domain
controller with the same name is found.

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: ADDSDomainController, ADDSDomainControllerReadOnly
Aliases: 

Required: False
Position: Named
Default value: NULL
Accept pipeline input: False
Accept wildcard characters: False
```

### -AllowPasswordReplicationAccountName

Specifies an array of names of user accounts, group accounts, and computer accounts whose passwords
can be replicated to this RODC. Use an empty string (`""`) if you want to keep the value empty. By
default, only the `Allowed` read-only domain controller (RODC) Password Replication Group is
allowed.

```yaml
Type: System.String[]
Parameter Sets: ADDSDomainControllerReadOnly
Aliases: 

Required: False
Position: Named
Default value: NULL
Accept pipeline input: False
Accept wildcard characters: False
```

### -ApplicationPartitionsToReplicate

Specifies an array of application directory partitions that DCPromo will replicate.
Use the following format: "partition1" "partition2" "partitionN".
Use * to replicate all application directory partitions.

```yaml
Type: System.String[]
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: NULL
Accept pipeline input: False
Accept wildcard characters: False
```

### -Confirm

Prompts you for confirmation before running the cmdlet.

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: (All)
Aliases: cf

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### -CreateDnsDelegation

Indicates that the cmdlet creates a DNS delegation that references the new DNS server that this
cmdlet installs along with the domain controller. Valid for Active Directory-integrated DNS only.
If this parameter is specified then the DNS delegation is created. If the value of `$False` is
specified then no DNS delegation is created. By default, the value for this parameter is computed
automatically based on the environment.

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: ADDSDomainController
Aliases: 

Required: False
Position: Named
Default value: NULL
Accept pipeline input: False
Accept wildcard characters: False
```

### -Credential

Specifies the user name and password that corresponds to the account used to install the domain
controller. Use the `Get-Credential` to prompt the user to supply a password.

```yaml
Type: System.Management.Automation.PSCredential
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: NULL
Accept pipeline input: False
Accept wildcard characters: False
```

### -CriticalReplicationOnly

Indicates that the cmdlet performs only critical replication before reboot and then continues during
the AD DS installation operation. This parameter skips the noncritical and potentially lengthy
portion of replication. The noncritical replication happens after the installation finishes and the
computer reboots. By default, the cmdlet performs both critical and noncritical portions of the
replication.

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: NULL
Accept pipeline input: False
Accept wildcard characters: False
```

### -DatabasePath

Specifies the fully qualified, non-Universal Naming Convention (UNC) path to a directory on a fixed
disk of the local computer that will contain the domain database, for instance, `C:\Windows\NTDS`.
The default is `%SYSTEMROOT%\NTDS`.

```yaml
Type: System.String
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: NULL
Accept pipeline input: False
Accept wildcard characters: False
```

### -DelegatedAdministratorAccountName

Specifies the name of the user or group that is the delegated administrator of this domain
controller.

```yaml
Type: System.String
Parameter Sets: ADDSDomainControllerReadOnly
Aliases: 

Required: False
Position: Named
Default value: NULL
Accept pipeline input: False
Accept wildcard characters: False
```

### -DenyPasswordReplicationAccountName

Specifies the names of user accounts, group accounts, and computer accounts whose passwords are not
to be replicated to this RODC. Use an empty string (`""`) if you do not want to deny the replication
of credentials of any users or computers. By default, Administrators, Server Operators, Backup
Operators, Account Operators, and the Denied RODC Password Replication Group are denied. By default,
the Denied RODC Password Replication Group includes Cert Publishers, Domain Admins, Enterprise
Admins, Enterprise Domain Controllers, Enterprise Read-Only Domain Controllers, Group Policy Creator
Owners, the krbtgt account, and Schema Admins.

```yaml
Type: System.String[]
Parameter Sets: ADDSDomainControllerReadOnly
Aliases: 

Required: False
Position: Named
Default value: NULL
Accept pipeline input: False
Accept wildcard characters: False
```

### -DnsDelegationCredential

Specifies the user name and password for creating DNS delegation. This parameter is skipped if the
value for the **CreateDnsDelegation** parameter is either specified or computed to be `$false`.

```yaml
Type: System.Management.Automation.PSCredential
Parameter Sets: ADDSDomainController
Aliases: 

Required: False
Position: Named
Default value: NULL
Accept pipeline input: False
Accept wildcard characters: False
```

### -DomainName

Specifies the fully qualified domain name (FQDN) for the domain where the domain controller is
installed or added.

```yaml
Type: System.String
Parameter Sets: (All)
Aliases: 

Required: True
Position: Named
Default value: <mandatory>
Accept pipeline input: False
Accept wildcard characters: False
```

### -Force

Forces the command to run without asking for user confirmation.

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -InstallDns

Indicates the cmdlet installs and configures the DNS Server service on the domain controller. For
domain controller installation, if this parameter is left unspecified and the current domain
already hosts and stores the DNS names for the domain, then the default for this parameter is
`$true` and the DNS server is installed. Otherwise, if DNS domain names are hosted outside of
Active Directory, the default is `$false` and no DNS server is installed.

To test if DNS domain names are hosted outside of Active Directory, this cmdlet uses a start of
authority (SOA) type DNS query. For instance, if the value of **DomainName** is `corp.contoso.com`,
Active Directory performs an SOA query for `corp.contoso.com` and ensures that the zone name in the
response is `corp.contoso.com`.

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: ADDSDomainController, ADDSDomainControllerReadOnly
Aliases: 

Required: False
Position: Named
Default value: NULL
Accept pipeline input: False
Accept wildcard characters: False
```

### -InstallationMediaPath

Indicates the location of the installation media that is used to install a new domain controller.

```yaml
Type: System.String
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: NULL
Accept pipeline input: False
Accept wildcard characters: False
```

### -LogPath

Specifies the fully qualified, non-UNC path to a directory on a fixed disk of the local computer
that will contain the domain log files, for example, `C:\Windows\Logs`. The default is
`%SYSTEMROOT%\NTDS`.

```yaml
Type: System.String
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: NULL
Accept pipeline input: False
Accept wildcard characters: False
```

### -MoveInfrastructureOperationMasterRoleIfNecessary

Indicates that the cmdlet transfers the infrastructure master role to the domain controller being
installed. To successfully complete the transfer, the **NoGlobalCatalog** parameter must be
included as well. Do not specify this parameter if you want the infrastructure master role to
remain where it currently is.

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: ADDSDomainController, ADDSDomainControllerReadOnly
Aliases: 

Required: False
Position: Named
Default value: NULL
Accept pipeline input: False
Accept wildcard characters: False
```

### -NoDnsOnNetwork

Indicates that the DNS service is not available on the network. This parameter is used only when the
IP setting of the network adapter for this computer is not configured with the name of a DNS server
for name resolution. It indicates that a DNS server is installed on this computer for name
resolution. Otherwise, the IP settings of the network adapter must first be configured with the
address of a DNS server.

Omitting this parameter (the default) indicates that the TCP/IP client settings of the network
adapter on this server computer is used to contact a DNS server. Therefore, if you are not
specifying this parameter, ensure that TCP/IP client settings are first configured with a preferred
DNS server address.

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -NoGlobalCatalog

Indicates that the RODC will not be a global catalog server.
By default, the domain controller that you are installing is a global catalog server.

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: ADDSDomainController, ADDSDomainControllerReadOnly
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -NoRebootOnCompletion

Indicates that the cmdlet does not restart the computer upon the completion of the operation to
install the domain controller. By default, if this parameter is omitted the computer will restart
upon the completion of the install operation. As a general rule, Microsoft support recommends that
you not use this parameter except for testing or troubleshooting purposes because once configuration
has completed the server will not function correctly as either a member server or a DC until it is
rebooted.

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -ReadOnlyReplica

Indicates that the cmdlet installs the domain controller as an RODC for an existing domain.

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: ADDSDomainControllerReadOnly
Aliases: 

Required: False
Position: Named
Default value: FALSE
Accept pipeline input: False
Accept wildcard characters: False
```

### -ReplicationSourceDC

Specifies the name of the domain controller to be used as the source for replicating to this domain
controller.

```yaml
Type: System.String
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: NULL
Accept pipeline input: False
Accept wildcard characters: False
```

### -SafeModeAdministratorPassword

Supplies the password for the administrator account when the computer is started in Safe Mode or a
variant of Safe Mode, such as Directory Services Restore Mode. If no value is specified for this
parameter, the cmdlet prompts you to enter and confirm a masked password. If specified with a value,
the value must be a secure string.

Supplies the password for the administrator account when the computer is started in Safe Mode or a
variant of Safe Mode, such as Directory Services Restore Mode. You must supply a password that meets
the password complexity rules of the domain and the password cannot be blank. If specified with a
value, the value must be a secure string.

If this parameter is not specified, the cmdlet prompts you to enter and confirm a masked password.
This is the preferred usage when running the cmdlet interactively. If additionally there are no
other arguments specified with the cmdlet, you is prompted to enter a masked password for this
parameter but no confirmation of the password entered is made. This is not recommended as it could
allow a mistyped password to be configured. Another available advanced option is to use the
`ConvertTo-SecureString` cmdlet and specify the password string inline as unmasked console input,
which is also not a recommended security best practice in production deployments.

```yaml
Type: System.Security.SecureString
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: <mandatory>
Accept pipeline input: False
Accept wildcard characters: False
```

### -SiteName

Specifies the name of an existing site where you can place the new domain controller. The default
value depends on the type of installation. For a new forest, the default is
`Default-First-Site-Name`. For all other installations, the default is the site that is associated
with the subnet that includes the IP address of this server. If no such site exists, the default is
the site of the replication source domain controller.

```yaml
Type: System.String
Parameter Sets: ADDSDomainController
Aliases: 

Required: False
Position: Named
Default value: <mandatory>
Accept pipeline input: False
Accept wildcard characters: False
```

```yaml
Type: System.String
Parameter Sets: ADDSDomainControllerReadOnly
Aliases: 

Required: True
Position: Named
Default value: <mandatory>
Accept pipeline input: False
Accept wildcard characters: False
```

### -SkipAutoConfigureDns

Indicates that the cmdlet skips automatic configuration of the DNS client settings, forwarders, and
root hints. This parameter is in effect only if the DNS Server service is already installed.

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: NULL
Accept pipeline input: False
Accept wildcard characters: False
```

### -SkipPreChecks

Indicates that the cmdlet performs only a base set of validations. This behavior is equivalent to
the validations that were performed when using `Dcpromo.exe` in earlier versions of Windows Server
to add a new domain controller. When this switch parameter is set, it specifies that additional
preliminary checks should be bypassed. For more information on the scope of these additional
preliminary checks that the **ADDSDeployment** module performs by default when using Windows Server
2016, refer to the table in the section "ADPrep and Prerequisite Checking Architecture" in
[AD DS Simplified Administration](https://go.microsoft.com/fwlink/?LinkID=237244).

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -SystemKey

Specifies the system key for the media from which you replicate the data.
The default is none.

```yaml
Type: System.Security.SecureString
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: NULL
Accept pipeline input: False
Accept wildcard characters: False
```

### -SysvolPath

Specifies the fully qualified, non-UNC path to a directory on a fixed disk of the local computer
that will contain the Sysvol data, for example, `C:\Windows\SYSVOL`. The default is
`%SYSTEMROOT%\SYSVOL`.

```yaml
Type: System.String
Parameter Sets: (All)
Aliases: 

Required: False
Position: Named
Default value: NULL
Accept pipeline input: False
Accept wildcard characters: False
```

### -UseExistingAccount

Indicates that the cmdlet attaches a server to an existing RODC account.
If specified, a member of the Domain Admins group or a delegated user can run this cmdlet.

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: ADDSDomainControllerUseExistingAccount
Aliases: 

Required: False
Position: Named
Default value: FALSE
Accept pipeline input: False
Accept wildcard characters: False
```

### -WhatIf

Shows what would happen if the cmdlet runs.
The cmdlet is not run.

```yaml
Type: System.Management.Automation.SwitchParameter
Parameter Sets: (All)
Aliases: wi

Required: False
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters

This cmdlet supports the common parameters: `-Debug`, `-ErrorAction`, `-ErrorVariable`,
`-InformationAction`, `-InformationVariable`, `-OutVariable`, `-OutBuffer`, `-PipelineVariable`,
`-Verbose`, `-WarningAction`, and `-WarningVariable`. For more information, see
[about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

## OUTPUTS

### Microsoft.DirectoryServices.Deployment.Types.Result

## NOTES

- By default, this cmdlet always prompts for confirmation. To bypass confirmation, you need to
  include the **Confirm** parameter and specify a value of `$false`. For example,
  `-Confirm:$false`.
- By default, this cmdlet is always run when executed. To see what will happen if the cmdlet runs
  without executing or committing installation changes, first run the cmdlet using the **WhatIf**
  parameter to show what would happen.

## RELATED LINKS

[AD DS Simplified Administration](https://go.microsoft.com/fwlink/?LinkID=237244)

[Add-ADDSReadOnlyDomainControllerAccount](./Add-ADDSReadOnlyDomainControllerAccount.md)

[Install-ADDSDomain](./Install-ADDSDomain.md)

[Install-ADDSForest](./Install-ADDSForest.md)

[Get-Credential](https://go.microsoft.com/fwlink/?LinkID=293936)

[ConvertTo-SecureString](https://go.microsoft.com/fwlink/p/?LinkId=113291)
