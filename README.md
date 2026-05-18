local repo = "https://raw.githubusercontent.com/deividcomsono/Obsidian/main/"
local Library = loadstring(game:HttpGet(repo .. "Library.lua"))()

-- ======================== UI DEFINITION ========================
local Window = Library:CreateWindow({
    Title = "Lxcid",
    Footer = "v1.0",
    Icon = "rbxassetid://75573698952528",
    NotifySide = "Right",
    ShowCustomCursor = true,
})

local function enlargeIcon()
    for _, gui in ipairs(game:GetService("CoreGui"):GetChildren()) do
        if gui:IsA("ScreenGui") then
            for _, obj in ipairs(gui:GetDescendants()) do
                if obj:IsA("ImageLabel") and obj.Image == "rbxassetid://75573698952528" then
                    obj.Size = UDim2.new(0, 45, 0, 45)
                    obj.Position = UDim2.new(0, 8, 0.5, -22)
                    return
                end
            end
        end
    end
end
task.spawn(function() task.wait(0.2) enlargeIcon() end)

local Tabs = {
    Main = Window:AddTab("Main", "crosshair"),
    Rage = Window:AddTab("Rage", "zap"),
    Visuals = Window:AddTab("Visuals", "eye"),
    Settings = Window:AddTab("Settings", "settings"),
}

-- ======================== UI ELEMENTS ========================

-- Main Tab (unchanged)
local MainGroup = Tabs.Main:AddLeftGroupbox("Camlock", "")
MainGroup:AddToggle("Enabled", { Text = "Enabled", Default = false })
MainGroup:AddToggle("StickyAim", { Text = "Sticky Aim", Default = false })

MainGroup:AddToggle("Humanizer", { Text = "Humanizer", Default = false })
MainGroup:AddSlider("HumanizerMinSpeed", { Text = "Min Speed", Default = 0.06, Min = 0.01, Max = 1, Rounding = 3 })
MainGroup:AddSlider("HumanizerMaxSpeed", { Text = "Max Speed", Default = 0.09, Min = 0.01, Max = 1, Rounding = 3 })
MainGroup:AddSlider("HumanizerAcceleration", { Text = "Acceleration", Default = 0.013, Min = 0.001, Max = 0.1, Rounding = 3 })
MainGroup:AddSlider("HumanizerHOffset", { Text = "Horizontal Offset", Default = 0.20, Min = 0, Max = 2, Rounding = 2 })
MainGroup:AddSlider("HumanizerVOffset", { Text = "Vertical Offset", Default = 0.15, Min = 0, Max = 2, Rounding = 2 })
MainGroup:AddSlider("HumanizerChangeInterval", { Text = "Change Interval", Default = 0.30, Min = 0.1, Max = 2, Rounding = 2 })

local FlickGroup = Tabs.Main:AddLeftGroupbox("System", "")
FlickGroup:AddToggle("Flick_Enabled", { Text = "Enabled", Default = false })
FlickGroup:AddSlider("CameraSmoothness", { Text = "Camera Smoothness", Default = 0.9, Min = 0, Max = 1, Rounding = 2, Suffix = "" })
FlickGroup:AddToggle("Resolver", { Text = "Resolver", Default = false })
FlickGroup:AddSlider("HitChance", { Text = "Silent Aim Hit Chance", Default = 100, Min = 0, Max = 100, Rounding = 0, Suffix = "%" })
FlickGroup:AddSlider("AntiCurve", { Text = "Anti Curve", Default = 0, Min = 0, Max = 100, Rounding = 0, Suffix = "%" })
FlickGroup:AddDropdown("EasingStyle", { Text = "Easing Style", Values = { "Sine", "Linear", "Quad", "Cubic", "Quart" }, Default = "Sine" })
FlickGroup:AddDropdown("EasingDirection", { Text = "Easing Direction", Values = { "Out", "In", "InOut" }, Default = "Out" })
FlickGroup:AddToggle("LookAt", { Text = "Look At", Default = false })
FlickGroup:AddToggle("AntiAimViewer", { Text = "Anti Aim Viewer", Default = false })
FlickGroup:AddToggle("AutoAir", { Text = "Auto Air", Default = false })
FlickGroup:AddSlider("AutoAirDelay", { Text = "Auto Air Delay", Default = 0.22, Min = 0, Max = 1, Rounding = 2, Suffix = "" })
FlickGroup:AddDropdown("LockMethod", { Text = "Lock Method", Values = { "Index", "Namecall" }, Default = "Index" })

local GunGroup = Tabs.Main:AddLeftGroupbox("Gun Modification", "")
GunGroup:AddToggle("RapidFire", { Text = "Rapid Fire", Default = false })
GunGroup:AddSlider("RapidFireDelay", { Text = "Rapid Fire Delay", Default = 0.04, Min = 0, Max = 1, Rounding = 2, Suffix = "" })

local HitGroup = Tabs.Main:AddLeftGroupbox("Hit Part", "")
HitGroup:AddDropdown("AimPart", {
    Text = "Aim Part", Values = { "HumanoidRootPart", "Head", "UpperTorso", "LowerTorso", "RightFoot", "LeftFoot" },
    Default = "Head", Multi = false
})
HitGroup:AddDropdown("AirAimPart", {
    Text = "Air Aim Part", Values = { "HumanoidRootPart", "Head", "UpperTorso", "LowerTorso", "RightFoot", "LeftFoot" },
    Default = "HumanoidRootPart", Multi = false
})

local SilentAimGroup = Tabs.Main:AddRightGroupbox("Silent Aim", "")
SilentAimGroup:AddToggle("SilentAim", { Text = "Silent Aim", Default = false })

local PredictionGroup = Tabs.Main:AddRightGroupbox("Prediction", "")
PredictionGroup:AddSlider("HorizontalPrediction", { Text = "Horizontal Prediction", Default = 0.134, Min = 0, Max = 1, Rounding = 2, Suffix = "" })
PredictionGroup:AddSlider("VerticalPrediction", { Text = "Vertical Prediction", Default = 0.134, Min = 0, Max = 1, Rounding = 2, Suffix = "" })
PredictionGroup:AddToggle("AutoPred", { Text = "AutoPred", Default = false })

local ChecksGroup = Tabs.Main:AddRightGroupbox("Checks", "")
ChecksGroup:AddToggle("KnockOut", { Text = "KnockOut", Default = false })
ChecksGroup:AddToggle("Wall", { Text = "Wall", Default = false })
ChecksGroup:AddToggle("Friend", { Text = "Friend", Default = false })
ChecksGroup:AddToggle("Team", { Text = "Team", Default = false })

-- ======================== RAGE TAB – ANTI LOCK (DESYNC ONLY) ========================
local AntiLockGroup = Tabs.Rage:AddLeftGroupbox("Anti Lock", "")
AntiLockGroup:AddToggle("EnableAntiLock", { Text = "Enable Anti Lock", Default = false })
AntiLockGroup:AddToggle("AntiNetwork", { Text = "Anti Network", Default = false })
AntiLockGroup:AddToggle("P1000Desync", { Text = "P1000 Desync", Default = false })

local CFrameGroup = Tabs.Rage:AddLeftGroupbox("CFrame", "")
CFrameGroup:AddToggle("LoadCFrame", { Text = "CFrame", Default = false })
CFrameGroup:AddSlider("CFrame_SpeedPercent", { Text = "Speed", Default = 3, Min = 0, Max = 100, Rounding = 0, Suffix = "%" })

-- Visuals Tab
local VisualsGlobalGroup = Tabs.Visuals:AddLeftGroupbox("Global", "")
VisualsGlobalGroup:AddToggle("BoxCorners", { Text = "Box Corners", Default = false })
VisualsGlobalGroup:AddSlider("BoxWidth", { Text = "Box Width", Default = 2, Min = 0, Max = 10, Rounding = 0 })
VisualsGlobalGroup:AddSlider("BoxHeight", { Text = "Box Height", Default = 2, Min = 0, Max = 10, Rounding = 0 })
VisualsGlobalGroup:AddToggle("HealthBarEnabled", { Text = "Health Bar", Default = false })
VisualsGlobalGroup:AddToggle("NameEnabled", { Text = "Name", Default = false })

-- Settings Tab
local KeybindsGroup = Tabs.Settings:AddLeftGroupbox("Keybinds", "")
KeybindsGroup:AddLabel("Lock Keybind"):AddKeyPicker("LockKeybind", { Default = "End", Mode = "Toggle", NoUI = true, Text = "Lock Keybind" })

local CameraGroup = Tabs.Settings:AddLeftGroupbox("Camera", "")
CameraGroup:AddSlider("FieldOfView", { Text = "Field Of View", Default = 80, Min = 1, Max = 120, Rounding = 0 })

-- ======================== WAIT FOR UI ========================
task.wait(0.5)
local Options = Library.Options
local Toggles = Library.Toggles
