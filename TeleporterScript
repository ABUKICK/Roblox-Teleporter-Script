
-- SERVICES
local Workspace = game:GetService("Workspace")
local Players = game:GetService("Players")
local Debris = game:GetService("Debris")

-- TELEPORTER FINDEN
local tp1 = Workspace:WaitForChild("teleporter1")
local tp2 = Workspace:WaitForChild("teleporter2")

-- EINSTELLUNGEN
local COOLDOWN = 1
local HOEHE = 5

-- COOLDOWN PRO SPIELER
local cooldown = {}

-- SPIELER ERKENNEN
local function findeSpieler(part)
    local charakter = part:FindFirstAncestorOfClass("Model")

    if not charakter then
        return nil
    end

    return Players:GetPlayerFromCharacter(charakter)
end

-- PARTIKEL UND LEUCHTEFFEKT
local function erzeugeEffekte(charakter)
    local wurzel = charakter:FindFirstChild("HumanoidRootPart")

    if not wurzel then
        return
    end

    -- Blauer Leuchteffekt
    local highlight = Instance.new("Highlight")
    highlight.FillColor = Color3.fromRGB(0, 170, 255)
    highlight.OutlineColor = Color3.fromRGB(255, 255, 255)
    highlight.FillTransparency = 0.35
    highlight.Parent = charakter

    Debris:AddItem(highlight, 0.5)

    -- Partikel erzeugen
    local attachment = Instance.new("Attachment")
    attachment.Parent = wurzel

    local emitter = Instance.new("ParticleEmitter")
    emitter.Texture = "rbxasset://textures/particles/sparkles_main.dds"
    emitter.Color = ColorSequence.new(
        Color3.fromRGB(0, 170, 255),
        Color3.fromRGB(255, 255, 255)
    )
    emitter.Lifetime = NumberRange.new(0.3, 0.7)
    emitter.Speed = NumberRange.new(4, 8)
    emitter.SpreadAngle = Vector2.new(180, 180)
    emitter.Rate = 0
    emitter.Parent = attachment

    emitter:Emit(25)

    Debris:AddItem(attachment, 1)
end

-- SPIELER TELEPORTIEREN
local function teleportiereSpieler(beruehrtesPart, zielPart)
    local spieler = findeSpieler(beruehrtesPart)

    if not spieler then
        return
    end

    if cooldown[spieler.UserId] then
        return
    end

    local charakter = spieler.Character

    if not charakter then
        return
    end

    local humanoid = charakter:FindFirstChildOfClass("Humanoid")
    local wurzel = charakter:FindFirstChild("HumanoidRootPart")

    if not humanoid or not wurzel or humanoid.Health <= 0 then
        return
    end

    -- Cooldown aktivieren
    cooldown[spieler.UserId] = true

    -- Effekte erzeugen
    erzeugeEffekte(charakter)

    -- Zum Ziel teleportieren
    charakter:PivotTo(
        zielPart.CFrame + Vector3.new(0, HOEHE, 0)
    )

    -- Cooldown nach einer Sekunde aufheben
    task.delay(COOLDOWN, function()
        cooldown[spieler.UserId] = nil
    end)
end

-- TELEPORTER VERBINDEN
tp1.Touched:Connect(function(part)
    teleportiereSpieler(part, tp2)
end)

tp2.Touched:Connect(function(part)
    teleportiereSpieler(part, tp1)
end)

-- SPIELER BEIM VERLASSEN AUFRÄUMEN
Players.PlayerRemoving:Connect(function(spieler)
    cooldown[spieler.UserId] = nil
end)
