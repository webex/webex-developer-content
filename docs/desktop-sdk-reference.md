---
type: Guide
title: Desktop SDK Reference
display_title: Desktop SDK Reference
canonical_url: https://developer.webex.com/docs/desktop-sdk-reference
content_type: documentation
product_group:
- webex-contact-center
categories:
- webex-contact-center
---

> Official Webex documentation: [View this page on Webex for Developers](https://developer.webex.com/docs/desktop-sdk-reference)

Find Desktop SDK modules, methods, properties, and events with links to their detailed reference pages.

## SDK Modules

Initialize the SDK inside Desktop before using a module. See [Get Started with the Desktop SDK](https://developer.webex.com/docs/desktop-sdk-getting-started).

| Module | Purpose | Detailed reference |
| --- | --- | --- |
| `Desktop.config` | Initialize the SDK and register CRM connectors. | [Get Started with the Desktop SDK](https://developer.webex.com/docs/desktop-sdk-getting-started) |
| `Desktop.agentConfigJsApi` | Retrieve paginated idle and wrap-up codes. | [Agent State and Availability](https://developer.webex.com/docs/desktop-agent-state#fetchpaginatedauxcodes) |
| `Desktop.i18n` | Manage localization bundles. | [Localization](https://developer.webex.com/docs/desktop-localization) |
| `Desktop.actions` | Read data, send notifications, add tasks, and control WebRTC calls. | [Tasks and Call Control](https://developer.webex.com/docs/desktop-call-control), [availability](https://developer.webex.com/docs/desktop-agent-state), [notifications](https://developer.webex.com/docs/desktop-notifications-screen-pops), [authentication token](https://developer.webex.com/docs/desktop-sdk-getting-started#gettoken) |
| `Desktop.logger` | Create and collect widget logs. | [Logging and Diagnostics](https://developer.webex.com/docs/desktop-logging-diagnostics) |
| `Desktop.agentStateInfo` | Read agent data and change channel availability. | [Agent State and Availability](https://developer.webex.com/docs/desktop-agent-state), [address books and ANI](https://developer.webex.com/docs/desktop-outbound-callbacks#address-books-and-outbound-ani) |
| `Desktop.agentContact` | Control interactions, consultations, conferences, and transfers. | [Tasks and Call Control](https://developer.webex.com/docs/desktop-call-control), [consultation](https://developer.webex.com/docs/desktop-consultation-conferences), [transfers](https://developer.webex.com/docs/desktop-transfers), [events](https://developer.webex.com/docs/desktop-contact-events) |
| `Desktop.dialer` | Start outbound calls and update CAD variables. | [Outbound Calls and Scheduled Callbacks](https://developer.webex.com/docs/desktop-outbound-callbacks) |
| `Desktop.screenpop` | Listen for screen-pop events. | [Notifications and Screen Pops](https://developer.webex.com/docs/desktop-notifications-screen-pops) |
| `Desktop.shortcutKey` | Register shortcut actions and handle conflicts. | [Keyboard Shortcuts](https://developer.webex.com/docs/desktop-keyboard-shortcuts) |
| `Desktop.monitoring` | Control supervisor call monitoring. | [Supervisor Call Monitoring](https://developer.webex.com/docs/desktop-supervisor-monitoring) |
| `Desktop.webexMetricsInternal` | Track widget behavioral events; documented as an internal module. | [Logging and Diagnostics](https://developer.webex.com/docs/desktop-logging-diagnostics) |
| `Desktop.scheduleCallback` | Manage scheduled callbacks and valid campaign times. | [Outbound Calls and Scheduled Callbacks](https://developer.webex.com/docs/desktop-outbound-callbacks) |
| `Desktop.popover` | Manage anchored popovers in sandboxed widgets. | [Popovers](https://developer.webex.com/docs/desktop-popovers) |

## Methods and Properties

Each link opens the parameters, examples, responses, and restrictions for that API member. Deprecation notes identify legacy APIs; use the documented replacement where one is available.

### Get Started with the Desktop SDK

| API member | Purpose | Status |
| --- | --- | --- |
| [init(config)](https://developer.webex.com/docs/desktop-sdk-getting-started#initconfig) | Initiates the configuration module to start utilizing any of the `Desktop` modules. | — |
| [registerCrmConnector()](https://developer.webex.com/docs/desktop-sdk-getting-started#registercrmconnector) | The registerCrmConnector method is introduced as a new function to register a CRM connector. | — |
| [clientLocale](https://developer.webex.com/docs/desktop-sdk-getting-started#clientlocale) | Requests system data such as locale of the client. | — |
| [getToken()](https://developer.webex.com/docs/desktop-sdk-getting-started#gettoken) | Retrieves the authentication token used for SSO authentication. | — |

### Agent State and Availability

| API member | Purpose | Status |
| --- | --- | --- |
| [fetchPaginatedAuxCodes](https://developer.webex.com/docs/desktop-agent-state#fetchpaginatedauxcodes) | Retrieves the current idle codes or the current wrap up codes. | — |
| [getIdleCodes()](https://developer.webex.com/docs/desktop-agent-state#getidlecodes) | Retrieves the current idle codes. | Deprecated; use fetchPaginatedAuxCodes |
| [getWrapUpCodes()](https://developer.webex.com/docs/desktop-agent-state#getwrapupcodes) | Retrieves the wrap up codes. | Deprecated; use fetchPaginatedAuxCodes |
| [getMediaTypeQueue(mediaType)](https://developer.webex.com/docs/desktop-agent-state#getmediatypequeuemediatype) | Retrieves the current media queue for one channel type. | — |
| [latestData](https://developer.webex.com/docs/desktop-agent-state#latestdata) | Fetches the latest user related information. | — |
| [stateChange(state, auxCodeIdArray)](https://developer.webex.com/docs/desktop-agent-state#statechangestate-auxcodeidarray) | Changes the state of an agent. | Deprecated; use stateChangeV2 |
| [stateChangeV2(channelType, state, auxCodeId, reason, agentId)](https://developer.webex.com/docs/desktop-agent-state#statechangev2channeltype-state-auxcodeid-reason-agentid) | Changes the state of a particular channel for the agent. | — |
| [addEventListener](https://developer.webex.com/docs/desktop-agent-state#addeventlistener) | Listens to an event named **updated** that is logged if the dn, status, or subStatus field is changed. | — |

### Tasks and Call Control

| API member | Purpose | Status |
| --- | --- | --- |
| [addCustomTask()](https://developer.webex.com/docs/desktop-call-control#addcustomtask) | Adds a new custom task within your widget. | — |
| [getTaskMap()](https://developer.webex.com/docs/desktop-call-control#gettaskmap) | Retrieves the full list of tasks that are assigned to an agent at a given time. | — |
| [acceptWebRtcCall()](https://developer.webex.com/docs/desktop-call-control#acceptwebrtccall) | Accepts an incoming WebRTC call. | — |
| [declineWebRtcCall()](https://developer.webex.com/docs/desktop-call-control#declinewebrtccall) | Declines an incoming WebRTC call. | — |
| [toggleMuteUnmuteWebRtcCall()](https://developer.webex.com/docs/desktop-call-control#togglemuteunmutewebrtccall) | Toggles the mute/unmute state for an active WebRTC call. | — |
| [sendDtmf(dtmfData)](https://developer.webex.com/docs/desktop-call-control#senddtmfdtmfdata) | Sends Dual-Tone Multi-Frequency (DTMF) signals during an active call. | — |
| [accept()](https://developer.webex.com/docs/desktop-call-control#accept) | Accepts an incoming task. | Future deprecation |
| [end()](https://developer.webex.com/docs/desktop-call-control#end) | Ends an interaction for a specific task. | Future deprecation |
| [wrapup()](https://developer.webex.com/docs/desktop-call-control#wrapup) | Wraps up work for a task. | Future deprecation |
| [hold()](https://developer.webex.com/docs/desktop-call-control#hold) | Places a voice call on hold. | — |
| [unHold()](https://developer.webex.com/docs/desktop-call-control#unhold) | Resumes a voice call that is placed on hold. | — |
| [pauseRecording()](https://developer.webex.com/docs/desktop-call-control#pauserecording) | Pauses a call recording while obtaining sensitive information such as credit card information from the customer. | Future deprecation |
| [resumeRecording()](https://developer.webex.com/docs/desktop-call-control#resumerecording) | Resumes a voice call recording that is paused. | Future deprecation |
| [acceptV2()](https://developer.webex.com/docs/desktop-call-control#acceptv2) | Accepts an incoming task. | — |
| [endV2()](https://developer.webex.com/docs/desktop-call-control#endv2) | Ends an interaction for a specific task. | — |
| [cancelTaskV2()](https://developer.webex.com/docs/desktop-call-control#canceltaskv2) | Ends an interaction for a specific task. | — |
| [pauseRecordingV2()](https://developer.webex.com/docs/desktop-call-control#pauserecordingv2) | Pauses a call recording while obtaining sensitive information such as credit card information from the customer. | — |
| [resumeRecordingV2()](https://developer.webex.com/docs/desktop-call-control#resumerecordingv2) | Resumes a voice call recording that is paused. | — |
| [wrapupV2()](https://developer.webex.com/docs/desktop-call-control#wrapupv2) | Wraps up work for a task. | — |

### Consultation and Conferences

| API member | Purpose | Status |
| --- | --- | --- |
| [consultAccept()](https://developer.webex.com/docs/desktop-consultation-conferences#consultaccept) | Accepts a consult task. | — |
| [buddyAgents()](https://developer.webex.com/docs/desktop-consultation-conferences#buddyagents) | Fetches the list of agents available for consult call and conference call. | Deprecated; use buddyAgentsV2 |
| [consult()](https://developer.webex.com/docs/desktop-consultation-conferences#consult) | Initiates a consult request with an agent, a dial number (DN), or a queue. | Deprecated; use consultV2 |
| [consultConference()](https://developer.webex.com/docs/desktop-consultation-conferences#consultconference) | Initiates a conference request with one of the agents from the list of buddyAgents. | Deprecated; use consultConferenceV2 |
| [consultEnd()](https://developer.webex.com/docs/desktop-consultation-conferences#consultend) | Ends a consult request. | Deprecated; use consultEndV2 |
| [decline()](https://developer.webex.com/docs/desktop-consultation-conferences#decline) | Declines a consult request. | — |
| [cancelCtq()](https://developer.webex.com/docs/desktop-consultation-conferences#cancelctq) | Cancels a consult to queue request. | — |
| [consultV2()](https://developer.webex.com/docs/desktop-consultation-conferences#consultv2) | Initiates a consult request with an agent, a dial number (DN), a entrypoint or a queue. | — |
| [consultEndV2()](https://developer.webex.com/docs/desktop-consultation-conferences#consultendv2) | Ends a consult request. | — |
| [consultConferenceV2()](https://developer.webex.com/docs/desktop-consultation-conferences#consultconferencev2) | Initiates a conference request with consulting agent. | — |
| [exitConference()](https://developer.webex.com/docs/desktop-consultation-conferences#exitconference) | exits a conference request. | — |
| [buddyAgentsV2()](https://developer.webex.com/docs/desktop-consultation-conferences#buddyagentsv2) | Fetches the list of agents available for consult call and conference call. | — |
| [dropConferenceParticipant()](https://developer.webex.com/docs/desktop-consultation-conferences#dropconferenceparticipant) | Removes a participant from an active conference. | — |

### Transfer Contacts

| API member | Purpose | Status |
| --- | --- | --- |
| [vteamList()](https://developer.webex.com/docs/desktop-transfers#vteamlist) | Retrieves a list of vTeams (queues) available for transfer. | — |
| [vteamTransfer()](https://developer.webex.com/docs/desktop-transfers#vteamtransfer) | Initiates a vTeam transfer request. | Future deprecation |
| [blindTransfer()](https://developer.webex.com/docs/desktop-transfers#blindtransfer) | Initiates a blind transfer request. | Future deprecation |
| [consultTransfer()](https://developer.webex.com/docs/desktop-transfers#consulttransfer) | Initiates a consult transfer request. | Future deprecation |
| [consultTransferV2()](https://developer.webex.com/docs/desktop-transfers#consulttransferv2) | Initiates a consult transfer request. | — |
| [blindTransferV2()](https://developer.webex.com/docs/desktop-transfers#blindtransferv2) | Initiates a blind transfer request. | — |
| [vteamTransferV2()](https://developer.webex.com/docs/desktop-transfers#vteamtransferv2) | Initiates a vTeam transfer request. | — |

### Outbound Calls and Scheduled Callbacks

| API member | Purpose | Status |
| --- | --- | --- |
| [fetchAddressBooks()](https://developer.webex.com/docs/desktop-outbound-callbacks#fetchaddressbooks) | Retrieves the address book details. | — |
| [mockOutdialAniList()](https://developer.webex.com/docs/desktop-outbound-callbacks#mockoutdialanilist) | Fetches the ANI list that is used for an outdial call. | — |
| [startOutdial(data)](https://developer.webex.com/docs/desktop-outbound-callbacks#startoutdialdata) | Initiates an outdial call. | — |
| [updateCadVariables()](https://developer.webex.com/docs/desktop-outbound-callbacks#updatecadvariables) | Updates the Call-Associated Data (CAD) variables of a task. | — |
| [fetchByAssigneeAgentId(data)](https://developer.webex.com/docs/desktop-outbound-callbacks#fetchbyassigneeagentiddata) | Fetches scheduled callbacks for a given assignee agent ID. | — |
| [fetchByCallbackPhoneNumber(data)](https://developer.webex.com/docs/desktop-outbound-callbacks#fetchbycallbackphonenumberdata) | Fetches scheduled callbacks for a given callback phone number. | — |
| [createScheduleCallback(data)](https://developer.webex.com/docs/desktop-outbound-callbacks#createschedulecallbackdata) | Creates a new scheduled callback entry. | — |
| [updateCallBackDetails(data)](https://developer.webex.com/docs/desktop-outbound-callbacks#updatecallbackdetailsdata) | Updates an existing scheduled callback entry. | — |
| [deleteScheduleCallback(data)](https://developer.webex.com/docs/desktop-outbound-callbacks#deleteschedulecallbackdata) | Deletes a scheduled callback entry by its unique identifier. | — |
| [getValidCampaignTimes(data)](https://developer.webex.com/docs/desktop-outbound-callbacks#getvalidcampaigntimesdata) | Retrieves valid campaign callback time slots for a given campaign and agent. | — |

### Notifications and Screen Pops

| API member | Purpose | Status |
| --- | --- | --- |
| [fireGeneralSilentNotification(raw)](https://developer.webex.com/docs/desktop-notifications-screen-pops#firegeneralsilentnotificationraw) | Triggers silent notifications. | — |
| [fireGeneralAutoDismissNotification(raw)](https://developer.webex.com/docs/desktop-notifications-screen-pops#firegeneralautodismissnotificationraw) | Triggers the auto-dismiss notification. | — |
| [fireGeneralAcknowledgeNotification(raw)](https://developer.webex.com/docs/desktop-notifications-screen-pops#firegeneralacknowledgenotificationraw) | Triggers the acknowledge notification. | — |

### Keyboard Shortcuts

| API member | Purpose | Status |
| --- | --- | --- |
| [register()](https://developer.webex.com/docs/desktop-keyboard-shortcuts#register) | Registers the shortcut key actions. | — |
| [getRegisteredKeys()](https://developer.webex.com/docs/desktop-keyboard-shortcuts#getregisteredkeys) | Retrieves the registered shortcut keys with the modifiers. | — |
| [DEFAULT_SHORTCUT_KEYS](https://developer.webex.com/docs/desktop-keyboard-shortcuts#default-shortcut-keys) | Read default shortcut keys. | — |
| [MODIFIERS](https://developer.webex.com/docs/desktop-keyboard-shortcuts#modifiers) | Read shortcut modifiers. | — |
| [REGISTERED_KEYS](https://developer.webex.com/docs/desktop-keyboard-shortcuts#registered-keys) | Read registered keys without modifiers. | — |
| [unregisterKeys()](https://developer.webex.com/docs/desktop-keyboard-shortcuts#unregisterkeys) | Unregisters the shortcut keys. | — |
| [listenKeyPress(callback)](https://developer.webex.com/docs/desktop-keyboard-shortcuts#listenkeypresscallback) | Listens to shortcut key press. | — |
| [listenKeyConflict(callback)](https://developer.webex.com/docs/desktop-keyboard-shortcuts#listenkeyconflictcallback) | Listens to shortcut key conflicts. | — |
| [listenConflictResolved(callback)](https://developer.webex.com/docs/desktop-keyboard-shortcuts#listenconflictresolvedcallback) | Listens to shortcut key conflict resolved status. | — |

### Popovers

| API member | Purpose | Status |
| --- | --- | --- |
| [open(options)](https://developer.webex.com/docs/desktop-popovers#openoptions) | Opens a popover and renders the specified custom element inside it. | — |
| [close()](https://developer.webex.com/docs/desktop-popovers#close) | Closes the popover opened by your widget. | — |
| [resize(dimensions)](https://developer.webex.com/docs/desktop-popovers#resizedimensions) | Resizes the open popover. | — |
| [isActive()](https://developer.webex.com/docs/desktop-popovers#isactive) | Returns `true` when the current code is running **inside** a popover (that is, your widget was loaded as popover content). | — |
| [onOpen(callback) / onClose(callback)](https://developer.webex.com/docs/desktop-popovers#onopencallback--onclosecallback) | Subscribe to popover lifecycle events. | — |

### Localization

| API member | Purpose | Status |
| --- | --- | --- |
| [init(initOptions)](https://developer.webex.com/docs/desktop-localization#initinitoptions) | Initiates the localization module. | — |
| [createInstance(createOptions)](https://developer.webex.com/docs/desktop-localization#createinstancecreateoptions) | Creates the localization bundles for lit-element based widgets. | — |
| [createMixin()](https://developer.webex.com/docs/desktop-localization#createmixin) | Creates the localization (i18n) service instance into lit-element mixing. | — |
| [getMergedInitOptions()](https://developer.webex.com/docs/desktop-localization#getmergedinitoptions) | Adds or merges your localization package with the existing set of packages in Desktop. | — |
| [cleanup()](https://developer.webex.com/docs/desktop-localization#cleanup) | Triggers the clean up when init service returns an undefined response. | — |

### Logging and Diagnostics

| API member | Purpose | Status |
| --- | --- | --- |
| [createLogger(my-custom-component)](https://developer.webex.com/docs/desktop-logging-diagnostics#createloggermy-custom-component) | Initializes the logger for third-party widgets that help in logging related information to a particular component. | — |
| [browserDownloadLogsJson(my-custom-component)](https://developer.webex.com/docs/desktop-logging-diagnostics#browserdownloadlogsjsonmy-custom-component) | Downloads logs as a JSON file for the `my-custom-component` prefix. | — |
| [browserDownloadLogsText(my-custom-component)](https://developer.webex.com/docs/desktop-logging-diagnostics#browserdownloadlogstextmy-custom-component) | Downloads logs as a text file for the `my-custom-component` prefix. | — |
| [getLogsCollection(my-custom-component)](https://developer.webex.com/docs/desktop-logging-diagnostics#getlogscollectionmy-custom-component) | Retrieves logs as a collection of objects for the `my-custom-component` prefix. | — |
| [getLogsJsonUrl(my-custom-component)](https://developer.webex.com/docs/desktop-logging-diagnostics#getlogsjsonurlmy-custom-component) | Retrieves logs as a Base64 encoded URL to initiate browser download as a JSON file for the `my-custom-component` prefix. | — |
| [getLogsTextUrl(my-custom-component)](https://developer.webex.com/docs/desktop-logging-diagnostics#getlogstexturlmy-custom-component) | Retrieves logs as a Base64 encoded URL to initiate browser download as a text file for the `my-custom-component` prefix. | — |
| [cleanupPrefixedLogs(my-custom-component)](https://developer.webex.com/docs/desktop-logging-diagnostics#cleanupprefixedlogsmy-custom-component) | Cleans up logs from the local storage for the `my-custom-component` prefix. | — |
| [trackBehavioralEvent](https://developer.webex.com/docs/desktop-logging-diagnostics#trackbehavioralevent) | Log widget behavioral events; documented as an internal API. | — |

### Supervisor Call Monitoring

| API member | Purpose | Status |
| --- | --- | --- |
| [startMonitoring()](https://developer.webex.com/docs/desktop-supervisor-monitoring#start-monitoring) | The `Desktop.monitoring.startMonitoring` request monitors the calls received by an agent. | — |
| [holdMonitoring()](https://developer.webex.com/docs/desktop-supervisor-monitoring#pause-monitoring) | The `Desktop.monitoring.holdMonitoring` request pauses the call monitoring requests. | — |
| [unHoldMonitoring()](https://developer.webex.com/docs/desktop-supervisor-monitoring#resume-monitoring) | The `Desktop.monitoring.unHoldMonitoring` request resumes call monitoring that was paused earlier. | — |
| [endMonitoring()](https://developer.webex.com/docs/desktop-supervisor-monitoring#end-monitoring) | The `Desktop.monitoring.endMonitoring` request ends active call monitoring requests. | — |
| [bargeIn()](https://developer.webex.com/docs/desktop-supervisor-monitoring#barge-in) | The `Desktop.monitoring.bargeIn` request allows a supervisor to barge into an ongoing call between an agent and a customer, that is already being monitored. | — |

## Events and Subscriptions

For widget mounting behavior and listener cleanup, see [Contact Events and Subscriptions](https://developer.webex.com/docs/desktop-contact-events).

| Event or listener | Detailed reference |
| --- | --- |
| [addEventListener(event, handler)](https://developer.webex.com/docs/desktop-contact-events#addeventlistenerevent-handler) | Contact Events and Subscriptions |
| [removeEventListener(event, handler)](https://developer.webex.com/docs/desktop-contact-events#removeeventlistenerevent-handler) | Contact Events and Subscriptions |
| [addOnceEventListener(event, handler)](https://developer.webex.com/docs/desktop-contact-events#addonceeventlistenerevent-handler) | Contact Events and Subscriptions |
| [removeOnceEventListener(event, handler)](https://developer.webex.com/docs/desktop-contact-events#removeonceeventlistenerevent-handler) | Contact Events and Subscriptions |
| [removeAllEventListeners()](https://developer.webex.com/docs/desktop-contact-events#removealleventlisteners) | Contact Events and Subscriptions |
| [eParticipantLeftConference](https://developer.webex.com/docs/desktop-contact-events#eparticipantleftconference) | Contact Events and Subscriptions |
| [eAgentContactEnded](https://developer.webex.com/docs/desktop-contact-events#eagentcontactended) | Contact Events and Subscriptions |
| [eAgentCampaignContactUpdated](https://developer.webex.com/docs/desktop-contact-events#eagentcampaigncontactupdated) | Contact Events and Subscriptions; SDK 3 |
| [eContactOwnerChanged](https://developer.webex.com/docs/desktop-contact-events#econtactownerchanged) | Contact Events and Subscriptions; SDK 3 |
| [eParticipantJoinedConference](https://developer.webex.com/docs/desktop-contact-events#eparticipantjoinedconference) | Contact Events and Subscriptions; SDK 3 |
| [eAgentConsultConferencing](https://developer.webex.com/docs/desktop-contact-events#eagentconsultconferencing) | Contact Events and Subscriptions; SDK 3 |
| [eAgentConsultTransferring](https://developer.webex.com/docs/desktop-contact-events#eagentconsulttransferring) | Contact Events and Subscriptions; SDK 3 |
| [eAgentContact](https://developer.webex.com/docs/desktop-contact-events#eagentcontact) | Contact Events and Subscriptions |
| [eAgentContactAssigned](https://developer.webex.com/docs/desktop-contact-events#eagentcontactassigned) | Contact Events and Subscriptions |
| [eAgentContactAssignFailed](https://developer.webex.com/docs/desktop-contact-events#eagentcontactassignfailed) | Contact Events and Subscriptions |
| [eAgentContactWrappedUp](https://developer.webex.com/docs/desktop-contact-events#eagentcontactwrappedup) | Contact Events and Subscriptions |
| [eAgentContactAniUpdated](https://developer.webex.com/docs/desktop-contact-events#eagentcontactaniupdated) | Contact Events and Subscriptions |
| [eAgentOfferContact](https://developer.webex.com/docs/desktop-contact-events#eagentoffercontact) | Contact Events and Subscriptions |
| [eAgentOfferContactRona](https://developer.webex.com/docs/desktop-contact-events#eagentoffercontactrona) | Contact Events and Subscriptions |
| [eAgentOfferConsult](https://developer.webex.com/docs/desktop-contact-events#eagentofferconsult) | Contact Events and Subscriptions |
| [eAgentWrapup](https://developer.webex.com/docs/desktop-contact-events#eagentwrapup) | Contact Events and Subscriptions |
| [eAgentContactHeld](https://developer.webex.com/docs/desktop-contact-events#eagentcontactheld) | Contact Events and Subscriptions |
| [eAgentContactUnHeld](https://developer.webex.com/docs/desktop-contact-events#eagentcontactunheld) | Contact Events and Subscriptions |
| [eCallRecordingStarted](https://developer.webex.com/docs/desktop-contact-events#ecallrecordingstarted) | Contact Events and Subscriptions |
| [eResumeRecording](https://developer.webex.com/docs/desktop-contact-events#eresumerecording) | Contact Events and Subscriptions |
| [ePauseRecording](https://developer.webex.com/docs/desktop-contact-events#epauserecording) | Contact Events and Subscriptions |
| [eConsultTransfer](https://developer.webex.com/docs/desktop-contact-events#econsulttransfer) | Contact Events and Subscriptions |
| [eAgentblindTransferred](https://developer.webex.com/docs/desktop-contact-events#eagentblindtransferred) | Contact Events and Subscriptions |
| [eAgentvteamTransfer](https://developer.webex.com/docs/desktop-contact-events#eagentvteamtransfer) | Contact Events and Subscriptions |
| [eAgentConsultCreated](https://developer.webex.com/docs/desktop-contact-events#eagentconsultcreated) | Contact Events and Subscriptions |
| [eAgentConsultConferenced](https://developer.webex.com/docs/desktop-contact-events#eagentconsultconferenced) | Contact Events and Subscriptions |
| [eAgentConsultEnded](https://developer.webex.com/docs/desktop-contact-events#eagentconsultended) | Contact Events and Subscriptions |
| [eAgentCtqCancelled](https://developer.webex.com/docs/desktop-contact-events#eagentctqcancelled) | Contact Events and Subscriptions |
| [eAgentConsultConferenceEnded](https://developer.webex.com/docs/desktop-contact-events#eagentconsultconferenceended) | Contact Events and Subscriptions |
| [eAgentConsulting](https://developer.webex.com/docs/desktop-contact-events#eagentconsulting) | Contact Events and Subscriptions |
| [eAgentConsultFailed](https://developer.webex.com/docs/desktop-contact-events#eagentconsultfailed) | Contact Events and Subscriptions |
| [eAgentConsultEndFailed](https://developer.webex.com/docs/desktop-contact-events#eagentconsultendfailed) | Contact Events and Subscriptions |
| [eAgentCtqFailed](https://developer.webex.com/docs/desktop-contact-events#eagentctqfailed) | Contact Events and Subscriptions |
| [eAgentCtqCancelFailed](https://developer.webex.com/docs/desktop-contact-events#eagentctqcancelfailed) | Contact Events and Subscriptions |
| [eAgentConsultConferenceEndFailed](https://developer.webex.com/docs/desktop-contact-events#eagentconsultconferenceendfailed) | Contact Events and Subscriptions |
| [eAgentMonitorStateChanged](https://developer.webex.com/docs/desktop-contact-events#eagentmonitorstatechanged) | Contact Events and Subscriptions |
| [eAgentMonitoringEnded](https://developer.webex.com/docs/desktop-contact-events#eagentmonitoringended) | Contact Events and Subscriptions |
| [eAgentOfferCampaignReserved](https://developer.webex.com/docs/desktop-contact-events#eagentoffercampaignreserved) | Contact Events and Subscriptions |
| [eAgentAddCampaignReserved](https://developer.webex.com/docs/desktop-contact-events#eagentaddcampaignreserved) | Contact Events and Subscriptions |
| [eOutdialFailed](https://developer.webex.com/docs/desktop-outbound-callbacks#eoutdialfailed) | Outbound Calls and Scheduled Callbacks |
| [eScreenPop](https://developer.webex.com/docs/desktop-notifications-screen-pops#escreenpop) | Notifications and Screen Pops |
| [eMonitoringOffered](https://developer.webex.com/docs/desktop-supervisor-monitoring#start-monitoring-success) | Supervisor Call Monitoring |
| [eMonitoringRequestCreateFailed](https://developer.webex.com/docs/desktop-supervisor-monitoring#start-monitoring-create-failed) | Supervisor Call Monitoring |
| [eMonitoringStarted](https://developer.webex.com/docs/desktop-supervisor-monitoring#start-monitoring-call-offer-event-to-supervisor) | Supervisor Call Monitoring |
| [eMonitoringFailed](https://developer.webex.com/docs/desktop-supervisor-monitoring#start-monitoring-call-failed) | Supervisor Call Monitoring |
| [eMonitoringHeld](https://developer.webex.com/docs/desktop-supervisor-monitoring#pause-monitoring-success-event) | Supervisor Call Monitoring |
| [eMonitoringHoldFailed](https://developer.webex.com/docs/desktop-supervisor-monitoring#pause-monitoring-failed-event) | Supervisor Call Monitoring |
| [eMonitoringUnHeld](https://developer.webex.com/docs/desktop-supervisor-monitoring#resume-monitoring-success-event) | Supervisor Call Monitoring |
| [eMonitoringUnHoldFailed](https://developer.webex.com/docs/desktop-supervisor-monitoring#resume-monitoring-failed-event) | Supervisor Call Monitoring |
| [eMonitoringEnded](https://developer.webex.com/docs/desktop-supervisor-monitoring#end-monitoring-success-event) | Supervisor Call Monitoring |
| [eMonitoringEndFailed](https://developer.webex.com/docs/desktop-supervisor-monitoring#end-monitoring-failed-event) | Supervisor Call Monitoring |
| [eAgentMonitorStateChanged](https://developer.webex.com/docs/desktop-supervisor-monitoring#barge-in-success-event) | Supervisor Call Monitoring |
| [eAgentMonitorStateChangeFailed](https://developer.webex.com/docs/desktop-supervisor-monitoring#barge-in-failed-event) | Supervisor Call Monitoring |
| [updated](https://developer.webex.com/docs/desktop-agent-state#addeventlistener) | Agent State and Availability; global fields only |
| [eAgentChannelStateChanged](https://developer.webex.com/docs/desktop-agent-state#addeventlistener) | Agent State and Availability; granular channel states |

## Widget Data

For `STORE` fields and layout bindings, see [Widget Data and Desktop Layout](https://developer.webex.com/docs/desktop-widget-data-layout).

## Version and Availability Notes

- The SDK runs in widgets embedded within Desktop; it does not create a separate Desktop.
- With granular state control, use `stateChangeV2`, `STORE.agent.channelsStatesMap`, and `eAgentChannelStateChanged`. Global `subStatus` and the `updated` state-change event are not valid for that flow.
- The Popover APIs are available only in the isolated environment Desktop provides for custom widgets.
- The Webex Metrics module is documented as internal; its presence in this index does not establish availability for third-party widgets.

## Related Pages

- [Agent Desktop overview](https://developer.webex.com/docs/desktop)
- [Build Custom Widgets](https://developer.webex.com/docs/desktop-custom-widgets)
