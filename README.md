

```python
#Dependencies
import pandas as pd
import numpy as np
```


```python
#Load json
json_path1="purchase_data.json"
#json_path2="purchase_data2.json"
```


```python
#Read files with pandas
file1=pd.read_json(json_path1)
file2=pd.read_json(json_path2)


purchase_data1_df = pd.DataFrame(file1)
purchase_data1_df.head()
purchase_data2_df=pd.DataFrame(file2)
purchase_data2_df.head()

```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20</td>
      <td>Male</td>
      <td>93</td>
      <td>Apocalyptic Battlescythe</td>
      <td>4.49</td>
      <td>Iloni35</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>12</td>
      <td>Dawne</td>
      <td>3.36</td>
      <td>Aidaira26</td>
    </tr>
    <tr>
      <th>2</th>
      <td>17</td>
      <td>Male</td>
      <td>5</td>
      <td>Putrid Fan</td>
      <td>2.63</td>
      <td>Irim47</td>
    </tr>
    <tr>
      <th>3</th>
      <td>17</td>
      <td>Male</td>
      <td>123</td>
      <td>Twilight's Carver</td>
      <td>2.55</td>
      <td>Irith83</td>
    </tr>
    <tr>
      <th>4</th>
      <td>22</td>
      <td>Male</td>
      <td>154</td>
      <td>Feral Katana</td>
      <td>4.11</td>
      <td>Philodil43</td>
    </tr>
  </tbody>
</table>
</div>




```python
#entries in file 1
purchase_data1_df.count()
```




    Age          780
    Gender       780
    Item ID      780
    Item Name    780
    Price        780
    SN           780
    dtype: int64




```python
#entries in file 2
purchase_data2_df.count()
```




    Age          78
    Gender       78
    Item ID      78
    Item Name    78
    Price        78
    SN           78
    dtype: int64




```python
#combine files
combined_PurDAta_df = pd.concat([purchase_data1_df,purchase_data2_df], axis=0)
combined_PurDAta_df.count()
combined_PurDAta_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
    </tr>
  </tbody>
</table>
</div>




```python
#finding number of plays
NumPlayers=combined_PurDAta_df.groupby("SN").nunique()
NumPlayers = NumPlayers["SN"].count()
NumPlayers
Player_Breakdown=pd.DataFrame({"Number of Players":[NumPlayers]})
Player_Breakdown
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Number of Players</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>612</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Purchasing Analysis
#Number of Unique Items
UniqueItems = combined_PurDAta_df.groupby("Item Name").nunique()
UniqueItems = UniqueItems["Item Name"].count()
UniqueItems =180

#Finding Average Purchase Price
Average_Price = combined_PurDAta_df.groupby("Item Name").nunique()
Average_Price = Average_Price["Price"].mean()
#Average_Price = 1.37

#Number of Purchases
TotalPurchases = len(combined_PurDAta_df)
TotalPurchases

#Total Purchase Value
Total_Purchase_Value = combined_PurDAta_df["Price"].sum()
Total_Purchase_Value

Purchase_Breakdown = pd.DataFrame({"# of Unique Items":[UniqueItems], "Average Price":[Average_Price],
                                  "Number of Purchases":[TotalPurchases], "Total Revenue":[Total_Purchase_Value]})

Purchase_Breakdown["Average Price"]=Purchase_Breakdown["Average Price"].map("${0:,.2f}".format)
Purchase_Breakdown["Total Revenue"]=Purchase_Breakdown["Total Revenue"].map("${0:,.2f}".format)
Purchase_Breakdown
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th># of Unique Items</th>
      <th>Average Price</th>
      <th>Number of Purchases</th>
      <th>Total Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>180</td>
      <td>$1.37</td>
      <td>858</td>
      <td>$2,514.43</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Gender Demographics
#filter for unique players
UniquePlayers_df = combined_PurDAta_df.drop_duplicates(["SN"])

#Calculating Male Players
MaleCount = UniquePlayers_df["Gender"].value_counts()["Male"]
MaleCount_Percentage = MaleCount / NumPlayers*100

#Calculating Female Players
FemaleCount = UniquePlayers_df["Gender"].value_counts()["Female"]
FemaleCount_Percentage = FemaleCount / NumPlayers*100

#Calculating non-disclosed gender
NonDisclosedCount = NumPlayers - MaleCount - FemaleCount
NonDisclosed_Percentage = NonDisclosedCount / NumPlayers*100

#Putting Data into DataFrame
Gender_Breakdown = pd.DataFrame({"Percentage of Players":{"Males": MaleCount_Percentage, "Females":FemaleCount_Percentage,"Undisclosed":NonDisclosed_Percentage}})
                               
Gender_Count=pd.DataFrame({"Total Count":{"Males":MaleCount,"Females":FemaleCount, "Undisclosed":NonDisclosedCount}})

Gender_merge = pd.concat([Gender_Breakdown,Gender_Count],axis=1) 
#Fix Formatting
Gender_merge["Percentage of Players"]=Gender_merge["Percentage of Players"].map("{0:,.2f}%".format)
Gender_merge

```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Percentage of Players</th>
      <th>Total Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Females</th>
      <td>17.65%</td>
      <td>108</td>
    </tr>
    <tr>
      <th>Males</th>
      <td>80.88%</td>
      <td>495</td>
    </tr>
    <tr>
      <th>Undisclosed</th>
      <td>1.47%</td>
      <td>9</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Purchasing Analysis (Gender)

#Male Calculations
Male_df = combined_PurDAta_df.loc[combined_PurDAta_df["Gender"]=="Male"]
Male_Average_Purchase_Price = Male_df["Price"].mean()
Male_Total_Purchase_Value = Male_df["Price"].sum()
Male_Purchase_Count=len(Male_df)
Male_Normalized_Total=Male_Total_Purchase_Value / MaleCount

#Female Calculations
Female_df = combined_PurDAta_df.loc[combined_PurDAta_df["Gender"]=="Female"]
Female_Average_Purchase_Price = Female_df["Price"].mean()
Female_Total_Purchase_Value = Female_df["Price"].sum()
Female_Purchase_Count=len(Female_df)
Female_Normalized_Total=Female_Total_Purchase_Value / FemaleCount

#Other Calculation
Other_df = combined_PurDAta_df.loc[(combined_PurDAta_df["Gender"] !="Male") & (combined_PurDAta_df["Gender"]!="Female")]
Other_Average_Purchase_Price = Other_df["Price"].mean()
Other_Total_Purchase_Value = Other_df["Price"].sum()
Other_Purchase_Count=len(Other_df)
Other_Normalized_Total=Other_Total_Purchase_Value / NonDisclosedCount

#Put into DataFrame
Gender_Purchase_Analysis=[ {"Purchase Count":Male_Purchase_Count,"Average Purchase Price": Male_Average_Purchase_Price,"Total Purchase Value":Male_Total_Purchase_Value,"Normalized Purchase Price":Male_Normalized_Total},
                         { "Purchase Count":Female_Purchase_Count,"Average Purchase Price": Female_Average_Purchase_Price,"Total Purchase Value":Female_Total_Purchase_Value,"Normalized Purchase Price":Female_Normalized_Total},
                         { "Purchase Count":Other_Purchase_Count,"Average Purchase Price": Other_Average_Purchase_Price,"Total Purchase Value":Other_Total_Purchase_Value,"Normalized Purchase Price":Other_Normalized_Total}
                         ]

#Add Index Header
Gender_Purchase_Table = pd.DataFrame(Gender_Purchase_Analysis, index=['Male', 'Female', 'Other'])
Gender_Purchase_Table.index.name="Gender"

#Fix Formatting
Gender_Purchase_Table["Average Purchase Price"]=Gender_Purchase_Table["Average Purchase Price"].map("${0:,.2f}".format)
Gender_Purchase_Table["Normalized Purchase Price"]=Gender_Purchase_Table["Normalized Purchase Price"].map("${0:,.2f}".format)
Gender_Purchase_Table["Total Purchase Value"]=Gender_Purchase_Table["Total Purchase Value"].map("${0:,.2f}".format)
Gender_Purchase_Table.columns
Gender_Purchase_Table=Gender_Purchase_Table[["Purchase Count","Average Purchase Price","Total Purchase Value","Normalized Purchase Price"]]
Gender_Purchase_Table
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Normalized Purchase Price</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Male</th>
      <td>697</td>
      <td>$2.94</td>
      <td>$2,052.28</td>
      <td>$4.15</td>
    </tr>
    <tr>
      <th>Female</th>
      <td>149</td>
      <td>$2.85</td>
      <td>$424.29</td>
      <td>$3.93</td>
    </tr>
    <tr>
      <th>Other</th>
      <td>12</td>
      <td>$3.15</td>
      <td>$37.86</td>
      <td>$4.21</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Age Demographics
#Creating bins (0-12,12-16,16-22,22+)
bins=[0,12,16,22,99]
group_names=["<12","12-16","16-22","22+"]

#cut dataframe and place age into bins
combined_PurDAta_df["Age Range"]=pd.cut(combined_PurDAta_df["Age"],bins,labels=group_names)
UniquePlayers_df = combined_PurDAta_df.drop_duplicates(["SN"])
#unique players
age_groups_unique=UniquePlayers_df.groupby("Age Range")
#all players
age_groups_all=combined_PurDAta_df.groupby("Age Range")
AgeGroup_Total=age_groups_unique["SN"].count()

AgeGroup_Average_Purchase_Price = age_groups_all["Price"].mean()
AgeGroup_Total_Purchase_Value=age_groups_all["Price"].sum()
AgeGroup_Normalized_Average = AgeGroup_Total_Purchase_Value/AgeGroup_Total

#Put into DataFrame
AgeGroup_Breakdown=pd.concat([AgeGroup_Total,AgeGroup_Average_Purchase_Price,AgeGroup_Total_Purchase_Value,AgeGroup_Normalized_Total],axis=1) 
AgeGroup_Breakdown=pd.DataFrame(AgeGroup_Breakdown)
AgeGroup_Breakdown.columns=["Purchase Count","Average Purchase Price","Total Purchase Price","Normalized Average"]

#Format Data Table
AgeGroup_Breakdown["Average Purchase Price"]=AgeGroup_Breakdown["Average Purchase Price"].map("${0:,.2f}".format)
AgeGroup_Breakdown["Total Purchase Price"]=AgeGroup_Breakdown["Total Purchase Price"].map("${0:,.2f}".format)
AgeGroup_Breakdown["Normalized Average"]=AgeGroup_Breakdown["Normalized Average"].map("${0:,.2f}".format)
AgeGroup_Breakdown
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Price</th>
      <th>Normalized Average</th>
    </tr>
    <tr>
      <th>Age Range</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;12</th>
      <td>35</td>
      <td>$3.06</td>
      <td>$165.37</td>
      <td>$4.72</td>
    </tr>
    <tr>
      <th>12-16</th>
      <td>66</td>
      <td>$2.75</td>
      <td>$250.38</td>
      <td>$3.79</td>
    </tr>
    <tr>
      <th>16-22</th>
      <td>223</td>
      <td>$2.92</td>
      <td>$873.71</td>
      <td>$3.92</td>
    </tr>
    <tr>
      <th>22+</th>
      <td>288</td>
      <td>$2.96</td>
      <td>$1,224.97</td>
      <td>$4.25</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Top Spenders
TopSpenders_df = combined_PurDAta_df.groupby("SN", as_index=True).agg({"Price":"sum","Item ID":"count"})
TopSpenders_df["Average Purchase Price"]=TopSpenders_df["Price"]/TopSpenders_df["Item ID"]
TopSpenders_df=TopSpenders_df.rename(columns={"Price":"Total Purchase Value","Item ID": "Purchase Count"})
TopSpenders_df=TopSpenders_df.sort_values("Total Purchase Value",ascending=False)

#Formatting
TopSpenders_df["Total Purchase Value"]=TopSpenders_df["Total Purchase Value"].map("${0:,.2f}".format)
TopSpenders_df["Average Purchase Price"]=TopSpenders_df["Average Purchase Price"].map("${0:,.2f}".format)
#Reorder columns
TopSpenders_df=TopSpenders_df[["Purchase Count", "Average Purchase Price","Total Purchase Value"]]
#display
TopSpenders_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Undirrala66</th>
      <td>5</td>
      <td>$3.41</td>
      <td>$17.06</td>
    </tr>
    <tr>
      <th>Aerithllora36</th>
      <td>4</td>
      <td>$3.77</td>
      <td>$15.10</td>
    </tr>
    <tr>
      <th>Saedue76</th>
      <td>4</td>
      <td>$3.39</td>
      <td>$13.56</td>
    </tr>
    <tr>
      <th>Sondim43</th>
      <td>4</td>
      <td>$3.25</td>
      <td>$13.02</td>
    </tr>
    <tr>
      <th>Mindimnya67</th>
      <td>4</td>
      <td>$3.18</td>
      <td>$12.74</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Most Popular Items
TopItems_df = combined_PurDAta_df.groupby([ "Item Name","Item ID"], as_index=True).agg({"SN":"count","Price":"sum"})
TopItems_df["Item Price"]=TopItems_df["Price"]/TopItems_df["SN"]
TopItems_df=TopItems_df.sort_values("SN",ascending=False)
TopItems_df = TopItems_df.rename(columns={"SN":"Purchase Count","Price":"Total Purchase Value"})
#top profitable dataframe
TopProfitable_df = TopItems_df.sort_values("Total Purchase Value",ascending=False)

#Formatting
TopItems_df["Total Purchase Value"]=TopItems_df["Total Purchase Value"].map("${0:,.2f}".format)
TopItems_df["Item Price"]=TopItems_df["Item Price"].map("${0:,.2f}".format)
#Reorder columns
TopItems_df=TopItems_df[["Purchase Count","Item Price","Total Purchase Value"]]
#display
TopItems_df.head()

```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item Name</th>
      <th>Item ID</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Arcane Gem</th>
      <th>84</th>
      <td>12</td>
      <td>$2.45</td>
      <td>$29.34</td>
    </tr>
    <tr>
      <th>Betrayal, Whisper of Grieving Widows</th>
      <th>39</th>
      <td>11</td>
      <td>$2.35</td>
      <td>$25.85</td>
    </tr>
    <tr>
      <th>Trickster</th>
      <th>31</th>
      <td>10</td>
      <td>$2.32</td>
      <td>$23.22</td>
    </tr>
    <tr>
      <th>Feral Katana</th>
      <th>154</th>
      <td>9</td>
      <td>$2.62</td>
      <td>$23.55</td>
    </tr>
    <tr>
      <th>Serenity</th>
      <th>13</th>
      <td>9</td>
      <td>$1.49</td>
      <td>$13.41</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Most Profitable Item
#Formatting
TopProfitable_df["Total Purchase Value"]=TopProfitable_df["Total Purchase Value"].map("${0:,.2f}".format)
TopProfitable_df["Item Price"]=TopProfitable_df["Item Price"].map("${0:,.2f}".format)
#Reorder columns
#TopItems_df=TopItems_df[["Purchase Count","Item Price","Total Purchase Value"]]
#display
TopProfitable_df.head()


```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Purchase Count</th>
      <th>Total Purchase Value</th>
      <th>Item Price</th>
    </tr>
    <tr>
      <th>Item Name</th>
      <th>Item ID</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Retribution Axe</th>
      <th>34</th>
      <td>9</td>
      <td>$37.26</td>
      <td>$4.14</td>
    </tr>
    <tr>
      <th>Splitter, Foe Of Subtlety</th>
      <th>107</th>
      <td>9</td>
      <td>$33.03</td>
      <td>$3.67</td>
    </tr>
    <tr>
      <th>Spectral Diamond Doomblade</th>
      <th>115</th>
      <td>7</td>
      <td>$29.75</td>
      <td>$4.25</td>
    </tr>
    <tr>
      <th>Orenmir</th>
      <th>32</th>
      <td>6</td>
      <td>$29.70</td>
      <td>$4.95</td>
    </tr>
    <tr>
      <th>Arcane Gem</th>
      <th>84</th>
      <td>12</td>
      <td>$29.34</td>
      <td>$2.45</td>
    </tr>
  </tbody>
</table>
</div>


