# Altimetry Extension Specification

- **Title:** Altimetry
- **Identifier:** <https://stac-extensions.github.io/altimetry/v0.1.0/schema.json>
- **Field Name Prefix:** altm
- **Scope:** Item
- **Extension [Maturity Classification](https://github.com/radiantearth/stac-spec/tree/master/extensions/README.md#extension-maturity):** Proposal
- **Owner**: @emmanuelmathot

This document explains the [Altimetry](https://www.aviso.altimetry.fr/en/techniques/altimetry/principle.html) Extension 
to the [SpatioTemporal Asset Catalog](https://github.com/radiantearth/stac-spec) (STAC) specification.

- Examples:
  - [Sentinel-3 example](examples/sentinel3.json): Shows the basic usage of the extension in a STAC Item with Sentinel-3 data.
- [JSON Schema](json-schema/schema.json)
- [Changelog](./CHANGELOG.md)

## Fields

The fields in the table below can be used in these parts of STAC documents:

- [ ] Catalogs
- [ ] Collections
- [x] Item Properties (incl. Summaries in Collections)
- [ ] Assets (for both Collections and Items, incl. Item Asset Definitions in Collections)
- [ ] Links

| Field Name           | Type                                                                                                | Description                                                                                                                                                                                                                                                                                 |
| -------------------- | --------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| altm:instrument_type | string                                                                                              | Primary instrument type. See the list of [primary instrument types](#primary-instrument-types).                                                                                                                                                                                             |
| altm:instrument_mode | string                                                                                              | Instrument mode.                                                                                                                                                                                                                                                                            |
| altm:sampling_rate   | number                                                                                              | Sampling rate of the instrument in Hz.                                                                                                                                                                                                                                                      |
| altm:nominal_track   | [GeoJSON LineString Coordinates Array](https://datatracker.ietf.org/doc/html/rfc7946#section-3.1.4) | An array of coordinates used to define the nominal track on the earths surface. This value is recommended ONLY if the item geometry is not representative of the acquisition track. |

> \[!NOTE]
> Various fields and objects in this extensions replace [deprecated fields](https://github.com/stac-extensions/sentinel-3/blob/main/deprecated.md)
> from the [sentinel-3 extension](https://github.com/stac-extensions/sentinel-3).
> Please see the section [sentinel-3 mapping](#sentinel-3-mapping) for more information.

### Primary Instrument Types

The following values are valid for the `altm:instrument_type` field:

| Value     | Description              |
| --------- | ------------------------ |
| sar       | Synthetic Aperture Radar |
| doppler   | Doppler                  |
| laser     | Laser                    |
| microwave | Microwave Radiometer     |
| other     |                          |

### Sentinel-3 Mapping

The following table shows the mapping between the [deprecated fields](https://github.com/stac-extensions/sentinel-3/blob/main/deprecated.md)
in the [Sentinel-3 extension](https://github.com/stac-extensions/sentinel-3) and the fields in the Altimetry extension.

| Sentinel-3 Field Name | Altimetry Field Name   | Altimetry Field Value |
| --------------------- | ---------------------- | --------------------- |
| `s3:lrm_mode`         | `altm:instrument_mode` | `lrm`                 |
| `s3:sar_mode`         | `altm:instrument_mode` | `sar`                 |

## Contributing

All contributions are subject to the
[STAC Specification Code of Conduct](https://github.com/radiantearth/stac-spec/blob/master/CODE_OF_CONDUCT.md).
For contributions, please follow the
[STAC specification contributing guide](https://github.com/radiantearth/stac-spec/blob/master/CONTRIBUTING.md) Instructions
for running tests are copied here for convenience.

### Running tests

The same checks that run as checks on PR's are part of the repository and can be run locally to verify that changes are valid. 
To run tests locally, you'll need `npm`, which is a standard part of any [node.js installation](https://nodejs.org/en/download/).

First you'll need to install everything with npm once. Just navigate to the root of this repository and on 
your command line run:
```bash
npm install
```

Then to check markdown formatting and test the examples against the JSON schema, you can run:
```bash
npm test
```

This will spit out the same texts that you see online, and you can then go and fix your markdown or examples.

If the tests reveal formatting problems with the examples, you can fix them with:
```bash
npm run format-examples
```
