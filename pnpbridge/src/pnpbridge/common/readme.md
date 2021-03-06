# Common helper utilities for PnP Sample

This directory contains helper routines used by the bridge to implement PnP functionality when using the Azure IoT Hub SDK.

For reference the files are:

* `pnp_device_client` header and .c file implement a function to help create a `IOTHUB_DEVICE_CLIENT_HANDLE`.  The `IOTHUB_DEVICE_CLIENT_HANDLE` is an existing IoTHub Device SDK that can be used for device <=> IoTHub communication.

    Creating a `IOTHUB_DEVICE_CLIENT_HANDLE` that works with PnP requires a few additional steps, most importantly defining the device's PnP ModelId, which is
    defined by the PnP Bridge's Root Interface Model Id and retrieved from the configuration file.

* `pnp_dps` header and .c file implement functions to help provision a device handle through the device provisioning service.

* `pnp_protocol` header and .c file implement functions to help with serializing and de-serializing the PnP convention. As an example of their usefulness, PnP properties are sent between the device and IoTHub using a specific JSON convention over the device twin. Functions in this header perform some of the tedious parsing and JSON string generation that is offloaded from the PnP Bridge.

    The functions are agnostic to the underlying transport handle used.  If you use `IOTHUB_DEVICE_CLIENT_LL_HANDLE`, `IOTHUB_MODULE_CLIENT_HANDLE` or `IOTHUB_MODULE_CLIENT_LL_HANDLE` instead of the sample's `IOTHUB_DEVICE_CLIENT_HANDLE`, the `pnp_protocol` logic does not need to change.
