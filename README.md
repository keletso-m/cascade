# SystemPulse

A lightweight, cross-platform system performance and health assistant built with C# and .NET.

SystemPulse monitors system resources, identifies processes consuming significant CPU and memory, tracks performance over time, and provides explainable recommendations to help users understand and manage their system.

The project is designed to be lightweight, understandable, and practical rather than a replacement for tools such as `btop`, or enterprise monitoring platforms.

> Monitor your system. Understand resource usage. Detect unusual activity. Take informed action.

---

## Screenshots

> Screenshots will be added as the application develops.

### System Dashboard

<!-- Add dashboard screenshot here -->

### Process Monitoring

<!-- Add process monitoring screenshot here -->

### Performance History

<!-- Add historical performance screenshot here -->

---

## Features

### System Monitoring

- Monitor overall CPU utilization.
- Monitor memory usage.
- Monitor disk activity.
- Display system health metrics.
- Track system performance over time.

### Process Monitoring

- Discover running processes.
- Display per-process CPU usage.
- Display per-process memory usage.
- Sort processes by resource consumption.
- View process details.
- Monitor process activity over time.

### Alerts and Recommendations

- Detect sustained high CPU usage.
- Detect high memory consumption.
- Notify users about significant resource usage.
- Provide explainable recommendations.
- Allow users to configure monitoring thresholds.
- Support process exclusions.

### Performance History

- Store resource measurements locally.
- Display historical CPU and memory usage.
- Identify recurring resource-intensive processes.
- Compare current usage with historical patterns.

### Cross-Platform Support

- Linux-first development and testing.
- Designed for cross-platform support.
- Platform-specific system integrations isolated behind abstractions.

---

## Technology Stack

| Component | Technology |
|---|---|
| Language | C# |
| Runtime | .NET 10 |
| Desktop UI | Avalonia UI |
| Monitoring | Linux `/proc` and platform-specific system APIs |
| Background processing | .NET Worker Services |
| Database | SQLite |
| Data access | Entity Framework Core or Dapper |
| Backend API | ASP.NET Core |
| Cloud platform | Microsoft Azure |
| Testing | xUnit |
| CI/CD | GitHub Actions |

> Azure integration is optional and will be introduced after the local application is functional.

---

## Architecture

SystemPulse follows a modular architecture that separates system monitoring, application logic, data persistence, and the user interface.

```text
┌─────────────────────────────────────┐
│             Desktop UI              │
│             Avalonia                │
└──────────────────┬──────────────────┘
                   │
                   ▼
┌─────────────────────────────────────┐
│          Application Layer          │
│                                     │
│  Health Service                     │
│  Alert Service                      │
│  Recommendation Service             │
└──────────────────┬──────────────────┘
                   │
                   ▼
┌─────────────────────────────────────┐
│          Monitoring Layer           │
│                                     │
│  CPU Monitor                        │
│  Memory Monitor                     │
│  Disk Monitor                       │
│  Process Monitor                    │
└──────────────────┬──────────────────┘
                   │
                   ▼
┌─────────────────────────────────────┐
│       Platform Abstraction Layer    │
│                                     │
│  Linux System Metrics               │
│  Windows System Metrics             │
│  macOS System Metrics               │
└──────────────────┬──────────────────┘
                   │
                   ▼
┌─────────────────────────────────────┐
│          Infrastructure             │
│                                     │
│  SQLite                             │
│  Logging                            │
│  Configuration                      │
└─────────────────────────────────────┘
```

### Optional Cloud Architecture

```text
┌───────────────────────────────┐
│        SystemPulse            │
│        Desktop Client         │
└───────────────┬───────────────┘
                │
                ▼
┌───────────────────────────────┐
│       ASP.NET Core API        │
└───────────────┬───────────────┘
                │
                ▼
┌───────────────────────────────┐
│       Microsoft Azure         │
│                               │
│  Azure App Service            │
│  Azure SQL / Storage          │
│  Application Insights         │
└───────────────────────────────┘
```

---

## Project Structure

```text
SystemPulse/
│
├── src/
│   ├── SystemPulse.Core/
│   │   ├── Models/
│   │   ├── Interfaces/
│   │   └── Exceptions/
│   │
│   ├── SystemPulse.Application/
│   │   ├── Services/
│   │   ├── DTOs/
│   │   └── Interfaces/
│   │
│   ├── SystemPulse.Infrastructure/
│   │   ├── Monitoring/
│   │   ├── Persistence/
│   │   ├── Platform/
│   │   └── Configuration/
│   │
│   ├── SystemPulse.Desktop/
│   │   ├── Views/
│   │   ├── ViewModels/
│   │   └── Assets/
│   │
│   └── SystemPulse.Api/
│       ├── Controllers/
│       ├── Services/
│       └── Configuration/
│
├── tests/
│   ├── SystemPulse.Core.Tests/
│   ├── SystemPulse.Application.Tests/
│   └── SystemPulse.Infrastructure.Tests/
│
├── docs/
│   ├── architecture.md
│   ├── development.md
│   └── screenshots/
│
├── .github/
│   └── workflows/
│
├── .gitignore
├── LICENSE
├── README.md
└── SystemPulse.sln
```

---

## How It Works

SystemPulse periodically collects system performance metrics from the host operating system.

The monitoring pipeline follows these steps:

1. Discover running processes.
2. Collect CPU and memory measurements.
3. Collect system-wide resource metrics.
4. Normalize platform-specific data.
5. Store relevant measurements locally.
6. Evaluate configurable alert conditions.
7. Generate explainable recommendations.
8. Display the results in the desktop application.

### Example Alert

```text
SystemPulse Alert

High CPU usage detected.

Process: example-process
CPU Usage: 87%
Duration: 6 minutes

Observation:
The process has maintained elevated CPU usage
for an extended period.

Suggested actions:
- Check whether the process is performing a
  legitimate workload.
- Review active tasks or background operations.
- Investigate the process if its activity is unexpected.
```

SystemPulse does not automatically assume that high resource usage indicates malicious activity or a faulty application.

---

## Linux Monitoring

Linux is the primary development and testing platform.

SystemPulse may use Linux system interfaces such as:

- `/proc/stat` for CPU statistics.
- `/proc/meminfo` for memory statistics.
- `/proc/[pid]/stat` for process statistics.
- `/proc/[pid]/status` for process information.
- `/proc/[pid]/cmdline` for command-line information, subject to permissions.
- `/proc/[pid]/exe` for executable path information, subject to permissions.

Some information may be unavailable without elevated privileges.

The application should handle permission failures gracefully and should not require root privileges for ordinary monitoring.

---

## Roadmap

### Phase 1 — Minimum Viable Product

- [ ] Initialize .NET solution.
- [ ] Implement Linux CPU monitoring.
- [ ] Implement process discovery.
- [ ] Display per-process CPU usage.
- [ ] Display memory usage.
- [ ] Build initial Avalonia dashboard.
- [ ] Add configurable CPU thresholds.
- [ ] Add basic desktop notifications.

### Phase 2 — Local Application

- [ ] Add SQLite persistence.
- [ ] Add performance history.
- [ ] Add disk monitoring.
- [ ] Add process details.
- [ ] Add process exclusions.
- [ ] Add recommendation engine.
- [ ] Add application settings.
- [ ] Add structured logging.
- [ ] Add unit and integration tests.

### Phase 3 — Cross-Platform Support

- [ ] Isolate platform-specific monitoring code.
- [ ] Add Windows monitoring implementation.
- [ ] Add macOS monitoring implementation.
- [ ] Test platform-specific behavior.
- [ ] Improve packaging and installation.

### Phase 4 — Optional Azure Integration

- [ ] Build ASP.NET Core Web API.
- [ ] Implement secure authentication.
- [ ] Add cloud data storage.
- [ ] Add historical cloud analytics.
- [ ] Deploy API to Azure App Service.
- [ ] Configure Application Insights.
- [ ] Add optional remote dashboard.

---

## Design Principles

SystemPulse is guided by the following principles.

### Lightweight

The monitoring application should consume minimal system resources.

### Explainable

Recommendations should be based on observable metrics and understandable rules.

### Local-First

The core application should work without an internet connection.

### Privacy-Aware

System metrics should remain local by default.

Cloud synchronization should be optional and configurable.

### Cross-Platform

Platform-specific functionality should be isolated behind clear interfaces.

### Safe by Default

The application should not automatically terminate processes or modify system configuration without explicit user action.

### Testable

Core monitoring and recommendation logic should be independently testable.

---

## Development Setup

### Prerequisites

- .NET 10 SDK
- Git
- Linux development environment
- SQLite
- Avalonia development dependencies

### Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/SystemPulse.git

cd SystemPulse
```

### Build the Project

```bash
dotnet restore

dotnet build
```

### Run Tests

```bash
dotnet test
```

### Run the Application

```bash
dotnet run --project src/SystemPulse.Desktop
```

> The project is currently under development. Setup instructions may change as the architecture evolves.

---

## Testing

SystemPulse aims to maintain reliable monitoring and recommendation behavior through automated testing.

Testing areas include:

- CPU measurement calculations.
- Process discovery.
- Memory usage calculations.
- Threshold evaluation.
- Recommendation generation.
- Handling terminated processes.
- Handling inaccessible process information.
- Database persistence.
- Platform-specific behavior.

---

## Security and Privacy

SystemPulse is intended for monitoring systems that the user owns or is authorized to manage.

The application should:

- Avoid requiring unnecessary elevated privileges.
- Treat process information as potentially sensitive.
- Avoid uploading system information by default.
- Protect locally stored data where appropriate.
- Require explicit consent for cloud synchronization.
- Avoid automatically terminating processes.
- Clearly distinguish observations from security conclusions.

SystemPulse is a performance monitoring tool, not a malware detector or endpoint protection platform.

---

## Project Goals

The primary goals of SystemPulse are to:

1. Build a practical Linux-first system monitoring application.
2. Improve C# and .NET development skills.
3. Learn cross-platform systems programming.
4. Practice modular software architecture.
5. Explore desktop application development with Avalonia.
6. Implement reliable performance monitoring.
7. Develop explainable resource-management recommendations.
8. Gain practical experience with optional Azure integration.

---

## License

This project is licensed under the MIT License.

See the [LICENSE](LICENSE) file for details.

---

## Author

Built by Keletso Monyamane.

---

## Status

**Early Development**

SystemPulse is currently being designed and implemented.
