-- Fly Script Básico
local player = game.Players.LocalPlayer
local char = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = char:WaitForChild("HumanoidRootPart")

local flying = false
local speed = 50  -- Velocidad de vuelo

-- Crear cuerpo de movimiento
local bodyGyro = Instance.new("BodyGyro")
local bodyVelocity = Instance.new("BodyVelocity")
bodyGyro.P = 9e4
bodyGyro.maxTorque = Vector3.new(9e9, 9e9, 9e9)
bodyGyro.cframe = humanoidRootPart.CFrame
bodyGyro.Parent = humanoidRootPart

bodyVelocity.velocity = Vector3.new(0, 0, 0)
bodyVelocity.maxForce = Vector3.new(9e9, 9e9, 9e9)
bodyVelocity.Parent = humanoidRootPart

-- Activar vuelo
flying = true

-- Conexión al input del teclado
local UIS = game:GetService("UserInputService")

UIS.InputBegan:Connect(function(input)
    if input.KeyCode == Enum.KeyCode.Space then
        bodyVelocity.velocity = Vector3.new(0, speed, 0)
    end
end)

UIS.InputEnded:Connect(function(input)
    if input.KeyCode == Enum.KeyCode.Space then
        bodyVelocity.velocity = Vector3.new(0, 0, 0)
    end
end)

-- Finalización al morir
char:WaitForChild("Humanoid").Died:Connect(function()
    bodyGyro:Destroy()
    bodyVelocity:Destroy()
end)

print("Vuelo activado: Mantén ESPACIO para volar.")