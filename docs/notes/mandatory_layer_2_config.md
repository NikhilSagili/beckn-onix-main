## Note on mandatory Layer 2 Config (Important)

This note will eventually be moved to a proper place in the documentation. It has been put here to alert people who run Beckn-ONIX in the meantime.
Beckn-ONIX mandates availability of Layer 2 Config for a particular domain before any transactions can be conducted on it. If the layer 2 config is not present, on either the BAP or the BPP, the following error is returned back to the caller. "Config error : Layer 2 config not found."

Usually the network facilitators will host the Layer 2 config and provide a way to access it. Currently we have a small script (layer2/download_layer_2_config_bap.sh and layer2/download_layer_2_config_bpp.sh) that can download the layer 2 config from a fixed location and insert it into the docker container that runs the Protocol Server Client.

- In case you do not have layer 2 config file with you, some sample files are hosted in this repo in this [folder](../../layer2/samples/)
- In case you do not have layer 2 config file with you, and the samples folder does not have the domain that you need, as developer machine workaround, you can copy the core_version.yaml(e.g. core_1.1.0.yaml) and rename it as the layer 2 config for a domain (e.g. for a domain named retail for core version 1.1.0, retail_1.1.0.yaml). This is strictly not recommended for production networks.
- If you have the Layer 2 config file with you and not hosted, you can use the following procedure to update it manually.

Process to manually update layer 2 config.

```
docker cp "$FILENAME" "$CONTAINER_NAME":"$CONTAINER_PATH/$FILENAME"

# example
docker cp retail_1.1.0.yaml bap-client:/usr/src/app/schemas/retail_1.1.0.yaml
docker cp retail_1.1.0.yaml bap-network:/usr/src/app/schemas/retail_1.1.0.yaml

docker cp retail_1.1.0.yaml bpp-client:/usr/src/app/schemas/retail_1.1.0.yaml
docker cp retail_1.1.0.yaml bpp-netork:/usr/src/app/schemas/retail_1.1.0.yaml

```
