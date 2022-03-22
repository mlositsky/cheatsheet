# Conda issues

Usually these issues happen after running `conda init` command

## Issue

cmd.exe returns `& was unexpected at this time` and exits.

## Fix

Check registry pathes:

```
HKEY_LOCAL_MACHINE\Software\Microsoft\Command Processor
HKEY_CURRENT_USER\Software\Microsoft\Command Processor
```

for Autorun entries

## Issue

powershell.exe starts with error `...Documents\WindowsPowerShell\profile.ps1 cannot be loaded because running scripts is disabled on
this system.`

## Fix

in powershell enter:

```Set-ExecutionPolicy RemoteSigned -Scope CurrentUser```
