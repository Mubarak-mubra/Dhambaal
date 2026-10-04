# Dhambaal

**A decentralized, peer-to-peer communication platform built for the Somali community.**

Dhambaal is a cross-platform communication application **built specifically for the Somali community**.

The project combines a peer-to-peer communication model with local-first data storage and resilient network connectivity. Its goal is to provide a communication experience that is more direct, user-controlled, and adapted to Somali users and their digital environment.

Dhambaal uses **WebRTC for peer-to-peer data and media transport**, **MQTT for signaling and presence**, and **device-local storage for application data**.

The application currently targets **mobile and web** using React Native, Expo, and React Native Web.

---

## Built for the Somali Community

Dhambaal is not simply a generic communication application translated into Somali.

It is a project **built specifically for Somali users and the Somali digital community**.

Somali is a primary language within the application interface, and the project is designed around the needs, usability, accessibility, and digital environment of Somali users.

The broader vision is to contribute to a Somali technology ecosystem where Somali users are not only consumers of existing global platforms, but can also use and build systems created specifically for their own community.

---

# Why Dhambaal?

Traditional communication systems often rely on centralized infrastructure for message delivery and storage.

Dhambaal explores another model.

The application tries to establish a **direct peer-to-peer connection** between users. When network conditions such as NAT or firewall restrictions prevent direct connectivity, Dhambaal can use TURN relay infrastructure.

A key part of Dhambaal is that users can also configure their **own TURN servers**.

This gives the project a connectivity model built around three layers:

```text
                ┌───────────────────────────────┐
                │        Layer 1: P2P           │
                │   Direct WebRTC connection    │
                └───────────────┬───────────────┘
                                │
                       Direct path unavailable
                                │
                                ▼
                ┌───────────────────────────────┐
                │     Layer 2: Custom Relay     │
                │   User-managed TURN server    │
                └───────────────┬───────────────┘
                                │
                  Custom relay unavailable
                    or cannot provide a path
                                │
                                ▼
                ┌───────────────────────────────┐
                │     Layer 3: Default Relay    │
                │   Dhambaal-provided TURN      │
                └───────────────────────────────┘
```

---

# Connectivity Architecture

## Layer 1 — Direct P2P

Dhambaal first aims to establish a **direct WebRTC connection** between two users.

When the network environment allows it, data and voice communication can travel directly between the two peers without requiring a TURN relay.

This is the preferred communication path because it minimizes dependence on relay infrastructure.

---

## Layer 2 — Custom Relay

Direct peer-to-peer connectivity is not always possible.

NAT behavior, restrictive firewalls, mobile carrier networks, VPNs, and other network conditions can prevent two devices from establishing a usable direct path.

For this reason, Dhambaal allows users to configure their own TURN servers.

A user can rent or operate a TURN server from a provider and configure it inside the application.

The configuration is available from:

```text
Aniga
→ Xiriirka (Relay)
→ Add Relay
```

A custom relay can contain:

* Relay name
* One or more TURN URLs
* Username
* Credential
* Enabled / disabled state

Multiple custom relays can be configured and stored locally.

This allows users to bring their own relay infrastructure instead of depending exclusively on infrastructure operated by Dhambaal.

---

## Layer 3 — Default Relay

Dhambaal also includes built-in TURN infrastructure as a final connectivity option.

When a user does not configure a custom relay, or when configured relay infrastructure cannot provide a usable connection, the application can use its built-in TURN providers.

The current implementation includes multiple default TURN providers for redundancy.

---

# Important Connectivity Detail

The three layers describe Dhambaal's **connectivity strategy**, but WebRTC does not implement them as a simple hard-coded sequence where an entire layer must completely fail before the next layer is even considered.

Dhambaal constructs an ICE configuration containing:

```text
STUN servers
+
User-configured TURN servers
+
Built-in TURN servers
```

WebRTC ICE evaluates the available candidates and selects a working candidate pair.

Conceptually:

```text
Prefer direct connectivity
          ↓
Use relay connectivity when direct connectivity is unavailable
          ↓
Custom and built-in TURN provide relay candidates
          ↓
Retry when the connection fails
```

The architectural idea is:

**Direct P2P → User-controlled relay → Dhambaal-provided relay**

while actual connectivity selection is performed by WebRTC ICE.

---

# Architecture

Dhambaal is built from several cooperating layers:

```text
┌──────────────────────────────────────────────────────────┐
│                        Dhambaal UI                        │
│             React Native + Expo + Expo Router            │
│                  Somali-first experience                 │
└────────────────────────────┬─────────────────────────────┘
                             │
                             ▼
┌──────────────────────────────────────────────────────────┐
│                     Feature Services                      │
│                                                          │
│ Messaging │ Contacts │ Contact Requests │ Calls          │
│ Voice Notes │ File Sharing │ Presence                    │
└────────────────────────────┬─────────────────────────────┘
                             │
              ┌──────────────┴──────────────┐
              ▼                             ▼
┌──────────────────────────┐   ┌───────────────────────────┐
│     Transport Layer      │   │      Local Data Layer     │
│                          │   │                           │
│ WebRTC Data Channels     │   │ AsyncStorage              │
│ WebRTC Media             │   │ GunDB (local-only)        │
│ ICE / STUN / TURN        │   │ Device file storage       │
│ MQTT Signaling           │   │ Web storage on Web        │
└──────────────┬───────────┘   └───────────────────────────┘
               │
       ┌───────┴────────┐
       ▼                ▼
   Direct P2P       TURN Relay
                       │
              ┌────────┴─────────┐
              ▼                  ▼
        Custom TURN         Default TURN
```

---

# Control Plane and Data Plane

A major architectural decision in Dhambaal is the separation between **signaling** and the actual communication transport.

## Control Plane — MQTT

MQTT is primarily used for coordination.

Dhambaal currently connects to multiple MQTT brokers to provide signaling redundancy.

MQTT is used for:

* WebRTC offers
* WebRTC answers
* ICE candidates
* wake-up signals
* call signaling
* presence
* connection coordination

Conceptually:

```text
User A
   │
   │ Offer / Answer / ICE / Presence
   ▼
MQTT Brokers
   │
   ▼
User B
```

MQTT therefore acts as the **signaling and coordination layer**.

---

## Data Plane — WebRTC

The main communication transport is WebRTC.

WebRTC DataChannels are used for:

* text messages
* contact request messages
* voice-note payloads
* file metadata
* file chunks
* other peer-to-peer application payloads

WebRTC media connections are used for:

* voice calls

Conceptually:

```text
             MQTT
      Signaling / Coordination
          /            \
         /              \
        ▼                ▼
   User A  <----------> User B
             WebRTC
```

The MQTT brokers are therefore not the primary transport for the application's chat and call media.

---

# Connection Establishment

A typical WebRTC connection works approximately like this:

```text
1. User wants to connect
          │
          ▼
2. Dhambaal creates a WebRTC PeerConnection
          │
          ▼
3. ICE configuration is loaded
   ├── STUN
   ├── Custom TURN
   └── Default TURN
          │
          ▼
4. Offer is created
          │
          ▼
5. Offer is sent through MQTT
          │
          ▼
6. Peer receives the offer
          │
          ▼
7. Peer creates an answer
          │
          ▼
8. Answer is sent through MQTT
          │
          ▼
9. ICE candidates are exchanged
          │
          ▼
10. WebRTC selects the best available path
          │
          ├── Direct P2P
          │
          └── TURN relay
          │
          ▼
11. DataChannel / media connection becomes available
```

Dhambaal also buffers ICE candidates when necessary so that candidates received before a remote description is available can be added later.

---

# Network Path Detection

After a connection succeeds, Dhambaal inspects WebRTC connection statistics.

This allows it to determine whether the active path is:

```text
P2P
```

or:

```text
Relay
```

For relay connections, the application can attempt to identify a configured custom relay and record local relay statistics.

The local statistics include information such as:

* successful relay attempts
* failed relay attempts
* last-used time

---

# Automatic Connection Recovery

Network conditions can change after a connection has already been established.

Dhambaal monitors the WebRTC ICE connection state and reacts to connection failures.

Conceptually:

```text
connected
    │
    ├── P2P
    │
    └── Relay

If connection becomes disconnected
            │
            ▼
       monitor / wait
            │
            ▼
        reconnect

If ICE fails
            │
            ▼
      close connection
            │
            ▼
       retry connection
            │
            ▼
    evaluate ICE paths again
```

This is particularly useful for mobile networks, unstable Wi-Fi, NAT changes, and other real-world connectivity conditions.

---

# Custom Relay Infrastructure

One of the distinctive features of Dhambaal is its **bring-your-own-TURN** approach.

A user can:

```text
1. Rent or operate a TURN server
2. Obtain the TURN server URL
3. Obtain authentication credentials
4. Open Dhambaal
5. Go to Aniga → Xiriirka (Relay)
6. Add the relay
```

The relay configuration supports:

```text
Relay Name
TURN URLs
Username
Credential
Enabled / Disabled
```

Multiple relays may be configured.

Example:

```text
My TURN Server

URLs:
turn:example.com:3478
turns:example.com:5349

Username:
my-user

Credential:
********
```

The configuration is stored locally on the user's device.

---

# Presence

Dhambaal implements a presence system using MQTT.

Users publish their presence and subscribe to the presence topics of their contacts.

Presence is used to determine whether contacts are online or offline and can help trigger connection attempts.

Conceptually:

```text
User A
   │
   │ online
   ▼
MQTT Presence
   │
   ▼
User B
   │
   ▼
Contact appears online
```

Presence belongs to the signaling/control plane and is separate from the application's main message transport.

---

# Messaging

Dhambaal follows a local-first messaging model.

A message is stored locally before delivery is attempted.

```text
User writes message
        │
        ▼
Save locally
        │
        ▼
Attempt WebRTC delivery
        │
        ├── Connected
        │       │
        │       ▼
        │    Send directly
        │
        └── Not connected
                │
                ▼
          Store in queue
                │
                ▼
        Retry when connection
           becomes available
```

This allows outgoing messages to remain available locally even when a peer connection is temporarily unavailable.

---

# Pending Message Queue

Dhambaal maintains a local queue for messages that cannot be delivered immediately.

Queued messages are persisted locally.

When the peer connection becomes available again, Dhambaal attempts to send the pending messages.

```text
Message
   │
   ├── Connection available → Send
   │
   └── Connection unavailable
            │
            ▼
       Local queue
            │
            ▼
    Connection restored
            │
            ▼
        Send message
```

---

# Voice Calls

Voice calls use WebRTC media connections.

Call coordination uses MQTT signaling.

Conceptually:

```text
Call Offer
    ↓
MQTT
    ↓
Call Answer
    ↓
MQTT
    ↓
ICE Candidates
    ↓
WebRTC Media
```

The call layer supports:

* outgoing calls
* incoming calls
* missed calls
* accepted calls
* rejected calls
* ended calls

Dhambaal also integrates native notification handling for incoming calls on supported platforms.

---

# Voice Notes

Voice notes are recorded locally and transferred through the peer connection.

The application supports:

* web recording
* native mobile recording
* local audio storage
* playback
* peer-to-peer transfer

On mobile, voice recordings can be stored in the device file system.

On the web, browser-compatible storage mechanisms are used.

---

# File Sharing

Files are transferred using WebRTC DataChannels.

Dhambaal divides file data into **32 KB chunks**.

```text
File
 │
 ├── Chunk 1
 ├── Chunk 2
 ├── Chunk 3
 ├── ...
 └── Chunk N
        │
        ▼
    WebRTC DataChannel
        │
        ▼
      Receiver
        │
        ▼
   Reconstruct file
```

The receiver collects the chunks and reconstructs the complete payload after all chunks have arrived.

---

# Local-First Storage

Dhambaal keeps application data primarily on the user's device.

The current implementation uses:

* AsyncStorage for persistent application data
* GunDB as a local-only reactive data layer
* browser storage mechanisms for web-specific media data
* device file storage for mobile files and voice recordings

The current GunDB instance is initialized without configured Gun peers.

Therefore, GunDB is not being used as the project's network transport.

The local data model can be represented as:

```text
GunDB
   +
AsyncStorage
   +
Device / Browser Storage
```

---

# Decentralization Model

Dhambaal should be understood as a **decentralized communication architecture**, not as a completely serverless system.

The project's goal is to minimize dependence on a centralized message-storage backend while keeping communication as direct and user-controlled as practical.

```text
User Data
    │
    ▼
Stored locally on user device

Communication
    │
    ▼
Prefer direct P2P

NAT Traversal
    │
    ├── User-controlled TURN
    └── Dhambaal-provided TURN

Signaling
    │
    ▼
MQTT infrastructure
```

In other words:

**Users keep their application data locally, peers communicate directly whenever possible, and relay infrastructure is used when network conditions require it.**

Shared infrastructure still exists because peers need signaling and because TURN may be required to traverse restrictive networks.

---

# Security and Privacy

Dhambaal is designed around peer-to-peer communication and local data ownership.

WebRTC provides encrypted transport for its data and media channels.

However, the current implementation should **not be described as having a separately implemented application-layer end-to-end encryption protocol for chat messages** unless and until such a protocol is implemented and formally reviewed.

An important distinction is:

```text
WebRTC transport encryption
        ≠
Application-layer E2EE protocol
```

The MQTT control plane carries signaling information such as:

* offers
* answers
* ICE candidates
* presence information
* call coordination signals

Therefore the current privacy model is best described as:

> **Local-first, peer-to-peer communication using WebRTC for encrypted transport, with MQTT used for signaling and presence and TURN used when direct connectivity is unavailable.**

---

# Technology Stack

## Application

* React Native
* Expo
* Expo Router
* React Native Web
* TypeScript
* JavaScript

## Communication

* WebRTC
* `react-native-webrtc`
* MQTT
* STUN
* TURN
* ICE

## Local Data

* AsyncStorage
* GunDB
* Browser storage
* Device file system

## Native Features

* Notifee
* Expo Audio
* Expo Sharing
* QR code support
* Android background and notification integrations

---

# Project Structure

A simplified view of the current codebase:

```text
Dhambaal/
│
├── app/
│   ├── (tabs)/
│   │   ├── aniga.tsx
│   │   ├── dadka.tsx
│   │   ├── fariimaha.tsx
│   │   └── wicitaano.tsx
│   │
│   ├── fariin/
│   └── otherPages/
│
├── src/
│   ├── components/
│   │
│   ├── services/
│   │   ├── connection.js
│   │   ├── signaling.js
│   │   ├── iceServers.js
│   │   ├── messages.js
│   │   ├── calls.js
│   │   ├── callService.js
│   │   ├── contacts.js
│   │   ├── contactRequests.ts
│   │   ├── fileSharing.js
│   │   ├── voiceNotes.js
│   │   ├── voiceStorage.js
│   │   ├── storage.js
│   │   └── ...
│   │
│   └── theme/
│
├── plugins/
│   ├── withNotifee.js
│   └── withWebRTC.js
│
├── assets/
│
├── app.json
├── package.json
├── tsconfig.json
└── index.ts
```

---

# Running the Project

Install dependencies:

```bash
npm install
```

Start the development server:

```bash
npm start
```

Run on Android:

```bash
npm run android
```

Run on iOS:

```bash
npm run ios
```

Run on Web:

```bash
npm run web
```

---

# Network Testing

Because WebRTC behavior depends heavily on the underlying network environment, Dhambaal should be tested across multiple network conditions.

Useful test scenarios include:

```text
Wi-Fi ↔ Wi-Fi
Wi-Fi ↔ Mobile Data
Mobile Data ↔ Mobile Data
Different NAT environments
Restricted networks
VPN environments
Custom TURN available
Custom TURN unavailable
Default TURN available
Connection loss
Connection recovery
```

The actual network path should be verified through WebRTC connection statistics rather than inferred solely from configured ICE servers.

---

# Relay Management

Custom relay management is available from:

```text
Aniga
→ Xiriirka (Relay)
```

Users can manage their relay configurations and inspect locally recorded relay statistics.

The application records information such as:

```text
Successful attempts
Failed attempts
Last used time
```

These statistics are stored locally.

---

# Graduation Project

Dhambaal was developed as a **graduation project** as part of a Computer Science education.

The project combines implementation of:

```text
Peer-to-peer networking
WebRTC
NAT traversal
TURN infrastructure
MQTT signaling
Local-first storage
Cross-platform development
```

The project also explores how these technologies can be applied to communication needs within the Somali community.

---

# Project Team & Credits

Dhambaal was developed as a **graduation project** with the goal of building decentralized, peer-to-peer communication technology for the Somali community.

## Creator & Lead Developer

### Mubarak Abdikadir Jamac

**Known as:** `Mubra`

Creator and primary developer of Dhambaal.

Mubarak is responsible for the project's core architecture, implementation, integration, development, testing, and overall technical direction.

Dhambaal was developed as part of his **Computer Science / Software Engineering graduation project**.

---

## Contributor

### Safiyo Mohamed Mohamud

**Known as:** `Safa`

A project contributor who actively contributed to the development and improvement of Dhambaal.

Safiyo is recognized as the project's **main contributor** outside the lead developer.

---

## Project Helpers

### Zamzam Shucayb Maxamed

Supported the project during its development through assistance and collaboration.

### Ismael Yusuf Ibrahim

**Known as:** `Isma`

Supported the project during its development through assistance and collaboration.

---

Dhambaal is primarily the work of its creator and lead developer, with contributions and support from the people credited above.

---

# Design Philosophy

### Direct First

Prefer direct peer-to-peer communication whenever the network allows it.

### User Control

Allow users to bring their own TURN infrastructure.

### Resilience

Maintain built-in relay infrastructure so communication still has a fallback path.

### Local Ownership

Keep application data primarily on the user's device.

### Somali-First

Build communication technology **for the Somali community**, with Somali users treated as a first-class audience from the beginning.

### Cross-Platform

Make the communication experience available across web and mobile environments.

---

# Current Limitations

Dhambaal is an evolving project.

Current limitations include:

* WebRTC signaling still depends on MQTT infrastructure.
* TURN relays are required for some NAT environments.
* Custom and built-in TURN servers are supplied as ICE candidates rather than implemented as a strict sequential state machine.
* Large file transfer currently uses base64 data and in-memory chunk reconstruction, which can become expensive for very large files.
* Chat transport currently relies on WebRTC's encrypted transport rather than a separately implemented application-layer E2EE protocol.
* TURN credentials should not be embedded directly in public client source code in a production deployment.

---

# Production Security Notes

Before using the current repository as a production public communication service:

```text
1. Rotate any exposed TURN credentials.
2. Move sensitive relay credentials out of public client source code.
3. Use an appropriate TURN credential strategy.
4. Review MQTT broker exposure and signaling metadata.
5. Design and formally review an application-layer cryptographic protocol
   before making stronger E2EE claims.
6. Perform security testing across the complete WebRTC and signaling stack.
```

---

# Roadmap

Potential future improvements include:

* Strong application-layer end-to-end encryption
* Better TURN credential management
* Improved relay health scoring
* More explicit relay fallback control
* Efficient streaming for large files
* Better NAT diagnostics
* Additional signaling infrastructure options
* Self-hosted signaling support
* Improved background reliability
* Better network diagnostics
* Production observability
* Stronger identity and key management
* Expanded Somali localization and accessibility

---

# Why "Dhambaal"?

**Dhambaal** is a Somali word associated with a **message**.

The name reflects the project's central purpose: enabling people to communicate and exchange messages.

The technology behind Dhambaal is built around a simple idea:

> Communication technology should serve the people using it.

For Dhambaal, that starts with the **Somali community**.

---

# Project Vision

Dhambaal is more than a messaging experiment.

It is an exploration of how communication systems can be designed around:

```text
Somali community
       +
User control
       +
Local-first data
       +
Peer-to-peer communication
       +
Resilient connectivity
```

The long-term vision is to contribute to a stronger Somali technology ecosystem by building products that are not only available to Somali users, but are **designed specifically for Somali users from the beginning**.

---

# Project Status

Dhambaal is an evolving peer-to-peer communication project focused on:

```text
P2P communication
+
Local-first storage
+
Resilient connectivity
+
User-controlled relay infrastructure
+
Technology built for the Somali community
```

The project intentionally explores an alternative to conventional centralized chat architectures while remaining practical enough to operate across real-world network environments.

---

## License

See the [`LICENSE`](LICENSE) file for the project's license.
