
https://usa.visa.com/careers/job-details.jobid.743999772263330.deptid.2641535.html
https://usa.visa.com/careers/job-details.jobid.743999740858315.deptid.1146589.html

import pandas as pd

# File paths
input_filename = 'output.txt'
output_filename = 'output.csv'

# Initialize lists to store data
directories = []
first_dates = []
last_dates = []

# Read and process the input file
with open(input_filename, 'r') as file:
    for line in file:
        if 'Directory:' in line:
            dir_name = line.split('Directory:')[1].strip().rstrip('/')
            directories.append(dir_name)
        elif 'First Date:' in line:
            first_date = line.split('First Date:')[1].strip()
            first_dates.append(first_date)
        elif 'Last Date:' in line:
            last_date = line.split('Last Date:')[1].strip()
            last_dates.append(last_date)

# Create a DataFrame
df = pd.DataFrame({
    'Directory': directories,
    'First Date': first_dates,
    'Last Date': last_dates
})

# Save the DataFrame to a CSV file
df.to_csv(output_filename, index=False)

print(f"Data has been written to {output_filename}")