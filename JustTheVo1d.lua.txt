-- Создание GUI
local ScreenGui = Instance.new("ScreenGui")
local MainFrame = Instance.new("Frame")
local HeaderLabel = Instance.new("TextLabel") -- Заголовок
local OpenMenuButton = Instance.new("TextButton")
local SavePositionButton = Instance.new("TextButton")
local CloseMenuButton = Instance.new("TextButton")

local Positions = {} -- Таблица для сохранения позиций
local TpButtons = {} -- Таблица для кнопок телепортации
local MaxPoints = 10 -- Максимальное количество точек

-- Настройка GUI
ScreenGui.Parent = game.CoreGui

MainFrame.Parent = ScreenGui
MainFrame.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
MainFrame.Position = UDim2.new(0.4, 0, 0.4, 0)
MainFrame.Size = UDim2.new(0, 200, 0, 300)
MainFrame.Visible = false

-- Настройка заголовка
HeaderLabel.Parent = MainFrame
HeaderLabel.Text = "by JustTheVo1d"
HeaderLabel.Size = UDim2.new(1, 0, 0, 30)
HeaderLabel.Position = UDim2.new(0, 0, 0, 0)
HeaderLabel.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
HeaderLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
HeaderLabel.Font = Enum.Font.SourceSans
HeaderLabel.TextSize = 20

-- Кнопка открытия меню
OpenMenuButton.Parent = ScreenGui
OpenMenuButton.Text = "O"
OpenMenuButton.Size = UDim2.new(0, 50, 0, 50)
OpenMenuButton.Position = UDim2.new(0.9, 0, 0.1, 0)
OpenMenuButton.BackgroundColor3 = Color3.fromRGB(100, 100, 100)
OpenMenuButton.TextColor3 = Color3.fromRGB(255, 255, 255)
OpenMenuButton.Font = Enum.Font.SourceSans
OpenMenuButton.TextSize = 20

-- Кнопка сохранения позиции
SavePositionButton.Parent = MainFrame
SavePositionButton.Text = "Save Position"
SavePositionButton.Size = UDim2.new(1, -20, 0, 30)
SavePositionButton.Position = UDim2.new(0, 10, 0, 40)
SavePositionButton.BackgroundColor3 = Color3.fromRGB(70, 70, 70)
SavePositionButton.TextColor3 = Color3.fromRGB(255, 255, 255)
SavePositionButton.Font = Enum.Font.SourceSans
SavePositionButton.TextSize = 18

-- Кнопка закрытия меню
CloseMenuButton.Parent = MainFrame
CloseMenuButton.Text = "Close"
CloseMenuButton.Size = UDim2.new(1, -20, 0, 30)
CloseMenuButton.Position = UDim2.new(0, 10, 0, 80)
CloseMenuButton.BackgroundColor3 = Color3.fromRGB(70, 70, 70)
CloseMenuButton.TextColor3 = Color3.fromRGB(255, 255, 255)
CloseMenuButton.Font = Enum.Font.SourceSans
CloseMenuButton.TextSize = 18

-- Логика кнопок
OpenMenuButton.MouseButton1Click:Connect(function()
    MainFrame.Visible = true
end)

CloseMenuButton.MouseButton1Click:Connect(function()
    MainFrame.Visible = false
end)

SavePositionButton.MouseButton1Click:Connect(function()
    if #Positions < MaxPoints then
        local player = game.Players.LocalPlayer
        if player and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
            local position = player.Character.HumanoidRootPart.Position
            table.insert(Positions, position)

            -- Создание кнопки телепортации
            local TpButton = Instance.new("TextButton")
            TpButton.Parent = MainFrame
            TpButton.Text = "TP " .. #Positions
            TpButton.Size = UDim2.new(1, -20, 0, 30)
            TpButton.Position = UDim2.new(0, 10, 0, 100 + (#TpButtons * 40))
            TpButton.BackgroundColor3 = Color3.fromRGB(70, 70, 70)
            TpButton.TextColor3 = Color3.fromRGB(255, 255, 255)
            TpButton.Font = Enum.Font.SourceSans
            TpButton.TextSize = 18

            table.insert(TpButtons, TpButton)

            TpButton.MouseButton1Click:Connect(function()
                player.Character.HumanoidRootPart.CFrame = CFrame.new(position)
            end)
        end
    else
        warn("Максимальное количество точек достигнуто!")
    end
end)
