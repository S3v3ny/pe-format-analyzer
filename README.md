# PE Format Analyzer

A small C++ learning project for inspecting the structure of Windows Portable Executable (PE) files.

The current implementation validates the DOS and NT signatures, then prints the entry-point RVA, image base, section count, and key fields from every section table entry.

## Features

- Validates the DOS `MZ` signature
- Locates and validates the PE/NT header
- Prints the entry-point RVA and image base
- Enumerates section names, virtual addresses, raw offsets, and sizes
- Uses the Windows API for file and memory handling

## Requirements

- Windows
- Visual Studio Build Tools or another compiler that provides `Windows.h`

## Build

From a Developer Command Prompt for Visual Studio:

```powershell
cl /EHsc /std:c++17 PE.cpp
```

## Usage

The current version reads a file named `test.exe` from the working directory:

```powershell
Copy-Item C:\path\to\sample.exe .\test.exe
.\PE.exe
```

Example output:

```text
PE文件基本信息:
  入口点RVA: 0x...
  镜像基址: 0x...
  节表数量: ...
  节表 1:
    名称: .text
    虚拟大小: 0x...
```

Only inspect files you are authorized to analyze. Prefer an isolated VM for untrusted samples; this tool reads a file but does not execute it.

## Current limitations

- The input path is currently hard-coded as `test.exe`.
- The parser is Windows-only.
- Bounds checks for malformed or intentionally corrupted PE files are still limited.
- PE32 and PE32+ handling is not yet separated explicitly.
- Automated tests and structured output are not yet included.

## Roadmap

- Accept the file path through command-line arguments
- Distinguish PE32 and PE32+
- Add robust range and overflow validation
- Decode section characteristics and data directories
- Add JSON output and tests with safe fixtures

## 中文说明

这是一个用于学习 Windows PE 文件结构的 C++ 项目。目前可以验证 DOS/NT 头，并输出入口点、镜像基址和节表信息。

编译后，将待分析文件命名为 `test.exe` 并放到程序工作目录中运行。请仅分析你有权访问的文件；对于不可信样本，建议在隔离虚拟机中操作。
