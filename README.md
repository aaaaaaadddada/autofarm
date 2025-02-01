local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")
local debrisFolder = workspace:FindFirstChild("Debris")


local function getClosestItem()
    if not debrisFolder then return nil end

    local closestItem = nil
    local minDistance = math.huge

    for _, item in pairs(debrisFolder:GetChildren()) do
        if item:IsA("MeshPart") then
            local distance = (humanoidRootPart.Position - item.Position).Magnitude
            if distance < minDistance then
                minDistance = distance
                closestItem = item
            end
        end
    end

    return closestItem
end


local function pressKeyE()
    local VirtualInputManager = game:GetService("VirtualInputManager")
    VirtualInputManager:SendKeyEvent(true, Enum.KeyCode.E, false, game)
    wait(2)
    VirtualInputManager:SendKeyEvent(false, Enum.KeyCode.E, false, game)
end


while true do
    local item = getClosestItem()
    if item then
        humanoidRootPart.CFrame = item.CFrame 
        wait(0.5)

        
        while item.Parent ~= nil do
            pressKeyE()
            wait(1) 
        end
    end
    wait(2) 
end
