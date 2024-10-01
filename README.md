# Wezterm Battery Module

A battery module for Wezterm that provides information about battery status,
including charge levels and remaining time.

This module is designed to enhance your terminal experience by
displaying battery statistics in a visually appealing way.

## Features

- Display battery icons based on charge levels.
- Show the remaining time for charging or discharging batteries.
- Color-coded battery status for better visibility.
- Option to invert colors for light backgrounds.

## Installation

To use this module in your WezTerm configuration, include it as a plugin:

```lua
local wezterm = require("wezterm")
local config = wezterm.config_builder()
local battery = wezterm.plugin.require("https://github.com/rootiest/battery.wez")
battery.invert = true -- Optionally invert the color brightness
battery.apply_to_config(config) -- Optionally apply the necessary config settings
```

## Usage

### Get Battery Information

You can get detailed battery information using the following functions:

- **`get_batteries()`**:
Returns a list of battery components with their current status.
  
  ```lua
  local batteries = battery.get_batteries()
  for _, b in ipairs(batteries) do
      print(b.battery.percentage)  -- Prints battery percentages
  end
  ```

- **`get_battery_icons()`**:
Returns a formatted string containing icons for all batteries.

  ```lua
  local icons = battery.get_battery_icons()
  print(icons)  -- Prints battery icons
  ```

- **`get_battery_stats()`**:
Returns a formatted string containing the statistics of all batteries.

  ```lua
  local stats = battery.get_battery_stats()
  print(stats)  -- Prints battery stats
  ```

### Configuration Options

You can set the `invert` option to change the color brightness
of the battery icons/text to match your terminal's background:

```lua
battery.invert = true  -- Enable color brightness inversion
```

## Applications

### tabline.wez

To use the battery module in the `tabline.wez` plugin, use the following method:

```lua
local wezterm = require("wezterm")
local tabline = wezterm.plugin.require("https://github.com/michaelbrusegard/tabline.wez")

local battery = wezterm.plugin.require("https://github.com/rootiest/battery.wez")
battery.invert = true -- Optionally invert the color brightness

tabline.setup({
  -- etc
  sections = {
    -- etc
    tabline_z = {
      batteries.get_battery_icons,
    },
  },
})
```

This will add the battery icons to the end of the tabline.

### Native tab-bar

To use the battery module in the native tab-bar, use the following method:

```lua
local wezterm = require("wezterm")
local config = wezterm.config_builder()

local battery = wezterm.plugin.require("https://github.com/rootiest/battery.wez")
battery.apply_to_config(config) -- Optionally apply the necessary config settings

wezterm.on("update-right-status", function(window, _)
  window:set_right_status(battery.get_battery_icons())
end)
```

This will add the battery icons to the right status bar.

## API Reference

### Module: `battery`

- **`invert`**: (boolean) Whether to invert colors.

- **`get_batteries()`**: Returns a list of battery components.
  
- **`get_battery_icons()`**: Returns a formatted string of battery icons.
  
- **`get_battery_stats()`**: Returns a formatted string of battery statistics.
  
- **`apply_to_config(config)`**: Applies plugin configuration to the WezTerm config.

## License

This project is licensed under the MIT License.
See the [LICENSE](LICENSE) file for more details.
