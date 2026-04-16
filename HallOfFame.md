---
title: Hall Of Fame 
layout: page
---
# Hall of Fame

## PicoCTF 2024 **SansAlpha**
The following is a solution to a problem created for the 2024 picoCTF competition by syreal called SansAlpha.
Players are provided with ssh details to an instance of a server running in a different universe which only has numbers and symbols, no alphabetical characters. When trying to run any command containig a letter, the server returns `Unknown character detected`.

This means we need to find an unorthodox way to run our cat command to poke around the file system and print the contents of any files without inluding any letters in the commands we send to the server.


Running cat with no letters 

```bash
"$(- 2>&1)";${_:9:1}${_:13:1}${_:19:1} ~/*/*
```

`"$(- 2>&1)"` tries to run the command `-` which gives an error `command not found`

The `2>&1` pipes stderr into stdout so it tries to run `bash: -: command not found`

`${_:9:1}` gives the 9th character in the last command run which is c, `${_:13:1}` gives the 13th which is a and `${_:19:1}` gives the 19th which is t

And that spells cat

So `$(- 2>&1)";${_:9:1}${_:13:1}${_:19:1}` runs the command cat and `~/*/*` points to every file in directories in the home directory, giving us the flag in amongst 
