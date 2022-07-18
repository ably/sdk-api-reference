# Classes and types

## class Rest

The `Rest` object offers a simple stateless API to interact directly with Ably's REST API.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| constructor(keyOrTokenStr: String) ||| RSC1 | Constructs a REST client object using an Ably API key or token string. |
|| `keyOrTokenStr` ||| The Ably API key or token string used to validate the client. |
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
| stats(start: Time api-default epoch(), end: Time api-default now(), direction: .Backwards \| Forwards api-default .Backwards, limit: int api-default 100, unit: .Minute \| .Hour \| .Day \| .Month api-default .Minute => io `PaginatedResult<Stats>` ||| RSC6a | Queries the [REST `/stats` API](https://ably.com/docs/rest-api#stats) and retrieves your application's usage statistics. A [`PaginatedResult`]{@link} object is returned, containing an array of stats for the first page of results. `PaginatedResult` objects are iterable providing a means to page through historical statistics. See the [Stats docs](https://ably.com/docs/general/statistics). |
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
| constructor(keyOrTokenStr: String) ||| RSC1 | Constructs a realtime client object using an Ably API key or token string. |
|| `keyOrTokenStr` ||| The Ably API key or token string used to validate the client. |
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
| stats: ||| Same as Rest.stats, RTC5a | Queries the [REST `/stats` API](https://ably.com/docs/rest-api#stats) and retrieves your application's usage statistics. A [`PaginatedResult`]{@link} object is returned, containing an array of stats for the first page of results. `PaginatedResult` objects are iterable providing a means to page through historical statistics. See the [Stats docs](https://ably.com/docs/general/statistics). |
| close() ||| proxy for RTN12 | Calls `connection.close()` and causes the connection to close, entering the closing state. Once closed, the library will not attempt to re-establish the connection without an explicit call to `connect()`. |
| connect() ||| proxy for RTN11 | Calls `connection.connect()` and causes the connection to open, entering the connecting state. Explicitly calling `connect()` is unnecessary unless the `autoConnect` property of the [`ClientOptions`]{@link} object is disabled. |
| time() => io Time ||| RTC6a | Retrieves the time from the Ably service as a Unix timestamp in milliseconds. Clients that do not have access to a sufficiently well maintained time source and wish to issue Ably `TokenRequest`s with a more accurate timestamp should use the [`queryTime`]{@link} property of the [`ClientOption`]{@link} object instead of this method. |
||| `Time` || The time as a Unix timestamp. |

## class ClientOptions

||| Spec | Description |
|---|---|---|---|
| embeds AuthOptions || TO3j | |
| autoConnect: Bool default true || RTC1b, TO3e | |
| clientId: String? || RSC17, RSA4, RSA15, TO3a | |
| defaultTokenParams: TokenParams? || TO3j11 | |
| echoMessages: Bool default true || RTC1a, TO3h | |
| environment: String? || RSC15b, TO3k1 | |
| logHandler: || platform specific - TO3c | |
| logLevel: || platform specific - TO3b | |
| logExceptionReportingUrl: String default "[library specific]" || TO3m (deprecated) | |
| port: Int default 80 || TO3k4 | |
| queueMessages: Bool default true || RTP16b, TO3g | |
| restHost: String default "rest.ably.io" || RSC12, TO3k2 | |
| realtimeHost: String default "realtime.ably.io" || RTC1d, TO3k3 | |
| fallbackHosts: String[] default nil || RSC15b, RSC15a, TO3k6 | |
| fallbackHostsUseDefault: Bool default false || TO3k7 (deprecated) | |
| recover: String? || RTC1c, TO3i | |
| tls: Bool default true || RSC18, TO3d | |
| tlsPort: Int default 443 || TO3k5 | |
| useBinaryProtocol: Bool default true || TO3f | |
| transportParams: [String: Stringifiable]? || RTC1f | |
| addRequestIds: Bool default false || TO3p | |
| disconnectedRetryTimeout: Duration default 15s || TO3l1 | |
| suspendedRetryTimeout: Duration default 30s || RTN14d, TO3l2 | |
| channelRetryTimeout: Duration default 15s || RTL13b, TO3l7 | |
| httpOpenTimeout: Duration default 4s || TO3l3 | |
| httpRequestTimeout: Duration default 10s || TO3l4 | |
| realtimeRequestTimeout: Duration default 10s || TO3l11 | |
| httpMaxRetryCount: Int default 3 || TO3l5 | |
| httpMaxRetryDuration: Duration default 15s || TO3l6 | |
| maxMessageSize: Int default 65536 || TO3l8 | |
| maxFrameSize: Int default 524288 || TO3l8 | |
| fallbackRetryTimeout: Duration default 600s || TO3l10 | |
| plugins: `Dict<PluginType, Plugin>` || TO3o | |
| idempotentRestPublishing: bool default true || RSL1k1, RTL6a1, TO3n | |
| agents: [String: String?]? || RSC7d6 - interface only offered by some libraries | |

## class AuthOptions

||| Spec | Description |
|---|---|---|---|
| authCallback: ((TokenParams) -> io (String \| TokenDetails \| TokenRequest \| JsonObject))? || RSA4a, RSA4, TO3j5, AO2b | |
| authHeaders: [String: Stringifiable]? || RSA8c3, TO3j8, AO2e | |
| authMethod: .GET \| .POST default .GET || RSA8c, TO3j7, AO2d | |
| authParams: [String: Stringifiable]? || RSA8c3, RSA8c1, TO3j9, AO2f | |
| authUrl: String? || RSA4a, RSA4, RSA8c, TO3j6, AO2c | |
| key: String? || RSA11, RSA14, TO3j1, AO2a | |
| queryTime: Bool default false || RSA9d, TO3j10, AO2a | |
| token: String? \| TokenDetails? \| TokenRequest? || RSA4a, RSA4, TO3j2 | |
| tokenDetails: TokenDetails? || RSA4a, RSA4, TO3j3 | |
| useTokenAuth: Bool? || RSA4, RSA14, TO3j4 | |

## class TokenParams

||| Spec | Description |
|---|---|---|---|
| capability: String api-default `'{"*":["*"]}'` || RSA9f, TK2b | |
| clientId: String? || TK2c | |
| nonce: String? || RSA9c, Tk2d | |
| timestamp: Time? || RSA9d, Tk2d | |
| ttl: Duration api-default 60min || RSA9e, TK2a | |

## class Auth

||| Spec | Description |
|---|---|---|---|
| clientId: String? || RSA7, RSC17, RSA12 | |
| authorize(TokenParams?, AuthOptions?) => io TokenDetails || RSA10 | |
| createTokenRequest(TokenParams?, AuthOptions?) => io TokenRequest || RSA9 | |
| requestToken(TokenParams?, AuthOptions?) => io TokenDetails || RSA8e | |
| tokenDetails: TokenDetails? || RSA16 | |

## class TokenDetails

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| +fromJson(String \| JsonObject) -> TokenDetails ||| TD7 |Creates a `TokenDetails` object from a String or JsonObject.|
|||`TokenDetails`||A [`TokenDetails`]{@link} object containing details of a new or exisiting token.|
||`String`|||Should be parased as a JSON string.|
||`JsonObject`|||Object of JSON strings.|
| capability: String? ||| TD5 |Capability associated with the token, JSON stringified.|
| clientId: String? ||| TD6 |Contains the `clientId` assigned to the token. If null or omitted, the token is prohibited from assuming a client ID in any operations, however if `clientId` is a wildcard string '*', then the token is permitted to assume any client ID. Any other string value for `clientId` implies that the client ID is both enforced and assumed for all operations for this token|
| expires: Time? ||| TD3 |Contains the expiry time in milliseconds. Where idiomatic in the language, this can be a Date/Time object.|
| issued: Time? ||| TD4 |Contains the time the token was issued in milliseconds. Where idiomatic in the language, this can be a Date/Time object.|
| token: String ||| TD2 |Contains the token string.|

## class TokenRequest

||| Spec | Description |
|---|---|---|---|
| +fromJson(String \| JsonObject) -> TokenRequest || TE6 | |
| capability: String || TE3 | |
| clientId: String? || TE2 | |
| keyName: String || TE2 | |
| mac: String || TE2 | |
| nonce: String || TE2 | |
| timestamp: Time? || TE5 | |
| ttl: Duration? api-default 60min || TE4 | |

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

## class MessageFilterObject

The `MessageFilterObject` handles the attaching and removing of a listener which only executes when a message matches a set of criteria.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| hasRef: bool ||| RTL22b | Checks whether the message has a `extras.ref`.|
| refId: string ||| RTL22a | Checks that the message matches one or more of: `extras.ref.timeserial`, `extras.ref.type` or `name`. |
| refType: string ||| RTL22a | Checks if a message’s `extras.ref.type` matches the supplied value.|
| name: string ||| RTL22a | Check if a message’s `name` matches the supplied value |

## class ChannelProperties

||| Spec | Description |
|---|---|---|---|
| attachSerial: String || CP2a | |

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

## class MessageFilter

 The `MessageFilter` object supplies filter options to subscribe to a message.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
|isRef: bool|||MFI2a| Checks if a message contains the specified `extra.ref`.|
|refTimeserial: string|||MFI2b| Checks if a message contains the specified `extras.ref.timeserial`.|
|refType: string|||MFI2c| Checks if a message contains the specified `extras.ref.type`. |
|name: string|||MFI2d|Checks if a message contains the specified `name`.|
 
## class ReferenceExtras

The `ReferenceExtras` object supplies fields to be referenced by the `MessageFilter` object.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
|timeserial: string|||REX2a| Provides a `timeserial` field that can be referenced by `MessageFilter`.|
|type: string|||REX2b|Provides a `type` field that can be referenced by `MessageFilter`, should be written in reverse domain name notation. `com.ably.` values are reserved|

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

The `ChannelOptions` object is used to configure a channel when creating a channel object.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|----|
| +withCipherKey(key: Binary \| String)? -> ChannelOptions ||| TB3 | Constructor `withCipherKey`, that takes a key only. |
|| `key` ||| A private key used to encrypt and decrypt payloads. |
||| `ChannelOptions` || A [`ChannelOptions`]{@link} object. |
| cipher: (CipherParams \| CipherParamOptions)? ||| RSL5a, TB2b | Requests encryption for this channel when not null, and specifies encryption-related parameters (such as algorithm, chaining mode, key length and key). See [an example](https://ably.com/docs/realtime/encryption#getting-started). |
| params?: `Dict<String, String>` ||| TB2c | [Channel Parameters](https://ably.com/docs/realtime/channels/channel-parameters/overview) that configure the behavior of the channel. |
| modes?: [ChannelMode] ||| TB2d | For realtime client libraries only. An array of [`ChannelMode`]{@link} objects. |

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

## class CipherParamOptions 

`CipherParamOptions` is used creating a @CipherParams@ instance, may be implemented as a hashmap or a class depending on language.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| algorithm?: String ||| CO2a | The algorithm used for encryption; currently the only supported non-null value is AES. |
| key: Binary \| String ||| CO2b | The private key used to encrypt and decrypt payloads. |
| keyLength?: Int ||| CO2c | The length in bits of the @key@; for example 128 or 256. |
| mode?: String ||| CO2d | The cipher mode; currently only supports the non-null value @CBC@. |

## class Crypto

The `Crypto` object ensures that message payloads are encrypted, can never be decrypted by Ably, and can only be decrypted by other clients that share the same secret symmetric key.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| +getDefaultParams(Params) -> CipherParams ||| RSE1 | Retrieves, or optionally sets, the [`CipherParams`]{@link} for the channel. |
|| `CipherParamOptions` ||| Overrides the default parameters. A suitable `key` must be provided as a minimum. |
||| `CipherParams` || A [`CipherParams`]{@link} object, using the default values for any field not supplied. |
| +generateRandomKey(keyLength: Int?) => io Binary ||| RSE2 | Generates a random key to be used in the encryption of the channel. |
|| `keyLength` ||| The length of the key, in bits, to be generated. If not specified, this is equal to the default `keyLength` of the default algorithm: for AES this is 256 bits. |
||| `Binary` || The key as a binary, for example, a byte array. If the language cryptographic randomness primitives are blocking or async, a callback is used. The callback returns the generated binary key. |


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

Internal only.

||| Spec | Description |
|---|---|---|---|
| clientId: String? || RSA12a, CD2a | |
| connectionKey: String || RTN15e, CD2b | |
| connectionStateTtl: Duration || CD2f, RTN14e, DF1a | |
| maxFrameSize: Int || CD2d | |
| maxInboundRate: Int || CD2e | |
| maxMessageSize: Int || CD2c | |
| serverId: String || CD2g | |
| maxIdleInterval: Duration || CD2h | |

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

||| Spec | Description |
|---|---|---|---|
| accessToken: String || AD2 | |

## class Connection

||| Spec | Description |
|---|---|---|---|
| embeds `EventEmitter<ConnectionEvent, ConnectionStateChange>` || RTN4a, RTN4e, RTN4g | |
| errorReason: ErrorInfo? || RTN14a | |
| id: String? || RTN8 | |
| key: String? || RTN9 | |
| recoveryKey: String? || RTN16b, RTN16c | |
| serial: Int? || RTN10 | |
| state: ConnectionState || RTN4d | |
| close() || RTN12 | |
| connect() || RTC1b, RTN3, RTN11 | |
| ping() => io Duration || RTN13 | |

## enum ConnectionState

||| Spec | Description |
|---|---|---|---|
| INITIALIZED || |
| CONNECTING || |
| CONNECTED || |
| DISCONNECTED || |
| SUSPENDED || |
| CLOSING || |
| CLOSED || |
| FAILED || |

## enum ConnectionEvent

||| Spec | Description |
|---|---|---|---|
| embeds ConnectionState || |
| UPDATE || RTN4h | |

## class ConnectionStateChange

||| Spec | Description |
|---|---|---|---|
| current: ConnectionState || TA2 | |
| event: ConnectionEvent || TA5 | |
| previous: ConnectionState || TA2 | |
| reason: ErrorInfo? || RTN4f, TA3 | |
| retryIn: Duration? || RTN14d, TA2 | |

## class Stats

||| Spec | Description |
|---|---|---|---|
| intervalId: String || TS12a | |
| intervalTime: Time || TS12b (calculated client-side) | |
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

The `DeltaExtras` object is JSON-encodable and used to contain any arbitrary key-value pairs, which may also contain other primitive JSON types, JSON-encodable objects, or JSON-encodable arrays. 

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| from: String |||| The ID of the message the delta was generated from. |
| format: String |||| The delta compression format. Only `vcdiff` is supported. |

## class InteractionExtras

| timeserial: String || | |
| type: String || | |
