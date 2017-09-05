---
title: WorkLog PowerShell Module
slug: worklog-powershell-module
date: 2015-02-06
author: "Kevin Kirkpatrick"
draft: false
tags:
  - powershell
---

As part of a new initiative, of sorts, I wanted a way to record daily accomplishments, which is something that I have thought about doing for quite some time, but never got enough motivation to actually do anything about it. That said, I decided to revisit, take action and come up with some requirements on what a workable solution would look like (for me):

  * It needs to be easy to record entries (if it's hard or cumbersome, it won't have sustainability)
  * It needs to fit into my daily workflow
  * The format needs to be somewhat open/easy to move between different platforms (Mainly Windows & Mac OS)
  * If possible, pick a solution that can sharpen a skill-set, in the process

Given each of those, my final solution ended up being quite simple: GitHub and GitHub Flavored Markdown (GFM) files. This was ideal, because it really meets all of the requirements, above.

  * It needs to be easy to record entries
   * _Use Sublime Text to create/edit GFM files for each day._
  * It needs to fit into my daily workflow
   * _I already use GitHub on a daily basis for source control of various scripts, projects, modules, etc._
  * The format needs to be somewhat open/easy to move between different platforms
   * _Again, I already use GitHub as a central source control for all of my code repositories and have that synced between my Windows and Mac systems_
  * If possible, pick a solution that can sharpen a skill-set, in the process
   * _While familiar with GitHub and GFM files, I can always use some extra practice_

Now, after I started building out how I wanted things setup and started creating entries into a log file, I realized that flipping over to a text editor to make entries was working fine, but I wanted deeper integration; why not use PowerShell!

What resulted was a PowerShell module comprised of 3 functions:

* New-WorkLog
* Add-WorkLog
* Get-WorkLog

The main functionality I needed out of this module was:

  * Create a new Work Log file for each day
  * Standard file name format
  * Generate pre-formatted file layout (Title, fully formatted date and an initial bullet point)
  * Ability to add entries right from the PowerShell console
  * Ability to view the contents of the Work Log for the current day, from within the console
  * Basic support for bullet point indentation
  * Basic fail-safes so that files wouldn't get overwritten.

Before I continue, you can get more information as well as download, clone or fork the Module from <a href="https://github.com/vScripter/WorkLogModule" target="_blank">GitHub</a>

Lets take a closer look at each function.

* * *

## New-Worklog

### Function header

<script src="https://gist.github.com/vScripter/b3038ff5dca92467cb43c6e79c0e9f98.js"></script>

Pretty standard material getting things started. The main item worth noting is that I hard coded the working directory and assigned it to the -Path parameter.

### BEGIN Block

<script src="https://gist.github.com/vScripter/235539b140c5b75432689f009897eb67.js"></script>

I need to get some date details and convert them to strings so that I can create a custom, standard file name as well as the date detail that will get stored in the actual file.

  * __`$now`__ - Get and assign the current date information in the $now variable, so that we can use to construct our custom file format.
  * __`$dateFormat`__ - Call the .tostring() method on the $now variable and format the output so it will look like '20150205'
  * __`$dateDay`__ - Call the .tostring() method but specify 'dddd' in order to get the day of the week in long format, like 'Thursday'
  * __`$fileName`__ - Build out the actual file name string. I'm adding the value stored in $dateFormat; then add an underscore `_`; then add the value stored in $dateDay; then another underscore `_`; finally, add the last piece 'WL.md' ('WL' just stands for Work Log)
  * __`$filePath`__ - Join the value stored in `$Path` with the value stored in `$fileName`, and the end result is the full path of the daily Work log file, which looks something like: __`C:\Users\%USERNAME%\Documents\GitHub\WorkLog\20150205_Thursday_WL.md`__



### PROCESS Block

<script src="https://gist.github.com/vScripter/875d57a8b453e2a1661f83f7f9c2be46.js"></script>

*  First, we create a logical statement that tests for the existence of the log file and if it does not exist, we want to create it, but if it does exist, we want to display a message to the console saying that it already exists. Since I only want to take action if it DOES NOT exist, I start by using that criteria as the first validation via '-not' operator. `if (-not (Test-Path -LiteralPath $filePath -PathType Leaf)`

* I then create the desired file and use Write-Output to add the desired detail to the file. As a general comment, the spacing of the text does matter, to a certain degree, when creating these markdown files, since spaces and special characters actually mean something when the markdown files are read/displayed.
* If the file does exist, use Write-Warning to display some text in the console letting me know that one is already created. I used Write-Warning here because I wanted to avoid clouding up the 'Output/Success' data stream ([great article](http://blogs.technet.com/b/heyscriptingguy/archive/2014/03/30/understanding-streams-redirection-and-write-host-in-powershell.aspx) by June Blender on PowerShell streams). As a best practice, I ALWAYS try to avoid sending informational messages that are only useful to the user running the cmdlet/script/function, from going down the pipeline; Output from the 'Write-Output' cmdlet uses the 'Output/Success' stream (stream 1). Write-Host is forbidden and kills kittens, so it should never be used 🙂 (It also sends nothing to any stream, which can very problematic).
* We don't do anything in the END {} block so we can move on to the next function

* * *


## Add-Workload

### Function Header

<script src="https://gist.github.com/vScripter/b6916f6c39f89e913417c628983fe5b3.js"></script>

* I needed some parameters to deal with the actual message/update to be entered into the Work Log, as well as an -Indent parameter to specify the level of indentation
    * `-Message` - This is the string data that will actually be appended into the Work Log file. I set the position at '0' so that I can quickly add entries without having to specify '-Message' before typing the message.
    * `-Indent` - This is the level of desired indentation and is only required if you want to indent the entry. I only want to offer 4 levels of indentation, so I specify a [ValidateSet()] attribute to the parameter with the only values I want to accept (1,2,3,4). These values get passed to a function that actually reads the value and performs the proper indentation spacing when it appends the entry to the Work Log file. More on that in the PROCESS block

### BEGIN Block

<script src="https://gist.github.com/vScripter/a2deac64abf66ad6758426f24b59efec.js"></script>

* I won't go over the date variables since we reviewed that in the 'New-WorkLog' function
* I created the 'Add-Indent' function to handle the indentation spacing that results in a properly formatted, indented, markdown file.
    * I accept the -Indent parameter, if it was supplied, in the -Level parameter of this function
    * I use a basic 'switch' statement to define the spacing that gets outputted when the function is called. More on this functionality in the PROCESS block

### PROCESS Block

<script src="https://gist.github.com/vScripter/376fcc4c5c6027f9d3d6903c2e4136da.js"></script>

* I start with a conditional statement to check and see if the WorkLog file exists and if it does, then check to see if there was a desired indent level.
* `$indentMessage` - Stores the properly indented message that will be written to the Work Log file. It merges the desired indent with the provided -Message string
* If no indent is desired, it simply appends the message to the current Work Log file
* If the Work Log file DOES NOT exist, we want to go ahead and create it. The main differences the way the file gets created with 'Add-WorkLog' vs. 'New-WorkLog' are:
    * There is no asterisk (bullet point) created as part of the initial file create; if the file doesn't exist, we want our first entry to be the first bullet point.
    * Along the same lines, if we supplied an indent level and the file doesn't exist, we don't want to to indent the first entry, so, I just ignore indents if the file has to be created using this function
* There is nothing in the END {} block so we will move on to the next function

* * *

## Get-Worklog

### Function Header

<script src="https://gist.github.com/vScripter/1d5d89607a403930085eaae1e4a718e4.js"></script>

This isn't any different than the start of the New-WorkLog function, so you can reference that if you have any questions


### BEGIN Block
This is also no different than the New-WorkLog function; you can reference more detail above

### PROCESS Block

<script src="https://gist.github.com/vScripter/94bf70bd9caad40d85109db32b9ef0da.js"></script>

* This is the most straight forward function, of all the rest. We are just using the Get-Content cmdlet to read in and display the contents of the current work log file.
* I use the '-ReadCount 0' parameter so that is reads the entire file contents in at one time, instead of line-by-line.
* If the Work Log file has not been created, display a message to the console
* There is no END {} block


* * *

## Output

Below are some example commands and the file/file format that they produce

<script src="https://gist.github.com/vScripter/278883d3ca1f5e0d6d98cc8d595c1ebd.js"></script>

#### Output file name

```
20150206_Friday_WL.md
```

#### Output file content

<script src="https://gist.github.com/vScripter/084f7fac5a029973af29d28467679362.js"></script>

#### End result

<script src="https://gist.github.com/vScripter/2423657ccb434eaab7328aa1f567a7a9.js"></script>