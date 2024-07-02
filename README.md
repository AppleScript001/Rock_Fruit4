local Library = loadstring(game:HttpGet("https://pastebin.com/raw/KNBp0LRy"), "Coastified UI")()
repeat wait() until game:IsLoaded()
game:GetService("Players").LocalPlayer.Idled:connect(function()
game:GetService("VirtualUser"):ClickButton2(Vector2.new())
end)
local Window = Library:NewWindow("Rock Fruit 2")

local Section = Window:NewSection("AutoFarm")

local Mobs_Table = {}
for _, v in ipairs(workspace.Mob:GetDescendants()) do
    if v:IsA("Model") and v:FindFirstChild("HumanoidRootPart") and not table.find(Mobs_Table, v.Name) then
        table.insert(Mobs_Table, v.Name)
        table.sort(Mobs_Table)
    end
end

local PlayerTP1
local TweenService = game:GetService("TweenService")

local Dropdown = Section:CreateDropdown("Select Mobs!", Mobs_Table, 0, function(t)
    PlayerTP1 = t
end)
local Dropdown = Section:CreateDropdown("Select Weapon!", {"Combat", "Katana"}, 0, function(t)
    Weapon = t
end)
local Toggle = Section:CreateToggle("Auto [Mobs]", function(Value)
_G.Attack = Value
while _G.Attack do
task.wait(1)  -- Wait for 1 second before checking for enemies
pcall(function()
for i,v in pairs(workspace.Mob:GetDescendants()) do
if v.Name == PlayerTP1 then
if v.Humanoid.Health > 0 then
repeat
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame * CFrame.new(0,0,5)
wait()  -- Wait a short time before checking again
until not _G.Attack or v.Humanoid.Health <= 0
end
end
end
end)
end
end)
local Toggle = Section:CreateToggle("Auto [Click]", function(Value)
_G.weapon = Value
while _G.weapon do
wait()  -- Wait for 1 second before checking for enemies
local toolName = Weapon -- Replace "YourToolNameHere" with the name of your tool
    
local LocalPlayer = game:GetService("Players").LocalPlayer
for i, v in pairs(LocalPlayer.Backpack:GetChildren()) do
if v:IsA('Tool') and v.Name == toolName then
    v.Parent = LocalPlayer.Character
    break -- Stop the loop after picking up the tool
end
end
LocalPlayer.Character:FindFirstChild(toolName):Activate()
end
end)
