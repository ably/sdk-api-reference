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
|| `clientOptions` ||| Options to configure the client connection to Ably. |
| auth: Auth ||| RSC5 | An [`Auth`]{@link} authentication object. |
| push: Push ||| RSH7 | A [`Push`]{@link} object. |
| batch: BatchOperations ||| BO1 | A [`BatchOperations`]{@link} object. |
| device() => LocalDevice ||  | RSH8 | Retrieves a local device object. |
||| `LocalDevice` || A [`LocalDevice`]{@link} object that represents the current state of the device as a target for push notifications. |
| channels: `Channels<RestChannel>` ||| RSN1 | A [`Channel`]{@link} collection object. |
| request() => io HttpPaginatedResponse ||  | RSC19 | Makes a REST request to a provided path. This is provided as a convenience for developers who wish to use REST API functionality that is either not documented or is not yet included in the public API, without having to directly handle features such as authentication, paging, fallback hosts, MsgPack and JSON support. |
|| `method` ||| Request method to use such as `GET`, `POST`. |
|| `path` ||| Request path. |
|| `params` ||| Parameters for the REST request. |
|| `body` ||| JSON body for the request. |
|| `headers` ||| Headers for the request. |
||| `HttpPaginatedResponse` || Response from an HTTP request containing an empty or JSON-encodable object response. |
| stats() => io `PaginatedResult<Stats>` ||| RSC6a | Queries the [REST `/stats` API](https://ably.com/docs/rest-api#stats) and retrieves your application's usage statistics. A [`PaginatedResult`]{@link} is returned, containing an array of stats for the first page of results. `PaginatedResult` objects are iterable providing a means to page through historical statistics. See the [Stats docs](https://ably.com/docs/general/statistics). |
|| `start` | | RSC6b1 | Earliest time as a Unix timestamp for any stats retrieved. |
|| `end` | | RSC6b1 | Latest time as a Unix timestamp for any stats retrieved. |
|| `direction` | | RSC6b2 | Work `backwards` or `forwards` through time. |
|| `limit` | | RSC6b3 | Maximum number of messages to retrieve up to 1,000. |
|| `unit` | | RSC6b4 | `minute`, `hour`, `day` or `month`. Based on the unit selected, the given `start` or `end` times are rounded down to the start of the relevant interval depending on the unit granularity of the query. |
||| `PaginatedResult` | | A [`PaginatedResult`]{@link} containing an array of stats for the first page of results. |
| time() => io Time ||| RSC16 | Retrieves the time from the Ably service as a Unix timestamp in milliseconds. Clients that do not have access to a sufficiently well maintained time source and wish to issue Ably `TokenRequest`s with a more accurate timestamp should use the `queryTime` `ClientOptions` instead of this method. |
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
|| `clientOptions` ||| Options to configure the client connection to Ably. |
| auth: Auth ||| RTC4 | An [`Auth`]{@link} authentication object. |
| push: Push ||| | A [`Push`]{@link} object. |
| device() => LocalDevice ||  | RSH8 | Retrieves a local device object. |
||| `LocalDevice` || A [`LocalDevice`]{@link} object that represents the current state of the device as a target for push notifications. |
| channels: `Channels<RealtimeChannel>` ||| RTC3, RTS1 | A [`Channel`]{@link} collection object. |
| clientId: String? ||| proxy for RSA7 | A client ID, used for identifying this client when publishing messages or for presence purposes. The `clientId` can be any non-empty string. This option is primarily intended to be used in situations where the library is instantiated with a key. A `clientId` may also be implicit in a token used to instantiate the library; an error will be raised if a `clientId` specified here conflicts with the `clientId` implicit in the token.|
| connection: Connection ||| RTC2 | A reference to the [`Connection`]{@link} object. |
| request() => io HttpPaginatedResponse ||| RTC9 | Makes a REST request to a provided path. This is provided as a convenience for developers who wish to use REST API functionality that is either not documented or is not yet included in the public API, without having to directly handle features such as authentication, paging, fallback hosts, MsgPack and JSON support. |
|| `method` ||| Request method to use such as `GET`, `POST`.|
|| `path` ||| Request path. |
|| `params` ||| Parameters for the REST request. |
|| `body` ||| JSON body for the request. |
|| `headers` ||| Headers for the request. |
||| `HttpPaginatedResponse` || The response from an HTTP request containing an empty or JSON-encodable object response. |
| stats: ||| Same as Rest.stats, RTC5a | Queries the [REST `/stats` API](https://ably.com/docs/rest-api#stats) and retrieves your application's usage statistics. A [`PaginatedResult`]{@link} is returned, containing an array of stats for the first page of results. `PaginatedResult` objects are iterable providing a means to page through historical statistics. See the [Stats docs](https://ably.com/docs/general/statistics). |
| close() ||| proxy for RTN12 | This calls `connection.close()` and causes the connection to close, entering the closing state. Once closed, the library will not attempt to re-establish the connection without an explicit call to `connect()`. |
| connect() ||| proxy for RTN11 | This method calls `connection.connect()` and causes the connection to open, entering the connecting state. Explicitly calling `connect()` is unnecessary unless the `ClientOptions` `autoConnect` is disabled. |
| time() => io Time ||| RTC6a | Retrieves the time from the Ably service as a Unix timestamp in milliseconds. Clients that do not have access to a sufficiently well maintained time source and wish to issue Ably `TokenRequest`s with a more accurate timestamp should use the [`queryTime`]{@link} client option instead of this method. |
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