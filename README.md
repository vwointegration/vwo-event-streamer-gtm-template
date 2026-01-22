# VWO Event Streamer (GTM Template)

The **VWO Event Streamer** is a custom Google Tag Manager template designed to capture events from your website and stream them directly to VWO. It can stream events added to DataLayer to VWO.

## Features

* **Dual Modes:**
    1.  **SmartCode Mode:** Uses the existing VWO SmartCode on your website.
    2.  **Direct/Offline Mode:** Uses a helper script to send events for Feature Experiments or offline conversions (requires Account ID).
* **Advanced Data Control:** Includes options for nested JSON mapping and strict event/property exclusions.

---

## Configuration Guide

### 1. Connection Settings

* **Send Events for Feature Experiments or Offline Conversions:**
    * **Unchecked (Default):** The tag will assume VWO SmartCode is running on the page and push events locally (`window.VWO.push`).
    * **Checked:** The tag will load a lightweight helper script to send events directly to VWO servers. This is useful for Feature Experiments or when SmartCode might not be available.
* **Account ID:** (Required if the above box is checked) Your VWO Account ID.
* **Region:** Select your data region (EU, India, or US/Default).
* **VWO Visitor ID:** (Optional) If you are tracking offline conversions or specific users, map a variable here to identify the visitor.

### 2. Custom Properties & Mapping

* **Additional Custom Properties:** Manually add key-value pairs to every event sent by this tag.
* **Nested JSON Field Mapping:** If your DataLayer event has nested structures (e.g., `ecommerce.value`), use this to flatten them.
    * *Property Name:* The name you want in VWO (e.g., `revenue`).
    * *JSON Key Path:* The path in the DataLayer object (e.g., `ecommerce.value` or `items.0.item_name`).

### 3. Exclusions

You can prevent specific events or properties from being sent to VWO.



## Technical Details

### Event Detection Logic
The tag prioritizes detection in this order:
1.  **GA4 Model:** Checks for `eventModel` in the DataLayer.
2.  **Standard DataLayer:** Checks for `gtm.uniqueEventId` and scans the `dataLayer` array.

### Permissions
This template requires the following sandboxed permissions to function:
* `read_data_layer`: To scan for events.
* `access_globals`: To read/write `window.VWO` and `window.dataLayer`.
* `inject_script`: To load the VWO Helper script (only used in Feature Experiment mode).
* `logging`: For debug messages.

