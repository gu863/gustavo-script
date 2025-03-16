-- Script básico para coletar frutas automaticamente no Blox Fruits com função para ligar e desligar

local player = game.Players.LocalPlayer
local fruits = game.Workspace.Fruits
local collecting = false

-- Função para coletar frutas
local function collectFruits()
    while collecting do
        for _, fruit in pairs(fruits:GetChildren()) do
            if fruit:IsA("Model") and fruit:FindFirstChild("TouchInterest") then
                -- Move o jogador para a fruta
                player.Character.HumanoidRootPart.CFrame = fruit.CFrame
                -- Aguarda um curto período para garantir a coleta da fruta
                wait(0.5)
            end
        end
        wait(10) -- Aguarda 10 segundos antes de tentar coletar novamente
    end
end

-- Função para alternar coleta de frutas
local function toggleCollecting()
    collecting = not collecting
    if collecting then
        print("Coleta de frutas ativada")
        collectFruits()
    else
        print("Coleta de frutas desativada")
    end
end

-- Conecta a função de alternância a uma tecla (por exemplo, "P")
game:GetService("UserInputService").InputBegan:Connect(function(input, gameProcessed)
    if input.KeyCode == Enum.KeyCode.P and not gameProcessed then
        toggleCollecting()
    end
end)

print("Script de coleta de frutas carregado. Pressione 'P' para alternar.")
