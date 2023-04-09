# data_science

# Problem 1

## (1) Following are the $Statistics$ obtained:
* Initial number if trips: `6867`
* Trips after removing $0 duration$ trips: `6821`
* Maximum duration of the trip: `518 minutes`   
* Minimum duration of the trip: `1 minutes`  
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

* For the given input data, we will need approximately $4692^2   \approx 4.7$ x $10^7$ `operations` and the progam did not `terminate` on my machine after `20 minutes` 

### `Faster Algorithm`
* Toward building the `algorithm` I followed the shown thoughtprocess:
Let $i$ and $j$ be two row indices: $0 <= i,j < n$ 

1) 


Time Complexity: $\mathcal{O}(nlog(n))$  
Auxillary Space: $\mathcal{O}(n)$

#### For the given data, it produced the output in $$ $seconds$
#### Total number of `feasible pairs` = 





