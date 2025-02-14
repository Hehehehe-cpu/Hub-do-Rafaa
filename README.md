local autor = "Rafael"
local versao = "1.0"

-- Funções
local function farmFruit(fruit)
    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = fruit.CFrame
    wait(0.5)
    game:GetService("ReplicatedStorage"):FindFirstChild("FruitPick"):FireServer(fruit)
end

local function getClosestFruit()
    local closestFruit = nil
    local closestDistance = math.huge
    for _, fruit in pairs(game:GetService("Workspace"):GetDescendants()) do
        if fruit.Name == "Dragon Fruit" and fruit:IsA("Part") then
            local distance = (fruit.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude
            if distance < closestDistance then
                closestFruit = fruit
                closestDistance = distance
            end
        end
    end
    return closestFruit
end

-- Loop de farm
while true do
    local closestFruit = getClosestFruit()
    if closestFruit then
        farmFruit(closestFruit)
    end
    wait(1)
end
