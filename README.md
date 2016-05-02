# AutomationExercisePart2

       Pre-requisites to run the code: SoapUI

-	Project name “AutomationExercisePart2.xml”. Under this project I have created 1 test Suite named AutomationExercisePart2 and 2 test cases.

Test case 1: GetAllStations&CheckHyattAustin
https://api.data.gov/nrel/alt-fuel-stations/v1/nearest.json?api_key=fcflhx3qKi54i86kKfJpc4GNRLnOdzdAL8FNlAb1&location=Austin+TX
Test Step 1 is “AllFuelStationsAustin” - From the response, I get all the stations.
Assertion: I assert that results are returned
Test Step 2 is groovy script “AssertHyatt&SaveStationID” – In this step, from the response I get in step 1, I iterate over the response and filter out all the station names for which the env_network = “ChargePoint Network” and put this in list
For HYATT AUSTIN, save the stationID in a TESTSUITE level Property
Assertion: Assert that HYATT AUSTIN is there in the list
Save the station id in TestSuite level property so that I can use this in another test case
Test case 2: VerifyStreetAddressForHyattAustin
Resource: http://developer.nrel.gov/api/alt-fuel-stations/v1/
Child Resource: {id}.json
http://developer.nrel.gov/api/alt-fuel-stations/v1/{id}.json
id value is taken from the TESTSuite property station id by setting the resource parameters like this ${#TestSuite#stationID}
From the response, I make the following assertions:
assert jsonResponse.alt_fuel_station.station_name == "HYATT AUSTIN"
assert jsonResponse.alt_fuel_station.street_address == "208 Barton Springs Rd"
assert jsonResponse.alt_fuel_station.city == "Austin"
assert jsonResponse.alt_fuel_station.state == "TX"
assert jsonResponse.alt_fuel_station.zip == "78704"
