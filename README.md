
--Gui for Roblox and is cs sadly :(
-- Create the GUI
local player = game.Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "W33P_GUI"
screenGui.Parent = playerGui

-- Create the main frame for the GUI
local mainFrame = Instance.new("Frame")
mainFrame.Name = "MainFrame"
mainFrame.Size = UDim2.new(0, 300, 0, 600)
mainFrame.Position = UDim2.new(0, 0, 0.5, -300)
mainFrame.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
mainFrame.BorderColor3 = Color3.fromRGB(255, 0, 0)
mainFrame.BorderSizePixel = 2
mainFrame.Parent = screenGui

-- Make the GUI draggable
local dragInput, dragStart, startPos
local function update(input)
    local delta = input.Position - dragStart
    mainFrame.Position = UDim2.new(0, startPos.X + delta.X, 0, startPos.Y + delta.Y)
end

mainFrame.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        dragStart = input.Position
        startPos = mainFrame.Position
        input.Changed:Connect(function()
            if input.UserInputState == Enum.UserInputState.End then
                dragInput:Disconnect()
            end
        end)
        dragInput = game:GetService("UserInputService").InputChanged:Connect(update)
    end
end)

-- Add title text
local titleLabel = Instance.new("TextLabel")
titleLabel.Text = "W33P GUI V1"
titleLabel.Size = UDim2.new(0, 300, 0, 50)
titleLabel.Position = UDim2.new(0, 0, 0, 0)
titleLabel.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
titleLabel.TextColor3 = Color3.fromRGB(255, 0, 0)
titleLabel.TextSize = 24
titleLabel.TextStrokeTransparency = 0
titleLabel.TextStrokeColor3 = Color3.fromRGB(255, 0, 0)
titleLabel.Parent = mainFrame

-- Create function to set player walk speed
local function createButton(name, yPos, func)
    local button = Instance.new("TextButton")
    button.Name = name
    button.Text = name
    button.Size = UDim2.new(0, 300, 0, 50)
    button.Position = UDim2.new(0, 0, 0, yPos)
    button.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
    button.TextColor3 = Color3.fromRGB(255, 0, 0)
    button.BorderColor3 = Color3.fromRGB(255, 0, 0)
    button.BorderSizePixel = 2
    button.TextSize = 18
    button.TextStrokeTransparency = 0
    button.TextStrokeColor3 = Color3.fromRGB(255, 0, 0)
    button.Parent = mainFrame

    button.MouseButton1Click:Connect(func)
    return button
end

-- Speed Set button
local speedTextBox = Instance.new("TextBox")
speedTextBox.Size = UDim2.new(0, 300, 0, 50)
speedTextBox.Position = UDim2.new(0, 0, 0, 50)
speedTextBox.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
speedTextBox.BorderColor3 = Color3.fromRGB(255, 0, 0)
speedTextBox.TextColor3 = Color3.fromRGB(255, 0, 0)
speedTextBox.TextSize = 18
speedTextBox.PlaceholderText = "Enter Speed"
speedTextBox.TextStrokeTransparency = 0
speedTextBox.TextStrokeColor3 = Color3.fromRGB(255, 0, 0)
speedTextBox.Parent = mainFrame

createButton("Speed Set", 100, function()
    local speed = tonumber(speedTextBox.Text)
    if speed then
        player.Character.Humanoid.WalkSpeed = speed
    end
end)

-- Jump Set button
local jumpTextBox = Instance.new("TextBox")
jumpTextBox.Size = UDim2.new(0, 300, 0, 50)
jumpTextBox.Position = UDim2.new(0, 0, 0, 150)
jumpTextBox.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
jumpTextBox.BorderColor3 = Color3.fromRGB(255, 0, 0)
jumpTextBox.TextColor3 = Color3.fromRGB(255, 0, 0)
jumpTextBox.TextSize = 18
jumpTextBox.PlaceholderText = "Enter Jump Power"
jumpTextBox.TextStrokeTransparency = 0
jumpTextBox.TextStrokeColor3 = Color3.fromRGB(255, 0, 0)
jumpTextBox.Parent = mainFrame

createButton("Jump Set", 200, function()
    local jumpPower = tonumber(jumpTextBox.Text)
    if jumpPower then
        player.Character.Humanoid.JumpPower = jumpPower
    end
end)

-- Fire All button
createButton("Fire All", 250, function()
    for _, obj in pairs(workspace:GetChildren()) do
        if obj:IsA("BasePart") then
            local fire = Instance.new("Fire")
            fire.Parent = obj
            fire.Heat = 10
            fire.Size = 10
        end
    end
end)

-- Disco Fog button
createButton("Disco Fog", 300, function()
    local fog = Instance.new("FogEnd")
    fog.Parent = workspace
    game.Lighting.FogColor = Color3.fromRGB(255, 0, 0)
    
    while true do
        wait(1)
        game.Lighting.FogColor = Color3.fromRGB(math.random(0, 255), math.random(0, 255), math.random(0, 255))
    end
end)

-- Give Sword button
createButton("Give Sword", 350, function()
    local sword = Instance.new("Tool")
    sword.Name = "Sword"
    sword.Parent = player.Backpack
    -- Add sword functionality (damage, etc.) here
end)

-- Flood button
createButton("Flood", 400, function()
    for _, obj in pairs(workspace:GetChildren()) do
        if obj:IsA("BasePart") then
            obj.Position = Vector3.new(obj.Position.X, 145, obj.Position.Z)
        end
    end
end)

-- Ultimate Destruction button
createButton("Ultimate Destruction", 450, function()
    for i = 1, 2000 do
        local part = Instance.new("Part")
        part.Size = Vector3.new(4, 4, 4)
        part.Position = Vector3.new(math.random(-1000, 1000), 100, math.random(-1000, 1000))
        part.Color = Color3.fromRGB(255, 0, 0)
        part.Anchored = true
        part.CanCollide = false
        part.Parent = workspace
        local fire = Instance.new("Fire")
        fire.Parent = part
    end
end)

-- Heal button
createButton("Heal", 500, function()
    player.Character.Humanoid.Health = 100
end)
