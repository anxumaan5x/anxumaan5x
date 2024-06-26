```python
import csv
from datetime import datetime, timedelta

# Function to generate date ranges
def generate_date_ranges(start_date, end_date):
    current_date = start_date
    date_ranges = []
    while current_date <= end_date:
        week_start = current_date
        week_end = current_date + timedelta(days=4)  # Monday to Friday
        if week_end > end_date:
            week_end = end_date
        date_ranges.append((week_start, week_end))
        current_date += timedelta(days=7)  # Move to next Monday
    return date_ranges

# Function to get alternating contacts
def get_alternating_contacts(length):
    contacts = ['A', 'B', 'C']
    return [contacts[i % 3] for i in range(length)]

# Main function to create CSV
def create_csv(filename, start_date, end_date):
    date_ranges = generate_date_ranges(start_date, end_date)
    contacts = get_alternating_contacts(len(date_ranges))

    with open(filename, mode='w', newline='') as file:
        writer = csv.writer(file)
        writer.writerow(['Date Range', 'Contact'])
        for date_range, contact in zip(date_ranges, contacts):
            writer.writerow([f"{date_range[0].strftime('%d %b %Y')} - {date_range[1].strftime('%d %b %Y')}", contact])

# Define the start and end dates
start_date = datetime.strptime('2024-06-24', '%Y-%m-%d')
end_date = start_date + timedelta(days=90)

# Create the CSV file
create_csv('contact_schedule.csv', start_date, end_date)
```
