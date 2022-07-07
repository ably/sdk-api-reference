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
| logExceptionReportingUrl: String default "[library specific]" || TO3c (deprecated) | |
| port: Int default 80 || TO3k4 | |
| queueMessages: Bool default true || RTP16b, TO3g | |
| restHost: String default "rest.ably.io" || RSC12, TO3k2 | |
| realtimeHost: String default "realtime.ably.io" || RTC1d, TO3k3 | |
| fallbackHosts: String[] default nil || RSC15b, RSC15a, TO3k6 | |
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
| httpMaxRetryCount: Int default 3 || TO3l5 | |
| httpMaxRetryDuration: Duration default 15s || TO3l6 | |
| maxMessageSize: Int default 65536 || TO3l8 | |
| maxFrameSize: Int default 524288 || TO3l8 | |
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

## class TokenDetails

||| Spec | Description |
|---|---|---|---|
| +fromJson(String \| JsonObject) -> TokenDetails || TD7 | |
| capability: String || TD5 | |
| clientId: String? || TD6 | |
| expires: Time || TD3 | |
| issued: Time || TD4 | |
| token: String || TD2 | |

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
| unsubscribe() ||| RTP7a, RTE5 | Unregisters all listeners currently receiving [`PresenceMessage`]{@link} for the channel. |
| unsubscribe((PresenceMessage) ->) ||| RTP7a | Unregisters a specific listener that is registered to receive [`PresenceMessage`]{@link} on the channel. |
| unsubscribe(PresenceAction, (PresenceMessage) ->) ||| RTP7b | Unregisters a specific listener that is registered to receive [`PresenceMessage`]{@link} on the channel for a given [`PresenceAction`]{@link}. |
|| `PresenceAction` || | A specific [`PresenceAction`]{@link} to unregister the listener for. |
| enter(Data?, extras?: JsonObject) => io ||| RTP8 | Enters the presence set for the channel, optionally passing a `data` payload. A [clientID]{@link} is required to be present on a channel. An optional callback may be provided to notify of the success or failure of the operation. |
|| `Data` || | The payload associated with the presence member. |
|| `extras` || | A JSON object of arbitrary `key:value` pairs that may contain metadata, and/or ancillary payloads. |
| update(Data?, extras?: JsonObject) => io ||| RTP9 | Updates the `data` payload for a presence member. If called before entering the presence set, this is treated as an `enter` event. An optional callback may be provided to notify of the success or failure of the operation. |
|| `Data` || | The payload to update for the presence member. |
|| `extras` || | A JSON object of arbitrary `key:value` pairs that may contain metadata, and/or ancillary payloads. |
| leave(Data?, extras?: JsonObject) => io ||| RTP10 | Leaves the presence set for the channel. A client must have previously entered the presence set before they can leave it. An optional callback may be provided to notify of the success or failure of the operation. |
|| `Data` || | The payload associated with the presence member. |
|| `extras` || | A JSON object of arbitrary `key:value` pairs that may contain metadata, and/or ancillary payloads. |
| enterClient(clientId: String, Data?, extras?: JsonObject) => io ||| RTP4, RTP14, RTP15 | Enters the presence set of the channel for a given `clientId`. Enables a single client to update presence on behalf of any number of clients using a single connection. The library must have been instantiated with an API key or a token bound to a wildcard `clientId`. An optional callback may be provided to notify of the success or failure of the operation. |
|| `clientId` || | The ID of the client to enter into the presence set. |
|| `Data` || | The payload associated with the presence member. |
|| `extras` || | A JSON object of arbitrary `key:value` pairs that may contain metadata, and/or ancillary payloads. |
| updateClient(clientId: String, Data?, extras?: JsonObject) => io ||| RTP15 | Updates the `data` payload for a presence member using a given `clientId`. Enables a single client to update presence on behalf of any number of clients using a single connection. The library must have been instantiated with an API key or a token bound to a wildcard `clientId`. An optional callback may be provided to notify of the success or failure of the operation. |
|| `clientId` || | The ID of the client to update in the presence set. |
|| `Data` || | The payload to update for the presence member. |
|| `extras` || | A JSON object of arbitrary `key:value` pairs that may contain metadata, and/or ancillary payloads. |
| leaveClient(clientId: String, Data?, extras?: JsonObject) => io ||| RTP15 | Leaves the presence set of the channel for a given `clientId`. Enables a single client to update presence on behalf of any number of clients using a single connection. The library must have been instantiated with an API key or a token bound to a wildcard `clientId`. An optional callback may be provided to notify of the success or failure of the operation. |
|| `clientId` || | The ID of the client to leave the presence set for. |
|| `Data` || | The payload associated with the presence member. |
|| `extras` || | A JSON object of arbitrary `key:value` pairs that may contain metadata, and/or ancillary payloads. |

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
| extras: JsonObject? ||| TP3i | A JSON object of arbitrary `key:value` pairs that may contain metadata, and/or ancillary payloads. |
| id: String ||| TP3a | A unique ID assigned to each `PresenceMessage` by Ably. |
| timestamp: Time ||| TP3g | The time the `PresenceMessage` was received by Ably, as a Unix timestamp. |
| memberKey() -> String ||| TP3h | Combines `clientId` and `connectionId` to ensure that multiple connected clients with an identical `clientId` are uniquely identifiable. A string function that returns the combined `clientId` and `connectionId`. |
||| `String` || A combination of `clientId` and `connectionId`. |

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
| ping() => io || RTN13 | |

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

`ConnectionEvent` describes the events emitted by a [`Connection`]{@link} object. An event is either an `UPDATE` or a `ConnectionState`.

| Enum | Spec | Description |
|---|---|---|
| embeds ConnectionState || The event contains a [`ConnectionState`]{@link}. |
| UPDATE | RTN4h | An event for changes to connection conditions for which the [`ConnectionState`]{@link} does not change. |

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

`PluginType` describes the type of plugin used.

| Enum | Spec | Description |
|---|---|---|
| "vcdiff" || A plugin capable of decoding `vcdiff`-encoded messages. It must implement the [`VCDiffDecoder`]{@link} interface. |

## class VCDiffDecoder

||| Spec | Description |
|---|---|---|---|
| decode([byte] delta, [byte] base) -> [byte]  || |

## class DeltaExtras

||| Spec | Description |
|---|---|---|---|
| from: String ||| |
| format: String ||| |