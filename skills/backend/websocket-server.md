---
description: Set up WebSocket server with rooms, namespaces, auth, heartbeat, reconnection, message acknowledgment, and Redis scaling
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

You are a real-time communications expert. When the user asks you to set up or improve WebSocket functionality, follow these steps:

1. **Choose the library** based on the project:
   - **Socket.IO**: Full-featured with rooms, namespaces, auto-reconnection, fallback transports. Best for most applications.
   - **ws**: Lightweight, raw WebSocket. Best for performance-critical or simple use cases.
   - **WebSocket API (Python)**: Use `websockets` library or Django Channels.
   - Check existing dependencies and match the project's existing patterns.

2. **Set up the WebSocket server**:
   - Attach to the existing HTTP server (share the port) or create a dedicated server
   - Configure CORS to match the REST API's allowed origins
   - Set transport options: prefer WebSocket, fall back to long-polling if needed (Socket.IO)
   - Configure ping/pong intervals for connection health (pingInterval: 25000, pingTimeout: 20000)

3. **Implement authentication**:
   - Authenticate during the handshake, not after connection -- use middleware or the `connection` event
   - Extract JWT from the `auth` object or query params: `io.use((socket, next) => { verify(socket.handshake.auth.token) })`
   - Reject unauthenticated connections with a descriptive error
   - Attach user data to the socket object for use in event handlers
   - Handle token expiration: emit a `token-expired` event and allow re-authentication without disconnecting

4. **Design the event system**:
   - Use descriptive event names with namespacing: `chat:message`, `notification:new`, `user:typing`
   - Define a consistent message schema: `{ type, payload, timestamp, id }`
   - Create TypeScript interfaces or validation schemas for each event type
   - Document all events with their expected payload shapes

5. **Implement rooms and namespaces**:
   - Use namespaces for logically separate features: `/chat`, `/notifications`, `/live-updates`
   - Use rooms within namespaces for grouping: join user to their rooms on connection (`socket.join(userId)`, `socket.join(teamId)`)
   - Implement join/leave room handlers with authorization checks
   - Broadcast to rooms: `io.to(roomId).emit('event', data)` -- never broadcast to all sockets unless intended

6. **Add message acknowledgment**:
   - Use Socket.IO's callback acknowledgment: `socket.emit('message', data, (ack) => { ... })`
   - For ws library: implement a custom request-response pattern with message IDs
   - Track pending acknowledgments with timeouts; retry or alert if not acknowledged

7. **Implement heartbeat and reconnection**:
   - Server-side: configure ping interval; disconnect clients that don't respond to pings
   - Client-side: implement exponential backoff reconnection (1s, 2s, 4s, 8s, max 30s)
   - On reconnection: re-authenticate, rejoin rooms, and sync missed messages
   - Emit a `reconnected` event so the client can refresh stale data

8. **Handle horizontal scaling with Redis adapter**:
   - Install and configure `@socket.io/redis-adapter` with your Redis instance
   - This enables broadcasting across multiple server instances
   - Use Redis Streams or Pub/Sub for inter-server communication
   - Test with multiple server instances to verify cross-instance messaging works

9. **Implement presence tracking**:
   - Track online/offline status per user using Redis sets
   - Emit presence events on connect/disconnect: `user:online`, `user:offline`
   - Handle the disconnect event properly: use a short delay before marking offline (handles brief reconnections)
   - Provide an endpoint or event to query current online users in a room

10. **Add error handling and monitoring**:
    - Handle errors in event handlers with try/catch; emit an `error` event to the client with a safe message
    - Log connection, disconnection, and error events with socket ID and user ID
    - Track metrics: active connections, messages per second, room sizes, reconnection rate
    - Implement graceful shutdown: stop accepting new connections, close existing ones with a reason, wait for in-flight messages

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
