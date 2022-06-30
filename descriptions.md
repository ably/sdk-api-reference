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
| syncComplete: Bool ||| RTP13 | Shows whether the presence set sync between Ably and the clients on the channel has been completed. Set to `true` when the sync is complete. |
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

||| Spec | Description |
|---|---|---|---|
| ABSENT || TP2 | |
| PRESENT || TP2 | |
| ENTER || TP2 | |
| LEAVE || TP2 | |
| UPDATE || TP2 | |

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