#!/bin/bash

# ==============================================
# Linux File Permissions Hardening Script
# Author: [Your Name]
# Date: June 2026
# Description: This script checks current permissions
# on the /home/researcher2/projects/ directory,
# modifies permissions to enforce Least Privilege,
# and verifies the changes.
# ==============================================

# Step 1: Define the target directory and file
TARGET_DIR="/home/researcher2/projects/"
TARGET_FILE="patient_data.txt"

echo "=============================================="
echo " STARTING PERMISSIONS HARDENING AUDIT"
echo "=============================================="
echo ""

# Step 2: Check current permissions before changes
echo "[1] Checking current permissions for $TARGET_FILE..."
ls -la $TARGET_DIR$TARGET_FILE
echo ""

# Step 3: Analyze the current permissions
# The script checks if the file exists before proceeding.
if [ -f "$TARGET_DIR$TARGET_FILE" ]; then
    echo "[2] File found. Proceeding with permission changes..."
    
    # Step 4: Change permissions using chmod 740
    # Owner (researcher2): Read, Write, Execute (7)
    # Group (research_team): Read only (4)
    # Others: No access (0)
    echo "     Running: sudo chmod 740 $TARGET_DIR$TARGET_FILE"
    sudo chmod 740 $TARGET_DIR$TARGET_FILE
    
    echo "[3] Permissions updated successfully!"
    echo ""
    
    # Step 5: Verify the changes
    echo "[4] Verifying new permissions..."
    ls -la $TARGET_DIR$TARGET_FILE
    echo ""
    
    echo "=============================================="
    echo " AUDIT COMPLETE"
    echo " The file now has restrictive permissions (740)."
    echo " Only the owner ($USER) has full access."
    echo "=============================================="
else
    echo "[ERROR] File $TARGET_DIR$TARGET_FILE not found!"
    echo " Please ensure the file exists before running this script."
    exit 1
fi

# Step 6: Exit successfully
exit 0
