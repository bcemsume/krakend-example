
KrakenD Example
====
Wellcome, workshop is a demonstration environment that puts together the necessary pieces to get you started with our API Gateway, using an example web application.

API gateway, we have added to the environment both the API (backend) that feeds the gateway and a website consuming the api gateway. 
Additionally, a dashboard with the metrics is also available so you can see your activity.


## Services
The docker-compose starts the following services:


### Backend
A simple API that provides raw data to the gateway.

You can add or remove data any time by adding XML, JSON or RSS files in the `data` folder.

Runs on [http://localhost:8000](http://localhost:8000)

### The designer
An instance of Krakendesigner (the GUI for manipulating the `api-gw/krakend.json` file.

You can drag the file `api-gw/krakend.json` anytime in the dashboard and resume the edition from there.

Runs on [http://localhost:8787](http://localhost:8787)

### The gateway!
An instance of KrakenD with several endpoints. Its configuration is in the folder `api-gw/`.


Runs on [http://localhost:5001](http://localhost:5001)

### Metrics
A Jaeger dashboard shows the traces of the activity you generate. Runs on [http://localhost:16686](http://localhost:16686)

### Prometheus
A Prometheus gathers the metrics from api gateway and stores them. Runs on [http://localhost:9090](http://localhost:9090)

### Grafana
Grafana is dashboarding UI, shows the metrics Runs on [http://localhost:3333](http://localhost:3333)



### Start the service
Just:

    docker-compose up -d

## Development stuff

### krakend-config2dot
Transalte your KrakenD config file into a dot graph
```go get github.com/devopsfaith/krakend-config2dot/cmd/krakend-config2dot```

```
krakend-config2dot -c api-gw/krakend.json |dot -Tpng -o config.png
```

### krakend-postman
```
go get -u github.com/devopsfaith/krakend-postman
```


## Play!
Fire up your browser, curl, postman, httpie or anything else you like to interact with any of the published services.

## Editing the API Gateway endpoints
To add or remove endpoints, edit the file `api-gw/krakend.json`. The easiest way to do it is by **dragging this file to the [KrakenD designer](http://localhost:8787)** and download the edited file. 
To reflect the changes restart docker-compose.


The following endpoints are worth noticing:


- `/public`: Simple aggregation of two public API calls from Bitbucket and Github with some field selection.
- `/splash`: Public endpoint aggregating data from the internal backend

## lets generate some load!

```
k6 run loadtest/test.js
```