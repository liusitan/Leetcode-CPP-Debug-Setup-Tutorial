# Leetcode CPP Debug Setup Tutorial

This tutorial helps the leetcoder who is not familiar with c++ quickly setup their debugging environment with ease. There are vscode extension outthere, but I found them hard to use, especially for poor support for data structure like trees, and metascript addition to original leetcode file. By following this tutorial, you should make sure you have your own c++ compiler, vscode [leetcode]{https://marketplace.visualstudio.com/items?itemName=LeetCode.vscode-leetcode} extension installed.  

## usage: 
open your target leetcode file for debugging


In Run and Debug Section: launch leetcode debug 
<img width="969" alt="image" src="https://user-images.githubusercontent.com/20542539/178038758-033f51ee-b457-4fa7-9f03-3b3f799fd74c.png">

At the bottom of Solution Class:
type Debug to invoke the template:
<img width="1018" alt="image" src="https://user-images.githubusercontent.com/20542539/178038930-cce26dd6-52b3-441f-bd32-161643be9080.png">

## Step by Step:

### Add task in your_leetcode_repo_directory/.vscode/tasks.json 

```json
{
    "tasks": [
        {
            "type": "cppbuild",
            "label": "C/C++: clang++ build active file",
            "command": "/usr/bin/clang++",
            "args": [
                "-fdiagnostics-color=always",
                "-g",
                "${file}",
                "-DSITAN=1",
                "-o",
                "${fileDirname}/leetcode.out"
            ],
            "options": {
                "cwd": "${fileDirname}"
            },
            "problemMatcher": [
                "$gcc"
            ],
            "group": {
                "kind": "build",
                "isDefault": true
            },
            "detail": "Task generated by Debugger."
        }
    ],
    "version": "2.0.0"
}
```

### add configuration to your_leetcode_repo_directory/.vscode/launch.json
```json
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [


        {
            "name": "leetcode debug",
            "type": "cppdbg",
            "request": "launch",
            "program": "${workspaceFolder}/leetcode.out",
            "preLaunchTask": "C/C++: clang++ build active file",
            "args": [],
            "stopAtEntry": false,
            "cwd": "${fileDirname}",
            "environment": [],
            "externalConsole": false,
            "MIMode": "lldb"
        }

    ]
}
```
### add snippets to your_leetcode_repo_directory/.vscode/snippets.leetcode.code-snippets to enable auto template completion.
```
{
	"Debug template": {
		"scope": "cpp",
		"prefix": "DEBUG",
		"body": [
			"#if defined(SITAN)",
			"int main(){",
			"    $0",
			"}",
			"#endif"
		]
	}
}
```

### To enable correct highlighting, in your c/c++ extension settings(remember to switch setting scope to your own workspace!!!):
modify C_Cpp.default.compilerArgs to -DSITAN=1.



