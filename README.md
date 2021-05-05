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
