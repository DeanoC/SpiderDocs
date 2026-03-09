# Assistant

This use case defines Spider as a unified home assistant that can act across the user's devices, accounts, and smart-home systems.

The target outcome is not a chatbot that answers questions in isolation. It is an agent that can understand intent, use connected systems, and complete real household tasks with minimal back-and-forth.

## Goal

Give the user one assistant that can:

- manage personal information such as email and calendar
- answer questions in voice or text
- discover and play media on the correct device
- control smart-home devices such as lights
- remember preferences across rooms and devices

## Primary Actors

- User: asks for help by voice or text from any supported device
- Spider primary brain: interprets the request, decides which capabilities are needed, and coordinates execution
- Device and service adapters: expose calendars, email, media services, TVs, speakers, lights, and other systems as usable capabilities

## Example Workflow

### Setup

1. User connects their devices, accounts, and smart-home systems.
2. Spider discovers available endpoints and records what each one can do.
3. User sets preferences such as preferred calendar, default TV, favorite streaming services, quiet hours, and notification rules.

### Day-to-day execution

1. User makes a request such as "Play something light on the living room TV and dim the lights."
2. Spider resolves the target room, devices, and services from user preferences and current availability.
3. Spider finds a suitable film or show, confirms only if confidence is low, then starts playback.
4. Spider adjusts the lights to the requested mood or a saved scene.
5. Spider reports completion by voice or notification and stays available for follow-up actions.

### Another example

1. User asks, "What is on my calendar tomorrow, and can you move my 3 PM if there is a clash?"
2. Spider reads the calendar, summarizes the day, identifies conflicts, and proposes a safe change.
3. Spider only sends updates or invitations once the user confirms the change.

## Required Venoms / Capabilities

### Identity and account access

Read and update email, calendar, contacts, and other personal systems with explicit permission boundaries.

### Device control

Control TVs, speakers, lights, and other smart devices, including room-level targeting and current-state discovery.

### Media discovery and playback

Search connected services, compare options, and start playback on the selected device.

### Voice input and output

Accept spoken requests and return spoken responses when the interaction surface supports it.

### Memory

Persist preferences, recent context, device mappings, and household routines in a form the agent can inspect and update.

### Notifications

Send confirmations, follow-ups, and exception reports to the appropriate device.

### Timers and scheduling

Support delayed actions, reminders, routines, and follow-up checks.

## Guardrails

- Do not send emails, messages, purchases, or calendar changes without confirmation unless the user has explicitly pre-approved that class of action.
- Do not control devices outside the permitted rooms, users, or schedules.
- Prefer clarification over guessing when identity, room, or target device is ambiguous.
- Keep household data private and scoped to the approved users and systems.

## Success Criteria

- The same request can be made from multiple devices and resolved consistently.
- Spider can complete common household tasks end-to-end, not just recommend actions.
- User preferences improve the quality of future actions without constant retraining.
- The user stays in control of high-impact actions while low-risk tasks feel automatic.
