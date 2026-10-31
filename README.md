
-- JK ULTRA POTATO GRAPHICS
-- Extreme visual simplification
-- LocalScript

local Lighting = game:GetService("Lighting")
local Workspace = game:GetService("Workspace")

local function optimize(obj)

    pcall(function()

        -- PARTS
        if obj:IsA("BasePart") then
            obj.Material = Enum.Material.SmoothPlastic
            obj.Reflectance = 0
            obj.CastShadow = false

        -- REMOVE TEXTURES
        elseif obj:IsA("Decal") or obj:IsA("Texture") then
            obj:Destroy()

        elseif obj:IsA("SurfaceAppearance") then
            obj:Destroy()

        elseif obj:IsA("MeshPart") then
            obj.TextureID = ""

        -- PARTICLES AND EFFECTS
        elseif obj:IsA("ParticleEmitter")
        or obj:IsA("Trail")
        or obj:IsA("Beam")
        or obj:IsA("Fire")
        or obj:IsA("Smoke")
        or obj:IsA("Sparkles") then
            obj.Enabled = false

        -- LIGHTS
        elseif obj:IsA("PointLight")
        or obj:IsA("SpotLight")
        or obj:IsA("SurfaceLight") then
            obj.Enabled = false

        -- POST PROCESSING
        elseif obj:IsA("PostEffect") then
            obj.Enabled = false

        elseif obj:IsA("Atmosphere") then
            obj.Density = 0
            obj.Haze = 0
            obj.Glare = 0

        elseif obj:IsA("Clouds") then
            obj.Enabled = false
        end

    end)
end

-- EXTREME LIGHTING
pcall(function()
    Lighting.GlobalShadows = false
    Lighting.ShadowSoftness = 0
    Lighting.EnvironmentDiffuseScale = 0
    Lighting.EnvironmentSpecularScale = 0
    Lighting.Brightness = 1
    Lighting.FogEnd = 100000
end)

-- TERRAIN
pcall(function()
    local terrain = Workspace.Terrain

    terrain.Decoration = false
    terrain.WaterWaveSize = 0
    terrain.WaterWaveSpeed = 0
    terrain.WaterReflectance = 0
end)

-- OPTIMIZE EVERYTHING
for _, obj in ipairs(Workspace:GetDescendants()) do
    optimize(obj)
end

for _, obj in ipairs(Lighting:GetDescendants()) do
    optimize(obj)
end

-- OPTIMIZE NEW OBJECTS
Workspace.DescendantAdded:Connect(function(obj)
    task.defer(optimize, obj)
end)

Lighting.DescendantAdded:Connect(function(obj)
    task.defer(optimize, obj)
end)

print("JK ULTRA POTATO GRAPHICS ACTIVATED")
