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



