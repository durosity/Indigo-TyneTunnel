# Tyne Tunnel Indigo Plugin

An [Indigo](https://www.indigodomo.com) plugin for monitoring your [TT2 Pre-Paid account](https://www.tt2.co.uk/pre-paid-account/) balance and status.

## Features

- Displays your current pre-paid account balance (in pence and formatted £ value)
- Configurable low balance alert state for use in Indigo triggers
- Configurable polling interval (10 minutes to 6 hours)
- Automatic JWT token refresh — re-authenticates seamlessly without storing session data between restarts
- Manual refresh action available
- Multiple accounts supported (one device per account)

## Requirements

- Indigo 2022.1 or later
- A TT2 Pre-Paid account ([sign up here](https://account.tt2.co.uk/sign-up))
- Python 3 (provided by Indigo)

## Installation

1. Download the latest release zip from the [Releases](../../releases) page
2. Unzip and double-click `TyneTunnel.indigoPlugin` to install
3. Indigo will install the required `requests` dependency automatically

## Setup

1. In Indigo, go to **Plugins → Tyne Tunnel → Enable**
2. Create a new device and select **TT2 Account** as the device type
3. Enter your TT2 account email address and password
4. Choose a polling interval (default: every 30 minutes)
5. Optionally set a low balance threshold in pence (default: 1000p = £10.00)

## Device States

| State | Type | Description |
|-------|------|-------------|
| `displayState` | String | Formatted balance (e.g. `£12.50`) — shown in device list |
| `balance` | Number | Balance in pence (e.g. `1250`) |
| `balancePounds` | String | Formatted balance string (e.g. `£12.50`) |
| `accountLabel` | String | Account label as set in TT2 portal |
| `accountReference` | String | TT2 account reference number |
| `lowBalance` | Boolean | `true` when balance is below the configured threshold |
| `lastUpdated` | String | Timestamp of last successful update |
| `status` | String | `OK` or error description |

## Actions

| Action | Description |
|--------|-------------|
| Refresh Account | Forces an immediate balance update outside of the polling schedule |

## Automation Ideas

- **Low balance notification** — trigger a notification or announcement when `lowBalance` becomes `true`
- **Top-up reminder** — use `balance` in a condition to alert when you're getting close to running low
- **Journey logging** — poll frequently and log `lastUpdated` changes to track tunnel usage patterns

## Notes

- Balance values are stored in **pence** (GBP) to avoid floating point issues. Divide by 100 for pounds.
- The plugin uses TT2's GraphQL API at `api.tt2.co.uk`. This is not an official public API — if TT2 change their portal, the plugin may need updating.
- Credentials are stored locally in Indigo's device configuration. The password field is masked in the UI.

## License

MIT License — see [LICENSE](LICENSE) for details.

## Author

[Durosity](https://github.com/Durosity)
