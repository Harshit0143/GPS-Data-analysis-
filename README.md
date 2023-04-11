[Link to dataset](https://drive.google.com/drive/folders/18U6j-TobpwupjejTyipQaW-YB52JjnsL?usp=sharing)

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
* Maximum probable duration: `5.015  6.019 minutes` with probability: `0.07243530829951987`
* For constructing the `pdf`/`cdf`, the number of `buckets` was carefully chosen to `515` (found by hit and trial) so that the 
  $CDF(time) \to 1$ as $t \to \infty$. 
* Average ride duration: 
## `PDF` and `CDF` for ride duration:
 <p align = "center">
      
<img width="400" alt="Screenshot 2023-04-11 at 3 46 58 AM" src="https://user-images.githubusercontent.com/97736991/231009406-50008a3e-73ab-4c49-b13f-6b0f2ebeabee.png">
<img width="410
" alt="Screenshot 2023-04-11 at 3 47 10 AM" src="https://user-images.githubusercontent.com/97736991/231009431-432ab91f-8dc7-4c42-add6-906f4d4b5957.png">


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
#### Total number of `feasible pairs` = `41518`



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


# Problem 2


# Part 1
### Assumptions 
* The distance travelled by the person is the `Great Circle Distance` which uses the `Haversines` formula and assumes the `Earth` to be a perfectt sphere. 
* The change in `altitude` does not affect the calculation of `distances` significantly.  
* When the `trajector_id` changes, I have not started counting the distance separately, but continued. i.e. the distance between `last point` of trip $i$ and `first point` of trip $(i+1)$ has been added, effectiely, makind `trajectory_id` immmaterial in this purpose. 
* For an individual the distance travelled is the displacement summed up onver all consecutive pairs (maintaining `chronilogical` order)
* Successive time intervals are so small that we `approximate` the displacement` as the `distance` 



# Implemetation Details 

* For the implemetatoin, `multiprocesing` has been used. Using a `Pool()`, the processes of computing distance have been `started` simultaneously for each individual 
* Tere is a row with a `faulty` latitude value. Dropped that row.
* It takes `~2 minutes 53 seconds` on the local machine to return the distances

# Part 2
* I decided to look at the variation of `crowding density` in $Bejing$ $City$  as a a function of time. I grouped that data (ignoring the `date`) into 
* Hence I obtained `12` haeat maps over the day. The total size `~653.9 MB` and took mre than `30 mins` to process  the `maps` while using `multiprocessing`. 
  
### Here are the results ( in order `(00:00:00-02:00:00)` hrs, .......`(22:00:00-00:00:00)` hrs

<p align="center">
<img width="400" alt="Screenshot 2023-04-10 at 1 34 01 PM" src="https://user-images.githubusercontent.com/97736991/230856649-373df9df-4625-4325-8dd4-1db07e165705.png">
<img width="400" alt="Screenshot 2023-04-10 at 1 34 32 PM" src="https://user-images.githubusercontent.com/97736991/230856754-00cdc70b-9c4f-4fe5-9ecf-9ab3f3e3da07.png">
<img width="400" alt="Screenshot 2023-04-10 at 1 36 03 PM" src="https://user-images.githubusercontent.com/97736991/230857011-da1ea58c-d0f5-4384-9eee-636f3bb6bd85.png">
<img width="400" alt="Screenshot 2023-04-10 at 1 36 29 PM" src="https://user-images.githubusercontent.com/97736991/230857071-3c8d6e28-cc47-480a-a0f7-4cdfcc43e9d3.png">
<img width="400" alt="Screenshot 2023-04-10 at 1 36 53 PM" src="https://user-images.githubusercontent.com/97736991/230857148-54c44f94-6237-4a4a-948c-14b8eeed0160.png">
<img width="400" alt="Screenshot 2023-04-10 at 1 37 42 PM" src="https://user-images.githubusercontent.com/97736991/230857274-d1904e25-bb9e-4e02-b6cb-a130a29a45ec.png">
<img width="400" alt="Screenshot 2023-04-10 at 1 38 06 PM" src="https://user-images.githubusercontent.com/97736991/230857345-e17b41c3-c399-4ed8-a167-52391600b377.png">
<img width="400" alt="Screenshot 2023-04-10 at 1 38 36 PM" src="https://user-images.githubusercontent.com/97736991/230857412-85ec1b08-10c7-4c51-a9c0-fc7c56ec6d2a.png">
<img width="400" alt="Screenshot 2023-04-10 at 1 38 54 PM" src="https://user-images.githubusercontent.com/97736991/230857458-bd0adb2d-c554-4d65-876e-9e2edaab5f55.png">
<img width="400" alt="Screenshot 2023-04-10 at 1 39 10 PM" src="https://user-images.githubusercontent.com/97736991/230857511-3660cfe7-14eb-4476-bf38-e49eb657759e.png">
<img width="400" alt="Screenshot 2023-04-10 at 1 39 27 PM" src="https://user-images.githubusercontent.com/97736991/230857572-655d2574-4cc1-44fd-94e5-72f026212731.png">
<img width="400" alt="Screenshot 2023-04-10 at 1 40 13 PM" src="https://user-images.githubusercontent.com/97736991/230857679-1283b5b1-5af0-4455-8655-2eeb242153ac.png"></p>

* Once direct conclusion from this is that, unsurprisingly, the `heat` map changes with time but the city center is at all times the hotspot
* On zooming in the `heat` map we can also see
<p align="center">
<img width="400" alt="Screenshot 2023-04-10 at 4 36 19 PM" src="https://user-images.githubusercontent.com/97736991/230890310-5aeb08b9-1c6a-4b55-8692-1f3f673c9a21.png">
  <img width="400" alt="Screenshot 2023-04-10 at 4 41 06 PM" src="https://user-images.githubusercontent.com/97736991/230890947-f6912cbe-b768-4bb0-a6f4-910812f319e7.png">
</p>
* We can conclude that not all roads are equally conjested, as a result of factors like width  and connectivity 



# Implementation Details:
* Parsing the date-time values takes a lot of time. There were some `faulty` data-time values too.
# Part 3 


* I had ideas like: 
  *  Optimising Advertising locations based on crowding data 
  *  Tracking spread of contagious diseases like COVID 19
  *  Using tracking data to optimise routes for Fast delivery services (Especially companies offereing 10 minutes delivery) 
  *  Or designing public transport routes 
  *  Using traffic data to decide necessary constructions like divergences to divert trafic 
  
We can use the data to 
* For the purpose of traffic monitoring, ee should analyse the data in time slots because locations at two completely unrelated times shouldn't give much conclustion. First step should be the standard data cleaning step. Heat maps can be used to visualise the crowded spots in the city. For analysing the data more computationally, we can use clustering algorithmns like `k means clustering`. This will give us the location of the hotspots. It can be manually inspected what is the flow of traffic in this area, what could be the reaosnfor such crowding and then it can be decided to take suitable measures. 



