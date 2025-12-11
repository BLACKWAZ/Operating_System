1. Performance Testing Plan

Objective:
To establish a systematic and repeatable methodology for monitoring system resource usage and evaluating how the Linux server behaves under different workload conditions. The goal is to gather accurate performance data while maintaining a lightweight, command-line–only environment consistent with the requirements of a headless server.

⸻

Remote Monitoring Methodology

For this coursework, I adopted a lightweight, agent-free monitoring strategy. Instead of installing additional monitoring daemons or graphical dashboards on the server, all performance observations are made remotely from the workstation using SSH. This ensures minimal resource overhead and provides an industry-standard approach to server monitoring.

The monitoring process relies entirely on built-in Linux utilities and small terminal-based tools that provide real-time insights into CPU usage, memory allocation, process activity, disk I/O, and network behaviour.

⸻

Tools Selected for Monitoring

1. top – Real-time Resource Overview

top offers a live snapshot of system resource consumption and process activity.

Purpose:
	•	Observe overall CPU utilisation
	•	Monitor memory usage
	•	Track load averages
	•	Identify high-usage processes in real time

Commands used 
top
Inside the program:
	•	Press P to reorder processes by CPU usage
	•	Press M to list processes by memory consumption

(HTOP/BTOP could be alternatives, but for this project I prioritised core utilities already included in most server distributions.)

⸻

2. ps + Filtering Options – Detailed Process Snapshots

ps provides a static, detailed list of running processes that can be sorted or filtered depending on the information needed.

Purpose:
	•	Capture process state at specific test intervals
	•	Compare memory and CPU consumption under different workloads
	•	Verify correct process creation during performance tests
example commands

ps aux
ps aux --sort=-%cpu     # sort by highest CPU usage
ps aux --sort=-%mem     # sort by highest memory usage
ps -u <username>        # view processes for specific user
ps -p <PID>             # view a single process by PID
pstree -p               # visualise process hierarchy

3. nmon – Exportable System Statistics

nmon provides a more comprehensive set of performance metrics while still remaining lightweight and terminal-based.

Purpose:
	•	Capture system behaviour over time
	•	Export monitoring data for later analysis in Week 6
	•	Collect CPU, memory, disk, and network statistics simultaneously
commands syntax:

nmon -t

Useful options:
	•	-o → save output to file
	•	-C → CPU-related statistics
	•	-M → memory metrics
	•	-D → disk activity
	•	-N → network usage

Testing Approach




