# tli-spawnselector

# Manual Installation
This is the installation guide

Go To [qb-apartments/client/main.lua] Then Go To The Event `apartments:client:setupSpawnUI` And Replace It With This:
```
RegisterNetEvent('apartments:client:setupSpawnUI', function(cData)
    QBCore.Functions.TriggerCallback('apartments:GetOwnedApartment', function(result)
        if result then
            TriggerEvent('qb-spawn:client:setupSpawns', cData, false, nil)
            TriggerEvent("apartments:client:SetHomeBlip", result.type)
        else
            if Apartments.Starting then
                TriggerEvent('qb-spawn:client:setupSpawns', cData, true, Apartments.Locations)
                TriggerEvent('qb-spawn:client:openUI', true)
            else
                TriggerEvent('qb-spawn:client:setupSpawns', cData, false, nil)
                TriggerEvent('qb-spawn:client:openUI', true)
            end
        end
    end, cData.citizenid)
end)
```

Then Go To [qb-spawn/client.lua] Then Go To The Event `qb-spawn:client:setupSpawns` And Replace It With This:

```
RegisterNetEvent('qb-spawn:client:setupSpawns', function(cData, new, apps)
    if not new then
         TriggerEvent('tli-spawnselector:set')
    elseif new then
        SendNUIMessage({
            action = "setupAppartements",
            locations = apps,
        })
    end
end)
```

If You Want The Locations To Not Be By Jobs Go To `fs-spawnselector/settings.lua` And Comment -- On The Jobs
