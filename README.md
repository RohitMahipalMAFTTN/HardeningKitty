# Windows Hardening 

This is the Powershell Script for Hardening the Microsoft Windows Servers ( _HardeningKitty_ )

_HardeningKitty_ supports hardening of a Windows system. The configuration of the system is retrieved and assessed using a finding list. In addition, the system can be hardened according to predefined values. _HardeningKitty_ reads settings from the registry and uses other modules to read configurations outside the registry.


## How to run

Run the script with administrative privileges to access machine settings. For the user settings it is better to execute them with a normal user account. Ideally, the user account is used for daily work.

Download _HardeningKitty_ and copy it to the target system (script and policies). After that HardeningKitty can be imported and executed:

```powershell
PS C:\tmp> Import-Module .\Invoke-HardeningKitty.ps1
```

## Examples

### Audit

HardeningKitty performs an audit, saves the results in a CSV file and creates a log file. The files are automatically named and receive a timestamp. Using the parameters _ReportFile_ or _LogFile_, it is also possible to assign your own name and path. 

```powershell
Invoke-HardeningKitty -Mode Audit -Log -Report
```

HardeningKitty can be executed with a specific list defined by the parameter _FileFindingList_. If HardeningKitty is run several times on the same system, it may be useful to hide the machine information. The parameter _SkipMachineInformation_ is used for this purpose.

```powershell
Invoke-HardeningKitty -FileFindingList .\lists\finding_list_0x6d69636b_user.csv -SkipMachineInformation
```

HardeningKitty ready only the setting with the default list, and saves the results in a specific file

```powershell
Invoke-HardeningKitty -Mode Config -Report -ReportFile C:\tmp\my_hardeningkitty_report.log
```

### Backup

Backups are important. Really important. Therefore, HardeningKitty also has a function to retrieve the current configuration and save it in a form that can be easily restored. The _Backup_ switch specifies that the file is written in form of a finding list and can thus be used for the _HailMary_ mode. The name and path of the backup can be specified with the parameter _BackupFile_.

```powershell
Invoke-HardeningKitty -Mode Config -Backup
```

Please test this function to see if it really works properly on the target system before making any serious changes. A Schrödinger's backup is dangerous.

### HailMary

The _HailMary_ method is very powerful. It can be used to deploy a finding list on a system. All findings are set on this system as recommended in the list. With power comes responsibility. Please use this mode only if you know what you are doing. Be sure to have a backup of the system.

```powershell
Invoke-HardeningKitty -Mode HailMary -Log -Report -FileFindingList .\lists\finding_list_0x6d69636b_machine.csv
```

## HardeningKitty Score

Each Passed finding gives 4 points, a Low finding gives 2 points, a Medium finding gives 1 point and a High Finding gives 0 points.

The formula for the HardeningKitty Score is _(Points achieved / Maximum points) * 5 + 1_.

### Rating

| Score | Rating Casual | Rating Professional |
| :---- | :------------ | :------------------ |
| 6 | 😹 Excellent | Excellent |
| 5 | 😺 Well done | Good |
| 4 | 😼 Sufficient | Sufficient |
| 3 | 😿 You should do better | Insufficient |
| 2 | 🙀 Weak | Insufficient |
| 1 | 😾 Bogus | Insufficient |

## HardeningKitty Interface

[ataumo](https://github.com/ataumo) build a web based interface for HardeningKitty. The tool can be used to create your own lists and provides additional information on the hardening settings. The [source code](https://github.com/ataumo/policies_hardening_interface) is under AGPL license and there is a [demo site](https://phi.cryptonit.fr/policies_hardening_interface/).

## Last Update

HardeningKitty can be used to audit systems against the following baselines / benchmarks:

| Name | System Version    | Version  |
| :--- | :---------------- | :------  |
| 0x6d69636b (Machine) | 20H2, 21H1 | |
| 0x6d69636b (User) | 20H2, 21H1 | |
| BSI SiSyPHuS Windows 10 hoher Schutzbedarf Domänenmitglied (Machine) | 1809 | 1.0 |
| BSI SiSyPHuS Windows 10 hoher Schutzbedarf Domänenmitglied (User) | 1809| 1.0
| BSI SiSyPHuS Windows 10 normaler Schutzbedarf Domänenmitglied (Machine) | 1809| 1.0 |
| BSI SiSyPHuS Windows 10 normaler Schutzbedarf Domänenmitglied (User) | 1809| 1.0 |
| BSI SiSyPHuS Windows 10 normaler Schutzbedarf Einzelrechner (Machine) | 1809| 1.0 |
| BSI SiSyPHuS Windows 10 normaler Schutzbedarf Einzelrechner (User) | 1809 | 1.0 |
| CIS Microsoft Windows 10 Enterprise (Machine) | 1809 | 1.6.1 |
| CIS Microsoft Windows 10 Enterprise (User) | 1809 | 1.6.1 |
| CIS Microsoft Windows 10 Enterprise (Machine) | 1903 | 1.7.1 |
| CIS Microsoft Windows 10 Enterprise (User) | 1903 | 1.7.1 |
| CIS Microsoft Windows 10 Enterprise (Machine) | 1909 | 1.8.1 |
| CIS Microsoft Windows 10 Enterprise (User) | 1909 | 1.8.1 |
| CIS Microsoft Windows 10 Enterprise (Machine) | 2004 | 1.9.1 |
| CIS Microsoft Windows 10 Enterprise (User) | 2004 | 1.9.1 |
| CIS Microsoft Windows 10 Enterprise (Machine) | 20H2 | 1.10.1 |
| CIS Microsoft Windows 10 Enterprise (User) | 20H2 | 1.10.1 |
| CIS Microsoft Windows Server 2012 R2 (Machine) | R2 | 2.4.0 |
| CIS Microsoft Windows Server 2012 R2 (User) | R2 | 2.4.0 |
| CIS Microsoft Windows Server 2016 (Machine) | 1607 | 1.2.0 |
| CIS Microsoft Windows Server 2016 (User) | 1607 | 1.2.0 |
| CIS Microsoft Windows Server 2019 (Machine) | 1809 | 1.1.0 |
| CIS Microsoft Windows Server 2019 (User) | 1809 | 1.1.0 |
| CIS Microsoft Windows Server 2019 (Machine) | 1809 | 1.2.0 |
| CIS Microsoft Windows Server 2019 (User) | 1809 | 1.2.0 |
| DoD Microsoft Windows 10 STIG (Machine) | 20H2 | v2r1 |
| DoD Microsoft Windows 10 STIG (User) | 20H2 | v2r1 |
| DoD Windows Server 2019 Domain Controller STIG (Machine) | 20H2 | v2r1 |
| DoD Windows Server 2019 Domain Controller STIG (User) | 20H2 | v2r1 |
| DoD Windows Server 2019 Member Server STIG (Machine) | 20H2 | v2r1 |
| DoD Windows Server 2019 Member Server STIG (User) | 20H2 | v2r1 |
| DoD Windows Defender Antivirus STIG | 20H2 | v2r1 |
| DoD Windows Firewall STIG | 20H2 | v1r7 |
| Microsoft Security baseline for Microsoft Edge | 87 | Final |
| Microsoft Security baseline for Microsoft Edge | 88, 89, 90, 91 | Final |
| Microsoft Security baseline for Microsoft Edge | 92 | Final |
| Microsoft Security baseline for Microsoft Edge | 93, 94 | Final |
| Microsoft Security baseline for Microsoft Edge | 95 | Final |
| Microsoft Security baseline for Microsoft Edge | 96 | Final |
| Microsoft Security baseline for Windows 10 | 2004 | Final |
| Microsoft Security baseline for Windows 10 | 20H2, 21H1 | Final |
| Microsoft Security baseline for Windows 10 | 21H2 | Final |
| Microsoft Security baseline for Windows 11 | 21H2 | Final |
| Microsoft Security baseline for Windows Server (DC) | 2004 | Final |
| Microsoft Security baseline for Windows Server (Member) | 2004 | Final |
| Microsoft Security baseline for Windows Server (DC) | 20H2 | Final |
| Microsoft Security baseline for Windows Server (Member) | 20H2 | Final |
| Microsoft Security baseline for Windows Server 2022 (DC) | 21H2 | Final |
| Microsoft Security baseline for Windows Server 2022 (Member) | 21H2 | Final |
| Microsoft Security baseline for Office 365 ProPlus (Machine) | Sept 2019 | Final |
| Microsoft Security baseline for Office 365 ProPlus (User) | Sept 2019 | Final |
| Microsoft Security Baseline for Microsoft 365 Apps for enterprise (Machine) | v2104, v2106 | Final |
| Microsoft Security Baseline for Microsoft 365 Apps for enterprise (User) | v2104, v2106 | Final |
| Microsoft Security Baseline for Microsoft 365 Apps for enterprise (Machine) | v2112 | Final |
| Microsoft Security Baseline for Microsoft 365 Apps for enterprise (User) | v2112 | Final |
| Microsoft Windows Server TLS Settings | 1809 | 1.0 |
| Microsoft Windows Server TLS Settings (Future Use with TLSv1.3) | 1903 | 1.0 |
