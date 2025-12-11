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
