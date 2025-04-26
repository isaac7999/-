local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Parent = game.Players.LocalPlayer.PlayerGui
ScreenGui.Name = "CustomESP"

-- Função para criar a imagem de boas-vindas
local welcomeImage = Instance.new("ImageLabel")
welcomeImage.Parent = ScreenGui
welcomeImage.Size = UDim2.new(0, 400, 0, 400)
welcomeImage.Position = UDim2.new(0.5, -200, 0.5, -200)
welcomeImage.Image = "rbxassetid://70715640238366"  -- A ID da imagem que você mencionou
welcomeImage.BackgroundTransparency = 1

-- Função para mostrar a mensagem de boas-vindas
local welcomeMessage = Instance.new("TextLabel")
welcomeMessage.Parent = ScreenGui
welcomeMessage.Size = UDim2.new(0, 400, 0, 50)
welcomeMessage.Position = UDim2.new(0.5, -200, 0.8, 0)
welcomeMessage.Text = "BEM VINDO, " .. game.Players.LocalPlayer.Name
welcomeMessage.TextColor3 = Color3.fromRGB(255, 255, 255)
welcomeMessage.TextScaled = true
welcomeMessage.BackgroundTransparency = 1

-- Esperar 3 segundos para remover a imagem e mensagem
wait(3)

-- Remover imagem e mensagem de boas-vindas
welcomeImage:Destroy()
welcomeMessage:Destroy()

-- Flee the Facility Script Movível + Minimizar como Fita

local ScreenGui = Instance.new("ScreenGui")
local MainFrame = Instance.new("Frame")
local UICorner = Instance.new("UICorner")
local UIListLayout = Instance.new("UIListLayout")
local Title = Instance.new("TextLabel")
local ToggleButton = Instance.new("TextButton")

ScreenGui.Name = "FleeFacilityPanel"
ScreenGui.Parent = game.CoreGui
ScreenGui.ResetOnSpawn = false

MainFrame.Parent = ScreenGui
MainFrame.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
MainFrame.Position = UDim2.new(0.05, 0, 0.2, 0)
MainFrame.Size = UDim2.new(0, 220, 0, 500)
MainFrame.Active = true
MainFrame.Draggable = true

UICorner.Parent = MainFrame

Title.Parent = MainFrame
Title.BackgroundTransparency = 1
Title.Size = UDim2.new(1, 0, 0, 30)
Title.Text = "Flee Facility Panel"
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.Font = Enum.Font.GothamBold
Title.TextSize = 16

ToggleButton.Parent = MainFrame
ToggleButton.Size = UDim2.new(1, -10, 0, 28)
ToggleButton.Position = UDim2.new(0, 5, 0, 35)
ToggleButton.Text = "Minimizar"
ToggleButton.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
ToggleButton.TextColor3 = Color3.fromRGB(255, 255, 255)
ToggleButton.Font = Enum.Font.Gotham
ToggleButton.TextSize = 14

local minimized = false

local function Minimize()
    minimized = true
    for _, child in ipairs(MainFrame:GetChildren()) do
        if child:IsA("TextButton") or child:IsA("TextLabel") then
            if child ~= ToggleButton then
                child.Visible = false
            end
        end
    end
    MainFrame.Size = UDim2.new(0, 220, 0, 40)
    ToggleButton.Text = "Maximizar"
end

local function Maximize()
    minimized = false
    for _, child in ipairs(MainFrame:GetChildren()) do
        if child:IsA("TextButton") or child:IsA("TextLabel") then
            child.Visible = true
        end
    end
    MainFrame.Size = UDim2.new(0, 220, 0, 500)
    ToggleButton.Text = "Minimizar"
end

ToggleButton.MouseButton1Click:Connect(function()
    if minimized then
        Maximize()
    else
        Minimize()
    end
end)

-- Layout
local ButtonHolder = Instance.new("Frame")
ButtonHolder.Parent = MainFrame
ButtonHolder.Size = UDim2.new(1, 0, 1, -70)
ButtonHolder.Position = UDim2.new(0, 0, 0, 70)
ButtonHolder.BackgroundTransparency = 1

local ListLayout = Instance.new("UIListLayout")
ListLayout.Parent = ButtonHolder
ListLayout.Padding = UDim.new(0, 4)
ListLayout.SortOrder = Enum.SortOrder.LayoutOrder

-- 20 Funções úteis para Flee the Facility

local function SpeedHack()
    game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 30
end

local function SuperJump()
    game.Players.LocalPlayer.Character.Humanoid.JumpPower = 100
end

local function Noclip()
    local player = game.Players.LocalPlayer
    player.Character.Humanoid:ChangeState(11)
end

local function Invisible()
    for _, part in pairs(game.Players.LocalPlayer.Character:GetChildren()) do
        if part:IsA("BasePart") then
            part.Transparency = 1
        end
    end
end

local function ESPPlayers()
    for _, player in pairs(game.Players:GetPlayers()) do
        if player.Name ~= game.Players.LocalPlayer.Name then
            local esp = Instance.new("Highlight", player.Character)
            esp.FillColor = Color3.fromRGB(0, 255, 0)
        end
    end
end

local function ESPBeast()
    for _, player in pairs(game.Players:GetPlayers()) do
        if player:FindFirstChild("Beast") then
            local beastESP = Instance.new("Highlight", player.Character)
            beastESP.FillColor = Color3.fromRGB(255, 0, 0)
        end
    end
end

local function ESPComputers()
    for _, comp in pairs(workspace:GetDescendants()) do
        if comp.Name == "ComputerTable" then
            local esp = Instance.new("Highlight", comp)
            esp.FillColor = Color3.fromRGB(0, 0, 255)
        end
    end
end

local function AutoHack()
    local player = game.Players.LocalPlayer
    task.spawn(function()
        while task.wait(0.1) do
            for _, comp in pairs(workspace:GetDescendants()) do
                if comp.Name == "ComputerTable" and (player:DistanceFromCharacter(comp.Position) < 10) then
                    fireproximityprompt(comp.ProximityPrompt)
                end
            end
        end
    end)
end

local function TrackBeast()
    for _, p in pairs(game.Players:GetPlayers()) do
        if p:FindFirstChild("Beast") then
            print("Marretão é:", p.Name)
        end
    end
end

local function ESPExits()
    for _, exit in pairs(workspace:GetDescendants()) do
        if exit.Name == "ExitDoor" then
            local highlight = Instance.new("Highlight", exit)
            highlight.FillColor = Color3.fromRGB(255, 255, 0)
        end
    end
end

local function FreezeImmunity()
    game.Players.LocalPlayer.Character.Humanoid.PlatformStand = false
end

local function AutoEscape()
    local player = game.Players.LocalPlayer
    for _, exit in pairs(workspace:GetDescendants()) do
        if exit.Name == "ExitDoor" then
            player.Character.HumanoidRootPart.CFrame = exit.CFrame
        end
    end
end

local function SilentWalk()
    game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 16
end

local function Flashlight()
    local light = Instance.new("PointLight", game.Players.LocalPlayer.Character.Head)
    light.Brightness = 2
    light.Range = 30
end

local function AntiDrag()
    game.Players.LocalPlayer.Character.HumanoidRootPart.Anchored = false
end

local function SuperVault()
    game.Players.LocalPlayer.Character.Humanoid:ChangeState(3)
end

local function NoDoors()
    for _, door in pairs(workspace:GetDescendants()) do
        if door.Name == "Door" then
            door.CanCollide = false
            door.Transparency = 0.6
        end
    end
end

local function QuickHack()
    task.spawn(function()
        while task.wait(0.2) do
            for _, comp in pairs(workspace:GetDescendants()) do
                if comp.Name == "ComputerTable" then
                    fireproximityprompt(comp.ProximityPrompt)
                end
            end
        end
    end)
end

local function AutoSave()
    local lp = game.Players.LocalPlayer
    task.spawn(function()
        while task.wait(0.5) do
            for _, p in pairs(game.Players:GetPlayers()) do
                if p ~= lp and p.Character and p.Character:FindFirstChild("Frozen") then
                    lp.Character.HumanoidRootPart.CFrame = p.Character.HumanoidRootPart.CFrame
                end
            end
        end
    end)
end

local function BeastBuff()
    if game.Players.LocalPlayer:FindFirstChild("Beast") then
        game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = 40
        game.Players.LocalPlayer.Character.Humanoid.JumpPower = 100
    end
end

-- Criar botões de funções

local functions = {
    {"Speed Hack", SpeedHack},
    {"Super Jump", SuperJump},
    {"Noclip", Noclip},
    {"Invisível", Invisible},
    {"ESP Players", ESPPlayers},
    {"ESP Beast", ESPBeast},
    {"ESP Computers", ESPComputers},
    {"Auto Hack", AutoHack},
    {"Track Beast", TrackBeast},
    {"ESP Exits", ESPExits},
    {"Freeze Immunity", FreezeImmunity},
    {"Auto Escape", AutoEscape},
    {"Silent Walk", SilentWalk},
    {"Flashlight", Flashlight},
    {"Anti Drag", AntiDrag},
    {"Super Vault", SuperVault},
    {"No Doors", NoDoors},
    {"Quick Hack", QuickHack},
    {"Auto Save", AutoSave},
    {"Beast Buff", BeastBuff},
}

for _, func in pairs(functions) do
    local button = Instance.new("TextButton")
    button.Parent = ButtonHolder
    button.Size = UDim2.new(1, -10, 0, 28)
    button.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
    button.TextColor3 = Color3.fromRGB(255, 255, 255)
    button.Text = func[1]
    button.Font = Enum.Font.Gotham
    button.TextSize = 14

    local corner = Instance.new("UICorner")
    corner.Parent = button

    button.MouseButton1Click:Connect(func[2])
end
