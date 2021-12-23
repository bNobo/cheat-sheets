# Windows cheat sheet

## Enable full dump collection on app crash

Add a registry key containing 

```reg
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps]
"DumpType"=dword:00000002
```

Apps executed by the current user dumps go to `%LOCALAPPDATA%\CrashDumps`. Windows services dumps go to `C:\Windows\System32\config\systemprofile\AppData\Local\CrashDumps\`

To change dump folder add a `DumpFolder` string value and set it to `C:\ProgramData`

Source : https://support.microfocus.com/kb/doc.php?id=7013369#
