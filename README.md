# Capstone-Project-Linux-Shell-Scripting-

Linux Shell Scripting Capstone Project: Multiplication Table Generator
Project Overview
This document provides a comprehensive guide to the Linux Shell Scripting Capstone Project. You will create a Bash script that generates a multiplication table for a number entered by the user. This project reinforces essential Bash scripting concepts, including loops, user input handling, conditional logic, and input validation.

Table of Contents
Project Description

Learning Objectives

Project Requirements

Script Architecture

Part 1: List Form For Loop

Part 2: C-Style For Loop

Part 3: Enhanced Version with Full/Partial Table

Part 4: Bonus Features

Complete Script Examples

Assessment Criteria

Testing and Validation

Troubleshooting Guide

Git Commands for Submission

Project Description
Your script should prompt the user to enter a number and then ask if they prefer to see a full multiplication table from 1 to 10 or a partial table within a specified range. Based on the user's choice, the script will display the corresponding multiplication table.

https://www.tutorialspoint.com/unix/images/loops.jpg
Figure 1: Bash loop structures used in this project

Learning Objectives
By completing this project, you will:

✅ Understand how to use variables to store user inputs and use them in calculations
✅ Learn the syntax and use cases of both list form and C-style for loops
✅ Practice using loops to automate repetitive tasks
✅ Enhance script interactivity with user input and clear output formatting
✅ Implement input validation and error handling
✅ Create well-commented and readable code

Project Requirements
Requirement	Description
User Input	Prompt user to enter a number for the multiplication table
Table Range Choice	Ask if user wants full table (1-10) or partial table (specific range)
Loops	Implement using both list form and C-style for loops
Conditional Logic	Use if-else statements for handling user choices
Input Validation	Validate numbers and ranges, provide feedback for invalid inputs
Readable Output	Display table in clear, formatted output
Comments	Well-commented code explaining purpose and logic
Script Architecture
Basic Structure
text
┌─────────────────────────────────────┐
│         START SCRIPT                │
└─────────────────────────────────────┘
              │
              ▼
┌─────────────────────────────────────┐
│  1. Prompt for Number               │
│     - Read user input               │
│     - Validate input                │
└─────────────────────────────────────┘
              │
              ▼
┌─────────────────────────────────────┐
│  2. Prompt for Table Type           │
│     - Full (1-10)                   │
│     - Partial (range)               │
└─────────────────────────────────────┘
              │
              ▼
┌─────────────────────────────────────┐
│  3. Generate Table                  │
│     - Using List Form Loop          │
│     - Using C-Style Loop            │
└─────────────────────────────────────┘
              │
              ▼
┌─────────────────────────────────────┐
│  4. Display Results                 │
│     - Formatted output              │
│     - Error messages if invalid     │
└─────────────────────────────────────┘
              │
              ▼
┌─────────────────────────────────────┐
│  5. Repeat or Exit (Bonus)          │
└─────────────────────────────────────┘
Part 1: List Form For Loop
The list form for loop iterates over a list of values. This is the most common and readable form in Bash.

Syntax
bash
for variable in list
do
    commands
done
Implementation
bash
#!/bin/bash

# ==========================================
# PART 1: Using List Form For Loop
# ==========================================

# Prompt user for a number
echo "====================================="
echo "   MULTIPLICATION TABLE GENERATOR"
echo "====================================="
echo -n "Enter a number: "
read number

# Validate input is a number
if ! [[ "$number" =~ ^[0-9]+$ ]]; then
    echo "Error: Please enter a valid positive integer."
    exit 1
fi

echo ""
echo "=== Multiplication Table for $number (List Form) ==="
echo ""

# Using List Form for loop
for i in 1 2 3 4 5 6 7 8 9 10
do
    result=$((number * i))
    echo "$number × $i = $result"
done
Sample Output
text
=====================================
   MULTIPLICATION TABLE GENERATOR
=====================================
Enter a number: 3

=== Multiplication Table for 3 (List Form) ===

3 × 1 = 3
3 × 2 = 6
3 × 3 = 9
3 × 4 = 12
3 × 5 = 15
3 × 6 = 18
3 × 7 = 21
3 × 8 = 24
3 × 9 = 27
3 × 10 = 30
Using Sequence Expansion
A more concise way to write the list form:

bash
# Using brace expansion
for i in {1..10}
do
    result=$((number * i))
    echo "$number × $i = $result"
done

# Or using seq command
for i in $(seq 1 10)
do
    result=$((number * i))
    echo "$number × $i = $result"
done
https://www.golinuxcloud.com/wp-content/uploads/bash-for-loop.jpg
Figure 2: Bash for loop syntax and structure

Part 2: C-Style For Loop
The C-style for loop uses a syntax similar to C programming language, offering more control over the iteration process.

Syntax
bash
for (( initialization; condition; increment ))
do
    commands
done
Implementation
bash
#!/bin/bash

# ==========================================
# PART 2: Using C-Style For Loop
# ==========================================

# Prompt user for a number
echo -n "Enter a number: "
read number

# Validate input
if ! [[ "$number" =~ ^[0-9]+$ ]]; then
    echo "Error: Please enter a valid positive integer."
    exit 1
fi

echo ""
echo "=== Multiplication Table for $number (C-Style Loop) ==="
echo ""

# Using C-Style for loop
for (( i=1; i<=10; i++ ))
do
    result=$((number * i))
    echo "$number × $i = $result"
done
Comparison: List Form vs C-Style
Feature	List Form	C-Style
Syntax	for i in {1..10}	for (( i=1; i<=10; i++ ))
Readability	Very readable	More complex
Control	Iterates over list	Full control over initialization, condition, increment
Use Case	Simple iterations	Complex iterations with custom step values
Flexibility	Limited to list values	Can use any arithmetic expression
C-Style with Custom Step
bash
# Count by 2s (even numbers only)
for (( i=2; i<=10; i+=2 ))
do
    result=$((number * i))
    echo "$number × $i = $result"
done
Part 3: Enhanced Version with Full/Partial Table
This enhanced version combines all requirements with user choice and input validation.

Complete Script
bash
#!/bin/bash

# ===============================================================
# MULTIPLICATION TABLE GENERATOR - ENHANCED VERSION
# 
# This script generates a multiplication table for a user-specified
# number with options for full or partial table display.
# ===============================================================

# Function to display the header
display_header() {
    echo ""
    echo "╔══════════════════════════════════════════════════════╗"
    echo "║         MULTIPLICATION TABLE GENERATOR             ║"
    echo "║              (Enhanced Version)                    ║"
    echo "╚══════════════════════════════════════════════════════╝"
    echo ""
}

# Function to validate if input is a positive integer
validate_number() {
    local input=$1
    if ! [[ "$input" =~ ^[0-9]+$ ]] || [ "$input" -lt 1 ]; then
        return 1
    fi
    return 0
}

# Function to generate table using list form
generate_list_form() {
    local num=$1
    local start=$2
    local end=$3
    
    echo ""
    echo "=== Using List Form For Loop ==="
    echo ""
    
    # Using brace expansion for clean list
    for i in $(seq $start $end)
    do
        result=$((num * i))
        printf "  %2d × %2d = %3d\n" "$num" "$i" "$result"
    done
}

# Function to generate table using C-style loop
generate_cstyle_form() {
    local num=$1
    local start=$2
    local end=$3
    
    echo ""
    echo "=== Using C-Style For Loop ==="
    echo ""
    
    # C-style for loop with custom range
    for (( i=start; i<=end; i++ ))
    do
        result=$((num * i))
        printf "  %2d × %2d = %3d\n" "$num" "$i" "$result"
    done
}

# Main script starts here
display_header

# ===========================================================
# STEP 1: Get the number from user
# ===========================================================
while true; do
    echo -n "Enter a number for the multiplication table: "
    read number
    
    if validate_number "$number"; then
        break
    else
        echo "❌ Error: Please enter a valid positive integer (1, 2, 3, ...)."
        echo ""
    fi
done

echo ""
echo "✅ Number accepted: $number"

# ===========================================================
# STEP 2: Ask for table type
# ===========================================================
while true; do
    echo ""
    echo "Do you want:"
    echo "  1. Full table (1 to 10)"
    echo "  2. Partial table (custom range)"
    echo ""
    echo -n "Enter your choice (1 or 2): "
    read choice
    
    if [[ "$choice" == "1" ]]; then
        start=1
        end=10
        table_type="full"
        break
    elif [[ "$choice" == "2" ]]; then
        # Get range from user
        echo ""
        echo "Enter the range (between 1 and 10):"
        
        # Get start
        while true; do
            echo -n "  Starting number: "
            read start
            if validate_number "$start" && [ "$start" -le 10 ]; then
                break
            else
                echo "  ❌ Please enter a number between 1 and 10."
            fi
        done
        
        # Get end
        while true; do
            echo -n "  Ending number: "
            read end
            if validate_number "$end" && [ "$end" -le 10 ]; then
                break
            else
                echo "  ❌ Please enter a number between 1 and 10."
            fi
        done
        
        # Validate range
        if [ "$start" -gt "$end" ]; then
            echo ""
            echo "⚠️  Invalid range detected (start > end)."
            echo "   Defaulting to full table (1 to 10)."
            start=1
            end=10
            table_type="full (default)"
        else
            table_type="partial ($start to $end)"
        fi
        break
    else
        echo "❌ Invalid choice. Please enter 1 or 2."
    fi
done

# ===========================================================
# STEP 3: Display the table
# ===========================================================
echo ""
echo "════════════════════════════════════════════════════════"
echo "  🎯 Multiplication Table for: $number"
echo "  📊 Table Type: $table_type"
echo "════════════════════════════════════════════════════════"

# Generate with both loop styles for comparison
generate_list_form "$number" "$start" "$end"
generate_cstyle_form "$number" "$start" "$end"

# ===========================================================
# STEP 4: Summary
# ===========================================================
echo ""
echo "════════════════════════════════════════════════════════"
echo "  ✅ Table generation complete!"
echo "  📝 Total calculations: $((end - start + 1))"
echo "════════════════════════════════════════════════════════"
echo ""
Sample Outputs
Full Table Example:
text
╔══════════════════════════════════════════════════════╗
║         MULTIPLICATION TABLE GENERATOR             ║
║              (Enhanced Version)                    ║
╚══════════════════════════════════════════════════════╝

Enter a number for the multiplication table: 3
✅ Number accepted: 3

Do you want:
  1. Full table (1 to 10)
  2. Partial table (custom range)

Enter your choice (1 or 2): 1

════════════════════════════════════════════════════════
  🎯 Multiplication Table for: 3
  📊 Table Type: full
════════════════════════════════════════════════════════

=== Using List Form For Loop ===

   3 ×  1 =   3
   3 ×  2 =   6
   3 ×  3 =   9
   3 ×  4 =  12
   3 ×  5 =  15
   3 ×  6 =  18
   3 ×  7 =  21
   3 ×  8 =  24
   3 ×  9 =  27
   3 × 10 =  30

=== Using C-Style For Loop ===

   3 ×  1 =   3
   3 ×  2 =   6
   3 ×  3 =   9
   3 ×  4 =  12
   3 ×  5 =  15
   3 ×  6 =  18
   3 ×  7 =  21
   3 ×  8 =  24
   3 ×  9 =  27
   3 × 10 =  30

════════════════════════════════════════════════════════
  ✅ Table generation complete!
  📝 Total calculations: 10
════════════════════════════════════════════════════════
Partial Table Example:
text
Enter a number for the multiplication table: 3
✅ Number accepted: 3

Do you want:
  1. Full table (1 to 10)
  2. Partial table (custom range)

Enter your choice (1 or 2): 2

Enter the range (between 1 and 10):
  Starting number: 2
  Ending number: 4

════════════════════════════════════════════════════════
  🎯 Multiplication Table for: 3
  📊 Table Type: partial (2 to 4)
════════════════════════════════════════════════════════

=== Using List Form For Loop ===

   3 ×  2 =   6
   3 ×  3 =   9
   3 ×  4 =  12

=== Using C-Style For Loop ===

   3 ×  2 =   6
   3 ×  3 =   9
   3 ×  4 =  12

════════════════════════════════════════════════════════
  ✅ Table generation complete!
  📝 Total calculations: 3
════════════════════════════════════════════════════════
Invalid Range Handling:
text
Enter a number for the multiplication table: 3
✅ Number accepted: 3

Do you want:
  1. Full table (1 to 10)
  2. Partial table (custom range)

Enter your choice (1 or 2): 2

Enter the range (between 1 and 10):
  Starting number: 8
  Ending number: 2

⚠️  Invalid range detected (start > end).
   Defaulting to full table (1 to 10).

════════════════════════════════════════════════════════
  🎯 Multiplication Table for: 3
  📊 Table Type: full (default)
════════════════════════════════════════════════════════
  [Full table displayed...]
Part 4: Bonus Features
Bonus 1: Ascending or Descending Order
Ask the user if they want the table in ascending or descending order.

bash
#!/bin/bash

# ==========================================
# BONUS: Ascending/Descending Order
# ==========================================

# Ask for order preference
echo ""
echo "Display order:"
echo "  1. Ascending (1 to 10)"
echo "  2. Descending (10 to 1)"
echo -n "Enter your choice (1 or 2): "
read order

# Determine loop direction
if [ "$order" == "1" ]; then
    # Ascending
    for i in {1..10}
    do
        result=$((number * i))
        echo "$number × $i = $result"
    done
elif [ "$order" == "2" ]; then
    # Descending
    for (( i=10; i>=1; i-- ))
    do
        result=$((number * i))
        echo "$number × $i = $result"
    done
else
    echo "Invalid choice. Defaulting to ascending."
fi
Bonus 2: Repeat Program Option
Allow users to generate tables for multiple numbers without restarting.

bash
#!/bin/bash

# ==========================================
# BONUS: Repeat Program
# ==========================================

while true; do
    # [Main script logic here]
    
    # Ask if user wants to continue
    echo ""
    echo -n "Generate another table? (y/n): "
    read continue_choice
    
    if [[ "$continue_choice" != "y" && "$continue_choice" != "Y" ]]; then
        echo ""
        echo "Thank you for using the Multiplication Table Generator!"
        echo "Goodbye! 👋"
        break
    fi
    echo ""
done
Bonus 3: Creative Display Options
Offer different formatting styles for the table display.

bash
#!/bin/bash

# ==========================================
# BONUS: Display Format Options
# ==========================================

display_formatted_table() {
    local num=$1
    local start=$2
    local end=$3
    local format=$4
    
    echo ""
    case $format in
        1)  # Simple format
            echo "Simple Format:"
            echo "---------------"
            for i in $(seq $start $end); do
                echo "$num x $i = $((num * i))"
            done
            ;;
        2)  # Boxed format
            echo "Boxed Format:"
            echo "┌─────────────┐"
            for i in $(seq $start $end); do
                printf "│ %2d x %2d = %3d │\n" "$num" "$i" "$((num * i))"
            done
            echo "└─────────────┘"
            ;;
        3)  # Table format
            echo "Table Format:"
            echo "──────────────"
            printf "  Number  │  Multiplier  │  Result  \n"
            echo "──────────┼──────────────┼──────────"
            for i in $(seq $start $end); do
                printf "  %6d  │  %10d  │  %6d  \n" "$num" "$i" "$((num * i))"
            done
            echo "──────────┴──────────────┴──────────"
            ;;
        *)
            echo "Invalid format. Using simple format."
            ;;
    esac
}

# Usage in main script
echo "Choose display format:"
echo "  1. Simple"
echo "  2. Boxed"
echo "  3. Table"
echo -n "Enter choice: "
read format_choice

display_formatted_table "$number" "$start" "$end" "$format_choice"
Complete Script Examples
Script 1: Basic Implementation
This is the simplest version meeting all core requirements.

bash
#!/bin/bash

# ==========================================
# BASIC MULTIPLICATION TABLE GENERATOR
# ==========================================

# Prompt for number
echo -n "Enter a number: "
read number

# Validate input
if ! [[ "$number" =~ ^[0-9]+$ ]]; then
    echo "Error: Invalid input. Please enter a number."
    exit 1
fi

echo ""
echo "Multiplication table for $number:"
echo ""

# Part 1: List Form
echo "--- Using List Form For Loop ---"
for i in 1 2 3 4 5 6 7 8 9 10
do
    echo "$number × $i = $((number * i))"
done

echo ""

# Part 2: C-Style Form
echo "--- Using C-Style For Loop ---"
for (( i=1; i<=10; i++ ))
do
    echo "$number × $i = $((number * i))"
done
Script 2: Advanced Implementation with All Features
bash
#!/bin/bash

# ===============================================================
# ADVANCED MULTIPLICATION TABLE GENERATOR
# 
# Features:
#   - Full and partial table support
#   - Input validation
#   - Both loop styles
#   - Ascending/descending order
#   - Repeat option
#   - Colorful output (ANSI)
# ===============================================================

# Colors for output
RED='\033[0;31m'
GREEN='\033[0;32m'
YELLOW='\033[1;33m'
BLUE='\033[0;34m'
PURPLE='\033[0;35m'
CYAN='\033[0;36m'
NC='\033[0m' # No Color

# Welcome header
echo -e "${CYAN}"
echo "╔═══════════════════════════════════════════════════════════╗"
echo "║     MULTIPLICATION TABLE GENERATOR - ADVANCED v2.0      ║"
echo "║          Your Ultimate Bash Scripting Practice          ║"
echo "╚═══════════════════════════════════════════════════════════╝"
echo -e "${NC}"

# Function to display colored table
display_table() {
    local num=$1
    local start=$2
    local end=$3
    local loop_type=$4
    local order=$5
    
    echo -e "\n${YELLOW}=== ${loop_type} For Loop ${NC}(${order} order)${YELLOW} ==="
    echo -e "${NC}"
    
    if [[ "$order" == "ascending" ]]; then
        for (( i=start; i<=end; i++ ))
        do
            result=$((num * i))
            if (( result % 2 == 0 )); then
                printf "${GREEN}  %2d × %2d = %3d${NC}\n" "$num" "$i" "$result"
            else
                printf "${BLUE}  %2d × %2d = %3d${NC}\n" "$num" "$i" "$result"
            fi
        done
    else
        for (( i=end; i>=start; i-- ))
        do
            result=$((num * i))
            if (( result % 2 == 0 )); then
                printf "${GREEN}  %2d × %2d = %3d${NC}\n" "$num" "$i" "$result"
            else
                printf "${BLUE}  %2d × %2d = %3d${NC}\n" "$num" "$i" "$result"
            fi
        done
    fi
}

# Main loop for repeated use
while true; do
    # Get number
    while true; do
        echo -n -e "${YELLOW}Enter a number: ${NC}"
        read number
        
        if [[ "$number" =~ ^[0-9]+$ ]] && [ "$number" -gt 0 ]; then
            echo -e "${GREEN}✅ Number accepted: $number${NC}"
            break
        else
            echo -e "${RED}❌ Error: Please enter a positive integer.${NC}"
        fi
    done
    
    # Get table type
    echo ""
    echo "Select table type:"
    echo "  1. Full table (1-10)"
    echo "  2. Partial table (custom range)"
    echo -n "Enter choice (1-2): "
    read choice
    
    if [[ "$choice" == "1" ]]; then
        start=1
        end=10
        table_label="Full (1-10)"
    elif [[ "$choice" == "2" ]]; then
        echo ""
        echo "Enter range (between 1 and 10):"
        
        while true; do
            echo -n "  Start: "
            read start
            if [[ "$start" =~ ^[0-9]+$ ]] && [ "$start" -ge 1 ] && [ "$start" -le 10 ]; then
                break
            else
                echo -e "${RED}  Please enter 1-10${NC}"
            fi
        done
        
        while true; do
            echo -n "  End: "
            read end
            if [[ "$end" =~ ^[0-9]+$ ]] && [ "$end" -ge 1 ] && [ "$end" -le 10 ]; then
                break
            else
                echo -e "${RED}  Please enter 1-10${NC}"
            fi
        done
        
        if [ "$start" -gt "$end" ]; then
            echo -e "${YELLOW}⚠️  Invalid range. Using full table.${NC}"
            start=1
            end=10
            table_label="Full (default)"
        else
            table_label="Partial ($start-$end)"
        fi
    else
        echo -e "${RED}Invalid choice. Using full table.${NC}"
        start=1
        end=10
        table_label="Full (default)"
    fi
    
    # Get order preference
    echo ""
    echo "Display order:"
    echo "  1. Ascending"
    echo "  2. Descending"
    echo -n "Enter choice (1-2): "
    read order_choice
    
    if [[ "$order_choice" == "2" ]]; then
        order="descending"
    else
        order="ascending"
    fi
    
    # Display results
    echo ""
    echo -e "${CYAN}════════════════════════════════════════════════════════${NC}"
    echo -e "${PURPLE}  🎯 Multiplication Table for: ${GREEN}$number${NC}"
    echo -e "${PURPLE}  📊 Table Type: ${GREEN}$table_label${NC}"
    echo -e "${PURPLE}  📈 Order: ${GREEN}$order${NC}"
    echo -e "${CYAN}════════════════════════════════════════════════════════${NC}"
    
    # Generate with list form
    display_table "$number" "$start" "$end" "List" "$order"
    
    # Generate with C-style
    display_table "$number" "$start" "$end" "C-Style" "$order"
    
    # Summary
    echo ""
    echo -e "${CYAN}════════════════════════════════════════════════════════${NC}"
    echo -e "${GREEN}✅ Table generation complete!${NC}"
    echo -e "${GREEN}📝 Total calculations: $((end - start + 1))${NC}"
    echo -e "${CYAN}════════════════════════════════════════════════════════${NC}"
    
    # Ask to continue
    echo ""
    echo -n "Generate another table? (y/n): "
    read continue_choice
    
    if [[ "$continue_choice" != "y" && "$continue_choice" != "Y" ]]; then
        echo ""
        echo -e "${PURPLE}Thank you for using the Multiplication Table Generator!${NC}"
        echo -e "${GREEN}Happy coding! 🚀${NC}"
        break
    fi
    echo ""
done
Assessment Criteria
Your project will be graded based on the following criteria:

Criteria	Weight	Description
Correctness and Functionality	20%	Script works correctly, no syntax errors
Implementation and Use of Loops	20%	Both loop styles implemented correctly
Code Quality and Readability	20%	Well-commented, properly formatted, logical structure
Input Validation and Error Handling	20%	Validates all inputs, handles errors gracefully
User Interaction and Presentation	20%	Clear prompts, formatted output, user-friendly
Bonus Points
Bonus Feature	Points
Ascending/descending order	+5
Repeat program option	+5
Creative display options	+5
Colorful output	+3
Additional features	+2
Testing and Validation
Test Cases
Test Case	Input	Expected Output
Valid number	5	Table for 5 displayed
Invalid number	abc	Error message
Full table	1	10 rows displayed
Partial table (valid)	start=2, end=4	3 rows displayed
Partial table (invalid)	start=8, end=2	Full table displayed
Ascending order	3, ascending	1 to 10 order
Descending order	3, descending	10 to 1 order
Running Tests
bash
# Test the script
./multiplication_table.sh

# Test with invalid input
echo "" | ./multiplication_table.sh

# Test with range
echo -e "3\n2\n2\n4" | ./multiplication_table.sh
Troubleshooting Guide
Common Issues and Solutions
Issue	Solution
Permission denied	chmod +x multiplication_table.sh
Syntax error near unexpected token	Check for missing spaces around brackets
Command not found	Ensure script is in correct path or use ./script.sh
Invalid number validation fails	Check regex pattern ^[0-9]+$
Loop not executing	Verify conditions and variable values
Debugging Tips
bash
# Enable debug mode
bash -x multiplication_table.sh

# Check for syntax errors
bash -n multiplication_table.sh

# Add debugging statements
set -x
# [code here]
set +x
Git Commands for Submission
bash
# Initialize Git repository
git init

# Create script file
touch multiplication_table.sh

# Make script executable
chmod +x multiplication_table.sh

# Add to staging
git add multiplication_table.sh

# Commit with message
git commit -m "Add multiplication table generator script"

# Add remote repository
git remote add origin https://github.com/your-username/multiplication-table.git

# Push to remote
git push -u origin main

# Tag your submission
git tag -a v1.0 -m "Complete multiplication table generator"
git push origin v1.0
Additional Resources
Bash Documentation

Bash For Loop Tutorial

Bash Conditional Expressions

Shell Scripting Best Practices

Conclusion
Congratulations on completing the Linux Shell Scripting Capstone Project! You have successfully created a fully functional multiplication table generator that demonstrates:

✅ User input handling and validation
✅ Both list form and C-style for loops
✅ Conditional logic with if-else statements
✅ Professional code organization and commenting
✅ Interactive and user-friendly output

This project has given me practical experience with Bash scripting, an essential skill for DevOps, system administration, and automation roles.
