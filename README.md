# Canonical table

This repository is intended to be a language-agnostic reference for SDK developers to use when adding docstring comments to Ably SDKs.

The repository contains a set of tables in [descriptions.md](/descriptions.md) that complements the [Ably features spec](https://docs.ably.io/client-lib-development-guide/features). Each class and enum has its own table with an associated description for the class or enum. Every method and property is documented within the appropriate table.

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

```
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

The following text is an introduction that can be added to each static site generated from an SDK after docstring comments have been added. It can be amended as necessary, for example where an SDK implements the REST and realtime interfaces as two separate libraries.

```
# Ably `<Language>` Client Library SDK API Reference

The `<Language>` Client Library SDK supports a realtime and a REST interface.

The realtime interface enables a client to maintain a persistent connection to Ably and publish, subscribe and be present on channels. The REST interface is stateless and typically implemented server-side. It is used to make requests such as retrieving statistics, token authentication and publishing to a channel.

**Note**: The `<Language>` Client Library SDK implements the realtime and REST interfaces as two separate libraries.

The `<Language>` API references are generated from the [Ably `<Language>` Client Library SDK source code](link-to-Ably-repo) using [`<Tool>`](link-to-tool). View the [Ably docs](http://ably.com/docs/) for conceptual information on using Ably and for client library API references split between the [realtime](http://ably.com/docs/api/realtime-sdk) and [REST](http://ably.com/docs/api/rest-sdk) interfaces.
```