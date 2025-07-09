CMCD Project Overview
This project implements a system for collecting, processing, and analyzing Common Media Client Data (CMCD) - a standardized format for streaming media telemetry defined by the Consumer Technology Association (CTA).

Core Components
Data Collection Infrastructure (AWS CloudFront + Kinesis)

Uses CloudFront distribution with real-time logs to capture CMCD metrics from streaming clients
Sends log data to Kinesis Data Stream for real-time processing
Lambda function processes the Kinesis stream data and stores it in InfluxDB
Data Storage

InfluxDB time-series database stores CMCD metrics
Organized in a database called "cmcd-metrics" with measurements in "cloudfront_logs"
Analytics Server (MCP Server)

Model Context Protocol (MCP) server provides tools to analyze CMCD data
Implements several analysis tools:
get_average_bitrate: Calculate average bitrate from metrics
get_session_details: Retrieve detailed session information
analyze_buffer_events: Analyze buffer-related events and rebuffering
identify_playback_errors: Detect potential playback issues

Client Components
Web player (index.html) using HLS.js with CMCD integration
Python client (cmcd_client.py) for interacting with the MCP server
Key CMCD Metrics Tracked
cmcd_bl: Buffer level in milliseconds
cmcd_br: Bitrate in kbps
cmcd_d: Duration in milliseconds
cmcd_mtp: Media type
cmcd_su: Startup delay in milliseconds
cmcd_tb: Target buffer in milliseconds
time_taken: Request processing time
edge_location: CDN edge location

Infrastructure Architecture

The project uses AWS services in a well-architected setup:
CloudFront for content delivery with CMCD field capture
Kinesis for real-time data streaming
Lambda for data processing
InfluxDB (via AWS Timestream) for time-series data storage
VPC with public/private subnets for security
Bastion host for secure access to the database

Use Cases

This system allows you to:
Monitor streaming media quality in real-time
Analyze playback performance across different sessions
Identify potential issues like rebuffering events
Track bitrate adaptation behavior
Measure and optimize CDN performance
The MCP server provides a structured way to query this data and extract meaningful insights about streaming performance and quality of experience.
