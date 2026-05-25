local TweenService = game:GetService("TweenService")
local UserInputService = game:GetService("UserInputService")
local CoreGui = game:GetService("CoreGui")
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local Player = Players.LocalPlayer
local HttpService = game:GetService("HttpService")

local Library = {}
local ConfigFileName = "WackShop_Config.json"

local SavedConfig = {
Width = 520,
Height = 340,
RGB = false,
ThemeColor = {0, 190, 255}
}

local function LoadConfig()
if isfile and isfile(ConfigFileName) then
local ok, res = pcall(function()
return HttpService:JSONDecode(readfile(ConfigFileName))
end)
if ok and type(res) == "table" then
for k, v in pairs(res) do SavedConfig[k] = v end
end
end
end

local function SaveConfig()
if writefile then
pcall(function()
writefile(ConfigFileName, HttpService:JSONEncode(SavedConfig))
end)
end
end

LoadConfig()

local function MakeDraggable(frame, handle)
local dragging, dragInput, dragStart, startPos
handle.InputBegan:Connect(function(input)
if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
dragging = true
dragStart = input.Position
startPos = frame.Position
input.Changed:Connect(function()
if input.UserInputState == Enum.UserInputState.End then dragging = false end
end)
end
end)
frame.InputChanged:Connect(function(input)
if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
dragInput = input
end
end)
UserInputService.InputChanged:Connect(function(input)
if input == dragInput and dragging then
local delta = input.Position - dragStart
frame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
end
end)
end

function Library:NewWindow(title)
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "WackShopUI"
ScreenGui.ResetOnSpawn = false
ScreenGui.IgnoreGuiInset = true
ScreenGui.Parent = CoreGui

local currentThemeColor = Color3.fromRGB(unpack(SavedConfig.ThemeColor))  

local MainFrame = Instance.new("Frame")  
MainFrame.Name = "MainFrame"  
MainFrame.Size = UDim2.fromOffset(SavedConfig.Width, SavedConfig.Height)  
MainFrame.Position = UDim2.new(0.5, -(SavedConfig.Width/2), 0.5, -(SavedConfig.Height/2))  
MainFrame.BackgroundColor3 = Color3.fromRGB(11, 11, 18)  
MainFrame.BorderSizePixel = 0  
MainFrame.ClipsDescendants = true  
MainFrame.Visible = false  
MainFrame.Parent = ScreenGui  
Instance.new("UICorner", MainFrame).CornerRadius = UDim.new(0, 14)  

local OuterStroke = Instance.new("UIStroke", MainFrame)  
OuterStroke.Color = currentThemeColor  
OuterStroke.Thickness = 1.8  

local BG = Instance.new("UIGradient", MainFrame)  
BG.Color = ColorSequence.new({  
    ColorSequenceKeypoint.new(0, Color3.fromRGB(15, 16, 26)),  
    ColorSequenceKeypoint.new(1, Color3.fromRGB(9, 9, 15))  
})  
BG.Rotation = 135  

-- TopBar  
local TopBar = Instance.new("Frame")  
TopBar.Size = UDim2.new(1, 0, 0, 50)  
TopBar.BackgroundColor3 = Color3.fromRGB(14, 15, 24)  
TopBar.BorderSizePixel = 0  
TopBar.ZIndex = 5  
TopBar.Parent = MainFrame  
Instance.new("UICorner", TopBar).CornerRadius = UDim.new(0, 14)  

local TopBarFix = Instance.new("Frame")  
TopBarFix.Size = UDim2.new(1, 0, 0, 14)  
TopBarFix.Position = UDim2.new(0, 0, 1, -14)  
TopBarFix.BackgroundColor3 = Color3.fromRGB(14, 15, 24)  
TopBarFix.BorderSizePixel = 0  
TopBarFix.ZIndex = 5  
TopBarFix.Parent = TopBar  

local TopLine = Instance.new("Frame")  
TopLine.Size = UDim2.new(1, 0, 0, 1)  
TopLine.Position = UDim2.new(0, 0, 1, -1)  
TopLine.BackgroundColor3 = currentThemeColor  
TopLine.BackgroundTransparency = 0.5  
TopLine.ZIndex = 6  
TopLine.Parent = TopBar  

local AvatarFrame = Instance.new("Frame")  
AvatarFrame.Size = UDim2.fromOffset(32, 32)  
AvatarFrame.Position = UDim2.new(0, 12, 0.5, -16)  
AvatarFrame.BackgroundColor3 = Color3.fromRGB(22, 23, 38)  
AvatarFrame.ZIndex = 6  
AvatarFrame.Parent = TopBar  
Instance.new("UICorner", AvatarFrame).CornerRadius = UDim.new(1, 0)  

local AvatarStroke = Instance.new("UIStroke", AvatarFrame)  
AvatarStroke.Color = currentThemeColor  

local AvatarImg = Instance.new("ImageLabel")  
AvatarImg.Size = UDim2.new(1, 0, 1, 0)  
AvatarImg.BackgroundTransparency = 1  
AvatarImg.Image = "rbxthumb://type=AvatarHeadShot&id=" .. Player.UserId .. "&w=150&h=150"  
AvatarImg.ZIndex = 7  
AvatarImg.Parent = AvatarFrame  
Instance.new("UICorner", AvatarImg).CornerRadius = UDim.new(1, 0)  

local NameLabel = Instance.new("TextLabel")  
NameLabel.Size = UDim2.fromOffset(120, 20)  
NameLabel.Position = UDim2.new(0, 52, 0.5, -10)  
NameLabel.BackgroundTransparency = 1  
NameLabel.Text = Player.Name  
NameLabel.TextColor3 = currentThemeColor  
NameLabel.Font = Enum.Font.GothamBold  
NameLabel.TextSize = 12  
NameLabel.TextXAlignment = Enum.TextXAlignment.Left  
NameLabel.ZIndex = 6  
NameLabel.Parent = TopBar  

local TitleLabel = Instance.new("TextLabel")  
TitleLabel.Size = UDim2.new(0, 160, 1, 0)  
TitleLabel.Position = UDim2.new(0.5, -80, 0, 0)  
TitleLabel.BackgroundTransparency = 1  
TitleLabel.Text = title  
TitleLabel.TextColor3 = Color3.fromRGB(240, 240, 250)  
TitleLabel.Font = Enum.Font.GothamBold  
TitleLabel.TextSize = 14  
TitleLabel.ZIndex = 6  
TitleLabel.Parent = TopBar  

local CloseBtn = Instance.new("TextButton")  
CloseBtn.Size = UDim2.fromOffset(28, 28)  
CloseBtn.AnchorPoint = Vector2.new(1, 0.5)  
CloseBtn.Position = UDim2.new(1, -12, 0.5, 0)  
CloseBtn.BackgroundColor3 = Color3.fromRGB(220, 50, 50)  
CloseBtn.Text = "×"  
CloseBtn.TextColor3 = Color3.new(1, 1, 1)  
CloseBtn.Font = Enum.Font.GothamBold  
CloseBtn.TextSize = 18  
CloseBtn.AutoButtonColor = false  
CloseBtn.ZIndex = 10  
CloseBtn.Parent = TopBar  
Instance.new("UICorner", CloseBtn).CornerRadius = UDim.new(0, 8)  

CloseBtn.MouseButton1Click:Connect(function()  
    ScreenGui:Destroy()  
end)  

MakeDraggable(MainFrame, TopBar)  

-- Sidebar (ไม่ใช้ UICorner ให้ ClipsDescendants ของ MainFrame จัดการ)  
local Sidebar = Instance.new("Frame")  
Sidebar.Name = "Sidebar"  
Sidebar.Size = UDim2.new(0, 125, 1, -50)  
Sidebar.Position = UDim2.new(0, 0, 0, 50)  
Sidebar.BackgroundColor3 = Color3.fromRGB(12, 13, 20)  
Sidebar.BorderSizePixel = 0  
Sidebar.ClipsDescendants = true  
Sidebar.Parent = MainFrame  

local SideLine = Instance.new("Frame")  
SideLine.Size = UDim2.new(0, 1, 1, 0)  
SideLine.Position = UDim2.new(1, 0, 0, 0)  
SideLine.BackgroundColor3 = currentThemeColor  
SideLine.BackgroundTransparency = 0.8  
SideLine.BorderSizePixel = 0  
SideLine.ZIndex = 7  
SideLine.Parent = Sidebar  

local SideLayout = Instance.new("UIListLayout", Sidebar)  
SideLayout.Padding = UDim.new(0, 4)  
SideLayout.SortOrder = Enum.SortOrder.LayoutOrder  

local SidePad = Instance.new("UIPadding", Sidebar)  
SidePad.PaddingTop = UDim.new(0, 10)  
SidePad.PaddingLeft = UDim.new(0, 8)  
SidePad.PaddingRight = UDim.new(0, 8)  
SidePad.PaddingBottom = UDim.new(0, 10)  

local ContentFrame = Instance.new("Frame")  
ContentFrame.Size = UDim2.new(1, -137, 1, -62)  
ContentFrame.Position = UDim2.new(0, 131, 0, 56)  
ContentFrame.BackgroundTransparency = 1  
ContentFrame.Parent = MainFrame  

-- Toggle Button (ปุ่ม W ลอยอยู่)  
local ToggleBtn = Instance.new("TextButton")  
ToggleBtn.Size = UDim2.fromOffset(44, 44)  
ToggleBtn.Position = UDim2.new(0, 10, 0.5, -22)  
ToggleBtn.BackgroundColor3 = Color3.fromRGB(15, 16, 26)  
ToggleBtn.Text = "W"  
ToggleBtn.TextColor3 = currentThemeColor  
ToggleBtn.Font = Enum.Font.GothamBold  
ToggleBtn.TextSize = 20  
ToggleBtn.AutoButtonColor = false  
ToggleBtn.ZIndex = 99999  
ToggleBtn.Parent = ScreenGui  
Instance.new("UICorner", ToggleBtn).CornerRadius = UDim.new(1, 0)  

local wStroke = Instance.new("UIStroke", ToggleBtn)  
wStroke.Color = currentThemeColor  
wStroke.Thickness = 1.8  

ToggleBtn.MouseButton1Click:Connect(function()  
    MainFrame.Visible = not MainFrame.Visible  
end)  

MakeDraggable(ToggleBtn, ToggleBtn)  

local Tabs = {}  

local function UpdateStaticColors(color)  
    OuterStroke.Color = color  
    wStroke.Color = color  
    ToggleBtn.TextColor3 = color  
    AvatarStroke.Color = color  
    TopLine.BackgroundColor3 = color  
    SideLine.BackgroundColor3 = color  
    NameLabel.TextColor3 = color  
    for _, v in pairs(Tabs) do  
        if v.Content.Visible then  
            v.Btn.TextColor3 = color  
            v.Ind.BackgroundColor3 = color  
        end  
    end  
end  

local rgbConnection  
if SavedConfig.RGB then  
    rgbConnection = RunService.RenderStepped:Connect(function()  
        local hue = (tick() % 5) / 5  
        UpdateStaticColors(Color3.fromHSV(hue, 0.85, 1))  
    end)  
end  

-- WindowFunctions  
local WindowFunctions = {}  

function WindowFunctions:NewTab(tabName, icon)  
    local tabContent = Instance.new("ScrollingFrame")  
    tabContent.Size = UDim2.new(1, 0, 1, 0)  
    tabContent.BackgroundTransparency = 1  
    tabContent.BorderSizePixel = 0  
    tabContent.ScrollBarThickness = 3  
    tabContent.ScrollBarImageColor3 = currentThemeColor  
    tabContent.Visible = false  
    tabContent.Parent = ContentFrame  

    local tabLayout = Instance.new("UIListLayout", tabContent)  
    tabLayout.Padding = UDim.new(0, 6)  
    tabLayout.SortOrder = Enum.SortOrder.LayoutOrder  

    local tabPad = Instance.new("UIPadding", tabContent)  
    tabPad.PaddingTop = UDim.new(0, 4)  
    tabPad.PaddingRight = UDim.new(0, 6)  

    tabLayout.Changed:Connect(function()  
        tabContent.CanvasSize = UDim2.new(0, 0, 0, tabLayout.AbsoluteContentSize.Y + 10)  
    end)  

    local TabBtn = Instance.new("TextButton")  
    TabBtn.Size = UDim2.new(1, 0, 0, 34)  
    TabBtn.BackgroundColor3 = Color3.fromRGB(18, 19, 30)  
    TabBtn.BackgroundTransparency = 1  
    TabBtn.Text = (icon or "") .. " " .. tabName  
    TabBtn.TextColor3 = Color3.fromRGB(120, 120, 140)  
    TabBtn.Font = Enum.Font.Gotham  
    TabBtn.TextSize = 11  
    TabBtn.AutoButtonColor = false  
    TabBtn.ZIndex = 8  
    TabBtn.Parent = Sidebar  
    Instance.new("UICorner", TabBtn).CornerRadius = UDim.new(0, 8)  

    local Indicator = Instance.new("Frame")  
    Indicator.Size = UDim2.new(0, 3, 0.6, 0)  
    Indicator.Position = UDim2.new(0, -2, 0.2, 0)  
    Indicator.BackgroundColor3 = currentThemeColor  
    Indicator.BackgroundTransparency = 1  
    Indicator.BorderSizePixel = 0  
    Indicator.ZIndex = 9  
    Indicator.Parent = TabBtn  
    Instance.new("UICorner", Indicator).CornerRadius = UDim.new(1, 0)  

    local tabEntry = {Btn = TabBtn, Content = tabContent, Ind = Indicator}  
    table.insert(Tabs, tabEntry)  

    local function SelectTab()  
        for _, v in pairs(Tabs) do  
            v.Content.Visible = false  
            v.Btn.TextColor3 = Color3.fromRGB(120, 120, 140)  
            v.Btn.BackgroundTransparency = 1  
            v.Ind.BackgroundTransparency = 1  
        end  
        tabContent.Visible = true  
        TabBtn.TextColor3 = currentThemeColor  
        TabBtn.BackgroundTransparency = 0.85  
        Indicator.BackgroundTransparency = 0  
    end  

    TabBtn.MouseButton1Click:Connect(SelectTab)  
    if #Tabs == 1 then SelectTab() end  

    local TabFunctions = {}  

    function TabFunctions:NewButton(btnText, callback)  
        local Btn = Instance.new("TextButton")  
        Btn.Size = UDim2.new(1, 0, 0, 32)  
        Btn.BackgroundColor3 = Color3.fromRGB(18, 19, 32)  
        Btn.Text = btnText  
        Btn.TextColor3 = Color3.fromRGB(210, 210, 225)  
        Btn.Font = Enum.Font.Gotham  
        Btn.TextSize = 12  
        Btn.AutoButtonColor = false  
        Btn.ZIndex = 8  
        Btn.Parent = tabContent  
        Instance.new("UICorner", Btn).CornerRadius = UDim.new(0, 8)  

        local BtnStroke = Instance.new("UIStroke", Btn)  
        BtnStroke.Color = Color3.fromRGB(35, 36, 55)  
        BtnStroke.Thickness = 1  

        Btn.MouseEnter:Connect(function()  
            TweenService:Create(Btn, TweenInfo.new(0.15), {BackgroundColor3 = Color3.fromRGB(28, 30, 48)}):Play()  
        end)  
        Btn.MouseLeave:Connect(function()  
            TweenService:Create(Btn, TweenInfo.new(0.15), {BackgroundColor3 = Color3.fromRGB(18, 19, 32)}):Play()  
        end)  
        Btn.MouseButton1Click:Connect(function()  
            pcall(callback)  
        end)  
    end  

    function TabFunctions:NewToggle(toggleText, default, callback)  
        local state = default or false  

        local Row = Instance.new("Frame")  
        Row.Size = UDim2.new(1, 0, 0, 32)  
        Row.BackgroundColor3 = Color3.fromRGB(18, 19, 32)  
        Row.ZIndex = 8  
        Row.Parent = tabContent  
        Instance.new("UICorner", Row).CornerRadius = UDim.new(0, 8)  
        Instance.new("UIStroke", Row).Color = Color3.fromRGB(35, 36, 55)  

        local Label = Instance.new("TextLabel")  
        Label.Size = UDim2.new(1, -50, 1, 0)  
        Label.Position = UDim2.new(0, 10, 0, 0)  
        Label.BackgroundTransparency = 1  
        Label.Text = toggleText  
        Label.TextColor3 = Color3.fromRGB(210, 210, 225)  
        Label.Font = Enum.Font.Gotham  
        Label.TextSize = 12  
        Label.TextXAlignment = Enum.TextXAlignment.Left  
        Label.ZIndex = 9  
        Label.Parent = Row  

        local Track = Instance.new("Frame")  
        Track.Size = UDim2.fromOffset(36, 18)  
        Track.AnchorPoint = Vector2.new(1, 0.5)  
        Track.Position = UDim2.new(1, -10, 0.5, 0)  
        Track.BackgroundColor3 = Color3.fromRGB(40, 40, 60)  
        Track.ZIndex = 9  
        Track.Parent = Row  
        Instance.new("UICorner", Track).CornerRadius = UDim.new(1, 0)  

        local Knob = Instance.new("Frame")  
        Knob.Size = UDim2.fromOffset(12, 12)  
        Knob.AnchorPoint = Vector2.new(0, 0.5)  
        Knob.Position = UDim2.new(0, 3, 0.5, 0)  
        Knob.BackgroundColor3 = Color3.fromRGB(160, 160, 180)  
        Knob.ZIndex = 10  
        Knob.Parent = Track  
        Instance.new("UICorner", Knob).CornerRadius = UDim.new(1, 0)  

        local function SetToggle(val)  
            state = val  
            if state then  
                TweenService:Create(Knob, TweenInfo.new(0.15), {Position = UDim2.new(0, 21, 0.5, 0), BackgroundColor3 = currentThemeColor}):Play()  
                TweenService:Create(Track, TweenInfo.new(0.15), {BackgroundColor3 = Color3.fromRGB(0, 60, 80)}):Play()  
            else  
                TweenService:Create(Knob, TweenInfo.new(0.15), {Position = UDim2.new(0, 3, 0.5, 0), BackgroundColor3 = Color3.fromRGB(160, 160, 180)}):Play()  
                TweenService:Create(Track, TweenInfo.new(0.15), {BackgroundColor3 = Color3.fromRGB(40, 40, 60)}):Play()  
            end  
            pcall(callback, state)  
        end  

        SetToggle(state)  
        Row.InputBegan:Connect(function(input)  
            if input.UserInputType == Enum.UserInputType.MouseButton1 then  
                SetToggle(not state)  
            end  
        end)  
    end  

    return TabFunctions  
end  

-- ==================== TABS ====================  

local Tab1 = WindowFunctions:NewTab("เคลื่อนไหว", "⚡")  
Tab1:NewButton("🔴 บิน", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/redfabza/FLY/refs/heads/main/FLY.lua"))() end)  
Tab1:NewButton("🔴 กระโดดไม่จำกัด", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/redfabza/jump/refs/heads/main/Jump"))() end)  
Tab1:NewButton("🔴 วิ่งเร็ว", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/redfabza/speed/refs/heads/main/speed"))() end)  
Tab1:NewButton("🔴 วาป", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/redfabza/Teleport/refs/heads/main/Teleport"))() end)  
Tab1:NewButton("🔴 ทะลุกำแพง", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/redfabza/Through-the-map/refs/heads/main/Through%20the%20map"))() end)  
Tab1:NewButton("🔴 หายตัว", function() loadstring(game:HttpGet("https://pastebin.com/raw/3Rnd9rHf"))() end)  
Tab1:NewButton("🔴 อมตะ", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/redfabza/GOD/refs/heads/main/GOD.lua"))() end)  

local Tab2 = WindowFunctions:NewTab("โจมตี", "⚔️")  
Tab2:NewButton("🟠 ล็อคหัวผู้เล่น", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/redfabza/Aimlock/refs/heads/main/%E0%B8%A5%E0%B9%87%E0%B8%AD%E0%B8%84%E0%B9%80%E0%B8%9B%E0%B9%89%E0%B8%B2.lua"))() end)  
Tab2:NewButton("🟠 ฆ่าบอทออร่า", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/wackshopr-tech/script-roblox-all/refs/heads/main/SCRIPT-ALL-BY-WACK-SHOP/kill-all-bot/killall-npc..lua"))() end)  
Tab2:NewButton("🟠 Hitbox", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/redfabza/Hitbox/refs/heads/main/Hitbox"))() end)  

local Tab3 = WindowFunctions:NewTab("เครื่องมือ", "🛠️")  
Tab3:NewButton("🟡 เพิ่มความลื่น", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/redfabza/FPS-BOOST/refs/heads/main/FPS_BOOST.lua"))() end)  
Tab3:NewButton("🟡 แมพสว่าง", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/redfabza/Bright-map/refs/heads/main/%E0%B8%9B%E0%B8%A3%E0%B8%B1%E0%B8%9A%E0%B8%84%E0%B8%A7%E0%B8%B2%E0%B8%A1%E0%B8%AA%E0%B8%A7%E0%B9%88%E0%B8%B2%E0%B8%87"))() end)  
Tab3:NewButton("🟡 เสกของ", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/redfabza/Earth-profile-/refs/heads/main/%E0%B9%80%E0%B8%AA%E0%B8%81%E0%B8%82%E0%B8%AD%E0%B8%87"))() end)  
Tab3:NewButton("🟡 แป้นพิมพ์", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/Xxtan31/Ata/main/deltakeyboardcrack.txt"))() end)  
Tab3:NewButton("🟡 ปรับความเร็วรถ", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/redfabza/speed-car/refs/heads/main/car%20speed"))() end)  
Tab3:NewButton("🟡 Infinite Yield", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/EdgeIY/infiniteyield/master/source"))() end)  
Tab3:NewButton("🟡 Quirky CMD", function() loadstring(game:HttpGet("https://gist.github.com/someunknowndude/38cecea5be9d75cb743eac8b1eaf6758/raw"))() end)  

local Tab4 = WindowFunctions:NewTab("แกล้ง", "🎭")  
Tab4:NewButton("🟢 หลุมดำ", function() loadstring(game:HttpGet("https://pastebin.com/raw/pkZnU5P5"))() end)  
Tab4:NewButton("🟢 ชนกระเด็น", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/wackshopr-tech/script-roblox-all/refs/heads/main/SCRIPT-ALL-BY-WACK-SHOP/FLINGCORE/FLINGCORE.lua"))() end)  
Tab4:NewButton("🟢 ดึงคน", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/wackshopr-tech/script-roblox-all/refs/heads/main/SCRIPT-ALL-BY-WACK-SHOP/pull%20false%20people/pull-false-people.lua"))() end)  
Tab4:NewButton("🟢 จับน้องชาย", function()
    loadstring(game:HttpGet("https://pastefy.app/wa3v2Vgm/raw"))()
end)  
Tab4:NewButton("🟢 F3X", function() loadstring(game:HttpGet("https://pastebin.com/raw/FZmTykdY"))() end)  

local Tab5 = WindowFunctions:NewTab("ดวงตาเทพ", "👁️")  
Tab5:NewButton("🟣 ESP Players", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/redfabza/ESP/refs/heads/main/ESP.lua"))() end)  
Tab5:NewButton("🟣 ESP NPC", function() loadstring(game:HttpGet("https://raw.githubusercontent.com/redfabza/ESP-BOT/refs/heads/main/ESP%20BOT.lua"))() end)  

return WindowFunctions

end

return Library
