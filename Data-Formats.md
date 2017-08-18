**mapping** is our database
***
**people_count**: to store the number of people in each station at any time
* _id: ObjectId
* day: int32, 
	* to indicate which day in a week (value in [0, 7=0])
* time: int32, 
	* to indicate which five-minute period starting from 8 AM each day. 
	* For example, 0 = 8:00 AM, 1 = 8:05 AM, ..., and etc.
* count: float64, 
	* the estimated number of people in the station at *day*, *time*.
***
**people_activity**: to store people's activity such as coordinates, flow
* _id: ObjectId
* time_stamp: int32
	* it indicates the timestamp of video in seconds
* frame_number: int32
	* it indicates the frame index of the current frame 
* floor: int32
* map_data: [int32, int32, int32, double, double]
	* Each row contains the crowd and flow information on the floor map
    * [x, y, number of person, flow magnitude, flow direction]
* big_clusters: [int32, int32, double, double, double, int32]
    * Each row is a cluster found on the floor map
    * [cluster’s x coordinate, cluster’s y coordinate, flow magnitude, flow direction, cluster’s density, cluster’s area in square meters]   
    	* flow magnitude: int
			* it means the speed of the flow, with pixel as the unit, the range is about [0, 10]
		* flow direction: float
			* it means the direction of the flow, with degree as the unit, the range is [0, 360]
* small_clusters: [int32, int32, double, double, double, int32, string]
	* Each row is a smaller cluster segmented from the big clusters
    * [cluster’s x coordinate, cluster’s y coordinate, flow magnitude, flow direction, density, exit ID] 
    * cluster area of each small cluster is fixed to 9 square meters
* ppl_cnt: int32 
	* The total number of people on the floor
***
**tickets_all**: to store ticketing data of passengers for all stations
* _id: ObjectId
* in_station: string, 
	* the station that the passenger got in
* out_station: string, 
	* the station that the passenger got out
* in_time: int32, 
	* the timestamp that the passenger got in
* out_time: int32, 
	* the timestamp that the passenger got out
* in_gate: string or null, 
	* the ticket barrier that the passenger got in
* out_gate: string or null, 
	* the ticket barrier that the passenger got out
***
**tickets_adm**: to store ticketing data for passengers at station ADM
* _id: ObjectId
* time_stamp: int32, 
	* the timestamp when the record was generated
* gate: int32, 
	* the ticket barrier at which the record was generated
* io: boolean, 
	* True when the passenger is getting into the station, and vice versa

