#!/bin/bash

# Count the number of .str and .jrp files in the repository
count_str=$(find . -type f -name "*.str" | wc -l)
count_jrp=$(find . -type f -name "*.jrp" | wc -l)

# Get the total number of files in the repository
total_files=$(find . -type f | wc -l)

# Calculate the percentages
if [[ $total_files -eq 0 ]]; then
    echo "No files found in the repository."
else
    percentage_str=$(echo "scale=2; ($count_str / $total_files) * 100" | bc)
    percentage_jrp=$(echo "scale=2; ($count_jrp / $total_files) * 100" | bc)

    # Create a Markdown file with the statistics
    echo "# File Extension Statistics" > extension_statistics.md
    echo "" >> extension_statistics.md
    echo "File Extension | Percentage" >> extension_statistics.md
    echo "-------------- | ----------" >> extension_statistics.md
    echo ".str           | $percentage_str%" >> extension_statistics.md
    echo ".jrp           | $percentage_jrp%" >> extension_statistics.md

    # Display a message indicating that the statistics have been saved
    echo "Statistics have been saved to extension_statistics.md"
fi