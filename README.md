# edge-docker

A quick self-contained example deploying Mezmo Edge using Docker Compose.

Quickstart:
-----------

Provision a token in your Mezmo account (Settings -> Organization -> API Keys -> Pipeline Service Keys)

Export your key or set in the environment:

> export MEZMO_PIPELINE_SERVICE_TOKEN=\<YOUR TOKEN HERE>

Run compose to start the service:

> docker compose up -d

Pipelines configured as type 'Edge' in this account will be automatically configured in the edge instance.

Contents:
---------

`.env`: contains base environment. Can be used to configure a different EDGE_ID for different instances of the service (this is used as an identifier for heartbeats, metrics, and tapping data).

`processor.yaml`: contains the heartbeat payload for the service. May be customized with different attributes depending on the deployment model. Values can interpolate variables from the container environment.

`compose.yaml`: defines the singular edge service. Modify this to inject additional variables and export additional ports.

Using disk buffers:
------------------
Edge pipelines have the option to condfigure disk-based buffers for
destinations. Presently this is feature-flagged in the application
(`pipeline-edge-disk-buffer`) and must be enabled for your account.

Disk buffers are disabled by default, but can be enabled per destination
by setting the toggle in the destination configuration drawer. Typically
if the goal is to decouple the source from the destination, one should
also disable "End-to-end Acknowledgement" at the same time.

By default this compose file will simply mount a local directory
`tmp-data` into the container under the default data directory. To test
with dedicated storage volumes, change the mount going into
`/data/vector`.

By default the node will limit disk buffers for all destinations to
256MiB. This is a minimum and can be increased by setting a higer value
into the container environment with `MEZMO_DISK_BUFFER_MAX_BYTES`.