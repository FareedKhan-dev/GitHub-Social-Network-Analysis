# SNA Group Assignment

Importing Libraries


```python
import networkx as nx
import pandas as pd
import matplotlib.pyplot as plt
```

Importing dataset


```python
users = pd.read_csv('musae_git_target.csv')
```

Reading Graphs


```python
Data = open('musae_git_edges.csv', "r")

next(Data, None)  # skip the first line in the input file

followers = nx.parse_edgelist(Data, delimiter=',', create_using=nx.Graph(), nodetype=int)
```

Finding Local Cluster (each nodes clustering coefficient)


```python
local_cluster = nx.clustering(followers)
sorted_local_cluster = {k: v for k, v in sorted(local_cluster.items(), key=lambda item: item[1])}
sorted_local_cluster
```




    {0: 0,
     34526: 0,
     34035: 0,
     6067: 0,
     20183: 0,
     3: 0,
     4950: 0,
     4: 0,
     ...
     13958: 0,
     7764: 0,
     ...}



Global Clustering with count zeroes (default)


```python
global_cluster = nx.average_clustering(followers, count_zeros=True)
global_cluster
```




    0.16753704480107323



eccentricity (shortest path with maximum number of nodes)


```python
# import pickle
# with open('eccentricity.pkl', 'rb') as f:
#     eccentricity = pickle.load(f)

eccentricity = nx.eccentricity(followers)
sorted_eccentricity = {k: v for k, v in sorted(eccentricity.items(), key=lambda item: item[1])}

sorted_eccentricity = list(dict(sorted(eccentricity.items(), key=lambda item: item[1], reverse=True)).items())

# get index (node number) and value (node eccentricity value) top 10 after sorting
sorted_eccentricity_indexes = [x[0] for x in sorted_eccentricity]
sorted_eccentricity_values = [x[1] for x in sorted_eccentricity]

# Creating dataframe
top_sorted_eccentricity = pd.DataFrame({'Name':users.iloc[sorted_eccentricity_indexes].name.tolist(), 
                                      'Eccentricity': sorted_eccentricity_values, 
                                      'ml_target':users.iloc[sorted_eccentricity_indexes].ml_target.tolist()})

top_sorted_eccentricity.groupby('Eccentricity').count()['ml_target'].sort_values(ascending=False)
# top_sorted_eccentricity
```




    Eccentricity
    7     27399
    8      8677
    6      1113
    9       480
    10       27
    11        4
    Name: ml_target, dtype: int64



Radius of Followers Graph


```python
radius_of_graph = nx.radius(followers)
radius_of_graph
```

    6
    

Diameter of Followers Graph


```python
diameter_of_graph = nx.diameter(followers)
diameter_of_graph
```

    11
    

For verification diameter=maximum eccentricity

Density of follower


```python
density_of_graph = nx.density(followers)
density_of_graph
```


    0.0004066878203117068


Degree Distribution upto degree value 50 


```python
degree_distrubution = nx.degree_histogram(followers)
fig = plt.figure(figsize=(15, 10))
x = [i for i in range(0, 50)]
plt.bar(x, degree_distrubution[0:50])
plt.show()
```


    
![png](GitHub%20Social%20Network%20Code%20File_21_0.png)
    


Connected Components


```python
print(nx.is_connected(followers))
print(nx.number_connected_components(followers))
```

    True
    1
    

Average Path Length


```python
average_short_path_length = nx.average_shortest_path_length(followers)
average_short_path_length
```


    3.2464090056353823


_______________


```python
# Creating dataframe
single_value_calc = pd.DataFrame({'Radius': [radius_of_graph], 'Diameter': [diameter_of_graph], 'Density':[density_of_graph], 
                                  'Connected Component': [nx.number_connected_components(followers)],
                                  'Average Path Length': [average_short_path_length]})

# single_value_calc = pd.DataFrame({'Radius': [6], 'Diameter': [11],  'Density': [0.0004066878203117068], 
#                                   'Connected Component': [1], 'Average Path Length': [3.2464090056353823]})

single_value_calc.rename(index={0:'Overall Graph Measures'})
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Radius</th>
      <th>Diameter</th>
      <th>Density</th>
      <th>Connected Component</th>
      <th>Average Path Length</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Overall Graph Measures</th>
      <td>6</td>
      <td>11</td>
      <td>0.000407</td>
      <td>1</td>
      <td>3.246409</td>
    </tr>
  </tbody>
</table>
</div>




```python
local_clustering_sort = list((k,v) for k, v in sorted(local_cluster.items(), key=lambda item: item[0], reverse=True))
eccentricity_sort = list((k,v)for k, v in sorted(eccentricity.items(), key=lambda item: item[0], reverse=True))

# get index (node number) and value (node centrality value) top 10 after sorting
sorted_indexes = [x[0] for x in local_clustering_sort]
local_values_sort = [x[1] for x in local_clustering_sort]
eccentricity_values_sort = [x[1] for x in eccentricity_sort]

# Creating dataframe
eccentricity_and_local_cluster = pd.DataFrame({'Name':users.iloc[sorted_indexes].name.tolist(), 
                                      'Eccentricity': eccentricity_values_sort, 
                                      'Local Clustering': local_values_sort})

eccentricity_and_local_cluster
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Eccentricity</th>
      <th>Local Clustering</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>caseycavanagh</td>
      <td>7</td>
      <td>0.333333</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Injabie3</td>
      <td>8</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>qpautrat</td>
      <td>7</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>kris-ipeh</td>
      <td>7</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>shawnwanderson</td>
      <td>8</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>37695</th>
      <td>sunilangadi2</td>
      <td>8</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>37696</th>
      <td>SuhwanCha</td>
      <td>7</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>37697</th>
      <td>JpMCarrilho</td>
      <td>8</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>37698</th>
      <td>shawflying</td>
      <td>8</td>
      <td>0.178571</td>
    </tr>
    <tr>
      <th>37699</th>
      <td>Eiryyy</td>
      <td>8</td>
      <td>0.000000</td>
    </tr>
  </tbody>
</table>
<p>37700 rows × 3 columns</p>
</div>



___________

### Centrality Measures

Degree Centrality


```python
# Applying degree centrality in NetworX
deg_centrality = nx.degree_centrality(followers)

# Applying degree centrality in NetworX
deg_centrality = nx.degree_centrality(followers)
# Sorting degree centrality and getting top 10
sorted_deg_centrality = list(dict(sorted(deg_centrality.items(), key=lambda item: item[1], reverse=True)).items())

# get index (node number) and value (node centrality value) top 10 after sorting
sorted_deg_centrality_indexes = [x[0] for x in sorted_deg_centrality]
sorted_deg_centrality_values = [x[1] for x in sorted_deg_centrality]

# Creating dataframe
top_degree_centrality = pd.DataFrame({'Name':users.iloc[sorted_deg_centrality_indexes].name.tolist(), 
                                      'Degree Centrality': sorted_deg_centrality_values, 
                                      'ml_target':users.iloc[sorted_deg_centrality_indexes].ml_target.tolist()})

top_degree_centrality
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Degree Centrality</th>
      <th>ml_target</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>dalinhuang99</td>
      <td>0.250882</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>nfultz</td>
      <td>0.187936</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>addyosmani</td>
      <td>0.088172</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Bunlong</td>
      <td>0.078464</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>gabrielpconceicao</td>
      <td>0.065466</td>
      <td>0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>37695</th>
      <td>chrisryancarter</td>
      <td>0.000027</td>
      <td>0</td>
    </tr>
    <tr>
      <th>37696</th>
      <td>kcakdemir</td>
      <td>0.000027</td>
      <td>1</td>
    </tr>
    <tr>
      <th>37697</th>
      <td>chadmazilly</td>
      <td>0.000027</td>
      <td>0</td>
    </tr>
    <tr>
      <th>37698</th>
      <td>orionblastar</td>
      <td>0.000027</td>
      <td>1</td>
    </tr>
    <tr>
      <th>37699</th>
      <td>jovanidash21</td>
      <td>0.000027</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>37700 rows × 3 columns</p>
</div>



Closeness Centrality


```python
# Loading save json of closeness centrality output
# import pickle
# with open('closness_centrality.pkl', 'rb') as f:
#     closeness_centrality = pickle.load(f)

# Applying closeness centrality in NetworX
closeness_centrality = nx.closeness_centrality(followers)


# Sorting degree centrality and getting top 10
sorted_closness_centrality = list(dict(sorted(closeness_centrality.items(), key=lambda item: item[1], reverse=True)).items())

# get index (node number) and value (node centrality value) top 10 after sorting
sorted_closeness_centrality_indexes = [x[0] for x in sorted_closness_centrality]
sorted_closeness_centrality_values = [x[1] for x in sorted_closness_centrality]

# Creating dataframe
top_closeness_centrality = pd.DataFrame({'Name':users.iloc[sorted_closeness_centrality_indexes].name.tolist(), 
                                      'Closeness Centrality': sorted_closeness_centrality_values, 
                                      'ml_target':users.iloc[sorted_closeness_centrality_indexes].ml_target.tolist()})

top_closeness_centrality
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Closeness Centrality</th>
      <th>ml_target</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>nfultz</td>
      <td>0.523081</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>dalinhuang99</td>
      <td>0.517787</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Bunlong</td>
      <td>0.466324</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>addyosmani</td>
      <td>0.450342</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>gabrielpconceicao</td>
      <td>0.447461</td>
      <td>0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>37695</th>
      <td>haochenli</td>
      <td>0.155371</td>
      <td>0</td>
    </tr>
    <tr>
      <th>37696</th>
      <td>abhishekpopli</td>
      <td>0.153934</td>
      <td>1</td>
    </tr>
    <tr>
      <th>37697</th>
      <td>scandeiro</td>
      <td>0.147439</td>
      <td>0</td>
    </tr>
    <tr>
      <th>37698</th>
      <td>jazzchipc</td>
      <td>0.145151</td>
      <td>0</td>
    </tr>
    <tr>
      <th>37699</th>
      <td>SOUMAJYOTI</td>
      <td>0.141389</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>37700 rows × 3 columns</p>
</div>



Betweenness Centrality


```python
# Loading save json of closeness centrality output
# import pickle
# with open('betweeness_centrality.pkl', 'rb') as f:
#     betweeness_centrality = pickle.load(f)

# Applying betweeness centrality in NetworX
betweeness_centrality = nx.betweenness_centrality(followers)

# Sorting degree centrality and getting top 10
sorted_between_centrality = list(dict(sorted(betweeness_centrality.items(), key=lambda item: item[1], reverse=True)).items())

# get index (node number) and value (node centrality value) top 10 after sorting
sorted_between_centrality_indexes = [x[0] for x in sorted_between_centrality]
sorted_between_centrality_values = [x[1] for x in sorted_between_centrality]

# Creating dataframe
top_between_centrality = pd.DataFrame({'Name':users.iloc[sorted_between_centrality_indexes].name.tolist(), 
                                      'Betweeness Centrality': sorted_between_centrality_values, 
                                      'ml_target':users.iloc[sorted_between_centrality_indexes].ml_target.tolist()})

top_between_centrality
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Betweeness Centrality</th>
      <th>ml_target</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>dalinhuang99</td>
      <td>0.269599</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>nfultz</td>
      <td>0.240541</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Bunlong</td>
      <td>0.055323</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>addyosmani</td>
      <td>0.043408</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>gabrielpconceicao</td>
      <td>0.035337</td>
      <td>0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>37695</th>
      <td>chrisryancarter</td>
      <td>0.000000</td>
      <td>0</td>
    </tr>
    <tr>
      <th>37696</th>
      <td>kcakdemir</td>
      <td>0.000000</td>
      <td>1</td>
    </tr>
    <tr>
      <th>37697</th>
      <td>chadmazilly</td>
      <td>0.000000</td>
      <td>0</td>
    </tr>
    <tr>
      <th>37698</th>
      <td>orionblastar</td>
      <td>0.000000</td>
      <td>1</td>
    </tr>
    <tr>
      <th>37699</th>
      <td>jovanidash21</td>
      <td>0.000000</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>37700 rows × 3 columns</p>
</div>




```python
plt.subplot(1,3,1)
plt.xlabel('Centrality Values')
plt.title('Degree Centrality')

top_degree_centrality['Degree Centrality'].plot.hist(figsize=(30, 5), ylim=(0,200))
plt.subplot(1,3,2)
plt.xlabel('Centrality Values')
plt.title('Closeness Centrality')

top_closeness_centrality['Closeness Centrality'].plot.hist(figsize=(30, 5))

plt.subplot(1,3,3)
plt.xlabel('Centrality Values')
plt.title('Betweeness Centrality')

top_between_centrality['Betweeness Centrality'].plot.hist(figsize=(30, 5))

plt.show()

```


    
![png](GitHub%20Social%20Network%20Code%20File_37_0.png)
    


Visualizing Highest Degree Centrality Node in Graph


```python
followers_network = pd.read_csv('musae_git_edges.csv')
users = pd.read_csv('musae_git_target.csv')

nodes_with_deg_gret_100 = dict((k, v) for k, v in dict(followers.degree).items() if v > 50)

# Creating a function to check if id_1 or id_2 is ML or Web developer
def check_if_exist(id):
    if id in list(nodes_with_deg_gret_100.keys()):
        return 1
    else:
        return 0

followers_network['first_id'] = followers_network['id_1'].apply(check_if_exist)
# followers_network['second_id'] = followers_network['id_2'].apply(check_if_exist)
followers_test = followers_network[(followers_network['first_id'] == 1) & (followers_network['id_2'] == 31890)]
G = nx.from_pandas_edgelist(followers_test, 'id_1', 'id_2')

# Visualizing the highest degree centrality node regin in Graph
fig = plt.figure(figsize=(10, 10))
plt.margins(0,0)

nodes_sizes = []
nodes_color = []

for each in list(G.nodes):
    if each == sorted_deg_centrality[0][0]:
        nodes_sizes.append(4000)
        nodes_color.append('#f02b79')

    elif each == sorted_deg_centrality[1][0]:
        nodes_sizes.append(1000)
        nodes_color.append('#f02b79')
    else:
        nodes_sizes.append(20)
        nodes_color.append('#02A4DE')

print('Highest Degree Centrality Node Lies in Red Shaded Region')
nx.draw(G, node_size=nodes_sizes, node_color=nodes_color, edge_color='#dce8e0')
```

    Highest Degree Centrality Node Lies in Red Shaded Region
    


    
![png](GitHub%20Social%20Network%20Code%20File_39_1.png)
    


Visualizing Two Highest Closeness Centrality Node in Graph


```python
followers_network = pd.read_csv('musae_git_edges.csv')
users = pd.read_csv('musae_git_target.csv')

nodes_with_deg_gret_100 = dict((k, v) for k, v in dict(followers.degree).items() if v > 50)

# Creating a function to check if id_1 or id_2 is ML or Web developer
def check_if_exist(id):
    if id in list(nodes_with_deg_gret_100.keys()):
        return 1
    else:
        return 0

followers_network['first_id'] = followers_network['id_1'].apply(check_if_exist)
# followers_network['second_id'] = followers_network['id_2'].apply(check_if_exist)
followers_test = followers_network[(followers_network['first_id'] == 1) & (followers_network['id_2'] == 31890)]
G = nx.from_pandas_edgelist(followers_test, 'id_1', 'id_2')

# Visualizing the highest degree centrality node regin in Graph
fig = plt.figure(figsize=(10, 10))
plt.margins(0,0)

nodes_sizes = []
nodes_color = []

for each in list(G.nodes):
    if each == sorted_closness_centrality[0][0]:
        nodes_sizes.append(4000)
        nodes_color.append('#f02b79')

    elif each == sorted_closness_centrality[1][0]:
        nodes_sizes.append(1000)
        nodes_color.append('#f02b79')
    else:
        nodes_sizes.append(20)
        nodes_color.append('#02A4DE')


print('Highest Closeness Centrality Node Lies in Red Shaded Region')
nx.draw(G, node_size=nodes_sizes, node_color=nodes_color, edge_color='#dce8e0')
```

    Highest Closeness Centrality Node Lies in Red Shaded Region
    


    
![png](GitHub%20Social%20Network%20Code%20File_41_1.png)
    


Visualizing Two Betwenness Closeness Centrality Node in Graph


```python
followers_network = pd.read_csv('musae_git_edges.csv')
users = pd.read_csv('musae_git_target.csv')

nodes_with_deg_gret_100 = dict((k, v) for k, v in dict(followers.degree).items() if v > 50)

# Creating a function to check if id_1 or id_2 is ML or Web developer
def check_if_exist(id):
    if id in list(nodes_with_deg_gret_100.keys()):
        return 1
    else:
        return 0

followers_network['first_id'] = followers_network['id_1'].apply(check_if_exist)
# followers_network['second_id'] = followers_network['id_2'].apply(check_if_exist)
followers_test = followers_network[(followers_network['first_id'] == 1) & (followers_network['id_2'] == 31890)]
G = nx.from_pandas_edgelist(followers_test, 'id_1', 'id_2')

# Visualizing the highest degree centrality node regin in Graph
fig = plt.figure(figsize=(10, 10))
plt.margins(0,0)

nodes_sizes = []
nodes_color = []

for each in list(G.nodes):
    if each == sorted_between_centrality[0][0]:
        nodes_sizes.append(4000)
        nodes_color.append('#f02b79')

    elif each == sorted_between_centrality[1][0]:
        nodes_sizes.append(1000)
        nodes_color.append('#f02b79')
    else:
        nodes_sizes.append(20)
        nodes_color.append('#02A4DE')


print('Highest Betweenness Centrality Node Lies in Red Shaded Region')
nx.draw(G, node_size=nodes_sizes, node_color=nodes_color, edge_color='#dce8e0')
```

    Highest Betweenness Centrality Node Lies in Red Shaded Region
    


    
![png](GitHub%20Social%20Network%20Code%20File_43_1.png)
