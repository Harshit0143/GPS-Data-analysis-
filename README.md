# Problem 1

## Part 1 
#### Following are the $Statistics$ obtained:
* Initial number of trips: `6867`
* Trips after removing $0$ $duration$ trips: `6821`
* Maximum $duration$ of the trip: `518 minutes`   
* Minimum $duration$ of the trip: `1 minutes`  
* Total number of trips corresponding to the minimum duration: `89` 
* Total number of $circular$ trips: `169`
* Percentage of total $circular$ trips: `2.478%`   
* Total runtime of `Statistics()` the function: `0.09171938896179199 seconds`  

* Average ride duration: `12.526755607682158 minutes`
* Maximum probable duration: `5.9115-6.17 minutes` with probability: `0.2813021681534756`
* Average ride duration: 

## `PDF` and `CDF` for ride duration:
 <p align = "center">
      
<img width="500" alt="Screenshot 2023-04-10 at 5 33 55 PM" src="https://user-images.githubusercontent.com/97736991/230898233-7d93d8ea-8c6d-45ba-b4cb-38ddbdcf8114.png">
<img width="500" alt="Screenshot 2023-04-10 at 5 34 12 PM" src="https://user-images.githubusercontent.com/97736991/230898291-e3e63eaa-26ff-4fec-a313-176f2923fb7a.png">

 </p>


<br><br><br><br><br>

## Part 2 

### After `filtering` out rides b=from `06:00 AM` to `06:00 PM`: `4692` rides 
### Running time for `filtering`: `0.002974987030029297 seconds`
### There are the following methods to compute the number of `feasible pairs`:

### The `Naive Algorithm`: 
#### Define: 
* $n$ = number of `rows` in the `filtered` data, here $n=4692$

Let $i$ and $j$ be two row indices: $0 <= i,j < n$ 
* for every pair $(i,j)$ , $i~=j$  we check if `trip` $i$ then `trip` $j$ is feasible. 
* There will be total $\frac{n(n-1)}{2}$ such pairs 
* `ordered pair` $(i,j)$ is $feasible \iff$ $(latitude_i,longitude_i) = (latitude_j,longitude_j)$ $and$ ($end\\_time_i <= start\\_time_j$) 

Time Complexity: $\mathcal{O}(n^2)$  
Auxillary Space: $\mathcal{O}(1)$

* For the given input data, we will need approximately $4692^2   \approx 2.2$ x $10^7$ `operations` a
* it did `terminated` on  `Google Colab` in ~`3 hr 17 min`    

### `Efficient Algorithm`
* Toward building the `algorithm` I followed the shown thoughtprocess:
Let $i$ and $j$ be two row indices: $0 <= i,j < n$ 

* For then to be fessible it is `necessary` that $end\\_depot_i = start\\_depot_j$
* Notice, there can be `atmost` $2n$ `distict` depots as each row as exactly $2$ $depots$ 
* We will exploit this. We for each $depot$ $d$ we will count the number of `feasible pairs` such that ride $i$ ends at $d$ and ride $j$ starts at $d$
* Not Make `2 groupings`.
* In `Grouping 1`, group all rides by their `start depot` (Atmost $n$ groups)
* In `Grouping 2`, group all rides by their `end depot` (Atmost $n$ groups)
* Sort `rides` in `Grouping 1` in each group individually by `start time` 
* Sort `rides` in `Grouping 2` in each group individually by `end time` 
* This further gives a direct `2 pointer` apporach to solve the remaining problem in $\mathcal{O}(n)$ time describled below:

#### We call `Grouping 1` as `dict_st`. Note that it is a `dictionary` with `key` = `start_depot` of ride, mapped to all `rides` with that `start depot`, sorted according to `start time` of ride
#### `Grouping 2` is called `dict_en` and is defined analogously 

1) Create a variable `cnt` to store the answer. Assign `cnt -> 0` initally   
2) Iterate over the `key` in `dict_en`.    
      ```
      if (key) is not present in (dict_st), 
                continue
      else 
        curr -> Number of feasible pairs in the 2 arrays `dict_st[key]` and  `dict_en[key]`
        cnt -> cnt + curr 
      ```
3) How to get `curr` ? 
  As = `dict_en[key]` : sorted by end time 
  Ae = `dict_st[key]` : sorted by start time 
  ```
  start with a:
     pointer x poining to Ae[0]
     pointer y poining to As[0]
  curr = 0 
  for x = 0, 1 , 2.......Ae.size() -1  [For every ride ending at key.]
       
       while [y is withing length] and [As[y].srart_time < Ae[x].end_time]
          y -> y + 1                          [Notice As[y].start_time are sorted. Once we reach a valid ride, ALL rides to it's right are valid 
       end while 
       
       curr -> curr + As.size() - y
  end for 
  
  Note that 
  Ae[x].end_time are increasing so the valid set of y's for Ae[x+1] is always a subset of valid set of y's for Ae[x]
  ``` 
  * One iteration takes: $\mathcal{O}(dict\\_st[key].size() + dict\\_en[key].size())$  time. 
  
  $$\sum\limits_{all &ensp; keys} dict\\_st[key].size() + dict\\_en[key].size() = n + n = 2n$$
   
  
  



Time Complexity: $\mathcal{O}(nlog(n))$  
Auxillary Space: $\mathcal{O}(n)$

#### For the given data, runtime:  `1.9116671085357666` seconds
#### Total number of `feasible pairs` = `43394`



# Part 3
#### Note that the `data` here is restricted to just the first 100 rows 
* First I had to decide a circle to to download the `graph_from_point()` from the `OSMnX` module
* I started with the rough estimate:  `average` of (latitude,longitude) of given points.
* Now i use the `folium` module to plot these points and the `circle` on a `map` 
* Then I used hit and trial to get roughly the cirle of `least radius` that enclosed all the given points (So that there is minimal computation required in downloading the Graph)

* Among the top 100 entries there are `147` unique depoots    
#### Figure shows the `depots` plotted on a map.
 <p align = "center"> 
<img width="700" alt="Screenshot 2023-04-10 at 4 56 42 PM" src="https://user-images.githubusercontent.com/97736991/230892995-b82f3251-d7dc-42c0-96f6-f003cde41a73.png"></p>

#### Here is the `circele` I decided to download `G` from. Center = `(38.98,-77.12)`, `radius = 22000 m`
 <p align = "center"> 
<img width="700" alt="Screenshot 2023-04-10 at 5 00 10 PM" src="https://user-images.githubusercontent.com/97736991/230893488-3ac17e6f-da12-48c0-9f23-5802ed4c3337.png"></p>



