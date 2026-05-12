# LogPlus ListEner

A lightweight, real-time log visualization dashboard that displays structured log data in customizable lists.

*(Doc generated with AI)*

## Features

- **Real-time Updates**: Auto-refresh from HTTP API endpoints at configurable intervals
- **Dynamic Lists**: Create and manage multiple log lists with custom styling
- **Dark Mode**: Toggle between light and dark themes
- **Customizable Display**: Configure colors, fonts, sizes, and layout per list or message
- **Message Management**: Automatic message limits, prepend/append modes, and manual deletion
- **State Persistence**: Download and load dashboard state as JSON
- **Responsive Layout**: Grid-based layout with configurable column widths and heights

## Quick Start

1. Open `index.html` in a web browser
2. Configure your API endpoint (default: `http://localhost:4040/data`)
3. Set refresh interval in milliseconds (default: 3000ms)
4. Click **Refresh** or enable **Auto-Refresh**

## API Format

The application expects a JSON array of command objects:

### List Command
```json
{
  "type": "list",
  "id": "list1",
  "name": "System Logs",
  "rows": 4,
  "columns": 6,
  "list_color": "#ffffff",
  "list_background_color": "#3273dc",
  "color": "#333333",
  "background_color": "#f0f0f0",
  "font_size": 14,
  "add_mode": "append",
  "max_messages": 100
}
```

**Parameters:**
- `type`: `"list"` (required)
- `id`: Unique identifier (auto-generated if omitted)
- `name`: Display name (defaults to `id`)
- `rows`: Column width (1-12, default: 3)
- `columns`: Height multiplier (default: 5, each unit = 50px)
- `list_color`: Header text color
- `list_background_color`: Header background color
- `color`: Default message text color
- `background_color`: Default message background color
- `font_size`: Default message font size in pixels
- `add_mode`: `"append"` or `"prepend"` (default: append)
- `max_messages`: Maximum messages to retain (default: 200)
- `remove`: Set to `true` to delete the list

### Message Command

```json
{
  "type": "message",
  "list": "list1",
  "id": "msg1",
  "name": "Application",
  "content": "Server started successfully",
  "color": "#00ff00",
  "background_color": "#1a1a1a",
  "font_size": 16
}
```

**Parameters:**
- `type`: `"message"` (required)
- `list`: Target list ID (required, creates list if missing)
- `id`: Unique identifier (auto-generated if omitted)
- `name`: Message title/source
- `content`: Message body (supports `\n` for line breaks)
- `color`: Text color (overrides list default)
- `background_color`: Background color (overrides list default)
- `font_size`: Font size in pixels (overrides list default)
- `remove`: Set to `true` to delete the message (requires `id`)

## Example API Response

```json
[
  {
"type": "list",
"id": "errors",
"name": "Error Log",
"rows": 6,
"columns": 8,
"list_background_color": "#da3633",
"add_mode": "prepend",
"max_messages": 50
  },
  {
"type": "message",
"list": "errors",
"name": "Database",
"content": "Connection timeout after 30s",
"background_color": "#2e1616"
  },
  {
"type": "message",
"list": "errors",
"name": "API",
"content": "Rate limit exceeded\nRetrying in 60s"
  }
]
```

## Controls

- **Theme Toggle**: Switch between light and dark mode
- **Auto-Refresh**: Start/stop automatic polling
- **Download**: Export current state as JSON
- **Load**: Import previously saved state
- **Delete Buttons**: Remove individual lists or messages (hover to reveal)

## Local Storage

The application persists:
- Theme preference (`darkMode`)
- API URL (`apiUrl`)
- Refresh interval (`refreshInterval`)

## Dependencies

- [Bulma CSS](https://bulma.io/) - UI framework
- [Alpine.js](https://alpinejs.dev/) - Reactive framework

Both are loaded from local files (`bulma.min.css`, `alpine.min.js`).

## Browser Compatibility

Requires a modern browser with ES6+ support and Fetch API.

## License

MIT
