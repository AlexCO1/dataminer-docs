---
uid: 10_2_9_General_RNs
---

# DataMiner 10.2.9 release notes

> [!IMPORTANT]
> We are still working on this release. Some release notes may still be modified or moved to a later release. Check back soon for updates!

> [!NOTE]
> For release notes related to DataMiner Cube, see [DataMiner Cube 10.2.9 release notes](xref:10_2_9_Cube_RNs).

## Highlights

## Other new features

### Core functionality

#### SLPort: Order of parameters in an HTTP session request will be identical to that in the protocol [ID_33796]

<!-- Main Release Version 10.1.0 [CU18]/10.2.0 [CU6] - Feature Release Version 10.2.9 -->

In an HTTP session request, the order of the parameters will now always be identical to that in the protocol.

#### DVE function protocol version of active functions will now be deleted when the main DVE protocol version is deleted [ID_33834]

<!-- Main Release Version 10.1.0 [CU18]/10.2.0 [CU6] - Feature Release Version 10.2.9 -->

When a version of a DVE protocol with function DVE protocols is deleted from the system while functions are active, from now on, the function DVE protocol versions associated with those active functions will also be removed from the system.

### DMS web apps

#### Web apps now also support parameter comments configured in Param.Message elements [ID_33784]

<!-- Main Release Version 10.2.0 [CU6] - Feature Release Version 10.2.9 -->

When configuring a parameter in a protocol, you can add a `<Message>` element containing a comment to be displayed in a confirmation box when users change that parameter on the user interface. Up to now, this `<Message>` element was only supported by DataMiner Cube. It is now also supported by web applications like Monitoring and Dashboards.

#### GQI: Table columns of type 'decimal' can now also be used when filtering or aggregating data [ID_33927]

<!-- Main Release Version 10.2.0 [CU6] - Feature Release Version 10.2.9 -->

Table columns of type "decimal" can now also be used when filtering or aggregating data.

### DMS tools

## Changes

### Enhancements

#### Cassandra Cluster Migrator: Enhanced resilience of the migration process [ID_33467] [ID_33621] [ID_33727]

<!-- Main Release Version 10.2.0 [CU6] - Feature Release Version 10.2.9 -->

The migration process will now be executed partition by partition. This greatly enhances the overall resilience of that process.

When the source database is a Cassandra database, at the end of a migration process, the Migrator tool will now automatically retry to migrate the partitions that could not be migrated the first time. Moreover, when you manually restart a migration with failed partitions, only those failed partitions will be included in the new migration attempt. The migration will no longer have to be redone from scratch.

Also, additional fail-safes have been built in to cope with situations where the target Cassandra database cannot be reached.

### Fixes

#### SLLogCollector would become unresponsive when the name of the process or the path where the files had to be stored contained spaces [ID_33493]

<!-- Main Release Version 10.1.0 [CU18]/10.2.0 [CU6] - Feature Release Version 10.2.9 -->

While collecting log information, SLLogCollector would become unresponsive when the name of the process or the path where the collected files had to be stored contained spaces.

#### Failover: SLNet would return old configuration when that configuration was being updated [ID_33619]

<!-- Main Release Version 10.3.0 - Feature Release Version 10.2.9 -->

When SLDataMiner or SLDMS requested the Failover configuration from SLNet while that configuration was being updated, in some rare cases, SLNet would incorrectly return the old configuration.

#### SLProtocol would leak memory leak each time a parameter of a replicated element was updated [ID_33745]

<!-- Main Release Version 10.1.0 [CU18]/10.2.0 [CU6] - Feature Release Version 10.2.9 -->

SLProtocol would leak memory each time a parameter of a replicated element was updated.

#### Web services API would incorrectly no longer clear a number of its caches when the connection was lost [ID_33764]

<!-- Main Release Version 10.3.0 - Feature Release Version 10.2.9 -->

When the connection was lost, the web services API would incorrectly no longer clear a number of its caches.

#### Service & Resource Management: Child DVE element would not get activated when the main DVE element was in an error state [ID_33787]

<!-- Main Release Version 10.3.0 - Feature Release Version 10.2.9 -->

When you tried to create a booking with a child DVE element linked to a main DVE element in an error state, the child DVE element would not automatically be activated, causing the booking to fail. Moreover, SLNet would not try to activate this child DVE element, causing subsequent bookings needing that same child DVE element to also fail, even if the main element had already recovered from the error state in the meantime.

#### GQI: Columns of type 'decimal' would incorrectly not be treated as columns of type 'numeric' [ID_33792]

<!-- Main Release Version 10.2.0 [CU6] - Feature Release Version 10.2.9 -->

Columns of type "decimal" would incorrectly be treated as columns of type "string" instead of columns of type "numeric".

### Dynamic virtual elements: Problem when processing table columns containing foreign keys [ID_33810]

<!-- Main Release Version 10.2.0 [CU6] - Feature Release Version 10.2.9 -->

When a table contained multiple foreign keys, invalid foreign key values referring to non-existing rows could prevent those rows from being exported to DVE child elements. This would cause alarms, trend information, subscriptions, etc. to not get updated for specific DVE elements and/or virtual functions.

#### Problem with SLElement when resolving foreign keys took a long time and the the element debug log level was equal to or higher than 1 [ID_33826]

<!-- Main Release Version 10.1.0 [CU18]/10.2.0 [CU6] - Feature Release Version 10.2.9 -->

When the element debug log level was equal to or higher than 1, an error could occur in SLElement when resolving foreign keys took a long time. 

#### Dashboards app - Service definition component: Function nodes would incorrectly not display the number of Process Automation tokens in queue or in progress [ID_33848]

<!-- Main Release Version 10.3.0 - Feature Release Version 10.2.9 -->
<!-- Not added to 10.3.0 -->

When a Process Automation definition was added to a Service definition component, the function nodes would incorrectly not display the number of tokens currently in queue or in progress.

#### Web apps: No group row would appear when you selected a single item in a list view [ID_33858]

<!-- Main Release Version 10.3.0 - Feature Release Version 10.2.9 -->
<!-- Not added to 10.3.0 -->

When you selected a single item in a list view, in some cases, no group row would appear.

#### SNMPv3 credentials would incorrectly be checked when replicating an element with SNMPv3 connections [ID_33859]

<!-- Main Release Version 10.1.0 [CU18]/10.2.0 [CU6] - Feature Release Version 10.2.9 -->

When you replicated an element with SNMPv3 connections, the SNMPv3 credentials of that element would incorrectly be checked. As a result, alarms like the following one would appear in the Alarm Console:

```txt
Load Element Failed: Error parsing SNMPv3 password for element: <element name>
```

#### Protocols: Additional connections with a 'Type' defined would incorrectly be ignored [ID_33941]

<!-- Main Release Version 10.0.0 [CU22]/10.1.0 [CU18]/10.2.0 [CU6] - Feature Release Version 10.2.9 -->

Additional connections that had a `<Type>` defined would incorrectly no longer be taken into account.

In the following example, the second connection would incorrectly be ignored.

```xml
<Connections>
    <Connection id="0" name="HTTP Connection">
        <Type>http</Type>
        ...
    </Connection>
    <Connection id="1" name="WebSocket Interface">
        <Type>http</Type>
        ...
```

> [!NOTE]
> Specifying a type with `<Type>` for one connection and specifying a type with e.g. `<Http>` for another connection is not supported.
