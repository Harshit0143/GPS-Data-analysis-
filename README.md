# data_science

# Problem 1

## (1) Following are the $Statistics$ obtained:
* Initial number if trips: `6867`
* Trips after removing $0$ $duration$ trips: `6821`
* Maximum $duration$ of the trip: `518 minutes`   
* Minimum $duration$ of the trip: `1 minutes`  
* Total number of trips corresponding to the minimum duration: `89` 
* Total number of $circular$ trips: `169`
* Percentage of total $circular$ trips: `2.478%`   
* Total runtime of `Statistics()` the function: `0.23416614532470703 seconds`  


## (2) 

### After `filtering` out rides b=from `06:00 AM` to `06:00 PM`: `4692` rides 
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

* For the given input data, we will need approximately $4692^2   \approx 2.2$ x $10^7$ `operations` and the progam did not `terminate` on my machine after `20 minutes` 

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
  Ae = `dict_st[key]` : sorted by srart time 
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

#### For the given data, it produced the output in $$ $seconds$
#### Total number of `feasible pairs` = 





