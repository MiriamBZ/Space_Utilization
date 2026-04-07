# Space_Utilization
import pandas as pd
import matplotlib.pyplot as plt

# Load the Excel file
file_path = 'WesternU Space Inventory_raw data  3.29. 26.xlsx'
df = pd.read_excel(file_path, engine='openpyxl')

# Create pivot summary by FICM (sum of area)
pivot = (
    df.dropna(subset=['FICM'])
      .pivot_table(index='FICM', values='Room_Area', aggfunc='sum')
      .sort_values('Room_Area', ascending=False)
)

# Create bar chart
plt.figure(figsize=(14, 8))
plt.bar(pivot.index, pivot['Room_Area'])
plt.xticks(rotation=75, ha='right')
plt.ylabel('Total Area (ASF)')
plt.title('WesternU Space Inventory – Total Area by FICM')

plt.tight_layout()
plt.show()
