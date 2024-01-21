# Roblox-Selling-Items

For this example im going to use selling shoes as an example

First, you would need to create a shoe object in the game for the player to pick up. This can be done using the Model and Part functions in Roblox. For example:

Download
Copy code
local shoe = Instance.new("Model")
shoe.Name = "Shoe"
local shoePart = Instance.new("Part")
shoePart.Name = "ShoePart"
shoePart.Parent = shoe
shoePart.Position = Vector3.new(0, 1, 0)
shoePart.Size = Vector3.new(1, 1, 1)
shoePart.BrickColor = BrickColor.new("Bright blue")
shoe.Parent = game.Workspace
Next, you would need to create a script that allows the player to pick up the shoe. This can be done using the Humanoid and Touch functions in Roblox. For example:

Download
Copy code
local shoe = game.Workspace.Shoe
local shoeService = game:GetService("Service")

local function onTouch(otherPart)
    local character = otherPart.Parent
    if character and character:FindFirstChild("Humanoid") then
        local humanoid = character:FindFirstChild("Humanoid")
        humanoid.Health = humanoid.Health - 10
        shoe.Parent = character.Backpack
    end
end

shoe.Touched:Connect(onTouch)
This script will cause the player's character to lose 10 health points when they touch the shoe, and the shoe will be added to the player's backpack.

Finally, you would need to create a script that allows the player to sell the shoe. This can be done using the MarketplaceService and RemoteEvent functions in Roblox. For example:

Download
Copy code
local shoe = game.Workspace.Shoe
local marketplaceService = game:GetService("MarketplaceService")
local sellEvent = Instance.new("RemoteEvent")
sellEvent.Name = "SellShoe"
sellEvent.Parent = game

local function onSell(player)
    local shoe = player.Backpack:FindFirstChild("ShoePart")
    if shoe then
        marketplaceService:PromptProductPurchase(player, shoe.Parent.Name, 50)
        shoe.Parent = game.Workspace
    end
end

sellEvent.OnServerEvent:Connect(onSell)
This script will create a remote event called SellShoe that players can use to sell the shoe. When the event is triggered, the shoe will be removed from the player's backpack and they will be prompted to purchase it for 50 robux. If the player successfully purchases the shoe, it will be added back to the game world.
