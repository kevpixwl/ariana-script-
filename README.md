-- =============================================================================
-- INTERFACE TVL 2 - OTIMIZADA PARA DELTA
-- CRÉDITOS / CREDITS: raimbow
-- =============================================================================

local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local TeleportService = game:GetService("TeleportService")

local PlayerGui = LocalPlayer:WaitForChild("PlayerGui")
local CoreGui = game:GetService("CoreGui")
local TargetParent = (CoreGui:FindFirstChild("RobloxGui") or PlayerGui)

if TargetParent:FindFirstChild("TVL2Hub") then
    TargetParent.TVL2Hub:Destroy()
end

local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "TVL2Hub"
ScreenGui.ResetOnSpawn = false
ScreenGui.Parent = TargetParent

-- =============================================================================
-- 1. LOADER / TELA DE ATIVAÇÃO
-- =============================================================================
local Loader = Instance.new("Frame")
Loader.Size = UDim2.new(0, 350, 0, 180)
Loader.Position = UDim2.new(0.5, -175, 0.5, -90)
Loader.BackgroundColor3 = Color3.fromRGB(20, 18, 24)
Loader.BorderSizePixel = 0
Loader.Parent = ScreenGui

local LoaderCorner = Instance.new("UICorner")
LoaderCorner.CornerRadius = UDim.new(0, 8)
LoaderCorner.Parent = Loader

local LoaderTitle = Instance.new("TextLabel")
LoaderTitle.Size = UDim2.new(1, 0, 0, 40)
LoaderTitle.BackgroundTransparency = 1
LoaderTitle.Text = "TVL 2 | Loader"
LoaderTitle.TextColor3 = Color3.fromRGB(255, 255, 255)
LoaderTitle.TextSize = 18
LoaderTitle.Font = Enum.Font.SourceSansBold
LoaderTitle.Parent = Loader

local LoaderCredits = Instance.new("TextLabel")
LoaderCredits.Size = UDim2.new(1, 0, 0, 30)
LoaderCredits.Position = UDim2.new(0, 0, 0, 40)
LoaderCredits.BackgroundTransparency = 1
LoaderCredits.Text = "credits: raimbow"
LoaderCredits.TextColor3 = Color3.fromRGB(150, 140, 180)
LoaderCredits.TextSize = 14
LoaderCredits.Font = Enum.Font.SourceSans
LoaderCredits.Parent = Loader

local ActiveBtn = Instance.new("TextButton")
ActiveBtn.Size = UDim2.new(0, 180, 0, 40)
ActiveBtn.Position = UDim2.new(0.5, -90, 0.6, 10)
ActiveBtn.BackgroundColor3 = Color3.fromRGB(40, 35, 50)
ActiveBtn.Text = "CARREGAR HUB"
ActiveBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
ActiveBtn.TextSize = 14
ActiveBtn.Font = Enum.Font.SourceSansBold
ActiveBtn.Parent = Loader

local BtnCorner = Instance.new("UICorner")
BtnCorner.CornerRadius = UDim.new(0, 6)
BtnCorner.Parent = ActiveBtn

-- =============================================================================
-- 2. INTERFACE PRINCIPAL TVL 2
-- =============================================================================
local MainFrame = Instance.new("Frame")
MainFrame.Size = UDim2.new(0, 680, 0, 460)
MainFrame.Position = UDim2.new(0.5, -340, 0.5, -230)
MainFrame.BackgroundColor3 = Color3.fromRGB(13, 11, 16)
MainFrame.BorderSizePixel = 0
MainFrame.Visible = false
MainFrame.Parent = ScreenGui

local MainCorner = Instance.new("UICorner")
MainCorner.CornerRadius = UDim.new(0, 8)
MainCorner.Parent = MainFrame

-- MENU LATERAL (ESQUERDA)
local Sidebar = Instance.new("Frame")
Sidebar.Size = UDim2.new(0, 180, 1, -30)
Sidebar.Position = UDim2.new(0, 0, 0, 0)
Sidebar.BackgroundColor3 = Color3.fromRGB(18, 16, 22)
Sidebar.BorderSizePixel = 0
Sidebar.Parent = MainFrame

local LogoLabel = Instance.new("TextLabel")
LogoLabel.Size = UDim2.new(1, 0, 0, 50)
LogoLabel.BackgroundTransparency = 1
LogoLabel.Text = "🔮 TVL 2"
LogoLabel.TextColor3 = Color3.fromRGB(240, 240, 240)
LogoLabel.TextSize = 16
LogoLabel.Font = Enum.Font.SourceSansBold
LogoLabel.TextXAlignment = Enum.TextXAlignment.Left
LogoLabel.Parent = Sidebar

local SidebarPadding = Instance.new("UIPadding")
SidebarPadding.PaddingLeft = UDim.new(0, 15)
SidebarPadding.Parent = Sidebar

local SideLayout = Instance.new("UIListLayout")
SideLayout.Padding = UDim.new(0, 10)
SideLayout.Parent = Sidebar

local function criarAbaBotao(text, ativo)
    local Btn = Instance.new("TextButton")
    Btn.Size = UDim2.new(1, -15, 0, 30)
    Btn.BackgroundTransparency = 1
    Btn.Text = text
    Btn.TextColor3 = ativo and Color3.fromRGB(230, 230, 230) or Color3.fromRGB(120, 115, 130)
    Btn.TextSize = 14
    Btn.Font = ativo and Enum.Font.SourceSansBold or Enum.Font.SourceSans
    Btn.TextXAlignment = Enum.TextXAlignment.Left
    Btn.Parent = Sidebar
end
criarAbaBotao("⚡ Main Features", true)
criarAbaBotao("👥 Players List", false)
criarAbaBotao("⚙️ Menu Settings", false)

-- TOPO / BARRA DE PESQUISA (SEARCH)
local Topbar = Instance.new("Frame")
Topbar.Size = UDim2.new(1, -180, 0, 50)
Topbar.Position = UDim2.new(0, 180, 0, 0)
Topbar.BackgroundTransparency = 1
Topbar.Parent = MainFrame

local SearchBar = Instance.new("TextBox")
SearchBar.Size = UDim2.new(1, -30, 0, 32)
SearchBar.Position = UDim2.new(0, 15, 0, 10)
SearchBar.BackgroundColor3 = Color3.fromRGB(22, 20, 28)
SearchBar.Text = ""
SearchBar.PlaceholderText = "🔍 Search"
SearchBar.TextColor3 = Color3.fromRGB(200, 200, 200)
SearchBar.PlaceholderColor3 = Color3.fromRGB(80, 75, 90)
SearchBar.TextSize = 14
SearchBar.Font = Enum.Font.SourceSans
SearchBar.TextXAlignment = Enum.TextXAlignment.Left
SearchBar.Parent = Topbar

local SearchPadding = Instance.new("UIPadding")
SearchPadding.PaddingLeft = UDim.new(0, 10)
SearchPadding.Parent = SearchBar

local SearchCorner = Instance.new("UICorner")
SearchCorner.CornerRadius = UDim.new(0, 6)
SearchCorner.Parent = SearchBar

-- CONTAINER DE CONTEÚDO EM COLUNAS (DIREITA)
local ContentFrame = Instance.new("Frame")
ContentFrame.Size = UDim2.new(1, -180, 1, -80)
ContentFrame.Position = UDim2.new(0, 180, 0, 50)
ContentFrame.BackgroundTransparency = 1
ContentFrame.Parent = MainFrame

-- Coluna Esquerda
local Col1 = Instance.new("ScrollingFrame")
Col1.Size = UDim2.new(0.5, -20, 1, 0)
Col1.Position = UDim2.new(0, 15, 0, 0)
Col1.BackgroundTransparency = 1
Col1.BorderSizePixel = 0
Col1.ScrollBarThickness = 0
Col1.Parent = ContentFrame

local L1 = Instance.new("UIListLayout")
L1.Padding = UDim.new(0, 15)
L1.Parent = Col1

-- Coluna Direita
local Col2 = Instance.new("ScrollingFrame")
Col2.Size = UDim2.new(0.5, -20, 1, 0)
Col2.Position = UDim2.new(0.5, 5, 0, 0)
Col2.BackgroundTransparency = 1
Col2.BorderSizePixel = 0
Col2.ScrollBarThickness = 0
Col2.Parent = ContentFrame

local L2 = Instance.new("UIListLayout")
L2.Padding = UDim.new(0, 15)
L2.Parent = Col2

-- RODAPÉ DE CRÉDITOS IDENTICO À IMAGEM
local Footer = Instance.new("TextLabel")
Footer.Size = UDim2.new(1, 0, 0, 30)
Footer.Position = UDim2.new(0, 0, 1, -30)
Footer.BackgroundTransparency = 1
Footer.Text = "credits: raimbow"
Footer.TextColor3 = Color3.fromRGB(70, 65, 80)
Footer.TextSize = 13
Footer.Font = Enum.Font.SourceSans
Footer.Parent = MainFrame

-- =============================================================================
-- FUNÇÃO PARA CRIAR OS BLOCOS DE SEÇÕES COM TOGGLES REDONDOS
-- =============================================================================
local function criarModulo(coluna, tituloCategoria)
    local Card = Instance.new("Frame")
    Card.Size = UDim2.new(1, 0, 0, 75)
    Card.BackgroundColor3 = Color3.fromRGB(18, 16, 22)
    Card.BorderSizePixel = 0
    Card.Parent = coluna

    local CardCorner = Instance.new("UICorner")
    CardCorner.CornerRadius = UDim.new(0, 6)
    CardCorner.Parent = Card

    local LabelCat = Instance.new("TextLabel")
    LabelCat.Size = UDim2.new(1, -20, 0, 25)
    LabelCat.Position = UDim2.new(0, 12, 0, 8)
    LabelCat.BackgroundTransparency = 1
    LabelCat.Text = tituloCategoria
    LabelCat.TextColor3 = Color3.fromRGB(115, 95, 175) -- Tom roxo dos títulos da print
    LabelCat.TextSize = 13
    LabelCat.Font = Enum.Font.SourceSansBold
    LabelCat.TextXAlignment = Enum.TextXAlignment.Left
    LabelCat.Parent = Card

    local function adicionarToggle(nomeFeature, callback)
        local Row = Instance.new("Frame")
        Row.Size = UDim2.new(1, 0, 0, 35)
        Row.Position = UDim2.new(0, 0, 0, 33)
        Row.BackgroundTransparency = 1
        Row.Parent = Card

        local LabelFeature = Instance.new("TextLabel")
        LabelFeature.Size = UDim2.new(1, -60, 1, 0)
        LabelFeature.Position = UDim2.new(0, 12, 0, 0)
        LabelFeature.BackgroundTransparency = 1
        LabelFeature.Text = nomeFeature
        LabelFeature.TextColor3 = Color3.fromRGB(190, 185, 200)
        LabelFeature.TextSize = 14
        LabelFeature.Font = Enum.Font.SourceSans
        LabelFeature.TextXAlignment = Enum.TextXAlignment.Left
        LabelFeature.Parent = Row

        -- Estrutura do Switch Oval da Print
        local SwitchBg = Instance.new("TextButton")
        SwitchBg.Size = UDim2.new(0, 36, 0, 20)
        SwitchBg.Position = UDim2.new(1, -48, 0.5, -10)
        SwitchBg.BackgroundColor3 = Color3.fromRGB(45, 40, 55)
        SwitchBg.Text = ""
        SwitchBg.Parent = Row

        local SwitchCorner = Instance.new("UICorner")
        SwitchCorner.CornerRadius = UDim.new(1, 0)
        SwitchCorner.Parent = SwitchBg

        local SliderCircle = Instance.new("Frame")
        SliderCircle.Size = UDim2.new(0, 14, 0, 14)
        SliderCircle.Position = UDim2.new(0, 3, 0.5, -7)
        SliderCircle.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
        SliderCircle.BorderSizePixel = 0
        SliderCircle.Parent = SwitchBg

        local CircleCorner = Instance.new("UICorner")
        CircleCorner.CornerRadius = UDim.new(1, 0)
        CircleCorner.Parent = SliderCircle

        local ligado = false
        SwitchBg.MouseButton1Click:Connect(function()
            ligado = not ligado
            if callback then callback(ligado) end
            
            if ligado then
                SwitchBg.BackgroundColor3 = Color3.fromRGB(130, 90, 230) -- Roxo ativo
                SliderCircle.Position = UDim2.new(1, -17, 0.5, -7)
            else
                SwitchBg.BackgroundColor3 = Color3.fromRGB(45, 40, 55) -- Retorna ao padrão desativado
