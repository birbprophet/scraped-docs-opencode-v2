---
url: https://opencode.ai/v2/docs/api
title: "API"
description: "OpenCode HTTP API reference and OpenAPI specification."
access_date: 2026-08-31T05:31:00.927Z
current_date: 2026-08-31T05:31:00.927Z
---

get `/api/health` Check server health

Report the owning server process and its application status.

Operation ID `v2.health.get`

### Responses

`200` ServiceHealth

`application/json` [ServiceHealth](#schema-ServiceHealth)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

get `/api/server` Get server information

Return the URLs that can be used to connect to this server.

Operation ID `v2.server.get`

### Responses

`200` Success

`application/json`

`object`

`urls`

`string[]` required

Items

`string`

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

get `/api/location` Get location

Resolve the requested location or the server default location.

Operation ID `v2.location.get`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Responses

`200` Location.Info

`application/json` [Location.InfoEncoded](#schema-Location.InfoEncoded)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

get `/api/agent` List agents

Retrieve currently registered agents.

Operation ID `v2.agent.list`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Responses

`200` Success

`application/json`

`object`

`location` [Location.InfoEncoded](#schema-Location.InfoEncoded)

`data`

`Agent.Info[]` required

Items [Agent.Info](#schema-Agent.Info)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

get `/api/agent/{agentID}` Get agent

Retrieve a single currently registered agent.

Operation ID `v2.agent.get`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `agentID` required | path | `string` | No description |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Responses

`200` Success

`application/json`

`object`

`location` [Location.InfoEncoded](#schema-Location.InfoEncoded)

`data` [Agent.Info](#schema-Agent.Info)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

`404` AgentNotFoundError

`application/json` [AgentNotFoundErrorEncoded](#schema-AgentNotFoundErrorEncoded)

get `/api/plugin` List plugins

Retrieve enabled server plugins and their current status.

Operation ID `v2.plugin.list`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Responses

`200` Success

`application/json`

`object`

`location` [Location.InfoEncoded](#schema-Location.InfoEncoded)

`data`

`Plugin.Info[]` required

Items [Plugin.Info](#schema-Plugin.Info)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

get `/api/session` List sessions

Retrieve sessions in the requested order. Items keep that order across pages; use cursor.next or cursor.previous to move through the ordered list.

Operation ID `v2.session.list`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `workspace` | query | `string \| null`  `string`  pattern ^wrk  or  `null` | No description |
| `limit` | query | `string \| null`  Maximum number of sessions to return. Defaults to the newest 50 sessions.  `string`  or  `null` | No description |
| `order` | query | `"asc" \| "desc" \| null`  Session order for the first page. Use desc for newest first or asc for oldest first.  `"asc" \| "desc"`  Values `"asc" \| "desc"`  or  `null` | No description |
| `search` | query | `string \| null`  `string`  or  `null` | No description |
| `parentID` | query | `string \| "null" \| null`  `string \| "null"`  Filter by parent session. Use null to return only root sessions.  `string`  pattern ^ses  or  `"null"`  Values `"null"`  or  `null` | No description |
| `directory` | query | `string \| null`  `string`  or  `null` | No description |
| `project` | query | `string \| null`  `string`  or  `null` | No description |
| `subpath` | query | `string \| null`  `string`  or  `null` | No description |
| `cursor` | query | `string \| null`  `string`  Opaque pagination cursor returned as cursor.previous or cursor.next in the previous response.  or  `null` | No description |

post `/api/session` Create session

Create a session at the requested location.

Operation ID `v2.session.create`

### Request body required

`application/json`

`object`

`id`

`string | null`

`string`

pattern ^ses

or

`null`

`title`

`string | null`

`string`

or

`null`

`agent`

`string | null`

`string`

or

`null`

`model`

`Model.Ref | null`

[Model.Ref](#schema-Model.Ref)

or

`null`

`location`

`Location.Ref | null`

[Location.Ref](#schema-Location.Ref)

or

`null`

`metadata`

`Session.Metadata | null`

[Session.Metadata](#schema-Session.Metadata)

or

`null`

### Responses

`200` Success

`application/json`

`object`

`data` [Session.Info](#schema-Session.Info)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

get `/api/session/stats` Get session statistics

Aggregate local session activity, usage, and tool reliability for a time range.

Operation ID `v2.session.stats`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `from` | query | `string \| null`  `string`  or  `null` | No description |
| `to` | query | `string \| null`  `string`  or  `null` | No description |
| `project` | query | `string \| null`  `string`  or  `null` | No description |
| `timezone` | query | `string \| null`  `string`  or  `null` | No description |
| `tools` | query | `"none" \| "summary" \| "detail" \| null`  `"none" \| "summary" \| "detail"`  Values `"none" \| "summary" \| "detail"`  or  `null` | No description |

post `/api/session/import` Import session

Import a projected session transcript at the requested location. If parentID is supplied, the parent session must already exist; import parents before children.

Operation ID `v2.session.import`

### Responses

`200` Success

`application/json`

`object`

`data` [Session.Info](#schema-Session.Info)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

`404` SessionNotFoundError

`application/json` [SessionNotFoundErrorEncoded](#schema-SessionNotFoundErrorEncoded)

`409` ConflictError

`application/json` [ConflictErrorEncoded](#schema-ConflictErrorEncoded)

get `/api/session/{sessionID}/export` Export session

Export a complete projected session transcript.

Operation ID `v2.session.export`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string`  pattern ^ses | No description |
| `sanitize` | query | `"true" \| "false" \| null`  `"true" \| "false"`  Values `"true" \| "false"`  or  `null` | No description |

### Responses

`200` Success

`application/json`

`object`

`data` [SessionTransfer.Data](#schema-SessionTransfer.Data)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

`404` SessionNotFoundError

`application/json` [SessionNotFoundErrorEncoded](#schema-SessionNotFoundErrorEncoded)

`500` UnknownError

`application/json` [UnknownErrorEncoded](#schema-UnknownErrorEncoded)

get `/api/session/active` List active sessions

Retrieve foreground Session drains currently owned by this OpenCode process. Sessions absent from the result are inactive.

Operation ID `v2.session.active`

### Responses

`200` Success

`application/json`

`object`

`data`

`object` required

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

get `/api/session/{sessionID}` Get session

Retrieve a session by ID.

Operation ID `v2.session.get`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string`  pattern ^ses | No description |

### Responses

`200` Success

`application/json`

`object`

`data` [Session.Info](#schema-Session.Info)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

`404` SessionNotFoundError

`application/json` [SessionNotFoundErrorEncoded](#schema-SessionNotFoundErrorEncoded)

delete `/api/session/{sessionID}` Delete session

Delete a session and its child sessions.

Operation ID `v2.session.remove`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string`  pattern ^ses | No description |

post `/api/session/{sessionID}/fork` Fork session

Create a child session by copying projected history through or before a message boundary.

Operation ID `v2.session.fork`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string`  pattern ^ses | No description |

### Request body required

`application/json`

`object`

`boundary` [Session.ForkRequestBoundary](#schema-Session.ForkRequestBoundary)

post `/api/session/{sessionID}/agent` Switch session agent

Switch the agent used by subsequent provider turns.

Operation ID `v2.session.switchAgent`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string`  pattern ^ses | No description |

### Request body required

`application/json`

`object`

`agent`

`string` required

post `/api/session/{sessionID}/model` Switch session model

Switch the model used by subsequent provider turns.

Operation ID `v2.session.switchModel`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string`  pattern ^ses | No description |

### Request body required

`application/json`

`object`

`model` [Model.Ref](#schema-Model.Ref)

post `/api/session/{sessionID}/rename` Rename session

Update the session title.

Operation ID `v2.session.rename`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string`  pattern ^ses | No description |

### Request body required

`application/json`

`object`

`title`

`string` required

post `/api/session/{sessionID}/move` Move session

Move a session to another project directory, optionally transferring local changes.

Operation ID `v2.session.move`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string`  pattern ^ses | No description |

### Request body required

`application/json`

`object`

`directory`

`string` required

`workspaceID`

`string`

pattern ^wrk

`delivery`

`Session.Inbox.Delivery | null`

[Session.Inbox.Delivery](#schema-Session.Inbox.Delivery)

or

`null`

post `/api/session/{sessionID}/prompt` Send message

Durably admit one session input and schedule agent-loop execution unless resume is false.

Operation ID `v2.session.prompt`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string`  pattern ^ses | No description |

### Request body required

`application/json`

`object`

`id`

`string | null`

`string`

pattern ^msg\_

or

`null`

`text`

`string` required

`files`

`PromptInput.FileAttachment[]`

Items [PromptInput.FileAttachment](#schema-PromptInput.FileAttachment)

`agents`

`Prompt.AgentAttachment[]`

Items [Prompt.AgentAttachment](#schema-Prompt.AgentAttachment)

`skills`

`PromptInput.SkillAttachment[]`

Items [PromptInput.SkillAttachment](#schema-PromptInput.SkillAttachment)

`metadata`

`object`

`delivery`

`Session.Inbox.Delivery | null`

[Session.Inbox.Delivery](#schema-Session.Inbox.Delivery)

or

`null`

`resume`

`boolean | null`

`boolean`

or

`null`

post `/api/session/{sessionID}/command` Run command

Execute a slash command callback immediately.

Operation ID `v2.session.command`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string`  pattern ^ses | No description |

post `/api/session/{sessionID}/skill` Activate skill

Activate a skill for a session by appending a skill message and resuming execution.

Operation ID `v2.session.skill`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string`  pattern ^ses | No description |

### Request body required

`application/json`

`object`

`id`

`string | null`

`string`

pattern ^msg\_

or

`null`

`skill`

`string` required

`resume`

`boolean | null`

`boolean`

or

`null`

post `/api/session/{sessionID}/synthetic` Add synthetic message

Durably admit synthetic session input and schedule execution unless resume is false.

Operation ID `v2.session.synthetic`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string`  pattern ^ses | No description |

### Request body required

`application/json`

`object`

`id`

`string | null`

`string`

pattern ^msg\_

or

`null`

`text`

`string` required

`description`

`string | null`

`string`

or

`null`

`metadata`

`object`

`delivery`

`Session.Inbox.Delivery | null`

[Session.Inbox.Delivery](#schema-Session.Inbox.Delivery)

or

`null`

`resume`

`boolean | null`

`boolean`

or

`null`

post `/api/session/{sessionID}/shell` Run shell command

Execute one shell command in the session's working directory. Emits a shell.started event before execution and a shell.ended event with the merged output after.

Operation ID `v2.session.shell`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string`  pattern ^ses | No description |

### Request body required

`application/json`

`object`

`id`

`string | null`

`string`

pattern ^evt\_

or

`null`

`command`

`string` required

post `/api/session/{sessionID}/compact` Compact session

Durably admit a session compaction request. Steers by default: it runs at the next step boundary instead of waiting behind queued prompts.

Operation ID `v2.session.compact`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string`  pattern ^ses | No description |

### Request body required

`application/json`

`object`

`id`

`string | null`

`string`

pattern ^msg\_

or

`null`

`delivery`

`Session.Inbox.Delivery | null`

[Session.Inbox.Delivery](#schema-Session.Inbox.Delivery)

or

`null`

post `/api/session/{sessionID}/wait` Wait for session

Wait for a session agent loop to become idle.

Operation ID `v2.session.wait`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string`  pattern ^ses | No description |

post `/api/session/{sessionID}/revert/stage` Stage session revert

Stage or move a reversible session boundary and optionally apply its file changes.

Operation ID `v2.session.revert.stage`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string`  pattern ^ses | No description |

### Request body required

`application/json`

`object`

`messageID`

`string` required

pattern ^msg\_

`files`

`boolean | null`

`boolean`

or

`null`

post `/api/session/{sessionID}/revert/clear` Clear staged revert

Operation ID `v2.session.revert.clear`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string`  pattern ^ses | No description |

post `/api/session/{sessionID}/revert/commit` Commit staged revert

Operation ID `v2.session.revert.commit`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string`  pattern ^ses | No description |

get `/api/session/{sessionID}/context` Get session context

Retrieve the active context messages for a session (all messages after the last compaction).

Operation ID `v2.session.context`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string`  pattern ^ses | No description |

### Responses

`200` Success

`application/json`

`object`

`data`

`Session.Message.Info[]` required

Items [Session.Message.Info](#schema-Session.Message.Info)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

`404` SessionNotFoundError

`application/json` [SessionNotFoundErrorEncoded](#schema-SessionNotFoundErrorEncoded)

`500` UnknownError

`application/json` [UnknownErrorEncoded](#schema-UnknownErrorEncoded)

get `/api/session/{sessionID}/inbox` List session inbox

List durable enqueued session work not yet delivered, ordered by enqueue sequence. Includes user, synthetic, compaction, and move items.

Operation ID `v2.session.inbox.list`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string`  pattern ^ses | No description |

### Responses

`200` Success

`application/json`

`object`

`data`

`Session.Inbox.Info[]` required

Items [Session.Inbox.Info](#schema-Session.Inbox.Info)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

`404` SessionNotFoundError

`application/json` [SessionNotFoundErrorEncoded](#schema-SessionNotFoundErrorEncoded)

delete `/api/session/{sessionID}/inbox/{inboxID}` Cancel inbox input

Cancel an inbox item that has not yet been delivered.

Operation ID `v2.session.inbox.cancel`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string`  pattern ^ses | No description |
| `inboxID` required | path | `string`  pattern ^msg\_ | No description |

### Responses

`204` <No Content>

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

`404` SessionNotFoundError

`application/json` [SessionNotFoundErrorEncoded](#schema-SessionNotFoundErrorEncoded)

`409` ConflictError

`application/json` [ConflictErrorEncoded](#schema-ConflictErrorEncoded)

post `/api/session/{sessionID}/inbox/{inboxID}/steer` Steer queued item

Change a queued inbox item to steer delivery and wake session execution.

Operation ID `v2.session.inbox.steer`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string`  pattern ^ses | No description |
| `inboxID` required | path | `string`  pattern ^msg\_ | No description |

### Responses

`204` <No Content>

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

`404` SessionNotFoundError

`application/json` [SessionNotFoundErrorEncoded](#schema-SessionNotFoundErrorEncoded)

`409` ConflictError

`application/json` [ConflictErrorEncoded](#schema-ConflictErrorEncoded)

post `/api/session/{sessionID}/inbox/{inboxID}/queue` Queue steered item

Change a steered inbox item to queued delivery.

Operation ID `v2.session.inbox.queue`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string`  pattern ^ses | No description |
| `inboxID` required | path | `string`  pattern ^msg\_ | No description |

### Responses

`204` <No Content>

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

`404` SessionNotFoundError

`application/json` [SessionNotFoundErrorEncoded](#schema-SessionNotFoundErrorEncoded)

`409` ConflictError

`application/json` [ConflictErrorEncoded](#schema-ConflictErrorEncoded)

get `/api/session/{sessionID}/instructions/entries` List instruction entries

List API-managed instruction entries attached to the session.

Operation ID `v2.session.instructions.entry.list`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string`  pattern ^ses | No description |

put `/api/session/{sessionID}/instructions/entries/{key}` Put instruction entry

Attach or replace one durable instruction entry. Changes announce as updates at the next step boundary.

Operation ID `v2.session.instructions.entry.put`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string`  pattern ^ses | No description |
| `key` required | path | [InstructionEntry.Key](#schema-InstructionEntry.Key) | No description |

### Request body required

`application/json`

`object`

`value`

`object` required

delete `/api/session/{sessionID}/instructions/entries/{key}` Remove instruction entry

Remove one instruction entry; the removal is announced to the model at the next step boundary.

Operation ID `v2.session.instructions.entry.remove`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string`  pattern ^ses | No description |
| `key` required | path | [InstructionEntry.Key](#schema-InstructionEntry.Key) | No description |

post `/api/session/{sessionID}/generate` Generate text from session context

Generate transient text from the current session context without mutating session history.

Operation ID `v2.session.generate`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string`  pattern ^ses | No description |

### Request body required

`application/json`

`object`

`prompt`

`string` required

get `/api/experimental/session/{sessionID}/log` Read the session log

Experimental durable session event log. Reads events after an exclusive aggregate sequence and continues with live events when follow=true.

Operation ID `v2.session.log`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string`  pattern ^ses | No description |
| `after` | query | `string \| null`  `string`  or  `null` | No description |
| `follow` | query | `"true" \| "false" \| null`  `"true" \| "false"`  Values `"true" \| "false"`  or  `null` | No description |

post `/api/session/{sessionID}/interrupt` Interrupt session execution

Interrupt active execution owned by this OpenCode process. Returns interrupted=true when an active execution was interrupted and false for the idle no-op. When continue=true, execution resumes pending steering input and next-in-line control items (manual compaction, moves) while queued prompts remain parked.

Operation ID `v2.session.interrupt`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string`  pattern ^ses | No description |
| `continue` | query | `"true" \| "false" \| null`  `"true" \| "false"`  Values `"true" \| "false"`  or  `null` | No description |

post `/api/session/{sessionID}/background` Background blocking session tools

Move active foreground backgroundable tools for this session into background observation. Idle requests are a no-op.

Operation ID `v2.session.background`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string`  pattern ^ses | No description |

get `/api/session/{sessionID}/message/{messageID}` Get session message

Retrieve one projected message owned by the Session.

Operation ID `v2.session.message`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string`  pattern ^ses | No description |
| `messageID` required | path | `string`  pattern ^msg\_ | No description |

patch `/api/session/{sessionID}/message/{messageID}` Update assistant message content

Replace the content of a completed assistant message in an idle session.

Operation ID `v2.session.messageUpdate`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string`  pattern ^ses | No description |
| `messageID` required | path | `string`  pattern ^msg\_ | No description |

### Request body required

`application/json`

`object`

`content`

`Session.Message.Assistant.Text | Session.Message.Assistant.Reasoning | Session.Message.Assistant.Tool[]` required

put `/api/session/{sessionID}/environment` Set session environment

Replace the process environment used by local shell commands for this session.

Operation ID `v2.session.environment`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string`  pattern ^ses | No description |

### Request body required

`application/json`

`object`

`variables`

`object` required

Additional properties

`string`

### Responses

`204` <No Content>

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

`404` SessionNotFoundError

`application/json` [SessionNotFoundErrorEncoded](#schema-SessionNotFoundErrorEncoded)

post `/api/session/{sessionID}/view` View session

Mark the idle transition observed by the viewer as viewed.

Operation ID `v2.session.view`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string`  pattern ^ses | No description |

### Request body required

`application/json`

`object`

`idle`

`integer` required

min 0

### Responses

`204` <No Content>

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

`404` SessionNotFoundError

`application/json` [SessionNotFoundErrorEncoded](#schema-SessionNotFoundErrorEncoded)

get `/api/session/{sessionID}/message` Get session messages

Retrieve projected messages for a session. Items keep the requested order across pages; use cursor.next or cursor.previous to move through the ordered timeline.

Operation ID `v2.message.list`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string`  pattern ^ses | No description |
| `limit` | query | `string \| null`  Maximum number of messages to return. When omitted, the endpoint returns its default page size.  `string`  or  `null` | No description |
| `order` | query | `"asc" \| "desc" \| null`  Message order for the first page. Use desc for newest first or asc for oldest first.  `"asc" \| "desc"`  Values `"asc" \| "desc"`  or  `null` | No description |
| `cursor` | query | `string \| null`  `string`  Opaque pagination cursor returned as cursor.previous or cursor.next in the previous response. Do not combine with order.  or  `null` | No description |

get `/api/model` List models

Retrieve the current snapshot of available models ordered by release date. The snapshot may precede initial plugin settlement.

Operation ID `v2.model.list`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Responses

`200` Success

`application/json`

`object`

`location` [Location.InfoEncoded](#schema-Location.InfoEncoded)

`data`

`Model.Info[]` required

Items [Model.Info](#schema-Model.Info)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

`503` ServiceUnavailableError

`application/json` [ServiceUnavailableErrorEncoded](#schema-ServiceUnavailableErrorEncoded)

get `/api/model/default` Get default model

Retrieve the model used when a session has no explicit model selection.

Operation ID `v2.model.default`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

post `/api/generate` Generate text

Run one stateless model generation using the server's base configuration and return the assistant text. Uses the base configuration's default model when none is specified.

Operation ID `v2.generate.text`

### Request body required

`application/json`

`object`

`prompt`

`string` required

`model`

`Model.Ref | null`

[Model.Ref](#schema-Model.Ref)

or

`null`

get `/api/provider` List providers

Retrieve active AI providers so clients can show provider availability and configuration.

Operation ID `v2.provider.list`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Responses

`200` Success

`application/json`

`object`

`location` [Location.InfoEncoded](#schema-Location.InfoEncoded)

`data`

`Provider.Info[]` required

Items [Provider.Info](#schema-Provider.Info)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

`503` ServiceUnavailableError

`application/json` [ServiceUnavailableErrorEncoded](#schema-ServiceUnavailableErrorEncoded)

get `/api/provider/{providerID}` Get provider

Retrieve a single AI provider so clients can inspect its availability and endpoint settings.

Operation ID `v2.provider.get`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `providerID` required | path | `string` | No description |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Responses

`200` Success

`application/json`

`object`

`location` [Location.InfoEncoded](#schema-Location.InfoEncoded)

`data` [Provider.Info](#schema-Provider.Info)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

`404` ProviderNotFoundError

`application/json` [ProviderNotFoundErrorEncoded](#schema-ProviderNotFoundErrorEncoded)

`503` ServiceUnavailableError

`application/json` [ServiceUnavailableErrorEncoded](#schema-ServiceUnavailableErrorEncoded)

get `/api/integration` List integrations

Retrieve available integrations and their authentication methods.

Operation ID `v2.integration.list`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Responses

`200` Success

`application/json`

`object`

`location` [Location.InfoEncoded](#schema-Location.InfoEncoded)

`data`

`Integration.Info[]` required

Items [Integration.Info](#schema-Integration.Info)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

get `/api/integration/{integrationID}` Get integration

Retrieve one integration and its authentication methods.

Operation ID `v2.integration.get`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `integrationID` required | path | `string` | No description |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

post `/api/experimental/integration/wellknown` Add wellknown integration

Discover and persist an experimental wellknown integration source.

Operation ID `v2.experimental.integration.wellknown.add`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Request body required

`application/json`

`object`

`url`

`string` required

post `/api/integration/{integrationID}/connect/key` Connect with key

Run a key authentication method and store the resulting credential.

Operation ID `v2.integration.connect.key`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `integrationID` required | path | `string` | No description |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Request body required

`application/json`

`object`

`key`

`string` required

`answer`

`Form.Answer | null`

[Form.Answer](#schema-Form.Answer)

or

`null`

`label`

`string | null`

`string`

or

`null`

post `/api/integration/{integrationID}/connect/oauth` Begin OAuth connection

Start an OAuth attempt and return the authorization details.

Operation ID `v2.integration.oauth.connect`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `integrationID` required | path | `string` | No description |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Request body required

`application/json`

`object`

`methodID`

`string` required

`answer`

`Form.Answer | null`

[Form.Answer](#schema-Form.Answer)

or

`null`

`label`

`string | null`

`string`

or

`null`

get `/api/integration/{integrationID}/connect/oauth/{attemptID}` Get OAuth attempt status

Poll the current status of an OAuth attempt.

Operation ID `v2.integration.oauth.status`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `integrationID` required | path | `string` | No description |
| `attemptID` required | path | `string` | No description |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Responses

`200` Success

`application/json`

`object`

`location` [Location.InfoEncoded](#schema-Location.InfoEncoded)

`data` [Integration.AttemptStatus](#schema-Integration.AttemptStatus)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

delete `/api/integration/{integrationID}/connect/oauth/{attemptID}` Cancel OAuth connection

Cancel an OAuth attempt and release its resources.

Operation ID `v2.integration.oauth.cancel`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `integrationID` required | path | `string` | No description |
| `attemptID` required | path | `string` | No description |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Responses

`204` <No Content>

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

post `/api/integration/{integrationID}/connect/oauth/{attemptID}/complete` Complete OAuth connection

Complete a code-based OAuth attempt and store the resulting credential.

Operation ID `v2.integration.oauth.complete`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `integrationID` required | path | `string` | No description |
| `attemptID` required | path | `string` | No description |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Request body required

`application/json`

`object`

`code`

`string | null`

`string`

or

`null`

post `/api/integration/{integrationID}/connect/command` Begin command connection

Start a command authentication attempt.

Operation ID `v2.integration.command.connect`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `integrationID` required | path | `string` | No description |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Request body required

`application/json`

`object`

`methodID`

`string` required

`label`

`string | null`

`string`

or

`null`

get `/api/integration/{integrationID}/connect/command/{attemptID}` Get command attempt status

Poll the current status and output of a command authentication attempt.

Operation ID `v2.integration.command.status`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `integrationID` required | path | `string` | No description |
| `attemptID` required | path | `string` | No description |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Responses

`200` Success

`application/json`

`object`

`location` [Location.InfoEncoded](#schema-Location.InfoEncoded)

`data` [Integration.CommandAttemptStatus](#schema-Integration.CommandAttemptStatus)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

delete `/api/integration/{integrationID}/connect/command/{attemptID}` Cancel command connection

Cancel a command authentication attempt and terminate its process.

Operation ID `v2.integration.command.cancel`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `integrationID` required | path | `string` | No description |
| `attemptID` required | path | `string` | No description |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Responses

`204` <No Content>

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

get `/api/mcp` List MCP servers

Retrieve configured MCP servers and their connection status.

Operation ID `v2.mcp.list`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Responses

`200` Success

`application/json`

`object`

`location` [Location.InfoEncoded](#schema-Location.InfoEncoded)

`data`

`Mcp.Server[]` required

Items [Mcp.Server](#schema-Mcp.Server)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

put `/api/mcp/{server}` Add MCP server

Add an MCP server at runtime or replace an existing one, connecting it immediately.

Operation ID `v2.mcp.add`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `server` required | path | `string` | No description |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Request body required

### Responses

`204` <No Content>

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

delete `/api/mcp/{server}` Remove MCP server

Stop an MCP server and remove it from the runtime set until restart.

Operation ID `v2.mcp.remove`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `server` required | path | `string` | No description |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Responses

`204` <No Content>

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

`404` McpServerNotFoundError

`application/json` [McpServerNotFoundErrorEncoded](#schema-McpServerNotFoundErrorEncoded)

post `/api/mcp/{server}/connect` Connect MCP server

Connect an MCP server at runtime, overriding a disabled configuration until restart.

Operation ID `v2.mcp.connect`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `server` required | path | `string` | No description |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Responses

`204` <No Content>

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

`404` McpServerNotFoundError

`application/json` [McpServerNotFoundErrorEncoded](#schema-McpServerNotFoundErrorEncoded)

post `/api/mcp/{server}/disconnect` Disconnect MCP server

Disconnect an MCP server at runtime, removing its tools until reconnected.

Operation ID `v2.mcp.disconnect`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `server` required | path | `string` | No description |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Responses

`204` <No Content>

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

`404` McpServerNotFoundError

`application/json` [McpServerNotFoundErrorEncoded](#schema-McpServerNotFoundErrorEncoded)

get `/api/mcp/resource` List MCP resources

Retrieve resources and resource templates from connected MCP servers.

Operation ID `v2.mcp.resource.catalog`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Responses

`200` Success

`application/json`

`object`

`location` [Location.InfoEncoded](#schema-Location.InfoEncoded)

`data` [Mcp.ResourceCatalog](#schema-Mcp.ResourceCatalog)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

patch `/api/credential/{credentialID}` Update credential

Update a stored credential label.

Operation ID `v2.credential.update`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `credentialID` required | path | `string` | No description |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Request body required

`application/json`

`object`

`label`

`string` required

### Responses

`204` <No Content>

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

delete `/api/credential/{credentialID}` Remove credential

Remove a stored integration credential.

Operation ID `v2.credential.remove`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `credentialID` required | path | `string` | No description |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Responses

`204` <No Content>

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

post `/api/credential/{credentialID}/activate` Activate credential

Activate a stored integration credential.

Operation ID `v2.credential.activate`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `credentialID` required | path | `string` | No description |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Responses

`204` <No Content>

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

get `/api/project` List projects patch `/api/project/{projectID}` Update project

Update project display metadata and workspace commands.

Operation ID `v2.project.update`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `projectID` required | path | `string` | No description |

### Responses

`200` Project

`application/json` [Project](#schema-Project)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

`404` ProjectNotFoundError

`application/json` [ProjectNotFoundErrorEncoded](#schema-ProjectNotFoundErrorEncoded)

get `/api/project/current` Get current project

Resolve the project for the requested location.

Operation ID `v2.project.current`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Responses

`200` Project.Current

`application/json` [Project.Current](#schema-Project.Current)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

get `/api/form/request` List pending form requests

Retrieve pending forms for a location.

Operation ID `v2.form.request.list`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Responses

`200` Success

`application/json`

`object`

`location` [Location.InfoEncoded](#schema-Location.InfoEncoded)

`data`

`Form.Info[]` required

Items [Form.Info](#schema-Form.Info)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

get `/api/session/{sessionID}/form` List session forms

Retrieve pending forms for a session.

Operation ID `v2.session.form.list`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string` | No description |

### Responses

`200` Success

`application/json`

`object`

`data`

`Form.Info[]` required

Items [Form.Info](#schema-Form.Info)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

`404` SessionNotFoundError

`application/json` [SessionNotFoundErrorEncoded](#schema-SessionNotFoundErrorEncoded)

post `/api/session/{sessionID}/form` Create session form

Create a form for a session.

Operation ID `v2.session.form.create`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string` | No description |

### Request body required

`application/json` [Form.CreatePayload](#schema-Form.CreatePayload)

get `/api/session/{sessionID}/form/{formID}` Get session form

Retrieve a form for a session.

Operation ID `v2.session.form.get`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string` | No description |
| `formID` required | path | `string`  pattern ^frm\_ | No description |

get `/api/session/{sessionID}/form/{formID}/state` Get form state

Retrieve the current state for a form.

Operation ID `v2.session.form.state`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string` | No description |
| `formID` required | path | `string`  pattern ^frm\_ | No description |

post `/api/session/{sessionID}/form/{formID}/reply` Reply to form

Submit an answer to a pending form.

Operation ID `v2.session.form.reply`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string` | No description |
| `formID` required | path | `string`  pattern ^frm\_ | No description |

### Request body required

`application/json` [Form.Reply](#schema-Form.Reply)

post `/api/session/{sessionID}/form/{formID}/cancel` Cancel form

Cancel a pending form.

Operation ID `v2.session.form.cancel`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string` | No description |
| `formID` required | path | `string`  pattern ^frm\_ | No description |

get `/api/permission/request` List pending permission requests

Retrieve pending permission requests for a location.

Operation ID `v2.permission.request.list`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Responses

`200` Success

`application/json`

`object`

`location` [Location.InfoEncoded](#schema-Location.InfoEncoded)

`data`

`Permission.Request[]` required

Items [Permission.Request](#schema-Permission.Request)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

get `/api/permission/saved` List saved permissions

Retrieve saved permissions, optionally filtered by project.

Operation ID `v2.permission.saved.list`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `projectID` | query | `string \| null`  `string`  or  `null` | No description |

### Responses

`200` Success

`application/json`

`object`

`data`

`PermissionSaved.Info[]` required

Items [PermissionSaved.Info](#schema-PermissionSaved.Info)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

delete `/api/permission/saved/{id}` Remove saved permission

Remove a saved permission by ID.

Operation ID `v2.permission.saved.remove`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `id` required | path | `string` | No description |

### Responses

`204` <No Content>

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

get `/api/session/{sessionID}/permission` List session permission requests

Retrieve pending permission requests owned by a session.

Operation ID `v2.session.permission.list`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string`  pattern ^ses | No description |

### Responses

`200` Success

`application/json`

`object`

`data`

`Permission.Request[]` required

Items [Permission.Request](#schema-Permission.Request)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

`404` SessionNotFoundError

`application/json` [SessionNotFoundErrorEncoded](#schema-SessionNotFoundErrorEncoded)

post `/api/session/{sessionID}/permission` Create permission request

Evaluate and, when approval is required, create a permission request for a session.

Operation ID `v2.session.permission.create`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string`  pattern ^ses | No description |

### Request body required

`application/json`

`object`

`id`

`string | null`

`string`

pattern ^per

or

`null`

`action`

`string` required

`resources`

`string[]` required

Items

`string`

`save`

`string[]`

Items

`string`

`metadata`

`object`

`source` [Permission.Source](#schema-Permission.Source)

`agent`

`string | null`

`string`

or

`null`

get `/api/session/{sessionID}/permission/{requestID}` Get permission request

Retrieve a pending permission request owned by a session.

Operation ID `v2.session.permission.get`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string`  pattern ^ses | No description |
| `requestID` required | path | `string`  pattern ^per | No description |

post `/api/session/{sessionID}/permission/{requestID}/reply` Reply to pending permission request

Respond to a pending permission request owned by a session.

Operation ID `v2.session.permission.reply`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string`  pattern ^ses | No description |
| `requestID` required | path | `string`  pattern ^per | No description |

### Request body required

`application/json`

`object`

`reply` [Permission.Reply](#schema-Permission.Reply)

`message`

`string | null`

`string`

or

`null`

get `/api/fs/read/*` Read file

Serve one file relative to the requested location.

Operation ID `v2.fs.read`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Responses

`200` Success

`application/octet-stream`

`string<binary>`

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

get `/api/fs/list` List directory

List direct children of one directory relative to the requested location.

Operation ID `v2.fs.list`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |
| `path` | query | `string \| null`  `string`  or  `null` | No description |

### Responses

`200` Success

`application/json`

`object`

`location` [Location.InfoEncoded](#schema-Location.InfoEncoded)

`data`

`FileSystem.Entry[]` required

Items [FileSystem.Entry](#schema-FileSystem.Entry)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

get `/api/fs/find` Find files

Find recursively ranked filesystem entries relative to the requested location.

Operation ID `v2.fs.find`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |
| `query` required | query | `string` | No description |
| `type` | query | `"file" \| "directory"`  Values `"file" \| "directory"` | No description |
| `limit` | query | `string \| null`  `string`  or  `null` | No description |

### Responses

`200` Success

`application/json`

`object`

`location` [Location.InfoEncoded](#schema-Location.InfoEncoded)

`data`

`FileSystem.Entry[]` required

Items [FileSystem.Entry](#schema-FileSystem.Entry)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

get `/api/command` List commands

Retrieve currently registered commands.

Operation ID `v2.command.list`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Responses

`200` Success

`application/json`

`object`

`location` [Location.InfoEncoded](#schema-Location.InfoEncoded)

`data`

`Command.Info[]` required

Items [Command.Info](#schema-Command.Info)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

get `/api/skill` List skills

Retrieve currently registered skills.

Operation ID `v2.skill.list`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Responses

`200` Success

`application/json`

`object`

`location` [Location.InfoEncoded](#schema-Location.InfoEncoded)

`data`

`Skill.Info[]` required

Items [Skill.Info](#schema-Skill.Info)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

post `/api/rpc/{rpcID}/{method}` Call a plugin RPC

Dispatch a method to the currently registered RPC at the requested location.

Operation ID `v2.rpc.call`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `rpcID` required | path | `string` | No description |
| `method` required | path | `string` | No description |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Request body required

`application/json` [Rpc.Input](#schema-Rpc.Input)

get `/api/event` Subscribe to events

get `/api/pty` List PTY sessions

List PTY sessions for a location, including exited sessions retained until removal.

Operation ID `v2.pty.list`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Responses

`200` Success

`application/json`

`object`

`location` [Location.InfoEncoded](#schema-Location.InfoEncoded)

`data`

`Pty[]` required

Items [Pty](#schema-Pty)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

post `/api/pty` Create PTY session

Create a pseudo-terminal session for a location.

Operation ID `v2.pty.create`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Request body required

`application/json`

`object`

`command`

`string`

`args`

`string[]`

Items

`string`

`cwd`

`string`

`title`

`string`

`env`

`object`

Additional properties

`string`

### Responses

`200` Success

`application/json`

`object`

`location` [Location.InfoEncoded](#schema-Location.InfoEncoded)

`data` [Pty](#schema-Pty)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

get `/api/pty/{ptyID}` Get PTY session

Get one PTY session, including its exit code once exited.

Operation ID `v2.pty.get`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `ptyID` required | path | `string`  pattern ^pty | No description |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Responses

`200` Success

`application/json`

`object`

`location` [Location.InfoEncoded](#schema-Location.InfoEncoded)

`data` [Pty](#schema-Pty)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

`404` PtyNotFoundError

`application/json` [PtyNotFoundErrorEncoded](#schema-PtyNotFoundErrorEncoded)

put `/api/pty/{ptyID}` Update PTY session

Update the title or viewport size of one PTY session.

Operation ID `v2.pty.update`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `ptyID` required | path | `string`  pattern ^pty | No description |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Request body required

`application/json`

`object`

`title`

`string`

`size`

`object`

`rows`

`integer` required

\> 0

`cols`

`integer` required

\> 0

### Responses

`200` Success

`application/json`

`object`

`location` [Location.InfoEncoded](#schema-Location.InfoEncoded)

`data` [Pty](#schema-Pty)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

`404` PtyNotFoundError

`application/json` [PtyNotFoundErrorEncoded](#schema-PtyNotFoundErrorEncoded)

delete `/api/pty/{ptyID}` Remove PTY session

Terminate and remove one PTY session.

Operation ID `v2.pty.remove`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `ptyID` required | path | `string`  pattern ^pty | No description |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Responses

`204` <No Content>

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

`404` PtyNotFoundError

`application/json` [PtyNotFoundErrorEncoded](#schema-PtyNotFoundErrorEncoded)

post `/api/pty/{ptyID}/connect-token` Create PTY WebSocket token

Create a short-lived single-use ticket for opening a PTY WebSocket connection.

Operation ID `v2.pty.connect.token`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `ptyID` required | path | `string`  pattern ^pty | No description |
| `x-opencode-ticket` | header | `string \| null`  `string`  or  `null` | No description |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Responses

`200` Success

`application/json`

`object`

`location` [Location.InfoEncoded](#schema-Location.InfoEncoded)

`data` [PtyTicket.ConnectToken](#schema-PtyTicket.ConnectToken)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

`403` ForbiddenError

`application/json` [ForbiddenErrorEncoded](#schema-ForbiddenErrorEncoded)

`404` PtyNotFoundError

`application/json` [PtyNotFoundErrorEncoded](#schema-PtyNotFoundErrorEncoded)

get `/api/pty/{ptyID}/connect` Connect to PTY session

Establish a WebSocket connection streaming PTY output and accepting terminal input.

Operation ID `v2.pty.connect`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `ptyID` required | path | `string`  pattern ^pty | No description |
| `location[directory]` | query | `string` | No description |
| `location[workspace]` | query | `string` | No description |
| `cursor` | query | `string` | No description |
| `ticket` | query | `string` | No description |

### Responses

`200` Success

`application/json`

`boolean`

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

`403` ForbiddenError

`application/json` [ForbiddenErrorEncoded](#schema-ForbiddenErrorEncoded)

`404` PtyNotFoundError

`application/json` [PtyNotFoundErrorEncoded](#schema-PtyNotFoundErrorEncoded)

get `/api/experimental/session/{sessionID}/terminal/read` Read the session's most recently controlled terminal

Read the last physical rows without changing selection or taking control. Omitted lines uses the live terminal height; larger counts include retained history. Blank rows are preserved. Screen dimensions and cursor remain relative to the live screen. Returns null when no current terminal exists. Selection is server-local and resets on restart. Experimental: may change without compatibility guarantees.

Operation ID `server.experimental.persistentPty.read`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string`  pattern ^ses | No description |
| `lines` | query | `PersistentPty.ReadLinesEncoded \| null`  [PersistentPty.ReadLinesEncoded](#schema-PersistentPty.ReadLinesEncoded)  or  `null` | No description |

get `/api/experimental/session/{sessionID}/terminal`

Operation ID `server.experimental.persistentPty.list`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string`  pattern ^ses | No description |

post `/api/experimental/session/{sessionID}/terminal`

Operation ID `server.experimental.persistentPty.create`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `sessionID` required | path | `string`  pattern ^ses | No description |

### Request body required

`application/json` [PersistentPty.CreateInput](#schema-PersistentPty.CreateInput)

post `/api/experimental/persistent-pty/shutdown` post `/api/experimental/persistent-pty/handoff` get `/api/experimental/persistent-pty/{ptyID}`

Operation ID `server.experimental.persistentPty.get`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `ptyID` required | path | `string`  pattern ^pty | No description |

### Responses

`200` Success

`application/json`

`object`

`data` [PersistentPty.Info](#schema-PersistentPty.Info)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

`404` PtyNotFoundError

`application/json` [PtyNotFoundErrorEncoded](#schema-PtyNotFoundErrorEncoded)

`503` ServiceUnavailableError

`application/json` [ServiceUnavailableErrorEncoded](#schema-ServiceUnavailableErrorEncoded)

put `/api/experimental/persistent-pty/{ptyID}`

Operation ID `server.experimental.persistentPty.update`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `ptyID` required | path | `string`  pattern ^pty | No description |

### Request body required

`application/json` [PersistentPty.UpdateInput](#schema-PersistentPty.UpdateInput)

### Responses

`200` Success

`application/json`

`object`

`data` [PersistentPty.Info](#schema-PersistentPty.Info)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

`404` PtyNotFoundError

`application/json` [PtyNotFoundErrorEncoded](#schema-PtyNotFoundErrorEncoded)

`503` ServiceUnavailableError

`application/json` [ServiceUnavailableErrorEncoded](#schema-ServiceUnavailableErrorEncoded)

delete `/api/experimental/persistent-pty/{ptyID}`

Operation ID `server.experimental.persistentPty.remove`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `ptyID` required | path | `string`  pattern ^pty | No description |

### Responses

`204` <No Content>

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

`404` PtyNotFoundError

`application/json` [PtyNotFoundErrorEncoded](#schema-PtyNotFoundErrorEncoded)

`503` ServiceUnavailableError

`application/json` [ServiceUnavailableErrorEncoded](#schema-ServiceUnavailableErrorEncoded)

get `/api/experimental/persistent-pty/{ptyID}/snapshot`

Operation ID `server.experimental.persistentPty.snapshot`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `ptyID` required | path | `string`  pattern ^pty | No description |

### Responses

`200` Success

`application/json`

`object`

`data` [PersistentPty.Snapshot](#schema-PersistentPty.Snapshot)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

`404` PtyNotFoundError

`application/json` [PtyNotFoundErrorEncoded](#schema-PtyNotFoundErrorEncoded)

`503` ServiceUnavailableError

`application/json` [ServiceUnavailableErrorEncoded](#schema-ServiceUnavailableErrorEncoded)

post `/api/experimental/persistent-pty/{ptyID}/connect-token`

Operation ID `server.experimental.persistentPty.connectToken`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `ptyID` required | path | `string`  pattern ^pty | No description |
| `x-opencode-ticket` | header | `string \| null`  `string`  or  `null` | No description |

### Responses

`200` Success

`application/json`

`object`

`data` [PtyTicket.ConnectToken](#schema-PtyTicket.ConnectToken)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

`403` ForbiddenError

`application/json` [ForbiddenErrorEncoded](#schema-ForbiddenErrorEncoded)

`404` PtyNotFoundError

`application/json` [PtyNotFoundErrorEncoded](#schema-PtyNotFoundErrorEncoded)

`503` ServiceUnavailableError

`application/json` [ServiceUnavailableErrorEncoded](#schema-ServiceUnavailableErrorEncoded)

get `/api/experimental/persistent-pty/{ptyID}/connect` Connect to a persistent PTY

Stream persistent PTY output through the OpenCode server.

Operation ID `v2.persistentPty.connect`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `ptyID` required | path | `string`  pattern ^pty | No description |
| `cursor` | query | `string` | No description |
| `role` | query | `string` | No description |
| `attachment_id` | query | `string` | No description |
| `takeover` | query | `string` | No description |
| `input_protocol` | query | `string` | No description |
| `ticket` | query | `string` | No description |

### Responses

`200` Success

`application/json`

`boolean`

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

`403` ForbiddenError

`application/json` [ForbiddenErrorEncoded](#schema-ForbiddenErrorEncoded)

`404` PtyNotFoundError

`application/json` [PtyNotFoundErrorEncoded](#schema-PtyNotFoundErrorEncoded)

`503` ServiceUnavailableError

`application/json` [ServiceUnavailableErrorEncoded](#schema-ServiceUnavailableErrorEncoded)

get `/api/shell` List running shell commands

List currently running shell commands for a location. Exited commands are not included.

Operation ID `v2.shell.list`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Responses

`200` Success

`application/json`

`object`

`location` [Location.InfoEncoded](#schema-Location.InfoEncoded)

`data`

`Shell.Info[]` required

Items [Shell.Info](#schema-Shell.Info)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

post `/api/shell` Run shell command

Spawn one non-interactive shell command for a location. Combined stdout/stderr is captured to a file pageable via output.

Operation ID `v2.shell.create`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Request body required

`application/json`

`object`

`command`

`string` required

`cwd`

`string`

`timeout`

`integer` required

min 0

`metadata`

`object`

### Responses

`200` Success

`application/json`

`object`

`location` [Location.InfoEncoded](#schema-Location.InfoEncoded)

`data` [Shell.Info](#schema-Shell.Info)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

get `/api/shell/{id}` Get shell command

Get one shell command, including its status and exit code once exited.

Operation ID `v2.shell.get`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `id` required | path | `string`  pattern ^sh\_ | No description |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Responses

`200` Success

`application/json`

`object`

`location` [Location.InfoEncoded](#schema-Location.InfoEncoded)

`data` [Shell.Info](#schema-Shell.Info)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

`404` ShellNotFoundError

`application/json` [ShellNotFoundErrorEncoded](#schema-ShellNotFoundErrorEncoded)

delete `/api/shell/{id}` Remove shell command

Terminate and remove one shell command and its retained output.

Operation ID `v2.shell.remove`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `id` required | path | `string`  pattern ^sh\_ | No description |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Responses

`204` <No Content>

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

`404` ShellNotFoundError

`application/json` [ShellNotFoundErrorEncoded](#schema-ShellNotFoundErrorEncoded)

patch `/api/shell/{id}/timeout` Update shell timeout

Replace a running shell command's timeout from now, or clear it with zero.

Operation ID `v2.shell.timeout`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `id` required | path | `string`  pattern ^sh\_ | No description |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Request body required

`application/json`

`object`

`timeout`

`integer` required

min 0

### Responses

`200` Success

`application/json`

`object`

`location` [Location.InfoEncoded](#schema-Location.InfoEncoded)

`data` [Shell.Info](#schema-Shell.Info)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

`404` ShellNotFoundError

`application/json` [ShellNotFoundErrorEncoded](#schema-ShellNotFoundErrorEncoded)

get `/api/shell/{id}/output` Read shell output

Page through captured combined output by absolute byte cursor.

Operation ID `v2.shell.output`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `id` required | path | `string`  pattern ^sh\_ | No description |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |
| `cursor` | query | `string`  pattern ^\[+-\]?\\d\*\\.?\\d+(?:\[Ee\]\[+-\]?\\d+)?$ | No description |
| `limit` | query | `string`  pattern ^\[+-\]?\\d\*\\.?\\d+(?:\[Ee\]\[+-\]?\\d+)?$ | No description |

get `/api/reference` List references

List references available in the requested location.

Operation ID `v2.reference.list`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Responses

`200` Success

`application/json`

`object`

`location` [Location.InfoEncoded](#schema-Location.InfoEncoded)

`data`

`Reference.Info[]` required

Items [Reference.Info](#schema-Reference.Info)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

get `/api/worktree/{projectID}` List worktrees

List known local worktrees for a project.

Operation ID `v2.worktree.list`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `projectID` required | path | `string` | No description |

### Responses

`200` Worktree.List

`application/json` [Worktree.List](#schema-Worktree.List)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

post `/api/worktree/{projectID}` Create worktree

Create a worktree for a project and run its configured setup script.

Operation ID `v2.worktree.create`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `projectID` required | path | `string` | No description |

### Request body required

`application/json`

`object`

`strategy`

`string` required

`from`

`string`

`branch`

`string`

`directory`

`string` required

`name`

`string`

delete `/api/worktree/{projectID}` Remove worktree

Remove a managed worktree from a project.

Operation ID `v2.worktree.remove`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `projectID` required | path | `string` | No description |

### Request body required

`application/json`

`object`

`directory`

`string` required

`force`

`boolean` required

### Responses

`204` <No Content>

`400` WorktreeError | InvalidRequestError

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

post `/api/worktree/{projectID}/refresh` Refresh worktrees

Reconcile stored worktrees with the project repositories.

Operation ID `v2.worktree.refresh`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `projectID` required | path | `string` | No description |

### Responses

`204` <No Content>

`400` WorktreeError | InvalidRequestError

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

post `/api/workspace` Create workspace

Create a logical workspace. A caller-supplied ID is idempotent when retried with the same provider; reusing it with another provider returns a conflict.

Operation ID `v2.workspace.create`

### Request body required

`application/json`

`object`

`id`

`string | null`

`string`

pattern ^wrk

or

`null`

`provider`

`string` required

### Responses

`200` Success

`application/json`

`object`

`data`

`string` required

pattern ^wrk

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

`404` ProviderNotFoundError

`application/json` [ProviderNotFoundErrorEncoded](#schema-ProviderNotFoundErrorEncoded)

`409` ConflictError

`application/json` [ConflictErrorEncoded](#schema-ConflictErrorEncoded)

delete `/api/workspace/{workspaceID}` Destroy workspace

Make a workspace not exist. This operation is idempotent: an already-missing workspace succeeds with \`destroyed: false\`, while a workspace removed by this request returns \`destroyed: true\`.

Operation ID `v2.workspace.destroy`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `workspaceID` required | path | `string`  pattern ^wrk | No description |

### Responses

`200` Reports whether this request destroyed an existing workspace.

`application/json` [WorkspaceDestroyResult](#schema-WorkspaceDestroyResult)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

`500` UnknownError

`application/json` [UnknownErrorEncoded](#schema-UnknownErrorEncoded)

get `/api/vcs` VCS info

Get current and default branch information for the requested location.

Operation ID `v2.vcs.get`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Responses

`200` Success

`application/json`

`object`

`location` [Location.InfoEncoded](#schema-Location.InfoEncoded)

`data` [Vcs.Info](#schema-Vcs.Info)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

get `/api/vcs/base` VCS review base

Infer a local review base from named branch creation history, or the repository default only when currently on that branch. Returns null before the first commit or when the provider lacks base metadata; ambiguous Git history requires an explicit base on diff requests.

Operation ID `v2.vcs.base`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

get `/api/vcs/status` VCS status

List uncommitted working-copy changes relative to the requested location.

Operation ID `v2.vcs.status`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Responses

`200` Success

`application/json`

`object`

`location` [Location.InfoEncoded](#schema-Location.InfoEncoded)

`data`

`Vcs.FileStatus[]` required

Items [Vcs.FileStatus](#schema-Vcs.FileStatus)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

get `/api/vcs/branches` VCS branches

List local and remote branches available at the requested location.

Operation ID `v2.vcs.branches`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |
| `search` | query | `string \| null`  `string`  or  `null` | No description |
| `limit` | query | `string \| null`  `string`  or  `null` | No description |

### Responses

`200` Success

`application/json`

`object`

`location` [Location.InfoEncoded](#schema-Location.InfoEncoded)

`data` [Vcs.BranchList](#schema-Vcs.BranchList)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

get `/api/vcs/diff` VCS diff

Diff HEAD to the working copy (working), the base merge-base to the working copy (branch), or the base merge-base to HEAD (committed). Omitting base preserves repository-default comparison; supplying it overrides the comparison without saving it.

Operation ID `v2.vcs.diff`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |
| `mode` required | query | [Vcs.Mode](#schema-Vcs.Mode) | No description |
| `base` | query | `string` | No description |
| `context` | query | `string \| null`  `string`  or  `null` | No description |

### Responses

`200` Success

`application/json`

`object`

`location` [Location.InfoEncoded](#schema-Location.InfoEncoded)

`data`

`FileDiff.Info[]` required

Items [FileDiff.Info](#schema-FileDiff.Info)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

`503` ServiceUnavailableError

`application/json` [ServiceUnavailableErrorEncoded](#schema-ServiceUnavailableErrorEncoded)

get `/api/debug/location` List loaded locations

List locations currently loaded by the server.

Operation ID `v2.debug.location.list`

### Responses

`200` Success

`application/json`

`Location.Ref[]`

Items [Location.Ref](#schema-Location.Ref)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

delete `/api/debug/location` Evict a loaded location

Dispose the requested location's cached services so its next use boots them fresh.

Operation ID `v2.debug.location.evict`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Responses

`204` <No Content>

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

get `/api/experimental/migration/v1` Get V1 migration status

Return the progress of the V1 to V2 session history migration.

Operation ID `v2.experimental.migration.v1.status`

### Responses

`200` Success

`application/json`

`object | object | object`

`object`

`status`

`"required" | "completed"` required

Values `"required" | "completed"`

or

`object`

`status`

`"running"` required

Values `"running"`

`progress`

`object` required

`label`

`string` required

`numerator`

`integer | null`

`integer`

min 0

or

`null`

`denominator`

`integer | null`

`integer`

min 0

or

`null`

or

`object`

`status`

`"error"` required

Values `"error"`

`error`

`string` required

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

get `/api/websearch/provider` List web search providers

Return the registered web search providers.

Operation ID `v2.websearch.providers`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Responses

`200` Success

`application/json`

`object`

`location` [Location.InfoEncoded](#schema-Location.InfoEncoded)

`data`

`WebSearch.Provider[]` required

Items [WebSearch.Provider](#schema-WebSearch.Provider)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

`503` ServiceUnavailableError

`application/json` [ServiceUnavailableErrorEncoded](#schema-ServiceUnavailableErrorEncoded)

post `/api/websearch` Search the web

Run one web search through the selected provider. Specify a provider to override the configured default.

Operation ID `v2.websearch.query`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Request body required

`application/json`

`object`

`query`

`string` required

`providerID`

`string`

get `/api/config` Get configuration

Return configuration documents and discovery sources for the requested location, from lowest to highest priority.

Operation ID `v2.config.get`

### Parameters

| Name | Location | Type | Description |
| --- | --- | --- | --- |
| `location` | query | `object \| null`  `object`  `directory`  `string \| null`  `string`  or  `null`  `workspace`  `string \| null`  `string`  or  `null`  or  `null` | No description |

### Responses

`200` Success

`application/json`

`Config.Entry[]`

Items [Config.Entry](#schema-Config.Entry)

`400` InvalidRequestError

`application/json` [InvalidRequestErrorEncoded](#schema-InvalidRequestErrorEncoded)

`401` UnauthorizedError

`application/json` [UnauthorizedErrorEncoded](#schema-UnauthorizedErrorEncoded)

`Agent.Color` string

`string`

`Agent.Info` object

`object`

`id`

`string` required

`name`

`string` required

`model` [Model.Ref](#schema-Model.Ref)

`request` [Provider.Request](#schema-Provider.Request)

`system`

`string`

`description`

`string`

`mode`

`"subagent" | "primary" | "all"` required

Values `"subagent" | "primary" | "all"`

`hidden`

`boolean` required

`color` [Agent.Color](#schema-Agent.Color)

`steps`

`integer`

\> 0

`permissions` [Permission.Ruleset](#schema-Permission.Ruleset)

`AgentNotFoundErrorEncoded` object

`object`

`_tag`

`"AgentNotFoundError"` required

Values `"AgentNotFoundError"`

`agentID`

`string` required

`message`

`string` required

`Command.Info` object

`object`

`name`

`string` required

`description`

`string`

`CommandExecutionErrorEncoded` object

`object`

`_tag`

`"CommandExecutionError"` required

Values `"CommandExecutionError"`

`command`

`string` required

`message`

`string` required

`CommandNotFoundErrorEncoded` object

`object`

`_tag`

`"CommandNotFoundError"` required

Values `"CommandNotFoundError"`

`command`

`string` required

`message`

`string` required

`Config.AgentEncoded` object

`object`

`model`

`string | object`

`string`

pattern ^\[^/#\]+\\/\[^#\]+(?:#\[^#\]+)?$

or

`object`

`providerID`

`string` required

pattern ^\[^/#\]+$

`model`

`string` required

pattern ^\[^#\]+$

`variant`

`string`

pattern ^\[^#\]+$

`request`

`object`

`headers`

`object`

Additional properties

`string`

`body`

`object`

`system`

`string`

`description`

`string`

`mode`

`"subagent" | "primary" | "all"`

Values `"subagent" | "primary" | "all"`

`hidden`

`boolean`

`color`

`string`

pattern ^#\[0-9a-fA-F\]{6}$

`steps`

`integer`

\> 0

`disabled`

`boolean`

`permissions` [Permission.Ruleset](#schema-Permission.Ruleset)

`Config.AgentsDirectoryEncoded` object

`object`

`type`

`"agents"` required

Values `"agents"`

`path`

`string` required

`Config.ClaudeDirectoryEncoded` object

`object`

`type`

`"claude"` required

Values `"claude"`

`path`

`string` required

`Config.CommandEncoded` object

`object`

`template`

`string` required

`description`

`string`

`agent`

`string`

`model`

`string | object`

`string`

pattern ^\[^/#\]+\\/\[^#\]+(?:#\[^#\]+)?$

or

`object`

`providerID`

`string` required

pattern ^\[^/#\]+$

`model`

`string` required

pattern ^\[^#\]+$

`variant`

`string`

pattern ^\[^#\]+$

`subtask`

`boolean`

`Config.DirectoryEncoded` object

`object`

`type`

`"directory"` required

Values `"directory"`

`path`

`string` required

`Config.DocumentEncoded` object

`object`

`type`

`"document"` required

Values `"document"`

`path`

`string`

`info` [Config.InfoEncoded](#schema-Config.InfoEncoded)

`Config.Entry` Config.DocumentEncoded | Config.DirectoryEncoded | Config.AgentsDirectoryEncoded | Config.ClaudeDirectoryEncoded `Config.Formatter.EntryEncoded` object

`object`

`disabled`

`boolean`

`command`

`string[]`

Items

`string`

`environment`

`object`

Additional properties

`string`

`extensions`

`string[]`

Items

`string`

`Config.InfoEncoded` object `Config.LSP.ServerEncoded` object

`object`

`command`

`string[]` required

Items

`string`

`extensions`

`string[]`

Items

`string`

`disabled`

`boolean`

`env`

`object`

Additional properties

`string`

`initialization`

`object`

`Config.Model.CostEncoded` object

`object`

`tier`

`object`

`type`

`"context"` required

Values `"context"`

`size`

`integer` required

`input` [Money.USDPerMillionTokens](#schema-Money.USDPerMillionTokens)

`output` [Money.USDPerMillionTokens](#schema-Money.USDPerMillionTokens)

`cache`

`object`

`read` [Money.USDPerMillionTokens](#schema-Money.USDPerMillionTokens)

`write` [Money.USDPerMillionTokens](#schema-Money.USDPerMillionTokens)

`Config.ModelEncoded` object `Config.Plugin.EntryEncoded` object

`object`

`package`

`string` required

`options`

`object`

`Config.ProviderEncoded` object

`object`

`name`

`string`

`env`

`string[]`

Items

`string`

`package`

`string`

`settings`

`object`

`headers`

`object`

Additional properties

`string`

`body`

`object`

`models`

`object`

Additional properties [Config.ModelEncoded](#schema-Config.ModelEncoded)

`Config.Reference.GitEncoded` object

`object`

`repository`

`string` required

`branch`

`string`

`description`

`string`

`hidden`

`boolean`

`Config.Reference.LocalEncoded` object

`object`

`path`

`string` required

`description`

`string`

`hidden`

`boolean`

`Config.WarmingEncoded` object

`object`

`prompt`

`string`

`interval`

`string`

`duration`

`string`

`ConfigWebSearch.InfoEncoded` object

`object`

`provider`

`"random" | string` required

`"random"`

Values `"random"`

or

`string`

`ConflictErrorEncoded` object

`object`

`_tag`

`"ConflictError"` required

Values `"ConflictError"`

`message`

`string` required

`resource`

`string | null`

`string`

or

`null`

`Connection.CredentialInfo` object

`object`

`type`

`"credential"` required

Values `"credential"`

`id`

`string` required

`label`

`string` required

`Connection.EnvInfo` object

`object`

`type`

`"env"` required

Values `"env"`

`name`

`string` required

`Connection.Info` Connection.CredentialInfo | Connection.EnvInfo `FileSystem.Entry` object

`object`

`path`

`string` required

`type`

`"file" | "directory"` required

Values `"file" | "directory"`

`ForbiddenErrorEncoded` object

`object`

`_tag`

`"ForbiddenError"` required

Values `"ForbiddenError"`

`message`

`string` required

`Form.Answer` object

`object`

Additional properties [Form.Value](#schema-Form.Value)

`Form.BooleanField` object

`object`

`key`

`string` required

`title`

`string`

`description`

`string`

`required`

`boolean`

`when`

`Form.When[]`

Items [Form.When](#schema-Form.When)

`type`

`"boolean"` required

Values `"boolean"`

`default`

`boolean`

`Form.CreatePayload` object

`object`

`id`

`string | null`

`string`

pattern ^frm\_

or

`null`

`title`

`string` required

`metadata` [Form.Metadata](#schema-Form.Metadata)

`fields` [Form.Fields\_2](#schema-Form.Fields_2)

`Form.ExternalField` object

`object`

`key`

`string` required

`type`

`"external"` required

Values `"external"`

`url`

`string` required

`title`

`string`

`description`

`string`

`Form.Field` Form.StringField | Form.NumberField | Form.IntegerField | Form.BooleanField | Form.MultiselectField | Form.ExternalField `Form.Fields` Form.Field\[\]

`Form.Field[]`

min items 1

Items [Form.Field](#schema-Form.Field)

`Form.Fields_1` Form.Field\[\]

`Form.Field[]`

min items 1

Items [Form.Field](#schema-Form.Field)

`Form.Fields_2` Form.Field\[\]

`Form.Field[]`

min items 1

Items [Form.Field](#schema-Form.Field)

`Form.Info` object

`object`

`id`

`string` required

pattern ^frm\_

`sessionID`

`string` required

`title`

`string` required

`metadata` [Form.Metadata](#schema-Form.Metadata)

`fields` [Form.Fields\_2](#schema-Form.Fields_2)

`Form.IntegerField` object

`object`

`key`

`string` required

`title`

`string`

`description`

`string`

`required`

`boolean`

`when`

`Form.When[]`

Items [Form.When](#schema-Form.When)

`type`

`"integer"` required

Values `"integer"`

`minimum`

`number | "Infinity" | "-Infinity" | "NaN"`

`number`

or

`"Infinity" | "-Infinity" | "NaN"`

Values `"Infinity" | "-Infinity" | "NaN"`

`maximum`

`number | "Infinity" | "-Infinity" | "NaN"`

`number`

or

`"Infinity" | "-Infinity" | "NaN"`

Values `"Infinity" | "-Infinity" | "NaN"`

`default`

`number | "Infinity" | "-Infinity" | "NaN"`

`number`

or

`"Infinity" | "-Infinity" | "NaN"`

Values `"Infinity" | "-Infinity" | "NaN"`

`Form.MultiselectField` object `Form.NumberField` object

`object`

`key`

`string` required

`title`

`string`

`description`

`string`

`required`

`boolean`

`when`

`Form.When[]`

Items [Form.When](#schema-Form.When)

`type`

`"number"` required

Values `"number"`

`minimum`

`number | "Infinity" | "-Infinity" | "NaN"`

`number`

or

`"Infinity" | "-Infinity" | "NaN"`

Values `"Infinity" | "-Infinity" | "NaN"`

`maximum`

`number | "Infinity" | "-Infinity" | "NaN"`

`number`

or

`"Infinity" | "-Infinity" | "NaN"`

Values `"Infinity" | "-Infinity" | "NaN"`

`default`

`number | "Infinity" | "-Infinity" | "NaN"`

`number`

or

`"Infinity" | "-Infinity" | "NaN"`

Values `"Infinity" | "-Infinity" | "NaN"`

`Form.Option` object

`object`

`value`

`string` required

`label`

`string` required

`description`

`string`

`Form.Reply` object

`object`

`answer` [Form.Answer](#schema-Form.Answer)

`Form.State` object | object | object

`object | object | object`

`object`

`status`

`"pending"` required

Values `"pending"`

or

`object`

`status`

`"answered"` required

Values `"answered"`

`answer` [Form.Answer](#schema-Form.Answer)

or

`object`

`status`

`"cancelled"` required

Values `"cancelled"`

`Form.StringField` object

`object`

`key`

`string` required

`title`

`string`

`description`

`string`

`required`

`boolean`

`when`

`Form.When[]`

Items [Form.When](#schema-Form.When)

`type`

`"string"` required

Values `"string"`

`format`

`"email" | "uri" | "date" | "date-time"`

Values `"email" | "uri" | "date" | "date-time"`

`minLength`

`integer`

min 0

`maxLength`

`integer`

min 0

`pattern`

`string`

`placeholder`

`string`

`default`

`string`

`options`

`Form.Option[]`

Items [Form.Option](#schema-Form.Option)

`custom`

`boolean`

`Form.Value` string | number | "Infinity" | "-Infinity" | "NaN" | boolean | string\[\]

`string | number | "Infinity" | "-Infinity" | "NaN" | boolean | string[]`

`string`

or

`number | "Infinity" | "-Infinity" | "NaN"`

`number`

or

`"Infinity" | "-Infinity" | "NaN"`

Values `"Infinity" | "-Infinity" | "NaN"`

or

`boolean`

or

`string[]`

Items

`string`

`Form.When` object

`object`

`key`

`string` required

`op`

`"eq" | "neq"` required

Values `"eq" | "neq"`

`value`

`string | number | "Infinity" | "-Infinity" | "NaN" | boolean` required

`string`

or

`number | "Infinity" | "-Infinity" | "NaN"`

`number`

or

`"Infinity" | "-Infinity" | "NaN"`

Values `"Infinity" | "-Infinity" | "NaN"`

or

`boolean`

`FormAlreadySettledErrorEncoded` object

`object`

`_tag`

`"FormAlreadySettledError"` required

Values `"FormAlreadySettledError"`

`id`

`string` required

`message`

`string` required

`FormInvalidAnswerErrorEncoded` object

`object`

`_tag`

`"FormInvalidAnswerError"` required

Values `"FormInvalidAnswerError"`

`id`

`string` required

`message`

`string` required

`FormNotFoundErrorEncoded` object

`object`

`_tag`

`"FormNotFoundError"` required

Values `"FormNotFoundError"`

`id`

`string` required

`message`

`string` required

`GenerateTextResponse` object

`object`

`data`

`object` required

`text`

`string` required

`InstructionEntry.Info` object

`object`

`key` [InstructionEntry.Key](#schema-InstructionEntry.Key)

`value`

`object` required

JSON value attached to the session's instructions

`InstructionEntry.Key` string

`string`

Instruction entry key (lowercase alphanumerics plus. \_ -)

pattern ^\[a-z0-9\]\[a-z0-9.\_-\]\*$

`InstructionEntryValueTooLargeErrorEncoded` object

`object`

`_tag`

`"InstructionEntryValueTooLargeError"` required

Values `"InstructionEntryValueTooLargeError"`

`actualBytes`

`integer` required

`maxBytes`

`integer` required

`message`

`string` required

`Integration.AttemptEncoded` object

`object`

`attemptID`

`string` required

`url`

`string` required

`instructions`

`string` required

`mode`

`"auto" | "code"` required

Values `"auto" | "code"`

`time`

`object` required

`created`

`number | "Infinity" | "-Infinity" | "NaN"` required

`number`

or

`"Infinity" | "-Infinity" | "NaN"`

Values `"Infinity" | "-Infinity" | "NaN"`

`expires`

`number | "Infinity" | "-Infinity" | "NaN"` required

`number`

or

`"Infinity" | "-Infinity" | "NaN"`

Values `"Infinity" | "-Infinity" | "NaN"`

`Integration.AttemptStatus` object | object | object | object

`object | object | object | object`

`object`

`status`

`"pending"` required

Values `"pending"`

`time`

`object` required

`created`

`number | "Infinity" | "-Infinity" | "NaN"` required

`number`

or

`"Infinity" | "-Infinity" | "NaN"`

Values `"Infinity" | "-Infinity" | "NaN"`

`expires`

`number | "Infinity" | "-Infinity" | "NaN"` required

`number`

or

`"Infinity" | "-Infinity" | "NaN"`

Values `"Infinity" | "-Infinity" | "NaN"`

or

`object`

`status`

`"complete"` required

Values `"complete"`

`time`

`object` required

`created`

`number | "Infinity" | "-Infinity" | "NaN"` required

`number`

or

`"Infinity" | "-Infinity" | "NaN"`

Values `"Infinity" | "-Infinity" | "NaN"`

`expires`

`number | "Infinity" | "-Infinity" | "NaN"` required

`number`

or

`"Infinity" | "-Infinity" | "NaN"`

Values `"Infinity" | "-Infinity" | "NaN"`

or

`object`

`status`

`"failed"` required

Values `"failed"`

`message`

`string` required

`time`

`object` required

`created`

`number | "Infinity" | "-Infinity" | "NaN"` required

`number`

or

`"Infinity" | "-Infinity" | "NaN"`

Values `"Infinity" | "-Infinity" | "NaN"`

`expires`

`number | "Infinity" | "-Infinity" | "NaN"` required

`number`

or

`"Infinity" | "-Infinity" | "NaN"`

Values `"Infinity" | "-Infinity" | "NaN"`

or

`object`

`status`

`"expired"` required

Values `"expired"`

`time`

`object` required

`created`

`number | "Infinity" | "-Infinity" | "NaN"` required

`number`

or

`"Infinity" | "-Infinity" | "NaN"`

Values `"Infinity" | "-Infinity" | "NaN"`

`expires`

`number | "Infinity" | "-Infinity" | "NaN"` required

`number`

or

`"Infinity" | "-Infinity" | "NaN"`

Values `"Infinity" | "-Infinity" | "NaN"`

`Integration.CommandAttempt` object

`object`

`attemptID`

`string` required

`time`

`object` required

`created`

`number | "Infinity" | "-Infinity" | "NaN"` required

`number`

or

`"Infinity" | "-Infinity" | "NaN"`

Values `"Infinity" | "-Infinity" | "NaN"`

`expires`

`number | "Infinity" | "-Infinity" | "NaN"` required

`number`

or

`"Infinity" | "-Infinity" | "NaN"`

Values `"Infinity" | "-Infinity" | "NaN"`

`Integration.CommandAttemptStatus` object | object | object | object

`object | object | object | object`

`object`

`status`

`"pending"` required

Values `"pending"`

`message`

`string`

`time`

`object` required

`created`

`number | "Infinity" | "-Infinity" | "NaN"` required

`number`

or

`"Infinity" | "-Infinity" | "NaN"`

Values `"Infinity" | "-Infinity" | "NaN"`

`expires`

`number | "Infinity" | "-Infinity" | "NaN"` required

`number`

or

`"Infinity" | "-Infinity" | "NaN"`

Values `"Infinity" | "-Infinity" | "NaN"`

or

`object`

`status`

`"complete"` required

Values `"complete"`

`time`

`object` required

`created`

`number | "Infinity" | "-Infinity" | "NaN"` required

`number`

or

`"Infinity" | "-Infinity" | "NaN"`

Values `"Infinity" | "-Infinity" | "NaN"`

`expires`

`number | "Infinity" | "-Infinity" | "NaN"` required

`number`

or

`"Infinity" | "-Infinity" | "NaN"`

Values `"Infinity" | "-Infinity" | "NaN"`

or

`object`

`status`

`"failed"` required

Values `"failed"`

`message`

`string` required

`time`

`object` required

`created`

`number | "Infinity" | "-Infinity" | "NaN"` required

`number`

or

`"Infinity" | "-Infinity" | "NaN"`

Values `"Infinity" | "-Infinity" | "NaN"`

`expires`

`number | "Infinity" | "-Infinity" | "NaN"` required

`number`

or

`"Infinity" | "-Infinity" | "NaN"`

Values `"Infinity" | "-Infinity" | "NaN"`

or

`object`

`status`

`"expired"` required

Values `"expired"`

`time`

`object` required

`created`

`number | "Infinity" | "-Infinity" | "NaN"` required

`number`

or

`"Infinity" | "-Infinity" | "NaN"`

Values `"Infinity" | "-Infinity" | "NaN"`

`expires`

`number | "Infinity" | "-Infinity" | "NaN"` required

`number`

or

`"Infinity" | "-Infinity" | "NaN"`

Values `"Infinity" | "-Infinity" | "NaN"`

`Integration.CommandMethod` object

`object`

`id`

`string` required

`type`

`"command"` required

Values `"command"`

`label`

`string` required

`command`

`string[]` required

Items

`string`

`Integration.EnvMethod` object

`object`

`type`

`"env"` required

Values `"env"`

`names`

`string[]` required

Items

`string`

`Integration.Info` object

`object`

`id`

`string` required

`name`

`string` required

`metadata`

`object`

`methods`

`Integration.Method[]` required

Items [Integration.Method](#schema-Integration.Method)

`connections`

`Connection.Info[]` required

Items [Connection.Info](#schema-Connection.Info)

`Integration.KeyMethod` object

`object`

`type`

`"key"` required

Values `"key"`

`label`

`string`

`form` [Form.Fields\_1](#schema-Form.Fields_1)

`Integration.Method` Integration.OAuthMethod | Integration.CommandMethod | Integration.KeyMethod | Integration.EnvMethod `Integration.OAuthMethod` object

`object`

`id`

`string` required

`type`

`"oauth"` required

Values `"oauth"`

`label`

`string` required

`form` [Form.Fields](#schema-Form.Fields)

`InvalidCursorErrorEncoded` object

`object`

`_tag`

`"InvalidCursorError"` required

Values `"InvalidCursorError"`

`message`

`string` required

`InvalidRequestErrorEncoded` object

`object`

`_tag`

`"InvalidRequestError"` required

Values `"InvalidRequestError"`

`message`

`string` required

`kind`

`string | null`

`string`

or

`null`

`field`

`string | null`

`string`

or

`null`

`Location.InfoEncoded` object

`object`

`directory`

`string` required

`workspaceID`

`string`

pattern ^wrk

`project`

`object` required

`id`

`string` required

`directory`

`string` required

`canonical`

`string` required

`Location.Ref` object

`object`

`directory`

`string` required

`workspaceID`

`string`

pattern ^wrk

`Mcp.LocalConfigEncoded` object

`object`

`type`

`"local"` required

Values `"local"`

`command`

`string[]` required

Items

`string`

`cwd`

`string`

`environment`

`object`

Additional properties

`string`

`disabled`

`boolean`

`codemode`

`boolean`

`timeout`

`object`

`startup`

`integer`

\> 0

`catalog`

`integer`

\> 0

`execution`

`integer`

\> 0

`Mcp.OAuthConfigEncoded` object

`object`

`client_id`

`string`

`client_secret`

`string`

`scope`

`string`

`callback_port`

`integer`

min 1, max 65535

`redirect_uri`

`string`

`Mcp.RemoteConfigEncoded` object

`object`

`type`

`"remote"` required

Values `"remote"`

`url`

`string` required

`headers`

`object`

Additional properties

`string`

`oauth`

`Mcp.OAuthConfigEncoded | false`

[Mcp.OAuthConfigEncoded](#schema-Mcp.OAuthConfigEncoded)

or

`false`

Values `false`

`disabled`

`boolean`

`codemode`

`boolean`

`timeout`

`object`

`startup`

`integer`

\> 0

`catalog`

`integer`

\> 0

`execution`

`integer`

\> 0

`Mcp.Resource` object

`object`

`server`

`string` required

`name`

`string` required

`uri`

`string` required

`description`

`string`

`mimeType`

`string`

`Mcp.ResourceCatalog` object

`object`

`resources`

`Mcp.Resource[]` required

Items [Mcp.Resource](#schema-Mcp.Resource)

`templates`

`Mcp.ResourceTemplate[]` required

Items [Mcp.ResourceTemplate](#schema-Mcp.ResourceTemplate)

`Mcp.ResourceTemplate` object

`object`

`server`

`string` required

`name`

`string` required

`uriTemplate`

`string` required

`description`

`string`

`mimeType`

`string`

`Mcp.Server` object `Mcp.Status.Connected` object

`object`

`status`

`"connected"` required

Values `"connected"`

`Mcp.Status.Disabled` object

`object`

`status`

`"disabled"` required

Values `"disabled"`

`Mcp.Status.Failed` object

`object`

`status`

`"failed"` required

Values `"failed"`

`error`

`string` required

`Mcp.Status.NeedsAuth` object

`object`

`status`

`"needs_auth"` required

Values `"needs_auth"`

`Mcp.Status.Pending` object

`object`

`status`

`"pending"` required

Values `"pending"`

`McpServerNotFoundErrorEncoded` object

`object`

`_tag`

`"McpServerNotFoundError"` required

Values `"McpServerNotFoundError"`

`server`

`string` required

`message`

`string` required

`MessageNotFoundErrorEncoded` object

`object`

`_tag`

`"MessageNotFoundError"` required

Values `"MessageNotFoundError"`

`sessionID`

`string` required

`messageID`

`string` required

`message`

`string` required

`Model.Capabilities` object

`object`

`tools`

`boolean` required

`input`

`string[]` required

Items

`string`

`output`

`string[]` required

Items

`string`

`responsesWebsockets`

`boolean`

`Model.Compatibility` object

`object`

`reasoningField` [Model.ReasoningField](#schema-Model.ReasoningField)

`requireReasoning`

`boolean`

`maxTokensField` [Model.MaxTokensField](#schema-Model.MaxTokensField)

`requireFinishReason`

`boolean`

`requireAssistantAfterTool`

`boolean`

`Model.Cost` object

`object`

`tier`

`object`

`type`

`"context"` required

Values `"context"`

`size`

`integer` required

`input` [Money.USDPerMillionTokens](#schema-Money.USDPerMillionTokens)

`output` [Money.USDPerMillionTokens](#schema-Money.USDPerMillionTokens)

`cache`

`object` required

`read` [Money.USDPerMillionTokens](#schema-Money.USDPerMillionTokens)

`write` [Money.USDPerMillionTokens](#schema-Money.USDPerMillionTokens)

`Model.Info` object

`object`

`id`

`string` required

`modelID`

`string` required

`providerID`

`string` required

`family`

`string`

`name`

`string` required

`compatibility` [Model.Compatibility](#schema-Model.Compatibility)

`package`

`string`

`settings`

`object`

`headers`

`object`

Additional properties

`string`

`body`

`object`

`capabilities` [Model.Capabilities](#schema-Model.Capabilities)

`variants`

`Model.Variant[]` required

Items [Model.Variant](#schema-Model.Variant)

`time`

`object` required

`released`

`number` required

`cost`

`Model.Cost[]` required

Items [Model.Cost](#schema-Model.Cost)

`status`

`"alpha" | "beta" | "deprecated" | "active"` required

Values `"alpha" | "beta" | "deprecated" | "active"`

`enabled`

`boolean` required

`limit`

`object` required

`context`

`integer` required

`input`

`integer`

`output`

`integer` required

`Model.MaxTokensField` "max\_completion\_tokens" | "max\_tokens"

`"max_completion_tokens" | "max_tokens"`

Values `"max_completion_tokens" | "max_tokens"`

`Model.ReasoningField` "reasoning" | "reasoning\_content" | "reasoning\_text" | string

`"reasoning" | "reasoning_content" | "reasoning_text" | string`

`"reasoning" | "reasoning_content" | "reasoning_text"`

Values `"reasoning" | "reasoning_content" | "reasoning_text"`

or

`string`

`Model.Ref` object

`object`

`id`

`string` required

`providerID`

`string` required

`variant`

`string`

`Model.Variant` object

`object`

`id`

`string` required

`settings`

`object`

`headers`

`object`

Additional properties

`string`

`body`

`object`

`Money.USD` number

`number`

`Money.USDPerMillionTokens` number

`number`

`Permission.Effect` "allow" | "deny" | "ask"

`"allow" | "deny" | "ask"`

Values `"allow" | "deny" | "ask"`

`Permission.Reply` "once" | "always" | "reject"

`"once" | "always" | "reject"`

Values `"once" | "always" | "reject"`

`Permission.Request` object

`object`

`id`

`string` required

pattern ^per

`sessionID`

`string` required

pattern ^ses

`action`

`string` required

`resources`

`string[]` required

Items

`string`

`save`

`string[]`

Items

`string`

`metadata`

`object`

`source` [Permission.Source](#schema-Permission.Source)

`message`

`string`

`Permission.Rule` object

`object`

`action`

`string` required

`resource`

`string` required

`effect` [Permission.Effect](#schema-Permission.Effect)

`Permission.Ruleset` Permission.Rule\[\]

`Permission.Rule[]`

Items [Permission.Rule](#schema-Permission.Rule)

`Permission.Source` object

`object`

`object`

`type`

`"tool"` required

Values `"tool"`

`messageID`

`string` required

`id`

`string` required

`PermissionNotFoundErrorEncoded` object

`object`

`_tag`

`"PermissionNotFoundError"` required

Values `"PermissionNotFoundError"`

`requestID`

`string` required

`message`

`string` required

`PermissionSaved.Info` object

`object`

`id`

`string` required

`projectID`

`string` required

`action`

`string` required

`resource`

`string` required

`PersistentPty.CreateInput` object

`object`

`command`

`string`

`args`

`string[]` required

Items

`string`

`cwd`

`string`

`title`

`string` required

`env`

`object` required

Additional properties

`string`

`size`

`object`

`cols`

`integer` required

\> 0

`rows`

`integer` required

\> 0

`PersistentPty.Handoff` object

`object`

`directory`

`string` required

`instanceID`

`string` required

`ticket`

`string` required

`expiresAt`

`number | "Infinity" | "-Infinity" | "NaN"` required

`number`

or

`"Infinity" | "-Infinity" | "NaN"`

Values `"Infinity" | "-Infinity" | "NaN"`

`PersistentPty.Info` object

`object`

`id`

`string` required

pattern ^pty

`title`

`string` required

`command`

`string` required

`args`

`string[]` required

Items

`string`

`cwd`

`string` required

`status`

`"running" | "exited"` required

Values `"running" | "exited"`

`pid`

`integer` required

min 0

`exitCode`

`integer`

min 0

`sessionID`

`string` required

pattern ^ses

`foregroundProcess`

`string | null` required

`string`

or

`null`

`size`

`object` required

`cols`

`integer` required

\> 0

`rows`

`integer` required

\> 0

`output`

`object` required

`head`

`integer` required

min 0

`tail`

`integer` required

min 0

`PersistentPty.ReadLinesEncoded` string

`string`

`PersistentPty.ReadResult` object

`object`

`ptyID`

`string` required

pattern ^pty

`title`

`string` required

`cwd`

`string` required

`foregroundProcess`

`string | null` required

`string`

or

`null`

`screen`

`object` required

`text`

`string` required

`cols`

`integer` required

\> 0

`rows`

`integer` required

\> 0

`cursor`

`object` required

`x`

`integer` required

min 0

`y`

`integer` required

min 0

`PersistentPty.Snapshot` object

`object`

`info` [PersistentPty.Info](#schema-PersistentPty.Info)

`text`

`string` required

`checkpoint`

`string<byte>` required

`cursor`

`object` required

`x`

`integer` required

min 0

`y`

`integer` required

min 0

`PersistentPty.UpdateInput` object

`object`

`attachmentID`

`string`

`size`

`object` required

`cols`

`integer` required

\> 0

`rows`

`integer` required

\> 0

`Plugin.Features` object

`object`

`server`

`true`

Values `true`

`tui`

`true`

Values `true`

`rpc`

`true`

Values `true`

`Plugin.Info` object

`object`

`id`

`string`

`source` [Plugin.Source](#schema-Plugin.Source)

`features` [Plugin.Features](#schema-Plugin.Features)

`state` [Plugin.State](#schema-Plugin.State)

`Plugin.Source` object | object | object | object

`object | object | object | object`

`object`

`type`

`"builtin"` required

Values `"builtin"`

or

`object`

`type`

`"package"` required

Values `"package"`

`package`

`string` required

or

`object`

`type`

`"local"` required

Values `"local"`

`path`

`string` required

or

`object`

`type`

`"sdk"` required

Values `"sdk"`

`Plugin.State` object | object

`object | object`

`object`

`status`

`"active"` required

Values `"active"`

or

`object`

`status`

`"failed"` required

Values `"failed"`

`error`

`string` required

`Project` object

`object`

`id`

`string` required

`canonical`

`string` required

`vcs` [Project.Vcs](#schema-Project.Vcs)

`name`

`string`

`icon` [Project.Icon](#schema-Project.Icon)

`commands` [Project.Commands](#schema-Project.Commands)

`time` [Project.Time](#schema-Project.Time)

`sandboxes`

`string[]` required

Items

`string`

`Project.Commands` object

`object`

`start`

`string`

Startup script to run when creating a new workspace (worktree)

`Project.Current` object

`object`

`id`

`string` required

`directory`

`string` required

`canonical`

`string` required

`Project.Icon` object

`object`

`url`

`string`

`override`

`string`

`color`

`string`

`Project.Time` object

`object`

`created`

`integer` required

min 0

`updated`

`integer` required

min 0

`initialized`

`integer`

min 0

`Project.Vcs` string

`string`

pattern ^\[a-z\]\[a-z0-9.\_-\]\*$

`ProjectNotFoundErrorEncoded` object

`object`

`_tag`

`"ProjectNotFoundError"` required

Values `"ProjectNotFoundError"`

`projectID`

`string` required

`message`

`string` required

`Prompt.AgentAttachment` object

`object`

`name`

`string` required

`mention` [Prompt.Mention](#schema-Prompt.Mention)

`Prompt.Base64` string

`string`

pattern ^(?:\[A-Za-z0-9+/\]{4})\*(?:\[A-Za-z0-9+/\]{2}==|\[A-Za-z0-9+/\]{3}=)?$

`Prompt.FileAttachment` object

`object`

`data` [Prompt.Base64](#schema-Prompt.Base64)

`mime`

`string` required

`source` [Prompt.FileSource](#schema-Prompt.FileSource)

`name`

`string`

`description`

`string`

`mention` [Prompt.Mention](#schema-Prompt.Mention)

`Prompt.FileSource` object | object

`object | object`

`object`

`type`

`"inline"` required

Values `"inline"`

or

`object`

`type`

`"uri"` required

Values `"uri"`

`uri`

`string` required

`Prompt.Mention` object

`object`

`start`

`number` required

`end`

`number` required

`text`

`string` required

`Prompt.SkillAttachment` object

`object`

`id`

`string` required

`name`

`string` required

`text`

`string`

`mention` [Prompt.Mention](#schema-Prompt.Mention)

`PromptInput.FileAttachment` object

`object`

`uri`

`string` required

`name`

`string`

`description`

`string`

`mention` [Prompt.Mention](#schema-Prompt.Mention)

`PromptInput.SkillAttachment` object

`object`

`id`

`string` required

`mention` [Prompt.Mention](#schema-Prompt.Mention)

`Provider.Info` object

`object`

`id`

`string` required

`integrationID`

`string`

`name`

`string` required

`activation`

`"auto" | "enabled" | "disabled"` required

Values `"auto" | "enabled" | "disabled"`

`package`

`string` required

`settings`

`object`

`headers`

`object`

Additional properties

`string`

`body`

`object`

`Provider.Request` object

`object`

`settings` [Provider.Settings](#schema-Provider.Settings)

`headers`

`object` required

Additional properties

`string`

`body`

`object` required

`Provider.Settings` object

`object`

`ProviderNotFoundErrorEncoded` object

`object`

`_tag`

`"ProviderNotFoundError"` required

Values `"ProviderNotFoundError"`

`providerID`

`string` required

`message`

`string` required

`Pty` object

`object`

`id`

`string` required

pattern ^pty

`title`

`string` required

`command`

`string` required

`args`

`string[]` required

Items

`string`

`cwd`

`string` required

`status`

`"running" | "exited"` required

Values `"running" | "exited"`

`pid`

`integer` required

min 0

`exitCode`

`integer`

min 0

`PtyNotFoundErrorEncoded` object

`object`

`_tag`

`"PtyNotFoundError"` required

Values `"PtyNotFoundError"`

`ptyID`

`string` required

`message`

`string` required

`PtyTicket.ConnectToken` object

`object`

`ticket`

`string` required

`expires_in`

`integer` required

\> 0

`Reference.GitSource` object

`object`

`type`

`"git"` required

Values `"git"`

`repository`

`string` required

`branch`

`string`

`description`

`string`

`hidden`

`boolean`

`Reference.Info` object

`object`

`name`

`string` required

`path`

`string` required

`description`

`string`

`hidden`

`boolean`

`source` [Reference.Source](#schema-Reference.Source)

`Reference.LocalSource` object

`object`

`type`

`"local"` required

Values `"local"`

`path`

`string` required

`description`

`string`

`hidden`

`boolean`

`Reference.Source` Reference.LocalSource | Reference.GitSource `Rpc.Input` object

`object`

`input`

`object`

`Rpc.Output` object

`object`

`output`

`object`

`RpcErrorEncoded` object

`object`

`_tag`

`"RpcError"` required

Values `"RpcError"`

`type`

`string` required

`message`

`string` required

`data`

`object | null`

`object`

or

`null`

`RpcInternalErrorEncoded` object

`object`

`_tag`

`"RpcInternalError"` required

Values `"RpcInternalError"`

`type`

`"rpc.internal" | "rpc.invalid_output"` required

Values `"rpc.internal" | "rpc.invalid_output"`

`message`

`string` required

`data`

`object | null`

`object`

or

`null`

`ServiceHealth` object

`object`

`healthy`

`true` required

Values `true`

`version`

`string` required

`pid`

`integer` required

min 0

`ServiceUnavailableErrorEncoded` object

`object`

`_tag`

`"ServiceUnavailableError"` required

Values `"ServiceUnavailableError"`

`message`

`string` required

`service`

`string | null`

`string`

or

`null`

`Session.ForkBoundary` object | object

`object | object`

`object`

`type`

`"before"` required

Values `"before"`

`messageID`

`string` required

pattern ^msg\_

or

`object`

`type`

`"through"` required

Values `"through"`

`messageID`

`string` required

pattern ^msg\_

`Session.ForkRequestBoundary` object | object

`object | object`

`object`

`type`

`"before"` required

Values `"before"`

`messageID`

`string` required

pattern ^msg\_

or

`object`

`type`

`"through"` required

Values `"through"`

`Session.Inbox.Compaction` object `Session.Inbox.CompactionPayload` object | empty\[\]

`object | empty[]`

`object`

or

`empty[]`

`Session.Inbox.Delivery` "steer" | "queue"

`"steer" | "queue"`

Values `"steer" | "queue"`

`Session.Inbox.Info` Session.Inbox.User | Session.Inbox.Synthetic | Session.Inbox.Compaction | Session.Inbox.Move `Session.Inbox.Move` object `Session.Inbox.MovePayload` object

`object`

`location` [Location.Ref](#schema-Location.Ref)

`projectID`

`string` required

`subpath`

`string`

`Session.Inbox.Synthetic` object `Session.Inbox.SyntheticPayload` object

`object`

`text`

`string` required

`description`

`string`

`metadata`

`object`

`Session.Inbox.User` object `Session.Inbox.UserPayload` object

`object`

`text`

`string` required

`files`

`Prompt.FileAttachment[]`

Items [Prompt.FileAttachment](#schema-Prompt.FileAttachment)

`agents`

`Prompt.AgentAttachment[]`

Items [Prompt.AgentAttachment](#schema-Prompt.AgentAttachment)

`skills`

`Prompt.SkillAttachment[]`

Items [Prompt.SkillAttachment](#schema-Prompt.SkillAttachment)

`metadata`

`object`

`Session.Info` object `Session.Message.AgentSelected` object

`object`

`id`

`string` required

pattern ^msg\_

`metadata`

`object`

`time`

`object` required

`created`

`number` required

`type`

`"agent-switched"` required

Values `"agent-switched"`

`agent`

`string` required

`previous`

`string`

`Session.Message.Assistant` object

`object`

`id`

`string` required

pattern ^msg\_

`metadata`

`object`

`time`

`object` required

`created`

`number` required

`streamed`

`number`

`completed`

`number`

`type`

`"assistant"` required

Values `"assistant"`

`agent`

`string` required

`model` [Model.Ref](#schema-Model.Ref)

`content`

`Session.Message.Assistant.Text | Session.Message.Assistant.Reasoning | Session.Message.Assistant.Tool[]` required

`snapshot`

`object`

`start`

`string`

`end`

`string`

`files`

`string[]`

Items

`string`

`finish`

`"stop" | "length" | "tool-calls" | "content-filter" | "error" | "unknown"`

Values `"stop" | "length" | "tool-calls" | "content-filter" | "error" | "unknown"`

`rawFinish`

`string`

`providerState` [Session.Message.ProviderState\_4](#schema-Session.Message.ProviderState_4)

`cost` [Money.USD](#schema-Money.USD)

`tokens` [TokenUsage.Info](#schema-TokenUsage.Info)

`error` [Session.StructuredError](#schema-Session.StructuredError)

`retry` [Session.Message.Assistant.Retry](#schema-Session.Message.Assistant.Retry)

`Session.Message.Assistant.Reasoning` object

`object`

`type`

`"reasoning"` required

Values `"reasoning"`

`text`

`string` required

`state` [Session.Message.ProviderState\_1](#schema-Session.Message.ProviderState_1)

`time`

`object`

`created`

`number` required

`completed`

`number`

`Session.Message.Assistant.Retry` object

`object`

`attempt`

`integer` required

\> 0

`at`

`number` required

`error` [Session.StructuredError](#schema-Session.StructuredError)

`Session.Message.Assistant.Text` object

`object`

`type`

`"text"` required

Values `"text"`

`text`

`string` required

`state` [Session.Message.ProviderState](#schema-Session.Message.ProviderState)

`Session.Message.Assistant.Tool` object `Session.Message.Compaction` Session.Message.Compaction.Running | Session.Message.Compaction.Completed | Session.Message.Compaction.Failed `Session.Message.Compaction.Completed` object

`object`

`type`

`"compaction"` required

Values `"compaction"`

`id`

`string` required

pattern ^msg\_

`metadata`

`object`

`time`

`object` required

`created`

`number` required

`status`

`"completed"` required

Values `"completed"`

`reason`

`"auto" | "manual"` required

Values `"auto" | "manual"`

`summary`

`string` required

`recent`

`string` required

`Session.Message.Compaction.Failed` object

`object`

`type`

`"compaction"` required

Values `"compaction"`

`id`

`string` required

pattern ^msg\_

`metadata`

`object`

`time`

`object` required

`created`

`number` required

`status`

`"failed"` required

Values `"failed"`

`reason`

`"auto" | "manual"` required

Values `"auto" | "manual"`

`error` [Session.StructuredError](#schema-Session.StructuredError)

`Session.Message.Compaction.Running` object

`object`

`type`

`"compaction"` required

Values `"compaction"`

`id`

`string` required

pattern ^msg\_

`metadata`

`object`

`time`

`object` required

`created`

`number` required

`status`

`"running"` required

Values `"running"`

`reason`

`"auto" | "manual"` required

Values `"auto" | "manual"`

`summary`

`string` required

`recent`

`string` required

`Session.Message.Info` Session.Message.AgentSelected | Session.Message.ModelSelected | Session.Message.LocationSwitched | Session.Message.User | Session.Message.Synthetic | Session.Message.System | Session.Message.Skill | Session.Message.Shell | Session.Message.Assistant | Session.Message.Compaction `Session.Message.LocationSwitched` object

`object`

`id`

`string` required

pattern ^msg\_

`metadata`

`object`

`time`

`object` required

`created`

`number` required

`type`

`"location-switched"` required

Values `"location-switched"`

`location` [Location.Ref](#schema-Location.Ref)

`projectID`

`string`

`subpath`

`string`

`previous`

`object`

`location` [Location.Ref](#schema-Location.Ref)

`projectID`

`string`

`subpath`

`string`

`Session.Message.ModelSelected` object

`object`

`id`

`string` required

pattern ^msg\_

`metadata`

`object`

`time`

`object` required

`created`

`number` required

`type`

`"model-switched"` required

Values `"model-switched"`

`model` [Model.Ref](#schema-Model.Ref)

`previous` [Model.Ref](#schema-Model.Ref)

`Session.Message.ProviderState` object

`object`

`Session.Message.ProviderState_1` object

`object`

`Session.Message.ProviderState_2` object

`object`

`Session.Message.ProviderState_3` object

`object`

`Session.Message.ProviderState_4` object

`object`

`Session.Message.Shell` object

`object`

`id`

`string` required

pattern ^msg\_

`metadata`

`object`

`time`

`object` required

`created`

`number` required

`completed`

`number`

`type`

`"shell"` required

Values `"shell"`

`shellID`

`string` required

pattern ^sh\_

`command`

`string` required

`status`

`"running" | "exited" | "timeout" | "killed"` required

Values `"running" | "exited" | "timeout" | "killed"`

`exit`

`number | "Infinity" | "-Infinity" | "NaN"`

`number`

or

`"Infinity" | "-Infinity" | "NaN"`

Values `"Infinity" | "-Infinity" | "NaN"`

`output`

`object`

`output`

`string` required

`cursor`

`integer` required

min 0

`size`

`integer` required

min 0

`truncated`

`boolean` required

`Session.Message.Skill` object

`object`

`id`

`string` required

pattern ^msg\_

`metadata`

`object`

`time`

`object` required

`created`

`number` required

`type`

`"skill"` required

Values `"skill"`

`skill`

`string` required

`name`

`string` required

`text`

`string` required

`Session.Message.Synthetic` object

`object`

`id`

`string` required

pattern ^msg\_

`metadata`

`object`

`time`

`object` required

`created`

`number` required

`text`

`string` required

`description`

`string`

`type`

`"synthetic"` required

Values `"synthetic"`

`Session.Message.System` object

`object`

`id`

`string` required

pattern ^msg\_

`metadata`

`object`

`time`

`object` required

`created`

`number` required

`type`

`"system"` required

Values `"system"`

`text`

`string` required

`description`

`string`

`Session.Message.ToolState.Completed` object

`object`

`status`

`"completed"` required

Values `"completed"`

`input`

`object` required

`content`

`Tool.Content[]` required

min items 1

Items [Tool.Content](#schema-Tool.Content)

`metadata`

`object`

`Session.Message.ToolState.Error` object `Session.Message.ToolState.Running` object

`object`

`status`

`"running"` required

Values `"running"`

`input`

`object` required

`metadata`

`object` required

`Session.Message.ToolState.Streaming` object

`object`

`status`

`"streaming"` required

Values `"streaming"`

`input`

`string` required

`Session.Message.User` object

`object`

`id`

`string` required

pattern ^msg\_

`metadata`

`object`

`time`

`object` required

`created`

`number` required

`text`

`string` required

`files`

`Prompt.FileAttachment[]`

Items [Prompt.FileAttachment](#schema-Prompt.FileAttachment)

`agents`

`Prompt.AgentAttachment[]`

Items [Prompt.AgentAttachment](#schema-Prompt.AgentAttachment)

`skills`

`Prompt.SkillAttachment[]`

Items [Prompt.SkillAttachment](#schema-Prompt.SkillAttachment)

`type`

`"user"` required

Values `"user"`

`Session.Revert` object

`object`

`messageID`

`string` required

pattern ^msg\_

`partID`

`string`

`snapshot`

`string`

`files`

`FileDiff.Info[]`

Items [FileDiff.Info](#schema-FileDiff.Info)

`Session.StructuredError` object

`object`

`type`

`string` required

`message`

`string` required

`status`

`integer`

min 100, max 599

`SessionActive` object

`object`

`type`

`"running"` required

Values `"running"`

`SessionBusyErrorEncoded` object

`object`

`_tag`

`"SessionBusyError"` required

Values `"SessionBusyError"`

`sessionID`

`string` required

`message`

`string` required

`SessionGenerateResponse` object

`object`

`data`

`object` required

`text`

`string` required

`SessionInterruptResponse` object

`object`

`interrupted`

`boolean` required

Whether an active execution owned by this OpenCode process was interrupted.

`SessionLogItemEncoded` string

`string`

`SessionMessagesResponse` object

`object`

`data`

`Session.Message.Info[]` required

Items [Session.Message.Info](#schema-Session.Message.Info)

`cursor`

`object` required

`previous`

`string | null`

`string`

or

`null`

`next`

`string | null`

`string`

or

`null`

`SessionNotFoundErrorEncoded` object

`object`

`_tag`

`"SessionNotFoundError"` required

Values `"SessionNotFoundError"`

`sessionID`

`string` required

`message`

`string` required

`SessionStats.Activity` object

`object`

`date`

`string` required

`steps`

`integer` required

min 0

`SessionStats.Info` object `SessionStats.ModelUsage` object

`object`

`model` [Model.Ref](#schema-Model.Ref)

`steps`

`integer` required

min 0

`tokens` [TokenUsage.Info](#schema-TokenUsage.Info)

`cost` [Money.USD](#schema-Money.USD)

`SessionStats.ToolTotals` object

`object`

`calls`

`integer` required

min 0

`succeeded`

`integer` required

min 0

`failed`

`integer` required

min 0

`unfinished`

`integer` required

min 0

`SessionStats.ToolUsage` object

`object`

`name`

`string` required

`calls`

`integer` required

min 0

`succeeded`

`integer` required

min 0

`failed`

`integer` required

min 0

`unfinished`

`integer` required

min 0

`durationP50`

`number`

`SessionStats.Tools` object | object | object `SessionTransfer.Data` object

`object`

`info` [Session.Info](#schema-Session.Info)

`messages`

`Session.Message.Info[]` required

Items [Session.Message.Info](#schema-Session.Message.Info)

`SessionsResponse` object

`object`

`data`

`Session.Info[]` required

Items [Session.Info](#schema-Session.Info)

`cursor`

`object` required

`previous`

`string | null`

`string`

or

`null`

`next`

`string | null`

`string`

or

`null`

`Shell.Info` object

`object`

`id`

`string` required

pattern ^sh\_

`status`

`"running" | "exited" | "timeout" | "killed"` required

Values `"running" | "exited" | "timeout" | "killed"`

`command`

`string` required

`cwd`

`string` required

`shell`

`string` required

`file`

`string` required

`pid`

`integer`

min 0

`exit`

`number`

`metadata`

`object` required

`time`

`object` required

`started`

`number` required

`completed`

`number`

`ShellNotFoundErrorEncoded` object

`object`

`_tag`

`"ShellNotFoundError"` required

Values `"ShellNotFoundError"`

`id`

`string` required

`message`

`string` required

`Skill.Info` object

`object`

`id`

`string` required

`name`

`string` required

`description`

`string`

`slash`

`boolean`

`autoinvoke`

`boolean`

`location`

`string` required

`content`

`string` required

`SkillNotFoundErrorEncoded` object

`object`

`_tag`

`"SkillNotFoundError"` required

Values `"SkillNotFoundError"`

`skill`

`string` required

`message`

`string` required

`TokenUsage.Info` object

`object`

`input`

`number` required

`output`

`number` required

`reasoning`

`number` required

`cache`

`object` required

`read`

`number` required

`write`

`number` required

`Tool.Content` Tool.TextContent | Tool.FileContent `Tool.FileContent` object

`object`

`type`

`"file"` required

Values `"file"`

`uri`

`string` required

`mime`

`string` required

`name`

`string | null`

`string`

or

`null`

`Tool.TextContent` object

`object`

`type`

`"text"` required

Values `"text"`

`text`

`string` required

`UnauthorizedErrorEncoded` object

`object`

`_tag`

`"UnauthorizedError"` required

Values `"UnauthorizedError"`

`message`

`string` required

`UnknownErrorEncoded` object

`object`

`_tag`

`"UnknownError"` required

Values `"UnknownError"`

`message`

`string` required

`ref`

`string | null`

`string`

or

`null`

`V2EventEncoded` string

`string`

`Vcs.Base` object

`object`

`name`

`string` required

`ref`

`string` required

`source`

`"reflog" | "default"` required

Values `"reflog" | "default"`

`Vcs.Branch` object

`object`

`current`

`string`

`default`

`string`

`Vcs.BranchList` string\[\]

`string[]`

Items

`string`

`Vcs.FileStatus` object

`object`

`file`

`string` required

`additions`

`integer` required

min 0

`deletions`

`integer` required

min 0

`status`

`"added" | "deleted" | "modified"` required

Values `"added" | "deleted" | "modified"`

`Vcs.Info` object

`object`

`branch` [Vcs.Branch](#schema-Vcs.Branch)

`Vcs.Mode` "working" | "branch" | "committed"

`"working" | "branch" | "committed"`

Values `"working" | "branch" | "committed"`

`WebSearch.Provider` object

`object`

`id`

`string` required

`name`

`string` required

`WebSearch.ResponseEncoded` object

`object`

`providerID`

`string` required

`results`

`WebSearch.Result[]` required

Items [WebSearch.Result](#schema-WebSearch.Result)

`WebSearch.Result` object

`object`

`url`

`string` required

`title`

`string`

`content`

`string`

`time`

`object` required

`published`

`number`

`WorkspaceDestroyResult` object

`object`

Reports whether this request destroyed an existing workspace.

`destroyed`

`boolean` required

True when this request transitioned the workspace from existing to destroyed.

`Worktree.Directory` object

`object`

`directory`

`string` required

`strategy`

`string`

`Worktree.Info` object

`object`

`directory`

`string` required

`Worktree.List` Worktree.Directory\[\]

`Worktree.Directory[]`

Items [Worktree.Directory](#schema-Worktree.Directory)

`WorktreeErrorEncoded` object

`object`

`name`

`"WorktreeError"` required

Values `"WorktreeError"`

`data`

`object` required

`message`

`string` required

`forceRequired`

`boolean | null`

`boolean`

or

`null`
