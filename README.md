
local animations = {
    {id = "rbxassetid://16945573694", name = "Ravage"},
    {id = "rbxassetid://16945550029", name = "Ravage full move"},
    {id = "rbxassetid://16944345619", name = "Swift Sweep"},
    {id = "rbxassetid://17325254223", name = "Collateral ruin"},
    {id = "rbxassetid://18447913645", name = "Wall combo"},
    {id = "rbxassetid://17140902079", name = "Ult anim 1"},
    {id = "rbxassetid://18445236460", name = "Ult anim 2"},
    {id = "rbxassetid://17141153099", name = "Stoic bomb"},
    {id = "rbxassetid://17354976067", name = "20-20-20 Dropkick"},
    {id = "rbxassetid://17420452843", name = "20-20-20 Dropkick Hit"}
}

local screenGui = Instance.new("ScreenGui")
screenGui.Name = "MovableScreenGui"
screenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")


local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 350, 0, 400)
frame.Position = UDim2.new(0.5, -175, 0.5, -200)
frame.BackgroundColor3 = Color3.fromRGB(200, 200, 200)
frame.Active = true
frame.Draggable = true
frame.Parent = screenGui


local closeButton = Instance.new("TextButton")
closeButton.Size = UDim2.new(0, 100, 0, 50)
closeButton.Position = UDim2.new(0, 0, 0, -50)
closeButton.Text = "Eliminar UI"
closeButton.Parent = frame


local function playAnimation(animationId)
    local player = game.Players.LocalPlayer
    local character = player.Character or player.CharacterAdded:Wait()
    local humanoid = character:WaitForChild("Humanoid")
    local animator = humanoid:FindFirstChild("Animator")

    if not animator then
        animator = Instance.new("Animator")
        animator.Parent = humanoid
    end

    local animation = Instance.new("Animation")
    animation.AnimationId = animationId
    local animationTrack = animator:LoadAnimation(animation)
    animationTrack:Play()
end


local function onCloseButtonClicked()
    screenGui:Destroy()
end


closeButton.MouseButton1Click:Connect(onCloseButtonClicked)


for i, anim in ipairs(animations) do
    local button = Instance.new("TextButton")
    button.Size = UDim2.new(0, 150, 0, 50)
    button.Position = UDim2.new(0.1, 0, (i - 1) * 0.1 + 0.1, 0)
    button.Text = anim.name
    button.Parent = frame

    
    button.MouseButton1Click:Connect(function()
        playAnimation(anim.id)
    end)
end
