local main = Instance.new("ScreenGui")
local Frame = Instance.new("Frame")
local up = Instance.new("TextButton")
local down = Instance.new("TextButton")
local onof = Instance.new("TextButton")
local TextLabel = Instance.new("TextLabel")
local plus = Instance.new("TextButton")
local speed = Instance.new("TextLabel")
local mine = Instance.new("TextButton")
local closebutton = Instance.new("TextButton")
local mini = Instance.new("TextButton")
local mini2 = Instance.new("TextButton")

main.Name = "main"
main.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")
main.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
main.ResetOnSpawn = false

Frame.Parent = main
Frame.BackgroundColor3 = Color3.fromRGB(0, 50, 0)
Frame.BorderColor3 = Color3.fromRGB(0, 100, 0)
Frame.Position = UDim2.new(0.1, 0, 0.38, 0)
Frame.Size = UDim2.new(0, 190, 0, 57)

up.Name = "up"
up.Parent = Frame
up.BackgroundColor3 = Color3.fromRGB(0, 75, 0)
up.Size = UDim2.new(0, 44, 0, 28)
up.Font = Enum.Font.SourceSans
up.Text = "UP"
up.TextColor3 = Color3.fromRGB(255, 255, 255)
up.TextSize = 14

down.Name = "down"
down.Parent = Frame
down.BackgroundColor3 = Color3.fromRGB(0, 75, 0)
down.Position = UDim2.new(0, 0, 0.49, 0)
down.Size = UDim2.new(0, 44, 0, 28)
down.Font = Enum.Font.SourceSans
down.Text = "DOWN"
down.TextColor3 = Color3.fromRGB(255, 255, 255)
down.TextSize = 14

onof.Name = "onof"
onof.Parent = Frame
onof.BackgroundColor3 = Color3.fromRGB(0, 100, 0)
onof.Position = UDim2.new(0.7, 0, 0.49, 0)
onof.Size = UDim2.new(0, 56, 0, 28)
onof.Font = Enum.Font.SourceSans
onof.Text = "Fly"
onof.TextColor3 = Color3.fromRGB(255, 255, 255)
onof.TextSize = 14

TextLabel.Parent = Frame
TextLabel.BackgroundColor3 = Color3.fromRGB(0, 80, 0)
TextLabel.Position = UDim2.new(0.47, 0, 0, 0)
TextLabel.Size = UDim2.new(0, 100, 0, 28)
TextLabel.Font = Enum.Font.SourceSans
TextLabel.Text = "FLY GUI"
TextLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
TextLabel.TextScaled = true
TextLabel.TextWrapped = true

plus.Name = "plus"
plus.Parent = Frame
plus.BackgroundColor3 = Color3.fromRGB(0, 75, 0)
plus.Position = UDim2.new(0.23, 0, 0, 0)
plus.Size = UDim2.new(0, 45, 0, 28)
plus.Font = Enum.Font.SourceSans
plus.Text = "+"
plus.TextColor3 = Color3.fromRGB(255, 255, 255)
plus.TextSize = 14

speed.Name = "speed"
speed.Parent = Frame
speed.BackgroundColor3 = Color3.fromRGB(0, 100, 0)
speed.Position = UDim2.new(0.47, 0, 0.49, 0)
speed.Size = UDim2.new(0, 44, 0, 28)
speed.Font = Enum.Font.SourceSans
speed.Text = "1"
speed.TextColor3 = Color3.fromRGB(255, 255, 255)
speed.TextScaled = true
speed.TextSize = 14

mine.Name = "mine"
mine.Parent = Frame
mine.BackgroundColor3 = Color3.fromRGB(0, 75, 0)
mine.Position = UDim2.new(0.23, 0, 0.49, 0)
mine.Size = UDim2.new(0, 45, 0, 29)
mine.Font = Enum.Font.SourceSans
mine.Text = "-"
mine.TextColor3 = Color3.fromRGB(255, 255, 255)
mine.TextSize = 14

closebutton.Name = "Close"
closebutton.Parent = main
closebutton.BackgroundColor3 = Color3.fromRGB(225, 25, 0)
closebutton.Font = Enum.Font.SourceSans
closebutton.Size = UDim2.new(0, 45, 0, 28)
closebutton.Text = "X"
closebutton.TextSize = 30
closebutton.Position = UDim2.new(0, 0, -1, 27)

mini.Name = "minimize"
mini.Parent = main
mini.BackgroundColor3 = Color3.fromRGB(192, 150, 230)
mini.Font = Enum.Font.SourceSans
mini.Size = UDim2.new(0, 45, 0, 28)
mini.Text = "-"
mini.TextSize = 40
mini.Position = UDim2.new(0, 44, -1, 27)

mini2.Name = "minimize2"
mini2.Parent = main
mini2.BackgroundColor3 = Color3.fromRGB(192, 150, 230)
mini2.Font = Enum.Font.SourceSans
mini2.Size = UDim2.new(0, 45, 0, 28)
mini2.Text = "+"
mini2.TextSize = 40
mini2.Position = UDim2.new(0, 44, -1, 57)
mini2.Visible = false

local speeds = 1
local flying = false
local speaker = game.Players.LocalPlayer

local function toggleFly()
    local char = speaker.Character
    if char then
        local humanoid = char:FindFirstChildOfClass("Humanoid")
        if flying then
            flying = false
            humanoid.PlatformStand = false
        else
            flying = true
            humanoid.PlatformStand = true
            local bodyGyro = Instance.new("BodyGyro", char.HumanoidRootPart)
            local bodyVelocity = Instance.new("BodyVelocity", char.HumanoidRootPart)
            bodyGyro.P = 9e4
            bodyGyro.MaxTorque = Vector3.new(9e9, 9e9, 9e9)
            bodyGyro.CFrame = char.HumanoidRootPart.CFrame
            bodyVelocity.Velocity = Vector3.new(0, 0, 0)
            bodyVelocity.MaxForce = Vector3.new(9e9, 9e9, 9e9)

            while flying do
                bodyGyro.CFrame = workspace.CurrentCamera.CFrame
                bodyVelocity.Velocity = Vector3.new(0, 50 * speeds, 0) -- Flying upwards
                wait(0.1)
            end

            bodyGyro:Destroy()
            bodyVelocity:Destroy()
        end
    end
end

up.MouseButton1Click:Connect(function()
    if flying then
        local char = speaker.Character
        if char then
            char:Move(Vector3.new(0, speeds, 0)) -- Move up
        end
    end
end)

down.MouseButton1Click:Connect(function()
    if flying then
        local char = speaker.Character
        if char then
            char:Move(Vector3.new(0, -speeds, 0)) -- Move down
        end
    end
end)

onof.MouseButton1Click:Connect(function()
    toggleFly()
    onof.Text = flying and "Stop" or "Fly"
end)

plus.MouseButton1Click:Connect(function()
    speeds = speeds + 1
    speed.Text = tostring(speeds)
end)

mine.MouseButton1Click:Connect(function()
    if speeds > 1 then
        speeds = speeds - 1
        speed.Text = tostring(speeds)
    end
end)

closebutton.MouseButton1Click:Connect(function()
    main:Destroy()
end)

mini.MouseButton1Click:Connect(function()
    Frame.Visible = false
    mini.Visible = false
    mini2.Visible = true
end)

mini2.MouseButton1Click:Connect(function()
    Frame.Visible = true
    mini.Visible = true
    mini2.Visible = false
end)

game:GetService("StarterGui"):SetCore("SendNotification", { 
    Title = "FLY GUI";
    Text = "BY CASHIER";
    Icon = "rbxthumb://type=Asset&id=5107182114&w=150&h=150"
})
