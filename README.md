# Win10PrivacyTool
Batch file that disables some of the Windows 10 features that could potentially be used for surveillance.


```Batch
@echo off

:: Disable Windows telemetry and data collection
reg add "HKLM\SOFTWARE\Policies\Microsoft\Windows\DataCollection" /v AllowTelemetry /t REG_DWORD /d 0 /f
reg add "HKLM\SOFTWARE\Policies\Microsoft\Windows\AppCompat" /v AITEnable /t REG_DWORD /d 0 /f
reg add "HKLM\SOFTWARE\Policies\Microsoft\Windows\AppCompat" /v DisableInventory /t REG_DWORD /d 1 /f

:: Disable Remote Desktop and Remote Assistance
reg add "HKLM\System\CurrentControlSet\Control\Terminal Server" /v fDenyTSConnections /t REG_DWORD /d 1 /f
reg add "HKLM\System\CurrentControlSet\Control\Remote Assistance" /v fAllowToGetHelp /t REG_DWORD /d 0 /f

:: Disable Cortana and Voice Recording
reg add "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Search" /v BingSearchEnabled /t REG_DWORD /d 0 /f
reg add "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Search" /v CortanaConsent /t REG_DWORD /d 0 /f
reg add "HKCU\SOFTWARE\Microsoft\Speech_OneCore\Privacy" /v AllowSpeechInput /t REG_DWORD /d 0 /f

:: Disable Windows Event Logs
wevtutil cl System
wevtutil cl Security
wevtutil cl Application

:: Disable Windows updates
reg add "HKLM\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU" /v NoAutoUpdate /t REG_DWORD /d 1 /f
reg add "HKLM\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU" /v AUOptions /t REG_DWORD /d 1 /f
reg add "HKLM\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU" /v ScheduledInstallDay /t REG_DWORD /d 0 /f
reg add "HKLM\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU" /v ScheduledInstallTime /t REG_DWORD /d 3 /f

echo Windows surveillance features have been disabled.

pause

```
This batch file does the following:
Disables Windows telemetry and data collection
Disables Remote Desktop and Remote Assistance
Disables Cortana and Voice Recording
Clears Windows Event Logs
Disables Windows updates
