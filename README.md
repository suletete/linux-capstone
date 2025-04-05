
```bash
#!/bin/bash

# Function to generate the multiplication table in ascending order using list form for loop
generate_multiplication_table_list_form() {
    local number=$1
    echo "Multiplication Table for $number (Ascending Order):"
    for i in {1..10}; do
        echo "$number x $i = $((number * i))"
    done
}

# Function to generate the multiplication table in descending order using list form for loop
generate_multiplication_table_descending_list_form() {
    local number=$1
    echo "Multiplication Table for $number (Descending Order):"
    for i in {10..1}; do
        echo "$number x $i = $((number * i))"
    done
}

# Function to generate the multiplication table using C-style for loop
generate_multiplication_table_c_style() {
    local number=$1
    echo "Multiplication Table for $number (C-Style Loop):"
    for ((i=1; i<=10; i++)); do
        echo "$number x $i = $((number * i))"
    done
}

# Function to generate the multiplication table in descending order using C-style for loop
generate_multiplication_table_descending_c_style() {
    local number=$1
    echo "Multiplication Table for $number (Descending Order with C-Style Loop):"
    for ((i=10; i>=1; i--)); do
        echo "$number x $i = $((number * i))"
    done
}

# Ask the user for the number
read -p "Enter a number for the multiplication table: " number

# Validate if the input is a valid number
if ! [[ "$number" =~ ^[0-9]+$ ]]; then
    echo "Invalid input! Please enter a valid number."
    exit 1
fi

# Ask the user if they want a full table or a partial table
read -p "Do you want a full table or a partial table? (Enter 'f' for full, 'p' for partial): " choice

# Full table (1 to 10)
if [[ "$choice" == "f" ]]; then
    # Ask the user if they want ascending or descending order
    read -p "Do you want the table in ascending or descending order? (Enter 'a' for ascending, 'd' for descending): " order

    if [[ "$order" == "a" ]]; then
        # Generate the table using list form loop in ascending order
        generate_multiplication_table_list_form $number
    elif [[ "$order" == "d" ]]; then
        # Generate the table using list form loop in descending order
        generate_multiplication_table_descending_list_form $number
    else
        echo "Invalid input for order. Defaulting to ascending order."
        generate_multiplication_table_list_form $number
    fi

# Partial table (user-defined range)
elif [[ "$choice" == "p" ]]; then
    # Ask for the start and end numbers for the partial table
    read -p "Enter the starting number (between 1 and 10): " start
    read -p "Enter the ending number (between 1 and 10): " end

    # Validate the range
    if ! [[ "$start" =~ ^[0-9]+$ ]] || ! [[ "$end" =~ ^[0-9]+$ ]]; then
        echo "Invalid input! Please enter valid numbers for the range."
        exit 1
    fi

    if [[ "$start" -gt "$end" ]]; then
        echo "Invalid range! Starting number must be less than or equal to the ending number. Showing full table instead."
        generate_multiplication_table_list_form $number
    else
        echo "The partial multiplication table for $number from $start to $end:"
        for ((i=$start; i<=$end; i++)); do
            echo "$number x $i = $((number * i))"
        done
    fi

else
    echo "Invalid input for table choice. Please enter 'f' for full or 'p' for partial."
    exit 1
fi

# Now, generate the multiplication table using the C-style loop
echo -e "\nUsing C-Style Loop:"
generate_multiplication_table_c_style $number

# Ask if the user wants to see the table in descending order using C-style loop
read -p "Do you want to see the table in descending order with C-style loop? (y/n): " desc_choice

if [[ "$desc_choice" == "y" ]]; then
    generate_multiplication_table_descending_c_style $number
else
    echo "Exiting script. Thank you!"
fi
```

### Breakdown of the script:
1. **User Input for Number**: 
   - The script prompts the user to enter a number for the multiplication table.
   - It validates the input to ensure the user enters a valid number (using regular expressions).

2. **Choice of Full or Partial Table**:
   - The user is prompted to choose between a full table (1 to 10) or a partial table. If the user chooses a partial table, they are then asked to provide a start and end number for the range.
   - If the user provides an invalid range (e.g., start > end), the script defaults to displaying the full table.

3. **Using Loops to Generate the Table**:
   - **List Form Loop**: The script uses a list form loop to display the multiplication table in both ascending and descending order.
   - **C-Style Loop**: The script also generates the table using a C-style `for` loop for comparison.

4. **Order of Output**:
   - After choosing between ascending and descending, the script generates the table accordingly.
   - If the user chooses "full", the table is displayed for numbers 1 to 10.
   - If the user opts for a partial table, the table is generated within the specified range.

5. **Bonus Feature**:
   - The user is given the option to generate the multiplication table in descending order using the C-style loop.

### Example output:

**Full Table, Ascending Order**:
```
Enter a number for the multiplication table: 3
Do you want a full table or a partial table? (Enter 'f' for full, 'p' for partial): f
Do you want the table in ascending or descending order? (Enter 'a' for ascending, 'd' for descending): a
Multiplication Table for 3 (Ascending Order):
3 x 1 = 3
3 x 2 = 6
3 x 3 = 9
3 x 4 = 12
3 x 5 = 15
3 x 6 = 18
3 x 7 = 21
3 x 8 = 24
3 x 9 = 27
3 x 10 = 30
```

**Partial Table**:
```
Enter a number for the multiplication table: 3
Do you want a full table or a partial table? (Enter 'f' for full, 'p' for partial): p
Enter the starting number (between 1 and 10): 2
Enter the ending number (between 1 and 10): 4
The partial multiplication table for 3 from 2 to 4:
3 x 2 = 6
3 x 3 = 9
3 x 4 = 12
```

### Final Notes:
- **Error Handling**: The script handles invalid user inputs (e.g., invalid range or non-numeric input) and provides feedback.
- **User Interaction**: The user is given multiple options to customize the output, such as choosing ascending or descending order.
