---

title: 'Telemetry'
weight: 45

menu:
  main:
    identifier: "user-guide-introduction-telemetry"
    parent: "user-guide-introduction"

---


At Camunda, we strive to offer an excellent user experience at a high and stable level. On a strict opt-in basis, we are looking to collect environment and usage data to further improve the user experience for you. These insights help us to understand typical environment setups and product usage patterns and will be used to make informed product improvement decisions to your benefit.

## Design

The process engine has a dedicated thread called the **Telemetry Reporter** to periodically report telemetry data to Camunda. By default, this thread is always running, but only reports data if telemetry is explicitly enabled. See the [how to enable telemetry]({{< ref "#how-to-enable-telemetry" >}}) section for how to do this. The collected data is available through multiple APIs, even if sending the data to Camunda is not enabled. See [how to access the data]({{< ref "#how-to-access-the-data" >}}) for more information on how to do this.

When enabled, the collected data is sent once every 24 hours via HTTPS. The telemetry reporter is designed so that your implemented processes are not negatively affected in case the reporter suddenly faces an unexpected error. The telemetry reporter stops in any case when the process engine is stopped.

## Collected data

Below you find the full list of data the reporter collects, followed by a real-world example. On a conceptual level, they can be categorized into general data, meta/environment data, and usage data.

### General data

The "General Data" category contains information about the process engine:

* Hashed IP address - the telemetry service that receives the data stores a hash of the IP address from which the data is sent to filter duplicate data and detect malicious access
* Installation - an id that is stored as process engine configuration property
* Product name - the name of the product (i.e., `Camunda BPM Runtime`)
* Product version - the version of the process engine (i.e., `7.X.Y`)
* Product edition - the edition of the product (i.e., either `community` or `enterprise`)
* License key - the customer name, expiry date and enabled features as well as the raw license info

License key data does not contain any protected data like the signature. License data is only transmitted if any of the following holds true

* it is present in the database on engine startup
* it is set to the engine via  [ManagementService#setLicenseKey ](https://docs.camunda.org/javadoc/camunda-bpm-platform/7.14/org/camunda/bpm/engine/ManagementService.html#setLicenseKey-java.lang.String-)
* it is set to the engine via [Admin Webapp](https://docs.camunda.org/manual/latest/webapps/admin/system-management/#camunda-license-key)

Please note that only in case of setting the license key through the Admin Webapp the telemetry data will contain structured metadata from the license key. In all other cases, unstructed raw data will be sent. If the license key is removed from the engine, it is removed from telemetry data as well.

### Meta and environment data
The "Meta/Environment Data" category contains information about the environmental setup:

* Database vendor and version
* Application server vendor and version
* JDK vendor and version
* Used Camunda Web Applications

The application server information cannot be obtained in an embedded process engine setup where no web application (e.g. Tasklist, Cockpit, REST application) is deployed and used.

In case of Azul Zulu JDK, the vendor will be send as "Oracle Corporation" as it cannot be distinguished programmatically from an Oracle JDK.


### Usage data
The "Usage Data" category contains information about the used features and components of the process engine:

* Commands count - the count of executed commands after the last retrieved data. It could be from the previous 24 hours if the data have been reported then, and the process engine has not been closed during that time. Whenever the process engine is shutdown, the currently collected data is reported immediately.
* Metrics count - the collected metrics are number of root process instance executions started, number of activity instances started or also known as flow node instances, and number of executed decision instances and elements.
The counts are collected from the start of the engine or the last reported time if the engine is already running for more than 24 hours.
* Camunda integration - a flag that shows if any of the Camunda integrations are used: Spring boot starter, Camunda Platform Run, WildFly subsystem or Camunda ejb service (e.g. WebSphere/WebLogic Application servers).

### Example

```
{
    "installation": "8343cc7a-8ad1-42d4-97d2-43452c0bdfa3",
    "product": {
      "name": "Camunda BPM Runtime",
      "version": "7.14.0",
      "edition": "enterprise",
      "internals": {
        "database": {  
          "vendor": "h2",
          "version": "1.4.190 (2015-10-11)"
        },
        "application-server": {
          "vendor": "Wildfly",
          "version": "WildFly Full 19.0.0.Final (WildFly Core 11.0.0.Final) - 2.0.30.Final"
        },
        "jdk": {
          "version": "14.0.2",
          "vendor": "Oracle Corporation"
        },
        "commands": {
          "StartProcessInstanceCmd": {"count": 40},
          "FetchExternalTasksCmd":  {"count": 100}
        },
        "metrics": {
          "process-instances": { "count": 936 },
          "flow-node-instances-start": { "count": 6125 },
          "decision-instances": { "count": 140 },
          "executed-decision-elements": { "count": 732 }
        },
        "camunda-integration": [
          "spring-boot-starter",
          "camunda-bpm-run"
        ],
        "license-key": {
          "customer": "customer name",
          "type": "UNIFIED",
          "valid-until": "2022-09-30",
          "unlimited": false,
          "features": {
            "camundaBPM": "true"
          },
          "raw": "customer=customer name;expiryDate=2022-09-30;camundaBPM=true;optimize=false;cawemo=false"
        },
        "webapps": [
          "cockpit",
          "admin"
        ]
      }
    }
}
```

### Logger

The logger with name `org.camunda.bpm.engine.telemetry` logs details about the sent information and errors in case the data couldn't be collected or sent. For further information check the [Logging]({{< ref "/user-guide/logging.md#telemetry-data" >}}) page in the User Guide.



## How to enable telemetry

### Process engine configuration

Use the `initializeTelemetry` configuration [flag][engine-config-initializeTelemetry] to enable the telemetry before starting the process engine. You can simply add it to your process engine configuration:

```
  <property name="initializeTelemetry">true</property>
```

Note that this property only has an effect when telemetry is initialized on the first engine startup. After that, it can be enabled/disabled via the engine API.

In case telemetry is not used, the `telemetryReporterActivate` configuration [flag][engine-config-telemetryReporterActivate] can be set to `false` to prevent the process engine from starting the telemetry reporter thread at all. This configuration is also useful for unit testing scenarios.

### Java/REST API

You can change the telemetry configuration via our API.

To enable/disable telemetry via Java API:

```java
  managementService.toggleTelemetry(true);
```

To achieve the same, you can also use the respective REST API request. For more information, have a look at the [telemetry][telemetry-config-rest] page in the REST API documentation.

### Admin webapp

Configuration adjustment can be performed in the [Admin][system-management] web application. There, a user member of camunda-admin group can enable/disable the telemetry.

## How to access the data

Telemetry data is constantly collected even if sending the data to Camunda is not enabled. This allows you to access the collected data through the Java and REST APIs of Camunda.
Being able to easily access the collected data is helpful when asking for help in our [forum](https://forum.camunda.org/) or when opening issues in our [issue tracker](https://app.camunda.com/jira) as it contains many of the information that are usually necessary to understand your Camunda setup.

Note that some of the dynamic data, like executed engine commands or reported metrics reset on sending the telemetry data to Camunda. Accessing them through one of the Camunda APIs, however, does not.

### Java API

To fetch the collected data via the Java API, you can use the `ManagementService` class. For example, the following code retrieves the detected JDK vendor and version:

```java
ProcessEngine processEngine = ...;
ManagementService managementService = processEngine.getManagementService();

TelemetryData telemetryData = managementService.getTelemetryData();
Internals productInternals = telemetryData.getProduct().getInternals();

String jdkVendor = productInternals.getJdk().getVendor();
String jdkVersion = productInternals.getJdk().getVersion();
```

### REST API

You can fetch the collected data via the REST API by calling the [Get Telemetry Data][telemetry-data-rest] endpoint.

## Legal note

Before you install a Camunda Platform Runtime version >= 7.14.0-alpha1 (and 7.13.7+, 7.12.12+, 7.11.19+) or activate the telemetry functionality, please make sure that you are authorized to take this step, and that the installation or activation of the [telemetry functionality][engine-config-initializeTelemetry] is not in conflict with any company-internal policies, compliance guidelines, any contractual or other provisions or obligations of your company.

Camunda cannot be held responsible in the event of unauthorized installation or activation of this function.

## Source code 

In case you want further details, you can have a look at the implementation of the telemetry topic in [our codebase](https://github.com/camunda/camunda-bpm-platform/blob/master/engine/src/main/java/org/camunda/bpm/engine/impl/telemetry/reporter/TelemetrySendingTask.java). The link leads you to the current `master` version of the feature. In case you would like to check the implementation of an old version, adjust the `master` branch to a released tag version, e.g. `7.14.0`.

## Initial data report

{{< note title="Previous Camunda versions only" class="info" >}}
In previous Camunda versions, the installation sends an anonymized one-time initial report to Camunda. This applies to the following versions:

* 7.17: All versions before 7.17.0
* 7.16: 7.16.6 and lower
* 7.15: 7.15.12 and lower
* 7.14: 7.14.18 and lower
* 7.13 / 7.12 / 7.11: all versions

In higher versions, the installation no longer sends this initial message.
{{< /note >}}

To support the understanding of typical use cases and the overall distribution of our products, the installation sends an anonymized one-time initial report to Camunda via HTTPS. This report contains no specifics that would allow any direct link to an outside entity and is limited to the following data:

```
{
  "installation": "b647de4d-e557-455a-a64f-feaecd55f53c",
  "product": {
    "name": "Camunda BPM Runtime",
    "version": "7.14.0",
    "edition": "community".
    "internals": { "telemetry-enabled": false}
  }
}
```
The telemetry service that receives this report also stores a hash of the IP address from which the report is sent. That hash of the IP address is stored to filter duplicate data and detect malicious access.
No other information will be included in that report. Furthermore, this report will be sent exactly once on the first run of your installation.
In case you disabled telemetry explicitly or did not configure it at all, this is the only report that will ever be sent to Camunda.

If there is the necessity to also prevent this anonymized report from being sent to us, you can set the `telemetryReporterActivate` configuration [flag][engine-config-telemetryReporterActivate] to `false`.
With this, the reporter thread will not be started and no request will ever be sent to Camunda. See the [how to enable telemetry]({{< ref "#how-to-enable-telemetry" >}}) section on how to do this.


[engine-config-initializeTelemetry]: {{< ref "/reference/deployment-descriptors/tags/process-engine.md#initializeTelemetry" >}}
[engine-config-telemetryReporterActivate]: {{< ref "/reference/deployment-descriptors/tags/process-engine.md#telemetryReporterActivate" >}}
[telemetry-config-rest]: {{< ref "/reference/rest/telemetry/post-telemetry-config.md" >}}
[telemetry-data-rest]: {{< ref "/reference/rest/telemetry/get-telemetry-data.md" >}}
[system-management]: {{< ref "/webapps/admin/system-management.md" >}}
