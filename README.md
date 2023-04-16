# Win10PrivacyTool
Batch file that disables some of the Windows 10 features that could potentially be used for surveillance.

This batch file does the following:<br>
- Disable Windows telemetry and data collection
- Disable Remote Desktop and Remote Assistance
- Disable Cortana and Voice Recording
- Disable Windows Event Logs
- Disable Windows updates
- Disable OneDrive synchronization
- Disable SmartScreen
- Disable Error Reporting and Feedback
- Disable Location Services
- Disable Camera and Microphone Access
- Disable Windows Hello
- Disable Wi-Fi Sense
- Disable Remote Registry
- Disable Windows Firewall
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

:: Disable OneDrive synchronization
reg add "HKLM\Software\Policies\Microsoft\Windows\OneDrive" /v DisableFileSyncNGSC /t REG_DWORD /d 1 /f
reg add "HKLM\Software\Policies\Microsoft\Windows\OneDrive" /v DisableFileSync /t REG_DWORD /d 1 /f

:: Disable SmartScreen
reg add "HKLM\SOFTWARE\Policies\Microsoft\Windows\System" /v EnableSmartScreen /t REG_DWORD /d 0 /f

:: Disable Error Reporting and Feedback
reg add "HKCU\Software\Microsoft\Siuf\Rules" /v "NumberOfSIUFInPeriod" /t REG_DWORD /d 0 /f
reg add "HKLM\SOFTWARE\Policies\Microsoft\Windows\DataCollection" /v ConsentStatus /t REG_DWORD /d 0 /f
reg add "HKLM\SOFTWARE\Policies\Microsoft\Windows\ErrorReporting" /v Disabled /t REG_DWORD /d 1 /f

:: Disable Location Services
reg add "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\CapabilityAccessManager\ConsentStore\location" /v Value /t REG_DWORD /d 0 /f
reg add "HKLM\SOFTWARE\Policies\Microsoft\Windows\LocationAndSensors" /v DisableLocation /t REG_DWORD /d 1 /f

:: Disable Camera and Microphone Access
reg add "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\CapabilityAccessManager\ConsentStore\webcam" /v Value /t REG_DWORD /d 0 /f
reg add "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\CapabilityAccessManager\ConsentStore\microphone" /v Value /t REG_DWORD /d 0 /f

:: Disable Windows Hello
reg add "HKLM\SOFTWARE\Policies\Microsoft\Biometrics\FacialFeatures" /v "AllowFaceUnlock" /t REG_DWORD /d 0 /f
reg add "HKLM\SOFTWARE\Policies\Microsoft\Windows\System" /v "AllowDomainPINLogon" /t REG_DWORD /d 0 /f

:: Disable Wi-Fi Sense
reg add "HKLM\SOFTWARE\Microsoft\PolicyManager\default\WiFi\AllowWiFiHotSpotReporting" /v "Value" /t REG_DWORD /d 0 /f
reg add "HKLM\SOFTWARE\Microsoft\PolicyManager\default\WiFi\AllowAutoConnectToWiFiSenseHotspots" /v "Value" /t REG_DWORD /d 0 /f

:: Disable Remote Registry
sc config RemoteRegistry start= disabled

:: Disable Windows Firewall
netsh advfirewall set allprofiles state off

pause
```
Disabling Windows telemetry and data collection ensures that user data is not being sent back to Microsoft, Remote Desktop and Remote Assistance can potentially allow others to access and control your computer, Cortana and Voice Recording can record personal conversations, Windows Event Logs can contain sensitive information, Windows updates can potentially introduce security vulnerabilities or other issues, OneDrive synchronization can allow others to access your files, SmartScreen can send information about your files to Microsoft, Error Reporting and Feedback can contain personal information, Location Services, Camera and Microphone Access, Windows Hello, Wi-Fi Sense, Remote Registry, and Windows Firewall can all potentially allow others to access or use your computer in ways that you do not want them to.
