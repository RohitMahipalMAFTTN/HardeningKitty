# Windows Hardening 

This is the Powershell Script for Hardening the Microsoft Windows Servers ( _HardeningKitty_ )

_HardeningKitty_ supports hardening of a Windows system. The configuration of the system is retrieved and assessed using a finding list. In addition, the system can be hardened according to predefined values. _HardeningKitty_ reads settings from the registry and uses other modules to read configurations outside the registry.


## How to run

Run the script with administrative privileges to access machine settings. For the user settings it is better to execute them with a normal user account. Ideally, the user account is used for daily work.

### Steps

| Steps | Command | Descriptions |
| :---- | :------------ | :------------------ |
| 1 | git clone git@github.com:scipag/HardeningKitty.git | Clone the Hardening Kitty Repo using this repo as source code. |
|  | Import-Module .\Invoke-HardeningKitty.ps1 | Initalizing the Powershell Script as Administator Access |
|  | Invoke-HardeningKitty -Mode Audit -Log -Report -ReportFile .\report\start_report.csv -FileFindingList .'\polices\final windows-hardening.csv' | Checking the Policies to be change before the Policies are applied as per your policies csv file. |
|  | Invoke-HardeningKitty -Mode HailMary -Log -Report -ReportFile .\report\result.csv -FileFindingList .'\polices\final windows-hardening.csv' | Applying the policies to the target server |
|  | Invoke-HardeningKitty -Mode Audit -Log -Report -ReportFile .\report\end_report.csv -FileFindingList .'\polices\final windows-hardening.csv' | Checking the Policies to be change after the Policies are applied as per your policies csv file. |

## Examples

### Audit

HardeningKitty performs an audit, saves the results in a CSV file and creates a log file. The files are automatically named and receive a timestamp. Using the parameters _ReportFile_ or _LogFile_, it is also possible to assign your own name and path. 

```powershell
Invoke-HardeningKitty -Mode Audit -Log -Report
```

HardeningKitty can be executed with a specific list defined by the parameter _FileFindingList_. If HardeningKitty is run several times on the same system, it may be useful to hide the machine information. The parameter _SkipMachineInformation_ is used for this purpose.

```powershell
Invoke-HardeningKitty -FileFindingList .'\polices\final windows-hardening.csv' -SkipMachineInformation
```

HardeningKitty ready only the setting with the default list, and saves the results in a specific file

```powershell
Invoke-HardeningKitty -Mode Config -Report -ReportFile .\report\start_report.csv
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
Invoke-HardeningKitty -Mode HailMary -Log -Report -FileFindingList .'\polices\final windows-hardening.csv'
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
