---
title: "Ekstra funksjon"
figures_to_include:
	- "4-3-3-visualisering_95_0.png"
	- "4-3-3-visualisering_98_0.png"
	- "4-3-3-visualisering_100_0.png"
---


```python
from scipy.stats import gaussian_kde

def kdeplot_with_info(values, central = 90, ax = None, unit = "", color = "green"):
    if ax is None:
        ax = plt.gca()

    d = (100-central)/2.0
    ps = np.percentile(values, d)
    pe = np.percentile(values, 100-d)
    mean = values.mean()
    median = values.median()
        
    kde = gaussian_kde(values)
    kde_mean = kde.evaluate(mean)[0]
    kde_median = kde.evaluate(median)[0]
        
    area90_label = f"Central {central}%: {ps:.2f} - {pe:.2f} {unit}"
    mean_label = f"Mean: {mean:.2f} {unit}"
    median_label = f"Median: {median:.2f} {unit}"

    sns.kdeplot(values, ax=ax, color="grey", fill=True)
    sns.kdeplot(values, ax=ax, color=color, fill=True, label=area90_label, clip=(ps, pe))
    ax.plot([mean, mean], [0, kde_mean], color=color, label=mean_label)
    ax.plot([median, median], [0, kde_median], color=color,  linestyle="--", label=median_label)
    plt.grid(True, which='both', linestyle='--', linewidth=0.5)
    ax.legend()

    xmax = np.percentile(values, 99)
    ymax = ax.get_ylim()[1]
    
    return xmax, ymax
```


```python
from matplotlib.gridspec import GridSpec

def kdeplots(df, column, unit="", color="green"):
    df_type = type(df)
    if df_type is pd.core.frame.DataFrame:
        l = 0
        c = 1
        r = 1
    elif df_type is pd.core.groupby.generic.DataFrameGroupBy:
        info = df.grouper.levels
        l = len(info)
        r = len(info[0])
        if l == 1:
            c = 1
        elif l == 2:
            c = len(info[1]) 
        else:
            raise ValueError("Cannot use DataFrame grouped by more than two columns")

    def create_figure(r, c, h=4, w=8, top=0.1):
        fig = plt.figure(figsize=(w*c, h*r + top))
        gs = GridSpec(r+1, c, figure=fig, hspace=0.3, height_ratios = [top] + [h]*r)
        axs = np.array([[fig.add_subplot(gs[i+1, j]) for j in range(c)] for i in range(r)])
        return fig, axs
        
    fig, axs = create_figure(r, c)
    axs1d = axs.ravel()
      
    def get_dataframe(d0, d1):
        if l==0:
            return df, ""
        elif l==1:
            index = info[0][d0]
            new_df = df.get_group(index)
            title = index
            return new_df, title
        else:
            index1 = info[0][d0]
            index2 = info[1][d1]
            index = (info[0][d0], info[1][d1])
            new_df = df.get_group(index)
            title = f"{index1}, {index2}"
            return new_df, title
    
    xmax = 0
    ymax = 0
    for d0 in range(r):
        for d1 in range(c):
            ax = axs[d0, d1]
            new_df, title = get_dataframe(d0, d1)
            values = new_df[column]
            n = values.size
            if n > 1:
                x, y = kdeplot_with_info(values, ax=ax, unit=unit, color=color)
                xmax = max(xmax, x)
                ymax = max(ymax, y) 
                ax.set_title(title)
            else: 
                fig.delaxes(ax)

    for ax in axs1d:
        ax.set_xlim(0, xmax)
        ax.set_ylim(0, ymax)
        ax.set_xlabel("")

    for ax in axs1d[1:]:
        ax.set_ylabel("")
        ax.set_yticklabels([])

    title_space = 0.5
    top = 1.0 - title_space / fig.get_figheight()
    plt.subplots_adjust(top=top)
    
    def present(s):
        return s.replace("_", " ").capitalize()

    title = f"Distribution of {present(column)}"
    fig.suptitle(title, fontsize=16)

    return fig, axs1d
```


```python
kdeplots(trips, "distance", unit="km")
plt.show()
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-3-visualisering_95_0.png' width=600>
    



```python
def get_hour_as_fraction(date_string):
    date_object = datetime.fromisoformat(date_string)
    return date_object.hour + date_object.minute/60 + date_object.second/3600

test = get_hour_as_fraction("2023-07-01 10:27:10")
print(test)
```

    10.452777777777778



```python
trips["hour_as_fraction"] = trips["started_at"].apply(get_hour_as_fraction)
```


```python
grouped = trips.groupby("part_of_week")

fig, axs = kdeplots(grouped, "hour_as_fraction")
axs[0].legend(loc="upper left", fontsize=9)
plt.show()
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-3-visualisering_98_0.png' width=600>
    



```python
trips["duration_in_minutes"] = trips["duration"]/60
print(trips["duration_in_minutes"])
```

    0         17.416667
    1         11.016667
    2         11.966667
    3         17.600000
    4          3.550000
                ...    
    131376     3.083333
    131377    16.600000
    131378    12.850000
    131379    39.116667
    131380     2.250000
Name: duration_in_minutes, Length: 131381, dtype: float64



```python
grouped = trips.groupby(["part_of_day", "part_of_week"]) 
kdeplots(grouped, "duration_in_minutes", unit="min")
plt.show()
```


    
<img src='/media/markdowncontent/assosiated_files/4-3-3-visualisering_100_0.png' width=600>
    



```python
means = grouped["duration"].mean()
print(means)
```

part_of_day  part_of_week
afternoon    weekday          841.186977
weekend         1049.025567
evening      weekday          817.043079
weekend          901.500420
morning      weekday          864.435644
weekend         1060.263795
night        weekday          568.903814
weekend          632.435294
Name: duration, dtype: float64

