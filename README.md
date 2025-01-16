# Squirrel Scheduler

Squirrel Scheduler is an open-source scheduling service designed to let you easily schedule and manage events or tasks to be executed at a specific point in time. With a simple push of a JSON payload, you can defer the execution of a workflow, send an email, trigger a webhook, or fire off any custom event at a predetermined date and time—all without having to spin up your own scheduling infrastructure.

## Key Features

- **RESTful API**: A straightforward HTTP endpoint that accepts an event payload and a `sendAt` timestamp.
- **Simple or Complex**: Handle single, one-shot events or orchestrate more complex scenarios with chained triggers.
- **Scalable Infrastructure**: Built with modern, cloud-native patterns for high availability and reliability.
- **Open Source**: Use it self-hosted for complete control, or let us host it for you with our managed service.

## Unique Value Proposition

While many scheduling services can handle delayed messages or periodic tasks, Squirrel Scheduler goes further with the following capabilities:

1. **Dependency Management**  
   Define child events that only trigger after the completion (or success) of other events—no need to build a separate orchestrator. This allows you to create complex flows (e.g., "once the user is notified, then schedule a follow-up email in 2 days").

2. **Dynamic Rescheduling**  
   Provide an API to update the execution time of already scheduled events. If your business logic or external factors change, simply call the update endpoint to adjust the schedule—no need to cancel and re-create events.

3. **Result Storage**  
   Not only does Squirrel Scheduler fire the event, but it can also store the resulting response for a configurable retention period (e.g., 7 days). This gives you an audit trail of what happened and the ability to re-send or replay events if needed.

4. **Native Fire-and-Forget with Fallback**  
   If the target endpoint does not respond, Squirrel Scheduler can automatically trigger a fallback mechanism (e.g., send a notification email or call a backup endpoint). This reduces the overhead of building such logic on your own.

5. **Drag & Drop UI for Scheduling Pipelines**  
   In addition to a robust API, a built-in visual workflow builder lets you design scheduling pipelines with multiple steps. Ideal for business teams or power users who want to define complex sequences without writing code.

## Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/DipSway/squirrel-scheduler.git
cd squirrel-scheduler
```

### 2. Install Dependencies

Depending on your technology stack, you'll need to install the required packages:

```bash
# Example for Node.js-based approach
npm install
```

### 3. Configure Environment

Create a `.env` file (or similar) with your preferred configuration settings (database connection, port, etc.). An example `.env.example` is provided.

### 4. Run the Server

```bash
npm start
```

If everything is configured properly, the service should be accessible on a local port (e.g., http://localhost:3000).

## Usage Example

Below is a simplified JSON payload to schedule an event:

```json
{
  "event": "email.send.paper_workflow_1",
  "message": {
    "subject": "Reminder",
    "body": "Hello, this is a scheduled email!"
  },
  "sendAt": "2025-02-01T10:00:00Z",
  "maxRetries": 0,
  "fireAndForget": true
}
```

- **event**: A human-readable identifier for the event.
- **message**: The payload you want forwarded to the endpoint you configure.
- **sendAt**: The exact date/time (UTC) to schedule the event.
- **maxRetries**: 0 for a single attempt, -1 for infinite retries.
- **fireAndForget**: If true, the scheduler sends the event once and doesn't track its outcome, unless fallback is configured.

Use a REST client (curl, Postman, etc.) or your preferred language to POST this payload to the Squirrel Scheduler endpoint (e.g., `POST /api/v1/schedule`).

## Roadmap

Below is our upcoming feature roadmap. Contributions and feedback are welcome!

### MVP Release

- Basic REST endpoints for scheduling single events
- maxRetries support (including an optional exponential backoff)
- Documentation and setup instructions

### Dependency Management (Parent-Child Events)

- Ability to define child events triggered only after the successful completion of their parents
- Orchestrate complex sequences without external workflow managers

### Dynamic Rescheduling

- Additional API endpoints to change the scheduled time (and possibly message payload) of existing events
- Graceful handling of in-progress tasks when rescheduling

### Result Storage & Replay

- Database or file storage for event execution logs and responses
- Simple UI to browse logs and resend or replay events if needed

### Native Fallback Mechanism

- Automatically trigger an alternative endpoint or send an alert when the primary endpoint fails or times out
- Configurable fallback policies (linear backoff, notifications, etc.)

### Visual Workflow Builder (Drag & Drop)

- Web-based editor to design multi-step scheduling pipelines
- Real-time visualization of event dependencies and scheduling timelines

### Plugins & Integrations

- Out-of-the-box connectors for popular services (Slack, AWS, etc.)
- Marketplace for custom plugins contributed by the community

### Performance & Scalability Enhancements

- Horizontal scaling options (Kubernetes, Docker Compose, etc.)
- Caching and rate limiting to handle large volumes of scheduled tasks

### Enterprise Features

- Role-based access control (RBAC) and audit trails
- Extended support for on-premises or private cloud deployments

## Contributing

We welcome community contributions! Please see our `CONTRIBUTING.md` for guidelines on submitting issues, pull requests, and feature suggestions.

## License

Squirrel Scheduler is released under an MIT Expat License. See the `LICENSE` file for details, including exceptions for any third-party components and optional enterprise directories (if applicable).

Happy Scheduling! If you have any questions or need additional help, please open an issue or join our community forums.