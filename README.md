# Advent of Code - REXX Programmers IDE (WIP)

### What does it do?
This is an ISPF appliaction that will make solving Advent of Code challenges in REXX a bit easier.
The appliaction will keep track of how many times you've tried to solve a particular puzzle and will show you when you started and when you finished :)

### Requirements
Because this ISPF application will download your puzzle-input via CURL you need this executable on your z/OS environment.
Also, because of the same reason, your z/OS should be capable of reaching the https://adventofcode.com servers.

### How to install?
Easiest way is to clone this repository with zigi. Otherwise you can download the XMI file from the 'binaries' that come with a future release of ZAOC.

#### Create config file
The CONFIG.EXAMPLE file that comes with this repository looks like below. Copy that to a .CONFIG datasets (a.k.a. remove the LLQ) and make the appropiate changes.

    CURL_PATH = /path/to/curl                                        
    SESSION = you_session_key_for_auto_download_your_puzzle_input    
    INPUTFILES = /path/to/where/to/store/puzzle/input                

#### How to get your session key?
Login to your https://adventofcode.com account, press the F12 button and click the "Application" tab.
In the "Storage" tree you will find the "Cookies", from there copy the value for the 'session' cookie.

### Running the application
Just 3.4 towards the '*.ADVENT.EXEC' PDS and execute the 'ZAOC' rexx. 
From that ISPF application you can type 'add' on the command line to add puzzle input for that year/day (will be stored at `INPUTFILES` location from your CONFIG file) 
and it will store a 'bootstrapped' REXX in `*.ADVENT.SOLVE.REXX` that will read that puzzle input and print all the lines from it. This skeleton REXX looks like this:

    /*--------------------------------------------[REXX]           
    | Made with ZAOC by wizard@zdevops.com             |             
    +-------------------------------------------------*/           
    say "Advent of Code xxxx day x"                                
    x = bpxwunix('cat /path/to/where/to/store/puzzle/input/yxxxx/dx',,file.,se.)
    do i = 1 to file.0                                             
      say file.i                                                   
    end                 

From there you can start writing your own solution. 

You do this with the 'E' line command in the application which will open the editor. Once you think your solution is good,
you can use the 'R' line command to run the REXX. (this will increment the 'tries' counter)

Once you've got the solution, use the 'S' line command to mark the challenge as solved.

### Demo?


https://github.com/user-attachments/assets/710a4695-f0a0-45ae-83b3-810fa3e1126a

