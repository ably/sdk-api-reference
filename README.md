# Ably's Canonical SDK API Reference Commentaries

_[Ably](https://ably.com) is the platform that powers synchronized digital experiences in realtime. Whether attending an event in a virtual venue, receiving realtime financial information, or monitoring live car performance data – consumers simply expect realtime digital experiences as standard. Ably provides a suite of APIs to build, extend, and deliver powerful digital experiences in realtime for more than 250 million devices across 80 countries each month. Organizations like Bloomberg, HubSpot, Verizon, and Hopin depend on Ably’s platform to offload the growing complexity of business-critical realtime data synchronization at global scale. For more information, see the [Ably documentation](https://ably.com/docs)._

## Overview

Language-agnostic reference API (Application Programming Interface) commentaries for SDK (Software Developent Kit) developers to use when adding docstring comments to Ably SDKs.

The repository contains a set of tables in [descriptions.md](/descriptions.md) that complements our [features spec](https://sdk.ably.com/builds/ably/specification/main/features/). Each class and enum has its own table with an associated description for the class or enum. Every method and property is documented within the appropriate table.

This repository is owned by our DevEd (Developer Education) Team, with contrbutions and review input from our SDK Team.

## Table format

### Classes

The table for each class contains the following columns:

```
| Method / Property | Parameter | Returns | Spec | Description |
```

* **Method/Property**: The full method signature (code formatted only where necessary, e.g. where it includes `<`, or property name.
* **Parameter**: Each parameter should have its own row and be code formatted.
* **Returns**: The return value should be code formatted and has its own row, after the parameters have been listed.
* **Spec**: The spec point related to the method or property.
* **Description**: The language-agnostic description that will form the docstrings.

### Enums

The table for each enum contains the following columns:

```markdown
| Enum | Spec | Description |
```

* **Enum**: The name of each value for the enum.
* **Spec**: The spec point related to the enum.
* **Description**: The language-agnostic description that will form the docstrings.

## Conventions

The following conventions should be followed when adding a new method or property to the table:

* Use a verb with an `s` for method descriptions. Common uses are:
    * `get` --> `retrieves`
    * `subscribe` --> `registers (a listener)`
    * `publish` --> `Publishes`
* The expression key-value pairs should be hyphenated.
* Parameters or returns that refer to another class are referred to in terms of objects, for example:
    ```
    A [`Channels`]{@link Channels} object.
    ```

* Links to other classes/enums are written in the format:
    ```
    [`<text>`]{@link <class>#<property>}
    ```

    For example:
    ```
    [`ClientOptions.logLevel`]{@link ClientOptions#logLevel}`
    ```
* If a method references its own class, it should just be code formatted, and not link to itself.
* Descriptions can link out to conceptual docs hosted on `ably.com/docs`, but should never link to the API references hosted there.
* A class or object should always be capitalized.
* Methods and parameters should always be lower-case.
* If adding a method/property to separate REST and realtime classes, ensure the descriptions are consistent (where possible).
* When a return value is returned in a paginated list, the description should link to the PaginatedResult class, as well as the class of whatever is returned.
* Items deprecated in the features spec should include the following text at the beginning of the description: `DEPRECATED: this <property/method> is deprecated and will be removed in a future version.`
* Default values should be listed in the description field.
* If a minimum or maximum value exists for a parameter then it should be listed in the description field.
* Time values should be referred to as `milliseconds since the Unix epoch` where applicable.

## Static site introduction

The following text is an introduction that can be added to each static site generated from an SDK after docstring comments have been added:

```markdown
# Ably `<Language>` Client Library SDK API Reference

The `<Language>` Client Library SDK supports a realtime and a REST interface. The `<Language>` API references are generated from the [Ably `<Language>` Client Library SDK source code](link-to-Ably-repo) using [`<Tool>`](link-to-tool) and structured by classes.

The realtime interface enables a client to maintain a persistent connection to Ably and publish, subscribe and be present on channels. The REST interface is stateless and typically implemented server-side. It is used to make requests such as retrieving statistics, token authentication and publishing to a channel.

**Note**: The `<Language>` Client Library SDK implements the realtime and REST interfaces as two separate libraries.

View the [Ably docs](http://ably.com/docs/) for conceptual information on using Ably, and for API references featuring all languages. The combined API references are organized by features and split between the [realtime](http://ably.com/docs/api/realtime-sdk) and [REST](http://ably.com/docs/api/rest-sdk) interfaces.
```

It can be amended as necessary, for example where an SDK implements the REST and realtime interfaces as two separate libraries.
