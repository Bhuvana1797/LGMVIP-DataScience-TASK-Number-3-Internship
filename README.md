This project focuses on Exploratory Data Analysis (EDA) of a terrorism dataset to identify "hot zones" of terrorist activities. The goal is to uncover patterns and trends in terrorist incidents to aid in security and defense strategies.

import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

df=pd.read_csv('/content/terrorism new.csv', encoding='latin-1')

# Display the first few rows of the dataset to verify it's loaded correctly
print("First few rows of the dataset:")
print(df.head())

# Display the first few rows of the dataset to verify it's loaded correctly
print("First few rows of the dataset:")
print(df.head())

# Calculate total fatalities and injuries per country
country_impact = df.groupby('Country')[['Fatalities', 'Injuries']].sum()
print("\nTotal fatalities and injuries per country:")
print(country_impact)

# Plotting total fatalities and injuries per country
plt.figure(figsize=(16, 10))  # Increased figure size
ax = country_impact.plot(kind='bar', stacked=True, figsize=(16, 10))
plt.title('Total Fatalities and Injuries per Country', fontsize=16)
plt.xlabel('Country', fontsize=14)
plt.ylabel('Count', fontsize=14)
plt.xticks(rotation=60, ha='right', fontsize=12)  # Rotate x-axis labels and align them to the right
plt.yticks(fontsize=12)
plt.tight_layout()
plt.show()

# Plotting attack locations on a scatter plot
plt.figure(figsize=(10, 6))
plt.scatter(df['Longitude'], df['Latitude'], c='red', alpha=0.6, edgecolor='k')
plt.title('Locations of Terrorist Attacks')
plt.xlabel('Longitude')
plt.ylabel('Latitude')
plt.grid(True)
plt.show()

# Heatmap to identify hot zones of attacks
plt.figure(figsize=(12, 8))  # Increased the figure size for better clarity
sns.kdeplot(
    x=df['Longitude'],
    y=df['Latitude'],
    fill=True,  # Use 'fill' instead of 'shade'
    cmap="Reds",
    bw_adjust=0.5,
    thresh=0,  # Set threshold to 0 to show even the lowest density
    levels=100,  # Increase the number of contour levels for smoother gradients
)

plt.title('Heatmap of Terrorist Attack Hot Zones')
plt.xlabel('Longitude')
plt.ylabel('Latitude')
plt.show()
