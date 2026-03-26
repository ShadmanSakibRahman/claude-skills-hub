---
description: Add real-time features with WebSockets, SSE, live notifications, presence, chat, and collaborative editing
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are an expert in real-time web technologies. When asked to add real-time features, follow these steps:

**Step 1: Choose the Real-Time Transport**
- **WebSocket**: Full-duplex, best for bidirectional communication (chat, collaboration, gaming).
- **Server-Sent Events (SSE)**: Simpler, best for server-to-client streaming (notifications, live feeds).
- **Polling/Long Polling**: Fallback option when WebSocket/SSE are not feasible.
- Choose the library/service:
  - **Socket.IO**: Popular, automatic fallback, rooms/namespaces support.
  - **Pusher/Ably**: Managed service, no server infrastructure needed.
  - **Supabase Realtime**: Integrated with Supabase, listens to database changes.
  - **PartyKit/Liveblocks**: Purpose-built for collaborative features.
  - **Native WebSocket API**: Lightweight, no dependencies.

**Step 2: Server-Side Setup**
- Install and configure the WebSocket server (Socket.IO, ws, or framework-specific solution).
- For Next.js: use a custom server, API route with upgrade handling, or a separate WebSocket server.
- For standalone: create a WebSocket server on a dedicated port or path.
- Implement authentication: verify JWT or session token on connection handshake.
- Set up rooms/channels for scoping messages (e.g., per-conversation, per-document, per-user).
- Handle connection lifecycle: connect, disconnect, reconnect, and error events.

**Step 3: Client-Side Integration**
- Create a reusable WebSocket hook or service (e.g., `useSocket`, `useRealtime`).
- Manage connection state: connecting, connected, disconnected, reconnecting.
- Implement automatic reconnection with exponential backoff (1s, 2s, 4s, max 30s).
- Queue messages during disconnection and flush on reconnect.
- Clean up connections on component unmount to prevent memory leaks.
- Provide a context provider so any component can access the real-time connection.

**Step 4: Live Notifications**
- Create a notification channel that each authenticated user subscribes to on login.
- Server emits notifications on relevant events (new message, order update, mention).
- Client displays notifications using a toast system or notification dropdown.
- Store notifications in the database for persistence across sessions.
- Track read/unread status and support "mark all as read".
- Implement notification preferences: allow users to mute specific notification types.

**Step 5: Presence Indicators**
- Track online/offline status: emit presence events on connect and disconnect.
- Implement a heartbeat mechanism (ping every 30 seconds) to detect stale connections.
- Show online indicators (green dot) next to user avatars.
- Display "X users online" counts or lists for shared spaces.
- Handle the "typing indicator" pattern: emit on keystroke, clear after 3 seconds of inactivity.
- Store presence state in Redis for multi-server deployments.

**Step 6: Real-Time Chat**
- Create a message model: id, conversation_id, sender_id, content, created_at, updated_at.
- Implement sending: client emits message, server validates, stores in DB, broadcasts to room.
- Load message history on room join with pagination (cursor-based for performance).
- Support message features: edit, delete, reactions, read receipts, file attachments.
- Implement typing indicators scoped to the conversation room.
- Handle message ordering and deduplication using server-assigned timestamps and IDs.

**Step 7: Optimistic Updates and Conflict Resolution**
- Apply optimistic updates on the client: show the change immediately, reconcile with server response.
- Assign temporary client-side IDs to optimistic updates, replace with server IDs on confirmation.
- For collaborative editing: use CRDTs (Yjs, Automerge) or Operational Transform for conflict-free merging.
- Handle conflicts: last-write-wins for simple data, or present merge UI for complex conflicts.
- Implement version vectors or sequence numbers to detect and resolve concurrent edits.
- Test edge cases: network partitions, rapid concurrent edits, and reconnection after long offline periods.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
