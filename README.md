# Plubox plugin for Claude Code

Connects Claude Code to your [Plubox](https://plubox.com) account through the
remote Plubox MCP server (`https://control.plubox.com/mcp/plubox`).

Plubox is a property-management platform for short-term and long-term rentals.
With this plugin Claude can read your organizations, bookings, payments,
schedules, nightly and long-term prices, stored Booking.com and Airbnb market
data, expenses, utility payments, tasks, cleanings, and statistics, and make
bounded operational and financial changes after explicit confirmation.

## Requirements

- A Plubox account with access to at least one organization
  (sign in at <https://admin.plubox.com>).
- Claude Code with plugin support.

No API keys are stored in this plugin. Authentication uses OAuth 2.0 with PKCE:
on first use Claude Code opens the Plubox authorization page in your browser,
you sign in and grant the `mcp:use` scope, and the token stays on your machine.

## Installation

From the Claude Code plugin directory (once listed):

```
/plugin install plubox@claude-community
```

Or straight from this repository while it is not yet listed:

```
/plugin marketplace add Plubox/plubox-claude-plugin
/plugin install plubox@plubox
```

Without the plugin system, the same server can be added directly:

```
claude mcp add --transport http plubox https://control.plubox.com/mcp/plubox
```

## What Claude can do

Read-only tools:

- `list-organizations`, `search-accommodations`, `search-expense-references`,
  `search-task-references`
- `list-bookings`, `list-booking-payments`, `get-schedule`, `get-calendar`,
  `list-availability-dates`, `get-inventory-calendar`, `list-cleanings`
- `get-accommodation-market-analytics` (stored Booking.com market availability
  and Airbnb competitors for an accommodation group)
- `list-long-term-rental-periods`, `list-expenses`, `list-utility-payments`,
  `list-tasks`, `list-equipment-shortages`, `get-statistics`

Write tools (Claude asks for confirmation before calling them):

- `update-booking`, `bulk-update-bookings`
- `add-booking-payment`, `update-booking-payment`
- `update-inventory-price`
- `create-long-term-rental-period`, `update-long-term-rental-period`,
  `delete-long-term-rental-period`
- `add-expense`, `delete-expense`
- `add-utility-payment`, `update-utility-payment`
- `add-task`, `update-task`

Every tool is scoped to the organizations your Plubox user can access. IDs are
always resolved through search or list tools first; the server never accepts
guessed identifiers. Booking deletion is not available.

## Example prompts

- "Show tomorrow's schedule for organization X and which bookings still owe a
  balance."
- "Compare apartment 24 occupancy and nightly rates for the next 7 days with
  Booking.com market availability and Airbnb competitors, and recommend price
  actions."
- "Add a 1450 UAH utility payment for electricity for apartment 12, paid today
  via the cash gateway."
- "Find the three bookings arriving on 2026-10-10 and, after I confirm, set
  check-in time to 17:30 for all of them."

## Privacy and support

The server only reads and writes data inside the authenticated user's Plubox
organizations. Some write tools may trigger notifications to organization
members or synchronization to connected channel managers and websites; the tool
descriptions state this explicitly.

- Privacy policy: <https://plubox.com/privacy>
- Terms: <https://plubox.com/terms>
- Support: <https://plubox.com/support> or office@plubox.com

## License

Apache-2.0. See [LICENSE](LICENSE).
