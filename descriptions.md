# Classes and types

## class Rest

||| Spec | Description |
|---|---|---|---|
| constructor(keyStr: String) || RSC1 | |
| constructor(tokenStr: String) || RSC1 | |
| constructor(ClientOptions) || RSC1 | |
| auth: Auth || RSC5 | |
| push: Push || |
| batch: BatchOperations || BO1 | |
| device() => io LocalDevice || |
| channels: `Channels<RestChannel>` || RSN1 | |
| request() => io HttpPaginatedResponse || RSC19 | |
|| String method, || |
|| String path, || |
|| `Dict<String, String>` params?, || |
|| JsonObject \| JsonArray body?, || |
|| `Dict<String, String>` headers || |
| stats() => io `PaginatedResult<Stats>` | RSC6a | |
|| start: Time api-default epoch(), | RSC6b1 | |
|| end: Time api-default now(), | RSC6b1 | |
|| direction: .Backwards \| .Forwards api-default .Backwards | RSC6b2 | |
|| limit: int api-default 100, | RSC6b3 | |
|| unit: .Minute \| .Hour \| .Day \| .Month api-default .Minute | RSC6b4 | |
| time() => io Time || RSC16 | |

## class Realtime

||| Spec | Description |
|---|---|---|---|
| constructor(keyStr: String) || RSC1 | |
| constructor(tokenStr: String) || RSC1 | |
| constructor(ClientOptions) || RSC1 | |
| auth: Auth || RTC4 | |
| push: Push || |
| device() => io LocalDevice || |
| channels: `Channels<RealtimeChannel>` || RTC3, RTS1 | |
| clientId: String? || proxy for RSA7 | |
| connection: Connection || RTC2 | |
| request() => io HttpPaginatedResponse || RTC9 | |
|| String method || |
|| String path || |
|| `Dict<String, String>` params? || |
|| JsonObject \| JsonArray body? || |
|| `Dict<String, String>` headers? || |
| stats: || Same as Rest.stats, RTC5a || |
| close() || proxy for RTN12 || |
| connect() || proxy for RTN11 || |
| time() => io Time || RTC6a || |

## class ClientOptions

The `ClientOptions` object is a plain JavaScript object and is used in the `Ably.Realtime` constructor’s options argument. `ClientOptions` extends `AuthOptions`.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| embeds AuthOptions ||| TO3j | An [`AuthOptions`]{@link} object. |
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
| transportParams: [String: Stringifiable]? ||| RTC1f | Can be used to pass in arbitrary connection parameters. |
| addRequestIds: Bool default false ||| TO3p | If enabled, every REST request to Ably should include a random string in a `request_id` query string parameter. The random string is a url-safe base64-encoding sequence of at least 9 bytes, obtained from a source of randomness. This request ID must remain the same if a request is retried to a fallback host. Any log messages associated with the request should include the request ID. If the request fails, the request ID must be included in the [`ErrorInfo`]{@link} returned to the user. |
| disconnectedRetryTimeout: Duration default 15s ||| TO3l1 |  If the connection is still in the `DISCONNECTED` state after this delay in milliseconds, the client library will attempt to reconnect automatically.|
| suspendedRetryTimeout: Duration default 30s ||| RTN14d, TO3l2 | When the connection enters the `SUSPENDED` state, after this delay in milliseconds, if the state is still `SUSPENDED`, the client library attempts to reconnect automatically. |
| channelRetryTimeout: Duration default 15s ||| RTL13b, TO3l7 | When a channel becomes `SUSPENDED` following a server initiated `DETACHED`, after this delay in milliseconds, if the channel is still `SUSPENDED` and the connection is `CONNECTED`, the client library will attempt to re-attach the channel automatically |
| httpOpenTimeout: Duration default 4s ||| TO3l3 | Timeout for opening the connection, available in the client library if supported by the transport. |
| httpRequestTimeout: Duration default 10s ||| TO3l4 | Timeout for any single HTTP request and response. |
| httpMaxRetryCount: Int default 3 ||| TO3l5 | The maximum number of fallback hosts to use as a fallback when an HTTP request to the primary host is unreachable or indicates that it is unserviceable. |
| httpMaxRetryDuration: Duration default 15s ||| TO3l6 | The maximum elapsed time in which fallback host retries for HTTP requests will be attempted. |
| maxMessageSize: Int default 65536 ||| TO3l8 | The maximum size of messages that can be published in one go. That is, the size of the `ProtocolMessage.messages` or `ProtocolMessage.presence` array for a realtime publish or presence action, or the message or array of messages being published for a REST publish. For realtime publishes, the default will be overridden by the `maxMessageSize` in the [`connectionDetails`]{@link}. |
| maxFrameSize: Int default 524288 ||| TO3l8 | The maximum size of a single POST body or WebSocket frame. This is mostly only relevant for `RestClient#request` (for batch publishes), since publishes will hit the `maxMessageSize` limit before this. |
| plugins: `Dict<PluginType, Plugin>` ||| TO3o | A map between a `PluginType` and a `Plugin` object. The client library might downcast a `Plugin` to particular plugin type. |
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
| queryTime: Bool default false ||| RSA9d, TO3j10, AO2a | If `true`, the library queries the Ably servers for the current time when issuing `TokenRequest`s instead of relying on a locally-available time of day. Knowing the time accurately is needed to create valid signed Ably [TokenRequests](https://ably.com/docs/realtime/authentication#token-authentication), so this option is useful for library instances on auth servers where for some reason the server clock cannot be kept synchronized through normal means, such as an [NTP daemon](https://en.wikipedia.org/wiki/Ntpd). The server is queried for the current time once per client library instance (which stores the offset from the local clock), so if using this option you should avoid instancing a new version of the library for each request. |
| token: String? \| TokenDetails? \| TokenRequest? ||| RSA4a, RSA4, TO3j2 | An authenticated token. This can either be a `TokenDetails` object, a `TokenRequest` object, or token string (obtained from the `token` property of a `TokenDetails` component of an Ably `TokenRequest` response, or a JSON Web Token satisfying [the Ably requirements for JWTs](https://ably.com/docs/core-features/authentication#ably-jwt)). This option is mostly useful for testing: since tokens are short-lived, in production you almost always want to use an authentication method that enables the client library to renew the token automatically when the previous one expires, such as `authUrl` or `authCallback`. Read more about [Token authentication](https://ably.com/docs/core-features/authentication#token-authentication).|
| tokenDetails: TokenDetails? ||| RSA4a, RSA4, TO3j3 | An authenticated `TokenDetails` object (most commonly obtained from an Ably Token Request response). This option is mostly useful for testing: since tokens are short-lived, in production you almost always want to use an authentication method that enables the client library to renew the token automatically when the previous one expires, such as `authUrl` or `authCallback`. Use this option if you wish to use Token authentication. Read more about [Token authentication](https://ably.com/docs/core-features/authentication#token-authentication). |
| useTokenAuth: Bool? ||| RSA4, RSA14, TO3j4 | When `true`, forces Token authentication to be used by the library. Please note that if a `clientId` is not specified in the `ClientOptions` or `TokenParams`, then the Ably Token issued is [anonymous](https://ably.com/docs/core-features/authentication#identified-clients). |

## class TokenParams

The `TokenParams` object is a plain JavaScript object and is used in the parameters of token authentication requests, corresponding to the desired attributes of the Ably Token.

|  Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| capability: String api-default `'{"*":["*"]}'` ||| RSA9f, TK2b | Capability requirements JSON stringified for the token. When omitted, Ably defaults to the capabilities of the underlying key. See the [capabilities docs](https://ably.com/docs/core-features/authentication#capabilities-explained) for more information. |
| clientId: String? ||| TK2c | A client ID, used for identifying this client when publishing messages or for presence purposes. The `clientId` can be any non-empty string. This option is primarily intended to be used in situations where the library is instantiated with a key. Note that a `clientId` may also be implicit in a token used to instantiate the library. An error is raised if a `clientId` specified here conflicts with the `clientId` implicit in the token. Find out more about [identified clients](https://ably.com/docs/core-features/authentication#identified-clients). |
| nonce: String? ||| RSA9c, Tk2d | An unquoted, un-escaped random string of at least 16 characters, used to ensure the [`TokenRequest`]{@link} cannot be reused. |
| timestamp: Time? ||| RSA9d, Tk2d | The Unix timestamp of this request. Timestamps, in conjunction with the `nonce`, are used to prevent requests from being replayed. `timestamp` is a "one-time" value, and is valid in a request, but is not validly a member of any default token params such as `ClientOptions.defaultTokenParams`. |
| ttl: Duration api-default 60min ||| RSA9e, TK2a | Requested time to live for the token in milliseconds. When omitted, Ably will default to a TTL of 60 minutes. |

## class Auth

The `Auth` object creates Ably `TokenRequest` objects with `createTokenRequest` or obtain Ably Tokens from Ably with `requestToken`, and then issue them to less trusted clients.

|  Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| clientId: String? ||| RSA7, RSC17, RSA12 | A client ID, used for identifying this client when publishing messages or for presence purposes. The `clientId` can be any non-empty string. This option is primarily intended to be used in situations where the library is instantiated with a key. Note that a `clientId` may also be implicit in a token used to instantiate the library. An error is raised if a `clientId` specified here conflicts with the `clientId` implicit in the token. Find out more about [identified clients](https://ably.com/docs/core-features/authentication#identified-clients). |
| authorize(TokenParams?, AuthOptions?) => io TokenDetails ||| RSA10 | Instructs the library to get a new token immediately. When using the realtime client, it upgrades the current realtime connection to use the new token, or if not connected, initiates a connection to Ably, once the new token has been obtained. Also stores any `tokenParams` and `authOptions` passed in as the new defaults, to be used for all subsequent implicit or explicit token requests. Any `tokenParams` and `authOptions` objects passed in entirely replace (as opposed to being merged with) the currently client library saved `tokenParams` and `authOptions`. |
||| `TokenDetails` ||  An ably authentication token. |
| createTokenRequest(TokenParams?, AuthOptions?) => io TokenRequest ||| RSA9 | Creates and signs an Ably `TokenRequest` based on the specified (or if none specified, the client library stored) `tokenParams` and `authOptions`. Note this can only be used when the API `key` value is available locally. Otherwise, the Ably `TokenRequest` must be obtained from the key owner. Use this to generate an Ably `TokenRequest` in order to implement an Ably Token request callback for use by other clients. Both `authOptions` and `tokenParams` are optional. When omitted or `null`, the default token parameters and authentication options for the client library are used, as specified in the `ClientOptions` when the client library was instantiated, or later updated with an explicit `authorize` request. Values passed in are used instead of (rather than being merged with) the default values. To understand why an Ably `TokenRequest` may be issued to clients in favor of a token, see [Token Authentication explained](https://ably.com/docs/core-features/authentication/#token-authentication). |
||| `TokenRequest` || An Ably token request object. |
| requestToken(TokenParams?, AuthOptions?) => io TokenDetails ||| RSA8e | Calls the [requestToken REST API endpoint](https://ably.com/docs/rest-api#request-token) to obtain an Ably Token according to the specified tokenParams and authOptions. Both `authOptions` and `tokenParams` are optional. When omitted or `null`, the default token parameters and authentication options for the client library are used, as specified in the `ClientOptions` when the client library was instantiated, or later updated with an explicit `authorize` request. Values passed in are used instead of (rather than being merged with) the default values. To understand why an Ably `TokenRequest` may be issued to clients in favor of a token, see [Token Authentication explained](https://ably.com/docs/core-features/authentication/#token-authentication). |
||| `TokenDetails` || An Ably authentication token. |


## class TokenDetails

The `TokenDetails` object represents an Ably token string and its associated metadata.

|  Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| +fromJson(String \| JsonObject) -> TokenDetails ||| TD7 | A static factory method to create a `TokenDetails` object from a deserialized TokenDetails-like object or a JSON stringified `TokenDetails` object. This method is provided to minimize bugs as a result of differing types by platform for fields such as `timestamp` or `ttl`. For example, in Ruby `ttl` in the `TokenDetails` object is exposed in seconds as that is idiomatic for the language, yet when serialized to JSON using `to_json` it is automatically converted to the Ably standard which is milliseconds. By using the `fromJson` method when constructing a `TokenDetails` object, Ably ensures that all fields are consistently serialized and deserialized across platforms. |
||| `TokenDetails` || An Ably authentication token. |
| capability: String ||| TD5 | The capability associated with this Ably Token. The capability is a a JSON stringified canonicalized representation of the resource paths and associated operations. Read more about capbilities in the [capabilities docs](https://ably.com/docs/core-features/authentication/#capabilities-explained). |
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
| keyName: String ||| TE2 | The key name of the key against which this request is made. The key name is public, whereas the key secret is private. |
| mac: String ||| TE2 | The Message Authentication Code for this request. |
| nonce: String ||| TE2 | An opaque nonce string of at least 16 characters. |
| timestamp: Time? ||| TE5 | The Unix timestamp of this request in milliseconds. |
| ttl: Duration? api-default 60min ||| TE4 | Requested time to live for the Ably Token in milliseconds. If the Ably `TokenRequest` is successful, the TTL of the returned Ably Token is less than or equal to this value, depending on application settings and the attributes of the issuing key. |

## class `Channels<ChannelType>`

||| Spec | Description |
|---|---|---|---|
| exists(String) -> Bool || RSN2, RTS2 | |
| get(String) -> ChannelType || RSN3a, RTS3a | |
| get(String, ChannelOptions) -> ChannelType || RSN3c, RTS3c | |
| iterate() -> `Iterator<ChannelType>` || RSN2, RTS2 | |
| release(String) || RSN4, RTS4 | |

## class RestChannel

||| Spec | Description |
|---|---|---|---|
| name: String? ||| |
| presence: RestPresence || RSL3 | |
| history() => io `PaginatedResult<Message>` || RSL2a | |
|| start: Time, | RSL2b1 | |
|| end: Time api-default now(), | RSL2b1 | |
|| direction: .Backwards \| .Forwards api-default .Backwards, | RSL2b2 | |
|| limit: int api-default 100 | RSL2b3 | |
| status() => ChannelDetails || RSL8 | |
| publish() => io || RSL1 | |
|| Message || |
|| params?: `Dict<String, Stringifiable>` || |
| publish() => io || RSL1 | |
|| [Message] || |
|| params?: `Dict<String, Stringifiable>` || |
| publish() => io || RSL1 | |
|| name: String? || |
|| data: Data? || |
| setOptions() => io || RSL7 | |
|| options: ChannelOptions || |
| push: PushChannel || RSH4 | |

## class RealtimeChannel

||| Spec | Description |
|---|---|---|---|
| embeds `EventEmitter<ChannelEvent, ChannelStateChange?>` || RTL2a, RTL2d, RTL2e | |
| errorReason: ErrorInfo? || RTL4e | |
| state: ChannelState || RTL2b | |
| presence: RealtimePresence || RTL9 | |
| properties: ChannelProperties || CP1, RTL15 | |
| push: PushChannel || |
| modes: readonly [ChannelMode] || RTL4m | |
| params: readonly `Dict<String, String>` || RTL4k1 | |
| attach() => io || RTL4d | |
| detach() => io || RTL5e | |
| history() => io `PaginatedResult<Message>` || RSL2a | |
|| start: Time, | RTL10a | |
|| end: Time api-default now(), | RTL10a | |
|| direction: .Backwards \| .Forwards api-default .Backwards, | RTL10a | |
|| limit: int api-default 100, | RTL10a | |
|| untilAttach: Bool default false | RTL10b | |
| publish(Message) => io || RTL6i | |
| publish([Message]) => io || RTL6i | |
| publish(name: String?, data: Data?) => io || RTL6i | |
| subscribe((Message) ->) => io || RTL7a | |
| subscribe(String, (Message) ->) => io || RTL7b | |
| unsubscribe() || RTL8a, RTE5 | |
| unsubscribe((Message) ->) || RTL8a | |
| unsubscribe(String, (Message) ->) || RTL8a | |
| setOptions(options: ChannelOptions) => io || RTL16 | |

## class BatchOperations

||| Spec | Description |
|---|---|---|---|
| publish([BatchSpec]) => `BatchResult<BatchPublishResponse>` || BO2a | |
| publish(BatchSpec) => `BatchResult<BatchPublishResponse>` || BO2a | |
| getPresence([String]) => `BatchResult<BatchPresenceResponse>` || BO2b | |

## class `BatchResult<T>`

||| Spec | Description |
|---|---|---|---|
| error: ErrorInfo? || BPA2b | |
| responses: []T? || BPA2a | |

## class BatchPublishResponse

||| Spec | Description |
|---|---|---|---|
| channel: String || BPB2a | |
| messageId: String? || BPB2b | |
| error: ErrorInfo? || BPB2c | |

## class BatchPresenceResponse

||| Spec | Description |
|---|---|---|---|
| channel: String || BPD2a | |
| presence: []BatchPresence || PBD2b | |

## class BatchPresence

||| Spec | Description |
|---|---|---|---|
| clientId: string || |
| action: string? || |
| error: ErrorInfo? || |

## class PushChannel

||| Spec | Description |
|---|---|---|---|
| subscribeDevice() => io || RSH7a | |
| subscribeClient() => io || RSH7b | |
| unsubscribeDevice() => io || RSH7c | |
| unsubscribeClient() => io || RSH7d | |
| listSubscriptions() => io `PaginatedResult<PushChannelSubscription>` || RSH7e | |

## class BatchSpec

||| Spec | Description |
|---|---|---|---|
| channels: [String] || |
| messages: [Message] || |

## enum ChannelState

||| Spec | Description |
|---|---|---|---|
| INITIALIZED || |
| ATTACHING || |
| ATTACHED || |
| DETACHING || |
| DETACHED || |
| SUSPENDED || |
| FAILED || |

## enum ChannelEvent

||| Spec | Description |
|---|---|---|---|
| embeds ChannelState || |
| UPDATE || RTL2g | |

## enum ChannelMode

||| Spec | Description |
|---|---|---|---|
| PRESENCE || |
| PUBLISH || |
| SUBSCRIBE || |
| PRESENCE_SUBSCRIBE || |

## class ChannelStateChange

||| Spec | Description |
|---|---|---|---|
| current: ChannelState || RTL2a, RTL2b | |
| event: ChannelEvent || TH5 | |
| previous: ChannelState || RTL2a, RTL2b | |
| reason: ErrorInfo? || RTL2e, TH3 | |
| resumed: Boolean || RTL2f, TH4 | |

## class ChannelOptions

||| Spec | Description |
|---|---|---|---|
| +withCipherKey(key: Binary \| String)? -> ChannelOptions || TB3 | |
| cipher: (CipherParams \| Params)? || RSL5a, TB2b | |
| params?: `Dict<String, String>` || TB2c | |
| modes?: [ChannelMode] || TB2d | |

## class ChannelDetails

||| Spec | Description |
|---|---|---|---|
| channelId: String || CHD2a | |
| name: String || CHD2b | |
| status: ChannelStatus || CHD2c | |

## class ChannelStatus

||| Spec | Description |
|---|---|---|---|
| isActive: Boolean || CHS2a | |
| occupancy: ChannelOccupancy || CHS2b | |

## class ChannelOccupancy

||| Spec | Description |
|---|---|---|---|
| metrics: ChannelMetrics || CHO2a | |

## class ChannelMetrics

||| Spec | Description |
|---|---|---|---|
| connections: Int || CHM2a | |
| presenceConnections: Int || CHM2b | |
| presenceMembers: Int || CHM2c | |
| presenceSubscribers: Int || CHM2d | |
| publishers: Int || CHM2e | |
| subscribers: Int || CHM2f | |

## class CipherParams

||| Spec | Description |
|---|---|---|---|
| algorithm: String default "AES" || TZ2a | |
| key: Binary || TZ2d | |
| keyLength: Int || TZ2b | |
| mode: String default "CBC" || TZ2c | |

## class Crypto

||| Spec | Description |
|---|---|---|---|
| +getDefaultParams(Params) -> CipherParams || RSE1 | |
| +generateRandomKey(keyLength: Int?) => io Binary || RSE2 | |

## class RestPresence

||| Spec | Description |
|---|---|---|---|
| get() => io `PaginatedResult<PresenceMessage>` || RSPa | |
|| limit: int api-default 100, | RSP3a | |
|| clientId: String?, | RSP3a2 | |
|| connectionId: String?, | RSP3a3 | |
| history() => io `PaginatedResult<PresenceMessage>` || RSP4a | |
|| start: Time, | RSP4b1 | |
|| end: Time api-default now(), | RSP4b1 | |
|| direction: .Backwards \| .Forwards api-default .Backwards, | RSP4b2 | |
|| limit: int api-default 100, | RSP4b3 | |

## class RealtimePresence

||| Spec | Description |
|---|---|---|---|
| syncComplete: Bool || RTP13 | |
| get() => io [PresenceMessage] || RTP11 | |
|| waitForSync: Bool default true, | RTP11c1
|| clientId: String?, | RTP11c2 | |
|| connectionId: String?, | RTP11c3 | |
| history() => io `PaginatedResult<PresenceMessage>` || RTP12c | |
|| start: Time, | RTP12a | |
|| end: Time, | RTP12a | |
|| direction: .Backwards \| .Forwards api-default .Backwards, | RTP12a | |
|| limit: int api-default 100, | RTP12a | |
| subscribe((PresenceMessage) ->) => io || RTP6a | |
| subscribe(PresenceAction, (PresenceMessage) ->) => io || RTP6b | |
| unsubscribe() || RTP7a, RTE5 | |
| unsubscribe((PresenceMessage) ->) || RTP7a | |
| unsubscribe(PresenceAction, (PresenceMessage) ->) || RTP7b | |
| enter(Data?, extras?: JsonObject) => io || RTP8 | |
| update(Data?, extras?: JsonObject) => io || RTP9 | |
| leave(Data?, extras?: JsonObject) => io || RTP10 | |
| enterClient(clientId: String, Data?, extras?: JsonObject) => io || RTP4, RTP14, RTP15 | |
| updateClient(clientId: String, Data?, extras?: JsonObject) => io || RTP15 | |
| leaveClient(clientId: String, Data?, extras?: JsonObject) => io || RTP15 | |

## enum PresenceAction

||| Spec | Description |
|---|---|---|---|
| ABSENT || TP2 | |
| PRESENT || TP2 | |
| ENTER || TP2 | |
| LEAVE || TP2 | |
| UPDATE || TP2 | |

## class ConnectionDetails

The `ConnectionDetails` object is optionally passed to the client library in the `CONNECTED` of `ProtocolMessage#connectionDetails`. It informs the client about any constraints it should adhere to, and provides additional metadata about the connection. For example, if a request is made to publish a message that exceeds the `maxMessageSize`, the client library can reject the message immediately, without communicating with the Ably service.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| clientId: String? ||| RSA12a, CD2a | Contains the client ID assigned to the token. If `clientId` is `null` or omitted, then the client is prohibited from assuming a `clientId` in any operations, however if `clientId` is a wildcard string `*`, then the client is permitted to assume any `clientId`. Any other string value for `clientId` implies that the `clientId` is both enforced and assumed for all operations from this client. |
| connectionKey: String ||| RTN15e, CD2b | The connection secret key string that is used to resume a connection and its state. |
| connectionStateTtl: Duration ||| CD2f, RTN14e, DF1a | The duration that Ably will persist the connection state when a Realtime client is abruptly disconnected. |
| maxFrameSize: Int ||| CD2d | Overrides the default `maxFrameSize`. |
| maxInboundRate: Int ||| CD2e | The maximum allowable number of requests per second from a client or Ably. In the case of a realtime connection, this restriction applies to the number of [`ProtocolMessage`]{@link} objects sent, whereas in the case of REST, it is the total number of REST requests per second. |
| maxMessageSize: Int ||| CD2c | Overrides the default `maxMessageSize`.|
| serverId: String ||| CD2g | A unique identifier for the front-end server that the client has connected to. This server ID is only used for the purposes of debugging. |
| maxIdleInterval: Duration ||| CD2h | The maximum length of time in milliseconds that the server will allow no activity to occur in the server to client direction. After such a period of inactivity, the server will send a `HEARTBEAT` or transport-level ping to the client. If the value is 0, the server will allow arbitrarily-long levels of inactivity. |

## class Message

||| Spec | Description |
|---|---|---|---|
| constructor(name: String?, data: Data?) || TM2 | |
| constructor(name: String?, data: Data?, clientId: String?) || TM2 | |
| +fromEncoded(JsonObject, ChannelOptions?) -> Message || TM3 | |
| +fromEncodedArray(JsonArray, ChannelOptions?) -> [Message] || TM3 | |
| clientId: String? || RSL1g1, TM2b | |
| connectionId: String? || TM2c | |
| data: Data? || TM2d | |
| encoding: String? || TM2e | |
| extras: JsonObject? || TM2i | |
| id: String || TM2a | |
| name: String? || TM2g | |
| timestamp: Time || TM2f | |

## class PresenceMessage

||| Spec | Description |
|---|---|---|---|
| +fromEncoded(JsonObject, ChannelOptions?) -> PresenceMessage || TP4 | |
| +fromEncodedArray(JsonArray, ChannelOptions?) -> [PresenceMessage] || TP4 | |
| action: PresenceAction || TP3b | |
| clientId: String || TP3c | |
| connectionId: String || TP3d | |
| data: Data? || TP3e | |
| encoding: String? || TP3f | |
| extras: JsonObject? || TP3i | |
| id: String || TP3a | |
| timestamp: Time || TP3g | |
| memberKey() -> String || TP3h | |

## class AuthDetails

The `AuthDetails` object contains the token string used to authenticate a client with Ably.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| accessToken: String ||| AD2 | The authentication token string. |

## class Connection

The `Connection` object enables the management of a connection with Ably.

|  Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| embeds `EventEmitter<ConnectionEvent, ConnectionStateChange>` ||| RTN4a, RTN4e, RTN4g | An [`EventEmitter`]{@link} object. |
| errorReason: ErrorInfo? ||| RTN14a | When a connection failure occurs this property contains the [`ErrorInfo`]{@link}. |
| id: String? ||| RTN8 | A unique public identifier String for this connection, used to identify this member in presence events and messages. |
| key: String? ||| RTN9 | A unique private connection key String used to recover or resume a connection, assigned by Ably. When recovering a connection explicitly, the `recoveryKey` is used in the recover client options as it contains both the key and the last message serial. This private connection key can also be used by other REST clients to publish on behalf of this client. See the [publishing over REST on behalf of a realtime client docs](https://ably.com/docs/rest/channels#publish-on-behalf) for more info. |
| recoveryKey: String? ||| RTN16b, RTN16c | The recovery key string can be used by another client to recover this connection's state in the recover client options property. See [connection state recover options](https://ably.com/docs/realtime/connection#connection-state-recover-options) for more information. |
| serial: Int? ||| RTN10 | The serial number of the last message to be received on this connection, used automatically by the library when recovering or resuming a connection. When recovering a connection explicitly, the `recoveryKey` is used in the recover client options as it contains both the key and the last message serial. |
| state: ConnectionState ||| RTN4d | The current state of this connection. See [Connection states](https://ably.com/docs/realtime/connection#connection-states) for more information. |
| close() ||| RTN12 | Causes the connection to close, entering the closing state. Once closed, the library does not attempt to re-establish the connection without an explicit call to `connect`. |
| connect() ||| RTC1b, RTN3, RTN11 | Explicitly calling `connect()` is unnecessary unless the `autoConnect` attribute of the [`ClientOptions`]{@link} object is false. Unless already connected or connecting, this method causes the connection to open, entering the connecting state. |
| ping() => io ||| RTN13 | When connected, sends a heartbeat ping to the Ably server and executes the callback with any error and the response time in milliseconds when a heartbeat ping request is echoed from the server. This can be useful for measuring true round-trip latency to the connected Ably server. |

## enum ConnectionState

The `ConnectionState` enum is a string with a value matching any of the realtime connection states.

|  Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| INITIALIZED ||| A [`Connection`]{@link} object having this state has been initialized but no connection has yet been attempted. |
| CONNECTING ||| A connection attempt has been initiated. The connecting state is entered as soon as the library has completed initialization, and is reentered each time connection is re-attempted following disconnection. |
| CONNECTED ||| A connection exists and is active. |
| DISCONNECTED ||| A temporary failure condition. No current connection exists because there is no network connectivity or no host is available. The disconnected state is entered if an established connection is dropped, or if a connection attempt was unsuccessful. In the disconnected state the library will periodically attempt to open a new connection (approximately every 15 seconds), anticipating that the connection will be re-established soon and thus connection and channel continuity will be possible. In this state, developers can continue to publish messages as they are automatically placed in a local queue, to be sent as soon as a connection is reestablished. Messages published by other clients while this client is disconnected will be delivered to it upon reconnection, so long as the connection was resumed within 2 minutes. After 2 minutes have elapsed, recovery is no longer possible and the connection will move to the `suspended` state. |
| SUSPENDED ||| A long term failure condition. No current connection exists because there is no network connectivity or no host is available. The suspended state is entered after a failed connection attempt if there has then been no connection for a period of two minutes. In the suspended state, the library will periodically attempt to open a new connection every 30 seconds. Developers are unable to publish messages in this state. A new connection attempt can also be triggered by an explicit call to `connect()` on the `Connection` object. Once the connection has been re-established, channels will be automatically re-attached. The client has been disconnected for too long for them to resume from where they left off, so if it wants to catch up on messages published by other clients while it was disconnected, it needs to use the [History API](https://ably.com/docs/realtime/history). |
| CLOSING ||| An explicit request by the developer to close the connection has been sent to the Ably service. If a reply is not received from Ably within a short period of time, the connection is forcibly terminated and the connection state becomes `closed`. |
| CLOSED ||| The connection has been explicitly closed by the client. In the closed state, no reconnection attempts are made automatically by the library, and clients may not publish messages. No connection state is preserved by the service or by the library. A new connection attempt can be triggered by an explicit call to `connect()` on the [`Connection`]{@link} object, which results in a new connection. |
| FAILED ||| This state is entered if the client library encounters a failure condition that it cannot recover from. This may be a fatal connection error received from the Ably service, for example an attempt to connect with an incorrect API key, or a local terminal error, for example the token in use has expired and the library does not have any way to renew it. In the failed state, no reconnection attempts are made automatically by the library, and clients may not publish messages. A new connection attempt can be triggered by an explicit call to `connect()` on the [`Connection`]{@link} object. |

## enum ConnectionEvent

||| Spec | Description |
|---|---|---|---|
| embeds ConnectionState || |
| UPDATE || RTN4h | |

## class ConnectionStateChange

A `ConnectionStateChange` object encapsulates state change information emitted by the [`Connection`]{@link} object.

|  Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| current: ConnectionState ||| TA2 | The new state. |
| event: ConnectionEvent ||| TA5 | The event that triggered this state change. |
| previous: ConnectionState ||| TA2 | The previous state. For the `update` event, this is equal to the current state. |
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

||| Spec | Description |
|---|---|---|---|
| MINUTE || |
| HOUR || |
| DAY || |
| MONTH || |

## class DeviceDetails

||| Spec | Description |
|---|---|---|---|
| id: String || |
| clientId: String? || |
| formFactor: DeviceFormFactor || |
| metadata: JsonObject || |
| platform: DevicePlatform || |
| push: DevicePushDetails || |

## class DevicePushDetails

||| Spec | Description |
|---|---|---|---|
| errorReason: ErrorInfo? || |
| recipient: JsonObject || |
| state: .Active \| .Failing \| .Failed || |

## class LocalDevice (extends DeviceDetails)

||| Spec | Description |
|---|---|---|---|
| deviceIdentityToken: String || |
| deviceSecret: String || |

## class Push

||| Spec | Description |
|---|---|---|---|
| admin: PushAdmin || RSH1 | |
| activate() => io ErrorInfo? || RSH2a | |
|| registerCallback: ((ErrorInfo?, DeviceDetails?) -> io String)?, || |
|| updateFailedCallback: ((ErrorInfo) ->) || |
| deactivate() => io ErrorInfo? || RSH2b | |
|| deregisterCallback: ((ErrorInfo?, deviceId: String?) -> io)? || |

## class PushAdmin

||| Spec | Description |
|---|---|---|---|
| publish(recipient: JsonObject, data: JsonObject) => io || RSH1a | |
| deviceRegistrations: PushDeviceRegistrations || RSH1b | |
| channelSubscriptions: PushChannelSubscriptions || RSH1c | |

## class JsonObject

||| Spec | Description |
|---|---|---|---|
|||| |

## class PushDeviceRegistrations

||| Spec | Description |
|---|---|---|---|
| get(DeviceDetails) => io DeviceDetails || RSH1b1 | |
| get(deviceId: String) => io DeviceDetails || RSH1b1 | |
| list(params: `Dict<String, String>`) => io `PaginatedResult<DeviceDetails>` || RSH1b2 | |
| save(DeviceDetails) => io DeviceDetails || RSH1b3 | |
| remove(DeviceDetails) => io || RSH1b4 | |
| remove(deviceId: String) => io || RSH1b4 | |
| removeWhere(params: `Dict<String, String>`) => io || RSH1b5 | |

## class PushChannelSubscriptions

||| Spec | Description |
|---|---|---|---|
| list(params: `Dict<String, String>`) => io `PaginatedResult<PushChannelSubscription>` || RSH1c1 | |
| listChannels(params: `Dict<String, String>`?) => io `PaginatedResult<String>` || RSH1c2 | |
| save(PushChannelSubscription) => io PushChannelSubscription || RSH1c3 | |
| remove(PushChannelSubscription) => io || RSH1c4 | |
| removeWhere(params: `Dict<String, String>`) => io || RSH1c5 | |

## enum DevicePushTransportType

||| Spec | Description |
|---|---|---|---|
| "fcm" || PTT1 | |
| "gcm" || PTT1 | |
| "apns" || PTT1 | |
| "web" || PTT1 | |

## enum DevicePlatform

||| Spec | Description |
|---|---|---|---|
| "android" || PPT1 | |
| "ios" || PPT1 | |
| "browser" || PPT1 | |

## enum DeviceFormFactor

||| Spec | Description |
|---|---|---|---|
| "phone" || PDT1 | |
| "tablet" || PDT1 | |
| "desktop" || PDT1 | |
| "tv" || PDT1 | |
| "watch" || PDT1 | |
| "car" || PDT1 | |
| "embedded" || PDT1 | |
| "other" || PDT1 | |

## class PushChannelSubscription

||| Spec | Description |
|---|---|---|---|
| +forDevice(channel: String, deviceId: String) => PushChannelSubscription || |
| +forClientId(channel: String, clientId: String) => PushChannelSubscription || |
| deviceId: String? || PCS2, PCS5, PCS6 | |
| clientId: String? || PCS3, PCS6 | |
| channel: String || PCS4 | |

## class ErrorInfo

||| Spec | Description |
|---|---|---|---|
| code: Int || TI1 | |
| href: String? || TI4 | |
| message: String || TI1 | |
| cause: ErrorInfo? || TI1 | |
| statusCode: Int || TI1 | |
| requestId: String? || RSC7c | |

## class `EventEmitter<Event, Data>`

||| Spec | Description |
|---|---|---|---|
| on((Data...) ->) || RTE4 | |
| on(Event, (Data...) ->) || RTE4 | |
| once((Data...) ->) || RTE4 | |
| once(Event, (Data...) ->) || RTE4 | |
| off() || RTE5 | |
| off((Data...) ->) || RTE5 | |
| off(Event, (Data...) ->) || RTE5 | |
| emit(Event, Data...) || RTE6 | |

## class `PaginatedResult<T>`

||| Spec | Description |
|---|---|---|---|
| items: [T] || TG3 | |
| first() => io `PaginatedResult<T>` || TG5 | |
| hasNext() -> Bool || TG6 | |
| isLast() -> Bool || TG7 | |
| next() => io `PaginatedResult<T>`? || TG4 | |

## class HttpPaginatedResponse

||| Spec | Description |
|---|---|---|---|
| embeds `PaginatedResult<JsonObject>` || |
| items: [JsonObject] || HP3 | |
| statusCode: Int || HP4 | |
| success: Bool || HP5 | |
| errorCode: Int || HP6 | |
| errorMessage: String || HP7 | |
| headers: `Dict<String, String>` || HP8 | |

## enum PluginType

||| Spec | Description |
|---|---|---|---|
| "vcdiff" || |

## class VCDiffDecoder

||| Spec | Description |
|---|---|---|---|
| decode([byte] delta, [byte] base) -> [byte]  || |

## class DeltaExtras

||| Spec | Description |
|---|---|---|---|
| from: String ||| |
| format: String ||| |