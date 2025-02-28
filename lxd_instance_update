#!/bin/bash

# ==================================================
# LXD Container Update & Upgrade Script
# Copyright (c) 2025 Kim Tholstorf
# All rights reserved.
# 
# This script updates and upgrades all running LXD containers.
# Use at your own risk. Ensure you have backups before running.
# ==================================================

# Define color codes using printf-compatible escape sequences
GREEN=$(printf '\033[32m')
YELLOW=$(printf '\033[33m')
BLUE=$(printf '\033[34m')
RESET=$(printf '\033[0m')

# Get a list of all running LXC containers
running_containers=$(lxc list --format csv -c n,s | awk -F, '$2=="RUNNING" {print $1}')

# Display a header
printf "%b=========================================%b\n" "$BLUE" "$RESET"
printf "%b LXD Container Update & Upgrade Script %b\n" "$GREEN" "$RESET"
printf "%b=========================================%b\n\n" "$BLUE" "$RESET"

printf "%bThe following containers will be updated:%b\n" "$YELLOW" "$RESET"
printf "%b-----------------------------------------%b\n" "$BLUE" "$RESET"
printf "%s\n" "$running_containers"
printf "%b-----------------------------------------%b\n\n" "$BLUE" "$RESET"

printf "%bStarting updates...%b\n\n" "$GREEN" "$RESET"

# Loop through each running container and run apt update (no output) & upgrade (minimal output)
for container in $running_containers; do
    printf "\n%bUpdating and upgrading container: %s%b\n" "$YELLOW" "$container" "$RESET"
    printf "%b-----------------------------------------%b\n" "$BLUE" "$RESET"
    lxc exec "$container" -- bash -c "DEBIAN_FRONTEND=noninteractive apt update -qq -y > /dev/null 2>&1 && apt upgrade -qq -y"
    printf "%bFinished updating %s%b\n" "$GREEN" "$container" "$RESET"
done

printf "\n%bAll running containers updated successfully.%b\n" "$GREEN" "$RESET"
