-- AutoClickerLoader.lua
-- Script completo para auto clicker que pode ser carregado via loadstring

local UserInputService = game:GetService("UserInputService")
local RunService = game:GetService("RunService")

local autoClicking = false
local clickInterval = 0.1 -- intervalo de clique em segundos (10 cliques por segundo)

-- Função que simula o clique do mouse
local function doClick()
    local mouse = game.Players.LocalPlayer:GetMouse()
    mouse1press()
    wait(0.01)
    mouse1release()
end

-- Alterna o estado de auto clicker ao pressionar a tecla "H"
UserInputService.InputBegan:Connect(function(input, gameProcessed)
    if gameProcessed then return end
    if input.KeyCode == Enum.KeyCode.H then
        autoClicking = not autoClicking
        print("AutoClicker " .. (autoClicking and "ativado" or "desativado"))
    end
end)

-- Loop de auto click enquanto estiver ativado
RunService.RenderStepped:Connect(function()
    if autoClicking then
        doClick()
        wait(clickInterval)
    end
end)

print("AutoClicker carregado. Pressione H para ativar/desativar.")
