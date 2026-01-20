# TeslaFleet v2.0

# Tesla Fleet Monitoring Script

This repository contains a Python script to monitor the usage of Tesla vehicles using the Fleet API. The script fetches and displays usage data for a fleet of 10 Tesla vehicles.

## Table of Contents
- [Introduction](#introduction)
- [Requirements](#requirements)
- [Installation](#installation)
- [Example Python Script](#example-python-script)
- [Example JSON Output](#example-json-output-for-vehicle-1)

## Introduction
This script allows you to extract the usage of Tesla vehicles in your fleet. The usage data includes mileage, battery status, last trip distance, last trip duration, location, charge cycles, and maintenance due status. The output of the script will enable you to use the telemetry data to monitor the usage and the status of the vehicles in the fleet for purposes required by you or your business.

## Requirements
- Python 3.6+
- `requests` library

## Installation

## Example Python Script
```python
import requests
import json

# Define the API endpoint and authentication token
api_endpoint = "https://api.fleet.example.com/vehicles"
auth_token = "YOUR_AUTH_TOKEN"

# Vehicle IDs
vehicle_ids = range(1, 11)  # Vehicle IDs from 1 to 10

def get_vehicle_usage(vehicle_id):
    headers = {
        'Authorization': f'Bearer {auth_token}',
        'Content-Type': 'application/json'
    }
    response = requests.get(f"{api_endpoint}/{vehicle_id}/usage", headers=headers)
    
    if response.status_code == 200:
        return response.json()
    else:
        print(f"Failed to get usage data for vehicle {vehicle_id}: {response.status_code}")
        return None

def monitor_usage():
    for vehicle_id in vehicle_ids:
        usage_data = get_vehicle_usage(vehicle_id)
        
        if usage_data:
            print(f"Vehicle ID: {vehicle_id}")
            print(f"Usage Data: {json.dumps(usage_data, indent=4)}\n")

if __name__ == "__main__":
    monitor_usage()

```


## Example JSON Output for Vehicle 1
```json
{
"Vehicle ID": 1,
"Usage Data": {
"mileage": 12500,
"battery_status": "85%",
"last_trip_distance": "25 miles",
"last_trip_duration": "35 minutes",
"location": "London, UK",
"charge_cycles": 150,
"maintenance_due": false
}


