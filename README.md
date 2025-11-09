-- LocalScript em ScreenGui

local Players = game:GetService("Players")
local player = Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoid = character:WaitForChild("Humanoid")
local speedBoostButton = script.Parent:WaitForChild("Speed Boost") -- O botão deve se chamar exatamente "Speed Boost"
local RUN_SPEED = 80 -- Pode ajustar a velocidade, padrão do Roblox é 16
local NORMAL_SPEED = 16
local DURATION = 6 -- segundos de boost

local function hasBrainrot()
    -- Checa se o jogador tem uma Tool chamada "Brainrot"
    if player.Backpack:FindFirstChild("Brainrot") then
        return true
    end
    if character:FindFirstChild("Brainrot") then
        return true
    end
    return false
end

local boostActive = false

local function onSpeedBoostClicked()
    if boostActive then return end -- Já está ativo
    if not hasBrainrot() then
        speedBoostButton.Text = "Precisa do Brainrot!"
        wait(1.5)
        speedBoostButton.Text = "Speed Boost"
        return
    end
    boostActive = true
    humanoid.WalkSpeed = RUN_SPEED
    speedBoostButton.Text = "Turbo Ativado!"
    wait(DURATION)
    humanoid.WalkSpeed = NORMAL_SPEED
    speedBoostButton.Text = "Speed Boost"
    boostActive = false
end

speedBoostButton.MouseButton1Click:Connect(onSpeedBoostClicked)
