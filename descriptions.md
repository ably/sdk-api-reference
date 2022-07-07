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

The `JsonObject` object denotes any type or interface in the target language that represents an RFC4627 object or array value respectively. Such types serialize to, and may be deserialized from, the corresponding JSON text. This object is platform-dependent, typically a Dict-like object.

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

The `PaginatedResult<T>` object represents a page of results for all message and presence history, stats, and REST presence requests. The response from an [Ably REST API paginated query](https://ably.com/docs/rest-api/#pagination) is accompanied by metadata that indicates the relative queries available to the `PaginatedResult` object.

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

||| Spec | Description |
|---|---|---|---|
| "vcdiff" || |

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
