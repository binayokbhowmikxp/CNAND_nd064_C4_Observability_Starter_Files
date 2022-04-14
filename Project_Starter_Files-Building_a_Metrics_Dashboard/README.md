**Note:** For the screenshots, you can store all of your answer images in the `answer-img` directory.

## Verify the monitoring installation

*TODO:* run `kubectl` command to show the running pods and services for all components. Take a screenshot of the output and include it here to verify the installation
![Screenshot 2022-04-13 at 2 12 28 AM](https://user-images.githubusercontent.com/40661295/163050352-f2aafb39-3b7e-4ce0-8936-bced222f8636.png)


## Setup the Jaeger and Prometheus source
*TODO:* Expose Grafana to the internet and then setup Prometheus as a data source. Provide a screenshot of the home page after logging into Grafana.

![Screenshot 2022-04-12 at 2 36 02 AM](https://user-images.githubusercontent.com/40661295/163050605-6e074bc3-60a7-4643-bf1e-d640f11c096f.png)

![Screenshot 2022-04-12 at 2 35 11 AM](https://user-images.githubusercontent.com/40661295/163050635-f9884a01-824a-4d08-95ed-a1368d706f81.png)


## Create a Basic Dashboard
*TODO:* Create a dashboard in Grafana that shows Prometheus as a source. Take a screenshot and include it here.

![Screenshot 2022-04-12 at 2 42 57 PM](https://user-images.githubusercontent.com/40661295/163052117-4decc806-96e5-450a-b058-bee261520125.png)


## Describe SLO/SLI
*TODO:* Describe, in your own words, what the SLIs are, based on an SLO of *monthly uptime* and *request response time*.

A Service-Level Indicator (SLI) is a specific metric used to measure the performance of a service.

Sometimes the term SLI is used to refer to the general metric—such as uptime or latency. But really what we need in the end is an actual measurement. For example, suppose that your team has the following SLO: The application will have an uptime of 99.9% during the next year.

In this case, your SLI would be the actual measurement of the uptime. Perhaps during that year, you actually achieved 99.5% uptime or 97.3% uptime. These measurements are your SLIs—they indicate the level of performance your service actually exhibited, and show you whether you achieved your SLO (in this case, the SLIs show that performance fell short of your objective).

## Creating SLI metrics.
*TODO:* It is important to know why we want to measure certain metrics for our customer. Describe in detail 5 metrics to measure these SLIs. 

Service is defined in terms of four core properties, called the Four Golden Signals:

Latency — The time taken to serve a request (usually measured in ms).
Traffic — The amount of stress on a system from demand (such as the number of HTTP requests/second).
Errors — The number of requests that are failing (such as number of HTTP 500 responses).
Saturation — The overall capacity of a service (such as the percentage of memory or CPU used).

We can use the below key indicators (specific) to measure SLI:

* Measure by response type and service: Flask HTTP requests status 200, 500, 400 (Errors)
* Failed responses per second (Errors, Traffic, Saturation)
* Uptime: frontend, trial, backend (Latency, Traffic, Saturation, Errors)
* Pods health: Pods not ready (Latency / Errors)
* Pods health: Pod restarts by namespace (Could be caused by any number of things : Errors in applications, traffic)
* Average Response time (Latency, Traffic, Saturation)

## Create a Dashboard to measure our SLIs
*TODO:* Create a dashboard to measure the uptime of the frontend and backend services We will also want to measure to measure 40x and 50x errors. Create a dashboard that show these values over a 24 hour period and take a screenshot.


![Screenshot 2022-04-13 at 9 21 57 PM](https://user-images.githubusercontent.com/40661295/163221385-2af8ec4c-0caf-4a09-849f-144b0e26f492.png)


![Screenshot 2022-04-13 at 9 22 21 PM](https://user-images.githubusercontent.com/40661295/163221662-3d12e790-355f-46e5-bbf9-a05ce36b4de5.png)

## Tracing our Flask App
*TODO:*  We will create a Jaeger span to measure the processes on the backend. Once you fill in the span, provide a screenshot of it here. Also provide a (screenshot) sample Python file containing a trace and span code used to perform Jaeger traces on the backend service.

![Screenshot 2022-04-12 at 5 09 04 PM](https://user-images.githubusercontent.com/40661295/163056227-c613bd99-b79d-485f-bbe0-fae0c03fba77.png)


The sample code is as below:

![Screenshot 2022-04-13 at 2 49 01 AM](https://user-images.githubusercontent.com/40661295/163056521-02420493-7d32-48dc-8281-c20132f4e57e.png)



## Jaeger in Dashboards
*TODO:* Now that the trace is running, let's add the metric to our current Grafana dashboard. Once this is completed, provide a screenshot of it here.

![Screenshot 2022-04-13 at 10 38 03 AM](https://user-images.githubusercontent.com/40661295/163104587-cfe49000-12e0-4dd8-86c2-57fbdbe8ed43.png)


## Report Error
*TODO:* Using the template below, write a trouble ticket for the developers, to explain the errors that you are seeing (400, 500, latency) and to let them know the file that is causing the issue also include a screenshot of the tracer span to demonstrate how we can user a tracer to locate errors easily.

![Screenshot 2022-04-13 at 10 18 24 PM](https://user-images.githubusercontent.com/40661295/163230575-8d1d031f-bc6c-4242-bb85-46e8138b7382.png)


TROUBLE TICKET

Name: Error on backend/app/app.py"

Date: April 13 2022, 22:08:34.720

Subject: cannot update backend data 

Affected Area:   File "/app/app.py", line 99, in add_star

Severity: High

Description: TypeError: There is an issue with the format of the POST data


## Creating SLIs and SLOs
*TODO:* We want to create an SLO guaranteeing that our application has a 99.95% uptime per month. Name four SLIs that you would use to measure the success of this SLO.

We need to focus on the below SLO:

* Latency: The response time of requests should less than 30ms within a month.
* Failure rate: Ensure that the status code 2xx rates are around 97%.
* Uptime: Uptime need to be approximate 99 percent within a month and response time should be around 500 milliseconds.
* Saturation: he overall capacity of a service (such as the percentage of memory or CPU used). CPU should be less than 90% within a month.

## Building KPIs for our plan
*TODO*: Now that we have our SLIs and SLOs, create a list of 2-3 KPIs to accurately measure these metrics as well as a description of why those KPIs were chosen. We will make a dashboard for this, but first write them down here.

* Latency: Response time. - Needed to measure how responsive the application are.
* Failure rate: Errors per second / response rate per second. - It is important to understand what kind of errors are happening in the application. This can be done with Jaeger Tracing
* Uptime: Sucessful requests during pod uptime. This is needed to measure availabilty of the pod itself.
* Network capcity: successful request per second / request per second. To measure any network bottlenect 
* Resource capcity: CPU, RAM usage per pod. . Needed to measure saturation

## Final Dashboard
*TODO*: Create a Dashboard containing graphs that capture all the metrics of your KPIs and adequately representing your SLIs and SLOs. Include a screenshot of the dashboard here, and write a text description of what graphs are represented in the dashboard.  

![Screenshot 2022-04-14 at 12 17 16 AM](https://user-images.githubusercontent.com/40661295/163249508-c7e49923-de9b-481a-a722-0d7ebf150717.png)

![Screenshot 2022-04-14 at 12 17 35 AM](https://user-images.githubusercontent.com/40661295/163249521-ee00e168-24c2-481f-8cb8-aa29a8d373fd.png)


![Screenshot 2022-04-14 at 12 17 54 AM](https://user-images.githubusercontent.com/40661295/163249551-6d5d11da-cf6a-4085-bd4e-410e585d2b82.png)


* Average Response time (Latency): Average latency of the overall frontend and backend application 
* Memory usage : Node memory usage
* Failed responses per second:  To capture the failed response of the bothe flask application
* Flask HTTP Request 5XX Code: To capture 5xx reponse code of frontend and backend application
* Flask HTTP Request 5XX Code: To capture 4xx reponse code of frontend and backend application
* Uptime (backend) : backend container uptime
* Uptime (frontend) : frontend container uptime
* CPU Usage : CPU usage over time
* Pods health : Pod restarts by namespace
