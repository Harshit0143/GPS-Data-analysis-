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
# Part (3) 


* I had ideas like: 
  *  Optimising Advertising locations based on crowding data 
  *  Tracking spread of contagious diseases like COVID 19
  *  Using tracking data to optimise routes for Fast delivery services (Especially companies offereing 10 minutes delivery) 
  *  Or designing public transport routes 
  *  Using traffic data to decide necessary constructions like divergences to divert trafic 
  
We can use the data to 
* For the purpose of traffic monitoring, ee should analyse the data in time slots because locations at two completely unrelated times shouldn't give much conclustion. First step should be the standard data cleaning step. Heat maps can be used to visualise the crowded spots in the city. For analysing the data more computationally, we can use clustering algorithmns like `k means clustering`. This will give us the location of the hotspots. It can be manually inspected what is the flow of traffic in this area, what could be the reaosnfor such crowding and then it can be decided to take suitable measures. 
