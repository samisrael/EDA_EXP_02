**Netflix Shows & Movies**

**Aim**

To analyze Netflix dataset and compare movies vs TV shows, top producing countries, and release year trends.

**Procedure / Algorithm**

  1)Load dataset (netflix_titles.csv).<br>
  2)Count movies vs TV shows.<br>
  3)Group by country → top contributors.<br>
  4)Create pivot table (release year vs type).<br>
  5)Visualize with bar & line charts.

**Program**
```
import pandas as pd
df = pd.read_csv(r'https://raw.githubusercontent.com/allenkong221/netflix-titles-dataset/main/netflix_titles.csv')
df.head()
 print("Shape:", df.shape)
 print("Columns:", df.columns, "\n")
 print("Type counts:\n", df['type'].value_counts(), "\n")
df.groupby('type')['type'].count()
df.pivot_table(
    index='country', 
    columns='type', 
    values='title', 
    aggfunc='count', 
    fill_value=0
)
top_directors = df['director'].value_counts().head(5)
print("Top 5 Directors:\n", top_directors, "\n")
df['date_added'] = pd.to_datetime(df['date_added'])
df['year_added'] = df['date_added'].dt.year
df['month_added'] = df['date_added'].dt.month
trend = df.groupby(['year_added', 'type']).size().unstack(fill_value=0)
print("Yearly Trend by Type:\n", trend.head(), "\n")
df_genre = (df[['show_id','listed_in']] .dropna().assign(listed_in=df['listed_in'].str.split(', ')).explode('listed_in'))
df_expanded = df.merge(df_genre, on='show_id', how='left')
print("Columns after merge:\n", df_expanded.columns)
print("\nExpanded Genre Sample:\n", df_expanded[['title','listed_in_y']].head())
top_genres = df_expanded['listed_in_y'].value_counts().head(5)
print("\nTop 5 Genres:\n", top_genres, "\n")

```

**Ouptut**
<img width="762" height="271" alt="image" src="https://github.com/user-attachments/assets/25f3842e-1812-442e-836a-6dac7c4af3bb" />
<BR>
<img width="537" height="133" alt="image" src="https://github.com/user-attachments/assets/6884db10-20c4-49be-b712-e3b0029a1310" /><BR>
<img width="377" height="471" alt="image" src="https://github.com/user-attachments/assets/c810b1ff-d043-4e71-8099-303db151d557" /><BR>
<img width="213" height="119" alt="image" src="https://github.com/user-attachments/assets/e1f8c602-4b74-403f-945e-b8fba0145070" /><BR>
<img width="469" height="315" alt="image" src="https://github.com/user-attachments/assets/7d313f37-4b6b-40c7-a58c-8a29d0daa6e4" />


**Result**

Helps Netflix in content planning & investments.
