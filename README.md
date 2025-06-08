# Uber-Rides-Data-Analysis-
The Uber Rides Data Analysis project focuses on analyzing real-world ride data from Uber, one of the world’s largest ride-sharing platforms. By examining ride patterns, pickup times, locations, and operational efficiency, we can uncover insights into rider behavior, peak times, and geographic ride distributions.
pip install pandas matplotlib seaborn
# Import libraries
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Set plot style
sns.set(style="darkgrid")

# Load dataset
df = pd.read_csv("uber-raw-data-sep14.csv")

# Preview the data
print("First 5 rows of the dataset:")
print(df.head())

# Convert 'Date/Time' to datetime format
df['Date/Time'] = pd.to_datetime(df['Date/Time'])

# Extract useful time-based features
df['Hour'] = df['Date/Time'].dt.hour
df['Day'] = df['Date/Time'].dt.day
df['Weekday'] = df['Date/Time'].dt.dayofweek
df['Month'] = df['Date/Time'].dt.month

# --------------------------------------
# ANALYSIS 1: Trips Per Hour of Day
# --------------------------------------
plt.figure(figsize=(10,5))
sns.countplot(x='Hour', data=df, palette="coolwarm")
plt.title("Uber Trips by Hour")
plt.xlabel("Hour of the Day")
plt.ylabel("Number of Trips")
plt.xticks(range(0, 24))
plt.show()

# --------------------------------------
# ANALYSIS 2: Trips Per Day of the Month
# --------------------------------------
plt.figure(figsize=(10,5))
sns.countplot(x='Day', data=df, palette="viridis")
plt.title("Uber Trips by Day of the Month")
plt.xlabel("Day")
plt.ylabel("Number of Trips")
plt.show()

# --------------------------------------
# ANALYSIS 3: Trips Per Weekday
# --------------------------------------
plt.figure(figsize=(10,5))
sns.countplot(x='Weekday', data=df, palette="Set2")
plt.title("Uber Trips by Weekday (0 = Mon, 6 = Sun)")
plt.xlabel("Weekday")
plt.ylabel("Number of Trips")
plt.xticks(ticks=range(7), labels=['Mon','Tue','Wed','Thu','Fri','Sat','Sun'])
plt.show()

# --------------------------------------
# ANALYSIS 4: Heatmap - Weekday vs Hour
# --------------------------------------
heatmap_data = df.groupby(['Weekday', 'Hour']).size().unstack()
plt.figure(figsize=(12,6))
sns.heatmap(heatmap_data, cmap="YlGnBu")
plt.title("Heatmap of Uber Trips: Weekday vs Hour")
plt.xlabel("Hour of Day")
plt.ylabel("Day of Week")
plt.show()

# --------------------------------------
# ANALYSIS 5: Uber Trips by Base
# --------------------------------------
plt.figure(figsize=(10,5))
sns.countplot(x='Base', data=df, palette="pastel")
plt.title("Uber Trips by Base Station")
plt.xlabel("Base Code")
plt.ylabel("Number of Trips")
plt.show()

# --------------------------------------
# Optional: Trips per Month (if multiple months are available)
# --------------------------------------
# plt.figure(figsize=(10,5))
# sns.countplot(x='Month', data=df, palette="muted")
# plt.title("Uber Trips by Month")
# plt.xlabel("Month")
# plt.ylabel("Number of Trips")
# plt.show()

print("\n✅ Uber Rides Data Analysis Completed.")
