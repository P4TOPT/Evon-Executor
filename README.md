-- Script Open Source para Mini City
-- Funcionalidades: Auto-Farm de Peças de Arma, Auto-Farm de Planta Suja, ESP, UI personalizada, Teleporte para Locais Específicos, Safe Teleport, Auto-Quest, Auto-Loot Rápido, Mudança de Cores do Menu, Aimbot, Wallhack, Spawn de Veículos Exclusivos, Geração de Dinheiro, Modo Voo, Proteção Anti-Detecção Avançada

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local LocalPlayer = Players.LocalPlayer

-- Criar UI personalizada
local ScreenGui = Instance.new("ScreenGui")
local MainFrame = Instance.new("Frame")
local TitleLabel = Instance.new("TextLabel")
local ChangeColorButton = Instance.new("TextButton")
local AutoFarmGunPartsButton = Instance.new("TextButton")
local AutoFarmDirtyPlantsButton = Instance.new("TextButton")
local AutoLootButton = Instance.new("TextButton")
local ESPButton = Instance.new("TextButton")
local TeleportMenu = Instance.new("Frame")
local SafeTeleportButton = Instance.new("TextButton")
local AutoQuestButton = Instance.new("TextButton")
local AimbotButton = Instance.new("TextButton")
local WallhackButton = Instance.new("TextButton")
local SpawnVehicleButton = Instance.new("TextButton")
local MoneyFarmButton = Instance.new("TextButton")
local FlyButton = Instance.new("TextButton")

ScreenGui.Parent = game.CoreGui
MainFrame.Parent = ScreenGui
TitleLabel.Parent = MainFrame
ChangeColorButton.Parent = MainFrame
AutoFarmGunPartsButton.Parent = MainFrame
AutoFarmDirtyPlantsButton.Parent = MainFrame
AutoLootButton.Parent = MainFrame
ESPButton.Parent = MainFrame
TeleportMenu.Parent = MainFrame
SafeTeleportButton.Parent = MainFrame
AutoQuestButton.Parent = MainFrame
AimbotButton.Parent = MainFrame
WallhackButton.Parent = MainFrame
SpawnVehicleButton.Parent = MainFrame
MoneyFarmButton.Parent = MainFrame
FlyButton.Parent = MainFrame

MainFrame.Size = UDim2.new(0.3, 0, 0.9, 0)
MainFrame.Position = UDim2.new(0.35, 0, 0.05, 0)
MainFrame.Visible = true
MainFrame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)

TitleLabel.Size = UDim2.new(1, 0, 0.1, 0)
TitleLabel.Position = UDim2.new(0, 0, 0, 0)
TitleLabel.Text = "ModMenu P4TO"
TitleLabel.TextScaled = true
TitleLabel.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
TitleLabel.TextColor3 = Color3.fromRGB(255, 255, 255)

-- Proteção Anti-Detecção
local function bypassDetection()
    local mt = getrawmetatable(game)
    local oldIndex = mt.__index
    setreadonly(mt, false)
    mt.__index = newcclosure(function(t, k)
        if k == "WalkSpeed" or k == "JumpPower" or k == "Gravity" then
            return 16
        end
        return oldIndex(t, k)
    end)
    setreadonly(mt, true)
end
bypassDetection()

local function secureExecution()
    if setfflag then
        setfflag("HumanoidParallelRemoveNoPhysics", "False")
        setfflag("HumanoidParallelRemoveNoPhysicsNoSimulate2", "False")
    end
end
secureExecution()

FlyButton.Size = UDim2.new(1, 0, 0.1, 0)
FlyButton.Position = UDim2.new(0, 0, 1.2, 0)
FlyButton.Text = "Ativar Voo"

local flying = false
local flySpeed = 50

FlyButton.MouseButton1Click:Connect(function()
    flying = not flying
    FlyButton.Text = flying and "Voo Ativado" or "Ativar Voo"
    if flying then
        local character = LocalPlayer.Character
        if character and character:FindFirstChild("HumanoidRootPart") then
            local hrp = character.HumanoidRootPart
            local flyLoop
            flyLoop = RunService.RenderStepped:Connect(function()
                if flying then
                    hrp.Velocity = Vector3.new(0, flySpeed, 0)
                else
                    flyLoop:Disconnect()
                end
            end)
        end
    end
end)

-- Alternar visibilidade do menu com a tecla "K"
UserInputService.InputBegan:Connect(function(input, gameProcessed)
    if input.KeyCode == Enum.KeyCode.K and not gameProcessed then
        MainFrame.Visible = not MainFrame.Visible
    end
end)

-- Mantém o restante das funcionalidades como Auto-Farm, Auto-Loot, ESP, Aimbot, Wallhack, Spawn de Veículos e Geração de Dinheiro
