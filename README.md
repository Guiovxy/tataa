local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")
local camera = game.Workspace.CurrentCamera
local playersList = game.Players:GetPlayers()
local menuOpen = false
local infiniteKillActive = false
local wideGrabActive = false

local function teleportToLook()
    local lookDirection = camera.CFrame.LookVector * 50  -- Alvo a 50 studs à frente
    humanoidRootPart.CFrame = CFrame.new(humanoidRootPart.Position + lookDirection)
end

local function toggleInfiniteKill()
    infiniteKillActive = not infiniteKillActive
    if infiniteKillActive the
        local targetPlayer = game.Players:FindFirstChild("PlayerName")  -- Substitua PlayerName pelo nome do jogador alvo
        if targetPlayer then
            local targetCharacter = targetPlayer.Character
            if targetCharacter then
                local targetHumanoid = targetCharacter:FindFirstChildOfClass("Humanoid")
                if targetHumanoid then
                    while infiniteKillActive do
                        targetHumanoid.Health = 0 
                        wait(0.1) 
                    end
                end
            end
        end
    end
end

local function toggleWideGrab()
    wideGrabActive = not wideGrabActive
    if wideGrabActive then
    end
end

local function createMenu()
    local screenGui = Instance.new("ScreenGui")
    screenGui.Parent = player.PlayerGui
    
    local frame = Instance.new("Frame")
    frame.Size = UDim2.new(0, 200, 0, 200)
    frame.Position = UDim2.new(0, 50, 0, 50)
    frame.Parent = screenGui

    local teleportButton = Instance.new("TextButton")
    teleportButton.Text = "Teletransportar"
    teleportButton.Size = UDim2.new(0, 180, 0, 50)
    teleportButton.Position = UDim2.new(0, 10, 0, 10)
    teleportButton.Parent = frame
    teleportButton.MouseButton1Click:Connect(teleportToLook)

    local killButton = Instance.new("TextButton")
    killButton.Text = infiniteKillActive and "Desativar Matar Infinito" or "Ativar Matar Infinito"
    killButton.Size = UDim2.new(0, 180, 0, 50)
    killButton.Position = UDim2.new(0, 10, 0, 70)
    killButton.Parent = frame
    killButton.MouseButton1Click:Connect(function()
        toggleInfiniteKill()
        killButton.Text = infiniteKillActive and "Desativar Matar Infinito" or "Ativar Matar Infinito"
    end)

    local wideGrabButton = Instance.new("TextButton")
    wideGrabButton.Text = wideGrabActive and "Desativar Pegada Ampla" or "Ativar Pegada Ampla"
    wideGrabButton.Size = UDim2.new(0, 180, 0, 50)
    wideGrabButton.Position = UDim2.new(0, 10, 0, 130)
    wideGrabButton.Parent = frame
    wideGrabButton.MouseButton1Click:Connect(function()
        toggleWideGrab()
        wideGrabButton.Text = wideGrabActive and "Desativar Pegada Ampla" or "Ativar Pegada Ampla"
    end)
end

game:GetService("UserInputService").InputBegan:Connect(function(input, gameProcessed)
    if gameProcessed then return end
    if input.KeyCode == Enum.KeyCode.M then
        if menuOpen then
            menuOpen = false
            player.PlayerGui:ClearAllChildren()
        else
            menuOpen = true
            createMenu()
        end
    end
end)
