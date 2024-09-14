# River-Water-Quality-Monitor-

import random
import csv
import os
import matplotlib.pyplot as plt
from tabulate import tabulate

# Cities through which the Yamuna River flows
cities = ["CityA", "CityB", "CityC", "CityD"]

# Pollution level categories
def categorize_pollution(pollution_level):
    if pollution_level <= 20:
        return "Normal"
    elif pollution_level <= 40:
        return "Medium"
    elif pollution_level <= 60:
        return "Alarming"
    elif pollution_level <= 80:
        return "Urgent Clean Required"
    else:
        return "Poisonous"

# Simulating pollution data collection (in arbitrary pollution index units)
def get_pollution_data(city):
    return round(random.uniform(0, 100), 2)  # Simulate pollution levels between 0 and 100

# Checking if industrial waste meets guidelines (assumed threshold for demonstration)
def check_waste_compliance(city, pollution_level, threshold=50):
    if pollution_level > threshold:
        return f"Non-compliant waste management in {city} (Pollution: {pollution_level})"
    else:
        return f"Compliant waste management in {city} (Pollution: {pollution_level})"

# Function to log data into a CSV file
def log_data_to_csv(data, filename='pollution_data.csv'):
    file_exists = os.path.isfile(filename)

    with open(filename, mode='a', newline='') as file:
        writer = csv.writer(file)
        
        # Write header only if file does not already exist
        if not file_exists:
            writer.writerow(["City", "Pollution Level", "Category"])
        
        for city, (pollution_level, category) in data.items():
            writer.writerow([city, pollution_level, category])

# Collecting pollution data for each city
pollution_data = {}
for city in cities:
    pollution_level = get_pollution_data(city)
    category = categorize_pollution(pollution_level)
    pollution_data[city] = (pollution_level, category)

# Display data in a tabular format
def display_data_table(data):
    table = []
    for city, (pollution_level, category) in data.items():
        table.append([city, pollution_level, category])
    
    headers = ["City", "Pollution Level", "Category"]
    print("\nPollution Data Table:")
    print(tabulate(table, headers=headers, tablefmt="grid"))

# Simulating data being sent to the server via 5G (pseudo-server update)
def send_data_to_server(data):
    # Simulate sending data to the server
    print("\nSending data to server...")
    print("Data sent successfully!\n")
    return True

# Plotting pollution level comparisons across cities
def plot_pollution_comparison(data):
    cities = list(data.keys())
    pollution_levels = [item[0] for item in data.values()]

    plt.bar(cities, pollution_levels, color='blue')
    plt.xlabel('Cities')
    plt.ylabel('Pollution Levels')
    plt.title('Pollution Level Comparison Across Cities')
    plt.show()

# Main flow of data monitoring and comparison
def main():
    print("\nYamuna River Pollution Monitoring System\n")
    
    # Display data in tabular form
    display_data_table(pollution_data)
    
    # Log data to CSV
    log_data_to_csv(pollution_data)
    print("Pollution data has been logged to CSV.")

    # Send data to server
    if send_data_to_server(pollution_data):
        # Plot comparison after data is sent
        plot_pollution_comparison(pollution_data)

if __name__ == "__main__":
    main()
