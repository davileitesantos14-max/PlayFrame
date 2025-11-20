local TweenService = game:GetService("TweenService")
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer

local gui = script.Parent
local frame1 = gui:FindFirstChild("Frame1")
local playButton = frame1 and frame1:FindFirstChild("PlayButton")
local playFrame = gui:FindFirstChild("PlayFrame")
local playLabel = playFrame and playFrame:FindFirstChild("PlayLabel")

-- Inicializa PlayFrame e PlayLabel invisíveis e transparentes
if playFrame then
    playFrame.Visible = false
    playFrame.BackgroundTransparency = 1
    -- Inicializa todos os TextButtons do PlayFrame transparentes
    for _, child in playFrame:GetChildren() do
        if child:IsA("TextButton") then
            child.TextTransparency = 1
            child.BackgroundTransparency = 1
        end
    end
end
if playLabel then
    playLabel.TextTransparency = 1
    playLabel.BackgroundTransparency = 1
end

local function fadeInPlayFrame()
    if not playFrame then
        print("PlayFrame não encontrado!")
        return
    end
    playFrame.Visible = true

    TweenService:Create(playFrame, TweenInfo.new(0.5, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {BackgroundTransparency = 0}):Play()
    
    for _, child in playFrame:GetChildren() do
        if child:IsA("TextButton") then
            TweenService:Create(child, TweenInfo.new(0.5, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {TextTransparency = 0, BackgroundTransparency = 0}):Play()
        end
    end

    if playLabel then
        TweenService:Create(playLabel, TweenInfo.new(0.5, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {TextTransparency = 0, BackgroundTransparency = 0}):Play()
    end
end

if playButton then
    playButton.MouseButton1Click:Connect(function()
        print("PlayButton clicado! Mostrando PlayFrame com Fade In.")
        fadeInPlayFrame()
    end)
end

