local player = game.Players.LocalPlayer
local starterGui = player:WaitForChild("PlayerGui")
local userInputService = game:GetService("UserInputService")

local titik1 = CFrame.new(-0.120088317, 5.92626429, 94.1715393, -0.987688184, 0.0193536859, -0.155233592, -6.64643673e-09, 0.992317557, 0.123716839, 0.156435385, 0.122193664, -0.980100334)
local titik2 = CFrame.new(53.7295532, 524.085571, -195.608505, -0.0581439883, 0.175470933, -0.982766092, -1.55020139e-08, 0.984431565, 0.175768301, 0.998308182, 0.010219885, -0.0572387725)

local screenGui = Instance.new("ScreenGui")
screenGui.Name = "TenkaHubGui"
screenGui.ResetOnSpawn = false
screenGui.Parent = starterGui

local mainFrame = Instance.new("Frame")
mainFrame.Name = "MainFrame"
mainFrame.Size = UDim2.new(0, 220, 0, 110)
mainFrame.Position = UDim2.new(0.5, -110, 0.5, -55) -- Pas di tengah layar kamu!
mainFrame.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
mainFrame.BorderSizePixel = 1
mainFrame.BorderColor3 = Color3.fromRGB(255, 255, 255)
mainFrame.Parent = screenGui

local mainCorner = Instance.new("UICorner")
mainCorner.CornerRadius = UDim.new(0, 8)
mainCorner.Parent = mainFrame

local dragIcon = Instance.new("ImageLabel")
dragIcon.Name = "DragIcon"
dragIcon.Size = UDim2.new(0, 32, 0, 32)
dragIcon.Position = UDim2.new(0, 10, 0, 10)
dragIcon.BackgroundTransparency = 1
dragIcon.Image = "rbxassetid://100900056737102"
dragIcon.Parent = mainFrame

local iconCorner = Instance.new("UICorner")
iconCorner.CornerRadius = UDim.new(1, 0)
iconCorner.Parent = dragIcon

local button = Instance.new("TextButton")
button.Name = "ToggleButton"
button.Size = UDim2.new(0, 180, 0, 45)
button.Position = UDim2.new(0.5, -90, 0.5, -5)
button.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
button.TextColor3 = Color3.fromRGB(255, 255, 255)
button.TextSize = 16
button.Font = Enum.Font.SourceSansBold
button.Text = "Start Teleport"
button.BorderSizePixel = 1
button.BorderColor3 = Color3.fromRGB(255, 255, 255)
button.Parent = mainFrame

local buttonCorner = Instance.new("UICorner")
buttonCorner.CornerRadius = UDim.new(0, 6)
buttonCorner.Parent = button

local dragging, dragInput, dragStart, startPos

local function update(input)
    local delta = input.Position - dragStart
    mainFrame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
end

dragIcon.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        dragging = true
        dragStart = input.Position
        startPos = mainFrame.Position
        
        input.Changed:Connect(function()
            if input.UserInputState == Enum.UserInputState.End then
                dragging = false
            end
        end)
    end
end)

dragIcon.InputChanged:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
        dragInput = input
    end
end)

userInputService.InputChanged:Connect(function(input)
    if input == dragInput and dragging then
        update(input)
    end
end)

local isTeleporting = false
local function startLoop()
    while isTeleporting do
        local character = player.Character or player.CharacterAdded:Wait()
        local rootPart = character:WaitForChild("HumanoidRootPart")
        rootPart.CFrame = titik1
        task.wait(0.5)
        if not isTeleporting then break end
        rootPart.CFrame = titik2
        task.wait(0.5)
    end
end

button.MouseButton1Click:Connect(function()
    isTeleporting = not isTeleporting
    if isTeleporting then
        button.Text = "[Active] Stop"
        button.TextColor3 = Color3.fromRGB(255, 100, 100)
        task.spawn(startLoop)
    else
        button.Text = "Start Teleport"
        button.TextColor3 = Color3.fromRGB(255, 255, 255)
    end
end)
