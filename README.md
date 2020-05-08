# mtdebug [WIP]

Light-weight, intuitive profiler API for Minetest mods. This mod is intended to be used
for debugging purposes, and isn't recommended to be used in release/production environments!

The recommended way to use this API is to profile segments of code using the
`mtdebug.profile_start` and `mtdebug.profile_end` methods, and posting the results to
the profiler HUD using the `mtdebug.hud_post` method. However, mods can certainly post
custom string values to the profiler HUD if so required. The API methods are not too
computationally-expensive, and can even be used in globalsteps (with caution, of course).

## API Methods

### `mtdebug.profile_start(name)`

- Starts profiling a segment of code.
- `name` [string]: Name of the profiling session; needs to be unique.
  - Throws an error if the name isn't unique.

### `mtdebug.profile_end(name)`

- Ends an active profiling session
- Returns the duration of the profiling session in seconds.
- `name` [string]: Name of the profiling session to end.
  - Throws an error if there isn't an profiling session associated with the name.

### `mtdebug.hud_post(name, value)`

- Creates new/updates existing profiler entry.
- `name` [string]: Name of a new/existing entry.
- `value` [string]: Value of the entry; can be any arbitrary string.
  - Boolean and numeric values are automatically converted to strings.

## Chat-commands

### `/mod_profiler`

- Toggles mod profiler HUD for the caller.

## Example code

The following is the recommended way to profile a segment of code:

```lua
local function fishy_business()
	mtdebug.profile_start("mymod:fishy_business")

	-- Your fishy business here

	local elapsed = mtdebug.profile_end("mymod:fishy_business")
	mtdebug.hud_post("fishy_business", elapsed)
end
```
