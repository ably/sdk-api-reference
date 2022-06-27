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

The state of the channel.

| Enum || Spec | Description |
|---|---|---|---|
| INITIALIZED || A `Channel` object having this state has been initialized but no attach has yet been attempted. |
| ATTACHING || An attach has been initiated by sending a request to Ably. This is a transient state; it will be followed either by a transition to attached, suspended, or failed. |
| ATTACHED || Attach has succeeded. In the attached state a client may publish and subscribe to messages, or be present. |
| DETACHING || A detach has been initiated on the attached `Channel` by sending a request to Ably. This is a transient state; it will be followed either by a transition to detached or failed. |
| DETACHED || The `Channel`, having previously been attached, has been detached by the user. |
| SUSPENDED || The `Channel`, having previously been attached, has lost continuity, usually due to the client being disconnected from Ably for more than two minutes. It will automatically attempt to reattach as soon as connectivity is restored. |
| FAILED || An indefinite failure condition. This state is entered if a `Channel` error has been received from the Ably service (such as an attempt to attach without the necessary access rights). |

## enum ChannelEvent

`ChannelEvent` is a string that can be emitted as an event on the `Channel` object; either a `ChannelState` or an `update` event.

| Enum || Spec | Description |
|---|---|---|---|
| embeds ChannelState || The event contains a `[ChannelState]{@link}`|
| UPDATE || RTL2g | An event for changes to channel conditions that do not result in a change in `ChannelState`. |

## enum ChannelMode

`ChannelMode` is set by the client to configure client capabilities. The mode flags can be combined to reflect the capabilities required.

| Enum || Spec | Description |
|---|---|---|---|
| PRESENCE || The client can enter presence. |
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

`PresenceAction` is a string with a value matching any of the Realtime Presence states and events.

| Enum || Spec | Description |
|---|---|---|---|
| ABSENT || TP2 | A member is not present in the channel. |
| PRESENT || TP2 | When subscribing to presence events on a channel that already has members present, this event is emitted for every member already present on the channel before the subscribe listener was registered. |
| ENTER || TP2 | A new member has entered the channel. |
| LEAVE || TP2 | A member who was present has now left the channel. This may be a result of an explicit request to leave or implicitly when detaching from the channel. Alternatively, if a member's connection is abruptly disconnected and they do not resume their connection within a minute, Ably treats this as a leave event as the client is no longer present. |
| UPDATE || TP2 | An already present member has updated their member data. Being notified of member data updates can be very useful, for example, it can be used to update the status of a user when they are typing a message. |

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

| Enum || Spec | Description |
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

`ConnectionEvent` is a string that can be emitted as an event on the `Connection` object; either a Realtime `ConnectionState` or an `update` event.

| Enum || Spec | Description |
|---|---|---|---|
| embeds ConnectionState || See [`ConnectionState`]{@link}. |
| UPDATE || RTN4h | An event for changes to connection conditions for which the `ConnectionState` (such as `CONNECTED`) does not change. |

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

The interval unit over which statistics are gathered.

| Enum || Spec | Description |
|---|---|---|---|
| MINUTE || Interval unit over which statistics are gathered is a minute. |
| HOUR || Interval unit over which statistics are gathered is an hour. |
| DAY || Interval unit over which statistics are gathered is a day. |
| MONTH || Interval unit over which statistics are gathered is a month. |

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

The device receiving push notifications.

| Enum || Spec | Description |
|---|---|---|---|
| "android" || PCD6 | Device platform is Android. |
| "ios" || PCD6 | Device platform is iOS. |
| "browser" || PCD6 | Device platform is web browser. |

## enum DeviceFormFactor

Form factor of device receiving the push notification.

| Enum || Spec | Description |
|---|---|---|---|
| "phone" || PCD4 | Device form factor. |
| "tablet" || PCD4 | Device form factor. |
| "desktop" || PCD4 | Device form factor. |
| "tv" || PCD4 | Device form factor. |
| "watch" || PCD4 | Device form factor. |
| "car" || PCD4 | Device form factor. |
| "embedded" || PCD4 | Device form factor. |
| "other" || PCD4 | Device form factor. |

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

| Enum || Spec | Description |
|---|---|---|---|
| "vcdiff" || A plugin capable of decoding vcdiff-encoded messages. It must implement the [`VCDiffDecoder`]{@link} interface. |

## class VCDiffDecoder

||| Spec | Description |
|---|---|---|---|
| decode([byte] delta, [byte] base) -> [byte]  || The `VCDiffDecoder.decode` method receives the stored base payload of the last message on a channel. If the base payload is a string, it should be encoded to binary using UTF-8, before being passed as the `base` argument to the `VCDiffDecoder.decode` method. |

## class DeltaExtras

||| Spec | Description |
|---|---|---|---|
| from: String ||| |
| format: String ||| |