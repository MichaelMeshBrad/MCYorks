# Suggested MeshCore repeater commands

These suggested settings have been deployed successfully across Yorkshire. Individual repeaters may need different settings based on their location, coverage and surrounding mesh traffic.

## Access the CLI

1. Log in to the repeater.
2. Navigate to the **CLI** section.
3. Enter each command on a separate line.
4. Wait for an `OK` response before entering the next command.
5. Save the configuration when complete.

## Suggested commands

| Command | Description |
| --- | --- |
| `set flood.max 20` | Sets the maximum flood distance for messages and advertisements to 20 hops. |
| `set flood.max.advert 0` | Sets advertisement flood messages to a maximum of 0 hops to help mesh congestion (firmware v1.16+). |
| `set flood.max.unscoped 32` | Sets un-scoped flood messages to a maximum of 32 hops (firmware v1.16+). |
| `set path.hash.mode 2` | Uses a 3-byte hash for repeater advertisement paths. This does not change the size of forwarded messages. |
| `set loop.detect minimal` | Enables minimal loop detection to drop packets when the repeater's ID or hash occurs too many times. |
| `set flood.advert.interval 0` | Sends a flood advertisement every 0 hours to reduce mesh congestion. manual Advert will still be available |
| `set advert.interval 237` | Sets the zero-hop advertisement interval to 237 minutes (approx. 4 hours). |
| `set dutycycle 10` | Sets the radio duty cycle to 10% (firmware v1.15+). |

Flood.Max - Controls Flood messages which ARE scoped with a region tag
Flood.Max.UnScoped - Controls Flood messages are NOT scoped with a region tag

!!! warning "Enter commands individually"
    Wait for an `OK` response after each command so you know it has been accepted.

## Expected result

With these settings, the repeater will:

- Forward flood messages up to 20 hops.
- Forward advertisement floods up to 0 hops.
- Forward un-scoped messages and floods up to 32 hops, (most of the UK is under this.)
- Use a 3-byte path hash for repeater advertisements.
- Apply minimal loop detection.
- Reduce unnecessary advertisement traffic.

## Radio Transmit Delay

The following commands may help messages get out based on the number of neighbours your repeater has.

## Suggested commands

| Command | Description |
| --- | --- |
| `set tx delay 0.5` | Sets a 0.5 second delay, best for 1-10 neighbours |
| `set tx delay 1.0` | Sets a 1.0 second delay, best for 11-20 neighbours |
| `set tx delay 1.8` | Sets a 1.8 second delay, best for 20+ neighbours |

If your repeater has 20+ neighbours, the TX Delay COULD be increased up to a max of 2.0

## Yorkshire Region Configuration

The following configuration is actively used on the Yorkshire region and the `#yorkshire` channel.

Enter these commands in order:

```text
region put yorkshire
region put eng-yh
region default yorkshire
region save
```

### Optional neighbouring regions

Add these only when the repeater needs useful North East or North West inter-region coverage:

```text
region put eng-ne
region put northwest
region save
```

| Command | Description |
| --- | --- |
| `region put yorkshire` | Adds and allows forwarding for the Yorkshire region identifier. |
| `region put eng-yh` | Adds the Yorkshire and Humber region code. |
| `region put eng-ne` | Adds the North East England region code. |
| `region put northwest` | Adds the North West England region code. |
| `region default yorkshire` | Makes Yorkshire the default region for repeater access and flood messages. |
| `region save` | Saves the region configuration permanently. |

## Client configuration

Once the regional settings are deployed, add the `yorkshire` region scope to the `#yorkshire` channel in the MeshCore client. This helps reduce unnecessary mesh traffic.

1. Open the `#yorkshire` channel.
2. Select the three-dot menu in the top-right corner.
3. Choose **Set Region Scope**.
4. Select **+** and add `yorkshire`.
5. Select the tick to save it and make sure the scope is selected.

!!! important
    These are suggested commands, not universal settings. Review the results and adapt them to the needs of each repeater.
