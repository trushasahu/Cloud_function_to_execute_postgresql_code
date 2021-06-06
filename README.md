# Cloud_function_to_execute_postgresql_code
Create one cloud function to connect cloud postgresql database and execute the sql/proc code

## Step1: Create one service account or use the existing one
Existing SA like '****@developer.gserviceaccount.com' 

and add the below role to this SA.

Cloud SQL > Cloud SQL Client

## Step2: Create cloud function by adding python script to invoke sql and execute the function.
create one cloud function name as 'function-to-psql' with below details:

	trigger type as : 'HTTP' 
	
	select authentication as : require
	
	advanced->service account-> provide/select "cloud SQL client" role service account i.e. created from above steps
	
	copy the main.py code from this repository into the function main.py block :- this contain main code to connect and execute the postgresql code
	
	copy the requirements.txt code from this repository into the function requirements.txt block :-this code executed first to build the dependencies
	
## Step3: Create a cloud scheduler to invoke the cloud function
create one sheduler job as 'scheduler-invoke-cloud-function' with below details:

	create one service account and provide the "cloud function invocker" role

	target type as: HTTP
	
	URL of the trigger URL of cloud function : https://europe-west2-third-campus-303308.cloudfunctions.net/function-to-psql
	
	HTTP method as :"GET"
	
	auth header as :"Add OIDC token" 
	
	scheduling interval depend on your requirement.every minute(* * * * *)
	













