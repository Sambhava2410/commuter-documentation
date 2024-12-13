<script>
    if (!localStorage.getItem('loggedIn')) {
        window.location.href = "login.html"; // Redirect to login page if not logged in
    }
</script>

# Inventory Fetch Logic

<summary>This document outlines the inventory retrieval logic for various OTAs, including Mantis, Bitla, and ITS. It provides sample code and details about the third-party APIs used for fetching services. Additionally, it includes execution time estimates for retrieving data for a single day and for a 30-day period.</summary>

## Mantis

<details>

    <summary><strong>Mantis Inventory Fetch Logic</strong></summary>
    
    <strong><h3>Logic Summary</h3></strong>
    <strong>Function: fetch_and_attach_bus_route_id_by_state()</strong>
    <p>This function is responsible for fetching bus inventory data for the next 30 days from a specified date and attaching the necessary route IDs to services in the database.<p>
    <li>The core flow of the function is as follows:</li>
    <ol>
        <li><strong>Logging Initialization:</strong>
            <ul>
                <li>The function starts by recording the execution timestamp in a log file (mantis_execution_log.txt) to track when the script begins and ends.</li>
            </ul>
        </li>
        <li><strong>Fetching City Pairs:</strong>
            <ul>
                <li>The function retrieves all city pairs (MentisCityPairs) from the database where a service is marked as found (service_found=True). These pairs represent the routes for which bus services are being fetched.
                last updated city pairs count - 46805
                </li>
            </ul>
        </li>
        <li><strong>Loop for 30 Days:</strong>
            <ul>
                <li>The script will iterate over the next 30 days (from a given start date, suppose, "2024-12-14") and for each day, it will:</li>
                <ol>
                    <li>Prepare a formatted date for the journey.</li>
                    <li>For each city pair (from city to city), make an GET API request to the Mantis Search API to fetch available bus routes.</li>
                </ol>
            </ul>
        </li>
        <li><strong>API Request to Mantis:</strong>
            <ul>
                <li>A GET request is made to the Mantis Search API with the fromCityId, toCityId, and journeyDate parameters.</li>
                <li>If the response status is 200 OK, the function processes the buses returned in the response.</li>
            </ul>
        </li>
        <li><strong>Token Management:</strong>
            <ul>
                <li>The function uses an access token to authenticate API requests. After every 3000 requests, a new access token is fetched using a helper function <code>fetch_access_token()</code>, ensuring the token is refreshed and valid.</li>
            </ul>
        </li>
        <li><strong>Processing Bus Data:</strong>
            <ul>
                <li>For each bus in the response:</li>
                <ol>
                    <li>The unique bus_route_id (RouteBusId) is fetched.</li>
                    <li>The bus type is checked to determine whether it's an AC bus.</li>
                    <li>Additional bus details such as departure time, arrival time, duration, operator name, price, and pickup/drop-off points are collected.</li>
                    <li>These details are then prepared to be saved in the database:</li>
                    <ul>
                        <li><code>updated_at</code>: Timestamp of the update.</li>
                        <li><code>from_city_name</code>, <code>to_city_name</code>: City names.</li>
                        <li><code>bus_route</code>: The unique bus route ID.</li>
                        <li><code>ac</code>: Boolean indicating whether the bus is AC.</li>
                        <li>Other relevant information is also captured in the meta field to store additional metadata.</li>
                    </ul>
                </ol>
            </ul>
        </li>
        <li><strong>Database Updates:</strong>
            <ul>
                <li>Before creating or updating a record, the function checks if the service already exists in the MentisRoutePricing table for the given from_city_id, to_city_id, journey_date, and bus_route_id.</li>
                <li>If there are duplicate entries for the same route, previous entries are marked as deleted (<code>is_deleted=True</code>).</li>
                <li>The function then uses <code>update_or_create</code> to either update an existing record or create a new one if no matching record is found on the basis of these primary keys <code>from_city_id, to_city_id, journey_date, and bus_route_id.</code></li>
            </ul>
        </li>
        <li><strong>Log Progress:</strong>
            <ul>
                <li>After processing each city pair, the script updates the <code>total_inventory_fetched_count</code>, printing the progress to the console.</li>
                <li>The script also logs the time when it ends, completing the fetching of bus routes for the 30-day period.</li>
            </ul>
        </li>
    </ol>

       


    <strong>Performance Estimate</strong>
    <ul>
    <li><strong>For 1 day inventory: ~3 hours 20 minutes</strong></li>
    <li><strong>For 30 days inventory: ~4 Days</strong></li>
    </ul>
    <br>

    ```python
    import requests
    from datetime import datetime, timedelta

    BASE_URL = "https://partnerapi.iamgds.com/ota/Search"

    def fetch_mantis_inventory(days=30):
        """Fetch bus routes for the next `days` days and update the database."""
        start_date = datetime.strptime("2024-12-14", "%Y-%m-%d")
        city_pairs = MentisCityPairs.objects.filter(service_found=True)
        token_count = 0
        headers = {"accept": "application/json", "access-token": "TOKEN"}

        for i in range(days):
            journey_date = (start_date + timedelta(days=i)).strftime("%Y-%m-%d")
            for city in city_pairs:
                url = f"{BASE_URL}?fromCityId={city.from_city_id}&toCityId={city.to_city_id}&journeyDate={journey_date}"
                response = requests.get(url, headers=headers)
                token_count += 1

                # Refresh token every 3000 requests
                if token_count == 3000:
                    headers["access-token"] = fetch_access_token()
                    token_count = 0

                if response.status_code == 200:
                    process_bus_data(response.json(), journey_date, city)

    def process_bus_data(data, journey_date, city):
        """Process and save bus data from the response."""
        buses = data.get("data", {}).get("Buses", [])
        if buses:
            for bus in buses:
                values = {
                    'updated_at': datetime.now(),
                    'from_city_name': bus.get("FromCityName"),
                    'to_city_name': bus.get("ToCityName"),
                    'bus_route': bus.get("RouteBusId"),
                    'ac': bus.get("BusType", {}).get("IsAC") == "AC",
                    'pickup_points': bus.get("Pickups"),
                    'drop_points': bus.get("Dropoffs"),
                    'price': bus.get("BusStatus"),
                    'operator_name': bus.get("CompanyName"),
                    'duration': bus.get("Duration"),
                    'arrival_time': bus.get("ArrTime"),
                    'dept_time': bus.get("DeptTime"),
                }

                # Save/update the bus route data
                MentisRoutePricing.objects.update_or_create(
                    from_city_id=city.from_city_id,
                    to_city_id=city.to_city_id,
                    journey_date=journey_date,
                    bus_route=bus.get("RouteBusId"),
                    defaults=values,
                )

    [Git Repository](https://tinyurl.com/4hc3y4f3)
    ```
</details>

## ITS

<details>

    <summary><strong>ITS Inventory Fetch Logic</strong></summary>
    
    <strong><h3>Logic Summary</h3></strong>
    <strong>Function: <code>fetch_bus_routes()</code></strong>
    <p>This function is responsible for fetching available bus routes for the next 30 days for city pairs from the CityPair model and storing them in the BusRoute model under its app.</p>
    <li>The core flow of the function is as follows:</li>
    <ol>
        <li><strong>Logging and Initialization:</strong>
            <ul>
                <li>The script records the start and end time of the execution in a log file (its_one_day_execution_log.txt) to track the execution timeline.</li>
                <li>It also initializes variables to track inventory count and handle any API request failures.</li>
            </ul>
        </li>
        <li><strong>Fetching City Pairs:</strong>
            <ul>
                <li>The script retrieves all city pairs from the CityPair model. (count - 121,612)</li>
                <li>For each city pair, a journey date is set, and an API call is made to fetch available routes for that date.</li>
            </ul>
        </li>
        <li><strong>Making API Request:</strong>
            <ul>
                <li>The script makes a POST request to the API endpoint <strong>https://itsplatform.itspl.net/api/GetAvailableRoutes</strong>, passing the city pair details and journey date.</li>
                <li>If the API response is successful (status code 200), it proceeds with processing the data.</li>
            </ul>
        </li>
        <li><strong>Processing API Response:</strong>
            <ul>
                <li>The script processes the route data by extracting and formatting important details like route time, city time, arrival time, and other parameters.</li>
                <li>It then stores or updates the data in the BusRoute model using <strong>update_or_create</strong> based on <code>city pair IDs, route ID, and journey date</code>.</li>
            </ul>
        </li>
        <li><strong>Exception Handling:</strong>
            <ul>
                <li>If any errors occur during the API request or while processing the data, the script logs the exception and continues processing other city pairs.</li>
            </ul>
        </li>
        <li><strong>Final Logging:</strong>
            <ul>
                <li>At the end of the script, the end time of the execution is recorded in the log file.</li>
            </ul>
        </li>
    </ol>

    <strong>Executing Time Estimate</strong>
    <ul>
    <li><strong>For 1 day inventory: ~3 hours 20 minutes</strong></li>
    <li><strong>For 30 days inventory: ~4 Days</strong></li>
    </ul>
    <br>

    ```python
    import requests
    from datetime import datetime, timedelta

    def fetch_bus_routes():
        log_file_path = os.path.join(os.path.dirname(os.path.abspath(__file__)), "its_one_day_execution_log.txt")
        start_time = datetime.now()
        
        with open(log_file_path, "a") as log_file:
            log_file.write(f"Script started at: {start_time.strftime('%Y-%m-%d %H:%M:%S')}\n")
        
        start_date = datetime.strptime("2024-12-15", "%Y-%m-%d")
        city_pairs = CityPair.objects.all()
        
        for pair in city_pairs:
            try:
                url = "https://itsplatform.itspl.net/api/GetAvailableRoutes"
                payload = json.dumps({
                    "fromID": pair.from_city_id,
                    "toID": pair.to_city_id,
                    "journeyDate": start_date.strftime("%d-%m-%Y"),
                    "verifyCall": "VERIFY KEY",
                })
                headers = {"Content-Type": "application/json"}
                response = requests.post(url, headers=headers, data=payload)
                
                if response.status_code == 200:
                    data = response.json().get("data", {}).get("AllRouteBusLists", [])
                    
                    for route_data in data:
                        defaults = {
                            "company_id": route_data.get("CompanyID"),
                            "from_city_name": route_data.get("FromCityName"),
                            "to_city_name": route_data.get("ToCityName"),
                            "route_time": route_data.get("RouteTime"),
                            "kilometer": route_data.get("Kilometer"),
                            "bus_type_name": route_data.get("BusTypeName"),
                            "ac_seat_rate": route_data.get("AcSeatRate"),
                            "non_ac_seat_rate": route_data.get("NonAcSeatRate"),
                            "boarding_points": route_data.get("BoardingPoints"),
                            "dropping_points": route_data.get("DroppingPoints"),
                        }
                        BusRoute.objects.update_or_create(
                            from_city_id=route_data.get("FromCityId"),
                            to_city_id=route_data.get("ToCityId"),
                            route_id=route_data.get("RouteID"),
                            journey_date=datetime.strptime(route_data.get("BookingDate"), "%d-%m-%Y").date(),
                            defaults=defaults,
                        )
            except Exception as e:
                print("Exception:", e)
        
        end_time = datetime.now()
        with open(log_file_path, "a") as log_file:
            log_file.write(f"Script ended at: {end_time.strftime('%Y-%m-%d %H:%M:%S')}\n")

    [Git Repository](https://github.com/Sambhava2410/commuter_apis/blob/develop_v3_copy/its/scripts/its_morning_script.py)
    ```
</details>

## Bitla

<details>

    <summary><strong>Bitla Inventory Fetch Logic</strong></summary>
    
    <strong><h3>Logic Summary</h3></strong>
    <strong>Function: operator_wise_services(op_id)</strong>
    <p>This function fetches operator-specific service schedules for the next 30 days from an external API and updates the NewBitlaServices model with the fetched data, ensuring that duplicate or outdated records are removed.</p>
    <li>The core flow of the function is as follows:</li>
    <ol>
        <li><strong>Logging and Initialization:</strong>
            <ul>
                <li>The function begins by iterating over the next 30 days, starting from the current date, and generates the appropriate URL for each day.</li>
                <li>For each date, the function makes a GET request to the API to fetch the schedule data for the specified operator.</li>
            </ul>
        </li>
        <li><strong>Processing API Response:</strong>
            <ul>
                <li>The function checks whether the response contains valid schedule data and ignores entries with statuses such as "Unavailable-Cancelled" or "Unavailable-SoldOut".</li>
                <li>For each valid schedule, the function extracts essential details such as origin ID, destination ID, route name, travel date, bus type, departure and arrival times, and fare information.</li>
            </ul>
        </li>
        <li><strong>Handling Bus Information:</strong>
            <ul>
                <li>If bus type information is available, it is parsed to extract details such as seat type and seat layout.</li>
            </ul>
        </li>
        <li><strong>Service Record Management:</strong>
            <ul>
                <li>The function checks for existing service records in the NewBitlaServices model for the same service ID, route ID, travel ID, and city pair. If duplicates are found, it deletes them, keeping only the first record.</li>
                <li>It then updates or creates a new service record in the database using <strong>update_or_create</strong> with the extracted details.</li>
            </ul>
        </li>
        <li><strong>Exception Handling:</strong>
            <ul>
                <li>If an exception occurs during the execution, the error is logged and the function proceeds with the next iteration.</li>
            </ul>
        </li>
    </ol>

    <strong>Function: operator_wise_inventory_store()</strong>
    <p>This function executes the <code>operator_wise_services</code> function for each operator in the <code>BitlaOperator</code> model and logs the start and end time of the script execution.</p>
    <li>The core flow of the function is as follows:</li>
    <ol>
        <li><strong>Logging and Initialization:</strong>
            <ul>
                <li>The function records the start and end time of the execution in a log file (<code>bitla_30_day_execution_log.txt</code>) to track the execution timeline.</li>
                <li>It fetches all operators from the <code>BitlaOperator</code> model to process their schedules.</li>
            </ul>
        </li>
        <li><strong>Processing Each Operator:</strong>
            <ul>
                <li>For each operator, the function calls <code>operator_wise_services</code> to fetch and update the service schedules for the next 30 days.</li>
            </ul>
        </li>
        <li><strong>Final Logging:</strong>
            <ul>
                <li>At the end of the execution, the script logs the end time of the process to track the completion time.</li>
            </ul>
        </li>
    </ol>

    <strong>Executing Time Estimate</strong>
    <ul>
    <li><strong>For 1 day inventory: ~3 hours 20 minutes</strong></li>
    <li><strong>For 30 days inventory: ~4 Days</strong></li>
    </ul>
    <br>

    ```python
    def operator_wise_services(op_id):
    try:
        headers = {
            "api-key": "KEY",
        }
        for i in range(1, 30):
            start_date = current_date + timedelta(days=i)
            formatted_date = start_date.strftime("%Y-%m-%d")
            url = f"https://gds.ticketsimply.com/gds/api/operator_schedules/{op_id}/{formatted_date}.json"
            schedule_details_response = requests.get(url, headers=headers)
            if "result" in schedule_details_response.json():
                schedule_details_json = schedule_details_response.text
                schedule_details_json = complex_json_to_normal_json(schedule_details_json)
                for schedule in schedule_details_json:
                    if schedule.get("status") != "Unavailable-Cancelled" and schedules.get("status") != "Unavailable-SoldOut":
                        origin_id = schedule.get("origin_id")
                        destination_id = schedule.get("destination_id")
                        schedule_id = schedule.get("id")
                        name = schedule.get("name")
                        travel_date = schedule.get("travel_date")
                        operator_service_name = schedule.get("operator_service_name")
                        route_id = schedule.get("route_id")
                        bus_info = schedule.get("bus_type")
                        if bus_info:
                            details = bus_info.split(", ")
                            seat_type = details[1]
                            seat_layout_type = details[0]
                        dep_time = schedule.get("dep_time")
                        arr_time = schedule.get("arr_time")
                        duration = schedule.get("duration")
                        if duration:
                            duration = duration.split(":")
                            duration = int(duration[0]) * 60 + int(duration[1])
                        fare_str = schedule.get("fare_str")
                        boarding_stages = schedule.get("boarding_stages")
                        dropoff_stages = schedule.get("dropoff_stages")
                        is_ac_bus = schedule.get("is_ac_bus")
                        travel_id = schedule.get("travel_id")
                        service_id = f"{schedule_id}"
                        values = {
                            "route_id": route_id,
                            "travel_id": travel_id,
                            "route": name,
                            "operator_name": operator_service_name,
                            "bus_type": seat_type,
                            "seat_layout_type": seat_layout_type,
                            "start_time": dep_time,
                            "end_time": arr_time,
                            "duration": duration,
                            "price": fare_str,
                            "pickup_points": boarding_stages,
                            "drop_points": dropoff_stages,
                            "is_ac": is_ac_bus,
                        }
                        meta_fields = {
                            key: value
                            for key, value in schedule.items()
                            if key not in values
                        }
                        values["meta"] = meta_fields
                        existing_services = NewBitlaServices.objects.filter(
                            service_id=service_id,
                            route_id=route_id,
                            travel_id=travel_id,
                            from_city_id=origin_id,
                            to_city_id=destination_id,
                            travel_date=travel_date,
                        )

                        if existing_services.exists():
                            # Retain only one record and delete duplicates
                            service_to_keep = existing_services.first()  # Keep the first record
                            duplicates = existing_services.exclude(id=service_to_keep.id)
                            duplicates.delete() 
                        bitla_obj, created = NewBitlaServices.objects.update_or_create(
                            service_id=service_id,
                            route_id=route_id,
                            travel_id=travel_id,
                            from_city_id=origin_id,
                            to_city_id=destination_id,
                            travel_date=travel_date,
                            defaults=values,
                        )
    except Exception as e:
        print(e)


    def operator_wise_inventory_store():
        log_file_path = os.path.join(os.path.dirname(os.path.abspath(__file__)), "bitla_30_day_execution_log.txt")

        # Record the start time
        start_time = datetime.now()
        with open(log_file_path, "a") as log_file:
            log_file.write(f"Script started at: {start_time.strftime('%Y-%m-%d %H:%M:%S')}\n")
        operators = BitlaOperator.objects.all()
        for op in operators:
            service = operator_wise_services(op.travel_id)
        end_time = datetime.now()
        with open(log_file_path, "a") as log_file:
            log_file.write(f"Script ended at: {end_time.strftime('%Y-%m-%d %H:%M:%S')}\n")
    [Git Repository](https://github.com/Sambhava2410/commuter_apis/blob/develop_v3_copy/bitla/scripts/service_store.py)
    ```
</details>

## SQL Queries to check services count:

<details>
    <p>
    It is essential to regularly verify the existence of services in your system to ensure that your inventory is up to date. To do this, you should run the following SQL queries every few days to check the number of services for different dates. This will help you track if any services are missing or if there are discrepancies in your data.
    For optimal performance, you can execute these queries in multiple threads to reduce the overall execution time, especially when dealing with large datasets.
    </p>
    <summary>Click to expand</summary>

        <ol>
            <li><strong>To check the count of services in <code>bitla_newbitlaservices</code>:</strong></li>
        </ol>
        <pre>
            <code>
    SELECT travel_date, COUNT(*) AS total_services
    FROM bitla_newbitlaservices 
    GROUP BY travel_date;
                </code>
            </pre>

            <ol>
                <li><strong>To check the count of services in <code>mentis_mentisroutepricing</code>:</strong></li>
            </ol>
            <pre>
                <code>
    SELECT journey_date, COUNT(*) 
    FROM mentis_mentisroutepricing 
    GROUP BY journey_date;
                </code>
            </pre>

            <ol>
                <li><strong>To check the count of services in <code>its_busroute</code>:</strong></li>
            </ol>
            <pre>
                <code>
    SELECT journey_date, COUNT(*) 
    FROM its_busroute ib 
    GROUP BY journey_date;
                </code>
            </pre>
</details>