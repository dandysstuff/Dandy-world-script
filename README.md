local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/shlexware/Orion/main/source')))()
local Window = OrionLib:MakeWindow({Name = "R4yHub | DandyWorld",IntroText = "R4yhub", HidePremium = false, SaveConfig = true, ConfigFolder = "OrionTest"})

local tab = Window:MakeTab({ 
    Name = "Main",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

local pl = game.Players.LocalPlayer
local char = pl.Character
local humanoid = char:WaitForChild("Humanoid")

local table = {
    speed = 0
}

tab:AddSlider({
	Name = "Walk speed",
	Min = 0,
	Max = 100,
	Default = 16,
	Color = Color3.fromRGB(255,255,255),
	Increment = 1,
	ValueName = "Walk speed",
	Callback = function(Value)
        while Wait() do
            table.speed = Value
        end
	end    
})


local on = false

tab:AddButton({
    Name = "Change walk speed",
    Callback = function(bool)
            while  Wait() do
                humanoid.WalkSpeed = table.speed
            end
    end

})



local runservice = game:GetService("RunService")
local esp = Instance.new("Highlight")
esp.Name = "hl"
esp.DepthMode = Enum.HighlightDepthMode.AlwaysOnTop
esp.OutlineTransparency = 1


tab:AddButton({
    Name = "Monsters esp",
    Callback = function()

       for _,k in pairs(game.Workspace.CurrentRoom:GetChildren()) do
        if k:IsA("Model") then
            local room = k
            for _,v in pairs(room:FindFirstChild("Monsters"):GetChildren()) do
                local folder = v
                runservice.Heartbeat:Connect(function()
                    for _, v in pairs(folder:GetChildren()) do
                        repeat Wait() until v
                        if not v:FindFirstChild("hl") then
                            local hlclone = esp:Clone()
                            hlclone.Adornee = v
                            hlclone.Parent = v
                        end
                    end
                end)
            end
        end
       end
        
    end
})
