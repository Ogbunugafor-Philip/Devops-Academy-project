# Module 1_Server Availability Logger — Automating Network Health Checks via ICMP (Ping)

## Introduction
In every production environment, ensuring that servers and network services remain reachable is a core requirement for maintaining system reliability and user trust. Even a few minutes of downtime can affect thousands of users, disrupt operations, and lead to financial or reputational losses.
This project aims to develop a lightweight automated network monitoring tool using Python that continuously pings target servers, logs their response times, and alerts when any host becomes unreachable. The tool provides a simple and cost-effective approach to monitoring uptime without requiring complex enterprise systems.
By applying fundamental networking principles such as TCP/IP, DNS resolution, and OSI Layer 3 communication, the project bridges theoretical knowledge with practical DevOps implementation. It helps learners and professionals gain hands-on experience in infrastructure reliability, network automation, and real-time system visibility, which are essential components of modern DevOps and site reliability engineering practices.

## Statement of the Problem
Organizations often depend on manual or third-party monitoring tools that may not provide real-time feedback or may be too costly for small environments.
When servers go down unexpectedly, it can take too long before system administrators are aware of the issue, leading to service degradation and missed uptime SLAs.
There is therefore a need for a lightweight, script-based monitoring solution that can:
- Detect server unavailability instantly,
- Log downtime events automatically, and
- Provide a basis for further automation or alert integration (e.g., email/SMS/Slack notifications).

## Project Objectives
i.	Understand how TCP/IP and DNS facilitate network communication and address resolution.

ii.	Implement a Python script to send ICMP (ping) requests to multiple servers and record their status.

iii.	Log results with timestamps in a structured format (CSV or text file) for easy review.

iv.	Extend the tool to include optional alerting or dashboard visualization.

v.	Demonstrate how low-level networking knowledge supports high-level DevOps monitoring and automation tasks.



## Project Steps

Step 1: Set up the project environment

Step 2: Define target hosts

Step 3: Implement ping functionality

Step 4: Log results and handle alerts


## Project Implementation
### Step 1: Set up the project environment

We are going to build a Server Availability Logger. This is a small, automated network monitoring tool you’re building in Python to check whether servers or websites are up (reachable) or down (unreachable). Before building the Server Availability Logger, it’s important to prepare a clean and structured working environment. This ensures that all dependencies are properly managed, the project remains organized, and future updates or scaling can be done easily. In this step, you’ll create the main project folder, set up a Python virtual environment, install the necessary libraries, and create the initial files (ping_logger.py, servers.txt, and logs/) that will serve as the foundation for your monitoring tool.

- Open Git Bash
- Create a project folder and move into in. run;
```
mkdir -p Projects
cd Projects
```
<img width="854" height="168" alt="image" src="https://github.com/user-attachments/assets/4b9885ca-6bec-4d2f-8e98-f4ef49559c74" />


- Create the server-availability-logger folder and move into it. Run;
```
mkdir -p server-availability-logger
cd server-availability-logger
``` 
<img width="975" height="237" alt="image" src="https://github.com/user-attachments/assets/62f052b9-ea68-4e10-aac5-60ddcf4ded95" />

We would create and activate a Python virtual environment. This isolates the project’s dependencies so the libraries you install don’t interfere with other Python projects on your system.

- In the server-availability-logger folder, run these commands to create a virtual environment and activate it;
```
py -m venv venv
source venv/Scripts/activate
```
<img width="975" height="189" alt="image" src="https://github.com/user-attachments/assets/e8832545-48c7-48b9-bf33-9815368e7f62" />


- Install Required Libraries. Run;
```
pip install --upgrade pip
pip install ping3 colorama pandas
``` 
<img width="975" height="259" alt="image" src="https://github.com/user-attachments/assets/591f680c-08df-4615-b27f-872bedbd1571" />

#### Explanation of each installed library:
a. 🛰 ping3 → sends ICMP echo requests (the “ping” itself).

b. 🎨 colorama → adds colored console output (green = up, red = down).

c. 📊 pandas → optional, used for structured logging (CSV / data frames).

- To confirm the libraries installed correctly, run;
```
pip list
```
<img width="975" height="271" alt="image" src="https://github.com/user-attachments/assets/5cc11686-625f-45e7-b145-ca0bbae10054" />


- Inside the server-availability-logger directory, create the main Python script, create a file that will hold your target servers and create a folder to store logs. Run;
```
touch ping_logger.py
touch servers.txt
mkdir logs
```
<img width="975" height="210" alt="image" src="https://github.com/user-attachments/assets/4258ff0a-7bee-4ba7-a2c9-0881ee810ab8" />


- To verify that the folder and files were created correctly, run;
```
ls -la
``` 
<img width="975" height="293" alt="image" src="https://github.com/user-attachments/assets/cf25f571-2c5b-4b55-ab9c-dd7769e6eb90" />

### Step 2: Define target hosts

Before any monitoring or logging can happen, the tool needs to know which servers or websites to check.
This step is about creating a simple, flexible way to store those targets so that you can:
- easily add or remove hosts without touching your Python code
- allow the script to read them dynamically
- scale from 2 to 200+ hosts effortlessly.

By keeping all the targets inside a plain text file called servers.txt, we separate configuration from logic, which is a best practice in DevOps automation.
Each line in this file will represent one host (for example: 8.8.8.8, aws.amazon.com, or github.com).

- Run these commands to save these servers in your created servers.txt file
```
echo "8.8.8.8" > servers.txt
echo "1.1.1.1" >> servers.txt
echo "aws.amazon.com" >> servers.txt
echo "github.com" >> servers.txt
```
- To verify, run;
```
cat servers.txt
```
 <img width="975" height="147" alt="image" src="https://github.com/user-attachments/assets/e07c6c7d-c102-4c8b-9094-462edb0a25d5" />


We’ll now write a small block of Python code inside ping_logger.py that:

  a. Opens servers.txt
  
  b. Reads all the lines
  
  c. Cleans up spaces and line breaks
  
  d. Stores the hosts in a Python list for later use.


- Open ping_logger.py with a text editor and paste the below script
```
# ping_logger.py
"""
Server Availability Logger — Step 2.2
Reads the list of target hosts from servers.txt.
"""

def load_targets(file_path="servers.txt"):
    """Read target hosts from a text file and return as a list"""
    try:
        with open(file_path, "r") as f:
            hosts = [line.strip() for line in f if line.strip()]
        print(f"✅ Loaded {len(hosts)} hosts from {file_path}")
        return hosts
    except FileNotFoundError:
        print("❌ servers.txt not found! Please create it first.")
        return []

# Quick test
if __name__ == "__main__":
    targets = load_targets()
    print("Targets to monitor:", targets)
```


- Run the script with this command;
```
py ping_logger.py
``` 
<img width="975" height="213" alt="image" src="https://github.com/user-attachments/assets/2cbb84ad-4ac9-4a24-8db3-3ea6084b5ed4" />

### Step 3: Implement ping functionality
Now that our tool can dynamically load target hosts from servers.txt, the next step is to check their actual network availability using the ICMP (Internet Control Message Protocol) — the same mechanism used by the ping command in any operating system.
At this stage, we’ll integrate the ping3 library into our script to send ICMP echo requests to each target host and capture the response time in milliseconds. If the host responds, it will be marked as “Reachable”; if not, the status will be “Unreachable.”

To make the output visually intuitive, we’ll also use the colorama library to display:
- 🟢 Green for reachable hosts (healthy servers)
- 🔴 Red for unreachable hosts (possible outage)

This step transforms our project from a static configuration reader into a functional network monitoring tool that provides real-time visibility into system uptime and latency.

- Copy and replace everything in your ping_logger.py file with the below;
```
# ping_logger.py
"""
Server Availability Logger — Step 3.1
Implements ICMP ping checks and colored output for reachability.
"""

from ping3 import ping
from colorama import Fore, Style, init

# initialize colorama
init(autoreset=True)

def load_targets(file_path="servers.txt"):
    """Read target hosts from a text file and return as a list"""
    try:
        with open(file_path, "r") as f:
            hosts = [line.strip() for line in f if line.strip()]
        print(f"✅ Loaded {len(hosts)} hosts from {file_path}")
        return hosts
    except FileNotFoundError:
        print("❌ servers.txt not found! Please create it first.")
        return []


def check_host_availability(host):
    """Ping a single host and print its availability"""
    try:
        response_time = ping(host, timeout=2)  # timeout after 2 seconds
        if response_time is not None:
            print(Fore.GREEN + f"🟢 {host} is Reachable — {round(response_time * 1000, 2)} ms")
        else:
            print(Fore.RED + f"🔴 {host} is Unreachable")
    except Exception as e:
        print(Fore.RED + f"⚠️ Error pinging {host}: {e}")


if __name__ == "__main__":
    targets = load_targets()
    print("\n--- Starting Ping Checks ---\n")
    for host in targets:
        check_host_availability(host)
    print("\n✅ Ping test completed!\n")
```

- Run the file with this command;
```
py ping_logger.py
``` 
<img width="953" height="240" alt="image" src="https://github.com/user-attachments/assets/5661edf0-6833-4182-9b6f-4aa568650e1a" />



### Step 4: Log results and handle alerts
After successfully implementing the ping functionality, the next step is to record those results so that network administrators or DevOps engineers can review uptime trends over time.

In this step, we’ll:
- Create a structured log file (logs/server_status_log.csv) to store every ping result.
- Include important data points: Timestamp, Host, Status (Reachable/Unreachable), and Response Time (ms).
- Add a simple alert system that immediately warns when a server is unreachable, printing a ⚠️ message to the console.

This allows our tool to serve as a lightweight monitoring and alerting system, useful for environments without enterprise tools like Zabbix or Datadog.

- Replace your current ping_logger.py file with this version
```
# ping_logger.py
"""
Server Availability Logger - Working Version
Logs each ping result to CSV file
"""
import csv
import os
from datetime import datetime
from ping3 import ping
from colorama import Fore, init

# Initialize colorama
init(autoreset=True)


def load_targets(file_path="servers.txt"):
    """Read target hosts from a text file"""
    try:
        with open(file_path, "r") as f:
            hosts = [line.strip() for line in f if line.strip()]
        print(f"✅ Loaded {len(hosts)} hosts from {file_path}")
        return hosts
    except FileNotFoundError:
        print("❌ servers.txt not found!")
        return []


def setup_log_file():
    """Create logs directory and CSV file with headers"""
    log_dir = "logs"
    if not os.path.exists(log_dir):
        os.makedirs(log_dir)
    
    log_file = os.path.join(log_dir, "server_status_log.csv")
    
    # Create file with header if it doesn't exist
    if not os.path.exists(log_file):
        with open(log_file, "w", newline="") as f:
            writer = csv.writer(f)
            writer.writerow(["Timestamp", "Host", "Status", "Response_Time(ms)"])
        print(f"📝 Created log file: {log_file}")
    
    return log_file


def write_log(log_file, timestamp, host, status, response_time):
    """Append a log entry to the CSV file"""
    with open(log_file, "a", newline="") as f:
        writer = csv.writer(f)
        writer.writerow([timestamp, host, status, response_time])
    print(f"✍️  Logged: {host} -> {status}")


def check_host(host, log_file):
    """Ping a host and log the result"""
    timestamp = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    
    try:
        response_time = ping(host, timeout=2)
        
        if response_time is not None:
            response_ms = round(response_time * 1000, 2)
            status = "Reachable"
            print(Fore.GREEN + f"🟢 {host} is Reachable — {response_ms} ms")
            write_log(log_file, timestamp, host, status, response_ms)
        else:
            status = "Unreachable"
            print(Fore.RED + f"🔴 {host} is Unreachable")
            print(Fore.YELLOW + f"⚠️  Alert: {host} is DOWN!")
            write_log(log_file, timestamp, host, status, "-")
            
    except Exception as e:
        print(Fore.RED + f"❌ Error pinging {host}: {e}")
        write_log(log_file, timestamp, host, "Error", "-")


def main():
    """Main execution"""
    # Setup
    targets = load_targets()
    if not targets:
        return
    
    log_file = setup_log_file()
    
    # Run ping checks
    print("\n--- Starting Ping Checks ---\n")
    for host in targets:
        check_host(host, log_file)
    
    # Final message
    print(f"\n✅ Ping test completed!")
    print(f"📄 Log file: {log_file}\n")


if __name__ == "__main__":
    main()
```

- Run the file with this command;
```
py ping_logger.py
``` 
<img width="975" height="418" alt="image" src="https://github.com/user-attachments/assets/2bd5bc5a-405d-4adb-8da3-420ef4e02095" />



- Run the below command to see the details of the server check;
```
cat logs/server_status_log.csv
```
<img width="975" height="319" alt="image" src="https://github.com/user-attachments/assets/13745649-29aa-45f9-b7af-3d3cce065281" />


## Conclusion
The Server Availability Logger project successfully demonstrates how foundational networking principles can be transformed into a practical DevOps monitoring solution using Python. By leveraging lightweight libraries such as ping3 for ICMP echo requests and colorama for visual feedback, this project offers a clear understanding of how network health checks can be automated efficiently without relying on heavy third-party systems.
Through the four key steps — environment setup, target definition, ping implementation, and logging with alerts — you’ve built a complete, functional tool that:
- ✅ Detects server reachability in real time
- ✅ Records every check with timestamps and response times
- ✅ Alerts instantly when a host becomes unreachable
- ✅ Stores results in a structured CSV log for later analysis
  
This project lays the groundwork for more advanced monitoring automation. The same logic can be extended to include features such as email or Slack notifications, dashboard visualization, or integration with CI/CD pipelines.
Overall, the Server Availability Logger stands as a beginner-friendly yet industry-relevant introduction to network automation, infrastructure observability, and real-world DevOps scripting — transforming theoretical networking knowledge into hands-on operational insight.






