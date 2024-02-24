---
title: "Klima Code"
date: 2024-02-24T21:07:37+03:00
type: "post"
tags: ["test"]
---

```luau
local Hitbox = Instance.new("Part")
    game:GetService("Debris"):AddItem(Hitbox,OffTime)
    Hitbox.Parent = workspace
    Hitbox.Transparency = 0.7
    Hitbox.CanCollide = false
    Hitbox.Anchored = true
    return Hitbox
end

module.Hit = function(Hitbox, HitType, Char)

    if HitType == "Classic" then

        local hits = workspace:GetPartsInPart(Hitbox)
        local hitCharacters = {}  -- Tüm karakterleri saklamak için bir tablo oluştur

        for i, v in pairs(hits) do
            if v.Parent and v.Parent:FindFirstChild("Humanoid") and v.Parent ~= Char and v.Name == "HumanoidRootPart" then
                table.insert(hitCharacters, v.Parent)  -- Her karakteri tabloya ekle
            end
        end

        return hitCharacters

    elseif HitType == "HitOnce" then
        local foundplayer = false

        while Hitbox.Parent and foundplayer == false do
            local oParams = OverlapParams.new()

            oParams.FilterType = Enum.RaycastFilterType.Exclude
            oParams.FilterDescendantsInstances = {Char}

            local hits = workspace:GetPartsInPart(Hitbox, oParams)
            print("aranıyor")

            for i, v in pairs(hits) do
                if v.Parent and v.Parent:FindFirstChild("Humanoid") and v.Name == "HumanoidRootPart" then

                    local Hedef = v.Parent

                    foundplayer = true
                    return Hedef
                end
            end







            if foundplayer == true or not Hitbox then
                print("bitti")
                break

            else
                task.wait(.02)
            end

        end
    end
end
```
