# iRPC
iRPC is a macOS App designed to help with gRPC development. By using server reflection, it offers an intuitive UI-based experience for connecting to and exploring the capabilities of any gRPC server that has reflection enabled.

### To Use
Currently, iRPC is only offered as a direct binary download. To run, clone this repo and launch the app by double-clicking the iRPC.app in the root folder. **NOTE: This has only been tested on macOS Big Sur 11.0.1, however it has been compiled for 11.0 and above.**

### Getting Started
Upon launching iRPC, you will want to start by adding your first service using the **Add New Service** button in the upper-left corner. After successfuly connecting to a reachable gRPC server with reflection enabled, you will be presented with a dropdown list containing all the available services. Select one of the available services and provide a descriptive name, then click **Add**.

![iRPC](/assets/screenshots/iRPC.png)

### Exploring New Service
The new service will be added to the list on the left, and can be expanded to display all of the available methods. The **plus** icon next to the method name will add a new tab, which is where you can prepare and send your requests. Each method can have multiple tabs, allowing for different request payloads.

### Invoking Methods
iRPC allows you to build the request using a form-based approach, or by editing the JSON directly. It also provides the response in an easy-to-view fashion.
#### Request
##### Metadata
Here, you can add headers to your request using standard key/value pairs. Header values can utilize macros (covered below).
##### Data
This displays a form representation of the method's input message. Using the type descriptors, it provides relevant input fields and allows you to quickly build out the request payload. Macros can also be used here where applicable.
##### JSON
This displays a raw JSON output of the payload, and can also be used for directly editing as needed (including pasting an entire payload from an external source). **NOTE: Due to limitations of the JSON library, this experience has a known issue where the text may jump around while editing. As such, it is not recommended for normal use.**
#### Response
##### Headers
This will display any of the response headers after a successful call.
##### Data
This will display the raw JSON response body after a successful call. You can copy the response text by using the **COPY** button above.
##### Trailers
This will display any response trailers provided by the server.

### Macros
In order to make testing easier with reusable calls, iRPC offers both default and custom global macros as a way to populate values when invoking a method. Review the available macros by clicking the **gear** icon near the upper-left of the screen.
#### Default
* {{$uuid}} - A standard UUID string
* {{$timestamp}} - An epoch timestamp to second precision
* {{$timestampMS}} - An epoch timestamp to millisecond precision
* {{$randomString}} - A random string of alpha characters (a-zA-Z)
* {{$randomInt}} - A random integer between 0-1000
#### Global
Custom macros can be added by providing a key/label and the value to inject. Currently, iRPC only allows static values. Similar to default macros, custom macros are referenced by surrounding the label with {{ }}. For example, to use a custom macro named "MY_MACRO", simply use {{MY_MACRO}} in the field value.

### Advanced Settings
#### Timeout
The timeout field next to the **SEND** button in the request view can be used to control the timeout of gRPC requests. This defaults to 5 seconds.
#### Rescan
Access the service settings view by hovering over a service in the list view on the left and clicking the icon that appears. Clicking the **RESCAN** tab will present an option to connect to the gRPC server using the original host, or a new one if it has changed. A successful connection will result in one of the following:
* No Changes: There were no changes detected for the gRPC service from what was previously stored
* Compatible Changes: New methods or fields were added which will be appended upon clicking **SAVE**
* Incompatible Changes: One or more methods or fields were removed, and clicking **SAVE** will wipe all existing data

**NOTE: The service name itself must remain the same - iRPC currently does not allow changing the service after adding**
