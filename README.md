--==================== HUB 1 - Amendoim-Hub ====================--
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local player = Players.LocalPlayer
local Camera = workspace.CurrentCamera

-- ScreenGui 1
local ScreenGui1 = Instance.new("ScreenGui", game.CoreGui)
ScreenGui1.Name = "AmendoimHub"
ScreenGui1.ResetOnSpawn = false

-- Main Frame 1
local MainFrame1 = Instance.new("Frame", ScreenGui1)
MainFrame1.Size = UDim2.new(0, 320, 0, 420)
MainFrame1.Position = UDim2.new(0.05, 0, 0.2, 0)
MainFrame1.BackgroundColor3 = Color3.fromRGB(10, 10, 10)
MainFrame1.BorderSizePixel = 0
MainFrame1.Active = true
MainFrame1.Draggable = true

local UICorner1 = Instance.new("UICorner", MainFrame1)
UICorner1.CornerRadius = UDim.new(0, 12)

-- Header 1
local Header1 = Instance.new("Frame", MainFrame1)
Header1.Size = UDim2.new(1, 0, 0, 45)
Header1.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
local HeaderCorner1 = Instance.new("UICorner", Header1)
HeaderCorner1.CornerRadius = UDim.new(0, 12)

local Title1 = Instance.new("TextLabel", Header1)
Title1.Size = UDim2.new(1, -50, 1, 0)
Title1.Position = UDim2.new(0, 15, 0, 0)
Title1.BackgroundTransparency = 1
Title1.Text = "⚡ Amendoim-Hub⚡"
Title1.TextColor3 = Color3.fromRGB(255, 220, 0)
Title1.Font = Enum.Font.GothamBold
Title1.TextSize = 22
Title1.TextXAlignment = Enum.TextXAlignment.Left

-- Botão minimizar 1
local ToggleButton1 = Instance.new("TextButton", Header1)
ToggleButton1.Size = UDim2.new(0, 45, 1, 0)
ToggleButton1.Position = UDim2.new(1, -45, 0, 0)
ToggleButton1.Text = "−"
ToggleButton1.BackgroundTransparency = 1
ToggleButton1.TextColor3 = Color3.fromRGB(255, 220, 0)
ToggleButton1.Font = Enum.Font.GothamBold
ToggleButton1.TextSize = 24

local MinimizedFrame1 = Instance.new("Frame", ScreenGui1)
MinimizedFrame1.Size = UDim2.new(0, 160, 0, 40)
MinimizedFrame1.Position = MainFrame1.Position
MinimizedFrame1.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
MinimizedFrame1.BorderSizePixel = 0
MinimizedFrame1.Active = true
MinimizedFrame1.Draggable = true
MinimizedFrame1.Visible = false

local MiniCorner1 = Instance.new("UICorner", MinimizedFrame1)
MiniCorner1.CornerRadius = UDim.new(0, 8)

local RestoreButton1 = Instance.new("TextButton", MinimizedFrame1)
RestoreButton1.Size = UDim2.new(1,0,1,0)
RestoreButton1.Text = "📂 Abrir Hub"
RestoreButton1.BackgroundTransparency = 1
RestoreButton1.TextColor3 = Color3.fromRGB(255,220,0)
RestoreButton1.Font = Enum.Font.GothamBold
RestoreButton1.TextSize = 18

ToggleButton1.MouseButton1Click:Connect(function()
	MainFrame1.Visible = false
	MinimizedFrame1.Position = MainFrame1.Position
	MinimizedFrame1.Visible = true
end)
RestoreButton1.MouseButton1Click:Connect(function()
	MainFrame1.Position = MinimizedFrame1.Position
	MainFrame1.Visible = true
	MinimizedFrame1.Visible = false
end)

-- Botões 1
local ButtonHolder1 = Instance.new("ScrollingFrame", MainFrame1)
ButtonHolder1.Size = UDim2.new(1,-20,1,-60)
ButtonHolder1.Position = UDim2.new(0,10,0,55)
ButtonHolder1.BackgroundTransparency = 1
ButtonHolder1.BorderSizePixel = 0
ButtonHolder1.ScrollBarThickness = 6
ButtonHolder1.CanvasSize = UDim2.new(0,0,0,0)

local UIListLayout1 = Instance.new("UIListLayout", ButtonHolder1)
UIListLayout1.Padding = UDim.new(0,10)
UIListLayout1.SortOrder = Enum.SortOrder.LayoutOrder

UIListLayout1:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()
	ButtonHolder1.CanvasSize = UDim2.new(0,0,0,UIListLayout1.AbsoluteContentSize.Y + 10)
end)

local function criarBotao1(nome, ativarFunc, desativarFunc)
	local btn = Instance.new("TextButton", ButtonHolder1)
	btn.Size = UDim2.new(1,0,0,45)
	btn.BackgroundColor3 = Color3.fromRGB(30,30,30)
	btn.TextColor3 = Color3.fromRGB(255,220,0)
	btn.Font = Enum.Font.GothamBold
	btn.TextSize = 18
	btn.Text = nome
	local btnCorner = Instance.new("UICorner", btn)
	btnCorner.CornerRadius = UDim.new(0,8)
	local ativo=false
	btn.MouseButton1Click:Connect(function()
		ativo = not ativo
		if ativo then
			btn.BackgroundColor3 = Color3.fromRGB(50,50,50)
			ativarFunc()
		else
			btn.BackgroundColor3 = Color3.fromRGB(30,30,30)
			if desativarFunc then desativarFunc() end
		end
	end)
end

-- Fly
criarBotao1("✈ Fly", function()
	loadstring(game:HttpGet("https://gist.githubusercontent.com/meozoneYT/bf037dff9f0a70017304ddd67fdcd370/raw/e14e74f425b060df523343cf30b787074eb3c5d2/arceus%2520x%2520fly%25202%2520obflucator",true))()
end)

-- ESP
local ESPEnabled = false
local skeletons, names, connections = {}, {}, {}
local cores = {
    police = Color3.fromRGB(0, 0, 255),
    criminals = Color3.fromRGB(255, 0, 0),
    prisoners = Color3.fromRGB(255, 140, 0),
    heroes = Color3.fromRGB(255, 255, 0),
    villains = Color3.fromRGB(128, 0, 128)
}

local function removerESP()
    for _, parts in pairs(skeletons) do
        for _, line in pairs(parts) do
            if line then line:Remove() end
        end
    end
    for _, text in pairs(names) do
        if text then text:Remove() end
    end
    skeletons, names = {}, {}
    for _, c in pairs(connections) do c:Disconnect() end
    connections = {}
end

local function criarESP(p)
    if p == player then return end
    local parts = {}
    for i = 1, 9 do
        local line = Drawing.new("Line")
        line.Thickness = 2
        line.Transparency = 1
        line.Visible = true
        table.insert(parts, line)
    end

    local text = Drawing.new("Text")
    text.Size = 15
    text.Center = true
    text.Outline = true
    text.Font = 2
    text.Visible = true

    skeletons[p] = parts
    names[p] = text

    table.insert(connections, RunService.RenderStepped:Connect(function()
        if not ESPEnabled then return end
        if p.Character and p.Character:FindFirstChild("HumanoidRootPart") and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
            local hrp = p.Character.HumanoidRootPart
            local head = p.Character:FindFirstChild("Head")
            local torso = p.Character:FindFirstChild("Torso") or p.Character:FindFirstChild("UpperTorso")
            local leftArm = p.Character:FindFirstChild("Left Arm") or p.Character:FindFirstChild("LeftUpperArm")
            local rightArm = p.Character:FindFirstChild("Right Arm") or p.Character:FindFirstChild("RightUpperArm")
            local leftLeg = p.Character:FindFirstChild("Left Leg") or p.Character:FindFirstChild("LeftUpperLeg")
            local rightLeg = p.Character:FindFirstChild("Right Leg") or p.Character:FindFirstChild("RightUpperLeg")
            local team = p.Team and p.Team.Name:lower() or ""
            local color = cores[team] or Color3.new(1,1,1)

            local function toScreen(part)
                if part then
                    local pos, onScreen = Camera:WorldToViewportPoint(part.Position)
                    return Vector2.new(pos.X, pos.Y), onScreen
                end
                return Vector2.new(0,0), false
            end

            -- posições
            local headPos, hOn = toScreen(head)
            local torsoPos, tOn = toScreen(torso)
            local lArmPos, laOn = toScreen(leftArm)
            local rArmPos, raOn = toScreen(rightArm)
            local lLegPos, llOn = toScreen(leftLeg)
            local rLegPos, rlOn = toScreen(rightLeg)

            local visible = hOn and tOn and laOn and raOn and llOn and rlOn

            if visible then
                -- linhas do esqueleto
                parts[1].From, parts[1].To = torsoPos, headPos
                parts[2].From, parts[2].To = torsoPos, lArmPos
                parts[3].From, parts[3].To = torsoPos, rArmPos
                parts[4].From, parts[4].To = torsoPos, lLegPos
                parts[5].From, parts[5].To = torsoPos, rLegPos

                parts[6].From, parts[6].To = lArmPos, torsoPos
                parts[7].From, parts[7].To = rArmPos, torsoPos
                parts[8].From, parts[8].To = lLegPos, torsoPos
                parts[9].From, parts[9].To = rLegPos, torsoPos

                for _, line in pairs(parts) do
                    line.Color = color
                    line.Visible = true
                end

                if head then
                    text.Position = headPos + Vector2.new(0, -20)
                    text.Text = p.Name
                    text.Color = color
                    text.Visible = true
                end
            else
                for _, line in pairs(parts) do line.Visible = false end
                text.Visible = false
            end
        else
            for _, line in pairs(parts) do line.Visible = false end
            text.Visible = false
        end
    end))
end

criarBotao1("👁 ESP", function()
	ESPEnabled = true
	for _,p in ipairs(Players:GetPlayers()) do criarESP(p) end
	table.insert(connections, Players.PlayerAdded:Connect(function(p)
		p.CharacterAdded:Connect(function() if ESPEnabled then criarESP(p) end end)
	end))
end, function()
	ESPEnabled=false
	removerESP()
end)

-- Aimbot
local AimPart, AimFov, AimSmoothness = "Head",120,0.15
local aiming, renderConnection = false,nil
local fovCircle = Drawing.new("Circle")
fovCircle.Radius,fovCircle.Thickness,fovCircle.Transparency=AimFov,2,1
fovCircle.Color,fovCircle.Filled,fovCircle.Visible=Color3.fromRGB(255,0,0),false,false
local function getClosest()
	local closest,dist=nil,AimFov
	for _,p in pairs(Players:GetPlayers()) do
		if p~=player and p.Character and p.Character:FindFirstChild(AimPart) and p.Character:FindFirstChild("Humanoid") and p.Character.Humanoid.Health>0 then
			local part=p.Character[AimPart]
			local pos,on=Camera:WorldToViewportPoint(part.Position)
			if on then
				local sPos,center=Vector2.new(pos.X,pos.Y),Vector2.new(Camera.ViewportSize.X/2,Camera.ViewportSize.Y/2)
				local mag=(sPos-center).Magnitude
				if mag<dist then dist,closest=mag,part end
			end
		end
	end
	return closest
end
local function ativarAimbot()
	aiming,fovCircle.Visible=true,true
	renderConnection=RunService.RenderStepped:Connect(function()
		fovCircle.Position=Vector2.new(Camera.ViewportSize.X/2,Camera.ViewportSize.Y/2)
		if aiming then
			local target=getClosest()
			if target then
				local camPos,newC=Camera.CFrame.Position,CFrame.new(Camera.CFrame.Position,target.Position)
				Camera.CFrame=Camera.CFrame:Lerp(newC,AimSmoothness)
			end
		end
	end)
end
local function desativarAimbot()
	aiming,fovCircle.Visible=false,false
	if renderConnection then renderConnection:Disconnect() renderConnection=nil end
end
criarBotao1("🎯 Aimbot",ativarAimbot,desativarAimbot)

-- No-Clip
local noclipEnabled = false
local noclipConnection

criarBotao1("👻 No-Clip", function()
    noclipEnabled = true
    noclipConnection = RunService.Stepped:Connect(function()
        if player.Character then
            for _, part in pairs(player.Character:GetChildren()) do
                if part:IsA("BasePart") and part.CanCollide then
                    part.CanCollide = false
                end
            end
        end
    end)
end, function()
    noclipEnabled = false
    if noclipConnection then
        noclipConnection:Disconnect()
        noclipConnection = nil
    end
    -- Restaurar colisão
    if player.Character then
        for _, part in pairs(player.Character:GetChildren()) do
            if part:IsA("BasePart") then
                part.CanCollide = true
            end
        end
    end
end)


--==================== HUB 2 - Gatuno Hub ====================--
local TweenService = game:GetService("TweenService")

local ScreenGui2 = Instance.new("ScreenGui", game.CoreGui)
ScreenGui2.Name = "GatunoHub"
ScreenGui2.ResetOnSpawn = false

local MainFrame2 = Instance.new("Frame", ScreenGui2)
MainFrame2.Size=UDim2.new(0,300,0,400)
MainFrame2.Position=UDim2.new(0.45,0,0.2,0)
MainFrame2.BackgroundColor3=Color3.fromRGB(10,10,10)
MainFrame2.BorderSizePixel=0
MainFrame2.Active=true
MainFrame2.Draggable=true

local UICorner2=Instance.new("UICorner",MainFrame2)
UICorner2.CornerRadius=UDim.new(0,12)

local Header2=Instance.new("Frame",MainFrame2)
Header2.Size=UDim2.new(1,0,0,45)
Header2.BackgroundColor3=Color3.fromRGB(20,20,20)
local HeaderCorner2=Instance.new("UICorner",Header2)
HeaderCorner2.CornerRadius=UDim.new(0,12)

local Title2=Instance.new("TextLabel",Header2)
Title2.Size=UDim2.new(1,-50,1,0)
Title2.Position=UDim2.new(0,15,0,0)
Title2.BackgroundTransparency=1
Title2.Text="🌟 Gatuno-Hub 🌟"
Title2.TextColor3=Color3.fromRGB(255,220,0)
Title2.Font=Enum.Font.GothamBold
Title2.TextSize=20
Title2.TextXAlignment=Enum.TextXAlignment.Left

local ToggleButton2=Instance.new("TextButton",Header2)
ToggleButton2.Size=UDim2.new(0,45,1,0)
ToggleButton2.Position=UDim2.new(1,-45,0,0)
ToggleButton2.Text="−"
ToggleButton2.BackgroundTransparency=1
ToggleButton2.TextColor3=Color3.fromRGB(255,220,0)
ToggleButton2.Font=Enum.Font.GothamBold
ToggleButton2.TextSize=22

local MinimizedFrame2=Instance.new("Frame",ScreenGui2)
MinimizedFrame2.Size=UDim2.new(0,150,0,40)
MinimizedFrame2.Position=MainFrame2.Position
MinimizedFrame2.BackgroundColor3=Color3.fromRGB(15,15,15)
MinimizedFrame2.BorderSizePixel=0
MinimizedFrame2.Active=true
MinimizedFrame2.Draggable=true
MinimizedFrame2.Visible=false

local MiniCorner2=Instance.new("UICorner",MinimizedFrame2)
MiniCorner2.CornerRadius=UDim.new(0,8)

local RestoreButton2=Instance.new("TextButton",MinimizedFrame2)
RestoreButton2.Size=UDim2.new(1,0,1,0)
RestoreButton2.Text="📂 Abrir Hub"
RestoreButton2.BackgroundTransparency=1
RestoreButton2.TextColor3=Color3.fromRGB(255,220,0)
RestoreButton2.Font=Enum.Font.GothamBold
RestoreButton2.TextSize=16

ToggleButton2.MouseButton1Click:Connect(function()
	MainFrame2.Visible=false
	MinimizedFrame2.Position=MainFrame2.Position
	MinimizedFrame2.Visible=true
end)
RestoreButton2.MouseButton1Click:Connect(function()
	MainFrame2.Position=MinimizedFrame2.Position
	MainFrame2.Visible=true
	MinimizedFrame2.Visible=false
end)

-- Botões 2
local ButtonHolder2=Instance.new("ScrollingFrame",MainFrame2)
ButtonHolder2.Size=UDim2.new(1,-20,1,-60)
ButtonHolder2.Position=UDim2.new(0,10,0,55)
ButtonHolder2.BackgroundTransparency=1
ButtonHolder2.BorderSizePixel=0
ButtonHolder2.ScrollBarThickness=6
ButtonHolder2.CanvasSize=UDim2.new(0,0,0,0)

local UIListLayout2=Instance.new("UIListLayout",ButtonHolder2)
UIListLayout2.Padding=UDim.new(0,10)
UIListLayout2.SortOrder=Enum.SortOrder.LayoutOrder

UIListLayout2:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()
	ButtonHolder2.CanvasSize=UDim2.new(0,0,0,UIListLayout2.AbsoluteContentSize.Y+10)
end)

local function criarBotao2(nome,destino)
	local btn=Instance.new("TextButton",ButtonHolder2)
	btn.Size=UDim2.new(1,0,0,40)
	btn.BackgroundColor3=Color3.fromRGB(30,30,30)
	btn.TextColor3=Color3.fromRGB(255,220,0)
	btn.Font=Enum.Font.GothamBold
	btn.TextSize=16
	btn.Text=nome
	local btnCorner=Instance.new("UICorner",btn)
	btnCorner.CornerRadius=UDim.new(0,8)
	btn.MouseEnter:Connect(function()
		TweenService:Create(btn,TweenInfo.new(0.2),{BackgroundColor3=Color3.fromRGB(50,50,50)}):Play()
	end)
	btn.MouseLeave:Connect(function()
		TweenService:Create(btn,TweenInfo.new(0.2),{BackgroundColor3=Color3.fromRGB(30,30,30)}):Play()
	end)
	btn.MouseButton1Click:Connect(function()
		local character=player.Character or player.CharacterAdded:Wait()
		local rootPart=character:WaitForChild("HumanoidRootPart")
		local info=TweenInfo.new(3,Enum.EasingStyle.Linear,Enum.EasingDirection.Out)
		local objetivo={Position=destino}
		local tween=TweenService:Create(rootPart,info,objetivo)
		tween:Play()
	end)
end

-- Teleportes
criarBotao2("Balada",Vector3.new(1176.3, 87.5, -10.0))
criarBotao2("Cassino",Vector3.new(1597.0, 45.3, 548.3))
criarBotao2("Joalheria",Vector3.new(-80.6, 87.3, 807.9))
criarBotao2("Aeroporto 2",Vector3.new(-2196.4, 38.4, -1536.7))
criarBotao2("Criminal",Vector3.new(2105.9, 41.4, 430.5))
criarBotao2("Lojinha-Armas",Vector3.new(-1641.9, 58.5, 714.6))
criarBotao2("Pirâmide",Vector3.new(-1057.2, 65.1, -543.3))
criarBotao2("Prisao",Vector3.new(-886.4, 151.6, -2919.7))
criarBotao2("Banco",Vector3.new(668.4, 65.2, 539.2))
