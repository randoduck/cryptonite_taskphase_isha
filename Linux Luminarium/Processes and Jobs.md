# Processes and Jobs 
## Challenge 1: Listing Challenges (Summary/Learning):
Here we have been introduced to the **ps** (Process Status) , which is used to list out the processes on your terminal. Two arguments have been talked about here **-ef** and **-aux**. where -e to list "every" process and -f for a "full format" output, including arguments. x to list processes that aren't running in a terminal, and u for a "user-readable" output. -ef is classified as the standard syntax while -aux is classified as the BSD Syntax.
### Solution
To Obtain the flag the following commands were used :
```bash
hacker@processes~listing-processes:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ ps -ef
hacker@processes~listing-processes:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ /challenge/14390-run-3558
```

## Challenge 2: Killing Challenges (Summary/Learning):
We have been introduced to a new command **kill**which  will terminate a process in a way that gives it a chance to get its affairs in order before ceasing to exist. We can kill a process by passing the process identifier (the PID from ps) as an argument
### Solution
To Obtain the flag the following commands were used :
```bash
hacker@processes~killing-processes:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ ps -ef | grep dont_run
hacker@processes~killing-processes:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ kill 203
hacker@processes~killing-processes:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ /challenge/run
```

## Challenge 3: Interrupting Processes (Summary/Learning):
We have been taught the concept of interuption . Its shortcut key being  Ctrl-C which sends an "interrupt" to whatever application is waiting on input from the terminal and, typically, this causes the application to cleanly exit.
### Solution
To Obtain the flag the following commands were used :
```bash
hacker@processes~interrupting-processes:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ /challebge/run
bash: /challebge/run: No such file or directory
hacker@processes~interrupting-processes:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ /challenge/run
ker@processes~interrupting-processes:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ 

```

## Challenge 4: Suspending Processes (Summary/Learning):
Another hotkey has been introduced here for the process of suspension .
One can suspend and ongoing processs to the background with Ctrl-Z
### Solution
To Obtain the flag the following commands were used :
```bash
hacker@processes~suspending-processes:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ /challenge/run
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~suspending-processes:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ /challenge/run
```

## Challenge 5: Resuming Processes (Summary/Learning):
One can resume a suspended process by executing the  fg command in your sheel which is a builtin that takes the suspended process, resumes it, and puts it back in the foreground of your terminal.
### Solution
To Obtain the flag the following commands were used :
```bash
hacker@processes~resuming-processes:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ /challenge/run
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~resuming-processes:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ fg /challenge/run

```

## Challenge 6: Background Processes (Summary/Learning):
Similar to resuming a suspended process in the previous case we can also put it in the background using the **bg** command . We can check if its suspended by using the **-o** option.
### Solution
To Obtain the flag the following commands were used :
```bash
hacker@processes~backgrounding-processes:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ /challenge/run
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~backgrounding-processes:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ bg /challenge/run
[1]+ /challenge/run &
hacker@processes~backgrounding-processes:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ /challenge/run
```

## Challenge 7: Foregrounding Processes (Summary/Learning):
This challenge deals with foregrounding an already backgrounded process 
### Solution
To Obtain the flag the following commands were used :
```bash
hacker@processes~foregrounding-processes:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ /challenge/run
^Z
[1]+  Stopped                 /challenge/run
hacker@processes~foregrounding-processes:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ bg /challenge/run
[1]+ /challenge/run &
hacker@processes~foregrounding-processes:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ fg /challenge/run

```
## Challenge 8: Starting Backgrounded Processes (Summary/Learning):
We can start a process and background it immediately without ever suspending it . This can be achieved by appending the **&** to the process as an argument.
### Solution
To Obtain the flag the following commands were used :
```bash
hacker@processes~starting-backgrounded-processes:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ /challenge/run &
[1] 760

```
## Challenge 9: Process Exit Codes (Summary/Learning):
We have been introduced to the concept of exit code. Every program and every builtin, exits with an exit code when it finishes running and terminates, This can be used by the shell, or the user of the shell (that's you!) to check if the process succeeded in its functionality (this determination, of course, depends on what the process is supposed to do in the first place). We can find the exit code to a process by using **$?** symbol as an argument.
### Solution
To Obtain the flag the following commands were used :
```bash
hacker@processes~process-exit-codes:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ /challenge/get-code
Exiting with an error code!
hacker@processes~process-exit-codes:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ $?
bash: 138: command not found
hacker@processes~process-exit-codes:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ /challenge/submit-code 138
```
## <3
