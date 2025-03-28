-- 🌟 Criando Interface do Bluex Hub
local BluexHub = Instance.new("ScreenGui")
local MainFrame = Instance.new("Frame")
local Title = Instance.new("TextLabel")
local UIStroke = Instance.new("UIStroke")

local AutoFarmButton = Instance.new("TextButton")
local AutoBountyButton = Instance.new("TextButton")
local AutoCDKButton = Instance.new("TextButton")
local AutoSeaBeastButton = Instance.new("TextButton")

BluexHub.Name = "BluexHub"
BluexHub.Parent = game.CoreGui

-- 🔳 Estilizando o Menu
MainFrame.Parent = BluexHub
MainFrame.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
MainFrame.Size = UDim2.new(0, 250, 0, 300)
MainFrame.Position = UDim2.new(0.5, -125, 0.5, -150)
MainFrame.BorderSizePixel = 0

UIStroke.Parent = MainFrame
UIStroke.Thickness = 3
UIStroke.Color = Color3.fromRGB(0, 0, 255)

Title.Parent = MainFrame
Title.Size = UDim2.new(1, 0, 0.15, 0)
Title.Text = "💙 BLUEX HUB 💙"
Title.BackgroundColor3 = Color3.fromRGB(0, 0, 255)
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.TextSize = 18
Title.Font = Enum.Font.SourceSansBold

-- 🟦 Criando Botões com Estilo Azul e Preto
function CreateButton(parent, text, position)
    local button = Instance.new("TextButton")
    button.Parent = parent
    button.Size = UDim2.new(0.9, 0, 0.15, 0)
    button.Position = UDim2.new(0.05, 0, position, 0)
    button.Text = text .. " OFF"
    button.BackgroundColor3 = Color3.fromRGB(0, 0, 255)
    button.TextColor3 = Color3.fromRGB(255, 255, 255)
    button.TextSize = 16
    button.Font = Enum.Font.SourceSansBold
    button.BorderSizePixel = 0
    return button
end

AutoFarmButton = CreateButton(MainFrame, "Auto Farm", 0.2)
AutoBountyButton = CreateButton(MainFrame, "Auto Bounty", 0.4)
AutoCDKButton = CreateButton(MainFrame, "Auto CDK", 0.6)
AutoSeaBeastButton = CreateButton(MainFrame, "Auto Sea Beast", 0.8)

-- 🌟 Variáveis de Controle
_G.AutoFarm = false
_G.AutoBounty = false
_G.AutoCDK = false
_G.AutoSeaBeast = false

-- 🌿 Função para Auto Farm
function AutoFarm()
    while _G.AutoFarm do
        wait(1)
        local enemies = game.Workspace.Enemies:GetChildren()
        for _, enemy in pairs(enemies) do
            if enemy:IsA("Model") and enemy:FindFirstChild("Humanoid") and enemy:FindFirstChild("HumanoidRootPart") then
                -- Teleporta para o inimigo
                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = enemy.HumanoidRootPart.CFrame + Vector3.new(0, 5, 0)
                wait(0.5)
                -- Ataca automaticamente
                game:GetService("VirtualUser"):ClickButton1(Vector2.new(0, 0)) 
            end
        end
    end
end

-- 🏆 Função para Auto Bounty
function AutoBounty()
    while _G.AutoBounty do
        wait(1)
        for _, target in pairs(game.Players:GetPlayers()) do
            if target ~= game.Players.LocalPlayer and target.Character and target.Character:FindFirstChild("HumanoidRootPart") then
                -- Teleporta para o jogador alvo
                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = target.Character.HumanoidRootPart.CFrame + Vector3.new(0, 5, 0)
                wait(0.5)
                -- Ataca automaticamente
                game:GetService("VirtualUser"):ClickButton1(Vector2.new(0, 0)) 
            end
        end
    end
end

-- ⚔️ Função para Auto CDK
function AutoCDK()
    while _G.AutoCDK do
        wait(1)
        local swords = {"Tushita", "Yama"}
        for _, sword in pairs(swords) do
            local tool = game.Players.LocalPlayer.Backpack:FindFirstChild(sword)
            if tool then
                -- Implementar farm de CDK aqui
                print("Encontrou a espada " .. sword)
            end
        end
    end
end

-- 🐉 Função para Auto Sea Beast
function AutoSeaBeast()
    while _G.AutoSeaBeast do
        wait(1)
        -- Código para detectar e farmar o Sea Beast
        -- Exemplo de lógica a ser implementada aqui
        print("Farmando Sea Beast...")
    end
end

-- 🔘 Conectando os Botões às Funções
AutoFarmButton.MouseButton1Click:Connect(function()
    _G.AutoFarm = not _G.AutoFarm
    AutoFarmButton.Text = "Auto Farm: " .. (_G.AutoFarm and "ON" or "OFF")
    if _G.AutoFarm then
        AutoFarm()
    end
end)

AutoBountyButton.MouseButton1Click:Connect(function()
    _G.AutoBounty = not _G.AutoBounty
    AutoBountyButton.Text = "Auto Bounty: " .. (_G.AutoBounty and "ON" or "OFF")
    if _G.AutoBounty then
        AutoBounty()
    end
end)

AutoCDKButton.MouseButton1Click:Connect(function()
    _G.AutoCDK = not _G.AutoCDK
    AutoCDKButton.Text = "Auto CDK: " .. (_G.AutoCDK and "ON" or "OFF")
    if _G.AutoCDK then
        AutoCDK()
    end
end)

AutoSeaBeastButton.MouseButton1Click:Connect(function()
    _G.AutoSeaBeast = not _G.AutoSeaBeast
    AutoSeaBeastButton.Text = "Auto Sea Beast: " .. (_G.AutoSeaBeast and "ON" or "OFF")
    if _G.AutoSeaBeast then
        AutoSeaBeast()
    end
end)
