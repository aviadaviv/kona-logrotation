# kona-logrotation

A log rotation utility for Kona applications logs that automatically clears log files at specified intervals.

## Overview

kona-logrotation is a bash script designed to manage log files for Kona applications. It periodically clears log files in the `/usr/kona/*/current/log/` directory, specifically targeting daemon log files. This helps prevent log files from growing too large and consuming excessive disk space.

## Log Retention and Monitoring

The script safely deletes logs because:
- All logs are continuously scraped to Loki every 30 seconds
- Historical logs can be accessed through Grafana
- The minimum safe deletion interval is 1 minute (to ensure all logs are scraped)
- Any deletion interval greater than 1 minute is acceptable

## Features

- Automatically finds and processes log files in `/usr/kona/*/current/log/` directories
- Targets daemon log files specifically
- Configurable sleep interval between rotation cycles
- Detailed logging of operations and any errors encountered
- Safe file handling with existence checks

## Configuration

The script can be configured by modifying the following parameters:

- `SLEEP_TIME`: Controls the interval between log rotation cycles
  - Format: `5m` (minutes), `5h` (hours), or `5d` (days)
  - Default: `2d` (2 days)

## Error Handling

The script includes error handling for:
- Missing log files
- Failed file operations
- Invalid file paths
