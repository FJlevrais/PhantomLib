```markdown
# PhantomLib

Simple Rayfield-style UI library for Roblox.

Has decent animations, theme support, FPS + Ping counter, and a gear icon to switch themes.

---

## Features

- Smooth animations (open, close, minimize)
- 4 themes: Default, Light, Cyber, Ocean
- Live FPS & Ping in the top bar
- Theme switcher (gear icon)
- Button, Toggle, Slider, Input, Color Picker
- Flags system
- Notifications
- Built-in Rejoin / ServerHop / JoinSmallServer
- Fully draggable

---

## How to use

### Load the library

```lua
local PhantomLib = loadstring(game:HttpGet("YOUR_RAW_LINK_HERE"))()
```

---

### Create a window

```lua
local Window = PhantomLib:CreateWindow({
    Name = "My Hub",
    Theme = "Default" -- Default, Light, Cyber, Ocean
})
```

You can also set a custom size if you want:

```lua
Size = UDim2.fromOffset(510, 315)
```

---

### Create tabs

```lua
local Main = Window:CreateTab("Main")
local Combat = Window:CreateTab("Combat")
local Settings = Window:CreateTab("Settings")
```

First tab gets selected automatically.

---

### Button

```lua
Main:CreateButton({
    Name = "Click Me",
    Callback = function()
        print("clicked")
    end
})
```

---

### Toggle

```lua
local MyToggle = Main:CreateToggle({
    Name = "Enable Feature",
    CurrentValue = false,
    Flag = "FeatureEnabled", -- optional
    Callback = function(Value)
        print(Value)
    end
})

-- You can also control it later
MyToggle:Set(true)
print(MyToggle:Get())
```

---

### Slider

```lua
Main:CreateSlider({
    Name = "WalkSpeed",
    Range = {16, 200},
    CurrentValue = 16,
    Suffix = "", -- optional
    Flag = "WalkSpeed",
    Callback = function(Value)
        local hum = game.Players.LocalPlayer.Character and game.Players.LocalPlayer.Character:FindFirstChild("Humanoid")
        if hum then
            hum.WalkSpeed = Value
        end
    end
})
```

---

### Input

```lua
Main:CreateInput({
    Name = "Player Name",
    CurrentValue = "",
    PlaceholderText = "Enter name...",
    Flag = "TargetName",
    Callback = function(Text)
        print(Text)
    end
})
```

---

### Color Picker

```lua
Main:CreateColorPicker({
    Name = "ESP Color",
    Color = Color3.fromRGB(255, 0, 0),
    Flag = "ESPColor",
    Callback = function(Color)
        print(Color)
    end
})
```

---

### Notifications

```lua
Window:Notify({
    Title = "Success",
    Content = "Something happened",
    Duration = 3
})
```

---

### Utility functions

```lua
Window:Rejoin()
Window:ServerHop()
Window:JoinSmallServer()
```

---

### Flags

When you set a `Flag` on an element, the value gets saved in `Window.Flags`.

```lua
print(Window.Flags["WalkSpeed"])
print(Window.Flags["FeatureEnabled"])
print(Window.Flags["TargetName"])
```

Useful if you don’t want to keep variables for every toggle/slider.

---

### Themes

Available themes:
- Default
- Light
- Cyber
- Ocean

You can set it when creating the window, or just click the gear icon in the top right to change it anytime.

---

## Full Example

```lua
local PhantomLib = loadstring(game:HttpGet("YOUR_LINK"))()

local Window = PhantomLib:CreateWindow({
    Name = "Example Hub",
    Theme = "Default"
})

local Main = Window:CreateTab("Main")
local Misc = Window:CreateTab("Misc")

Main:CreateToggle({
    Name = "Speed Hack",
    CurrentValue = false,
    Flag = "SpeedEnabled",
    Callback = function(Value)
        -- your code here
    end
})

Main:CreateSlider({
    Name = "Speed Amount",
    Range = {16, 150},
    CurrentValue = 16,
    Flag = "SpeedValue",
    Callback = function(Value)
        local char = game.Players.LocalPlayer.Character
        if char and char:FindFirstChild("Humanoid") then
            char.Humanoid.WalkSpeed = Value
        end
    end
})

Main:CreateButton({
    Name = "Test Notify",
    Callback = function()
        Window:Notify({
            Title = "Test",
            Content = "Notification is working",
            Duration = 2.5
        })
    end
})

Misc:CreateButton({
    Name = "Rejoin",
    Callback = function()
        Window:Rejoin()
    end
})

Misc:CreateButton({
    Name = "Server Hop",
    Callback = function()
        Window:ServerHop()
    end
})

Misc:CreateButton({
    Name = "Small Server",
    Callback = function()
        Window:JoinSmallServer()
    end
})
```

---

## Notes

- Always check if Character/Humanoid exists inside callbacks so it doesn’t error.
- Closing the UI turns all toggles off automatically.
- Pretty straightforward to use overall.
```
