# hmpps-probation-load-testing

## Prep for running load test - Connect to DB and get auth cookie:
To kick off the load tests you will need to do the following:

1. Port forward to [Access the DEV RDS Database](https://user-guide.cloud-platform.service.justice.gov.uk/documentation/other-topics/rds-external-access.html#accessing-your-rds-database)
2. Go to `Approved Premises` web application and grab the `connection.sid` cookie's value: 
  * Go here in Google Chrome: https://approved-premises-test.hmpps.service.justice.gov.uk
  * Log in
  * Right-click browser > Inspect
  * Go to `Application` tab > `Storage` in left nav > Expand `Cookies`
  * Find the `connect.sid` cookie in the list and copy its' value from the `Value` column
  * Copy the value for later step

## Run load tests in Terminal:
1. Change directory in a terminal and navigate to this repo's root folder
2. Run this command (and swap out variables below for real values - see `Prep for running load test` for how to get the value for `auth_cookie_value` and the rest our k8s secrets):
```
./gradlew gatlingRun --simulation uk.gov.justice.digital.hmpps.team.cas.simulations.BookingMadeSimulation -Dprofile=test -Dprotocol=https -Ddomain=approved-premises-test.hmpps.service.justice.gov.uk -Ddb_port=5432 -Ddb_name=<db_name_value> -Ddb_username=<db_username_value> -Ddb_password=<db_password_value> -DconnectSidCookieValue=<auth_cookie_value>
```
