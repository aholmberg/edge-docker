# edge-docker

A quick self-contained example deploying Mezmo Edge using Docker Compose.

Quickstart:
-----------

Provision a token in your Mezmo account (Settings -> Organization -> API Keys -> Pipeline Service Keys)

Export your key or set in the environment:

> export MEZMO_PIPELINE_SERVICE_TOKEN=\<YOUR TOKEN HERE>

Run compose to start the service:

> docker compose up -d

Contents:
---------

`.env`: contains base environment. Can be used to configure a different EDGE_ID for different instances of the service (this is used as an identifier for heartbeats, metrics, and tapping data).

`processor.yaml`: contains the heartbeat payload for the service. May be customized with different attributes depending on the deployment model. Values can interpolate variables from the container environment.

`compose.yaml`: defines the singular edge service. Modify this to inject additional variables and export additional ports.