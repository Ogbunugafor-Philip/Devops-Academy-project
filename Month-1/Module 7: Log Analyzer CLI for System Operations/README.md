# Module 7_Log Analyzer CLI for System Operations

## Introduction
In every IT environment, logs serve as the digital footprints of system activity. They capture everything from user logins and service failures to security warnings and performance trends. For system administrators and DevOps engineers, logs are often the first point of truth when diagnosing issues or monitoring infrastructure health.
However, raw logs are typically long, unstructured, and complex. A single day of server activity can generate thousands of log entries, making manual review almost impossible. To make sense of this data, teams need tools that can quickly extract the right information without wasting time.
A Log Analyzer Command Line Interface (CLI) provides exactly that. By combining the power of Python scripting with Linux log files, this project introduces learners to how DevOps professionals manage, filter, and interpret logs in real time. It demonstrates how automation can transform raw log files into actionable insights for faster decision-making and improved system reliability.

## Statement of Problem
Modern systems generate massive log files containing security events, application errors, and user activity. Manually scrolling through these logs is slow, error-prone, and often leads to missed critical issues. This results in delayed troubleshooting, reduced reliability, and increased security risks.
This project addresses the gap by creating a Python-powered CLI Log Analyzer that can quickly filter and highlight relevant information such as errors, warnings, or time-based events, making system operations faster and more reliable.

## Project Objectives
- Develop a CLI-based tool to parse and analyze log files automatically.
- Provide options to filter logs by date, keyword, severity level, or service.
- Generate concise summaries and highlight error/warning events for quick visibility.
- Improve troubleshooting efficiency by reducing manual search time.
- Deliver a lightweight, Python-based tool suitable for daily system operations.

## Project Steps
Step 1: Set Up the Environment

Step 2: Build the CLI Structure

Step 3: Parse the Log File

Step 4: Add Analysis Features

## Project Implementation

### Step 1: Set Up the Environment
Before building the Log Analyzer CLI, we need to prepare the working environment. This step ensures that you have the required tools installed and that your project has a structured starting point. By setting up everything correctly at the beginning, you’ll avoid errors later and keep your project organized.

- Go to the official Python download page: https://www.python.org/downloads/
- Download the latest stable release ≥3.9 (preferably 3.13.5 for best compatibility).
- Run the installer:
    - ✅ Check the box “Add Python to PATH” before clicking Install Now.
    - This ensures you can use python from the command line.
- After installation, open Command Prompt and check:
```
Py --version
```
<img width="769" height="95" alt="image" src="https://github.com/user-attachments/assets/0159db79-41f9-49e8-876f-c80c491729c0" />

- Create a Project Folder. Open Git Bash and run:
```
mkdir log_analyzer_cli
cd log_analyzer_cli
```
<img width="975" height="153" alt="image" src="https://github.com/user-attachments/assets/62fa3042-62f5-48a1-bfbe-750b51f3185b" />


This folder will hold all your project files (log_analyzer.py and sample logs).

- Create a dummy log file for practice. Open a vi text editor. Run;
```
vi sample.log
```
- Paste the below
```
2025-10-02 10:15:01 INFO User logged in
2025-10-02 10:20:45 WARNING Disk space low
2025-10-02 10:25:12 ERROR Service crashed
```
<img width="813" height="184" alt="image" src="https://github.com/user-attachments/assets/5c925d92-4542-4d38-bae9-d71d42407afc" />

### Step 2: Build the CLI Structure

Now that the environment is ready and we have a sample log file, the next step is to design the command-line interface (CLI) for our tool. A CLI allows users to interact with the script by passing options (arguments) directly in the terminal, instead of hardcoding values.
In Python, the argparse library is the standard way to build CLIs. With it, we can define arguments such as the log file path, the keyword to search, the severity level to filter, or even the date range. This makes our tool flexible and reusable for different scenarios.
The goal of this step is not to process logs yet — but simply to set up the “skeleton” of our program and confirm that arguments are captured correctly.

- Create the Python file. Run;
```
touch log_analyzer.py
```
- Open the created file with VI. Run;
```
vi log_analyzer.py
```
- Paste the below and then save it
```
import argparse  # <-- Import Libraries: argparse handles command-line arguments

def build_cli():
    parser = argparse.ArgumentParser(
        description="Log Analyzer CLI — Step 2: capture arguments only"
    )
    parser.add_argument(
        "--file", "-f", required=True,
        help="Path to the log file (e.g., sample.log)"
    )
    parser.add_argument(
        "--keyword", "-k",
        help="Keyword to search for (e.g., 'login')"
    )
    parser.add_argument(
        "--level", "-l", choices=["ERROR", "WARNING", "INFO"],
        help="Filter by severity level"
    )
    parser.add_argument(
        "--date", "-d",
        help="Filter by date/time substring (e.g., '2025-10-02' or '10:20')"
    )
    return parser.parse_args()

def main():
    args = build_cli()
    # Step 2 goal: just show what we captured (no log parsing yet)
    print("ARGS RECEIVED:")
    print(f"  file    = {args.file}")
    print(f"  keyword = {args.keyword}")
    print(f"  level   = {args.level}")
    print(f"  date    = {args.date}")

if __name__ == "__main__":
    main()

  ```

<img width="975" height="834" alt="image" src="https://github.com/user-attachments/assets/a83050b6-1bed-4ee8-8159-ae7f03e584ee" />

- Make it executable. Run;
```
chmod +x log_analyzer.py
```

- Check the CLI help to confirm argparse is wired correctly. Run;
```
py -3 log_analyzer.py –help
```
 <img width="975" height="359" alt="image" src="https://github.com/user-attachments/assets/142bb4c6-5fd7-4fcb-8553-4a5333076fbc" />


- Run tests to confirm arguments are captured
```
py log_analyzer.py --file sample.log
``` 
<img width="975" height="283" alt="image" src="https://github.com/user-attachments/assets/ff493961-9fd0-4dd6-b079-ecc55c0980f6" />

```
py log_analyzer.py --file sample.log --level ERROR
``` 
<img width="964" height="189" alt="image" src="https://github.com/user-attachments/assets/9fd24688-8fac-45a9-becf-cc26d35c0bfc" />

```
py log_analyzer.py --file sample.log --keyword "logged" --date "2025-10-02"
```
<img width="975" height="219" alt="image" src="https://github.com/user-attachments/assets/5c01fe82-fbd9-4ba5-b2dc-a27c3053c4ef" />

### Step 3: Parse the Log File
With our CLI structure ready, the next step is to actually read and process log files. The purpose of parsing is to scan through the file line by line and return only the entries that match the user’s criteria. Instead of dumping thousands of lines, the tool should highlight exactly what matters — errors, warnings, keywords, or events within a date range.
By implementing log file parsing, we move from a simple argument-capturing script to a functional analyzer that extracts useful insights from raw system data.

- Open the Python file to edit. Run,
```
vi log_analyzer.py
```

- Erase the old content. Paste this EXACT code. This code imports libraries (argparse, os, sys), reads the file line by line, and filters by --level, --keyword, and --date.

To erase entire code in vi, run 
```
:1,$d
```

- Now, paste this one
  
```
import argparse
import os
import sys

def build_cli():
    parser = argparse.ArgumentParser(
        description="Log Analyzer CLI — Step 3: parse and filter"
    )
    parser.add_argument(
        "--file","-f", required=True,
        help="Path to the log file (e.g., sample.log)"
    )
    parser.add_argument(
        "--keyword","-k",
        help="Keyword to search (e.g., 'login')"
    )
    parser.add_argument(
        "--level","-l", choices=["ERROR","WARNING","INFO"],
        help="Filter by severity level"
    )
    parser.add_argument(
        "--date","-d",
        help="Filter by date/time substring (e.g., '2025-10-02' or '10:20')"
    )
    return parser.parse_args()

def line_matches(line, args):
    # Level filter: look for the word (e.g., "ERROR") in the line
    if args.level and args.level not in line:
        return False
    # Keyword filter: case-insensitive
    if args.keyword and args.keyword.lower() not in line.lower():
        return False
    # Date/time filter: simple substring match
    if args.date and args.date not in line:
        return False
    return True

def analyze_log(file_path, args):
    if not os.path.exists(file_path):
        print(f"ERROR: File not found: {file_path}", file=sys.stderr)
        sys.exit(1)

    matches = 0
    with open(file_path, "r", encoding="utf-8", errors="ignore") as f:
        for raw in f:
            line = raw.rstrip("\n")
            if line_matches(line, args):
                print(line)
                matches += 1

    print(f"\n[Matched {matches} line(s)]")

def main():
    args = build_cli()
    analyze_log(args.file, args)

if __name__ == "__main__":
    main()
```
<img width="975" height="678" alt="image" src="https://github.com/user-attachments/assets/1aec0374-a84c-4817-9162-bdc8b6a4da6c" />

- Check the CLI help to confirm argparse is wired correctly. Run;
```
py -3 log_analyzer.py –help
```
<img width="975" height="147" alt="image" src="https://github.com/user-attachments/assets/32e03845-95af-415f-a44c-f3e3da8e8bd3" />


- Run with only the file (should print everything + a match count)
```
py log_analyzer.py --file sample.log
```
<img width="975" height="261" alt="image" src="https://github.com/user-attachments/assets/58282364-14a6-4d58-ba0f-61d9a406575f" />
 

- Filter by level (should print only ERROR lines + count)
```
py log_analyzer.py --file sample.log --level ERROR
```
<img width="975" height="141" alt="image" src="https://github.com/user-attachments/assets/93ed746d-cadc-4a33-ab78-a2ace9b74314" />


- Filter by keyword (case-insensitive)
```
py log_analyzer.py --file sample.log --keyword "logged"
``` 
<img width="975" height="160" alt="image" src="https://github.com/user-attachments/assets/a7c31503-3f6d-4f3c-9670-baf71bddec69" />


- Filter by date/time substring
```
py log_analyzer.py --file sample.log --date "2025-10-02"	
```
<img width="975" height="211" alt="image" src="https://github.com/user-attachments/assets/747c9ebd-3893-4823-9e22-c037e0c07964" />
 

- Combine filters (example: ERROR on that date)
```
py log_analyzer.py --file sample.log --level ERROR --date "2025-10-02"
```
<img width="975" height="140" alt="image" src="https://github.com/user-attachments/assets/609a430a-a95f-4a5c-a3b7-f9ec1e30683d" />


### Step 4: Add Analysis Features
We’ll create a new Python file log_summary.py that reads your log file, counts how many ERROR, WARNING, and INFO messages appear (both overall and within any filters you pass), prints a summary on the terminal, and can also save a text report or generate an HTML report (which you can open in your browser and “Print → Save as PDF”).


- In the project folder, run this command + script adding that would assist in report generation
```
cat > log_summary.py << 'PY'
import argparse
import os
import sys

def parse_args():
    p = argparse.ArgumentParser(
        description="Log Summary — counts ERROR/WARNING/INFO and produces reports (separate from log_analyzer.py)"
    )
    p.add_argument("--file","-f", required=True, help="Path to the log file (e.g., sample.log)")
    p.add_argument("--level","-l", choices=["ERROR","WARNING","INFO"], help="Filter by severity for matched summary")
    p.add_argument("--keyword","-k", help="Keyword filter (case-insensitive)")
    p.add_argument("--date","-d", help="Date/time substring filter (e.g., '2025-10-02')")
    p.add_argument("--out","-o", help="Save TEXT report to this path (e.g., analysis_report.txt)")
    p.add_argument("--html", help="Save HTML report to this path (e.g., analysis_report.html)")
    p.add_argument("--max-highlights","-m", type=int, default=5, help="How many matching lines to include in highlights")
    return p.parse_args()

def passes_filters(line, a):
    if a.level and a.level not in line: return False
    if a.keyword and a.keyword.lower() not in line.lower(): return False
    if a.date and a.date not in line: return False
    return True

def main():
    a = parse_args()
    if not os.path.exists(a.file):
        print(f"ERROR: File not found: {a.file}", file=sys.stderr)
        sys.exit(1)

    totals = {"ERROR":0, "WARNING":0, "INFO":0}
    matched = {"ERROR":0, "WARNING":0, "INFO":0}
    highlights = []

    with open(a.file, "r", encoding="utf-8", errors="ignore") as f:
        for raw in f:
            line = raw.rstrip("\n")

            # Count totals for the whole file
            if "ERROR" in line:   totals["ERROR"]   += 1
            if "WARNING" in line: totals["WARNING"] += 1
            if "INFO" in line:    totals["INFO"]    += 1

            # Count only lines that pass filters for matched summary
            if passes_filters(line, a):
                if "ERROR" in line:   matched["ERROR"]   += 1
                if "WARNING" in line: matched["WARNING"] += 1
                if "INFO" in line:    matched["INFO"]    += 1
                if len(highlights) < a.max_highlights:
                    highlights.append(line)

    filters = f"Filters -> level={a.level or '-'}, keyword={a.keyword or '-'}, date={a.date or '-'}"

    # Build TEXT summary
    text_lines = [
        "----- SUMMARY (Overall File) -----",
        f"Errors: {totals['ERROR']}, Warnings: {totals['WARNING']}, Info: {totals['INFO']}",
        "",
        "----- SUMMARY (Matched with Current Filters) -----",
        filters,
        f"Errors: {matched['ERROR']}, Warnings: {matched['WARNING']}, Info: {matched['INFO']}",
        "",
        f"----- HIGHLIGHTS (first {len(highlights)} match(es)) -----"
    ] + (highlights if highlights else ["(no matching lines)"])

    # Print to terminal
    print("\n".join(text_lines))

    # Optionally save TEXT report
    if a.out:
        try:
            with open(a.out, "w", encoding="utf-8") as tf:
                tf.write("LOG SUMMARY REPORT\n")
                tf.write(f"Source: {a.file}\n{filters}\n\n")
                tf.write("\n".join(text_lines) + "\n")
            print(f"\n[Saved text report to {a.out}]")
        except Exception as e:
            print(f"\nERROR: Could not write text report {a.out}: {e}", file=sys.stderr)

    # Optionally save HTML report (you can Print -> Save as PDF)
    if a.html:
        def esc(s): return s.replace("&","&amp;").replace("<","&lt;").replace(">","&gt;")
        html = f"""<!doctype html>
<html><head><meta charset="utf-8"><title>Log Summary Report</title>
<style>body{{font-family:Arial,Helvetica,sans-serif;max-width:900px;margin:40px auto;line-height:1.5}}
pre{{background:#f6f8fa;padding:8px;border-radius:6px;white-space:pre-wrap}}</style></head>
<body>
<h1>Log Summary Report</h1>
<p><strong>Source:</strong> {esc(a.file)}</p>
<p><strong>{esc(filters)}</strong></p>
<h2>Summary (Overall File)</h2>
<p>Errors: {totals['ERROR']}, Warnings: {totals['WARNING']}, Info: {totals['INFO']}</p>
<h2>Summary (Matched with Current Filters)</h2>
<p>Errors: {matched['ERROR']}, Warnings: {matched['WARNING']}, Info: {matched['INFO']}</p>
<h2>Highlights (first {len(highlights)} match(es))</h2>
{"<pre>" + "\\n".join(esc(h) for h in highlights) + "</pre>" if highlights else "<p><em>(no matching lines)</em></p>"}
</body></html>"""
        try:
            with open(a.html, "w", encoding="utf-8") as hf:
                hf.write(html)
            print(f"[Saved HTML report to {a.html}]")
        except Exception as e:
            print(f"\nERROR: Could not write HTML report {a.html}: {e}", file=sys.stderr)

if __name__ == "__main__":
    main()
PY
```
<img width="975" height="553" alt="image" src="https://github.com/user-attachments/assets/0cc120ca-7c25-4b3d-bcdd-0de9bcab233a" />

- Run a simple summary
```
py log_summary.py --file sample.log
``` 
<img width="975" height="358" alt="image" src="https://github.com/user-attachments/assets/cfe28f17-05e9-4b69-bf28-57c8aeec3f0b" />

- Save a TEXT report
```
py log_summary.py --file sample.log --out analysis_report.txt
``` 
<img width="975" height="305" alt="image" src="https://github.com/user-attachments/assets/ffd9c9e9-f70c-4055-9f62-7cf45c4f6a43" />

```
cat analysis_report.txt
``` 
<img width="975" height="356" alt="image" src="https://github.com/user-attachments/assets/34949e6d-444a-4fb6-90a3-4a0723752c1f" />

This would save the report in your project file. You can check manually in your file explorer to see the report

- Save an HTML report (then open and Save as PDF)
```
py log_summary.py --file sample.log --html analysis_report.html
cmd.exe /c start analysis_report.html
``` 
<img width="975" height="431" alt="image" src="https://github.com/user-attachments/assets/1d71df43-f4a8-4c3d-abca-55d654a65e90" />

- Now, lets do a check. Let us go to the project folder to see if the text and HTML we just generated are there
 <img width="975" height="216" alt="image" src="https://github.com/user-attachments/assets/42570e93-18e9-4637-b61e-da80799d82d1" />


- To save both reports at once (text file and HTML), Run;
```
py log_summary.py --file sample.log --out analysis_report.txt --html analysis_report.html
```
<img width="975" height="413" alt="image" src="https://github.com/user-attachments/assets/a24ae4f8-6bf2-420c-9778-992a5f0b9418" />

### Conclusion
This project demonstrates how raw, unstructured log data can be transformed into meaningful insights using Python and the command line. By building a Log Analyzer CLI, we automated the tedious process of scanning through thousands of log entries, making it easier to detect errors, warnings, and performance issues in real time.
Through the step-by-step implementation, learners gained hands-on experience with essential DevOps practices: setting up a Python environment, designing a CLI with argparse, parsing and filtering logs, and finally generating both text and HTML reports for actionable visibility.
The end result is a lightweight yet powerful tool that improves troubleshooting efficiency, strengthens system monitoring, and reflects the everyday workflow of system administrators and DevOps engineers. More importantly, it highlights how automation and scripting can reduce human error, speed up incident response, and increase overall infrastructure reliability.







