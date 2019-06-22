---
title: wsl+vscode配置
date: 2019-06-22 11:39:07
tags: 
    - vscode
---
# vscode+coderuner+wsl C++编译环境
```json
{
    "code-runner.executorMap": {
        "c": "gcc ./main.c && ./a.out",
        "cpp": "g++ ./main.cpp -pthread && ./a.out"
    },
    "C_Cpp.default.intelliSenseMode": "gcc-x64",
    "code-runner.runInTerminal": true,
    "code-runner.saveAllFilesBeforeRun": true,
    "code-runner.clearPreviousOutput": true,
    "terminal.integrated.shell.windows": "C:\\Windows\\System32\\wsl.exe",
    "files.associations": {
        "thread": "cpp",
        "cstdio": "cpp",
        "ostream": "cpp",
        "string": "cpp"
    },
    "C_Cpp.clang_format_fallbackStyle": "WebKit",
    "C_Cpp.errorSquiggles": "Disabled"
}
```
