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

The `Channels` object is used to create and destroy [`Channel`]{@link} objects.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| exists(String) -> Bool || | RSN2, RTS2 | Checks if a certain channel exists. |
|| `String` ||| The channel name. |
||| `Bool` || `true` if the channel exists, otherwise `false`. |
| get(String) -> ChannelType ||| RSN3a, RTS3a | Creates a new `ChannelType` if none for the channel exists, or returns the existing channel object. |
|| `String` ||| The channel name. |
||| `ChannelType` || A `ChannelType` object. |
| get(String, ChannelOptions) -> ChannelType || A `ChannelType` object. | RSN3c, RTS3c | Creates a new `ChannelType` object, with the specified [`ClientOptions`]{@link}, if none for the channel exists, or returns the existing channel object. |
|| `String` ||| The channel name. |
|| `ChannelOptions` ||| [`ChannelOptions`]{@link} used to configure the channel. |
||| `ChannelType` || A `ChannelType` object. |
| iterate() -> `Iterator<ChannelType>` ||| RSN2, RTS2 | Iterates through the existing channels. |
||| `ChannelType` || Each iteration returns a `ChannelType` object. |
| release(String) ||| RSN4, RTS4 | Releases a [`Channel`]{@link} object, deleting it, and enabling it to be garbage collected. It also removes any listeners associated with the channel. To release a channel, the channel state must be `initialized`, `detached`, or `failed`. |
|| `String` ||| The channel name. |

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

The `RealtimeChannel` object is one where when it becomes attached, all incoming messages and presence messages are processed and emitted where applicable. Incoming is defined as "received from Ably over the realtime transport".

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| embeds `EventEmitter<ChannelEvent, ChannelStateChange?>` ||| RTL2a, RTL2d, RTL2e | The `RealtimeChannel` implements [`EventEmitter`]{@link} and emits [`ChannelEvent`]{@link} events, where a `ChannelEvent` is either a [`ChannelState`]{@link} or `UPDATE`, and a `ChannelState` is either `INITIALIZED`, `ATTACHING`, `ATTACHED`, `DETACHING`, `DETACHED`, `SUSPENDED` and `FAILED`. |
| errorReason: ErrorInfo? ||| RTL4e | An error as an [`ErrorInfo`]{@link} object when a channel failure occurs. |
| state: ChannelState ||| RTL2b | The current [`ChannelState`]{@link} of this [`Channel`]{@link}. |
| presence: RealtimePresence ||| RTL9 | Provides access to the [`Presence`]{@link} object for this channel which can be used to access members present on the channel, or participate in presence. |
| properties: ChannelProperties ||| CP1, RTL15 | A [`ChannelProperties`]{@link} object representing properties of the channel state. |
| push: PushChannel ||| Provides access to the [`PushChannel`]{@link} object for this channel. |
| modes: readonly [ChannelMode] ||| RTL4m | An array of [`ChannelMode`]{@link} objects. |
| params: readonly `Dict<String, String>` ||| RTL4k1 | Optional [channel parameters](https://ably.com/docs/realtime/channels/channel-parameters/overview) that configure the behavior of the channel. |
| attach() => io ||| RTL4d | Attach to this channel ensuring the channel is created in the Ably system and all messages published on the channel are received by any channel listeners registered using `subscribe()`. Any resulting channel state change will be emitted to any listeners registered using the on or once methods. As a convenience, `attach()` is called implicitly if subscribe for the Channel is called, or `enter()` or `subscribe()` is called on the Presence for this Channel. |
| detach() => io ||| RTL5e | Detach from this channel. Any resulting channel state change is emitted to any listeners registered using the `on` or `once` methods. Once all clients globally have detached from the channel, the channel will be released in the Ably service within two minutes. |
| history(start: Time, end: Time api-default now(), direction: .Backwards \| .Forwards api-default .Backwards, limit: int api-default 100, untilAttach: Bool default false) => io `PaginatedResult<Message>` ||| RSL2a | Retrieves a paginated set of historical messages for this channel. If the channel is configured to persist messages to disk, then message history will typically be available for 24 – 72 hours. If not, messages are only retained in memory by the Ably service for two minutes. |
|| `start` || RTL10a | The time from which messages are retrieved, specified as a Unix timestamp. |
|| `end` || RTL10a | The time until messages are retrieved, specified as a Unix timestamp. |
|| `direction` || RTL10a | The order for which messages are returned in. The default is `Backwards` which orders messages from most recent to oldest. |
|| `limit` || RTL10a | An upper limit on the number of messages returned, up to 1000. |
|| `untilAttach` || RTL10b | When `true`, ensures message history is up until the point of the channel being attached. See [continuous history](https://ably.com/docs/realtime/history#continuous-history) for more info. Requires the direction to be backwards (the default). If the channel is not attached, or if direction is set to `forwards`, this option results in an error. |
| publish(Message) => io ||| RTL6i | Publishes a message on this channel. A callback may optionally be passed in to this call to be notified of success or failure of the operation. When publish is called with this client library, it won't attempt to implicitly attach to the channel. |
| publish([Message]) => io ||| RTL6i | Publishes several messages on this channel. A callback may optionally be passed in to this call to be notified of success or failure of the operation. When publish is called with this client library, it won't attempt to implicitly attach to the channel. |
| publish(name: String?, data: Data?) => io ||| RTL6i | Publishes a single message on this channel based on a given event name and payload. A callback may optionally be passed in to this call to be notified of success or failure of the operation. When publish is called with this client library, it won't attempt to implicitly attach to the channel, so long as [transient publishing](https://ably.com/docs/realtime/channels#transient-publish) is available in the library. Otherwise, the client will implicitly attach. |
| subscribe((Message) ->) => io ||| RTL7a | Subscribes to messages on this channel. The caller supplies a listener function, which is called each time one or more messages arrives on the channel. |
| subscribe(String, (Message) ->) => io ||| RTL7b | Subscribes to messages with a given event `name` on this channel. The caller supplies a listener function, which is called each time one or more matching messages arrives on the channel. |
| subscribe([String], (Message) ->) => io ||| RTL7a | Subscribes a single listener to messages on this channel for multiple event name values. |
| unsubscribe(String, (Message) ->) ||| RTL8a | Unsubscribes the given listener for the specified event name. This removes an earlier event-specific subscription. |
| unsubscribe((Message) ->) ||| RTL8a | Unsubscribes the given listener (for any/all event names). This removes an earlier subscription. |
| unsubscribe([String], (Message) ->) ||| RTL8a | Unsubscribes the given listener from all event names in the array. |
| unsubscribe(String) ||| RTL8a | Unsubscribes all listeners for the given event name. |
| unsubscribe([String]) ||| RTL8a | Unsubscribes all listeners for all event names in the array. |
| unsubscribe() ||| RTL8a, RTE5 | Unsubscribes all listeners to messages on this channel. This removes all earlier subscriptions. |
| setOptions(options: ChannelOptions) => io ||| RTL16 | Sets the [`ChannelOptions`]{@link} for the channel. |

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

The `ChannelStateChange`  object encapsulates state change information emitted by the `Channel` object.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|---|
| current: ChannelState ||| RTL2a, RTL2b | The new current state. |
| event: ChannelEvent ||| TH5 | The event that triggered this state change. |
| previous: ChannelState ||| RTL2a, RTL2b | The previous state. For the `update` event, this is equal to the `current` state. |
| reason: ErrorInfo? ||| RTL2e, TH3 | An [`ErrorInfo`]{@link} object containing any information relating to the transition. |
| resumed: Boolean ||| RTL2f, TH4 | A boolean indicated whether message continuity on this channel is preserved, see [Nonfatal channel errors](https://ably.com/docs/realtime/channels#nonfatal-errors) for more info. |

## class ChannelOptions

The `ChannelOptions` object is used when creating a channel object, to configure the channel.

| Method / Property | Parameter | Returns | Spec | Description |
|---|---|---|---|----|
| +withCipherKey(key: Binary \| String)? -> ChannelOptions || A `ChannelOptions` object. | TB3 | Optional constructor `withCipherKey`, that takes a key only. |
| cipher: (CipherParams \| Params)? ||| RSL5a, TB2b | Requests encryption for this channel when not null, and specifies encryption-related parameters (such as algorithm, chaining mode, key length and key). See [an example](https://ably.com/docs/realtime/encryption#getting-started). |
| params?: `Dict<String, String>` ||| TB2c | Optional [parameters](https://ably.com/docs/realtime/channels/channel-parameters/overview) that configure the behavior of the channel. |
| modes?: [ChannelMode] ||| TB2d | For realtime client libraries only. An array of [`ChannelMode`]{@link} objects. |

## class ChannelDetails

The `ChannelDetails` object represents information for a channel including `channelId`, `status` and occupancy.

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
| connections: Int ||| CHM2a | The total number of connections to the channel. |
| presenceConnections: Int ||| CHM2b | The total number of presence connections to the channel. |
| presenceMembers: Int ||| CHM2c | The total number of presence members for the channel. |
| presenceSubscribers: Int ||| CHM2d | The total number of presence subscribers for the channel. |
| publishers: Int ||| CHM2e | The total number of publishers to the channel. |
| subscribers: Int ||| CHM2f | The total number of subscribers to the channel. |

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
||| [`Message`] || An array of Message-like deserialized objects. |
| clientId: String? ||| RSL1g1, TM2b | The client ID of the publisher of this message. |
| connectionId: String? ||| TM2c | The connection ID of the publisher of this message. |
| data: Data? ||| TM2d | The message payload, if provided. |
| encoding: String? ||| TM2e | This is typically empty, as all messages received from Ably are automatically decoded client-side using this value. However, if the message encoding cannot be processed, this attribute contains the remaining transformations not applied to the `data` payload. |
| extras: JsonObject? ||| TM2i | A combination of metadata or ancillary payloads. Currently the only valid payload for `extras` is the `push` object. |
| id: String ||| TM2a | A Unique ID assigned by Ably to this message. |
| name: String? ||| TM2g | The event name. |
| timestamp: Time ||| TM2f | Timestamp of when the message was received by the Ably, as a Unix timestamp. |

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