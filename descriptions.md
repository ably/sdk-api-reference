# Classes and types

## class Rest

The `Rest` object offers a simple stateless API to interact directly with Ably's REST API.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| constructor(keyStr: String) ||| RSC1 | Constructs a REST client object using an Ably API key string. |
|| `keyStr` ||| The Ably API key string used to validate the client. |
| constructor(tokenStr: String) ||| RSC1 | Constructs a REST client object using an Ably token string. |
|| `tokenStr` ||| The Ably API token string used to validate the client. |
| constructor(ClientOptions) ||| RSC1 | Construct a REST client object using an Ably [`ClientOptions`]{@link} object. |
|| `ClientOptions` ||| A [`ClientOptions`]{@link} object to configure the client connection to Ably. |
| auth: Auth ||| RSC5 | An [`Auth`]{@link} object. |
| push: Push ||| RSH7 | A [`Push`]{@link} object. |
| batch: BatchOperations ||| BO1 | A [`BatchOperations`]{@link} object. |
| device() => LocalDevice ||  | RSH8 | Retrieves a local device object. |
||| `LocalDevice` || A [`LocalDevice`]{@link} object that represents the current state of the device as a target for push notifications. |
| channels: `Channels<RestChannel>` ||| RSN1 | A [`Channel`]{@link} collection object. |
| request(String method, String path, Dict<String, String> params?, JsonObject \| JsonArray body?, Dict<String, String> headers?) => io HttpPaginatedResponse ||  | RSC19 | Makes a REST request to a provided path. This is provided as a convenience for developers who wish to use REST API functionality that is either not documented or is not yet included in the public API, without having to directly handle features such as authentication, paging, fallback hosts, MsgPack and JSON support. |
|| `method` ||| Request method to use such as `GET`, `POST`. |
|| `path` ||| Request path. |
|| `params` ||| Parameters for the REST request. |
|| `body` ||| JSON body for the request. |
|| `headers` ||| Headers for the request. |
||| `HttpPaginatedResponse` || An [`HttpPaginatedResponse`]{@link} response object returned by the HTTP request, containing an empty or JSON-encodable object. |
| stats(start: Time api-default epoch(), end: Time api-default now(), direction: .Backwards \| Forwards api-default .Backwards, limit: int api-default 100, unit: .Minute \| .Hour \| .Day \| .Month api-default .Minute => io `PaginatedResult<Stats>` ||| RSC6a | Queries the REST `/stats` API and retrieves your application's usage statistics. A [`PaginatedResult`]{@link} object is returned, containing an array of stats for the first page of results. `PaginatedResult` objects are iterable providing a means to page through historical statistics. See the [Stats docs](https://ably.com/docs/general/statistics). |
|| `start` | | RSC6b1 | The time from which stats are retrieved, specified as a Unix timestamp. |
|| `end` | | RSC6b1 | The time until stats are retrieved, specified as a Unix timestamp. |
|| `direction` | | RSC6b2 | The order for which stats are returned in. The default is `Backwards` which orders stats from most recent to oldest. |
|| `limit` | | RSC6b3 | An upper limit on the number of stats returned, up to 1000. |
|| `unit` | | RSC6b4 | `minute`, `hour`, `day` or `month`. Based on the unit selected, the given `start` or `end` times are rounded down to the start of the relevant interval depending on the unit granularity of the query. |
||| `PaginatedResult` | | A [`PaginatedResult`]{@link} object containing an array of stats for the first page of results. |
| time() => io Time ||| RSC16 | Retrieves the time from the Ably service as a Unix timestamp in milliseconds. Clients that do not have access to a sufficiently well maintained time source and wish to issue Ably `TokenRequest`s with a more accurate timestamp should use the `queryTime` property of the [`ClientOptions`]{@link} object instead of this method. |
||| `Time` || The time as a Unix timestamp. |

## class Realtime

The `Realtime` object extends the REST client and provides the functionality available in the REST client, in addition to realtime-specific features.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| constructor(keyStr: String) ||| RSC1 | Constructs a realtime client object using an Ably API key string. |
|| `keyStr` ||| The Ably API key string used to validate the client. |
| constructor(tokenStr: String) ||| RSC1 | Constructs a realtime client object using an Ably token string. |
|| `tokenStr` ||| The Ably API token string used to validate the client. |
| constructor(ClientOptions) ||| RSC1 | Constructs a realtime client object using an Ably [`ClientOptions`]{@link} object. |
|| `ClientOptions` ||| A [`ClientOptions`]{@link} object to configure the client connection to Ably. |
| auth: Auth ||| RTC4 | An [`Auth`]{@link} object. |
| push: Push ||| | A [`Push`]{@link} object. |
| device() => LocalDevice ||  | RSH8 | Retrieves a local device object. |
||| `LocalDevice` || A [`LocalDevice`]{@link} object that represents the current state of the device as a target for push notifications. |
| channels: `Channels<RealtimeChannel>` ||| RTC3, RTS1 | A [`Channel`]{@link} collection object. |
| clientId: String? ||| proxy for RSA7 | A client ID, used for identifying this client when publishing messages or for presence purposes. The `clientId` can be any non-empty string. This option is primarily intended to be used in situations where the library is instantiated with a key. A `clientId` may also be implicit in a token used to instantiate the library; an error will be raised if a `clientId` specified here conflicts with the `clientId` implicit in the token.|
| connection: Connection ||| RTC2 | A reference to the [`Connection`]{@link} object. |
| request(String method, String path, Dict<String, String> params?, JsonObject \| JsonArray body?, Dict<String, String> headers?) => io HttpPaginatedResponse ||| RTC9 | Makes a REST request to a provided path. This is provided as a convenience for developers who wish to use REST API functionality that is either not documented or is not yet included in the public API, without having to directly handle features such as authentication, paging, fallback hosts, MsgPack and JSON support. |
|| `method` ||| Request method to use such as `GET`, `POST`.|
|| `path` ||| Request path. |
|| `params` ||| Parameters for the REST request. |
|| `body` ||| JSON body for the request. |
|| `headers` ||| Headers for the request. |
||| `HttpPaginatedResponse` || An [`HttpPaginatedResponse`]{@link} response object returned by the HTTP request, containing an empty or JSON-encodable object. |
| stats: ||| Same as Rest.stats, RTC5a | Queries the REST `/stats` API and retrieves your application's usage statistics. A [`PaginatedResult`]{@link} object is returned, containing an array of stats for the first page of results. `PaginatedResult` objects are iterable providing a means to page through historical statistics. See the [Stats docs](https://ably.com/docs/general/statistics). |
| close() ||| proxy for RTN12 | Calls `connection.close()` and causes the connection to close, entering the closing state. Once closed, the library will not attempt to re-establish the connection without an explicit call to `connect()`. |
| connect() ||| proxy for RTN11 | Calls `connection.connect()` and causes the connection to open, entering the connecting state. Explicitly calling `connect()` is unnecessary unless the `autoConnect` property of the [`ClientOptions`]{@link} object is disabled. |
| time() => io Time ||| RTC6a | Retrieves the time from the Ably service as a Unix timestamp in milliseconds. Clients that do not have access to a sufficiently well maintained time source and wish to issue Ably `TokenRequest`s with a more accurate timestamp should use the [`queryTime`]{@link} property of the [`ClientOption`]{@link} object instead of this method. |
||| `Time` || The time as a Unix timestamp. |

## class ClientOptions

The `ClientOptions` object is a plain JavaScript object and is used in the `Ably.Realtime` constructor’s options argument. `ClientOptions` extends `AuthOptions`.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| embeds AuthOptions ||| TO3j | Embeds an [`AuthOptions`]{@link} object. |
| autoConnect: Bool default true ||| RTC1b, TO3e | When `true`, the client connects to Ably as soon as it is instantiated. You can optionally set this to `false` and explicitly connect to Ably when required using the [`connect()`]{@link} method. |
| clientId: String? ||| RSC17, RSA4, RSA15, TO3a | A client ID, used for identifying this client when publishing messages or for presence purposes. The `clientId` can be any non-empty string. This option is primarily intended to be used in situations where the library is instantiated with a key. Note that a `clientId` may also be implicit in a token used to instantiate the library. An error will be raised if a `clientId` specified here conflicts with the `clientId` implicit in the token. |
| defaultTokenParams: TokenParams? ||| TO3j11 | When a [`TokenParams`]{@link} object is provided, it overrides the client library defaults when issuing new Ably Tokens or Ably `TokenRequest`s. |
| echoMessages: Bool default true ||| RTC1a, TO3h | If `false`, prevents messages originating from this connection being echoed back on the same connection. |
| environment: String? ||| RSC15b, TO3k1 | Enables a [custom environment](https://ably.com/docs/platform-customization), region or cluster to be used with the Ably service. Please [contact us](https://ably.com/contact) if you require a custom environment. Note that once a custom environment is specified, the [fallback host functionality](https://faqs.ably.com/routing-around-network-and-dns-issues) is disabled by default. |
| logHandler: ||| platform specific - TO3c | Controls the log output of the library. This is a function to handle each line of log output. If handler is not specified, `console.log()` is used. |
| logLevel: ||| platform specific - TO3b | Controls the log output of the library. This is a number controlling the verbosity of the output. Valid values are: 0 (no logs), 1 (errors only), 2 (errors plus connection and channel state changes), 3 (abbreviated debug output), and 4 (full debug output). |
| logExceptionReportingUrl: String default "[library specific]" ||| TO3c (deprecated) | Defaults to a string value for an Ably error reporting DSN (Data Source Name), which is typically a URL in the format `https://[KEY]:[SECRET]@errors.ably.io/[ID]`. When set to `null`, `false` or an empty string (depending on what is idiomatic for the platform), exception reporting is disabled. |
| port: Int default 80 ||| TO3k4 | Enables a non-default Ably port to be specified. For development environments only. |
| queueMessages: Bool default true ||| RTP16b, TO3g | If `false`, this disables the default behavior whereby the library queues messages on a connection in the disconnected or connecting states. The default behavior enables applications to submit messages immediately upon instantiating the library without having to wait for the connection to be established. Applications may use this option to disable queueing if they wish to have application-level control over the queueing. |
| restHost: String default "rest.ably.io" ||| RSC12, TO3k2 | Enables a non-default Ably host to be specified. For development environments only. |
| realtimeHost: String default "realtime.ably.io" ||| RTC1d, TO3k3 | Enables a non-default Ably host to be specified for realtime connections. For development environments only. |
| fallbackHosts: String[] default nil ||| RSC15b, RSC15a, TO3k6 | An array of fallback hosts to be used in the case of an error necessitating the use of an alternative host. When a custom environment is specified, the [fallback host functionality](https://faqs.ably.com/routing-around-network-and-dns-issues) is disabled. If your customer success manager has provided you with a set of custom fallback hosts, please specify them here.|
| recover: String? ||| RTC1c, TO3i | Enables a connection to inherit the state of a previous connection that may have existed under a different instance of the Realtime library. This might typically be used by clients of the browser library to ensure connection state can be preserved when the user refreshes the page. A recovery key string can be explicitly provided, or alternatively if a callback function is provided, the client library will automatically persist the recovery key between page reloads and call the callback when the connection is recoverable. The callback is then responsible for confirming whether the connection should be recovered or not. See [connection state recovery](https://ably.com/docs/realtime/connection/#connection-state-recovery) for further information. |
| tls: Bool default true ||| RSC18, TO3d | Use a non-secure connection. By default, a TLS connection is used to connect to Ably. |
| tlsPort: Int default 443 ||| TO3k5 | Enables a non-default Ably TLS port to be specified. For development environments only. |
| useBinaryProtocol: Bool default true ||| TO3f | When `true`, the more efficient `MsgPack` binary encoding is used. When `false`, JSON text encoding is used. |
| transportParams: [String: Stringifiable]? ||| RTC1f | Can be used to pass in arbitrary connection parameters, such as [`heartbeatInterval`](https://ably.com/docs/realtime/connection#heartbeats) or [`remainPresentFor`](https://ably.com/docs/realtime/presence#unstable-connections). |
| addRequestIds: Bool default false ||| TO3p | If enabled, every REST request to Ably should include a random string in a `request_id` query string parameter. The random string is a url-safe base64-encoding sequence of at least 9 bytes, obtained from a source of randomness. This request ID must remain the same if a request is retried to a fallback host. Any log messages associated with the request should include the request ID. If the request fails, the request ID must be included in the [`ErrorInfo`]{@link} returned to the user. |
| disconnectedRetryTimeout: Duration default 15s ||| TO3l1 |  If the connection is still in the `DISCONNECTED` state after this delay, the client library will attempt to reconnect automatically. |
| suspendedRetryTimeout: Duration default 30s ||| RTN14d, TO3l2 | When the connection enters the `SUSPENDED` state, after this delay, if the state is still `SUSPENDED`, the client library attempts to reconnect automatically. |
| channelRetryTimeout: Duration default 15s ||| RTL13b, TO3l7 | When a channel becomes `SUSPENDED` following a server initiated `DETACHED`, after this delay, if the channel is still `SUSPENDED` and the connection is `CONNECTED`, the client library will attempt to re-attach the channel automatically. |
| httpOpenTimeout: Duration default 4s ||| TO3l3 | Timeout for opening the connection, available in the client library if supported by the transport. |
| httpRequestTimeout: Duration default 10s ||| TO3l4 | Timeout for any single HTTP request and response. |
| httpMaxRetryCount: Int default 3 ||| TO3l5 | The maximum number of fallback hosts to use as a fallback when an HTTP request to the primary host is unreachable or indicates that it is unserviceable. |
| httpMaxRetryDuration: Duration default 15s ||| TO3l6 | The maximum elapsed time in which fallback host retries for HTTP requests will be attempted. |
| maxMessageSize: Int default 65536 ||| TO3l8 | The maximum size of messages that can be published in one go. For realtime publishes, the default can be overridden by the `maxMessageSize` in the [`connectionDetails`]{@link}. |
| maxFrameSize: Int default 524288 ||| TO3l8 | The maximum size of a single POST body or WebSocket frame. This is mostly only relevant for a REST client request (for batch publishes), since publishes will hit the `maxMessageSize` limit before this. |
| plugins: `Dict<PluginType, Plugin>` ||| TO3o | A map between a [`PluginType`]{@link} and a `Plugin` object. The client library may cast a `Plugin` object to particular plugin subclass for a specific plugin type. |
| idempotentRestPublishing: bool default true ||| RSL1k1, RTL6a1, TO3n | When `true`, enables idempotent publishing by assigning a unique message ID client-side, allowing the Ably servers to discard automatic publish retries following a failure such as a network fault. |
| agents: [String: String?]? ||| RSC7d6 - interface only offered by some libraries | For use only by other Ably-authored SDKs, on a need-to-have basis. |

## class AuthOptions

The `AuthOptions` object is a plain JavaScript object used when making authentication requests. If passed in, an `AuthOptions` object will be used instead of the default values given when the library is instantiated.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| authCallback: ((TokenParams) -> io (String \| TokenDetails \| TokenRequest \| JsonObject))? ||| RSA4a, RSA4, TO3j5, AO2b | Called when a new token is required. The role of the callback is to obtain a fresh token, one of: an Ably Token string (in plain text format); a signed `TokenRequest`; a `TokenDetails` (in JSON format); an [Ably JWT](https://ably.com/docs/core-features/authentication#ably-jwt). See [the authentication documentation](https://ably.com/docs/realtime/authentication) for details of the Ably [`TokenRequest`]{@link} format and associated API calls. |
| authHeaders: [String: Stringifiable]? ||| RSA8c3, TO3j8, AO2e | A set of key-value pair headers to be added to any request made to the `authUrl`. Useful when an application requires these to be added to validate the request or implement the response. If the `authHeaders` object contains an `authorization` key, then `withCredentials` is set on the XHR request. |
| authMethod: .GET \| .POST default .GET ||| RSA8c, TO3j7, AO2d | The HTTP verb to use for the request, either `GET` or `POST`.  |
| authParams: [String: Stringifiable]? ||| RSA8c3, RSA8c1, TO3j9, AO2f | A set of key-value pair params to be added to any request made to the `authUrl`. When the `authMethod` is `GET`, query params are added to the URL, whereas when `authMethod` is `POST`, the params are sent as URL encoded form data. Useful when an application requires these to be added to validate the request or implement the response. |
| authUrl: String? ||| RSA4a, RSA4, RSA8c, TO3j6, AO2c | A URL that the library may use to obtain a token string (in plain text format), or a signed `TokenRequest` or `TokenDetails` (in JSON format) from. |
| key: String? ||| RSA11, RSA14, TO3j1, AO2a | The full API key string, as obtained from the [Ably dashboard](https://ably.com/dashboard). Use this option if you wish to use Basic authentication, or wish to be able to issue Ably Tokens without needing to defer to a separate entity to sign Ably `TokenRequest`s. Read more about [Basic authentication](https://ably.com/docs/core-features/authentication#basic-authentication). |
| queryTime: Bool default false ||| RSA9d, TO3j10, AO2a | If `true`, the library queries the Ably servers for the current time when issuing `TokenRequest`s instead of relying on a locally-available time of day. Knowing the time accurately is needed to create valid signed Ably [`TokenRequest`s](https://ably.com/docs/realtime/authentication#token-authentication), so this option is useful for library instances on auth servers where for some reason the server clock cannot be kept synchronized through normal means, such as an [NTP daemon](https://en.wikipedia.org/wiki/Ntpd). The server is queried for the current time once per client library instance (which stores the offset from the local clock), so if using this option you should avoid instancing a new version of the library for each request. |
| token: String? \| TokenDetails? \| TokenRequest? ||| RSA4a, RSA4, TO3j2 | An authenticated token. This can either be a `TokenDetails` object, a `TokenRequest` object, or token string (obtained from the `token` property of a `TokenDetails` component of an Ably `TokenRequest` response, or a JSON Web Token satisfying [the Ably requirements for JWTs](https://ably.com/docs/core-features/authentication#ably-jwt)). This option is mostly useful for testing: since tokens are short-lived, in production you almost always want to use an authentication method that enables the client library to renew the token automatically when the previous one expires, such as `authUrl` or `authCallback`. Read more about [Token authentication](https://ably.com/docs/core-features/authentication#token-authentication).|
| tokenDetails: TokenDetails? ||| RSA4a, RSA4, TO3j3 | An authenticated `TokenDetails` object (most commonly obtained from an Ably Token Request response). This option is mostly useful for testing: since tokens are short-lived, in production you almost always want to use an authentication method that enables the client library to renew the token automatically when the previous one expires, such as `authUrl` or `authCallback`. Use this option if you wish to use Token authentication. Read more about [Token authentication](https://ably.com/docs/core-features/authentication#token-authentication). |
| useTokenAuth: Bool? ||| RSA4, RSA14, TO3j4 | When `true`, forces token authentication to be used by the library. If a `clientId` is not specified in the [`ClientOptions`]{@link} or [`TokenParams`]{@link}, then the Ably Token issued is [anonymous](https://ably.com/docs/core-features/authentication#identified-clients). |

## class TokenParams

The `TokenParams` object is a plain JavaScript object and is used to define Ably token characteristics when performing a token request.

|  Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| capability: String api-default `'{"*":["*"]}'` ||| RSA9f, TK2b | The permissions associated with this Ably Token. The capability is a JSON stringified canonicalized representation of the resource paths and associated operations. Read more about capbilities in the [capabilities docs](https://ably.com/docs/core-features/authentication/#capabilities-explained). |
| clientId: String? ||| TK2c | A client ID, used for identifying this client when publishing messages or for presence purposes. The `clientId` can be any non-empty string. This option is primarily intended to be used in situations where the library is instantiated with a key. Note that a `clientId` may also be implicit in a token used to instantiate the library. An error is raised if a `clientId` specified here conflicts with the `clientId` implicit in the token. Find out more about [identified clients](https://ably.com/docs/core-features/authentication#identified-clients). |
| nonce: String? ||| RSA9c, Tk2d | An unquoted, un-escaped random string of at least 16 characters, used to ensure the [`TokenRequest`]{@link} cannot be reused. |
| timestamp: Time? ||| RSA9d, Tk2d | The Unix timestamp of this request. Timestamps, in conjunction with the `nonce`, are used to prevent requests from being replayed. `timestamp` is a "one-time" value, and is valid in a request, but is not validly a member of any default token params such as `ClientOptions.defaultTokenParams`. |
| ttl: Duration api-default 60min ||| RSA9e, TK2a | Requested time to live for the token in milliseconds.  |

## class Auth

The `Auth` object creates Ably `TokenRequest` objects with `createTokenRequest` or is used to obtain Ably Tokens from Ably with `requestToken`, and then issue them to less trusted clients.

|  Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| clientId: String? ||| RSA7, RSC17, RSA12 | A client ID, used for identifying this client when publishing messages or for presence purposes. The `clientId` can be any non-empty string. This option is primarily intended to be used in situations where the library is instantiated with a key. Note that a `clientId` may also be implicit in a token used to instantiate the library. An error is raised if a `clientId` specified here conflicts with the `clientId` implicit in the token. Find out more about [identified clients](https://ably.com/docs/core-features/authentication#identified-clients). |
| authorize(TokenParams?, AuthOptions?) => io TokenDetails ||| RSA10 | Instructs the library to get a new token immediately. When using the realtime client, it upgrades the current realtime connection to use the new token, or if not connected, initiates a connection to Ably, once the new token has been obtained. Also stores any `tokenParams` and `authOptions` passed in as the new defaults, to be used for all subsequent implicit or explicit token requests. Any `tokenParams` and `authOptions` objects passed in entirely replace (as opposed to being merged with) the currently client library saved `tokenParams` and `authOptions`. |
|| `TokenParams` ||| A [`TokenParams`]{@link} object. |
|| `AuthOptions` ||| An [`AuthOptions`]{@link} object. |
||| `TokenDetails` ||  A [`TokenDetails`]{@link} object. |
| createTokenRequest(TokenParams?, AuthOptions?) => io TokenRequest ||| RSA9 | Creates and signs an Ably `TokenRequest` based on the specified (or if none specified, the client library stored) `tokenParams` and `authOptions`. Note this can only be used when the API `key` value is available locally. Otherwise, the Ably `TokenRequest` must be obtained from the key owner. Use this to generate an Ably `TokenRequest` in order to implement an Ably Token request callback for use by other clients. Both `authOptions` and `tokenParams` are optional. When omitted or `null`, the default token parameters and authentication options for the client library are used, as specified in the `ClientOptions` when the client library was instantiated, or later updated with an explicit `authorize` request. Values passed in are used instead of (rather than being merged with) the default values. To understand why an Ably `TokenRequest` may be issued to clients in favor of a token, see [Token Authentication explained](https://ably.com/docs/core-features/authentication/#token-authentication). |
|| `TokenParams` ||| A [`TokenParams`]{@link} object. |
|| `AuthOptions` ||| An [`AuthOptions`]{@link} object. |
||| `TokenRequest` || A [`TokenRequest`]{@link} object. |
| requestToken(TokenParams?, AuthOptions?) => io TokenDetails ||| RSA8e | Calls the `requestToken` REST API endpoint to obtain an Ably Token according to the specified `tokenParams` and `authOptions`. Both `authOptions` and `tokenParams` are optional. When omitted or `null`, the default token parameters and authentication options for the client library are used, as specified in the `ClientOptions` when the client library was instantiated, or later updated with an explicit `authorize` request. Values passed in are used instead of (rather than being merged with) the default values. To understand why an Ably `TokenRequest` may be issued to clients in favor of a token, see [Token Authentication explained](https://ably.com/docs/core-features/authentication/#token-authentication). |
|| `TokenParams` ||| A [`TokenParams`]{@link} object. |
|| `AuthOptions` ||| An [`AuthOptions`]{@link} object. |
||| `TokenDetails` || A [`TokenDetails`]{@link} object. |


## class TokenDetails

The `TokenDetails` object represents an Ably token string and its associated metadata.

|  Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| +fromJson(String \| JsonObject) -> TokenDetails ||| TD7 | A static factory method to create a `TokenDetails` object from a deserialized TokenDetails-like object or a JSON stringified `TokenDetails` object. This method is provided to minimize bugs as a result of differing types by platform for fields such as `timestamp` or `ttl`. For example, in Ruby `ttl` in the `TokenDetails` object is exposed in seconds as that is idiomatic for the language, yet when serialized to JSON using `to_json` it is automatically converted to the Ably standard which is milliseconds. By using the `fromJson` method when constructing a `TokenDetails` object, Ably ensures that all fields are consistently serialized and deserialized across platforms. |
||| `TokenDetails` || An Ably authentication token. |
| capability: String ||| TD5 | The permissions associated with this Ably Token. The capability is a JSON stringified canonicalized representation of the resource paths and associated operations. Read more about capbilities in the [capabilities docs](https://ably.com/docs/core-features/authentication/#capabilities-explained). |
| clientId: String? ||| TD6 | The client ID, if any, bound to this Ably Token. If a client ID is included, then the Ably Token authenticates its bearer as that client ID, and the Ably Token may only be used to perform operations on behalf of that client ID. The client is then considered to be an [identified client](https://ably.com/docs/core-features/authentication#identified-clients). |
| expires: Time ||| TD3 | The Unix timestamp at which this token expires. |
| issued: Time ||| TD4 | The Unix timestamp at which this token was issued. |
| token: String ||| TD2 | The [Ably Token](https://ably.com/docs/core-features/authentication#ably-tokens) itself. A typical Ably Token string appears with the form `xVLyHw.A-pwh7wicf3afTfgiw4k2Ku33kcnSA7z6y8FjuYpe3QaNRTEo4`. |

## class TokenRequest

The `TokenRequest` object represents properties used to generate an Ably TokenRequest. Tokens are generated using `Auth.requestToken`.

|  Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| +fromJson(String \| JsonObject) -> TokenRequest ||| TE6 | A static factory method to create a `TokenRequest` object from a deserialized TokenRequest-like object or a JSON stringified `TokenRequest` object. This method is provided to minimize bugs as a result of differing types by platform for fields such as `timestamp` or `ttl`. For example, in Ruby `ttl` in the `TokenRequest` object is exposed in seconds as that is idiomatic for the language, yet when serialized to JSON using `to_json` it is automatically converted to the Ably standard which is milliseconds. By using the `fromJson` method when constructing a `TokenRequest` object, Ably ensures that all fields are consistently serialized and deserialized across platforms. |
||| `TokenRequest` || An Ably token request object. |
| capability: String ||| TE3 | Capability of the requested Ably Token. If the Ably TokenRequest is successful, the capability of the returned Ably Token will be the intersection of this capability with the capability of the issuing key. The capability is a JSON stringified canonicalized representation of the resource paths and associated operations. Read more about capabilities in the [capabilities docs](https://ably.com/docs/realtime/authentication). |
| clientId: String? ||| TE2 | The client ID to associate with the requested Ably Token. When provided, the Ably Token may only be used to perform operations on behalf of that client ID. |
| keyName: String ||| TE2 | The name of the key against which this request is made. The key name is public, whereas the key secret is private. |
| mac: String ||| TE2 | The Message Authentication Code for this request. |
| nonce: String ||| TE2 | An opaque nonce string of at least 16 characters. |
| timestamp: Time? ||| TE5 | The Unix timestamp of this request in milliseconds. |
| ttl: Duration? api-default 60min ||| TE4 | Requested time to live for the Ably Token in milliseconds. If the Ably `TokenRequest` is successful, the TTL of the returned Ably Token is less than or equal to this value, depending on application settings and the attributes of the issuing key. |

## class `Channels<ChannelType>`

The `Channels` object is used to create and destroy [`Channel`]{@link} objects.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| exists(String) -> Bool || | RSN2, RTS2 | Checks if a certain channel exists. |
|| `String` ||| The channel name. |
||| `Bool` || `true` if the channel exists, otherwise `false`. |
| get(String) -> ChannelType ||| RSN3a, RTS3a | Creates a new `ChannelType`, or returns the existing channel object. |
|| `String` ||| The channel name. |
||| `ChannelType` || A `ChannelType` object. |
| get(String, ChannelOptions) -> ChannelType ||| RSN3c, RTS3c | Creates a new `ChannelType` object, with the specified [`ClientOptions`]{@link}, or returns the existing channel object. |
|| `String` ||| The channel name. |
|| `ChannelOptions` ||| [`ChannelOptions`]{@link} used to configure the channel. |
||| `ChannelType` || A `ChannelType` object. |
| iterate() -> `Iterator<ChannelType>` ||| RSN2, RTS2 | Iterates through the existing channels. |
||| `ChannelType` || Each iteration returns a `ChannelType` object. |
| release(String) ||| RSN4, RTS4 | Releases a [`Channel`]{@link} object, deleting it, and enabling it to be garbage collected. It also removes any listeners associated with the channel. To release a channel, the [`ChannelState`]{@link} must be `initialized`, `detached`, or `failed`. |
|| `String` ||| The channel name. |

## class RestChannel

The `RestChannel` object is used to interact with a specific channel instance. A channel instance is created or returned by [`channels.get()`]{@link}.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| name: String? |||| A unique channel name. |
| presence: RestPresence ||| RSL3 | The [`Presence`]{@link} object associated with the channel. Enables the retrieval of presence members on the channel. |
| history(start: Time, end: Time api-default now(), direction: .Backwards \| .Forwards api-default .Backwards, limit: int api-default 100) => io `PaginatedResult<Message>` ||| RSL2a | Retrieves a paginated list of historical messages for the channel. |
|| `start` || RSL2b1 | The time from which messages are retrieved, specified as a Unix timestamp. |
|| `end` || RSL2b1 | The time until messages are retrieved, specified as a Unix timestamp. |
|| `direction` || RSL2b2 | The order for which messages are returned in. The default is `Backwards` which orders messages from most recent to oldest. |
|| `limit` || RSL2b3 | An upper limit on the number of messages returned. The default is 100. |
||| `PaginatedResult<Message>` || A paginated list of [`Message`]{@link} objects. |
| status() => ChannelDetails ||| RSL8 | Retrieves metadata for the channel, such as status and occupancy metrics. Returns a [`ChannelDetails`]{@link} object. |
| publish(Message, params?: `Dict<String, Stringifiable>`) => io ||| RSL1 | Sends a message to the channel. |
|| `Message` ||| A [`Message`]{@link} object. |
|| `params` ||| Optional parameters, such as [`quickAck`](https://faqs.ably.com/why-are-some-rest-publishes-on-a-channel-slow-and-then-typically-faster-on-subsequent-publishes) sent as part of the query string. |
| publish([Message], params?: `Dict<String, Stringifiable>` ||| RSL1 | Sends an array of messages to the channel. |
|| [`Message`] ||| An array of [`Message`]{@link} objects. |
|| `params` ||| Optional parameters, such as [`quickAck`](https://faqs.ably.com/why-are-some-rest-publishes-on-a-channel-slow-and-then-typically-faster-on-subsequent-publishes) sent as part of the query string. |
| publish(name: String?, data: Data?) => io ||| RSL1 | Sends a message to the channel. |
|| `name` ||| The name of the message. |
|| `data` ||| The payload of the message. |
| setOptions(options: ChannelOptions) => io ||| RSL7 | Sets the [`ChannelOptions`]{@link} for the channel, such as encryption-related parameters. |
|| `options` ||| The [`ChannelOptions`]{@link} to set for the channel. |
| push: PushChannel ||| RSH4 | The [`PushChannel`]{@link} object associated with the channel. This enables devices to subscribe to push notifications for the channel. |

## class RealtimeChannel

The `RealtimeChannel` object handles all incoming messages and presence messages when it is attached. Incoming is defined as "received from Ably over the realtime transport".

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| embeds `EventEmitter<ChannelEvent, ChannelStateChange?>` ||| RTL2a, RTL2d, RTL2e | The `RealtimeChannel` implements [`EventEmitter`]{@link} and emits [`ChannelEvent`]{@link} events, where a `ChannelEvent` is either a [`ChannelState`]{@link} or `UPDATE`. |
| errorReason: ErrorInfo? ||| RTL4e | An error as an [`ErrorInfo`]{@link} object when a channel failure occurs. |
| state: ChannelState ||| RTL2b | The current [`ChannelState`]{@link} of this [`Channel`]{@link}. |
| presence: RealtimePresence ||| RTL9 | Provides access to the [`Presence`]{@link} object for this channel which can be used to access members present on the channel, or participate in presence. |
| properties: ChannelProperties ||| CP1, RTL15 | A [`ChannelProperties`]{@link} object representing properties of the channel state. |
| push: PushChannel |||| Provides access to the [`PushChannel`]{@link} object for this channel. |
| modes: readonly [ChannelMode] ||| RTL4m | An array of [`ChannelMode`]{@link} objects. |
| params: readonly `Dict<String, String>` ||| RTL4k1 | Optional [channel parameters](https://ably.com/docs/realtime/channels/channel-parameters/overview) that configure the behavior of the channel. |
| attach() => io ||| RTL4d | Attach to this channel ensuring the channel is created in the Ably system and all messages published on the channel are received by any channel listeners registered using [`subscribe()`]{@link}. Any resulting channel state change will be emitted to any listeners registered using the on or once methods. As a convenience, [`attach()`]{@link} is called implicitly if [`subscribe()`]{@link} for the channel is called, or [`enter()`]{@link} or [`subscribe()`]{@link} is called on the [`Presence`]{@link} object for this channel. |
| detach() => io ||| RTL5e | Detach from this channel. Any resulting channel state change is emitted to any listeners registered using the [`on`]{@link} or [`once`]{@link} methods of the [`EventEmitter`]{@link} object. Once all clients globally have detached from the channel, the channel will be released in the Ably service within two minutes. |
| history(start: Time, end: Time api-default now(), direction: .Backwards \| .Forwards api-default .Backwards, limit: int api-default 100, untilAttach: Bool default false) => io `PaginatedResult<Message>` ||| RSL2a | Retrieves a paginated set of historical messages for this channel. If the channel is configured to persist messages to disk, then message history will typically be available for 24 – 72 hours. If not, messages are only retained in memory by the Ably service for two minutes. |
|| `start` || RTL10a | The time from which messages are retrieved, specified as a Unix timestamp. |
|| `end` || RTL10a | The time until messages are retrieved, specified as a Unix timestamp. |
|| `direction` || RTL10a | The order for which messages are returned in. The default is `Backwards` which orders messages from most recent to oldest. |
|| `limit` || RTL10a | An upper limit on the number of messages returned, up to 1000. |
|| `untilAttach` || RTL10b | When `true`, ensures message history is up until the point of the channel being attached. See [continuous history](https://ably.com/docs/realtime/history#continuous-history) for more info. Requires the direction to be backwards (the default). If the channel is not attached, or if direction is set to `forwards`, this option results in an error. |
||| `PaginatedResult<Message>` || A paginated list of [`Message`]{@link} objects. |
| publish(Message) => io ||| RTL6i | Sends a message on this channel. A callback may optionally be passed in to this call to be notified of success or failure of the operation. When publish is called with this client library, it won't attempt to implicitly attach to the channel. |
|| `Message` ||| A [`Message`]{@link} object. |
| publish([Message]) => io ||| RTL6i | Sends several messages on this channel. A callback may optionally be passed in to this call to be notified of success or failure of the operation. When publish is called with this client library, it won't attempt to implicitly attach to the channel. |
|| [`Message`] ||| An array of [`Message`]{@link} objects. |
| publish(name: String?, data: Data?) => io ||| RTL6i | Sends a single message on this channel based on a given event name and payload. A callback may optionally be passed in to this call to be notified of success or failure of the operation. When publish is called with this client library, it won't attempt to implicitly attach to the channel, so long as [transient publishing](https://ably.com/docs/realtime/channels#transient-publish) is available in the library. Otherwise, the client will implicitly attach. |
|| `name` ||| Event name. |
|| `data` ||| Message payload. |
| subscribe((Message) ->) => io ||| RTL7a | Registers a listener for messages on this channel. The caller supplies a listener function, which is called each time one or more messages arrives on the channel. |
|| `(Message)` ||| Event listener function. |
| subscribe(String, (Message) ->) => io ||| RTL7b | Registers a listener for messages with a given event `name` on this channel. The caller supplies a listener function, which is called each time one or more matching messages arrives on the channel. |
|| `String` ||| Event name. |
|| `(Message)` ||| Event listener function. |
| subscribe([String], (Message) ->) => io ||| RTL7a | Registers a listener for messages on this channel for multiple event name values. |
|| [`String`] ||| An array of event names. |
|| `(Message)` ||| Event listener function. |
| unsubscribe(String, (Message) ->) ||| RTL8a | Deregisters the given listener for the specified event name. This removes an earlier event-specific subscription. |
|| `String` ||| Event name. |
|| `(Message)` ||| Event listener function. |
| unsubscribe((Message) ->) ||| RTL8a | Deregisters the given listener (for any/all event names). This removes an earlier subscription. |
|| `(Message)` ||| Event listener function. |
| unsubscribe([String], (Message) ->) ||| RTL8a | Deregisters the given listener from all event names in the array. |
|| [`String`] ||| An array of event names. |
|| `(Message)` ||| Event listener function. |
| unsubscribe(String) ||| RTL8a | Deregisters all listeners for the given event name. |
|| `String` ||| Event name. |
| unsubscribe([String]) ||| RTL8a | Deregisters all listeners for all event names in the array. |
|| [`String`] ||| An array of event names. |
| unsubscribe() ||| RTL8a, RTE5 | Deregisters all listeners to messages on this channel. This removes all earlier subscriptions. |
| setOptions(options: ChannelOptions) => io ||| RTL16 | Sets the [`ChannelOptions`]{@link} for the channel. |
|| `options` ||| A [`ChannelOptions`]{@link} object. |

## class BatchOperations

The `BatchOperations` object is used to publish messages to multiple channels, or retrieve the presence state from multiple channels, as batch operations. 

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| publish([BatchSpec]) => `BatchResult<BatchPublishResponse>` ||| BO2a | Sends an array of [`BatchSpec`]{@link} objects to one or more channels, up to a maximum of 100 channels. Each `BatchSpec` object can contain a single message or an array of messages. Returns a [`BatchResult<BatchPublishResponse>`]{@link} object. |
|| [`BatchSpec`] ||| An array of [`BatchSpec`]{@link} objects. |
||| `BatchResult<BatchPublishResponse>` || A [`BatchResult<BatchPublishResponse>`]{@link} object. |
| publish(BatchSpec) => `BatchResult<BatchPublishResponse>` ||| BO2a | Sends a [`BatchSpec`]{@link} object to one or more channels, up to a maximum of 100 channels. A `BatchSpec` object can contain a single message or an array of messages. Returns a [`BatchResult<BatchPublishResponse>`]{@link} object. |
|| `BatchSpec` ||| A [`BatchSpec`]{@link} object. |
| getPresence([String]) => `BatchResult<BatchPresenceResponse>` ||| BO2b | Retrieves the presence state for one or more channels, up to a maximum of 100 channels. Presence state includes the `clientId` of members and their current [`PresenceAction`]{@link}. Returns a [`BatchResult<BatchPresenceResponse>`]{@link} object. |
|| [`String`] ||| An array of one or more channel names, up to a maximum of 100. |

## class `BatchResult<T>`

The `BatchResult<T>` object contains the results of a batch operation.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| error: ErrorInfo? ||| BPA2b | Describes the reason for which a batch operation failed, or states that the batch operation was only partially successful as an [`ErrorInfo`]{@link} object. Will be `null` if the operation was successful. |
| responses: []T? ||| BPA2a | An array of [`BatchPublishResponse`]{@link} or [`BatchPresenceResponse`]{@link} objects that contain details of successful and partially successful batch operations. |

## class BatchPublishResponse

The `BatchPublishResponse` object contains the response information for each batch publish operation.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| channel: String ||| BPB2a | The channel name a message was successfully published to, or the channel name for which an `error` was returned. |
| messageId: String? ||| BPB2b | The unique ID for a successfully published message. |
| error: ErrorInfo? ||| BPB2c | Describes the reason for which a message, or messages failed to publish to a channel as an [`ErrorInfo`]{@link} object. |

## class BatchPresenceResponse

The `BatchPresenceResponse` contains the response information for each batch presence operation.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| channel: String ||| BPD2a | The channel name the presence state was retrieved for. |
| presence: []BatchPresence ||| PBD2b | An array of [`BatchPresence`]{@link} objects that contains details of the presence state for a channel, such as the `clientId` of members and their current [`PresenceAction`]{@link}. |

## class BatchPresence

The `BatchPresence` object contains the presence state of each batch presence request.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| clientId: string |||| The ID of each client entered into the presence set for the channel. |
| action: string? |||| The [`PresenceAction`]{@link} associated with each client. |
| error: ErrorInfo? |||| Describes the reason for which the presence details could not be retrieved for a channel as an [`ErrorInfo`]{@link} object. |

## class PushChannel

The `PushChannel` object enables devices to subscribe to push notifications for the channel.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| subscribeDevice() => io ||| RSH7a | Subscribes the device to push notifications for the channel. |
| subscribeClient() => io ||| RSH7b | Subscribes all devices associated with the current device's `clientId` to push notifications for the channel. |
| unsubscribeDevice() => io ||| RSH7c | Unsubscribes the device from receiving push notifications for the channel. |
| unsubscribeClient() => io ||| RSH7d | Unsubscribes all devices associated with the current device's `clientId` from receiving push notifications for the channel. |
| listSubscriptions() => io `PaginatedResult<PushChannelSubscription>` ||| RSH7e | |
||| `PaginatedResult<PushChannelSubscription>` || |

## class BatchSpec

The `BatchSpec` object contains the channel names and messages to batch publish to. 

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| channels: [String] || An array of channel names to publish messages to. |
| messages: [Message] || An array of [`Message`]{@link} objects to publish. |

## enum ChannelState

`ChannelState` describes the possible states of a `Channel`.

| Enum | Spec | Description |
|---|---|---|
| INITIALIZED || A `Channel` object having this state has been initialized but no attach has yet been attempted. |
| ATTACHING || An attach has been initiated by sending a request to Ably. This is a transient state, followed either by a transition to `ATTACHED`, `SUSPENDED`, or `FAILED`. |
| ATTACHED || The attach has succeeded. In the `ATTACHED` state a client may publish and subscribe to messages, or be present on the channel. |
| DETACHING || A detach has been initiated on an `ATTACHED` `Channel` by sending a request to Ably. This is a transient state, followed either by a transition to `DETACHED` or `FAILED`. |
| DETACHED || The `Channel`, having previously been `ATTACHED`, has been detached by the user. |
| SUSPENDED || The `Channel`, having previously been `ATTACHED`, has lost continuity, usually due to the client being disconnected from Ably for longer than two minutes. It will automatically attempt to reattach as soon as connectivity is restored. |
| FAILED || An indefinite failure condition. This state is entered if a `Channel` error has been received from the Ably service, such as an attempt to attach without the necessary access rights. |

## enum ChannelEvent

`ChannelEvent` describes the events emitted by a `Channel`. An event is either an `UPDATE` or a `ChannelState`.

| Enum | Spec | Description |
|---|---|---|
| embeds ChannelState || The event contains a [`ChannelState`]{@link}. |
| UPDATE | RTL2g | An event for changes to channel conditions that do not result in a change in [`ChannelState`]{@link}. |

## enum ChannelMode

`ChannelMode` describes the possible flags used to configure client capabilities.

| Enum | Spec | Description |
|---|---|---|
| PRESENCE || The client can enter the presence set. |
| PUBLISH || The client can publish messages. |
| SUBSCRIBE || The client can subscribe to messages. |
| PRESENCE_SUBSCRIBE || The client can receive presence messages. |

## class ChannelStateChange

The `ChannelStateChange`  object encapsulates state change information emitted by the `Channel` object.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| current: ChannelState ||| RTL2a, RTL2b | The new current [`ChannelState`]{@link}. |
| event: ChannelEvent ||| TH5 | The event that triggered this [`ChannelState`]{@link} change. |
| previous: ChannelState ||| RTL2a, RTL2b | The previous state. For the `update` event, this is equal to the `current` [`ChannelState`]{@link}. |
| reason: ErrorInfo? ||| RTL2e, TH3 | An [`ErrorInfo`]{@link} object containing any information relating to the transition. |
| resumed: Boolean ||| RTL2f, TH4 | Indicates whether message continuity on this channel is preserved, see [Nonfatal channel errors](https://ably.com/docs/realtime/channels#nonfatal-errors) for more info. |

## class ChannelOptions

The `ChannelOptions` object is used when creating a channel object, to configure the channel.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|----|
| +withCipherKey(key: Binary \| String)? -> ChannelOptions ||| TB3 | Constructor `withCipherKey`, that takes a key only. |
|| `key` ||| A private key used to encrypt and decrypt payloads. |
||| `ChannelOptions` || A [`ChannelOptions`]{@link} object. |
| cipher: (CipherParams \| Params)? ||| RSL5a, TB2b | Requests encryption for this channel when not null, and specifies encryption-related parameters (such as algorithm, chaining mode, key length and key). See [an example](https://ably.com/docs/realtime/encryption#getting-started). |
| params?: `Dict<String, String>` ||| TB2c | [Channel Parameters](https://ably.com/docs/realtime/channels/channel-parameters/overview) that configure the behavior of the channel. |
| modes?: [ChannelMode] ||| TB2d | For realtime client libraries only. An array of [`ChannelMode`]{@link} objects. |

## class ChannelDetails

The `ChannelDetails` object represents information for a channel including `channelId` and `status`.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| channelId: String ||| CHD2a | The identifier of the channel. |
| status: ChannelStatus ||| CHD2b | A [`ChannelStatus`]{@link} object. |

## class ChannelStatus

The `ChannelStatus` object contains the status and occupancy of a channel.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| isActive: Boolean ||| CHS2a | If `true`, the channel is active, otherwise `false`. |
| occupancy: ChannelOccupancy ||| CHS2b | A [`ChannelOccupancy`]{@link} object. |

## class ChannelOccupancy

The `ChannelOccupancy` object contains channel metrics.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| metrics: ChannelMetrics ||| CHO2a | A [`ChannelMetrics`]{@link} object. |

## class ChannelMetrics

The `ChannelMetrics` object contains the count of `publishers` and `subscribers`, `connections` and `presenceConnections`, `presenceMembers` and `presenceSubscribers`.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| connections: Int ||| CHM2a | The number of realtime connections attached to the channel. |
| presenceConnections: Int ||| CHM2b | The number of realtime connections attached to the channel with permission to enter the presence set, regardless of whether or not they have entered it. This requires the `presence` capability and for a client to not have specified a [`ChannelMode`]{@link} flag that excludes `PRESENCE`. |
| presenceMembers: Int ||| CHM2c | The number of members in the presence set of the channel. |
| presenceSubscribers: Int ||| CHM2d | The number of realtime attachments receiving presence messages on the channel. This requires the `subscribe` capability and for a client to not have specified a [`ChannelMode`]{@link} flag that excludes `PRESENCE_SUBSCRIBE`. |
| publishers: Int ||| CHM2e | The number of realtime attachments permitted to publish messages to the channel. This requires the `publish` capability and for a client to not have specified a [`ChannelMode`]{@link} flag that excludes `PUBLISH`. |
| subscribers: Int ||| CHM2f | The number of realtime attachments receiving messages on the channel. This requires the `subscribe` capability and for a client to not have specified a [`ChannelMode`]{@link} flag that excludes `SUBSCRIBE`. |

## class CipherParams

The `CipherParams` object contains properties to configure encryption for a channel.

| Method / Property | Parameter | Spec | Description |
|---|---|---|---|
| algorithm: String default "AES" || TZ2a | The algorithm to use for encryption. Only `AES` is supported. |
| key: Binary || TZ2d | The private key used to encrypt and decrypt payloads. |
| keyLength: Int || TZ2b | The length of the key in bits; for example 128 or 256. |
| mode: String default "CBC" || TZ2c | The cipher mode. Only `CBC` is supported. |

## class Crypto

The `Crypto` object ensures that message payloads are encrypted, can never be decrypted by Ably, and can only be decrypted by other clients that share the same secret symmetric key.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| +getDefaultParams(Params) -> CipherParams ||| RSE1 | Retrieves, or optionally sets, the [`CipherParams`]{@link} for the channel. |
|| `Params` ||| Overrides the default parameters. A suitable `key` must be provided as a minimum. |
||| `CipherParams` || A [`CipherParams`]{@link} object, using the default values for any field not supplied. |
| +generateRandomKey(keyLength: Int?) => io Binary ||| RSE2 | Generates a random key to be used in the encryption of the channel. |
|| `keyLength` ||| The length of the key, in bits, to be generated. If not specified, this is equal to the default `keyLength` of the default algorithm: for AES this is 256 bits. |
||| `Binary` || The key as a binary, for example, a byte array. If the language cryptographic randomness primitives are blocking or async, a callback is used. The callback returns the generated binary key. |

## class RestPresence

The `RestPresence` object associated with a channel, enabling the retrieval of the current and historic presence set for the channel.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| get(limit: int api-default 100, clientId: String?, connectionId: String?) => io `PaginatedResult<PresenceMessage>` ||| RSPa | Retrieves the current members present on the channel and the metadata for each member, such as their [`PresenceAction`]{@link} and ID. Returns a paginated list of [`PresenceMessage`]{@link} objects. |
|| `limit` || RSP3a | An upper limit on the number of messages returned. |
|| `clientId` || RSP3a2 | Filters the list of returned presence members by a specific client using its ID. |
|| `connectionId` || RSP3a3 | Filters the list of returned presence members by a specific connection using its ID. |
||| `PaginatedResult<PresenceMessage>` || A paginated list of [`PresenceMessage`]{@link} objects. |
| history(start: Time, end: Time api-default now(), direction: .Backwards \| .Forwards api-default .Backwards, limit: int api-default 100) => io `PaginatedResult<PresenceMessage>` ||| RSP4a | Retrieves a list of historic presence messages that occurred on the channel. Returns a paginated list of [`PresenceMessage`]{@link} objects. |
|| `start` || RSP4b1 | The time from which messages are retrieved, specified as a Unix timestamp. |
|| `end` || RSP4b1 | The time until messages are retrieved, specified as a Unix timestamp. |
|| `direction` || RSP4b2 | The order for which messages are returned in. The default is `Backwards` which orders messages from most recent to oldest. |
|| `limit` || RSP4b3 | An upper limit on the number of messages returned. |
||| `PaginatedResult<PresenceMessage>` || A paginated list of [`PresenceMessage`]{@link} objects. |

## class RealtimePresence

The `RealtimePresence` object associated with a channel, enabling clients to enter, update and leave the presence set and for the retrieval of the current and historic presence set for the channel.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| syncComplete: Bool ||| RTP13 | Shows whether the presence set synchronization between Ably and the clients on the channel has been completed. Set to `true` when the sync is complete. |
| get(waitForSync: Bool default true, clientId: String?, connectionId: String?) => io [`PresenceMessage`] ||| RTP11 | Retrieves the current members present on the channel and the metadata for each member, such as their [`PresenceAction`]{@link} and ID. Returns an array of [`PresenceMessage`]{@link} objects. |
|| `waitForSync` || RTP11c1 | Sets whether to wait for a full presence set synchronization between Ably and the clients on the channel to complete before returning the results. Synchronization begins as soon as the channel is [`attached`]{@link}. When set to `true` the results will be returned as soon as the sync is complete. When set to `false` the current list of members will be returned without the sync completing. |
|| `clientId` || RTP11c2 | Filters the array of returned presence members by a specific client using its ID. |
|| `connectionId` || RTP11c3 | Filters the array of returned presence members by a specific connection using its ID. |
||| [`PresenceMessage`] || An array of [`PresenceMessage`]{@link} objects. |
| history(start: Time, end: Time, direction: .Backwards \| .Forwards api-default .Backwards, limit: int api-default 100) => io `PaginatedResult<PresenceMessage>` ||| RTP12c | Retrieves a list of historic presence messages that occurred on the channel. Returns a paginated list of [`PresenceMessage`]{@link} objects. |
|| `start` || RTP12a | The time from which messages are retrieved, specified as a Unix timestamp. |
|| `end` || RTP12a | The time until messages are retrieved, specified as a Unix timestamp. |
|| `direction` || RTP12a | The order for which messages are returned in. The default is `Backwards` which orders messages from most recent to oldest. |
|| `limit` || RTP12a | An upper limit on the number of messages returned. |
||| `PaginatedResult<PresenceMessage>` || A paginated list of [`PresenceMessage`]{@link} objects. |
| subscribe((PresenceMessage) ->) => io ||| RTP6a | Registers a listener that is called each time a [`PresenceMessage`]{@link} is received on the channel, such as a new member entering the presence set. |
| subscribe(PresenceAction, (PresenceMessage) ->) => io ||| RTP6b | Registers a listener that is called each time a [`PresenceMessage`]{@link} matching a given [`PresenceAction`]{@link} is received on the channel, such as a new member entering the presence set. |
|| `PresenceAction` || | A specific [`PresenceAction`]{@link} to register the listener for. |
| unsubscribe() ||| RTP7a, RTE5 | Deregisters all listeners currently receiving [`PresenceMessage`]{@link} for the channel. |
| unsubscribe((PresenceMessage) ->) ||| RTP7a | Deregisters a specific listener that is registered to receive [`PresenceMessage`]{@link} on the channel. |
| unsubscribe(PresenceAction, (PresenceMessage) ->) ||| RTP7b | Deregisters a specific listener that is registered to receive [`PresenceMessage`]{@link} on the channel for a given [`PresenceAction`]{@link}. |
|| `PresenceAction` || | A specific [`PresenceAction`]{@link} to deregister the listener for. |
| enter(Data?, extras?: JsonObject) => io ||| RTP8 | Enters the presence set for the channel, optionally passing a `data` payload. A [clientID]{@link} is required to be present on a channel. An optional callback may be provided to notify of the success or failure of the operation. |
|| `Data` || | The payload associated with the presence member. |
|| `extras` || | A JSON object of arbitrary key-value pairs that may contain metadata, and/or ancillary payloads. |
| update(Data?, extras?: JsonObject) => io ||| RTP9 | Updates the `data` payload for a presence member. If called before entering the presence set, this is treated as an `enter` event. An optional callback may be provided to notify of the success or failure of the operation. |
|| `Data` || | The payload to update for the presence member. |
|| `extras` || | A JSON object of arbitrary key-value pairs that may contain metadata, and/or ancillary payloads. |
| leave(Data?, extras?: JsonObject) => io ||| RTP10 | Leaves the presence set for the channel. A client must have previously entered the presence set before they can leave it. An optional callback may be provided to notify of the success or failure of the operation. |
|| `Data` || | The payload associated with the presence member. |
|| `extras` || | A JSON object of arbitrary key-value pairs that may contain metadata, and/or ancillary payloads. |
| enterClient(clientId: String, Data?, extras?: JsonObject) => io ||| RTP4, RTP14, RTP15 | Enters the presence set of the channel for a given `clientId`. Enables a single client to update presence on behalf of any number of clients using a single connection. The library must have been instantiated with an API key or a token bound to a wildcard `clientId`. An optional callback may be provided to notify of the success or failure of the operation. |
|| `clientId` || | The ID of the client to enter into the presence set. |
|| `Data` || | The payload associated with the presence member. |
|| `extras` || | A JSON object of arbitrary key-value pairs that may contain metadata, and/or ancillary payloads. |
| updateClient(clientId: String, Data?, extras?: JsonObject) => io ||| RTP15 | Updates the `data` payload for a presence member using a given `clientId`. Enables a single client to update presence on behalf of any number of clients using a single connection. The library must have been instantiated with an API key or a token bound to a wildcard `clientId`. An optional callback may be provided to notify of the success or failure of the operation. |
|| `clientId` || | The ID of the client to update in the presence set. |
|| `Data` || | The payload to update for the presence member. |
|| `extras` || | A JSON object of arbitrary key-value pairs that may contain metadata, and/or ancillary payloads. |
| leaveClient(clientId: String, Data?, extras?: JsonObject) => io ||| RTP15 | Leaves the presence set of the channel for a given `clientId`. Enables a single client to update presence on behalf of any number of clients using a single connection. The library must have been instantiated with an API key or a token bound to a wildcard `clientId`. An optional callback may be provided to notify of the success or failure of the operation. |
|| `clientId` || | The ID of the client to leave the presence set for. |
|| `Data` || | The payload associated with the presence member. |
|| `extras` || | A JSON object of arbitrary key-value pairs that may contain metadata, and/or ancillary payloads. |

## enum PresenceAction

`PresenceAction` describes the possible actions presence members can emit.

| Enum | Spec | Description |
|---|---|---|
| ABSENT | TP2 | A member is not present in the channel. |
| PRESENT | TP2 | When subscribing to presence events on a channel that already has members present, this event is emitted for every member already present on the channel before the subscribe listener was registered. |
| ENTER | TP2 | A new member has entered the channel. |
| LEAVE | TP2 | A member who was present has now left the channel. This may be a result of an explicit request to leave or implicitly when detaching from the channel. Alternatively, if a member's connection is abruptly disconnected and they do not resume their connection within a minute, Ably treats this as a leave event as the client is no longer present. |
| UPDATE | TP2 | An already present member has updated their member data. Being notified of member data updates can be very useful, for example, it can be used to update the status of a user when they are typing a message. |

## class ConnectionDetails

The `ConnectionDetails` object is optionally passed to the client library in the `CONNECTED` property of `ProtocolMessage#connectionDetails`. It informs the client about any constraints it should adhere to, and provides additional metadata about the connection. For example, if a request is made to publish a message that exceeds the `maxMessageSize`, the client library can reject the message immediately, without communicating with the Ably service.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| clientId: String? ||| RSA12a, CD2a | Contains the client ID assigned to the token. If `clientId` is `null` or omitted, then the client is prohibited from assuming a `clientId` in any operations, however if `clientId` is a wildcard string `*`, then the client is permitted to assume any `clientId`. Any other string value for `clientId` implies that the `clientId` is both enforced and assumed for all operations from this client. |
| connectionKey: String ||| RTN15e, CD2b | The connection secret key string that is used to resume a connection and its state. |
| connectionStateTtl: Duration ||| CD2f, RTN14e, DF1a | The duration that Ably will persist the connection state for when a Realtime client is abruptly disconnected. |
| maxFrameSize: Int default 524288 ||| CD2d | Overrides the default `maxFrameSize`. |
| maxInboundRate: Int ||| CD2e | The maximum allowable number of requests per second from a client or Ably. In the case of a realtime connection, this restriction applies to the number of [`ProtocolMessage`]{@link} objects sent, whereas in the case of REST, it is the total number of REST requests per second. |
| maxMessageSize: Int default 65536 ||| CD2c | Overrides the default `maxMessageSize`.|
| serverId: String ||| CD2g | A unique identifier for the front-end server that the client has connected to. This server ID is only used for the purposes of debugging. |
| maxIdleInterval: Duration ||| CD2h | The maximum length of time in milliseconds that the server will allow no activity to occur in the server to client direction. After such a period of inactivity, the server will send a `HEARTBEAT` or transport-level ping to the client. If the value is 0, the server will allow arbitrarily-long levels of inactivity. |

## class Message

The `Message` object represents an individual message that is sent to, or received from, Ably.

| Method / Property | Parameter| Returns | Spec | Description |
|---|---|---|---|---|
| constructor(name: String?, data: Data?) ||| TM2 | Construct a `Message` object with an event name and payload. |
|| `name` ||| Event name. |
|| `data` ||| The message payload. |
| constructor(name: String?, data: Data?, clientId: String?) ||| TM2 | Construct a `Message` object with an event name, payload, and a unique client ID. |
|| `name` ||| Event name. |
|| `data` ||| The message payload. |
|| `clientId` ||| The client ID of the publisher of this message. |
| +fromEncoded(JsonObject, ChannelOptions?) -> Message ||| TM3 | A static factory method to create a `Message` object from a deserialized Message-like object encoded using Ably's wire protocol. |
|| `JsonObject` ||| A `Message`-like deserialized object. |
|| `ChannelOptions` ||| A [`ChannelOptions`]{@link} object. If you have an encrypted channel, use this to allow the library to decrypt the data. |
||| `Message` || A `Message` object. |
| +fromEncodedArray(JsonArray, ChannelOptions?) -> [Message] ||| TM3 | A static factory method to create an array of `Message` objects from an array of deserialized Message-like object encoded using Ably's wire protocol. |
|| `JsonArray` ||| An array of `Message`-like deserialized objects. |
|| `ChannelOptions` ||| A [`ChannelOptions`]{@link} object. If you have an encrypted channel, use this to allow the library to decrypt the data. |
||| [`Message`] || An array of [`Message`]{@link} objects. |
| clientId: String? ||| RSL1g1, TM2b | The client ID of the publisher of this message. |
| connectionId: String? ||| TM2c | The connection ID of the publisher of this message. |
| data: Data? ||| TM2d | The message payload, if provided. |
| encoding: String? ||| TM2e | This is typically empty, as all messages received from Ably are automatically decoded client-side using this value. However, if the message encoding cannot be processed, this attribute contains the remaining transformations not applied to the `data` payload. |
| extras: JsonObject? ||| TM2i | A combination of metadata or ancillary payloads. The only valid payload for `extras` is the `push` object. |
| id: String ||| TM2a | A Unique ID assigned by Ably to this message. |
| name: String? ||| TM2g | The event name. |
| timestamp: Time ||| TM2f | Timestamp of when the message was received by Ably, as a Unix timestamp. |

## class PresenceMessage

A `PresenceMessage` object represents an individual presence update sent to, or received from Ably.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| +fromEncoded(JsonObject, ChannelOptions?) -> PresenceMessage ||| TP4 | Decodes and decrypts a deserialized `PresenceMessage`-like object using the cipher in [`ChannelOption`]{@link}. Any residual transforms that cannot be decoded or decrypted will be in the `encoding` property. Intended for users receiving messages from a source other than a REST or Realtime channel (for example a queue) to avoid having to parse the encoding string. |
|| `JsonObject` ||| The deserialized `PresenceMessage`-like object to decode and decrypt. |
|| `ChannelOptions` ||| A [`ChannelOptions`]{@link} object containing the cipher. |
| +fromEncodedArray(JsonArray, ChannelOptions?) -> [PresenceMessage] ||| TP4 | Decodes and decrypts an array of deserialized `PresenceMessage`-like object using the cipher in [`ChannelOption`]{@link}. Any residual transforms that cannot be decoded or decrypted will be in the `encoding` property. Intended for users receiving messages from a source other than a REST or Realtime channel (for example a queue) to avoid having to parse the encoding string. |
|| `JsonArray` ||| An array of deserialized `PresenceMessage`-like objects to decode and decrypt.|
|| `ChannelOptions` ||| A [`ChannelOptions`]{@link} object containing the cipher. |
| action: PresenceAction ||| TP3b | The type of [`PresenceAction`]{@link} the `PresenceMessage` is for. |
| clientId: String ||| TP3c | The ID of the client that published the `PresenceMessage`. |
| connectionId: String ||| TP3d | The ID of the connection associated with the client that published the `PresenceMessage`. |
| data: Data? ||| TP3e | The payload of the `PresenceMessage`. |
| encoding: String? ||| TP3f | This will typically be empty as all presence messages received from Ably are automatically decoded client-side using this value. However, if the message encoding cannot be processed, this attribute will contain the remaining transformations not applied to the data payload. |
| extras: JsonObject? ||| TP3i | A JSON object of arbitrary key-value pairs that may contain metadata, and/or ancillary payloads. |
| id: String ||| TP3a | A unique ID assigned to each `PresenceMessage` by Ably. |
| timestamp: Time ||| TP3g | The time the `PresenceMessage` was received by Ably, as a Unix timestamp. |
| memberKey() -> String ||| TP3h | Combines `clientId` and `connectionId` to ensure that multiple connected clients with an identical `clientId` are uniquely identifiable. A string function that returns the combined `clientId` and `connectionId`. |
||| `String` || A combination of `clientId` and `connectionId`. |

## class AuthDetails

The `AuthDetails` object contains the token string used to authenticate a client with Ably.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| accessToken: String ||| AD2 | The authentication token string. |

## class Connection

The `Connection` object enables the management of a connection with Ably.

|  Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| embeds `EventEmitter<ConnectionEvent, ConnectionStateChange>` ||| RTN4a, RTN4e, RTN4g | Embeds an [`EventEmitter`]{@link} object. |
| errorReason: ErrorInfo? ||| RTN14a | When a connection failure occurs this property contains the [`ErrorInfo`]{@link}. |
| id: String? ||| RTN8 | A unique public identifier for this connection, used to identify this member. |
| key: String? ||| RTN9 | A unique private connection key used to recover or resume a connection, assigned by Ably. When recovering a connection explicitly, the `recoveryKey` is used in the recover client options as it contains both the key and the last message serial. This private connection key can also be used by other REST clients to publish on behalf of this client. See the [publishing over REST on behalf of a realtime client docs](https://ably.com/docs/rest/channels#publish-on-behalf) for more info. |
| recoveryKey: String? ||| RTN16b, RTN16c | The recovery key string can be used by another client to recover this connection's state in the recover client options property. See [connection state recover options](https://ably.com/docs/realtime/connection#connection-state-recover-options) for more information. |
| serial: Int? ||| RTN10 | The serial number of the last message to be received on this connection, used automatically by the library when recovering or resuming a connection. When recovering a connection explicitly, the `recoveryKey` is used in the recover client options as it contains both the key and the last message serial. |
| state: ConnectionState ||| RTN4d | The current state of this connection. See [Connection states](https://ably.com/docs/realtime/connection#connection-states) for more information. |
| close() ||| RTN12 | Causes the connection to close, entering the closing state. Once closed, the library does not attempt to re-establish the connection without an explicit call to [`connect()`]{@link}. |
| connect() ||| RTC1b, RTN3, RTN11 | Explicitly calling [`connect()`]{@link} is unnecessary unless the `autoConnect` attribute of the [`ClientOptions`]{@link} object is false. Unless already connected or connecting, this method causes the connection to open, entering the connecting state. |
| ping() => io ||| RTN13 | When connected, sends a heartbeat ping to the Ably server and executes the callback with any error and the response time in milliseconds when a heartbeat ping request is echoed from the server. This can be useful for measuring true round-trip latency to the connected Ably server. |

## enum ConnectionState

The `ConnectionState` enum is a string with a value matching any of the realtime connection states.

| Enum | Spec | Description |
|---|---|---|
| INITIALIZED || A [`Connection`]{@link} object having this state has been initialized but no connection has yet been attempted. |
| CONNECTING || A connection attempt has been initiated. The connecting state is entered as soon as the library has completed initialization, and is reentered each time connection is re-attempted following disconnection. |
| CONNECTED || A connection exists and is active. |
| DISCONNECTED || A temporary failure condition. No current connection exists because there is no network connectivity or no host is available. The disconnected state is entered if an established connection is dropped, or if a connection attempt was unsuccessful. In the disconnected state the library will periodically attempt to open a new connection (approximately every 15 seconds), anticipating that the connection will be re-established soon and thus connection and channel continuity will be possible. In this state, developers can continue to publish messages as they are automatically placed in a local queue, to be sent as soon as a connection is reestablished. Messages published by other clients while this client is disconnected will be delivered to it upon reconnection, so long as the connection was resumed within 2 minutes. After 2 minutes have elapsed, recovery is no longer possible and the connection will move to the `suspended` state. |
| SUSPENDED || A long term failure condition. No current connection exists because there is no network connectivity or no host is available. The suspended state is entered after a failed connection attempt if there has then been no connection for a period of two minutes. In the suspended state, the library will periodically attempt to open a new connection every 30 seconds. Developers are unable to publish messages in this state. A new connection attempt can also be triggered by an explicit call to [`connect()`]{@link} on the [`Connection`]{@link} object. Once the connection has been re-established, channels will be automatically re-attached. The client has been disconnected for too long for them to resume from where they left off, so if it wants to catch up on messages published by other clients while it was disconnected, it needs to use the [History API](https://ably.com/docs/realtime/history). |
| CLOSING || An explicit request by the developer to close the connection has been sent to the Ably service. If a reply is not received from Ably within a short period of time, the connection is forcibly terminated and the connection state becomes `closed`. |
| CLOSED || The connection has been explicitly closed by the client. In the closed state, no reconnection attempts are made automatically by the library, and clients may not publish messages. No connection state is preserved by the service or by the library. A new connection attempt can be triggered by an explicit call to [`connect()`]{@link} on the [`Connection`]{@link} object, which results in a new connection. |
| FAILED || This state is entered if the client library encounters a failure condition that it cannot recover from. This may be a fatal connection error received from the Ably service, for example an attempt to connect with an incorrect API key, or a local terminal error, for example the token in use has expired and the library does not have any way to renew it. In the failed state, no reconnection attempts are made automatically by the library, and clients may not publish messages. A new connection attempt can be triggered by an explicit call to [`connect()`]{@link} on the [`Connection`]{@link} object. |

## enum ConnectionEvent

`ConnectionEvent` describes the events emitted by a [`Connection`]{@link} object. An event is either an `UPDATE` or a `ConnectionState`.

| Enum | Spec | Description |
|---|---|---|
| embeds ConnectionState || The event contains a [`ConnectionState`]{@link}. |
| UPDATE | RTN4h | An event for changes to connection conditions for which the [`ConnectionState`]{@link} does not change. |

## class ConnectionStateChange

A `ConnectionStateChange` object encapsulates [`ConnectionState`]{@link} change information emitted by the [`Connection`]{@link} object.

|  Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| current: ConnectionState ||| TA2 | The new [`ConnectionState`]{@link}. |
| event: ConnectionEvent ||| TA5 | The event that triggered this [`ConnectionState`]{@link} change. |
| previous: ConnectionState ||| TA2 | The previous [`ConnectionState`]{@link}. For the `update` event, this is equal to the current [`ConnectionState`]{@link}. |
| reason: ErrorInfo? ||| RTN4f, TA3 | An [`ErrorInfo`]{@link} object containing any information relating to the transition. |
| retryIn: Duration? ||| RTN14d, TA2 | Duration in milliseconds, after which the client retries a connection where applicable. |

## class Stats

||| Spec | Description |
|---|---|---|---|
| intervalId: String || TS12a | |
| intervalTime: Time || TS12b (calculated clientside) | |
| unit: Stats.IntervalGranularity || TS12c | |
| intervalGranularity: Stats.IntervalGranularity? || TS12d (deprecated) | |
| all: Stats.MessageTypes || TS12e | |
| inbound: Stats.MessageTraffic || TS12f | |
| outbound: Stats.MessageTraffic || TS12g | |
| persisted: Stats.MessageTypes || TS12h | |
| connections: Stats.ConnectionTypes || TS12i | |
| channels: Stats.ResourceCount || TS12j | |
| apiRequests: Stats.RequestCount || TS12k | |
| tokenRequests: Stats.RequestCount || TS12l | |
| push: Stats.PushStats || TS12m | |
| xchgProducer: Stats.XchgMessages || TS12n | |
| xchgConsumer: Stats.XchgMessages || TS12o | |

## enum StatsIntervalGranularity

`StatsIntervalGranularity` describes the interval unit over which statistics are gathered.

| Enum | Spec | Description |
|---|---|---|
| MINUTE || Interval unit over which statistics are gathered as minutes. |
| HOUR || Interval unit over which statistics are gathered as hours. |
| DAY || Interval unit over which statistics are gathered as days. |
| MONTH || Interval unit over which statistics are gathered as months. |

## class DeviceDetails

The `DeviceDetails` object contains the properties of a device registered for push notifications.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| id: String |||| A unique ID generated by the device. |
| clientId: String? |||| The client ID the device is connected to Ably with. |
| formFactor: DeviceFormFactor |||| The [`DeviceFormFactor`]{@link} object associated with the device. Describes the type of the device, such as `phone` or `tablet`. |
| metadata: JsonObject |||| A JSON object of `key:value` pairs that contains metadata for the device. |
| platform: DevicePlatform |||| The [`DevicePlatform`]{@link} associated with the device. Describes the platform the device uses, such as `android` or `ios`. |
| push: DevicePushDetails |||| The [`DevicePushDetails`]{@link} object associated with the device. Describes the details of the push registration of the device. |

## class DevicePushDetails

The `DevicePushDetails` object contains the details of the push registration of a device.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| errorReason: ErrorInfo? |||| Any error information associated with the device push registration as an [`ErrorInfo`]{@link} object. |
| recipient: JsonObject |||| A JSON object of `key:value` pairs that contains of the push transport and address. |
| state: .Active \| .Failing \| .Failed |||| The current state of the push registration. |

## class LocalDevice (extends DeviceDetails)

The `LocalDevice` object extends [`DeviceDetails`]{@link} and contains the device identity token and secret.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| deviceIdentityToken: String |||| A unique device identity token used to communicate with APNS or FCM. |
| deviceSecret: String |||| A unique device secret generated by the Ably SDK. |

## class Push

The `Push` object enables registering and deregistering a device for push notifications.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| admin: PushAdmin ||| RSH1 | The [`PushAdmin`]{@link} object associated with the device. |
| activate(registerCallback: ((ErrorInfo?, DeviceDetails?) -> io String)?, updateFailedCallback: ((ErrorInfo) ->)) => io ErrorInfo? ||| RSH2a | Activates the device for push notifications with FCM or APNS, obtaining a unique identifier from them. Subsequently registers the device with Ably and stores the `deviceIdentityToken` in local storage. |
||| `ErrorInfo` || Describes why the activation was unsuccessful as an [`ErrorInfo`]{@link} object. |
| deactivate(deregisterCallback: ((ErrorInfo?, deviceId: String?) -> io)?) => io ErrorInfo? ||| RSH2b | Deactivates the device from receiving push notifications with Ably and FCM or APNS. |
||| `ErrorInfo` || Describes why the deactivation was unsuccessful as an [`ErrorInfo`]{@link} object. |

## class PushAdmin

The `PushAdmin` object enables the management of device registrations and push notification subscriptions, as well as enabling publishing of push notifications to devices.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| publish(recipient: JsonObject, data: JsonObject) => io ||| RSH1a | Sends a push notification directly to a device, or a group of devices sharing the same `clientId`. |
|| `recipient` ||| A JSON object containing the recipient details using `clientId`, `deviceId` or the underlying notifications service. |
|| `data` ||| A JSON object containing the push notification payload. |
| deviceRegistrations: PushDeviceRegistrations ||| RSH1b | A [`PushDeviceRegistrations`]{@link} object that provides functionality for registering, updating and listing push devices. |
| channelSubscriptions: PushChannelSubscriptions ||| RSH1c | A [`PushChannelSubscriptions`]{@link} object that provides functionality for subscribing, listing and unsubscribing devices from push notifications published to channels. |

## class JsonObject

The `JsonObject` object denotes any type or interface in the target language that represents an RFC4627 object or array value respectively. Such types serialize to, and may be deserialized from, the corresponding JSON text. This object is platform-dependent, typically a Dict-like object.

## class PushDeviceRegistrations

The `PushDeviceRegistrations` object is used to manage push notification registrations with Ably.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| get(DeviceDetails) => io DeviceDetails ||| RSH1b1 | Retrieves the [`DeviceDetails`]{@link} of a device registered to receive push notifications using the `id` property of a [`DeviceDetails`]{@link} object. |
|| `DeviceDetails` ||| The [`DeviceDetails`]{@link} object containing the `id` property of the device. |
||| `DeviceDetails` || A [`DeviceDetails`]{@link} object. |
| get(deviceId: String) => io DeviceDetails ||| RSH1b1 | Retrieves the [`DeviceDetails`]{@link} of a device registered to receive push notifications using its `deviceId`. |
|| `deviceId` ||| The unique ID of the device. |
||| `DeviceDetails` || A [`DeviceDetails`]{@link} object. |
| list(params: `Dict<String, String>`) => io `PaginatedResult<DeviceDetails>` ||| RSH1b2 | Retrieves all devices matching the filter `params` provided. Returns a [`DeviceDetails`]{@link} object for each matched device. |
|| `params` ||| An object containing key-value pairs to filter devices by. Can contain `clientId`, `deviceId` and a `limit` on the number of devices returned, up to 1,000. |
||| `PaginatedResult<DeviceDetails>` || A paginated list of [`DeviceDetails`]{@link} objects. |
| save(DeviceDetails) => io DeviceDetails ||| RSH1b3 | Registers or updates a [`DeviceDetails`]{@link} object with Ably. Returns the new, or updated [`DeviceDetails`]{@link} object. |
|| `DeviceDetails` ||| The [`DeviceDetails`]{@link} object to create or update. |
||| `DeviceDetails` || A [`DeviceDetails`]{@link} object. |
| remove(DeviceDetails) => io ||| RSH1b4 | Removes a device registered to receive push notifications from Ably using the `id` property of a [`DeviceDetails`]{@link} object. |
|| `DeviceDetails` ||| The [`DeviceDetails`]{@link} object containing the `id` property of the device. |
| remove(deviceId: String) => io ||| RSH1b4 | Removes a device registered to receive push notifications from Ably using its `deviceId`. |
|| `deviceId` ||| The unique ID of the device. |
| removeWhere(params: `Dict<String, String>`) => io ||| RSH1b5 | Removes all devices registered to receive push notifications from Ably matching the filter `params` provided. |
|| `params` ||| An object containing key-value pairs to filter devices by. Can contain `clientId` and `deviceId`. |

## class PushChannelSubscriptions

The `PushChannelSubscriptions` object is used to manage device push channel subscriptions.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| list(params: `Dict<String, String>`) => io `PaginatedResult<PushChannelSubscription>` ||| RSH1c1 | Retrieves all push channel subscriptions matching the filter `params` provided. Returns a [`PushChannelSubscription`]{@link} object for each matched subscriptions. |
|| `params` ||| An object containing key-value pairs to filter subscriptions by. Can contain `channel`, `clientId`, `deviceId` and a `limit` on the number of devices returned, up to 1,000. |
||| `PaginatedResult<PushChannelSubscription>` || A paginated list of [`PushChannelSubscription`]{@link} objects. |
| listChannels(params: `Dict<String, String>`?) => io `PaginatedResult<String>` ||| RSH1c2 | Retrieves all channels with at least one device subscribed to push notifications.  |
|| `params` ||| An object containing key-value pairs to filter channels by. Can contain a `limit` on the number of channels returned, up to 1,000. |
||| `PaginatedResult<String>` || A paginated list of channel names. |
| save(PushChannelSubscription) => io PushChannelSubscription ||| RSH1c3 | Subscribes a device, or a group of devices sharing the same `clientId` to push notifications on a channel. Returns a [`PushChannelSubscription`]{@link} object. |
|| `PushChannelSubscription` ||| A [`PushChannelSubscription`]{@link} object. |
||| `PushChannelSubscription` || A [`PushChannelSubscription`]{@link} object describing the new or updated subscriptions. |
| remove(PushChannelSubscription) => io ||| RSH1c4 | Unsubscribes a device, or a group of devices sharing the same `clientId` from receiving push notifications on a channel. |
|| `PushChannelSubscription` ||| A [`PushChannelSubscription`]{@link} object. |
| removeWhere(params: `Dict<String, String>`) => io ||| RSH1c5 | Unsubscribes all devices from receiving push notifications on a channel that match the filter `params` provided. |
|| `params` ||| An object containing key-value pairs to filter subscriptions by. Can contain `channel`, and optionally either `clientId` or `deviceId`. |

## enum DevicePlatform

`DevicePlatform` describes the device receiving push notifications.

| Enum | Spec | Description |
|---|---|---|
| "android" | PCD6 | The device platform is Android. |
| "ios" | PCD6 | The device platform is iOS. |
| "browser" | PCD6 | The device platform is a web browser. |

## enum DeviceFormFactor

`DeviceFormFactor` is the type of device receiving a push notification.

| Enum | Spec | Description |
|---|---|---|
| "phone" | PCD4 | The device is a phone. |
| "tablet" | PCD4 | The device is tablet. |
| "desktop" | PCD4 | The device is a desktop. |
| "tv" | PCD4 | The device is a TV. |
| "watch" | PCD4 | The device is a watch. |
| "car" | PCD4 | The device is a car. |
| "embedded" | PCD4 | The device is embedded. |
| "other" | PCD4 | The device is other. |

## class PushChannelSubscription

The `PushChannelSubscription` object contains the subscriptions a device, or a group of devices sharing the same `clientId`, has to a channel to receive push notifications.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| +forDevice(channel: String, deviceId: String) => PushChannelSubscription |||| |
|| `channel` ||| |
|| `deviceId` ||| |
||| `PushChannelSubscription` || |
| +forClientId(channel: String, clientId: String) => PushChannelSubscription |||| |
|| `channel` ||| |
|| `deviceId` ||| |
||| `PushChannelSubscription` || |
| deviceId: String? ||| PCS2, PCS5, PCS6 | The unique ID of the device. |
| clientId: String? ||| PCS3, PCS6 | The ID of the client the device, or devices are associated to. |
| channel: String ||| PCS4 | The channel the push notification subscription is for. |

## class ErrorInfo

The `ErrorInfo` object is a generic Ably error object that contains an Ably-specific status code, and a generic status code. Errors returned from the Ably server are compatible with the `ErrorInfo` structure and should result in errors that inherit from `ErrorInfo`.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| code: Int ||| TI1 | Ably [error code](https://github.com/ably/ably-common/blob/main/protocol/errors.json). |
| href: String? ||| TI4 | This is included for REST responses to provide a URL for additional help on the error code. |
| message: String ||| TI1 | Additional message information, where available. |
| cause: ErrorInfo? ||| TI1 | Information pertaining to what caused the error where available. |
| statusCode: Int ||| TI1 | HTTP Status Code corresponding to this error, where applicable. |
| requestId: String? ||| RSC7c | If a request fails, the request ID must be included in the `ErrorInfo` returned to the user. |

## class `EventEmitter<Event, Data>`

The `EventEmitter` object is a generic interface for event registration and delivery used in a number of the types in the Realtime client library. For example, the [`Connection`]{@link} object emits events for connection state using the EventEmitter pattern.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| on((Data...) ->) ||| RTE4 | Registers the provided listener all events. If `on` is called more than once with the same listener and event, the listener is added multiple times to its listener registry. Therefore, as an example, assuming the same listener is registered twice using `on`, and an event is emitted once, the listener would be invoked twice. |
|| `Data` ||| The event listener. |
| on(Event, (Data...) ->) ||| RTE4 | Registers the provided listener for the specified event. If `on` is called more than once with the same listener and event, the listener is added multiple times to its listener registry. Therefore, as an example, assuming the same listener is registered twice using `on`, and an event is emitted once, the listener would be invoked twice. |
|| `Event` ||| The named event to listen for. |
|| `Data` ||| The event listener. |
| once((Data...) ->) ||| RTE4 | Registers the provided listener for the first event that is emitted. If `once` is called more than once with the same listener, the listener is added multiple times to its listener registry. Therefore, as an example, assuming the same listener is registered twice using `once`, and an event is emitted once, the listener would be invoked twice. However, all subsequent events emitted would not invoke the listener as `once` ensures that each registration is only invoked once. |
|| `Data` ||| The event listener. |
| once(Event, (Data...) ->) ||| RTE4 | Registers the provided listener for the first occurrence of a single named event specified as the `Event` argument. If `once` is called more than once with the same listener, the listener is added multiple times to its listener registry. Therefore, as an example, assuming the same listener is registered twice using `once`, and an event is emitted once, the listener would be invoked twice. However, all subsequent events emitted would not invoke the listener as `once` ensures that each registration is only invoked once. |
|| `Event` ||| The named event to listen for. |
|| `Data` ||| The event listener. |
| off() ||| RTE5 | Deregisters all registrations, for all events and listeners. |
| off((Data...) ->) ||| RTE5 | Deregisters the specified listener. Removes all registrations matching the given listener, regardless of whether they are associated with an event or not. |
|| `Data` ||| The event listener. |
| off(Event, (Data...) ->) ||| RTE5 | Removes all registrations that match both the specified listener and the specified event. |
|| `Event` ||| The named event. |
|| `Data` ||| The event listener. |
| emit(Event, Data...) ||| RTE6 | Emits an event, calling registered listeners with the given event name and any other given arguments. If an exception is raised in any of the listeners, the exception is caught by the `EventEmitter` and the exception is logged to the Ably logger. |
|| `Event` ||| The named event. |
|| `Data` ||| The event listener. |

## class `PaginatedResult<T>`

The `PaginatedResult<T>` object represents a page of results for all message and presence history, stats, and REST presence requests. The response from a REST API paginated query is accompanied by metadata that indicates the relative queries available to the `PaginatedResult` object.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| items: [T] ||| TG3 | Contains the current page of results; for example, an array of `Message` or `PresenceMessage` objects for a channel history request. |
| first() => io `PaginatedResult<T>` ||| TG5 | Returns a new `PaginatedResult` for the first page of results. |
||| `PaginatedResult<T>` || A page of results for message and presence history, stats, and REST presence requests. |
| hasNext() -> Bool ||| TG6 | Returns `true` if there are more pages available by calling next and returns `false` if this page is the last page available. |
||| `Bool` || Whether or not there are more pages of results. |
| isLast() -> Bool ||| TG7 | Returns `true` if this page is the last page and returns `false` if there are more pages available by calling next available. |
||| `Bool` || Whether or not this is the last page of results. |
| next() => io `PaginatedResult<T>`? ||| TG4 | Returns a new `PaginatedResult` loaded with the next page of results. If there are no further pages, then `null` is returned. |
||| `PaginatedResult<T>` || A page of results for message and presence history, stats, and REST presence requests. |

## class HttpPaginatedResponse

The `HttpPaginatedResponse` object is a superset of `PaginatedResult`, which represents a page of results plus metadata indicating the relative queries available to it. `HttpPaginatedResponse` additionally carries information about the response to an HTTP request. It is used when making [custom HTTP requests](https://ably.com/docs/api/rest-sdk#request).

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| embeds `PaginatedResult<JsonObject>` |||| `HttpPaginatedResponse` embeds [`PaginatedResult`]{@link}. |
| items: [JsonObject] ||| HP3 | Contains a page of results; for example, an array of `Message` or `PresenceMessage` objects for a channel history request. |
| statusCode: Int ||| HP4 | The HTTP status code of the response. |
| success: Bool ||| HP5 | Whether `statusCode` indicates success. This is equivalent to `200 <= statusCode < 300`. |
| errorCode: Int ||| HP6 | The error code if the `X-Ably-Errorcode` HTTP header is sent in the response. |
| errorMessage: String ||| HP7 | The error message if the `X-Ably-Errormessage` HTTP header is sent in the response. |
| headers: `Dict<String, String>` ||| HP8 | The headers of the response. |

## enum PluginType

`PluginType` describes the type of plugin used.

| Enum | Spec | Description |
|---|---|---|
| "vcdiff" || A plugin capable of decoding `vcdiff`-encoded messages. It must implement the [`VCDiffDecoder`]{@link} interface. |

## class VCDiffDecoder

The `VCDiffDecode` object is capable of decoding `vcdiff` encoded messages. See [delta compression](https://ably.com/docs/realtime/channels/channel-parameters/deltas) for more information.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| decode([byte] delta, [byte] base) -> [byte]  ||| PC3 | Decodes `vcdiff` encoded messages. |
|| `delta` || PC3a | The delta encoded data. |
|| `base` || PC3a | The stored base payload of the last message on a channel. |
||| `[byte]` | PC3a | The decoded data. |

## class DeltaExtras

The `DeltaExtras` object is JSON-encodable and used to contain any arbitrary key-value pairs, which may also contain other primitive JSON types, JSON-encodable objects, or JSON-encodable arrays. 

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| from: String |||| The ID of the message the delta was generated from. |
| format: String |||| The delta compression format. Only `vcdiff` is supported. |
