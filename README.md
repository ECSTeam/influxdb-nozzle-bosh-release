# InfluxDB Nozzle Bosh Release

This provides a [BOSH](https://bosh.io) release for the [ECS Team InfluxDB Nozzle](https://github.com/ECSTeam/influxdb-nozzle).

## Jobs

This release provides no jobs, per se. See the [errands](#errands) section for more info.

## Errands

### Deploy Nozzle

This will deploy the nozzle into a Cloud Foundry environment. Configuration Properties:

```yaml
influxdb:
  nozzle:
    admin_client_id: ???            # The ID of a UAA user with uaa.admin scope
    admin_client_secret: ???        # The secret of the above client
    db_name: ???                    # The DB to which metrics will be sent
    db_user: ???                    # The DB user
    db_password: ???                # The DB password
    subscription_id: ???            # The ID that will be registered with the firehose
    client_id: ???                  # A client ID with doppler.firehose and cloud_controller.admin_read_only
                                    # permissions. If it does not exist, it will be created.
    client_secret: ???              # The secret of the above client. If the client already exists, the secret
                                    # must be correct, or the app will fail to start.
    foundation: ""                  # A tag representing this foundation that will be added to outgoing metrics
    batch_size: 250                 # The number of messages to batch before sending to InfluxDB. Must be [1,5000)
    tag_fields: "[]"                # A JSON array in string form with the fields that will be added as tags.
                                    # Currently valid values are 'job', 'index', 'ip', 'unit', 'deployment', 'tags'
buildpack: java_buildpack_offline   # The version of the Java buildpack to deploy the nozzle with
instances: 3                        # The number of instances to deploy
security:
  user: ""                          # (Optional) not currently used
  password: ""                      # (Optional) not currently used
ssl:
  skip_cert_verify: false           # Whether or not SSL should be ignored
cf:
  admin_user: ???                   # ID of a user with cloud_controller.admin permissions
  admin_password: ???               # Password for the above user
domain: ???                         # CF System Domain
app_domains: ???                    # list of app domains   
org: ecsteam-influxdb-org           # The org in which the nozzle should be deployed. Will be created if it doesn't exist
space: ecsteam-influxdb-space       # The org in which the nozzle should be deployed. Will be created if it doesn't exist
```

### Deploy Nozzle

This will delete the nozzle and associated artifacts. Configuration Properties:

```yaml                   
security:
  user: ""                          # (Optional) not currently used
  password: ""                      # (Optional) not currently used
ssl:
  skip_cert_verify: false           # Whether or not SSL should be ignored
cf:
  admin_user: ???                   # ID of a user with cloud_controller.admin permissions
  admin_password: ???               # Password for the above user
domain: ???                         # CF System Domain
app_domains: ???                    # list of app domains   
org: ecsteam-influxdb-org           # The org in which the nozzle is deployed
space: ecsteam-influxdb-space       # The org in which the nozzle is deployed
```
