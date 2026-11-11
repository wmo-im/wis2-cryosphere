# wis2-cryosphere

WIS2 cryosphere demo

# Overview

This repository provides examples of how to publish metadata and data to WIS2 for Cryosphere data.

# Tools used

- [pywcmp](https://github.com/World-Meteorological-Organization/pywcmp): pywcmp provides validation and quality assessment capabilities for the WMO WIS Core Metadata Profile (WCMP).  In this demo, pywcmp is used to validate WCMP2 records in the repository
- [pywis-pubsub](https://github.com/World-Meteorological-Organization/pywis-pubsub): pywis-pubsub provides subscription and download capability of data from WIS2.  In this demo, pywis-pubsub is used to publish WIS2 Notifications to the demo WIS2 Node MQTT broker

# WIS2 Node

- MQTT broker: a demo MQTT broker service is provided by [EMQX Cloud](https://www.emqx.com/en/cloud)
- HTTP server: this repository is used as the HTTP server, using a GitHub Pages setup

# Setup

This repository is setup as follows:

- [`config`](https://github.com/wmo-im/wis2-cryosphere/tree/main/config): configurations
- [`metadata`](https://github.com/wmo-im/wis2-cryosphere/tree/main/metadata): sample WCMP2 discovery metadata

The workflows are designed as "no code" approaches to publishing to WIS2.

To setup this repository:

```bash
# setup a Python virtual environment
python3 -m venv env
cd env
. bin/activate
pip3 install pywcmp pywis-pubsub

# clone this repository
git clone https://github.com/wmo-im/wis2-cryosphere.git
cd wis2-cryosphere
```

# Publishing data and metadata

## WGMS example

```bash
# publish sample WGMS metadata
pywis-pubsub wnm publish --metadata-id urn:wmo:md:ch-wgms-test:fog-2026-02-10 --url https://wmo-im.github.io/wis2-cryosphere/metadata/ch-wgms-test/fog-2026-02-10.json --topic origin/a/wis2/ch-wgms-test/metadata -c config/pywis-pubsub-config.yml 

# publish WGMS data
pywis-pubsub wnm publish --metadata-id urn:wmo:ch-wgms-test:fog-2026-02-10 --url https://wgms.ch/downloads/DOI-WGMS-FoG-2026-02-10.zip --topic origin/a/wis2/ch-wgms-test/data/core/cryosphere/experimental/glaciers -c pywis-pubsub-config.yml 
```
