# WinDBG-Hacks

## Symbols

For "Couldn't resolve error at " issues, try:  
```
0: kd> .symfix C:\debug\symbols
0: kd> !sym noisy
noisy mode - symbol prompts on
0: kd> .reload /f  

OR

0: kd> .sympath c:\path\to\your\pdb
0: kd> .symfix+ c:\symbols
0: kd> .reload /f
0: kd> ld xyz
```  


## Processes
### How to list processes  
```
0: kd> dx -r1 Debugger.Sessions[0].Processes.Contains("chrome.exe")
Error: Cannot compare non-intrinsic values to each other.  


0: kd> .tlist

0: kd> !dml_proc 
```

### How to search for process by name
```
dx @$cursession.Processes.Where(p => p.Environment.EnvironmentBlock.ProcessParameters->CommandLine->ToDisplayString().Contains("chrome"))
```  

### How to switch context to a process:   
```
// <PID> should replace with the process PID
0: kd> dx -s Debugger.Sessions[0].Processes[<PID>].SwitchTo()   

// OR like that, but notice that it search for processes by name and there might be number with the same name. 
0: kd> dx -s @$cursession.Processes.Where(p => p.Environment.EnvironmentBlock.ProcessParameters->CommandLine->ToDisplayString().Contains("chrome"))[<PID>].SwitchTo()


0: kd> !process 0 0 WindowsProject1.exe
// To his PEB ?
0: kd> .process /i 000000dd35f3e000d


0: kd> !process 0 0 WindowsProject1.exe
PROCESS ffffcf07bad91080
    SessionId: 1  Cid: 22c8    Peb: dd35f3e000  ParentCid: 1598
    DirBase: 1b9b83000  ObjectTable: ffffe5829cb59b00  HandleCount: 145.
    Image: WindowsProject1.exe  
0: kd> .process ffffcf07bad91080
Implicit process is now ffffcf07`bad91080
WARNING: .cache forcedecodeuser is not enabled
0: kd> bu /p ffffcf07bad91080 user32!SetWindowTextA 

```

### Find your current context:   
```
dx @$curprocess.Name
```
