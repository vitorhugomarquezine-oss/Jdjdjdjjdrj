local CG = game:GetService("CoreGui")
local PG = game:GetService("Players").LocalPlayer:WaitForChild("PlayerGui")
local Pai = CG or PG
 
local antiga = Pai:FindFirstChild("GiroUI")
if antiga then antiga:Destroy() end
 
local SG = Instance.new("ScreenGui", Pai)
SG.Name = "GiroUI"; SG.ResetOnSpawn = false
 
local Main = Instance.new("Frame", SG)
Main.Size, Main.Position = UDim2.new(0, 200, 0, 120), UDim2.new(0.4, 0, 0.4, 0)
Main.BackgroundColor3, Main.Active, Main.Draggable = Color3.fromRGB(20, 20, 20), true, true
Instance.new("UICorner", Main).CornerRadius = UDim.new(0, 8)
 
local Title = Instance.new("TextLabel", Main)
Title.Size, Title.Text, Title.TextColor3 = UDim2.new(1, 0, 0, 30), "🇧🇷♥️🇵🇹", Color3.fromRGB(255, 255, 255)
Title.Font, Title.TextSize, Title.BackgroundTransparency = "GothamBold", 14, 1
 
local Input = Instance.new("TextBox", Main)
Input.Size, Input.Position = UDim2.new(0.9, 0, 0, 25), UDim2.new(0.05, 0, 0, 35)
Input.BackgroundColor3, Input.Text, Input.TextColor3 = Color3.fromRGB(35, 35, 35), "World1", Color3.fromRGB(255, 255, 255)
Input.Font, Input.TextSize = "Gotham", 12
Instance.new("UICorner", Input).CornerRadius = UDim.new(0, 5)
 
local Btn = Instance.new("TextButton", Main)
Btn.Size, Btn.Position = UDim2.new(0.9, 0, 0, 30), UDim2.new(0.05, 0, 0, 70)
Btn.BackgroundColor3, Btn.Text, Btn.TextColor3 = Color3.fromRGB(180, 40, 40), "OFF", Color3.fromRGB(255, 255, 255)
Btn.Font, Btn.TextSize = "GothamBold", 13
Instance.new("UICorner", Btn).CornerRadius = UDim.new(0, 5)
 
local Ativo = false
Btn.MouseButton1Click:Connect(function()
    Ativo = not Ativo
    Btn.BackgroundColor3 = Ativo and Color3.fromRGB(40, 180, 40) or Color3.fromRGB(180, 40, 40)
    Btn.Text = Ativo and "ON" or "OFF"
 
    if Ativo then
        task.spawn(function()
            local remote = game:GetService("ReplicatedStorage"):WaitForChild("BridgeNet2"):WaitForChild("dataRemoteEvent")
            while Ativo do
                pcall(remote.FireServer, remote, {[1] = {["__BridgeTuplePayload__"] = true, ["Payload"] = {[1] = Input.Text, ["n"] = 2}}, [2] = "\\"})
                task.wait(0.1)
            end
        end)
    end
end)
