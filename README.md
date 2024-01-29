
https://usa.visa.com/careers/job-details.jobid.743999772263330.deptid.2641535.html
https://usa.visa.com/careers/job-details.jobid.743999740858315.deptid.1146589.html

#!/bin/bash

cd /rome_spark || exit

# Loop through each subdirectory of /rome_spark
for dir in */ ; do
    echo "Directory: $dir"

    # Initialize arrays to store dates
    dates=()

    # Loop through subdirectories and extract dates
    for subdir in "$dir"*/ ; do
        subdir_name=$(basename "$subdir")
        date=$(echo "$subdir_name" | grep -o '[0-9]\{4\}-[0-9]\{2\}-[0-9]\{2\}')
        dates+=("$date")
    done

    # Sort the dates and output the first and last one
    IFS=$'\n' sorted_dates=($(sort <<<"${dates[*]}"))
    unset IFS

    echo "First Date: ${sorted_dates[0]}"
    echo "Last Date: ${sorted_dates[-1]}"
    echo ""
done