# lotl-mshta
Demonstrates mshta.exe → inline JS → PowerShell (-EncodedCommand) with a staged download from a remote URL and in-memory binary execution, including complex DLL functionality. 
Read this article for instructions on how to run and understand this project: https://hackersterminal.com/how-mshta-spawns-powershell-and-executes-script-exe-dll-in-memory-from-remote-url/

Overview

This repository demonstrates a fileless, living-off-the-land (LotL) execution flow used in a controlled lab environment. The example shows how a small bootstrap launches an interpreter (mshta → JavaScript → PowerShell), fetches a staged task list at runtime, and executes actions — including in-memory execution of payloads — without writing those payloads to disk.

Execution Flow
Bootstrap

launch_script.ps1 starts mshta.exe with inline JavaScript.

The JavaScript spawns PowerShell using a base64-encoded command.

Child PowerShell Execution

child.ps1 is fetched at runtime from a remote URL.

It parses task.json (the staged task list) and drives task processing.

Task Processing

The child script iterates the tasks in task.json and performs actions according to the task type.

In-Memory Payload Execution

HelloWorld.exe and SimpleDll.dll are demonstrated as payloads executed directly in memory.

This demonstrates fileless execution patterns where payloads are never written to disk.



Detection Opportunities:

Monitor mshta.exe spawning powershell.exe with -EncodedCommand
Detect unusual parent-child process relationships
Watch for PowerShell downloading scripts from remote URLs
Look for in-memory .NET assembly loads ([Reflection.Assembly]::Load)

⚠️ Disclaimer

This repository is provided strictly for educational and defensive security research purposes only.
Do not use this project for unauthorized access or malicious activity. The author assumes no liability for misuse.
