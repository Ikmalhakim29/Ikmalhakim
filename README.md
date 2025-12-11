# Comprehensive Web Application Performance Testing & Analysis Report
## Student Name: Ikmalhakim Bin Mohd Fazlie
### Student ID: 2023682462
### Course: ITT440 - Network Programming
### Group: NBCS2555A
### Instructor: SHAHADAN BIN SAAD

# 1.0 Executive Summary
Performance testing is a critical phase in the Software Development Lifecycle (SDLC) to ensure that web applications remain stable, responsive, and scalable under varying levels of user traffic. This project evaluates the performance of ASCII Art Demo Web Application (http://asciiart.artillery.io:8080/) using Locust, a Python-based open-source load testing tool designed for concurrent user simulation.
Three performance tests were conducted Load Test, Stress Test, and Soak Test to measure how the application behaves under different load conditions. The objective was to capture key performance metrics such as Response Time, Throughput, and Error Rate, while identifying bottlenecks that could impact user experience. The overall findings indicate that while the ASCII Art application demonstrates excellent stability under low to moderate concurrency, noticeable degradation occurs when active users exceed 250–300 concurrent virtual users, leading to increased latency and occasional request failures. These results highlight clear opportunities for server-side optimization and horizontal scaling strategies.


# 2.0 Introduction & Objectives
Today’s applications must meet user expectations for fast loading speeds and uninterrupted service. Studies consistently show that even a one-second delay can significantly reduce user satisfaction and conversion rates. As such, performance testing is essential to validating whether a web application can maintain responsiveness under real-world usage conditions.
This assignment aims to simulate realistic user behavior and interaction with the ASCII Art web application to measure its overall robustness.


# 2.1 Project Objectives

•	To design and conduct a complete performance testing plan using a specialized testing tool (Locust).
•	To analyze core KPIs including Response Time, Throughput, and Error Rate.
•	To identify performance bottlenecks and propose data-driven recommendations for optimization.
•	To present technical findings in a structured, professional report suitable for stakeholders.


# 2.2 Target Application

Name: ASCII Art Demo Web Application
URL: http://asciiart.artillery.io:8080/
Description: A lightweight demo site that serves ASCII art via HTTP GET requests. The site’s simplicity makes it a suitable candidate for performance testing due to its static content-heavy architecture, enabling clear observation of server response behavior under varying user loads without risking ethical or legal issues.


# 3.0 Tool Selection Justification

For this project, Locust (Version 2.42.6) was selected as the performance testing tool.

Why Locust?

i. Python-Based and Easy to Script
Locust test scenarios are written in Python, making it flexible and highly customizable without complex configurations.

ii. Realistic User Simulation
Locust models virtual users (VUs) with structured tasks that simulate real behavior patterns.

iii. Web-Based Dashboard
It provides real-time metrics including RPS (Requests per Second), failures, response times, and active user counts.

iv. Lightweight and Scalable
Locust workers can be distributed across multiple machines for high-load scenarios.

v. Compared to Other Tools
Tool	Weakness	Why Locust Is Better Here
JMeter	Heavy GUI, high resource usage	Locust is faster and more lightweight
K6	Requires JavaScript scripting	Locust uses Python which is simpler
LoadRunner	Paid tool	Locust is open-source and free
Locust provides the best balance of performance, flexibility, and ease of use for this academic project.

# 4.0 Test Methodology & Environment Setup

### 4.1 Test Environment (Client Side)
To ensure the testing machine does not become the bottleneck, all tests were executed using the following hardware specifications:
Component	Specification
OS	Windows: 11
CPU:	AMD Ryzen 5 5600
RAM:	32GB DDR4
Network:	High-speed Fibre Broadband


### 4.2 Test Types Configured
| Test Type   | Peak Users | Ramp-up Rate | Duration |
|-------------|------------|--------------|----------|
| Load Test   | 50         | 5 users/s    | 1 min    |
| Stress Test | 300        | 20 users/s   | 1 min (Until Failure)    |
| Soak Test   | 300        | 10 users/s   | 10 min   |



# 5.0 Results & Critical Analysis

### 5.1 Load Test Analysis

Hypothesis:
The server should efficiently handle 50 concurrent users with minimal delays and zero errors since the application is lightweight.

Findings:

i. Average Response Time: 45–60 ms

ii. Throughput: 80–120 requests per second

iii. Error Rate: 0%

Interpretation:
The website performed exceptionally well under normal operating conditions. Response times remained consistent, indicating that the server can handle typical user loads with no risk of degradation.
No queuing delays or timeouts were observed during this test.

<img width="940" height="545" alt="image" src="https://github.com/user-attachments/assets/431cc4db-b388-4bfb-898e-b3b2506350a4" />


### 5.2 Stress Test Analysis

Hypothesis:
As concurrent users increase past 200–300, response times will rise sharply and errors (timeouts, connection failures) may occur.

Findings:
i. Peak Users Reached: 300

ii. Average Response Time: 200–350 ms

iii. Max Response Time: 1200 ms

iv. Error Rate: 1% (timeouts and connection failures)

Interpretation:
Under heavy load, the application begins to show strain:

i. Server response time increased drastically beyond 250 users.

ii. Timeouts were observed, indicating worker threads or server capacity saturation.

iii. Throughput plateaued around 300 RPS, revealing the server’s maximum capacity.

These symptoms confirm that the primary bottleneck lies in server concurrency limits rather than bandwidth.
 
 <img width="823" height="613" alt="image" src="https://github.com/user-attachments/assets/c7e40039-a974-4b77-8e96-05646d03268f" />

 <img width="839" height="66" alt="image" src="https://github.com/user-attachments/assets/1cd2b65d-6464-4509-9566-14cd147460d3" />

 
### 5.3 Soak Test Analysis

Hypothesis:
Long-duration load may reveal memory leaks or degradation over time.

Findings:

i. Duration: 10 minutes

ii. Average Response Time: 50–70 ms

iii. Maximum Response Time: ~600 ms

iv. Error Rate: 0%

Interpretation:
The application demonstrates strong long-term reliability. Response times remained consistent, and no growing trend (sawtooth or memory exhaustion pattern) was observed.
This indicates that the application handles repeated requests efficiently without accumulating resource leaks.

<img width="940" height="613" alt="image" src="https://github.com/user-attachments/assets/75a1e5b9-beb4-4528-bab9-61afad464b46" />


# 6.0 Video Presentation

A detailed walkthrough of the Locust  test execution, and result interpretation has been uploaded.

YouTube Link:

https://youtu.be/DjHJ1VpPuNs?si=hXpmmV4VvYXaKNxw 


# 7.0 Recommendations & Conclusion

### 7.1 Identified Bottlenecks

Based on the performance results:

1.	Server Concurrency Limitations
The server begins failing requests beyond 250–300 active users.

2.	Latency Spikes
During stress conditions, response time increased by more than 500%, degrading user experience.

4.	Throughput Ceiling
The system maxes out at approximately 300 RPS, suggesting limited processing threads.

### 7.2 Recommendations for Optimization

To enhance the application’s performance and scalability:

1. Horizontal Scaling
Deploy multiple instances and introduce a Load Balancer (e.g., NGINX, AWS ELB) to distribute traffic.

2. Implement Caching
Use CDN or server-level caching to serve ASCII content faster and reduce backend computation.

3. Upgrade Server Configuration
Increase the number of worker threads or upgrade server hardware (CPU/RAM) to better handle high concurrency.

4. Performance Monitoring
Integrate server profiling tools (e.g., Prometheus + Grafana) to continuously monitor CPU, memory, and I/O usage.

### 7.3 Conclusion

This project successfully demonstrates the core principles of performance testing using Locust. The ASCII Art demo site performs exceptionally under light to moderate loads but shows clear performance degradation under high concurrency. The testing methodology provided a reliable baseline for performance measurement and highlighted specific architectural areas needing improvement.
Through systematic testing and analysis, the study meets the assignment objectives by delivering actionable insights supported by empirical data, aligning with academic and industry best practices.

