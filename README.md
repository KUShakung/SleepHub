getgenv().Setting = {
    ["Join Team"] = "Pirate", -- "Pirate","Marine"
    ["Auto Farm Level"] = false,

    -- Setting etc
    ["Select Weapon"] = "",
    ["Auto Rejoin"] = false,

    -- Old World
    ["Auto New World"] = false,

    -- New World
    ["Auto Factory"] = false,
    ["Auto third World"] = false,

    -- New Fighting Styles & etc
    ["Auto Superhuman"] = false,
    ["Auto Superhuman [Full]"] = false,
    ["Auto Death Step"] = false,
    ["Auto Dragon Talon"] = false,
    ["Auto Electric Clow"] = false,
    ["Auto Buy Legendary Sword"] = false,
    ["Auto Buy Legendary Sword Hop"] = false,
    ["Auto Buy Enhancement"] = false,
    ["Auto Farm Select Boss Hop"] = false,

    -- Auto Stats
    ["Melee"] = false,
    ["Defense"] = false,
    ["Sword"] = false,
    ["Gun"] = false,
    ["Demon Fruit"] = false,

    -- Use Candy
    ["Auto Buy Exp x2"] = false,
    ["Auto Buy Exp x2[ Exp Expire ]"] = false,

    -- Players
    ["Bounty Hop"] = false
}
end

local placeId = game.PlaceId
if placeId == 2753915549 then
    OldWorld = true
elseif placeId == 4442272183 then
    NewWorld = true
elseif placeId == 7449423635 then
    ThreeWorld = true
end
StatsBypass = "NoBypassTP"

function HopServer()
    local PlaceID = game.PlaceId
    local AllIDs = {}
    local foundAnything = ""
    local actualHour = os.date("!*t").hour
    local Deleted = false
     --[[
     local File = pcall(function()
        AllIDs = game:GetService('HttpService'):JSONDecode(readfile("NotSameServers.json"))
     end)
     if not File then
        table.insert(AllIDs, actualHour)
        writefile("NotSameServers.json", game:GetService('HttpService'):JSONEncode(AllIDs))
     end
     ]]
    function TPReturner()
        local Site;
        if foundAnything == "" then
            Site = game.HttpService:JSONDecode(game:HttpGet('https://games.roblox.com/v1/games/' .. PlaceID .. '/servers/Public?sortOrder=Asc&limit=100'))
        else
            Site = game.HttpService:JSONDecode(game:HttpGet('https://games.roblox.com/v1/games/' .. PlaceID .. '/servers/Public?sortOrder=Asc&limit=100&cursor=' .. foundAnything))
        end
        local ID = ""
        if Site.nextPageCursor and Site.nextPageCursor ~= "null" and Site.nextPageCursor ~= nil then
            foundAnything = Site.nextPageCursor
        end
        local num = 0;
        for i,v in pairs(Site.data) do
            local Possible = true
            ID = tostring(v.id)
            if tonumber(v.maxPlayers) > tonumber(v.playing) then
                for _,Existing in pairs(AllIDs) do
                    if num ~= 0 then
                        if ID == tostring(Existing) then
                            Possible = false
                        end
                    else
                        if tonumber(actualHour) ~= tonumber(Existing) then
                            local delFile = pcall(function()
                                -- delfile("NotSameServers.json")
                                AllIDs = {}
                                table.insert(AllIDs, actualHour)
                            end)
                        end
                    end
                    num = num + 1
                end
                if Possible == true then
                    table.insert(AllIDs, ID)
                    wait()
                    pcall(function()
                        -- writefile("NotSameServers.json", game:GetService('HttpService'):JSONEncode(AllIDs))
                        wait()
                        game:GetService("TeleportService"):TeleportToPlaceInstance(PlaceID, ID, game.Players.LocalPlayer)
                    end)
                    wait(4)
                end
            end
        end
    end

    function Teleport()
        while wait() do
            pcall(function()
                TPReturner()
                if foundAnything ~= "" then
                    TPReturner()
                end
            end)
        end
    end

    Teleport()
    wait(1)
end

local Nonquest = false
function CheckQuest()
    local MyLevel = game.Players.LocalPlayer.Data.Level.Value
    if FastTween then
        if OldWorld then
            if MyLevel == 1 or MyLevel <= 9 then -- Bandit
                Nonquest = false
                Ms = "Bandit [Lv. 5]"
                NameQuest = "BanditQuest1"
                LevelQuest = 1
                NameMon = "Bandit"
                CFrameQuest = CFrame.new(1059.37195, 15.4495068, 1550.4231, 0.939700544, -0, -0.341998369, 0, 1, -0, 0.341998369, 0, 0.939700544)
                CFrameMon = CFrame.new(1353.44885, 3.40935516, 1376.92029, 0.776053488, -6.97791975e-08, 0.630666852, 6.99138596e-08, 1, 2.4612488e-08, -0.630666852, 2.49917598e-08, 0.776053488)
            elseif MyLevel == 10 or MyLevel <= 14 then -- Monkey
                Nonquest = false
                Ms = "Monkey [Lv. 14]"
                NameQuest = "JungleQuest"
                LevelQuest = 1
                NameMon = "Monkey"
                CFrameQuest = CFrame.new(-1598.08911, 35.5501175, 153.377838, 0, 0, 1, 0, 1, -0, -1, 0, 0)
                CFrameMon = CFrame.new(-1402.74609, 98.5633316, 90.6417007, 0.836947978, 0, 0.547282517, -0, 1, -0, -0.547282517, 0, 0.836947978)
            elseif MyLevel == 15 or MyLevel <= 29 then -- Gorilla
                Nonquest = false
                Ms = "Gorilla [Lv. 20]"
                NameQuest = "JungleQuest"
                LevelQuest = 2
                NameMon = "Gorilla"
                CFrameQuest = CFrame.new(-1598.08911, 35.5501175, 153.377838, 0, 0, 1, 0, 1, -0, -1, 0, 0)
                CFrameMon = CFrame.new(-1267.89001, 66.2034225, -531.818115, -0.813996196, -5.25169774e-08, -0.580869019, -5.58769671e-08, 1, -1.21082593e-08, 0.580869019, 2.26011476e-08, -0.813996196)
            elseif MyLevel == 30 or MyLevel <= 89 then -- Galley Captain
                Nonquest = true
                Ms = "Galley Captain [Lv. 650]"
                NameQuest = "FountainQuest"
                LevelQuest = 2
                NameMon = "Galley Captain"
                CFrameQuest = CFrame.new(5259.81982, 37.3500175, 4050.0293, 0.087131381, 0, 0.996196866, 0, 1, 0, -0.996196866, 0, 0.087131381)
                CFrameMon = CFrame.new(5782.90186, 94.5326462, 4716.78174, 0.361808896, -1.24757526e-06, -0.932252586, 2.16989656e-06, 1, -4.96097414e-07, 0.932252586, -1.84339774e-06, 0.361808896)
            elseif MyLevel == 90 or MyLevel <= 99 then -- Snow Bandits
                Nonquest = false
                Ms = "Snow Bandit [Lv. 90]"
                NameQuest = "SnowQuest"
                LevelQuest = 1
                NameMon = "Snow Bandits"
                CFrameQuest = CFrame.new(1389.74451, 86.6520844, -1298.90796, -0.342042685, 0, 0.939684391, 0, 1, 0, -0.939684391, 0, -0.342042685)
                CFrameMon = CFrame.new(1412.92346, 55.3503647, -1260.62036, -0.246266365, -0.0169920288, -0.969053388, 0.000432241941, 0.999844253, -0.0176417865, 0.969202161, -0.00476344163, -0.246220857)
            elseif MyLevel == 100 or MyLevel <= 119 then -- Snowman
                Nonquest = false
                Ms = "Snowman [Lv. 100]"
                NameQuest = "SnowQuest"
                LevelQuest = 2
                NameMon = "Snowman"
                CFrameQuest = CFrame.new(1389.74451, 86.6520844, -1298.90796, -0.342042685, 0, 0.939684391, 0, 1, 0, -0.939684391, 0, -0.342042685)
                CFrameMon = CFrame.new(1376.86401, 97.2779999, -1396.93115, -0.986755967, 7.71178321e-08, -0.162211925, 7.71531674e-08, 1, 6.08143536e-09, 0.162211925, -6.51427134e-09, -0.986755967)
            elseif MyLevel == 120 or MyLevel <= 149 then -- Chief Petty Officer
                Nonquest = false
                Ms = "Chief Petty Officer [Lv. 120]"
                NameQuest = "MarineQuest2"
                LevelQuest = 1
                NameMon = "Chief Petty Officer"
                CFrameQuest = CFrame.new(-5039.58643, 27.3500385, 4324.68018, 0, 0, -1, 0, 1, 0, 1, 0, 0)
                CFrameMon = CFrame.new(-4882.8623, 22.6520386, 4255.53516, 0.273695946, -5.40380647e-08, -0.96181643, 4.37720793e-08, 1, -4.37274998e-08, 0.96181643, -3.01326679e-08, 0.273695946)
            elseif MyLevel == 150 or MyLevel <= 174 then -- Sky Bandit
                Nonquest = false
                Ms = "Sky Bandit [Lv. 150]"
                NameQuest = "SkyQuest"
                LevelQuest = 1
                NameMon = "Sky Bandit"
                CFrameQuest = CFrame.new(-4839.53027, 716.368591, -2619.44165, 0.866007268, 0, 0.500031412, 0, 1, 0, -0.500031412, 0, 0.866007268)
                CFrameMon = CFrame.new(-4959.51367, 365.39267, -2974.56812, 0.964867651, 7.74418396e-08, 0.262737453, -6.95931988e-08, 1, -3.91783708e-08, -0.262737453, 1.95171506e-08, 0.964867651)
            elseif MyLevel == 175 or MyLevel <= 189 then -- Dark Master
                Nonquest = false
                Ms = "Dark Master [Lv. 175]"
                NameQuest = "SkyQuest"
                LevelQuest = 2
                NameMon = "Dark Master"
                CFrameQuest = CFrame.new(-4839.53027, 716.368591, -2619.44165, 0.866007268, 0, 0.500031412, 0, 1, 0, -0.500031412, 0, 0.866007268)
                CFrameMon = CFrame.new(-5079.98096, 376.477356, -2194.17139, 0.465965867, -3.69776352e-08, 0.884802461, 3.40249851e-09, 1, 4.00000886e-08, -0.884802461, -1.56281423e-08, 0.465965867)
            elseif MyLevel == 190 or MyLevel <= 209 then
                Nonquest = false
                Ms = "Prisoner [Lv. 190]"
                LevelQuest = 1
                NameQuest = "PrisonerQuest"
                NameMon = "Prisoner"
                CFrameQuest = CFrame.new(5308.93115, 1.65517521, 475.120514, -0.0894274712, -5.00292918e-09, -0.995993316, 1.60817859e-09, 1, -5.16744869e-09, 0.995993316, -2.06384709e-09, -0.0894274712)
                CFrameMon = CFrame.new(5433.39307, 88.678093, 514.986877, 0.879988372, 0, -0.474995494, 0, 1, 0, 0.474995494, 0, 0.879988372)
            elseif MyLevel == 210 or MyLevel <= 249 then
                Nonquest = false
                Ms = "Dangerous Prisoner [Lv. 210]"
                LevelQuest = 2
                NameQuest = "PrisonerQuest"
                NameMon = "Dangerous Prisoner"
                CFrameQuest = CFrame.new(5308.93115, 1.65517521, 475.120514, -0.0894274712, -5.00292918e-09, -0.995993316, 1.60817859e-09, 1, -5.16744869e-09, 0.995993316, -2.06384709e-09, -0.0894274712)
                CFrameMon = CFrame.new(5433.39307, 88.678093, 514.986877, 0.879988372, 0, -0.474995494, 0, 1, 0, 0.474995494, 0, 0.879988372)
            elseif MyLevel == 250 or MyLevel <= 274 then -- Toga Warrior
                Nonquest = false
                Ms = "Toga Warrior [Lv. 250]"
                NameQuest = "ColosseumQuest"
                LevelQuest = 1
                NameMon = "Toga Warrior"
                CFrameQuest = CFrame.new(-1576.11743, 7.38933945, -2983.30762, 0.576966345, 1.22114863e-09, 0.816767931, -3.58496594e-10, 1, -1.24185606e-09, -0.816767931, 4.2370063e-10, 0.576966345)
                CFrameMon = CFrame.new(-1779.97583, 44.6077499, -2736.35474, 0.984437346, 4.10396339e-08, 0.175734788, -3.62286876e-08, 1, -3.05844168e-08, -0.175734788, 2.3741821e-08, 0.984437346)
            elseif MyLevel == 275 or MyLevel <= 299 then -- Gladiato
                Nonquest = false
                Ms = "Gladiator [Lv. 275]"
                NameQuest = "ColosseumQuest"
                LevelQuest = 2
                NameMon = "Gladiato"
                CFrameQuest = CFrame.new(-1576.11743, 7.38933945, -2983.30762, 0.576966345, 1.22114863e-09, 0.816767931, -3.58496594e-10, 1, -1.24185606e-09, -0.816767931, 4.2370063e-10, 0.576966345)
                CFrameMon = CFrame.new(-1274.75903, 58.1895943, -3188.16309, 0.464524001, 6.21005611e-08, 0.885560572, -4.80449414e-09, 1, -6.76054768e-08, -0.885560572, 2.71497012e-08, 0.464524001)
            elseif MyLevel == 300 or MyLevel <= 329 then -- Military Soldier
                Nonquest = false
                Ms = "Military Soldier [Lv. 300]"
                NameQuest = "MagmaQuest"
                LevelQuest = 1
                NameMon = "Military Soldier"
                CFrameQuest = CFrame.new(-5316.55859, 12.2370615, 8517.2998, 0.588437557, -1.37880001e-08, -0.808542669, -2.10116209e-08, 1, -3.23446478e-08, 0.808542669, 3.60215964e-08, 0.588437557)
                CFrameMon = CFrame.new(-5363.01123, 41.5056877, 8548.47266, -0.578253984, -3.29503091e-10, 0.815856814, 9.11209668e-08, 1, 6.498761e-08, -0.815856814, 1.11920997e-07, -0.578253984)
            elseif MyLevel == 330 or MyLevel <= 374 then -- Military Spy
                Nonquest = false
                Ms = "Military Spy [Lv. 325]"
                NameQuest = "MagmaQuest"
                LevelQuest = 2
                NameMon = "Military Spy"
                CFrameQuest = CFrame.new(-5316.55859, 12.2370615, 8517.2998, 0.588437557, -1.37880001e-08, -0.808542669, -2.10116209e-08, 1, -3.23446478e-08, 0.808542669, 3.60215964e-08, 0.588437557)
                CFrameMon = CFrame.new(-5787.99023, 120.864456, 8762.25293, -0.188358366, -1.84706277e-08, 0.982100308, -1.23782129e-07, 1, -4.93306951e-09, -0.982100308, -1.22495649e-07, -0.188358366)
            elseif MyLevel == 375 or MyLevel <= 399 then -- Fishman Warrior
                Nonquest = false
                Ms = "Fishman Warrior [Lv. 375]"
                NameQuest = "FishmanQuest"
                LevelQuest = 1
                NameMon = "Fishman Warrior"
                CFrameQuest = CFrame.new(61122.5625, 18.4716396, 1568.16504, 0.893533468, 3.95251609e-09, 0.448996574, -2.34327455e-08, 1, 3.78297464e-08, -0.448996574, -4.43233645e-08, 0.893533468)
                CFrameMon = CFrame.new(60946.6094, 48.6735229, 1525.91687, -0.0817126185, 8.90751153e-08, 0.996655822, 2.00889794e-08, 1, -8.77269599e-08, -0.996655822, 1.28533992e-08, -0.0817126185)
            elseif MyLevel == 400 or MyLevel <= 449 then -- Fishman Commando
                Nonquest = false
                Ms = "Fishman Commando [Lv. 400]"
                NameQuest = "FishmanQuest"
                LevelQuest = 2
                NameMon = "Fishman Commando"
                CFrameQuest = CFrame.new(61122.5625, 18.4716396, 1568.16504)
                CFrameMon = CFrame.new(60946.6094, 48.6735229, 1525.916871)
            elseif MyLevel == 450 or MyLevel <= 474 then 
                Nonquest = false
                Ms = "God's Guard [Lv. 450]"
                NameQuest = "SkyExp1Quest"
                LevelQuest = 1
                NameMon = "God's Guards"
                CFrameQuest = CFrame.new(-4721.71436, 845.277161, -1954.20105)
                CFrameMon = CFrame.new(-4716.95703, 853.089722, -1933.925427)
            elseif MyLevel == 475 or MyLevel <= 524 then 
                Nonquest = false
                Ms = "Shanda [Lv. 475]"
                NameQuest = "SkyExp1Quest"
                LevelQuest = 2
                NameMon = "Shandas"
                CFrameQuest = CFrame.new(-7859.09814, 5544.19043, -381.476196, -0.422592998, 0, 0.906319618, 0, 1, 0, -0.906319618, 0, -0.422592998)
                CFrameMon = CFrame.new(-7904.57373, 5584.37646, -459.62973, 0.65171206, 5.11171692e-08, 0.758466363, -4.76232476e-09, 1, -6.33034247e-08, -0.758466363, 3.76435416e-08, 0.65171206)
            elseif MyLevel == 525 or MyLevel <= 549 then -- Royal Squad
                Nonquest = false
                Ms = "Royal Squad [Lv. 525]"
                NameQuest = "SkyExp2Quest"
                LevelQuest = 1
                NameMon = "Royal Squad"
                CFrameQuest = CFrame.new(-7906.81592, 5634.6626, -1411.99194, 0, 0, -1, 0, 1, 0, 1, 0, 0)
                CFrameMon = CFrame.new(-7555.04199, 5606.90479, -1303.24744, -0.896107852, -9.6057462e-10, -0.443836004, -4.24974544e-09, 1, 6.41599973e-09, 0.443836004, 7.63560326e-09, -0.896107852)
            elseif MyLevel == 550 or MyLevel <= 624 then -- Royal Soldier
                Nonquest = false
                Ms = "Royal Soldier [Lv. 550]"
                NameQuest = "SkyExp2Quest"
                LevelQuest = 2
                NameMon = "Royal Soldier"
                CFrameQuest = CFrame.new(-7906.81592, 5634.6626, -1411.99194, 0, 0, -1, 0, 1, 0, 1, 0, 0)
                CFrameMon = CFrame.new(-7837.31152, 5649.65186, -1791.08582, -0.716008604, 0.0104285581, -0.698013008, 5.02521061e-06, 0.99988848, 0.0149335321, 0.69809103, 0.0106890313, -0.715928733)
            elseif MyLevel == 625 or MyLevel <= 649 then -- Galley Pirate
                Nonquest = false
                Ms = "Galley Pirate [Lv. 625]"
                NameQuest = "FountainQuest"
                LevelQuest = 1
                NameMon = "Galley Pirate"
                CFrameQuest = CFrame.new(5259.81982, 37.3500175, 4050.0293, 0.087131381, 0, 0.996196866, 0, 1, 0, -0.996196866, 0, 0.087131381)
                CFrameMon = CFrame.new(5569.80518, 38.5269432, 3849.01196, 0.896460414, 3.98027495e-08, 0.443124533, -1.34262139e-08, 1, -6.26611296e-08, -0.443124533, 5.02237434e-08, 0.896460414)
            elseif MyLevel >= 650 then -- Galley Captain
                Nonquest = false
                Ms = "Galley Captain [Lv. 650]"
                NameQuest = "FountainQuest"
                LevelQuest = 2
                NameMon = "Galley Captain"
                CFrameQuest = CFrame.new(5259.81982, 37.3500175, 4050.0293, 0.087131381, 0, 0.996196866, 0, 1, 0, -0.996196866, 0, 0.087131381)
                CFrameMon = CFrame.new(5782.90186, 94.5326462, 4716.78174, 0.361808896, -1.24757526e-06, -0.932252586, 2.16989656e-06, 1, -4.96097414e-07, 0.932252586, -1.84339774e-06, 0.361808896)
            end
        end
        if NewWorld then
            Nonquest = false
            if MyLevel == 700 or MyLevel <= 724 then -- Raider [Lv. 700]
                Ms = "Raider [Lv. 700]"
                NameQuest = "Area1Quest"
                LevelQuest = 1
                NameMon = "Raider"
                CFrameQuest = CFrame.new(-429.543518, 71.7699966, 1836.18188, -0.22495985, 0, -0.974368095, 0, 1, 0, 0.974368095, 0, -0.22495985)
                CFrameMon = CFrame.new(-737.026123, 10.1748352, 2392.57959, 0.272128761, 0, -0.962260842, -0, 1, -0, 0.962260842, 0, 0.272128761)
            elseif MyLevel == 725 or MyLevel <= 774 then -- Mercenary [Lv. 725]
                Ms = "Mercenary [Lv. 725]"
                NameQuest = "Area1Quest"
                LevelQuest = 2
                NameMon = "Mercenary"
                CFrameQuest = CFrame.new(-429.543518, 71.7699966, 1836.18188, -0.22495985, 0, -0.974368095, 0, 1, 0, 0.974368095, 0, -0.22495985)
                CFrameMon = CFrame.new(-1022.21271, 72.9855194, 1891.39148, -0.990782857, 0, -0.135460541, 0, 1, 0, 0.135460541, 0, -0.990782857)
            elseif MyLevel == 775 or MyLevel <= 799 then -- Swan Pirate [Lv. 775]
                Ms = "Swan Pirate [Lv. 775]"
                NameQuest = "Area2Quest"
                LevelQuest = 1
                NameMon = "Swan Pirate"
                CFrameQuest = CFrame.new(638.43811, 71.769989, 918.282898, 0.139203906, 0, 0.99026376, 0, 1, 0, -0.99026376, 0, 0.139203906)
                CFrameMon = CFrame.new(976.467651, 111.174057, 1229.1084, 0.00852567982, -4.73897828e-08, -0.999963999, 1.12251888e-08, 1, -4.7295778e-08, 0.999963999, -1.08215579e-08, 0.00852567982)
            elseif MyLevel == 800 or MyLevel <= 874 then -- Factory Staff [Lv. 800]
                Ms = "Factory Staff [Lv. 800]"
                NameQuest = "Area2Quest"
                LevelQuest = 2
                NameMon = "Factory Staff"
                CFrameQuest = CFrame.new(638.43811, 71.769989, 918.282898, 0.139203906, 0, 0.99026376, 0, 1, 0, -0.99026376, 0, 0.139203906)
                CFrameMon = CFrame.new(336.74585, 73.1620483, -224.129272, 0.993632793, 3.40154607e-08, 0.112668738, -3.87658332e-08, 1, 3.99718729e-08, -0.112668738, -4.40850592e-08, 0.993632793)
            elseif MyLevel == 875 or MyLevel <= 899 then -- Marine Lieutenant [Lv. 875]
                Ms = "Marine Lieutenant [Lv. 875]"
                NameQuest = "MarineQuest3"
                LevelQuest = 1
                NameMon = "Marine Lieutenant"
                CFrameQuest = CFrame.new(-2440.79639, 71.7140732, -3216.06812, 0.866007268, 0, 0.500031412, 0, 1, 0, -0.500031412, 0, 0.866007268)
                CFrameMon = CFrame.new(-2842.69922, 72.9919434, -2901.90479, -0.762281299, 0, -0.64724648, 0, 1.00000012, 0, 0.64724648, 0, -0.762281299)
            elseif MyLevel == 900 or MyLevel <= 949 then -- Marine Captain [Lv. 900]
                Ms = "Marine Captain [Lv. 900]"
                NameQuest = "MarineQuest3"
                LevelQuest = 2
                NameMon = "Marine Captain"
                CFrameQuest = CFrame.new(-2440.79639, 71.7140732, -3216.06812, 0.866007268, 0, 0.500031412, 0, 1, 0, -0.500031412, 0, 0.866007268)
                CFrameMon = CFrame.new(-1814.70313, 72.9919434, -3208.86621, -0.900422215, 7.93464423e-08, -0.435017526, 3.68856199e-08, 1, 1.06050372e-07, 0.435017526, 7.94441988e-08, -0.900422215)
            elseif MyLevel == 950 or MyLevel <= 974 then -- Zombie [Lv. 950]
                Ms = "Zombie [Lv. 950]"
                NameQuest = "ZombieQuest"
                LevelQuest = 1
                NameMon = "Zombie"
                CFrameQuest = CFrame.new(-5497.06152, 47.5923004, -795.237061, -0.29242146, 0, -0.95628953, 0, 1, 0, 0.95628953, 0, -0.29242146)
                CFrameMon = CFrame.new(-5649.23438, 126.0578, -737.773743, 0.355238914, -8.10359282e-08, 0.934775114, 1.65461245e-08, 1, 8.04023372e-08, -0.934775114, -1.3095117e-08, 0.355238914)
            elseif MyLevel == 975 or MyLevel <= 999 then -- Vampire [Lv. 975]
                Ms = "Vampire [Lv. 975]"
                NameQuest = "ZombieQuest"
                LevelQuest = 2
                NameMon = "Vampire"
                CFrameQuest = CFrame.new(-5497.06152, 47.5923004, -795.237061, -0.29242146, 0, -0.95628953, 0, 1, 0, 0.95628953, 0, -0.29242146)
                CFrameMon = CFrame.new(-6030.32031, 0.4377408, -1313.5564, -0.856965423, 3.9138893e-08, -0.515373945, -1.12178942e-08, 1, 9.45958547e-08, 0.515373945, 8.68467822e-08, -0.856965423)
            elseif MyLevel == 1000 or MyLevel <= 1049 then -- Snow Trooper [Lv. 1000] **
                Ms = "Snow Trooper [Lv. 1000]"
                NameQuest = "SnowMountainQuest"
                LevelQuest = 1
                NameMon = "Snow Trooper"
                CFrameQuest = CFrame.new(609.858826, 400.119904, -5372.25928, -0.374604106, 0, 0.92718488, 0, 1, 0, -0.92718488, 0, -0.374604106)
                CFrameMon = CFrame.new(621.003418, 391.361053, -5335.43604, 0.481644779, 0, 0.876366913, 0, 1, 0, -0.876366913, 0, 0.481644779)
            elseif MyLevel == 1050 or MyLevel <= 1099 then -- Winter Warrior [Lv. 1050]
                Ms = "Winter Warrior [Lv. 1050]"
                NameQuest = "SnowMountainQuest"
                LevelQuest = 2
                NameMon = "Winter Warrior"
                CFrameQuest = CFrame.new(609.858826, 400.119904, -5372.25928, -0.374604106, 0, 0.92718488, 0, 1, 0, -0.92718488, 0, -0.374604106)
                CFrameMon = CFrame.new(1295.62683, 429.447784, -5087.04492, -0.698032081, -8.28980049e-08, -0.71606636, -1.98835952e-08, 1, -9.63858184e-08, 0.71606636, -5.30424877e-08, -0.698032081)
            elseif MyLevel == 1100 or MyLevel <= 1124 then -- Lab Subordinate [Lv. 1100]
                Ms = "Lab Subordinate [Lv. 1100]"
                NameQuest = "IceSideQuest"
                LevelQuest = 1
                NameMon = "Lab Subordinate"
                CFrameQuest = CFrame.new(-6064.06885, 15.2422857, -4902.97852, 0.453972578, -0, -0.891015649, 0, 1, -0, 0.891015649, 0, 0.453972578)
                CFrameMon = CFrame.new(-5769.2041, 37.9288292, -4468.38721, -0.569419742, -2.49055017e-08, 0.822046936, -6.96206541e-08, 1, -1.79282633e-08, -0.822046936, -6.74401548e-08, -0.569419742)
            elseif MyLevel == 1125 or MyLevel <= 1174 then -- Horned Warrior [Lv. 1125]
                Ms = "Horned Warrior [Lv. 1125]"
                NameQuest = "IceSideQuest"
                LevelQuest = 2
                NameMon = "Horned Warrior"
                CFrameQuest = CFrame.new(-6064.06885, 15.2422857, -4902.97852, 0.453972578, -0, -0.891015649, 0, 1, -0, 0.891015649, 0, 0.453972578)
                CFrameMon = CFrame.new(-6401.27979, 15.9775667, -5948.24316, 0.388303697, 0, -0.921531856, 0, 1, 0, 0.921531856, 0, 0.388303697)
            elseif MyLevel == 1175 or MyLevel <= 1199 then -- Magma Ninja [Lv. 1175]
                Ms = "Magma Ninja [Lv. 1175]"
                NameQuest = "FireSideQuest"
                LevelQuest = 1
                NameMon = "Magma Ninja"
                CFrameQuest = CFrame.new(-5428.03174, 15.0622921, -5299.43457, -0.882952213, 0, 0.469463557, 0, 1, 0, -0.469463557, 0, -0.882952213)
                CFrameMon = CFrame.new(-5466.06445, 57.6952019, -5837.42822, -0.988835871, 0, -0.149006829, 0, 1, 0, 0.149006829, 0, -0.988835871)
            elseif MyLevel == 1200 or MyLevel <= 1249 then 
                Ms = "Lava Pirate [Lv. 1200]"
                NameQuest = "FireSideQuest"
                LevelQuest = 2
                NameMon = "Lava Pirate"
                CFrameQuest = CFrame.new(-5431.09473, 15.9868021, -5296.53223, 0.831796765, 1.15322464e-07, -0.555080295, -1.10814341e-07, 1, 4.17010995e-08, 0.555080295, 2.68240168e-08, 0.831796765)
                CFrameMon = CFrame.new(-5169.71729, 34.1234779, -4669.73633, -0.196780294, 0, 0.98044765, 0, 1.00000012, -0, -0.98044765, 0, -0.196780294)
            elseif MyLevel == 1250 or MyLevel <= 1274 then 
                Ms = "Ship Deckhand [Lv. 1250]"
                NameQuest = "ShipQuest1"
                LevelQuest = 1
                NameMon = "Ship Deckhand"
                CFrameQuest = CFrame.new(1037.80127, 125.092171, 32911.6016, -0.244533166, -0, -0.969640911, -0, 1.00000012, -0, 0.96964103, 0, -0.244533136)
                CFrameMon = CFrame.new(1163.80872, 138.288452, 33058.4258, -0.998580813, 5.49076979e-08, -0.0532564968, 5.57436763e-08, 1, -1.42118655e-08, 0.0532564968, -1.71604082e-08, -0.998580813)
            elseif MyLevel == 1275 or MyLevel <= 1299 then 
                Ms = "Ship Engineer [Lv. 1275]"
                NameQuest = "ShipQuest1"
                LevelQuest = 2
                NameMon = "Ship Engineer"
                CFrameQuest = CFrame.new(1037.80127, 125.092171, 32911.6016, -0.244533166, -0, -0.969640911, -0, 1.00000012, -0, 0.96964103, 0, -0.244533136)
                CFrameMon = CFrame.new(921.30249023438, 125.400390625, 32937.34375)
            elseif MyLevel == 1300 or MyLevel <= 1324 then 
                Ms = "Ship Steward [Lv. 1300]"
                NameQuest = "ShipQuest2"
                LevelQuest = 1
                NameMon = "Ship Steward"
                CFrameQuest = CFrame.new(968.80957, 125.092171, 33244.125, -0.869560242, 1.51905191e-08, -0.493826836, 1.44108379e-08, 1, 5.38534195e-09, 0.493826836, -2.43357912e-09, -0.869560242)
                CFrameMon = CFrame.new(917.96057128906, 136.89932250977, 33343.4140625)
            elseif MyLevel == 1325 or MyLevel <= 1349 then 
                Ms = "Ship Officer [Lv. 1325]"
                NameQuest = "ShipQuest2"
                LevelQuest = 2
                NameMon = "Ship Officer"
                CFrameQuest = CFrame.new(968.80957, 125.092171, 33244.125, -0.869560242, 1.51905191e-08, -0.493826836, 1.44108379e-08, 1, 5.38534195e-09, 0.493826836, -2.43357912e-09, -0.869560242)
                CFrameMon = CFrame.new(944.44964599609, 181.40081787109, 33278.9453125)
            elseif MyLevel == 1350 or MyLevel <= 1374 then 
                Ms = "Arctic Warrior [Lv. 1350]"
                NameQuest = "FrostQuest"
                LevelQuest = 1
                NameMon = "Arctic Warrior"
                CFrameQuest = CFrame.new(5667.6582, 26.7997818, -6486.08984, -0.933587909, 0, -0.358349502, 0, 1, 0, 0.358349502, 0, -0.933587909)
                CFrameMon = CFrame.new(5878.23486, 81.3886948, -6136.35596, -0.451037169, 2.3908234e-07, 0.892505825, -1.08168464e-07, 1, -3.22542007e-07, -0.892505825, -2.4201924e-07, -0.451037169)
            elseif MyLevel == 1375 or MyLevel <= 1424 then -- Snow Lurker [Lv. 1375]
                Ms = "Snow Lurker [Lv. 1375]"
                NameQuest = "FrostQuest"
                LevelQuest = 2
                NameMon = "Snow Lurker"
                CFrameQuest = CFrame.new(5667.6582, 26.7997818, -6486.08984, -0.933587909, 0, -0.358349502, 0, 1, 0, 0.358349502, 0, -0.933587909)
                CFrameMon = CFrame.new(5513.36865, 60.546711, -6809.94971, -0.958693981, -1.65617333e-08, 0.284439981, -4.07668654e-09, 1, 4.44854642e-08, -0.284439981, 4.14883701e-08, -0.958693981)
            elseif MyLevel == 1425 or MyLevel <= 1449 then -- Sea Soldier [Lv. 1425]
                Ms = "Sea Soldier [Lv. 1425]"
                NameQuest = "ForgottenQuest"
                LevelQuest = 1
                NameMon = "Sea Soldier"
                CFrameQuest = CFrame.new(-3054.44458, 235.544281, -10142.8193, 0.990270376, -0, -0.13915664, 0, 1, -0, 0.13915664, 0, 0.990270376)
                CFrameMon = CFrame.new(-3115.78223, 63.8785706, -9808.38574, -0.913427353, 3.11199457e-08, 0.407000452, 7.79564235e-09, 1, -5.89660658e-08, -0.407000452, -5.06883708e-08, -0.913427353)
            elseif MyLevel >= 1450 then -- Water Fighter [Lv. 1450]
                Ms = "Water Fighter [Lv. 1450]"
                NameQuest = "ForgottenQuest"
                LevelQuest = 2
                NameMon = "Water Fighter"
                CFrameQuest = CFrame.new(-3054.44458, 235.544281, -10142.8193, 0.990270376, -0, -0.13915664, 0, 1, -0, 0.13915664, 0, 0.990270376)
                CFrameMon = CFrame.new(-3212.99683, 263.809296, -10551.8799, 0.742111444, -5.59139615e-08, -0.670276582, 1.69155214e-08, 1, -6.46908234e-08, 0.670276582, 3.66697037e-08, 0.742111444)
            end
        end
        if ThreeWorld then
            if MyLevel >= 1500 and MyLevel <= 1524 then -- Pirate Millionaire [Lv. 1500]
                Ms = "Pirate Millionaire [Lv. 1500]"
                NameQuest = "PiratePortQuest"
                LevelQuest = 1
                NameMon = "Pirate Millionaire"
                CFrameQuest = CFrame.new(-290.074677, 42.9034653, 5581.58984, 0.965929627, -0, -0.258804798, 0, 1, -0, 0.258804798, 0, 0.965929627)
                CFrameMon = CFrame.new(81.164993286133, 43.755737304688, 5724.7021484375)
            elseif MyLevel >= 1525 and MyLevel <= 1574 then -- Pistol Billionaire [Lv. 1525]
                Ms = "Pistol Billionaire [Lv. 1525]"
                NameQuest = "PiratePortQuest"
                LevelQuest = 2
                NameMon = "Pistol Billionaire"
                CFrameQuest = CFrame.new(-290.074677, 42.9034653, 5581.58984, 0.965929627, -0, -0.258804798, 0, 1, -0, 0.258804798, 0, 0.965929627)
                CFrameMon = CFrame.new(81.164993286133, 43.755737304688, 5724.7021484375)
            elseif MyLevel >= 1575 and MyLevel <= 1599 then -- Dragon Crew Warrior [Lv. 1575]
                Ms = "Dragon Crew Warrior [Lv. 1575]"
                NameQuest = "AmazonQuest"
                LevelQuest = 1
                NameMon = "Dragon Crew Warrior"
                CFrameQuest = CFrame.new(5832.83594, 51.6806107, -1101.51563, 0.898790359, -0, -0.438378751, 0, 1, -0, 0.438378751, 0, 0.898790359)
                CFrameMon = CFrame.new(6241.9951171875, 51.522083282471, -1243.9771728516)
            elseif MyLevel >= 1600 and MyLevel <= 1624 then -- Dragon Crew Archer [Lv. 1600]
                Ms = "Dragon Crew Archer [Lv. 1600]"
                NameQuest = "AmazonQuest"
                LevelQuest = 2
                NameMon = "Dragon Crew Archer"
                CFrameQuest = CFrame.new(5832.83594, 51.6806107, -1101.51563, 0.898790359, -0, -0.438378751, 0, 1, -0, 0.438378751, 0, 0.898790359)
                CFrameMon = CFrame.new(6488.9155273438, 383.38375854492, -110.66246032715)
            elseif MyLevel >= 1625 and MyLevel <= 1649 then -- Female Islander [Lv. 1625]
                Ms = "Female Islander [Lv. 1625]"
                NameQuest = "AmazonQuest2"
                LevelQuest = 1
                NameMon = "Female Islander"
                CFrameQuest = CFrame.new(5448.86133, 601.516174, 751.130676, 0, 0, 1, 0, 1, -0, -1, 0, 0)
                CFrameMon = CFrame.new(4770.4990234375, 758.95520019531, 1069.8680419922)
            elseif MyLevel >= 1650 and MyLevel <= 1699 then -- Giant Islander [Lv. 1650]
                Ms = "Giant Islander [Lv. 1650]"
                NameQuest = "AmazonQuest2"
                LevelQuest = 2
                NameMon = "Giant Islander"
                CFrameQuest = CFrame.new(5448.86133, 601.516174, 751.130676, 0, 0, 1, 0, 1, -0, -1, 0, 0)
                CFrameMon = CFrame.new(4530.3540039063, 656.75695800781, -131.60952758789)
            elseif MyLevel >= 1700 and MyLevel <= 1724 then -- Marine Commodore [Lv. 1700]
                Ms = "Marine Commodore [Lv. 1700]"
                NameQuest = "MarineTreeIsland"
                LevelQuest = 1
                NameMon = "Marine Commodore"
                CFrameQuest = CFrame.new(2180.54126, 27.8156815, -6741.5498, -0.965929747, 0, 0.258804798, 0, 1, 0, -0.258804798, 0, -0.965929747)
                CFrameMon = CFrame.new(2490.0844726563, 190.4232635498, -7160.0502929688)
            elseif MyLevel >= 1725 and MyLevel <= 1774 then -- Marine Rear Admiral [Lv. 1725]
                Ms = "Marine Rear Admiral [Lv. 1725]"
                NameQuest = "MarineTreeIsland"
                LevelQuest = 2
                NameMon = "Marine Rear Admiral"
                CFrameQuest = CFrame.new(2180.54126, 27.8156815, -6741.5498, -0.965929747, 0, 0.258804798, 0, 1, 0, -0.258804798, 0, -0.965929747)
                CFrameMon = CFrame.new(3951.3903808594, 229.11549377441, -6912.81640625)
            elseif MyLevel >= 1775 and MyLevel <= 1799 then -- Fishman Raider [Lv. 1775]
                Ms = "Fishman Raider [Lv. 1775]"
                NameQuest = "DeepForestIsland3"
                LevelQuest = 1
                NameMon = "Fishman Raider"
                CFrameQuest = CFrame.new(-10581.6563, 330.872955, -8761.18652, -0.882952213, 0, 0.469463557, 0, 1, 0, -0.469463557, 0, -0.882952213)
                CFrameMon = CFrame.new(-10322.400390625, 390.94473266602, -8580.0908203125)
            elseif MyLevel >= 1800 and MyLevel <= 1824 then -- Fishman Captain [Lv. 1800]
                Ms = "Fishman Captain [Lv. 1800]"
                NameQuest = "DeepForestIsland3"
                LevelQuest = 2
                NameMon = "Fishman Captain"
                CFrameQuest = CFrame.new(-10581.6563, 330.872955, -8761.18652, -0.882952213, 0, 0.469463557, 0, 1, 0, -0.469463557, 0, -0.882952213)
                CFrameMon = CFrame.new(-11194.541992188, 442.02795410156, -8608.806640625)
            elseif MyLevel >= 1825 and MyLevel <= 1849 then -- Forest Pirate [Lv. 1825]
                Ms = "Forest Pirate [Lv. 1825]"
                NameQuest = "DeepForestIsland"
                LevelQuest = 1
                NameMon = "Forest Pirate"
                CFrameQuest = CFrame.new(-13234.04, 331.488495, -7625.40137, 0.707134247, -0, -0.707079291, 0, 1, -0, 0.707079291, 0, 0.707134247)
                CFrameMon = CFrame.new(-13225.809570313, 428.19387817383, -7753.1245117188)
            elseif MyLevel >= 1850 and MyLevel <= 1899 then -- Mythological Pirate [Lv. 1850]
                Ms = "Mythological Pirate [Lv. 1850]"
                NameQuest = "DeepForestIsland"
                LevelQuest = 2
                NameMon = "Mythological Pirate"
                CFrameQuest = CFrame.new(-13234.04, 331.488495, -7625.40137, 0.707134247, -0, -0.707079291, 0, 1, -0, 0.707079291, 0, 0.707134247)
                CFrameMon = CFrame.new(-13869.172851563, 564.95251464844, -7084.4135742188)
            elseif MyLevel >= 1900 and MyLevel <= 1924 then -- Jungle Pirate [Lv. 1900]
                Ms = "Jungle Pirate [Lv. 1900]"
                NameQuest = "DeepForestIsland2"
                LevelQuest = 1
                NameMon = "Jungle Pirate"
                CFrameQuest = CFrame.new(-12680.3818, 389.971039, -9902.01953, -0.0871315002, 0, 0.996196866, 0, 1, 0, -0.996196866, 0, -0.0871315002)
                CFrameMon = CFrame.new(-11982.221679688, 376.32522583008, -10451.415039063)
            elseif MyLevel >= 1925 and MyLevel <= 1974 then -- Musketeer Pirate [Lv. 1925]
                Ms = "Musketeer Pirate [Lv. 1925]"
                NameQuest = "DeepForestIsland2"
                LevelQuest = 2
                NameMon = "Musketeer Pirate"
                CFrameQuest = CFrame.new(-12680.3818, 389.971039, -9902.01953, -0.0871315002, 0, 0.996196866, 0, 1, 0, -0.996196866, 0, -0.0871315002)
                CFrameMon = CFrame.new(-13282.3046875, 496.23684692383, -9565.150390625)
            elseif MyLevel >= 1975 and MyLevel <= 1999 then
                Ms = "Reborn Skeleton [Lv. 1975]"
                NameQuest = "HauntedQuest1"
                LevelQuest = 1
                NameMon = "Reborn Skeleton"
                CFrameQuest = CFrame.new(-9480.8271484375, 142.13066101074, 5566.0712890625)
                CFrameMon = CFrame.new(-8817.880859375, 191.16761779785, 6298.6557617188)
            elseif MyLevel >= 2000 and MyLevel <= 2024 then
                Ms = "Living Zombie [Lv. 2000]"
                NameQuest = "HauntedQuest1"
                LevelQuest = 2
                NameMon = "Living Zombie"
                CFrameQuest = CFrame.new(-9480.8271484375, 142.13066101074, 5566.0712890625)
                CFrameMon = CFrame.new(-10125.234375, 183.94705200195, 6242.013671875)
            elseif MyLevel >= 2025 and MyLevel <= 2049  then
                Ms = "Demonic Soul [Lv. 2025]"
                NameQuest = "HauntedQuest2"
                LevelQuest = 1
                NameMon = "Demonic Soul"
                CFrameQuest = CFrame.new(-9516.9931640625, 178.00651550293, 6078.4653320313)
                CFrameMon = CFrame.new(-9712.03125, 204.69589233398, 6193.322265625)
            elseif MyLevel >= 2050 and MyLevel <= 2074 then
                Ms = "Posessed Mummy [Lv. 2050]"
                NameQuest = "HauntedQuest2"
                LevelQuest = 2
                NameMon = "Posessed Mummy"
                CFrameQuest = CFrame.new(-9516.9931640625, 178.00651550293, 6078.4653320313)
                CFrameMon = CFrame.new(-9545.7763671875, 69.619895935059, 6339.5615234375)    
            elseif MyLevel >= 2075 and MyLevel <= 2099 then
                Ms = "Peanut Scout [Lv. 2075]"
                NameQuest = "NutsIslandQuest"
                LevelQuest = 1
                NameMon = "Peanut Scout"
                CFrameQuest = CFrame.new(-2104.17163, 38.1299706, -10194.418, 0.758814394, -1.38604395e-09, 0.651306927, 2.85280208e-08, 1, -3.1108879e-08, -0.651306927, 4.21863646e-08, 0.758814394)
                CFrameMon = CFrame.new(-2098.07544, 192.611862, -10248.8867, 0.983392298, -9.57031787e-08, 0.181492642, 8.7276355e-08, 1, 5.44169616e-08, -0.181492642, -3.76732068e-08, 0.983392298)
            elseif MyLevel >= 2100 and MyLevel <= 2124 then
                Ms = "Peanut President [Lv. 2100]"
                NameQuest = "NutsIslandQuest"
                LevelQuest = 2
                NameMon = "Peanut President"
                CFrameQuest = CFrame.new(-2104.17163, 38.1299706, -10194.418, 0.758814394, -1.38604395e-09, 0.651306927, 2.85280208e-08, 1, -3.1108879e-08, -0.651306927, 4.21863646e-08, 0.758814394)
                CFrameMon = CFrame.new(-1876.95959, 192.610947, -10542.2939, 0.0553516336, -2.83836812e-08, 0.998466909, -6.89634405e-10, 1, 2.84654931e-08, -0.998466909, -2.26418861e-09, 0.0553516336)
            elseif MyLevel >= 2125 and MyLevel <= 2149 then
                Ms = "Ice Cream Chef [Lv. 2125]"
                NameQuest = "IceCreamIslandQuest"
                LevelQuest = 1
                NameMon = "Ice Cream Chef"
                CFrameQuest = CFrame.new(-820.404358, 65.8453293, -10965.5654, 0.822534859, 5.24448502e-08, -0.568714678, -2.08336317e-08, 1, 6.20846663e-08, 0.568714678, -3.92184099e-08, 0.822534859)
                CFrameMon = CFrame.new(-821.614075, 208.39537, -10990.7617, -0.870096624, 3.18909272e-08, 0.492881238, -1.8357893e-08, 1, -9.71107568e-08, -0.492881238, -9.35439957e-08, -0.870096624)
            elseif MyLevel >= 2150 and MyLevel <= 2199 then 
                Ms = "Ice Cream Commander [Lv. 2150]"
                NameQuest = "IceCreamIslandQuest"
                LevelQuest = 2
                NameMon = "Ice Cream Commander"
                CFrameQuest = CFrame.new(-819.376526, 67.4634171, -10967.2832)
                CFrameMon = CFrame.new(-610.11669921875, 208.26904296875, -11253.686523438)
            elseif MyLevel >= 2200 and MyLevel <= 2224 then 
                Ms = "Cookie Crafter [Lv. 2200]"
                NameQuest = "CakeQuest1"
                LevelQuest = 1
                NameMon = "Cookie Crafter"
                CFrameQuest = CFrame.new(-2020.6068115234375, 37.82400894165039, -12027.80859375)
                CFrameMon = CFrame.new(-2286.684326171875, 146.5656280517578, -12226.8818359375)
            elseif MyLevel >= 2225 and MyLevel <= 2249 then 
                Ms = "Cake Guard [Lv. 2225]"
                NameQuest = "CakeQuest1"
                LevelQuest = 2
                NameMon = "Cake Guard"
                CFrameQuest = CFrame.new(-2020.6068115234375, 37.82400894165039, -12027.80859375)
                CFrameMon = CFrame.new(-1817.9747314453125, 209.5632781982422, -12288.9228515625)
            elseif MyLevel >= 2250 and MyLevel <= 2274 then 
                Ms = "Baking Staff [Lv. 2250]"
                NameQuest = "CakeQuest2"
                LevelQuest = 1
                NameMon = "Baking Staff"
                CFrameQuest = CFrame.new(-1928.31763, 37.7296638, -12840.626)
                CFrameMon = CFrame.new(-1818.347900390625, 93.41275787353516, -12887.66015625)
            elseif MyLevel >= 2275 then 
                Ms = "Head Baker [Lv. 2275]"
                NameQuest = "CakeQuest2"
                LevelQuest = 2
                NameMon = "Head Baker"
                CFrameQuest = CFrame.new(-1928.31763, 37.7296638, -12840.626)
                CFrameMon = CFrame.new(-2288.795166015625, 106.9419174194336, -12811.111328125)
            end
        end
    else
        if OldWorld then
            if MyLevel == 1 or MyLevel <= 9 then -- Bandit
                Nonquest = false
                Ms = "Bandit [Lv. 5]"
                NameQuest = "BanditQuest1"
                LevelQuest = 1
                NameMon = "Bandit"
                CFrameQuest = CFrame.new(1059.37195, 15.4495068, 1550.4231, 0.939700544, -0, -0.341998369, 0, 1, -0, 0.341998369, 0, 0.939700544)
                CFrameMon = CFrame.new(1353.44885, 3.40935516, 1376.92029, 0.776053488, -6.97791975e-08, 0.630666852, 6.99138596e-08, 1, 2.4612488e-08, -0.630666852, 2.49917598e-08, 0.776053488)
            elseif MyLevel == 10 or MyLevel <= 14 then -- Monkey
                Nonquest = false
                Ms = "Monkey [Lv. 14]"
                NameQuest = "JungleQuest"
                LevelQuest = 1
                NameMon = "Monkey"
                CFrameQuest = CFrame.new(-1598.08911, 35.5501175, 153.377838, 0, 0, 1, 0, 1, -0, -1, 0, 0)
                CFrameMon = CFrame.new(-1402.74609, 98.5633316, 90.6417007, 0.836947978, 0, 0.547282517, -0, 1, -0, -0.547282517, 0, 0.836947978)
            elseif MyLevel == 15 or MyLevel <= 29 then -- Gorilla
                Nonquest = false
                Ms = "Gorilla [Lv. 20]"
                NameQuest = "JungleQuest"
                LevelQuest = 2
                NameMon = "Gorilla"
                CFrameQuest = CFrame.new(-1598.08911, 35.5501175, 153.377838, 0, 0, 1, 0, 1, -0, -1, 0, 0)
                CFrameMon = CFrame.new(-1267.89001, 66.2034225, -531.818115, -0.813996196, -5.25169774e-08, -0.580869019, -5.58769671e-08, 1, -1.21082593e-08, 0.580869019, 2.26011476e-08, -0.813996196)
            elseif MyLevel >= 30 and MyLevel <= 40-1 then
                Nonquest = false
                Ms = "Pirate [Lv. 35]"
                NameQuest = "BuggyQuest1"
                LevelQuest = 1
                NameMon = "Pirate"
                CFrameQuest = CFrame.new(-1141.07483, 4.10001802, 3831.5498, 0.965929627, -0, -0.258804798, 0, 1, -0, 0.258804798, 0, 0.965929627)
                CFrameMon = CFrame.new(-1169.5365, 5.09531212, 3933.84082, -0.971822679, -3.73200315e-09, 0.235713184, -4.16762763e-10, 1, 1.41145424e-08, -0.235713184, 1.3618596e-08, -0.971822679)
            elseif MyLevel >= 40 and MyLevel <= 60-1 then
                Nonquest = false
                Ms = "Brute [Lv. 45]"
                NameQuest = "BuggyQuest1"
                LevelQuest = 2
                NameMon = "Brute"
                CFrameQuest = CFrame.new(-1141.07483, 4.10001802, 3831.5498, 0.965929627, -0, -0.258804798, 0, 1, -0, 0.258804798, 0, 0.965929627)
                CFrameMon = CFrame.new(-1165.09985, 15.1531372, 4363.51514, -0.962800264, 1.17564889e-06, 0.270213336, 2.60172015e-07, 1, -3.4237969e-06, -0.270213336, -3.22613073e-06, -0.962800264)
            elseif MyLevel >= 60 and MyLevel <= 75-1 then
                Nonquest = false
                Ms = "Desert Bandit [Lv. 60]"
                NameQuest = "DesertQuest"
                LevelQuest = 1
                NameMon = "Desert Bandit"
                CFrameQuest = CFrame.new(894.488647, 5.14000702, 4392.43359, 0.819155693, -0, -0.573571265, 0, 1, -0, 0.573571265, 0, 0.819155693)
                CFrameMon = CFrame.new(932.788818, 6.8503746, 4488.24609, -0.998625934, 3.08948351e-08, 0.0524050146, 2.79967303e-08, 1, -5.60361286e-08, -0.0524050146, -5.44919629e-08, -0.998625934)
            elseif MyLevel >= 75 and MyLevel <= 90-1 then
                Nonquest = false
                Ms = "Desert Officer [Lv. 70]"
                NameQuest = "DesertQuest"
                LevelQuest = 2
                NameMon = "Desert Officer"
                CFrameQuest = CFrame.new(894.488647, 5.14000702, 4392.43359, 0.819155693, -0, -0.573571265, 0, 1, -0, 0.573571265, 0, 0.819155693)
                CFrameMon = CFrame.new(1617.07886, 1.5542295, 4295.54932, -0.997540116, -2.26287735e-08, -0.070099175, -1.69377223e-08, 1, -8.17798806e-08, 0.070099175, -8.03913949e-08, -0.997540116)
            elseif MyLevel == 90 or MyLevel <= 99 then -- Snow Bandits
                Nonquest = false
                Ms = "Snow Bandit [Lv. 90]"
                NameQuest = "SnowQuest"
                LevelQuest = 1
                NameMon = "Snow Bandits"
                CFrameQuest = CFrame.new(1389.74451, 86.6520844, -1298.90796, -0.342042685, 0, 0.939684391, 0, 1, 0, -0.939684391, 0, -0.342042685)
                CFrameMon = CFrame.new(1412.92346, 55.3503647, -1260.62036, -0.246266365, -0.0169920288, -0.969053388, 0.000432241941, 0.999844253, -0.0176417865, 0.969202161, -0.00476344163, -0.246220857)
            elseif MyLevel == 100 or MyLevel <= 119 then -- Snowman
                Nonquest = false
                Ms = "Snowman [Lv. 100]"
                NameQuest = "SnowQuest"
                LevelQuest = 2
                NameMon = "Snowman"
                CFrameQuest = CFrame.new(1389.74451, 86.6520844, -1298.90796, -0.342042685, 0, 0.939684391, 0, 1, 0, -0.939684391, 0, -0.342042685)
                CFrameMon = CFrame.new(1376.86401, 97.2779999, -1396.93115, -0.986755967, 7.71178321e-08, -0.162211925, 7.71531674e-08, 1, 6.08143536e-09, 0.162211925, -6.51427134e-09, -0.986755967)
            elseif MyLevel == 120 or MyLevel <= 149 then -- Chief Petty Officer
                Nonquest = false
                Ms = "Chief Petty Officer [Lv. 120]"
                NameQuest = "MarineQuest2"
                LevelQuest = 1
                NameMon = "Chief Petty Officer"
                CFrameQuest = CFrame.new(-5039.58643, 27.3500385, 4324.68018, 0, 0, -1, 0, 1, 0, 1, 0, 0)
                CFrameMon = CFrame.new(-4882.8623, 22.6520386, 4255.53516, 0.273695946, -5.40380647e-08, -0.96181643, 4.37720793e-08, 1, -4.37274998e-08, 0.96181643, -3.01326679e-08, 0.273695946)
            elseif MyLevel == 150 or MyLevel <= 174 then -- Sky Bandit
                Nonquest = false
                Ms = "Sky Bandit [Lv. 150]"
                NameQuest = "SkyQuest"
                LevelQuest = 1
                NameMon = "Sky Bandit"
                CFrameQuest = CFrame.new(-4839.53027, 716.368591, -2619.44165, 0.866007268, 0, 0.500031412, 0, 1, 0, -0.500031412, 0, 0.866007268)
                CFrameMon = CFrame.new(-4959.51367, 365.39267, -2974.56812, 0.964867651, 7.74418396e-08, 0.262737453, -6.95931988e-08, 1, -3.91783708e-08, -0.262737453, 1.95171506e-08, 0.964867651)
            elseif MyLevel == 175 or MyLevel <= 189 then -- Dark Master
                Nonquest = false
                Ms = "Dark Master [Lv. 175]"
                NameQuest = "SkyQuest"
                LevelQuest = 2
                NameMon = "Dark Master"
                CFrameQuest = CFrame.new(-4839.53027, 716.368591, -2619.44165, 0.866007268, 0, 0.500031412, 0, 1, 0, -0.500031412, 0, 0.866007268)
                CFrameMon = CFrame.new(-5079.98096, 376.477356, -2194.17139, 0.465965867, -3.69776352e-08, 0.884802461, 3.40249851e-09, 1, 4.00000886e-08, -0.884802461, -1.56281423e-08, 0.465965867)
            elseif MyLevel == 190 or MyLevel <= 209 then
                Nonquest = false
                Ms = "Prisoner [Lv. 190]"
                LevelQuest = 1
                NameQuest = "PrisonerQuest"
                NameMon = "Prisoner"
                CFrameQuest = CFrame.new(5308.93115, 1.65517521, 475.120514, -0.0894274712, -5.00292918e-09, -0.995993316, 1.60817859e-09, 1, -5.16744869e-09, 0.995993316, -2.06384709e-09, -0.0894274712)
                CFrameMon = CFrame.new(5433.39307, 88.678093, 514.986877, 0.879988372, 0, -0.474995494, 0, 1, 0, 0.474995494, 0, 0.879988372)
            elseif MyLevel == 210 or MyLevel <= 249 then
                Nonquest = false
                Ms = "Dangerous Prisoner [Lv. 210]"
                LevelQuest = 2
                NameQuest = "PrisonerQuest"
                NameMon = "Dangerous Prisoner"
                CFrameQuest = CFrame.new(5308.93115, 1.65517521, 475.120514, -0.0894274712, -5.00292918e-09, -0.995993316, 1.60817859e-09, 1, -5.16744869e-09, 0.995993316, -2.06384709e-09, -0.0894274712)
                CFrameMon = CFrame.new(5433.39307, 88.678093, 514.986877, 0.879988372, 0, -0.474995494, 0, 1, 0, 0.474995494, 0, 0.879988372)
            elseif MyLevel == 250 or MyLevel <= 274 then -- Toga Warrior
                Nonquest = false
                Ms = "Toga Warrior [Lv. 250]"
                NameQuest = "ColosseumQuest"
                LevelQuest = 1
                NameMon = "Toga Warrior"
                CFrameQuest = CFrame.new(-1576.11743, 7.38933945, -2983.30762, 0.576966345, 1.22114863e-09, 0.816767931, -3.58496594e-10, 1, -1.24185606e-09, -0.816767931, 4.2370063e-10, 0.576966345)
                CFrameMon = CFrame.new(-1779.97583, 44.6077499, -2736.35474, 0.984437346, 4.10396339e-08, 0.175734788, -3.62286876e-08, 1, -3.05844168e-08, -0.175734788, 2.3741821e-08, 0.984437346)
            elseif MyLevel == 275 or MyLevel <= 299 then -- Gladiato
                Nonquest = false
                Ms = "Gladiator [Lv. 275]"
                NameQuest = "ColosseumQuest"
                LevelQuest = 2
                NameMon = "Gladiato"
                CFrameQuest = CFrame.new(-1576.11743, 7.38933945, -2983.30762, 0.576966345, 1.22114863e-09, 0.816767931, -3.58496594e-10, 1, -1.24185606e-09, -0.816767931, 4.2370063e-10, 0.576966345)
                CFrameMon = CFrame.new(-1274.75903, 58.1895943, -3188.16309, 0.464524001, 6.21005611e-08, 0.885560572, -4.80449414e-09, 1, -6.76054768e-08, -0.885560572, 2.71497012e-08, 0.464524001)
            elseif MyLevel == 300 or MyLevel <= 329 then -- Military Soldier
                Nonquest = false
                Ms = "Military Soldier [Lv. 300]"
                NameQuest = "MagmaQuest"
                LevelQuest = 1
                NameMon = "Military Soldier"
                CFrameQuest = CFrame.new(-5316.55859, 12.2370615, 8517.2998, 0.588437557, -1.37880001e-08, -0.808542669, -2.10116209e-08, 1, -3.23446478e-08, 0.808542669, 3.60215964e-08, 0.588437557)
                CFrameMon = CFrame.new(-5363.01123, 41.5056877, 8548.47266, -0.578253984, -3.29503091e-10, 0.815856814, 9.11209668e-08, 1, 6.498761e-08, -0.815856814, 1.11920997e-07, -0.578253984)
            elseif MyLevel == 330 or MyLevel <= 374 then -- Military Spy
                Nonquest = false
                Ms = "Military Spy [Lv. 325]"
                NameQuest = "MagmaQuest"
                LevelQuest = 2
                NameMon = "Military Spy"
                CFrameQuest = CFrame.new(-5316.55859, 12.2370615, 8517.2998, 0.588437557, -1.37880001e-08, -0.808542669, -2.10116209e-08, 1, -3.23446478e-08, 0.808542669, 3.60215964e-08, 0.588437557)
                CFrameMon = CFrame.new(-5787.99023, 120.864456, 8762.25293, -0.188358366, -1.84706277e-08, 0.982100308, -1.23782129e-07, 1, -4.93306951e-09, -0.982100308, -1.22495649e-07, -0.188358366)
            elseif MyLevel == 375 or MyLevel <= 399 then -- Fishman Warrior
                Nonquest = false
                Ms = "Fishman Warrior [Lv. 375]"
                NameQuest = "FishmanQuest"
                LevelQuest = 1
                NameMon = "Fishman Warrior"
                CFrameQuest = CFrame.new(61122.5625, 18.4716396, 1568.16504, 0.893533468, 3.95251609e-09, 0.448996574, -2.34327455e-08, 1, 3.78297464e-08, -0.448996574, -4.43233645e-08, 0.893533468)
                CFrameMon = CFrame.new(60946.6094, 48.6735229, 1525.91687, -0.0817126185, 8.90751153e-08, 0.996655822, 2.00889794e-08, 1, -8.77269599e-08, -0.996655822, 1.28533992e-08, -0.0817126185)
            elseif MyLevel == 400 or MyLevel <= 449 then -- Fishman Commando
                Nonquest = false
                Ms = "Fishman Commando [Lv. 400]"
                NameQuest = "FishmanQuest"
                LevelQuest = 2
                NameMon = "Fishman Commando"
                CFrameQuest = CFrame.new(61122.5625, 18.4716396, 1568.16504)
                CFrameMon = CFrame.new(60946.6094, 48.6735229, 1525.916871)
            elseif MyLevel == 450 or MyLevel <= 474 then 
                Nonquest = false
                Ms = "God's Guard [Lv. 450]"
                NameQuest = "SkyExp1Quest"
                LevelQuest = 1
                NameMon = "God's Guards"
                CFrameQuest = CFrame.new(-4721.71436, 845.277161, -1954.20105)
                CFrameMon = CFrame.new(-4716.95703, 853.089722, -1933.925427)
            elseif MyLevel == 475 or MyLevel <= 524 then 
                Nonquest = false
                Ms = "Shanda [Lv. 475]"
                NameQuest = "SkyExp1Quest"
                LevelQuest = 2
                NameMon = "Shandas"
                CFrameQuest = CFrame.new(-7859.09814, 5544.19043, -381.476196, -0.422592998, 0, 0.906319618, 0, 1, 0, -0.906319618, 0, -0.422592998)
                CFrameMon = CFrame.new(-7904.57373, 5584.37646, -459.62973, 0.65171206, 5.11171692e-08, 0.758466363, -4.76232476e-09, 1, -6.33034247e-08, -0.758466363, 3.76435416e-08, 0.65171206)
            elseif MyLevel == 525 or MyLevel <= 549 then -- Royal Squad
                Nonquest = false
                Ms = "Royal Squad [Lv. 525]"
                NameQuest = "SkyExp2Quest"
                LevelQuest = 1
                NameMon = "Royal Squad"
                CFrameQuest = CFrame.new(-7906.81592, 5634.6626, -1411.99194, 0, 0, -1, 0, 1, 0, 1, 0, 0)
                CFrameMon = CFrame.new(-7555.04199, 5606.90479, -1303.24744, -0.896107852, -9.6057462e-10, -0.443836004, -4.24974544e-09, 1, 6.41599973e-09, 0.443836004, 7.63560326e-09, -0.896107852)
            elseif MyLevel == 550 or MyLevel <= 624 then -- Royal Soldier
                Nonquest = false
                Ms = "Royal Soldier [Lv. 550]"
                NameQuest = "SkyExp2Quest"
                LevelQuest = 2
                NameMon = "Royal Soldier"
                CFrameQuest = CFrame.new(-7906.81592, 5634.6626, -1411.99194, 0, 0, -1, 0, 1, 0, 1, 0, 0)
                CFrameMon = CFrame.new(-7837.31152, 5649.65186, -1791.08582, -0.716008604, 0.0104285581, -0.698013008, 5.02521061e-06, 0.99988848, 0.0149335321, 0.69809103, 0.0106890313, -0.715928733)
            elseif MyLevel == 625 or MyLevel <= 649 then -- Galley Pirate
                Nonquest = false
                Ms = "Galley Pirate [Lv. 625]"
                NameQuest = "FountainQuest"
                LevelQuest = 1
                NameMon = "Galley Pirate"
                CFrameQuest = CFrame.new(5259.81982, 37.3500175, 4050.0293, 0.087131381, 0, 0.996196866, 0, 1, 0, -0.996196866, 0, 0.087131381)
                CFrameMon = CFrame.new(5569.80518, 38.5269432, 3849.01196, 0.896460414, 3.98027495e-08, 0.443124533, -1.34262139e-08, 1, -6.26611296e-08, -0.443124533, 5.02237434e-08, 0.896460414)
            elseif MyLevel >= 650 then -- Galley Captain
                Nonquest = false
                Ms = "Galley Captain [Lv. 650]"
                NameQuest = "FountainQuest"
                LevelQuest = 2
                NameMon = "Galley Captain"
                CFrameQuest = CFrame.new(5259.81982, 37.3500175, 4050.0293, 0.087131381, 0, 0.996196866, 0, 1, 0, -0.996196866, 0, 0.087131381)
                CFrameMon = CFrame.new(5782.90186, 94.5326462, 4716.78174, 0.361808896, -1.24757526e-06, -0.932252586, 2.16989656e-06, 1, -4.96097414e-07, 0.932252586, -1.84339774e-06, 0.361808896)
            end
        end
        if NewWorld then
            Nonquest = false
            if MyLevel == 700 or MyLevel <= 724 then -- Raider [Lv. 700]
                Ms = "Raider [Lv. 700]"
                NameQuest = "Area1Quest"
                LevelQuest = 1
                NameMon = "Raider"
                CFrameQuest = CFrame.new(-429.543518, 71.7699966, 1836.18188, -0.22495985, 0, -0.974368095, 0, 1, 0, 0.974368095, 0, -0.22495985)
                CFrameMon = CFrame.new(-737.026123, 10.1748352, 2392.57959, 0.272128761, 0, -0.962260842, -0, 1, -0, 0.962260842, 0, 0.272128761)
            elseif MyLevel == 725 or MyLevel <= 774 then -- Mercenary [Lv. 725]
                Ms = "Mercenary [Lv. 725]"
                NameQuest = "Area1Quest"
                LevelQuest = 2
                NameMon = "Mercenary"
                CFrameQuest = CFrame.new(-429.543518, 71.7699966, 1836.18188, -0.22495985, 0, -0.974368095, 0, 1, 0, 0.974368095, 0, -0.22495985)
                CFrameMon = CFrame.new(-1022.21271, 72.9855194, 1891.39148, -0.990782857, 0, -0.135460541, 0, 1, 0, 0.135460541, 0, -0.990782857)
            elseif MyLevel == 775 or MyLevel <= 799 then -- Swan Pirate [Lv. 775]
                Ms = "Swan Pirate [Lv. 775]"
                NameQuest = "Area2Quest"
                LevelQuest = 1
                NameMon = "Swan Pirate"
                CFrameQuest = CFrame.new(638.43811, 71.769989, 918.282898, 0.139203906, 0, 0.99026376, 0, 1, 0, -0.99026376, 0, 0.139203906)
                CFrameMon = CFrame.new(976.467651, 111.174057, 1229.1084, 0.00852567982, -4.73897828e-08, -0.999963999, 1.12251888e-08, 1, -4.7295778e-08, 0.999963999, -1.08215579e-08, 0.00852567982)
            elseif MyLevel == 800 or MyLevel <= 874 then -- Factory Staff [Lv. 800]
                Ms = "Factory Staff [Lv. 800]"
                NameQuest = "Area2Quest"
                LevelQuest = 2
                NameMon = "Factory Staff"
                CFrameQuest = CFrame.new(638.43811, 71.769989, 918.282898, 0.139203906, 0, 0.99026376, 0, 1, 0, -0.99026376, 0, 0.139203906)
                CFrameMon = CFrame.new(336.74585, 73.1620483, -224.129272, 0.993632793, 3.40154607e-08, 0.112668738, -3.87658332e-08, 1, 3.99718729e-08, -0.112668738, -4.40850592e-08, 0.993632793)
            elseif MyLevel == 875 or MyLevel <= 899 then -- Marine Lieutenant [Lv. 875]
                Ms = "Marine Lieutenant [Lv. 875]"
                NameQuest = "MarineQuest3"
                LevelQuest = 1
                NameMon = "Marine Lieutenant"
                CFrameQuest = CFrame.new(-2440.79639, 71.7140732, -3216.06812, 0.866007268, 0, 0.500031412, 0, 1, 0, -0.500031412, 0, 0.866007268)
                CFrameMon = CFrame.new(-2842.69922, 72.9919434, -2901.90479, -0.762281299, 0, -0.64724648, 0, 1.00000012, 0, 0.64724648, 0, -0.762281299)
            elseif MyLevel == 900 or MyLevel <= 949 then -- Marine Captain [Lv. 900]
                Ms = "Marine Captain [Lv. 900]"
                NameQuest = "MarineQuest3"
                LevelQuest = 2
                NameMon = "Marine Captain"
                CFrameQuest = CFrame.new(-2440.79639, 71.7140732, -3216.06812, 0.866007268, 0, 0.500031412, 0, 1, 0, -0.500031412, 0, 0.866007268)
                CFrameMon = CFrame.new(-1814.70313, 72.9919434, -3208.86621, -0.900422215, 7.93464423e-08, -0.435017526, 3.68856199e-08, 1, 1.06050372e-07, 0.435017526, 7.94441988e-08, -0.900422215)
            elseif MyLevel == 950 or MyLevel <= 974 then -- Zombie [Lv. 950]
                Ms = "Zombie [Lv. 950]"
                NameQuest = "ZombieQuest"
                LevelQuest = 1
                NameMon = "Zombie"
                CFrameQuest = CFrame.new(-5497.06152, 47.5923004, -795.237061, -0.29242146, 0, -0.95628953, 0, 1, 0, 0.95628953, 0, -0.29242146)
                CFrameMon = CFrame.new(-5649.23438, 126.0578, -737.773743, 0.355238914, -8.10359282e-08, 0.934775114, 1.65461245e-08, 1, 8.04023372e-08, -0.934775114, -1.3095117e-08, 0.355238914)
            elseif MyLevel == 975 or MyLevel <= 999 then -- Vampire [Lv. 975]
                Ms = "Vampire [Lv. 975]"
                NameQuest = "ZombieQuest"
                LevelQuest = 2
                NameMon = "Vampire"
                CFrameQuest = CFrame.new(-5497.06152, 47.5923004, -795.237061, -0.29242146, 0, -0.95628953, 0, 1, 0, 0.95628953, 0, -0.29242146)
                CFrameMon = CFrame.new(-6030.32031, 0.4377408, -1313.5564, -0.856965423, 3.9138893e-08, -0.515373945, -1.12178942e-08, 1, 9.45958547e-08, 0.515373945, 8.68467822e-08, -0.856965423)
            elseif MyLevel == 1000 or MyLevel <= 1049 then -- Snow Trooper [Lv. 1000] **
                Ms = "Snow Trooper [Lv. 1000]"
                NameQuest = "SnowMountainQuest"
                LevelQuest = 1
                NameMon = "Snow Trooper"
                CFrameQuest = CFrame.new(609.858826, 400.119904, -5372.25928, -0.374604106, 0, 0.92718488, 0, 1, 0, -0.92718488, 0, -0.374604106)
                CFrameMon = CFrame.new(621.003418, 391.361053, -5335.43604, 0.481644779, 0, 0.876366913, 0, 1, 0, -0.876366913, 0, 0.481644779)
            elseif MyLevel == 1050 or MyLevel <= 1099 then -- Winter Warrior [Lv. 1050]
                Ms = "Winter Warrior [Lv. 1050]"
                NameQuest = "SnowMountainQuest"
                LevelQuest = 2
                NameMon = "Winter Warrior"
                CFrameQuest = CFrame.new(609.858826, 400.119904, -5372.25928, -0.374604106, 0, 0.92718488, 0, 1, 0, -0.92718488, 0, -0.374604106)
                CFrameMon = CFrame.new(1295.62683, 429.447784, -5087.04492, -0.698032081, -8.28980049e-08, -0.71606636, -1.98835952e-08, 1, -9.63858184e-08, 0.71606636, -5.30424877e-08, -0.698032081)
            elseif MyLevel == 1100 or MyLevel <= 1124 then -- Lab Subordinate [Lv. 1100]
                Ms = "Lab Subordinate [Lv. 1100]"
                NameQuest = "IceSideQuest"
                LevelQuest = 1
                NameMon = "Lab Subordinate"
                CFrameQuest = CFrame.new(-6064.06885, 15.2422857, -4902.97852, 0.453972578, -0, -0.891015649, 0, 1, -0, 0.891015649, 0, 0.453972578)
                CFrameMon = CFrame.new(-5769.2041, 37.9288292, -4468.38721, -0.569419742, -2.49055017e-08, 0.822046936, -6.96206541e-08, 1, -1.79282633e-08, -0.822046936, -6.74401548e-08, -0.569419742)
            elseif MyLevel == 1125 or MyLevel <= 1174 then -- Horned Warrior [Lv. 1125]
                Ms = "Horned Warrior [Lv. 1125]"
                NameQuest = "IceSideQuest"
                LevelQuest = 2
                NameMon = "Horned Warrior"
                CFrameQuest = CFrame.new(-6064.06885, 15.2422857, -4902.97852, 0.453972578, -0, -0.891015649, 0, 1, -0, 0.891015649, 0, 0.453972578)
                CFrameMon = CFrame.new(-6401.27979, 15.9775667, -5948.24316, 0.388303697, 0, -0.921531856, 0, 1, 0, 0.921531856, 0, 0.388303697)
            elseif MyLevel == 1175 or MyLevel <= 1199 then -- Magma Ninja [Lv. 1175]
                Ms = "Magma Ninja [Lv. 1175]"
                NameQuest = "FireSideQuest"
                LevelQuest = 1
                NameMon = "Magma Ninja"
                CFrameQuest = CFrame.new(-5428.03174, 15.0622921, -5299.43457, -0.882952213, 0, 0.469463557, 0, 1, 0, -0.469463557, 0, -0.882952213)
                CFrameMon = CFrame.new(-5466.06445, 57.6952019, -5837.42822, -0.988835871, 0, -0.149006829, 0, 1, 0, 0.149006829, 0, -0.988835871)
            elseif MyLevel == 1200 or MyLevel <= 1249 then 
                Ms = "Lava Pirate [Lv. 1200]"
                NameQuest = "FireSideQuest"
                LevelQuest = 2
                NameMon = "Lava Pirate"
                CFrameQuest = CFrame.new(-5431.09473, 15.9868021, -5296.53223, 0.831796765, 1.15322464e-07, -0.555080295, -1.10814341e-07, 1, 4.17010995e-08, 0.555080295, 2.68240168e-08, 0.831796765)
                CFrameMon = CFrame.new(-5169.71729, 34.1234779, -4669.73633, -0.196780294, 0, 0.98044765, 0, 1.00000012, -0, -0.98044765, 0, -0.196780294)
            elseif MyLevel == 1250 or MyLevel <= 1274 then 
                Ms = "Ship Deckhand [Lv. 1250]"
                NameQuest = "ShipQuest1"
                LevelQuest = 1
                NameMon = "Ship Deckhand"
                CFrameQuest = CFrame.new(1037.80127, 125.092171, 32911.6016, -0.244533166, -0, -0.969640911, -0, 1.00000012, -0, 0.96964103, 0, -0.244533136)
                CFrameMon = CFrame.new(1163.80872, 138.288452, 33058.4258, -0.998580813, 5.49076979e-08, -0.0532564968, 5.57436763e-08, 1, -1.42118655e-08, 0.0532564968, -1.71604082e-08, -0.998580813)
            elseif MyLevel == 1275 or MyLevel <= 1299 then 
                Ms = "Ship Engineer [Lv. 1275]"
                NameQuest = "ShipQuest1"
                LevelQuest = 2
                NameMon = "Ship Engineer"
                CFrameQuest = CFrame.new(1037.80127, 125.092171, 32911.6016, -0.244533166, -0, -0.969640911, -0, 1.00000012, -0, 0.96964103, 0, -0.244533136)
                CFrameMon = CFrame.new(921.30249023438, 125.400390625, 32937.34375)
            elseif MyLevel == 1300 or MyLevel <= 1324 then 
                Ms = "Ship Steward [Lv. 1300]"
                NameQuest = "ShipQuest2"
                LevelQuest = 1
                NameMon = "Ship Steward"
                CFrameQuest = CFrame.new(968.80957, 125.092171, 33244.125, -0.869560242, 1.51905191e-08, -0.493826836, 1.44108379e-08, 1, 5.38534195e-09, 0.493826836, -2.43357912e-09, -0.869560242)
                CFrameMon = CFrame.new(917.96057128906, 136.89932250977, 33343.4140625)
            elseif MyLevel == 1325 or MyLevel <= 1349 then 
                Ms = "Ship Officer [Lv. 1325]"
                NameQuest = "ShipQuest2"
                LevelQuest = 2
                NameMon = "Ship Officer"
                CFrameQuest = CFrame.new(968.80957, 125.092171, 33244.125, -0.869560242, 1.51905191e-08, -0.493826836, 1.44108379e-08, 1, 5.38534195e-09, 0.493826836, -2.43357912e-09, -0.869560242)
                CFrameMon = CFrame.new(944.44964599609, 181.40081787109, 33278.9453125)
            elseif MyLevel == 1350 or MyLevel <= 1374 then 
                Ms = "Arctic Warrior [Lv. 1350]"
                NameQuest = "FrostQuest"
                LevelQuest = 1
                NameMon = "Arctic Warrior"
                CFrameQuest = CFrame.new(5667.6582, 26.7997818, -6486.08984, -0.933587909, 0, -0.358349502, 0, 1, 0, 0.358349502, 0, -0.933587909)
                CFrameMon = CFrame.new(5878.23486, 81.3886948, -6136.35596, -0.451037169, 2.3908234e-07, 0.892505825, -1.08168464e-07, 1, -3.22542007e-07, -0.892505825, -2.4201924e-07, -0.451037169)
            elseif MyLevel == 1375 or MyLevel <= 1424 then -- Snow Lurker [Lv. 1375]
                Ms = "Snow Lurker [Lv. 1375]"
                NameQuest = "FrostQuest"
                LevelQuest = 2
                NameMon = "Snow Lurker"
                CFrameQuest = CFrame.new(5667.6582, 26.7997818, -6486.08984, -0.933587909, 0, -0.358349502, 0, 1, 0, 0.358349502, 0, -0.933587909)
                CFrameMon = CFrame.new(5513.36865, 60.546711, -6809.94971, -0.958693981, -1.65617333e-08, 0.284439981, -4.07668654e-09, 1, 4.44854642e-08, -0.284439981, 4.14883701e-08, -0.958693981)
            elseif MyLevel == 1425 or MyLevel <= 1449 then -- Sea Soldier [Lv. 1425]
                Ms = "Sea Soldier [Lv. 1425]"
                NameQuest = "ForgottenQuest"
                LevelQuest = 1
                NameMon = "Sea Soldier"
                CFrameQuest = CFrame.new(-3054.44458, 235.544281, -10142.8193, 0.990270376, -0, -0.13915664, 0, 1, -0, 0.13915664, 0, 0.990270376)
                CFrameMon = CFrame.new(-3115.78223, 63.8785706, -9808.38574, -0.913427353, 3.11199457e-08, 0.407000452, 7.79564235e-09, 1, -5.89660658e-08, -0.407000452, -5.06883708e-08, -0.913427353)
            elseif MyLevel >= 1450 then -- Water Fighter [Lv. 1450]
                Ms = "Water Fighter [Lv. 1450]"
                NameQuest = "ForgottenQuest"
                LevelQuest = 2
                NameMon = "Water Fighter"
                CFrameQuest = CFrame.new(-3054.44458, 235.544281, -10142.8193, 0.990270376, -0, -0.13915664, 0, 1, -0, 0.13915664, 0, 0.990270376)
                CFrameMon = CFrame.new(-3212.99683, 263.809296, -10551.8799, 0.742111444, -5.59139615e-08, -0.670276582, 1.69155214e-08, 1, -6.46908234e-08, 0.670276582, 3.66697037e-08, 0.742111444)
            end
        end
        if ThreeWorld then
            if MyLevel >= 1500 and MyLevel <= 1524 then -- Pirate Millionaire [Lv. 1500]
                Ms = "Pirate Millionaire [Lv. 1500]"
                NameQuest = "PiratePortQuest"
                LevelQuest = 1
                NameMon = "Pirate Millionaire"
                CFrameQuest = CFrame.new(-290.074677, 42.9034653, 5581.58984, 0.965929627, -0, -0.258804798, 0, 1, -0, 0.258804798, 0, 0.965929627)
                CFrameMon = CFrame.new(81.164993286133, 43.755737304688, 5724.7021484375)
            elseif MyLevel >= 1525 and MyLevel <= 1574 then -- Pistol Billionaire [Lv. 1525]
                Ms = "Pistol Billionaire [Lv. 1525]"
                NameQuest = "PiratePortQuest"
                LevelQuest = 2
                NameMon = "Pistol Billionaire"
                CFrameQuest = CFrame.new(-290.074677, 42.9034653, 5581.58984, 0.965929627, -0, -0.258804798, 0, 1, -0, 0.258804798, 0, 0.965929627)
                CFrameMon = CFrame.new(81.164993286133, 43.755737304688, 5724.7021484375)
            elseif MyLevel >= 1575 and MyLevel <= 1599 then -- Dragon Crew Warrior [Lv. 1575]
                Ms = "Dragon Crew Warrior [Lv. 1575]"
                NameQuest = "AmazonQuest"
                LevelQuest = 1
                NameMon = "Dragon Crew Warrior"
                CFrameQuest = CFrame.new(5832.83594, 51.6806107, -1101.51563, 0.898790359, -0, -0.438378751, 0, 1, -0, 0.438378751, 0, 0.898790359)
                CFrameMon = CFrame.new(6241.9951171875, 51.522083282471, -1243.9771728516)
            elseif MyLevel >= 1600 and MyLevel <= 1624 then -- Dragon Crew Archer [Lv. 1600]
                Ms = "Dragon Crew Archer [Lv. 1600]"
                NameQuest = "AmazonQuest"
                LevelQuest = 2
                NameMon = "Dragon Crew Archer"
                CFrameQuest = CFrame.new(5832.83594, 51.6806107, -1101.51563, 0.898790359, -0, -0.438378751, 0, 1, -0, 0.438378751, 0, 0.898790359)
                CFrameMon = CFrame.new(6488.9155273438, 383.38375854492, -110.66246032715)
            elseif MyLevel >= 1625 and MyLevel <= 1649 then -- Female Islander [Lv. 1625]
                Ms = "Female Islander [Lv. 1625]"
                NameQuest = "AmazonQuest2"
                LevelQuest = 1
                NameMon = "Female Islander"
                CFrameQuest = CFrame.new(5448.86133, 601.516174, 751.130676, 0, 0, 1, 0, 1, -0, -1, 0, 0)
                CFrameMon = CFrame.new(4770.4990234375, 758.95520019531, 1069.8680419922)
            elseif MyLevel >= 1650 and MyLevel <= 1699 then -- Giant Islander [Lv. 1650]
                Ms = "Giant Islander [Lv. 1650]"
                NameQuest = "AmazonQuest2"
                LevelQuest = 2
                NameMon = "Giant Islander"
                CFrameQuest = CFrame.new(5448.86133, 601.516174, 751.130676, 0, 0, 1, 0, 1, -0, -1, 0, 0)
                CFrameMon = CFrame.new(4530.3540039063, 656.75695800781, -131.60952758789)
            elseif MyLevel >= 1700 and MyLevel <= 1724 then -- Marine Commodore [Lv. 1700]
                Ms = "Marine Commodore [Lv. 1700]"
                NameQuest = "MarineTreeIsland"
                LevelQuest = 1
                NameMon = "Marine Commodore"
                CFrameQuest = CFrame.new(2180.54126, 27.8156815, -6741.5498, -0.965929747, 0, 0.258804798, 0, 1, 0, -0.258804798, 0, -0.965929747)
                CFrameMon = CFrame.new(2490.0844726563, 190.4232635498, -7160.0502929688)
            elseif MyLevel >= 1725 and MyLevel <= 1774 then -- Marine Rear Admiral [Lv. 1725]
                Ms = "Marine Rear Admiral [Lv. 1725]"
                NameQuest = "MarineTreeIsland"
                LevelQuest = 2
                NameMon = "Marine Rear Admiral"
                CFrameQuest = CFrame.new(2180.54126, 27.8156815, -6741.5498, -0.965929747, 0, 0.258804798, 0, 1, 0, -0.258804798, 0, -0.965929747)
                CFrameMon = CFrame.new(3951.3903808594, 229.11549377441, -6912.81640625)
            elseif MyLevel >= 1775 and MyLevel <= 1799 then -- Fishman Raider [Lv. 1775]
                Ms = "Fishman Raider [Lv. 1775]"
                NameQuest = "DeepForestIsland3"
                LevelQuest = 1
                NameMon = "Fishman Raider"
                CFrameQuest = CFrame.new(-10581.6563, 330.872955, -8761.18652, -0.882952213, 0, 0.469463557, 0, 1, 0, -0.469463557, 0, -0.882952213)
                CFrameMon = CFrame.new(-10322.400390625, 390.94473266602, -8580.0908203125)
            elseif MyLevel >= 1800 and MyLevel <= 1824 then -- Fishman Captain [Lv. 1800]
                Ms = "Fishman Captain [Lv. 1800]"
                NameQuest = "DeepForestIsland3"
                LevelQuest = 2
                NameMon = "Fishman Captain"
                CFrameQuest = CFrame.new(-10581.6563, 330.872955, -8761.18652, -0.882952213, 0, 0.469463557, 0, 1, 0, -0.469463557, 0, -0.882952213)
                CFrameMon = CFrame.new(-11194.541992188, 442.02795410156, -8608.806640625)
            elseif MyLevel >= 1825 and MyLevel <= 1849 then -- Forest Pirate [Lv. 1825]
                Ms = "Forest Pirate [Lv. 1825]"
                NameQuest = "DeepForestIsland"
                LevelQuest = 1
                NameMon = "Forest Pirate"
                CFrameQuest = CFrame.new(-13234.04, 331.488495, -7625.40137, 0.707134247, -0, -0.707079291, 0, 1, -0, 0.707079291, 0, 0.707134247)
                CFrameMon = CFrame.new(-13225.809570313, 428.19387817383, -7753.1245117188)
            elseif MyLevel >= 1850 and MyLevel <= 1899 then -- Mythological Pirate [Lv. 1850]
                Ms = "Mythological Pirate [Lv. 1850]"
                NameQuest = "DeepForestIsland"
                LevelQuest = 2
                NameMon = "Mythological Pirate"
                CFrameQuest = CFrame.new(-13234.04, 331.488495, -7625.40137, 0.707134247, -0, -0.707079291, 0, 1, -0, 0.707079291, 0, 0.707134247)
                CFrameMon = CFrame.new(-13869.172851563, 564.95251464844, -7084.4135742188)
            elseif MyLevel >= 1900 and MyLevel <= 1924 then -- Jungle Pirate [Lv. 1900]
                Ms = "Jungle Pirate [Lv. 1900]"
                NameQuest = "DeepForestIsland2"
                LevelQuest = 1
                NameMon = "Jungle Pirate"
                CFrameQuest = CFrame.new(-12680.3818, 389.971039, -9902.01953, -0.0871315002, 0, 0.996196866, 0, 1, 0, -0.996196866, 0, -0.0871315002)
                CFrameMon = CFrame.new(-11982.221679688, 376.32522583008, -10451.415039063)
            elseif MyLevel >= 1925 and MyLevel <= 1974 then -- Musketeer Pirate [Lv. 1925]
                Ms = "Musketeer Pirate [Lv. 1925]"
                NameQuest = "DeepForestIsland2"
                LevelQuest = 2
                NameMon = "Musketeer Pirate"
                CFrameQuest = CFrame.new(-12680.3818, 389.971039, -9902.01953, -0.0871315002, 0, 0.996196866, 0, 1, 0, -0.996196866, 0, -0.0871315002)
                CFrameMon = CFrame.new(-13282.3046875, 496.23684692383, -9565.150390625)
            elseif MyLevel >= 1975 and MyLevel <= 1999 then
                Ms = "Reborn Skeleton [Lv. 1975]"
                NameQuest = "HauntedQuest1"
                LevelQuest = 1
                NameMon = "Reborn Skeleton"
                CFrameQuest = CFrame.new(-9480.8271484375, 142.13066101074, 5566.0712890625)
                CFrameMon = CFrame.new(-8817.880859375, 191.16761779785, 6298.6557617188)
            elseif MyLevel >= 2000 and MyLevel <= 2024 then
                Ms = "Living Zombie [Lv. 2000]"
                NameQuest = "HauntedQuest1"
                LevelQuest = 2
                NameMon = "Living Zombie"
                CFrameQuest = CFrame.new(-9480.8271484375, 142.13066101074, 5566.0712890625)
                CFrameMon = CFrame.new(-10125.234375, 183.94705200195, 6242.013671875)
            elseif MyLevel >= 2025 and MyLevel <= 2049  then
                Ms = "Demonic Soul [Lv. 2025]"
                NameQuest = "HauntedQuest2"
                LevelQuest = 1
                NameMon = "Demonic Soul"
                CFrameQuest = CFrame.new(-9516.9931640625, 178.00651550293, 6078.4653320313)
                CFrameMon = CFrame.new(-9712.03125, 204.69589233398, 6193.322265625)
            elseif MyLevel >= 2050 and MyLevel <= 2074 then
                Ms = "Posessed Mummy [Lv. 2050]"
                NameQuest = "HauntedQuest2"
                LevelQuest = 2
                NameMon = "Posessed Mummy"
                CFrameQuest = CFrame.new(-9516.9931640625, 178.00651550293, 6078.4653320313)
                CFrameMon = CFrame.new(-9545.7763671875, 69.619895935059, 6339.5615234375)    
            elseif MyLevel >= 2075 and MyLevel <= 2099 then
                Ms = "Peanut Scout [Lv. 2075]"
                NameQuest = "NutsIslandQuest"
                LevelQuest = 1
                NameMon = "Peanut Scout"
                CFrameQuest = CFrame.new(-2104.17163, 38.1299706, -10194.418, 0.758814394, -1.38604395e-09, 0.651306927, 2.85280208e-08, 1, -3.1108879e-08, -0.651306927, 4.21863646e-08, 0.758814394)
                CFrameMon = CFrame.new(-2098.07544, 192.611862, -10248.8867, 0.983392298, -9.57031787e-08, 0.181492642, 8.7276355e-08, 1, 5.44169616e-08, -0.181492642, -3.76732068e-08, 0.983392298)
            elseif MyLevel >= 2100 and MyLevel <= 2124 then
                Ms = "Peanut President [Lv. 2100]"
                NameQuest = "NutsIslandQuest"
                LevelQuest = 2
                NameMon = "Peanut President"
                CFrameQuest = CFrame.new(-2104.17163, 38.1299706, -10194.418, 0.758814394, -1.38604395e-09, 0.651306927, 2.85280208e-08, 1, -3.1108879e-08, -0.651306927, 4.21863646e-08, 0.758814394)
                CFrameMon = CFrame.new(-1876.95959, 192.610947, -10542.2939, 0.0553516336, -2.83836812e-08, 0.998466909, -6.89634405e-10, 1, 2.84654931e-08, -0.998466909, -2.26418861e-09, 0.0553516336)
            elseif MyLevel >= 2125 and MyLevel <= 2149 then
                Ms = "Ice Cream Chef [Lv. 2125]"
                NameQuest = "IceCreamIslandQuest"
                LevelQuest = 1
                NameMon = "Ice Cream Chef"
                CFrameQuest = CFrame.new(-820.404358, 65.8453293, -10965.5654, 0.822534859, 5.24448502e-08, -0.568714678, -2.08336317e-08, 1, 6.20846663e-08, 0.568714678, -3.92184099e-08, 0.822534859)
                CFrameMon = CFrame.new(-821.614075, 208.39537, -10990.7617, -0.870096624, 3.18909272e-08, 0.492881238, -1.8357893e-08, 1, -9.71107568e-08, -0.492881238, -9.35439957e-08, -0.870096624)
            elseif MyLevel >= 2150 and MyLevel <= 2199 then 
                Ms = "Ice Cream Commander [Lv. 2150]"
                NameQuest = "IceCreamIslandQuest"
                LevelQuest = 2
                NameMon = "Ice Cream Commander"
                CFrameQuest = CFrame.new(-819.376526, 67.4634171, -10967.2832)
                CFrameMon = CFrame.new(-610.11669921875, 208.26904296875, -11253.686523438)
            elseif MyLevel >= 2200 and MyLevel <= 2224 then 
                Ms = "Cookie Crafter [Lv. 2200]"
                NameQuest = "CakeQuest1"
                LevelQuest = 1
                NameMon = "Cookie Crafter"
                CFrameQuest = CFrame.new(-2020.6068115234375, 37.82400894165039, -12027.80859375)
                CFrameMon = CFrame.new(-2286.684326171875, 146.5656280517578, -12226.8818359375)
            elseif MyLevel >= 2225 and MyLevel <= 2249 then 
                Ms = "Cake Guard [Lv. 2225]"
                NameQuest = "CakeQuest1"
                LevelQuest = 2
                NameMon = "Cake Guard"
                CFrameQuest = CFrame.new(-2020.6068115234375, 37.82400894165039, -12027.80859375)
                CFrameMon = CFrame.new(-1817.9747314453125, 209.5632781982422, -12288.9228515625)
            elseif MyLevel >= 2250 and MyLevel <= 2274 then 
                Ms = "Baking Staff [Lv. 2250]"
                NameQuest = "CakeQuest2"
                LevelQuest = 1
                NameMon = "Baking Staff"
                CFrameQuest = CFrame.new(-1928.31763, 37.7296638, -12840.626)
                CFrameMon = CFrame.new(-1818.347900390625, 93.41275787353516, -12887.66015625)
            elseif MyLevel >= 2275 then 
                Ms = "Head Baker [Lv. 2275]"
                NameQuest = "CakeQuest2"
                LevelQuest = 2
                NameMon = "Head Baker"
                CFrameQuest = CFrame.new(-1928.31763, 37.7296638, -12840.626)
                CFrameMon = CFrame.new(-2288.795166015625, 106.9419174194336, -12811.111328125)
            end
        end
    end
end
CheckQuest()

SelectBoss = ""
function CheckQuestBoss()
    -- Old World
    if SelectBoss == "Saber Expert [Lv. 200] [Boss]" then
        MsBoss = "Saber Expert [Lv. 200] [Boss]"
        NameQuestBoss = ""
        LevelQuestBoss = 3
        NameBoss = ""
        CFrameQuestBoss = CFrame.new(-1458.89502, 29.8870335, -50.633564)
        CFrameBoss = CFrame.new(-1458.89502, 29.8870335, -50.633564, 0.858821094, 1.13848939e-08, 0.512275636, -4.85649254e-09, 1, -1.40823326e-08, -0.512275636, 9.6063415e-09, 0.858821094)
    elseif SelectBoss == "The Saw [Lv. 100] [Boss]" then
        MsBoss = "The Saw [Lv. 100] [Boss]"
        NameQuestBoss = ""
        LevelQuestBoss = 3
        NameBoss = ""
        CFrameQuestBoss = CFrame.new(-683.519897, 13.8534927, 1610.87854)
        CFrameBoss = CFrame.new(-683.519897, 13.8534927, 1610.87854, -0.290192783, 6.88365773e-08, 0.956968188, 6.98413629e-08, 1, -5.07531119e-08, -0.956968188, 5.21077759e-08, -0.290192783)
    elseif SelectBoss == "Greybeard [Lv. 750] [Raid Boss]" then
        MsBoss = "Greybeard [Lv. 750] [Raid Boss]"
        NameQuestBoss = ""
        LevelQuestBoss = 3
        NameBoss = ""
        CFrameQuestBoss = CFrame.new(-4955.72949, 80.8163834, 4305.82666)
        CFrameBoss = CFrame.new(-4955.72949, 80.8163834, 4305.82666, -0.433646321, -1.03394289e-08, 0.901083171, -3.0443168e-08, 1, -3.17633075e-09, -0.901083171, -2.88092288e-08, -0.433646321)
    elseif SelectBoss == "Mob Leader [Lv. 120] [Boss]" then
        MsBoss = "Mob Leader [Lv. 120] [Boss]"
        NameQuestBoss = ""
        LevelQuestBoss = 3
        NameBoss = ""
        CFrameQuestBoss = CFrame.new(-2848.59399, 7.4272871, 5342.44043)
        CFrameBoss = CFrame.new(-2848.59399, 7.4272871, 5342.44043, -0.928248107, -8.7248246e-08, 0.371961564, -7.61816636e-08, 1, 4.44474857e-08, -0.371961564, 1.29216433e-08, -0.92824)
    
    elseif SelectBoss == "The Gorilla King [Lv. 25] [Boss]" then
        MsBoss = "The Gorilla King [Lv. 25] [Boss]"
        NameQuestBoss = "JungleQuest"
        LevelQuestBoss = 3
        NameBoss = "The Gorilla King"
        CFrameQuestBoss = CFrame.new(-1604.12012, 36.8521118, 154.23732, 0.0648873374, -4.70858913e-06, -0.997892559, 1.41431883e-07, 1, -4.70933674e-06, 0.997892559, 1.64442184e-07, 0.0648873374)
        CFrameBoss = CFrame.new(-1223.52808, 6.27936459, -502.292664, 0.310949147, -5.66602516e-08, 0.950426519, -3.37275488e-08, 1, 7.06501808e-08, -0.950426519, -5.40241736e-08, 0.310949147)
    elseif SelectBoss == "Bobby [Lv. 55] [Boss]" then
        MsBoss = "Bobby [Lv. 55] [Boss]"
        NameQuestBoss = "BuggyQuest1"
        LevelQuestBoss = 3
        NameBoss = "Bobby"
        CFrameQuestBoss = CFrame.new(-1139.59717, 4.75205183, 3825.16211, -0.959730506, -7.5857054e-09, 0.280922383, -4.06310328e-08, 1, -1.11807175e-07, -0.280922383, -1.18718916e-07, -0.959730506)
        CFrameBoss = CFrame.new(-1147.65173, 32.5966301, 4156.02588, 0.956680477, -1.77109952e-10, -0.29113996, 5.16530874e-10, 1, 1.08897802e-09, 0.29113996, -1.19218679e-09, 0.956680477)
    elseif SelectBoss == "Yeti [Lv. 110] [Boss]" then
        MsBoss = "Yeti [Lv. 110] [Boss]"
        NameQuestBoss = "SnowQuest"
        LevelQuestBoss = 3
        NameBoss = "Yeti"
        CFrameQuestBoss = CFrame.new(1384.90247, 87.3078308, -1296.6825, 0.280209213, 2.72035177e-08, -0.959938943, -6.75690828e-08, 1, 8.6151708e-09, 0.959938943, 6.24481444e-08, 0.280209213)
        CFrameBoss = CFrame.new(1221.7356, 138.046906, -1488.84082, 0.349343032, -9.49245944e-08, 0.936994851, 6.29478194e-08, 1, 7.7838429e-08, -0.936994851, 3.17894653e-08, 0.349343032)
    elseif SelectBoss == "Vice Admiral [Lv. 130] [Boss]" then
        MsBoss = "Vice Admiral [Lv. 130] [Boss]"
        NameQuestBoss = "MarineQuest2"
        LevelQuestBoss = 2
        NameBoss = "Vice Admiral"
        CFrameQuestBoss = CFrame.new(-5035.42285, 28.6520386, 4324.50293, -0.0611100644, -8.08395768e-08, 0.998130739, -1.57416586e-08, 1, 8.00271849e-08, -0.998130739, -1.08217701e-08, -0.0611100644)
        CFrameBoss = CFrame.new(-5078.45898, 99.6520691, 4402.1665, -0.555574954, -9.88630566e-11, 0.831466436, -6.35508286e-08, 1, -4.23449258e-08, -0.831466436, -7.63661632e-08, -0.555574954)
    elseif SelectBoss == "Warden [Lv. 175] [Boss]" then
        MsBoss = "Warden [Lv. 175] [Boss]"
        NameQuestBoss = "ImpelQuest"
        LevelQuestBoss = 1
        NameBoss = "Warden"
        CFrameQuestBoss = CFrame.new(4851.35059, 5.68744135, 743.251282, -0.538484037, -6.68303741e-08, -0.842635691, 1.38001752e-08, 1, -8.81300792e-08, 0.842635691, -5.90851599e-08, -0.538484037)
        CFrameBoss = CFrame.new(5232.5625, 5.26856995, 747.506897, 0.943829298, -4.5439414e-08, 0.330433697, 3.47818627e-08, 1, 3.81658154e-08, -0.330433697, -2.45289105e-08, 0.943829298)
    elseif SelectBoss == "Chief Warden [Lv. 200] [Boss]" then
        MsBoss = "Chief Warden [Lv. 200] [Boss]"
        NameQuestBoss = "ImpelQuest"
        LevelQuestBoss = 2
        NameBoss = "Chief Warden"
        CFrameQuestBoss = CFrame.new(4851.35059, 5.68744135, 743.251282, -0.538484037, -6.68303741e-08, -0.842635691, 1.38001752e-08, 1, -8.81300792e-08, 0.842635691, -5.90851599e-08, -0.538484037)
        CFrameBoss = CFrame.new(5232.5625, 5.26856995, 747.506897, 0.943829298, -4.5439414e-08, 0.330433697, 3.47818627e-08, 1, 3.81658154e-08, -0.330433697, -2.45289105e-08, 0.943829298)
    elseif SelectBoss == "Swan [Lv. 225] [Boss]" then
        MsBoss = "Swan [Lv. 225] [Boss]"
        NameQuestBoss = "ImpelQuest"
        LevelQuestBoss = 3
        NameBoss = "Swan"
        CFrameQuestBoss = CFrame.new(4851.35059, 5.68744135, 743.251282, -0.538484037, -6.68303741e-08, -0.842635691, 1.38001752e-08, 1, -8.81300792e-08, 0.842635691, -5.90851599e-08, -0.538484037)
        CFrameBoss = CFrame.new(5232.5625, 5.26856995, 747.506897, 0.943829298, -4.5439414e-08, 0.330433697, 3.47818627e-08, 1, 3.81658154e-08, -0.330433697, -2.45289105e-08, 0.943829298)
    elseif SelectBoss == "Magma Admiral [Lv. 350] [Boss]" then
        MsBoss = "Magma Admiral [Lv. 350] [Boss]"
        NameQuestBoss = "MagmaQuest"
        LevelQuestBoss = 3
        NameBoss = "Magma Admiral"
        CFrameQuestBoss = CFrame.new(-5317.07666, 12.2721891, 8517.41699, 0.51175487, -2.65508806e-08, -0.859131515, -3.91131572e-08, 1, -5.42026761e-08, 0.859131515, 6.13418294e-08, 0.51175487)
        CFrameBoss = CFrame.new(-5530.12646, 22.8769703, 8859.91309, 0.857838571, 2.23414389e-08, 0.513919294, 1.53689133e-08, 1, -6.91265853e-08, -0.513919294, 6.71978384e-08, 0.857838571)
    elseif SelectBoss == "Fishman Lord [Lv. 425] [Boss]" then
        MsBoss = "Fishman Lord [Lv. 425] [Boss]"
        NameQuestBoss = "FishmanQuest"
        LevelQuestBoss = 3
        NameBoss = "Fishman Lord"
        CFrameQuestBoss = CFrame.new(61123.0859, 18.5066795, 1570.18018, 0.927145958, 1.0624845e-07, 0.374700129, -6.98219367e-08, 1, -1.10790765e-07, -0.374700129, 7.65569368e-08, 0.927145958)
        CFrameBoss = CFrame.new(61351.7773, 31.0306778, 1113.31409, 0.999974668, 0, -0.00714713801, 0, 1.00000012, 0, 0.00714714266, 0, 0.999974549)
    elseif SelectBoss == "Wysper [Lv. 500] [Boss]" then
        MsBoss = "Wysper [Lv. 500] [Boss]"
        NameQuestBoss = "SkyExp1Quest"
        LevelQuestBoss = 3
        NameBoss = "Wysper"
        CFrameQuestBoss = CFrame.new(-7862.94629, 5545.52832, -379.833954, 0.462944925, 1.45838088e-08, -0.886386991, 1.0534996e-08, 1, 2.19553424e-08, 0.886386991, -1.95022007e-08, 0.462944925)
        CFrameBoss = CFrame.new(-7925.48389, 5550.76074, -636.178345, 0.716468513, -1.22915289e-09, 0.697619379, 3.37381434e-09, 1, -1.70304748e-09, -0.697619379, 3.57381835e-09, 0.716468513)
    elseif SelectBoss == "Thunder God [Lv. 575] [Boss]" then
        MsBoss = "Thunder God [Lv. 575] [Boss]"
        NameQuestBoss = "SkyExp2Quest"
        LevelQuestBoss = 3
        NameBoss = "Thunder God"
        CFrameQuestBoss = CFrame.new(-7902.78613, 5635.99902, -1411.98706, -0.0361216255, -1.16895912e-07, 0.999347389, 1.44533963e-09, 1, 1.17024491e-07, -0.999347389, 5.6715117e-09, -0.0361216255)
        CFrameBoss = CFrame.new(-7917.53613, 5616.61377, -2277.78564, 0.965189934, 4.80563429e-08, -0.261550069, -6.73089886e-08, 1, -6.46515304e-08, 0.261550069, 8.00056768e-08, 0.965189934)
    elseif SelectBoss == "Cyborg [Lv. 675] [Boss]" then
        MsBoss = "Cyborg [Lv. 675] [Boss]"
        NameQuestBoss = "FountainQuest"
        LevelQuestBoss = 3
        NameBoss = "Cyborg"
        CFrameQuestBoss = CFrame.new(5253.54834, 38.5361786, 4050.45166, -0.0112687312, -9.93677887e-08, -0.999936521, 2.55291371e-10, 1, -9.93769547e-08, 0.999936521, -1.37512213e-09, -0.0112687312)
        CFrameBoss = CFrame.new(6041.82813, 52.7112198, 3907.45142, -0.563162148, 1.73805248e-09, -0.826346457, -5.94632716e-08, 1, 4.26280238e-08, 0.826346457, 7.31437524e-08, -0.563162148)
    
        -- New World
    elseif SelectBoss == "Don Swan [Lv. 1000] [Boss]" then
        MsBoss = "Don Swan [Lv. 1000] [Boss]"
        NameQuestBoss = ""
        LevelQuestBoss = 3
        NameBoss = "Don Swan"
        CFrameBoss = CFrame.new(2288.802, 15.1870775, 863.034607, 0.99974072, -8.41247214e-08, -0.0227668174, 8.4774733e-08, 1, 2.75850098e-08, 0.0227668174, -2.95079072e-08, 0.99974072)
    
    elseif SelectBoss == "Diamond [Lv. 750] [Boss]" then
        MsBoss = "Diamond [Lv. 750] [Boss]"
        NameQuestBoss = "Area1Quest"
        LevelQuestBoss = 3
        NameBoss = "Diamond"
        CFrameQuestBoss = CFrame.new(-424.080078, 73.0055847, 1836.91589, 0.253544956, -1.42165932e-08, 0.967323601, -6.00147771e-08, 1, 3.04272909e-08, -0.967323601, -6.5768397e-08, 0.253544956)
        CFrameBoss = CFrame.new(-1736.26587, 198.627731, -236.412857, -0.997808516, 0, -0.0661673471, 0, 1, 0, 0.0661673471, 0, -0.997808516)
    elseif SelectBoss == "Jeremy [Lv. 850] [Boss]" then
        MsBoss = "Jeremy [Lv. 850] [Boss]"
        NameQuestBoss = "Area2Quest"
        LevelQuestBoss = 3
        NameBoss = "Jeremy"
        CFrameQuestBoss = CFrame.new(632.698608, 73.1055908, 918.666321, -0.0319722369, 8.96074881e-10, -0.999488771, 1.36326533e-10, 1, 8.92172336e-10, 0.999488771, -1.07732087e-10, -0.0319722369)
        CFrameBoss = CFrame.new(2203.76953, 448.966034, 752.731079, -0.0217453763, 0, -0.999763548, 0, 1, 0, 0.999763548, 0, -0.0217453763)
    elseif SelectBoss == "Fajita [Lv. 925] [Boss]" then
        MsBoss = "Fajita [Lv. 925] [Boss]"
        NameQuestBoss = "MarineQuest3"
        LevelQuestBoss = 3
        NameBoss = "Fajita"
        CFrameQuestBoss = CFrame.new(-2442.65015, 73.0511475, -3219.11523, -0.873540044, 4.2329841e-08, -0.486752301, 5.64383384e-08, 1, -1.43220786e-08, 0.486752301, -3.99823996e-08, -0.873540044)
        CFrameBoss = CFrame.new(-2297.40332, 115.449463, -3946.53833, 0.961227536, -1.46645796e-09, -0.275756449, -2.3212845e-09, 1, -1.34094433e-08, 0.275756449, 1.35296352e-08, 0.961227536)
    elseif SelectBoss == "Smoke Admiral [Lv. 1150] [Boss]" then
        MsBoss = "Smoke Admiral [Lv. 1150] [Boss]"
        NameQuestBoss = "IceSideQuest"
        LevelQuestBoss = 3
        NameBoss = "Smoke Admiral"
        CFrameQuestBoss = CFrame.new(-6059.96191, 15.9868021, -4904.7373, -0.444992423, -3.0874483e-09, 0.895534337, -3.64098796e-08, 1, -1.4644522e-08, -0.895534337, -3.91229982e-08, -0.444992423)
        CFrameBoss = CFrame.new(-5115.72754, 23.7664986, -5338.2207, 0.251453817, 1.48345061e-08, -0.967869282, 4.02796978e-08, 1, 2.57916977e-08, 0.967869282, -4.54708946e-08, 0.251453817)
    elseif SelectBoss == "Awakened Ice Admiral [Lv. 1400] [Boss]" then
        MsBoss = "Awakened Ice Admiral [Lv. 1400] [Boss]"
        NameQuestBoss = "FrostQuest"
        LevelQuestBoss = 3
        NameBoss = "Awakened Ice Admiral"
        CFrameQuestBoss = CFrame.new(5669.33203, 28.2118053, -6481.55908, 0.921275556, -1.25320829e-08, 0.388910472, 4.72230788e-08, 1, -7.96414241e-08, -0.388910472, 9.17372489e-08, 0.921275556)
        CFrameBoss = CFrame.new(6407.33936, 340.223785, -6892.521, 0.49051559, -5.25310213e-08, -0.871432424, -2.76146022e-08, 1, -7.58250565e-08, 0.871432424, 6.12576301e-08, 0.49051559)
    elseif SelectBoss == "Tide Keeper [Lv. 1475] [Boss]" then
        MsBoss = "Tide Keeper [Lv. 1475] [Boss]"
        NameQuestBoss = "ForgottenQuest"             
        LevelQuestBoss = 3
        NameBoss = "Tide Keeper"
        CFrameQuestBoss = CFrame.new(-3053.89648, 236.881363, -10148.2324, -0.985987961, -3.58504737e-09, 0.16681771, -3.07832915e-09, 1, 3.29612559e-09, -0.16681771, 2.73641976e-09, -0.985987961)
        CFrameBoss = CFrame.new(-3570.18652, 123.328949, -11555.9072, 0.465199202, -1.3857326e-08, 0.885206044, 4.0332897e-09, 1, 1.35347511e-08, -0.885206044, -2.72606271e-09, 0.465199202)
    
    elseif SelectBoss == "Cursed Captain [Lv. 1325] [Raid Boss]" then
        MsBoss = "Cursed Captain [Lv. 1325] [Raid Boss]"
        NameQuestBoss = ""
        LevelQuestBoss = 3
        NameBoss = "Cursed Captain"
        CFrameQuestBoss = CFrame.new(916.928589, 181.092773, 33422)
        CFrameBoss = CFrame.new(916.928589, 181.092773, 33422, -0.999505103, 9.26310495e-09, 0.0314563364, 8.42916226e-09, 1, -2.6643713e-08, -0.0314563364, -2.63653774e-08, -0.999505103)
    elseif SelectBoss == "Darkbeard [Lv. 1000] [Raid Boss]" then
        MsBoss = "Darkbeard [Lv. 1000] [Raid Boss]"
        NameQuestBoss = ""
        LevelQuestBoss = 3
        NameBoss = "Darkbeard"
        CFrameQuestBoss = CFrame.new(3876.00366, 24.6882591, -3820.21777)
        CFrameBoss = CFrame.new(3876.00366, 24.6882591, -3820.21777, -0.976951957, 4.97356325e-08, 0.213458836, 4.57335361e-08, 1, -2.36868622e-08, -0.213458836, -1.33787044e-08, -0.976951957)
    elseif SelectBoss == "Order [Lv. 1250] [Raid Boss]" then
        MsBoss = "Order [Lv. 1250] [Raid Boss]"
        NameQuestBoss = ""
        LevelQuestBoss = 3
        NameBoss = "Order"
        CFrameQuestBoss = CFrame.new(-6221.15039, 16.2351036, -5045.23584)
        CFrameBoss = CFrame.new(-6221.15039, 16.2351036, -5045.23584, -0.380726993, 7.41463495e-08, 0.924687505, 5.85604774e-08, 1, -5.60738549e-08, -0.924687505, 3.28013137e-08, -0.380726993)
    
        -- Thire World
    elseif SelectBoss == "Stone [Lv. 1550] [Boss]" then
        MsBoss = "Stone [Lv. 1550] [Boss]"
        NameQuestBoss = "PiratePortQuest"             
        LevelQuestBoss = 3
        NameBoss = "Stone"
        CFrameQuestBoss = CFrame.new(-290, 44, 5577)
        CFrameBoss = CFrame.new(-1085, 40, 6779)
    elseif SelectBoss == "Island Empress [Lv. 1675] [Boss]" then
        MsBoss = "Island Empress [Lv. 1675] [Boss]"
        NameQuestBoss = "AmazonQuest2"             
        LevelQuestBoss = 3
        NameBoss = "Island Empress"
        CFrameQuestBoss = CFrame.new(5443, 602, 752)
        CFrameBoss = CFrame.new(5659, 602, 244)
    elseif SelectBoss == "Kilo Admiral [Lv. 1750] [Boss]" then
        MsBoss = "Kilo Admiral [Lv. 1750] [Boss]"
        NameQuestBoss = "MarineTreeIsland"             
        LevelQuestBoss = 3
        NameBoss = "Kilo Admiral"
        CFrameQuestBoss = CFrame.new(2178, 29, -6737)
        CFrameBoss =CFrame.new(2846, 433, -7100)
    elseif SelectBoss == "Captain Elephant [Lv. 1875] [Boss]" then
        MsBoss = "Captain Elephant [Lv. 1875] [Boss]"
        NameQuestBoss = "DeepForestIsland"             
        LevelQuestBoss = 3
        NameBoss = "Captain Elephant"
        CFrameQuestBoss = CFrame.new(-13232, 333, -7631)
        CFrameBoss = CFrame.new(-13221, 325, -8405)
    elseif SelectBoss == "Beautiful Pirate [Lv. 1950] [Boss]" then
        MsBoss = "Beautiful Pirate [Lv. 1950] [Boss]"
        NameQuestBoss = "DeepForestIsland2"             
        LevelQuestBoss = 3
        NameBoss = "Beautiful Pirate"
        CFrameQuestBoss = CFrame.new(-12686, 391, -9902)
        CFrameBoss = CFrame.new(5182, 23, -20)
    elseif SelectBoss == "Cake Queen [Lv. 2175] [Boss]" then
        MsBoss = "Cake Queen [Lv. 2175] [Boss]"
        NameQuestBoss = "IceCreamIslandQuest"             
        LevelQuestBoss = 3
        NameBoss = "Cake Queen"
        CFrameQuestBoss = CFrame.new(-716, 382, -11010)
        CFrameBoss = CFrame.new(-821, 66, -10965)

    elseif SelectBoss == "rip_indra True Form [Lv. 5000] [Raid Boss]" then
        MsBoss = "rip_indra True Form [Lv. 5000] [Raid Boss]"
        LevelQuestBoss = 3
        NameQuestBoss = ""
        NameBoss = "rip_indra True Form"
        CFrameQuestBoss = CFrame.new(-5359, 424, -2735)
        CFrameBoss = CFrame.new(-5359, 424, -2735)
    elseif SelectBoss == "Longma [Lv. 2000] [Boss]" then
        MsBoss = "Longma [Lv. 2000] [Boss]"

        LevelQuestBoss = 3
        NameQuestBoss = ""
        NameBoss = "Longma"

        CFrameQuestBoss = CFrame.new(-10248.3936, 353.79129, -9306.34473)
        CFrameBoss = CFrame.new(-10248.3936, 353.79129, -9306.34473)
    elseif SelectBoss == "Soul Reaper [Lv. 2100] [Raid Boss]" then
        MsBoss = "Soul Reaper [Lv. 2100] [Raid Boss]"
        LevelQuestBoss = 3
        NameQuestBoss = ""
        NameBoss = "Soul Reaper"
        CFrameQuestBoss = CFrame.new(-9515.62109, 315.925537, 6691.12012)
        CFrameBoss = CFrame.new(-9515.62109, 315.925537, 6691.12012)
    end
end
CheckQuestBoss()

do -- Init
    task = task or getrenv().task;
    fastSpawn,fastWait,delay = task.spawn,task.wait,task.delay
end

function SlowtoTarget(CFgo)

    local tween_s = game:service"TweenService"
    local info = TweenInfo.new((game:GetService("Players")["LocalPlayer"].Character.HumanoidRootPart.Position - CFgo.Position).Magnitude/250, Enum.EasingStyle.Linear)
    local tween = tween_s:Create(game.Players.LocalPlayer.Character["HumanoidRootPart"], info, {CFrame = CFgo})
    tween:Play()

end

function MytoTarget(CFgo)
    local tweenfunc = {}
    if (game:GetService("Players")["LocalPlayer"].Character.HumanoidRootPart.Position - CFgo.Position).Magnitude <= 20 then
        pcall(function()
            tween:Cancel()

            game:GetService("Players")["LocalPlayer"].Character.HumanoidRootPart.CFrame = CFgo

            return
        end)
    end
    local tween_s = game:service"TweenService"
    local info = TweenInfo.new((game:GetService("Players")["LocalPlayer"].Character.HumanoidRootPart.Position - CFgo.Position).Magnitude/275, Enum.EasingStyle.Linear)
    local tween = tween_s:Create(game.Players.LocalPlayer.Character["HumanoidRootPart"], info, {CFrame = CFgo})
    tween:Play()

    function tweenfunc:Stop()
        tween:Cancel()
    end 

    if not tween then return tween end
    return tweenfunc
end

function toTarget(targetPos, targetCFrame)
    if FastTween then
        Distance = (targetPos - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).Magnitude
        if Distance < 1000 then
            Speed = 325
        elseif Distance >= 1000 then
            Speed = 300
        end
    else
        Distance = (targetPos - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).Magnitude
        if Distance < 1000 then
            Speed = 275
        elseif Distance >= 1000 then
            Speed = 250
        end
    end
    local tweenfunc = {}

    local tween_s = game:service"TweenService"
    local info = TweenInfo.new((targetPos - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).Magnitude/Speed, Enum.EasingStyle.Linear)
    local tween = tween_s:Create(game:GetService("Players").LocalPlayer.Character["HumanoidRootPart"], info, {CFrame = targetCFrame * CFrame.fromAxisAngle(Vector3.new(1,0,0), math.rad(0))})
    tween:Play()

    function tweenfunc:Stop()
        tween:Cancel()
    end 

    if StatsBypass == "Bypassed" and UseTP then
        tween:Cancel()
        game:GetService("Players").LocalPlayer.Character["HumanoidRootPart"].CFrame = targetCFrame
    end
    if not tween then return tween end
    return tweenfunc
end

game.Players.LocalPlayer.CharacterAdded:Connect(function()
    StatsBypass = "NoBypassTP"
end)
spawn(function()
    while wait() do
        pcall(function()
            if game:GetService("Players").LocalPlayer.Character:FindFirstChild("HasBuso") then
                if StatsBypass == "Bypassing" or StatsBypass == "Bypassed" then
                    game.Players.LocalPlayer.Character.Humanoid:SetStateEnabled(15, false)
                else
                    game.Players.LocalPlayer.Character.Humanoid:SetStateEnabled(15, true)
                end
            end
        end)
    end
end)

function Click()
    local VirtualUser = game:GetService('VirtualUser')
    VirtualUser:CaptureController()
    VirtualUser:ClickButton1(Vector2.new(851, 158), game:GetService("Workspace").Camera.CFrame)
end

function EquipWeapon(ToolSe)
    if game.Players.LocalPlayer.Backpack:FindFirstChild(ToolSe) then
        local tool = game.Players.LocalPlayer.Backpack:FindFirstChild(ToolSe)
        wait(.4)
        game.Players.LocalPlayer.Character.Humanoid:EquipTool(tool)
    end
end      

spawn(function()
    while wait() do
        for i ,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
            if v:IsA("Tool") then
                if v.ToolTip == "Sword" then
                    SelectToolWeaponSword = v.Name
                end
            end
        end
        for i ,v in pairs(game.Players.LocalPlayer.Character:GetChildren()) do
            if v:IsA("Tool") then
                if v.ToolTip == "Sword" then
                    SelectToolWeaponSword = v.Name
                end
            end
        end
    end
end)

-- Get Weapon Gun
spawn(function()
    while wait() do
        for i,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do  
            if v:IsA("Tool") then
                if v:FindFirstChild("RemoteFunctionShoot") then 
                    SelectToolWeaponGun = v.Name
                end
            end
        end
        for i,v in pairs(game.Players.LocalPlayer.Character:GetChildren()) do  
            if v:IsA("Tool") then
                if v:FindFirstChild("RemoteFunctionShoot") then 
                    SelectToolWeaponGun = v.Name
                end
            end
        end
    end
end)

spawn(function()
    while wait() do
        if sethiddenproperty then
            sethiddenproperty(game.Players.LocalPlayer,"SimulationRadius",99999999999)
        end 
        if setscriptable then
            setscriptable(game.Players.LocalPlayer, "SimulationRadius", true)
            game.Players.LocalPlayer.SimulationRadius = math.huge * math.huge, math.huge * math.huge * 1 / 0 * 1 / 0 * 1 / 0 * 1 / 0 * 1 / 0
        end
    end
end)

function TP(P)
    NoClip = true
    Distance = (P.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).Magnitude
    if Distance < 10 then
        Speed = 1000
    elseif Distance < 170 then
        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = P
        Speed = 350
    elseif Distance < 1000 then
        Speed = 350
    elseif Distance >= 1000 then
        Speed = 250
    end
    game:GetService("TweenService"):Create(
        game.Players.LocalPlayer.Character.HumanoidRootPart,
        TweenInfo.new(Distance/Speed, Enum.EasingStyle.Linear),
        {CFrame = P}
    ):Play()
    NoClip = false
end

local CameraShakeInstanceSet = require(game.Players.LocalPlayer.PlayerScripts.CombatFramework.CameraShaker.CameraShakeInstance)
function AutoFarm(NameMonster,RemoteQuestGet,LevelQuestGet,TextQuestName,WaitMonSpawnCFrame,NPCQuestCFrame,FarmMode)
    local AutoFarmfunc = {}

    function AutoFarmfunc:Update(NewNameMonster,NewRemoteQuestGet,NewLevelQuestGet,NewTextQuestName,NewWaitMonSpawnCFrame,NewNPCQuestCFrame)
        NameMonster = NewNameMonster
        RemoteQuestGet = NewRemoteQuestGet
        LevelQuestGet = NewLevelQuestGet
        TextQuestName = NewTextQuestName
        WaitMonSpawnCFrame = NewWaitMonSpawnCFrame
        NPCQuestCFrame = NewNPCQuestCFrame
    end
    function AutoFarmfunc:UpdateFarmMode(NewFarmMode)
        FarmMode = NewFarmMode
    end
    function AutoFarmfunc:Start()
        farm = true
    end
    function AutoFarmfunc:Stop()
        farm = false
    end

    spawn(function()
        while true do
            if farm then
                if FarmMode == "AutoFarmLevel" then
                    if game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Visible == false and Nonquest == false then
                        Usefastattack = false
                        StartMagnetAutoFarmLevel= false
                        Questtween = toTarget(NPCQuestCFrame.Position,NPCQuestCFrame)
                        if OldWorld and (Ms == "Fishman Commando [Lv. 400]" or Ms == "Fishman Warrior [Lv. 375]") and (CFrameQuest.Position - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).magnitude > 50000 then
                            if Questtween then Questtween:Stop() end wait(.5)
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(61163.8515625, 11.6796875, 1819.7841796875))
                        elseif OldWorld and not (Ms == "Fishman Commando [Lv. 400]" or Ms == "Fishman Warrior [Lv. 375]") and (CFrameQuest.Position - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).magnitude > 50000 then
                            if Questtween then Questtween:Stop() end wait(.5)
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(3864.8515625, 6.6796875, -1926.7841796875))
                        elseif NewWorld and string.find(Ms, "Ship") and (CFrameQuest.Position - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).magnitude > 30000 then
                            if Questtween then Questtween:Stop() end
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(923.21252441406, 126.9760055542, 32852.83203125))
                        elseif NewWorld and not string.find(Ms, "Ship") and (CFrameQuest.Position - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).magnitude > 30000 then
                            if Questtween then Questtween:Stop() end
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-6508.5581054688, 89.034996032715, -132.83953857422))
                        elseif (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 100 then
                            if Questtween then Questtween:Stop() end
                            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrameQuest
                            wait(.9)
                            local string_1 = "StartQuest";
                            local string_2 = NameQuest;
                            local number_1 = LevelQuest;
                            local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
                            Target:InvokeServer(string_1, string_2, number_1);
                            local string_1 = "SetSpawnPoint";
                            local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
                            Target:InvokeServer(string_1);
                        end
                    elseif game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Visible == true or Nonquest == true then
                        if Nonquest == true then
                            local string_1 = "SetSpawnPoint";
                            local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
                            Target:InvokeServer(string_1);
                        end
                        if game:GetService("Workspace").Enemies:FindFirstChild(Ms) then
                            for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                                if farm and v.Name == Ms and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 then
                                    if string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, NameMon) or Nonquest == true then
                                        repeat wait()
                                            pcall(function()
                                                if game.Players.LocalPlayer.Character.Humanoid.Health > 0 then
                                                    Farmtween = toTarget(v.HumanoidRootPart.Position,v.HumanoidRootPart.CFrame * CFrame.new(0,30,0))
                                                    if v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 350 then
                                                        EquipWeapon(SelectToolWeapon)
                                                        if Farmtween then Farmtween:Stop() end
                                                        PosMon = v.HumanoidRootPart.CFrame
                                                        StartMagnetAutoFarmLevel = true
                                                        Usefastattack = true
                                                        if not game.Players.LocalPlayer.Character:FindFirstChild("HasBuso") then
                                                            local args = {
                                                                [1] = "Buso"
                                                            }
                                                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
                                                        end
                                                        if game.Players.LocalPlayer.Character:FindFirstChild("Black Leg") and game.Players.LocalPlayer.Character:FindFirstChild("Black Leg").Level.Value >= 150 then
                                                            local vim = game:service('VirtualInputManager')
                                                            vim:SendKeyEvent(true, "V", false, game)
                                                            vim:SendKeyEvent(false, "V", false, game)
                                                        end
                                                        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 1)
                                                        Click()
                                                    end
                                                end
                                            end)
                                        until (not farm or not v.Parent or v.Humanoid.Health <= 0) or (not string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, NameMon) and Nonquest == false) or (game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Visible == false and Nonquest == false)
                                        if not string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, NameMon) and Nonquest == false then
                                            game.ReplicatedStorage:WaitForChild("Remotes").CommF_:InvokeServer("AbandonQuest");
                                        end
                                        Usefastattack = false
                                        StartMagnetAutoFarmLevel= false
                                    else
                                        game.ReplicatedStorage:WaitForChild("Remotes").CommF_:InvokeServer("AbandonQuest");
                                    end 
                                end
                            end
                        else
                            if not string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, NameMon) and Nonquest == false then
                                game.ReplicatedStorage:WaitForChild("Remotes").CommF_:InvokeServer("AbandonQuest");
                            end
                            Usefastattack = false
                            StartMagnetAutoFarmLevel= false
                            Modstween = toTarget(CFrameMon.Position,CFrameMon)
                            if OldWorld and (Ms == "Fishman Commando [Lv. 400]" or Ms == "Fishman Warrior [Lv. 375]") and (CFrameQuest.Position - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).magnitude > 50000 then
                                if Modstween then Modstween:Stop() end wait(.5)
                                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(61163.8515625, 11.6796875, 1819.7841796875))
                            elseif OldWorld and not (Ms == "Fishman Commando [Lv. 400]" or Ms == "Fishman Warrior [Lv. 375]") and (CFrameQuest.Position - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).magnitude > 50000 then
                                if Modstween then Modstween:Stop() end wait(.5)
                                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(3864.8515625, 6.6796875, -1926.7841796875))
                            elseif NewWorld and string.find(Ms, "Ship") and (CFrameQuest.Position - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).magnitude > 30000 then
                                if Modstween then Modstween:Stop() end wait(.5)
                                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(923.21252441406, 126.9760055542, 32852.83203125))
                            elseif NewWorld and not string.find(Ms, "Ship") and (CFrameQuest.Position - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).magnitude > 30000 then
                                if Modstween then Modstween:Stop() end wait(.5)
                                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-6508.5581054688, 89.034996032715, -132.83953857422))
                            elseif (CFrameMon.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 350 then
                                if Modstween then Modstween:Stop() end wait(.5)
                                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrameMon
                            end
                        end
                    end
                elseif FarmMode == "AutoFarmGun" then
                    if game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Visible == false then
                        Usefastattack = false
                        StartMagnetAutoFarmLevel= false
                        Questtween = toTarget(NPCQuestCFrame.Position,NPCQuestCFrame) wait(.1)
                        if OldWorld and (Ms == "Fishman Commando [Lv. 400]" or Ms == "Fishman Warrior [Lv. 375]") and (CFrameQuest.Position - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).magnitude > 50000 then
                            if Questtween then Questtween:Stop() end wait(.5)
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(61163.8515625, 11.6796875, 1819.7841796875))
                        elseif OldWorld and not (Ms == "Fishman Commando [Lv. 400]" or Ms == "Fishman Warrior [Lv. 375]") and (CFrameQuest.Position - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).magnitude > 50000 then
                            if Questtween then Questtween:Stop() end wait(.5)
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(3864.8515625, 6.6796875, -1926.7841796875))
                        elseif NewWorld and string.find(Ms, "Ship") and (CFrameQuest.Position - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).magnitude > 30000 then
                            if Questtween then Questtween:Stop() end
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(923.21252441406, 126.9760055542, 32852.83203125))
                        elseif NewWorld and not string.find(Ms, "Ship") and (CFrameQuest.Position - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).magnitude > 30000 then
                            if Questtween then Questtween:Stop() end
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-6508.5581054688, 89.034996032715, -132.83953857422))
                        elseif (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 350 then
                            if Questtween then Questtween:Stop() end
                            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrameQuest
                            wait(1)
                            local string_1 = "StartQuest";
                            local string_2 = NameQuest;
                            local number_1 = LevelQuest;
                            local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
                            Target:InvokeServer(string_1, string_2, number_1);
                            local string_1 = "SetSpawnPoint";
                            local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
                            Target:InvokeServer(string_1);
                        end
                    elseif game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Visible == true then
                        if game:GetService("Workspace").Enemies:FindFirstChild(Ms) then
                            for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                                if farm and v.Name == Ms and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 then
                                    if string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, NameMon) then
                                        repeat wait()
                                            Farmtween = toTarget(v.HumanoidRootPart.Position,v.HumanoidRootPart.CFrame * CFrame.new(0,30,0))
                                            if v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 350 then
                                                EquipWeapon(SelectToolWeapon)
                                                if Farmtween then Farmtween:Stop() end
                                                if Modstween then Modstween:Stop() end
                                                PosMon = v.HumanoidRootPart.CFrame
                                                StartMagnetAutoFarmLevel= true
                                                Usefastattack = true
                                                if not game.Players.LocalPlayer.Character:FindFirstChild("HasBuso") then
                                                    local args = {
                                                        [1] = "Buso"
                                                    }
                                                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
                                                end
                                                HealthMin = v.Humanoid.MaxHealth*Persen/100
                                                PosMonGun = v.HumanoidRootPart.CFrame
                                                if v.Humanoid.Health <= HealthMin and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 then
                                                    EquipWeapon(SelectToolWeaponGun)
                                                    -- v.HumanoidRootPart.CanCollide = false
                                                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0)
                                                    if game:GetService("Players").LocalPlayer.Character:FindFirstChild(SelectToolWeaponGun) and game:GetService("Players").LocalPlayer.Character:FindFirstChild(SelectToolWeaponGun):FindFirstChild("RemoteFunctionShoot") then
                                                        tool = game:GetService("Players").LocalPlayer.Character[SelectToolWeaponGun]
                                                        v17 = workspace:FindPartOnRayWithIgnoreList(Ray.new(tool.Handle.CFrame.p, (v.HumanoidRootPart.Position - tool.Handle.CFrame.p).unit * 100), { game.Players.LocalPlayer.Character, workspace._WorldOrigin });
                                                        game:GetService("Players").LocalPlayer.Character:FindFirstChild(SelectToolWeaponGun).RemoteFunctionShoot:InvokeServer(v.HumanoidRootPart.Position, (ReplicatedStorage_Util.Other.hrpFromPart(v17)));
                                                    end 
                                                else
                                                    EquipWeapon(SelectToolWeapon)
                                                    Usefastattack = true
                                                    PosMonGun = v.HumanoidRootPart.CFrame
                                                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 30)
                                                    Click()
                                                    StartMagnetAutoFarmLevel = true
                                                end
                                            end
                                        until not farm or not v.Parent or v.Humanoid.Health <= 0 or not string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, NameMon) or game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Visible == false
                                        if not string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, NameMon) then
                                            game.ReplicatedStorage:WaitForChild("Remotes").CommF_:InvokeServer("AbandonQuest");
                                        end
                                        Usefastattack = false
                                        StartMagnetAutoFarmLevel= false
                                    else
                                        game.ReplicatedStorage:WaitForChild("Remotes").CommF_:InvokeServer("AbandonQuest");
                                    end 
                                end
                            end
                        else
                            if not string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, NameMon) then
                                game.ReplicatedStorage:WaitForChild("Remotes").CommF_:InvokeServer("AbandonQuest");
                            end
                            Usefastattack = false
                            StartMagnetAutoFarmLevel= false
                            Modstween = toTarget(CFrameMon.Position,CFrameMon)
                            if OldWorld and (Ms == "Fishman Commando [Lv. 400]" or Ms == "Fishman Warrior [Lv. 375]") and (CFrameQuest.Position - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).magnitude > 50000 then
                                if Modstween then Modstween:Stop() end wait(.5)
                                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(61163.8515625, 11.6796875, 1819.7841796875))
                            elseif OldWorld and not (Ms == "Fishman Commando [Lv. 400]" or Ms == "Fishman Warrior [Lv. 375]") and (CFrameQuest.Position - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).magnitude > 50000 then
                                if Modstween then Modstween:Stop() end wait(.5)
                                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(3864.8515625, 6.6796875, -1926.7841796875))
                            elseif NewWorld and string.find(Ms, "Ship") and (CFrameQuest.Position - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).magnitude > 30000 then
                                if Modstween then Modstween:Stop() end wait(.5)
                                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(923.21252441406, 126.9760055542, 32852.83203125))
                            elseif NewWorld and not string.find(Ms, "Ship") and (CFrameQuest.Position - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).magnitude > 30000 then
                                if Modstween then Modstween:Stop() end wait(.5)
                                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-6508.5581054688, 89.034996032715, -132.83953857422))
                            elseif (CFrameMon.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 350 then
                                if Modstween then Modstween:Stop() end wait(.5)
                                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrameMon
                            end 
                        end
                    end
                elseif FarmMode == "AutoFarmDevilfruit" then
                    if game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Visible == false then
                        Usefastattack = false
                        StartMagnetAutoFarmLevel= false
                        Questtween = toTarget(NPCQuestCFrame.Position,NPCQuestCFrame) wait(.1)
                        if OldWorld and (Ms == "Fishman Commando [Lv. 400]" or Ms == "Fishman Warrior [Lv. 375]") and (CFrameQuest.Position - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).magnitude > 50000 then
                            if Questtween then Questtween:Stop() end wait(.5)
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(61163.8515625, 11.6796875, 1819.7841796875))
                        elseif OldWorld and not (Ms == "Fishman Commando [Lv. 400]" or Ms == "Fishman Warrior [Lv. 375]") and (CFrameQuest.Position - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).magnitude > 50000 then
                            if Questtween then Questtween:Stop() end wait(.5)
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(3864.8515625, 6.6796875, -1926.7841796875))
                        elseif NewWorld and string.find(Ms, "Ship") and (CFrameQuest.Position - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).magnitude > 30000 then
                            if Questtween then Questtween:Stop() end
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(923.21252441406, 126.9760055542, 32852.83203125))
                        elseif NewWorld and not string.find(Ms, "Ship") and (CFrameQuest.Position - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).magnitude > 30000 then
                            if Questtween then Questtween:Stop() end
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-6508.5581054688, 89.034996032715, -132.83953857422))
                        elseif (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 350 then
                            if Questtween then Questtween:Stop() end
                            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrameQuest
                            wait(1)
                            local string_1 = "StartQuest";
                            local string_2 = NameQuest;
                            local number_1 = LevelQuest;
                            local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
                            Target:InvokeServer(string_1, string_2, number_1);
                            local string_1 = "SetSpawnPoint";
                            local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
                            Target:InvokeServer(string_1);
                        end
                    elseif game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Visible == true then
                        if game:GetService("Workspace").Enemies:FindFirstChild(Ms) then
                            for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                                if farm and v.Name == Ms and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 then
                                    if string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, NameMon) then
                                        repeat wait()
                                            Farmtween = toTarget(v.HumanoidRootPart.Position,v.HumanoidRootPart.CFrame * CFrame.new(0, 40, 1))
                                            if game:GetService("Workspace").Enemies:FindFirstChild(Ms) then
                                                if v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 350 then
                                                    if Farmtween then Farmtween:Stop() end
                                                    StartMagnetAutoFarmLevel= true
                                                    if not game.Players.LocalPlayer.Character:FindFirstChild("HasBuso") then
                                                        local args = {
                                                            [1] = "Buso"
                                                        }
                                                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
                                                    end
                                                    HealthMin = v.Humanoid.MaxHealth*Persen/100
                                                    PosMon = v.HumanoidRootPart.CFrame
                                                    if v.Humanoid.Health <= HealthMin and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 then
                                                        EquipWeapon(game.Players.LocalPlayer.Data.DevilFruit.Value)
                                                        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame * CFrame.new(0, 40, 1)
                                                        DevilFruitMastery = game:GetService("Players").LocalPlayer.Character[game.Players.LocalPlayer.Data.DevilFruit.Value].Level.Value
                                                        PositionSkillMasteryDevilFruit = v.HumanoidRootPart.Position
                                                        UseSkillMasteryDevilFruit = true
                                                        if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Dragon-Dragon") then
                                                            if SkillZ and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 and DevilFruitMastery >= 1 then
                                                                game:service('VirtualInputManager'):SendKeyEvent(true, "Z", false, game)
                                                                wait(.1)
                                                                game:service('VirtualInputManager'):SendKeyEvent(false, "Z", false, game)
                                                            end
                                                            if SkillX and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 and DevilFruitMastery >= 1 then
                                                                game:service('VirtualInputManager'):SendKeyEvent(true, "X", false, game)
                                                                wait(.1)
                                                                game:service('VirtualInputManager'):SendKeyEvent(false, "X", false, game)
                                                            end   
                                                        elseif game:GetService("Players").LocalPlayer.Character:FindFirstChild("Human-Human: Buddha") then
                                                            if SkillZ and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 and DevilFruitMastery >= 1 and game.Players.LocalPlayer.Character.HumanoidRootPart.Size == Vector3.new(7.6, 7.676, 3.686) then
                                                            else
                                                                game:service('VirtualInputManager'):SendKeyEvent(true, "Z", false, game)
                                                                wait(.1)
                                                                game:service('VirtualInputManager'):SendKeyEvent(false, "Z", false, game)
                                                            end
                                                            if SkillX and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 and DevilFruitMastery >= 1 then
                                                                game:service('VirtualInputManager'):SendKeyEvent(true, "X", false, game)
                                                                wait(.1)
                                                                game:service('VirtualInputManager'):SendKeyEvent(false, "X", false, game)
                                                            end
                                                            if SkillC and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 and DevilFruitMastery >= 1 then
                                                                game:service('VirtualInputManager'):SendKeyEvent(true, "C", false, game)
                                                                wait(.1)
                                                                game:service('VirtualInputManager'):SendKeyEvent(false, "C", false, game)
                                                            end  
                                                        elseif game:GetService("Players").LocalPlayer.Character:FindFirstChild(game.Players.LocalPlayer.Data.DevilFruit.Value) then
                                                            game:GetService("Players").LocalPlayer.Character:FindFirstChild(game.Players.LocalPlayer.Data.DevilFruit.Value).MousePos.Value = v.HumanoidRootPart.Position
                                                            if SkillZ and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 and DevilFruitMastery >= 1 then
                                                                game:service('VirtualInputManager'):SendKeyEvent(true, "Z", false, game)
                                                                wait(.1)
                                                                game:service('VirtualInputManager'):SendKeyEvent(false, "Z", false, game)
                                                            end
                                                            if SkillX and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 and DevilFruitMastery >= 1 then
                                                                game:service('VirtualInputManager'):SendKeyEvent(true, "X", false, game)
                                                                wait(.1)
                                                                game:service('VirtualInputManager'):SendKeyEvent(false, "X", false, game)
                                                            end
                                                            if SkillC and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 and DevilFruitMastery >= 1 then
                                                                game:service('VirtualInputManager'):SendKeyEvent(true, "C", false, game)
                                                                wait(.1)
                                                                game:service('VirtualInputManager'):SendKeyEvent(false, "C", false, game)
                                                            end
                                                            if SkillV and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 and DevilFruitMastery >= 1 then
                                                                game:service('VirtualInputManager'):SendKeyEvent(true, "V", false, game)
                                                                wait(.1)
                                                                game:service('VirtualInputManager'):SendKeyEvent(false, "V", false, game)
                                                            end
                                                        end
                                                    else
                                                        UseSkillMasteryDevilFruit = false
                                                        EquipWeapon(SelectToolWeapon)
                                                        Click()
                                                        if not game.Players.LocalPlayer.Character:FindFirstChild("HasBuso") then
                                                            local args = {
                                                                [1] = "Buso"
                                                            }
                                                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
                                                        end
                                                        PosMon = v.HumanoidRootPart.CFrame
                                                        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame * CFrame.new(0, 40, 1)
                                                        StartMagnetAutoFarmLevel = true
                                                    end
                                                end
                                            else
                                                if not string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, NameMon) then
                                                    game.ReplicatedStorage:WaitForChild("Remotes").CommF_:InvokeServer("AbandonQuest");
                                                end
                                                StartMagnetAutoFarmLevel= false
                                                Modstween = toTarget(CFrameMon.Position,CFrameMon)
                                                if OldWorld and (Ms == "Fishman Commando [Lv. 400]" or Ms == "Fishman Warrior [Lv. 375]") and (CFrameQuest.Position - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).magnitude > 50000 then
                                                    if Modstween then Modstween:Stop() end wait(.5)
                                                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(61163.8515625, 11.6796875, 1819.7841796875))
                                                elseif OldWorld and not (Ms == "Fishman Commando [Lv. 400]" or Ms == "Fishman Warrior [Lv. 375]") and (CFrameQuest.Position - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).magnitude > 50000 then
                                                    if Modstween then Modstween:Stop() end wait(.5)
                                                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(3864.8515625, 6.6796875, -1926.7841796875))
                                                elseif NewWorld and string.find(Ms, "Ship") and (CFrameQuest.Position - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).magnitude > 30000 then
                                                    if Modstween then Modstween:Stop() end wait(.5)
                                                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(923.21252441406, 126.9760055542, 32852.83203125))
                                                elseif NewWorld and not string.find(Ms, "Ship") and (CFrameQuest.Position - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).magnitude > 30000 then
                                                    if Modstween then Modstween:Stop() end wait(.5)
                                                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-6508.5581054688, 89.034996032715, -132.83953857422))
                                                elseif (CFrameMon.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 350 then
                                                    if Modstween then Modstween:Stop() end wait(.5)
                                                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrameMon
                                                end 
                                            end
                                        until not farm or not v.Parent or v.Humanoid.Health <= 0 or not string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, NameMon) or game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Visible == false
                                        if not string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, NameMon) then
                                            game.ReplicatedStorage:WaitForChild("Remotes").CommF_:InvokeServer("AbandonQuest");
                                        end
                                        StartMagnetAutoFarmLevel= false
                                    else
                                        game.ReplicatedStorage:WaitForChild("Remotes").CommF_:InvokeServer("AbandonQuest");
                                    end 
                                end
                            end
                        else
                            if not string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, NameMon) then
                                game.ReplicatedStorage:WaitForChild("Remotes").CommF_:InvokeServer("AbandonQuest");
                            end
                            StartMagnetAutoFarmLevel= false
                            Modstween = toTarget(CFrameMon.Position,CFrameMon)
                            if OldWorld and (Ms == "Fishman Commando [Lv. 400]" or Ms == "Fishman Warrior [Lv. 375]") and (CFrameQuest.Position - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).magnitude > 50000 then
                                if Modstween then Modstween:Stop() end wait(.5)
                                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(61163.8515625, 11.6796875, 1819.7841796875))
                            elseif OldWorld and not (Ms == "Fishman Commando [Lv. 400]" or Ms == "Fishman Warrior [Lv. 375]") and (CFrameQuest.Position - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).magnitude > 50000 then
                                if Modstween then Modstween:Stop() end wait(.5)
                                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(3864.8515625, 6.6796875, -1926.7841796875))
                            elseif NewWorld and string.find(Ms, "Ship") and (CFrameQuest.Position - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).magnitude > 30000 then
                                if Modstween then Modstween:Stop() end wait(.5)
                                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(923.21252441406, 126.9760055542, 32852.83203125))
                            elseif NewWorld and not string.find(Ms, "Ship") and (CFrameQuest.Position - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).magnitude > 30000 then
                                if Modstween then Modstween:Stop() end wait(.5)
                                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-6508.5581054688, 89.034996032715, -132.83953857422))
                            elseif (CFrameMon.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 350 then
                                if Modstween then Modstween:Stop() end wait(.5)
                                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrameMon
                            end 
                        end
                    end
                elseif FarmMode == "AutoFarmWeapon" then
                    if game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Visible == false then
                        Usefastattack = false
                        StartMagnetAutoFarmLevel= false
                        Questtween = toTarget(NPCQuestCFrame.Position,NPCQuestCFrame) wait(.1)
                        if OldWorld and (Ms == "Fishman Commando [Lv. 400]" or Ms == "Fishman Warrior [Lv. 375]") and (CFrameQuest.Position - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).magnitude > 50000 then
                            if Questtween then Questtween:Stop() end wait(.5)
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(61163.8515625, 11.6796875, 1819.7841796875))
                        elseif OldWorld and not (Ms == "Fishman Commando [Lv. 400]" or Ms == "Fishman Warrior [Lv. 375]") and (CFrameQuest.Position - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).magnitude > 50000 then
                            if Questtween then Questtween:Stop() end wait(.5)
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(3864.8515625, 6.6796875, -1926.7841796875))
                        elseif NewWorld and string.find(Ms, "Ship") and (CFrameQuest.Position - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).magnitude > 30000 then
                            if Questtween then Questtween:Stop() end
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(923.21252441406, 126.9760055542, 32852.83203125))
                        elseif NewWorld and not string.find(Ms, "Ship") and (CFrameQuest.Position - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).magnitude > 30000 then
                            if Questtween then Questtween:Stop() end
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-6508.5581054688, 89.034996032715, -132.83953857422))
                        elseif (CFrameQuest.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 350 then
                            if Questtween then Questtween:Stop() end
                            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrameQuest
                            wait(1)
                            local string_1 = "StartQuest";
                            local string_2 = NameQuest;
                            local number_1 = LevelQuest;
                            local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
                            Target:InvokeServer(string_1, string_2, number_1);
                            local string_1 = "SetSpawnPoint";
                            local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
                            Target:InvokeServer(string_1);
                        end
                    elseif game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Visible == true then
                        if game:GetService("Workspace").Enemies:FindFirstChild(Ms) then
                            for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                                if farm and v.Name == Ms and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 then
                                    if string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, NameMon) then
                                        repeat wait()
                                            Farmtween = toTarget(v.HumanoidRootPart.Position,v.HumanoidRootPart.CFrame * CFrame.new(0, 40, 1))
                                            if game:GetService("Workspace").Enemies:FindFirstChild(Ms) then
                                                if v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 350 then
                                                    if Farmtween then Farmtween:Stop() end
                                                    StartMagnetAutoFarmLevel= true
                                                    if not game.Players.LocalPlayer.Character:FindFirstChild("HasBuso") then
                                                        local args = {
                                                            [1] = "Buso"
                                                        }
                                                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
                                                    end
                                                    HealthMin = v.Humanoid.MaxHealth*Persen/100
                                                    PosMon = v.HumanoidRootPart.CFrame
                                                    if v.Humanoid.Health <= HealthMin and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 then
                                                        EquipWeapon(SelectToolWeaponSword)
                                                        Click()
                                                        Usefastattack = true
                                                        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame * CFrame.new(0, 40, 1)
                                                        StartMagnetAutoFarmLevel = true
                                                    else
                                                        EquipWeapon(SelectToolWeapon)
                                                        Click()
                                                        if not game.Players.LocalPlayer.Character:FindFirstChild("HasBuso") then
                                                            local args = {
                                                                [1] = "Buso"
                                                            }
                                                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
                                                        end
                                                        PosMon = v.HumanoidRootPart.CFrame
                                                        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame * CFrame.new(0, 40, 1)
                                                        StartMagnetAutoFarmLevel = true
                                                        Usefastattack = false
                                                    end
                                                end
                                            else
                                                if not string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, NameMon) then
                                                    game.ReplicatedStorage:WaitForChild("Remotes").CommF_:InvokeServer("AbandonQuest");
                                                end
                                                Usefastattack = false
                                                StartMagnetAutoFarmLevel= false
                                                Modstween = toTarget(CFrameMon.Position,CFrameMon)
                                                if OldWorld and (Ms == "Fishman Commando [Lv. 400]" or Ms == "Fishman Warrior [Lv. 375]") and (CFrameQuest.Position - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).magnitude > 50000 then
                                                    if Modstween then Modstween:Stop() end wait(.5)
                                                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(61163.8515625, 11.6796875, 1819.7841796875))
                                                elseif OldWorld and not (Ms == "Fishman Commando [Lv. 400]" or Ms == "Fishman Warrior [Lv. 375]") and (CFrameQuest.Position - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).magnitude > 50000 then
                                                    if Modstween then Modstween:Stop() end wait(.5)
                                                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(3864.8515625, 6.6796875, -1926.7841796875))
                                                elseif NewWorld and string.find(Ms, "Ship") and (CFrameQuest.Position - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).magnitude > 30000 then
                                                    if Modstween then Modstween:Stop() end wait(.5)
                                                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(923.21252441406, 126.9760055542, 32852.83203125))
                                                elseif NewWorld and not string.find(Ms, "Ship") and (CFrameQuest.Position - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).magnitude > 30000 then
                                                    if Modstween then Modstween:Stop() end wait(.5)
                                                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-6508.5581054688, 89.034996032715, -132.83953857422))
                                                elseif (CFrameMon.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 350 then
                                                    if Modstween then Modstween:Stop() end wait(.5)
                                                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrameMon
                                                end 
                                            end
                                        until not farm or not v.Parent or v.Humanoid.Health <= 0 or not string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, NameMon) or game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Visible == false
                                        if not string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, NameMon) then
                                            game.ReplicatedStorage:WaitForChild("Remotes").CommF_:InvokeServer("AbandonQuest");
                                        end
                                        StartMagnetAutoFarmLevel= false
                                        Usefastattack = false
                                    else
                                        game.ReplicatedStorage:WaitForChild("Remotes").CommF_:InvokeServer("AbandonQuest");
                                    end 
                                end
                            end
                        else
                            if not string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, NameMon) then
                                game.ReplicatedStorage:WaitForChild("Remotes").CommF_:InvokeServer("AbandonQuest");
                            end
                            Usefastattack = false
                            StartMagnetAutoFarmLevel= false
                            Modstween = toTarget(CFrameMon.Position,CFrameMon)
                            if OldWorld and (Ms == "Fishman Commando [Lv. 400]" or Ms == "Fishman Warrior [Lv. 375]") and (CFrameQuest.Position - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).magnitude > 50000 then
                                if Modstween then Modstween:Stop() end wait(.5)
                                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(61163.8515625, 11.6796875, 1819.7841796875))
                            elseif OldWorld and not (Ms == "Fishman Commando [Lv. 400]" or Ms == "Fishman Warrior [Lv. 375]") and (CFrameQuest.Position - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).magnitude > 50000 then
                                if Modstween then Modstween:Stop() end wait(.5)
                                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(3864.8515625, 6.6796875, -1926.7841796875))
                            elseif NewWorld and string.find(Ms, "Ship") and (CFrameQuest.Position - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).magnitude > 30000 then
                                if Modstween then Modstween:Stop() end wait(.5)
                                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(923.21252441406, 126.9760055542, 32852.83203125))
                            elseif NewWorld and not string.find(Ms, "Ship") and (CFrameQuest.Position - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).magnitude > 30000 then
                                if Modstween then Modstween:Stop() end wait(.5)
                                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(-6508.5581054688, 89.034996032715, -132.83953857422))
                            elseif (CFrameMon.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 350 then
                                if Modstween then Modstween:Stop() end wait(.5)
                                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrameMon
                            end 
                        end
                    end
                end
            end
            fastWait(.05)
        end
    end)
    spawn(function()
        game:GetService("RunService").Stepped:Connect(function()
            if farm or TweenIsland or TweenNPC or AutoFarmChest or FramBossSelectHop or AutoNew or Auto_Farm or AutoNew or Factory or Autothird or MasteryDevilFruit or MasteryWeapon or MasteryGun or FramBoss or KillAllBoss or AutoMobAura or Observation or AutoSaber or AutoPole or AutoPoleHOP or AutoQuestBartilo or AutoEvoRace2 or AutoRengoku or AutoFramEctoplasm or AutoBuddySwords or AutoBuddySwords or AutoFarmBone or AutoHallowScythe or AutoSoulReaper or AutoFarmCakePrince or AutoYama or HolyTorch or AutoEliteHunter or AutoHakiRainbow or MusketeeHat or AutoObservationHakiV2 or NextIsland or AutoRaids then
                if not KRNL_LOADED and game.Players.LocalPlayer.Character:FindFirstChild("Humanoid") then
                    setfflag("HumanoidParallelRemoveNoPhysics", "False")
                    setfflag("HumanoidParallelRemoveNoPhysicsNoSimulate2", "False")
                    game.Players.LocalPlayer.Character.Humanoid:ChangeState(11)
                else
                    if not game:GetService("Workspace"):FindFirstChild("LOL") then
                        local LOL = Instance.new("Part")
                        LOL.Name = "LOL"
                        LOL.Parent = game.Workspace
                        LOL.Anchored = true
                        LOL.Transparency = 0.8
                        LOL.Size = Vector3.new(50,0.5,50)
                    elseif game:GetService("Workspace"):FindFirstChild("LOL") then
                        game.Workspace["LOL"].CFrame = CFrame.new(game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame.X,game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame.Y - 3.8,game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame.Z)
                    end
                end
                for _, v in pairs(game.Players.LocalPlayer.Character:GetDescendants()) do
                    if v:IsA("BasePart") then
                        v.CanCollide = false
                    end
                end
            end
        end)
    end)
    spawn(function()
        game:GetService("RunService").Heartbeat:Connect(function() CheckQuest()
            for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                if farm and StartMagnetAutoFarmLevel and v.Name ~= "Ice Admiral [Lv. 700] [Boss]" and v.Name ~= "Don Swan [Lv. 3000] [Boss]" and v.Name ~= "Saber Expert [Lv. 200] [Boss]" and v.Name ~= "Longma [Lv. 2000] [Boss]" and (v.HumanoidRootPart.Position-PosMon.Position).magnitude <= 350 then
                    if syn then
                        if isnetworkowner(v.HumanoidRootPart) then
                            v.HumanoidRootPart.CFrame = PosMon
                            v.Humanoid.JumpPower = 0
                            v.Humanoid.WalkSpeed = 0
                            v.HumanoidRootPart.CanCollide = false
                            v.HumanoidRootPart.Size = Vector3.new(50,50,50)
                            if v.Humanoid:FindFirstChild("Animator") then
                                v.Humanoid.Animator:Destroy()
                            end
                            sethiddenproperty(game.Players.LocalPlayer, "SimulationRadius",  math.huge)
                            v.Humanoid:ChangeState(11)
                        end
                    else
                        v.HumanoidRootPart.CFrame = PosMon
                        v.Humanoid.JumpPower = 0
                        v.Humanoid.WalkSpeed = 0
                        v.HumanoidRootPart.CanCollide = false
                        v.HumanoidRootPart.Size = Vector3.new(50,50,50)
                        if v.Humanoid:FindFirstChild("Animator") then
                            v.Humanoid.Animator:Destroy()
                        end
                        sethiddenproperty(game.Players.LocalPlayer, "SimulationRadius",  math.huge)
                        v.Humanoid:ChangeState(11)
                    end	
                end
            end
        end)
    end)
    return AutoFarmfunc
end

spawn(function()
    local gg = getrawmetatable(game)
    local old = gg.__namecall
    setreadonly(gg,false)
    gg.__namecall = newcclosure(function(...)
        local method = getnamecallmethod()
        local args = {...}
        if tostring(method) == "FireServer" then
            if tostring(args[1]) == "RemoteEvent" then
                if tostring(args[2]) ~= "true" and tostring(args[2]) ~= "false" then
                    if UseSkillMasteryDevilFruit then
                        args[2] = PositionSkillMasteryDevilFruit
                        return old(unpack(args))
                    elseif Skillaimbot then
                        args[2] = AimBotSkillPosition
                        return old(unpack(args))
                    end
                end
            end
        end
        return old(...)
    end)
end)

local CombatFrameworkROld = require(game:GetService("Players").LocalPlayer.PlayerScripts.CombatFramework) 
local CombatFrameworkR = getupvalues(CombatFrameworkROld)[2]
local CameraShakerR = require(game.ReplicatedStorage.Util.CameraShaker)
CameraShakerR:Stop()
spawn(function()
    game:GetService("RunService").Stepped:Connect(function()
        pcall(function()
            CombatFrameworkR.activeController.hitboxMagnitude = 55
            if Usefastattack then
                if fastattack then
                    if game.Players.LocalPlayer.Character:FindFirstChild("Black Leg") then
                        CombatFrameworkR.activeController.timeToNextAttack = 3
                    elseif game.Players.LocalPlayer.Character:FindFirstChild("Electro") then
                        CombatFrameworkR.activeController.timeToNextAttack = 2
                    else
                        CombatFrameworkR.activeController.timeToNextAttack = 0
                    end
                    CombatFrameworkR.activeController.attacking = false
                    CombatFrameworkR.activeController.increment = 3
                    CombatFrameworkR.activeController.blocking = false
                    CombatFrameworkR.activeController.timeToNextBlock = 0
                    game.Players.LocalPlayer.Character.Humanoid.Sit = false	
                end
            end
        end)
    end)
end)

spawn(function()
    game:GetService("RunService").Stepped:Connect(function()
        pcall(function()
            if Usefastattack then
                if fastattack then
                    Click()
                end
            end
        end)
    end)
end)



-- Venyx Ui
-- init
local player = game.Players.LocalPlayer
local mouse = player:GetMouse()

-- services
local input = game:GetService("UserInputService")
local run = game:GetService("RunService")
local tween = game:GetService("TweenService")
local tweeninfo = TweenInfo.new

-- additional
local utility = {}

-- themes
local objects = {}
local themes = {
    NotToggledColor =  Color3.fromRGB(255, 100, 89),
    Background = Color3.fromRGB(25,25,25),
    Glow = Color3.fromRGB(0,0,0),
    Accent = Color3.fromRGB(255, 113, 51),
    LightContrast = Color3.fromRGB(40,40,40),
    DarkContrast = Color3.fromRGB(30,30,30),
    TextColor = Color3.fromRGB(255, 255, 255),
    ButtonColor = Color3.fromRGB(255, 113, 51),
    ToggledColor = Color3.fromRGB(255, 113, 51),
    SliderColor = Color3.fromRGB(255, 113, 51),
    TopBarColor = Color3.fromRGB(35,35,35),
}

do
    -- Dynamic Scroll
    function dynamicscroll(scrollingframe,uilis)
        uilis:GetPropertyChangedSignal('AbsoluteContentSize'):Connect(function()
            scrollingframe.CanvasSize = UDim2.new(0, 0, 0, uilis.AbsoluteContentSize.Y + 10)
        end)
    end 

    function utility:Create(instance, properties, children)
        local object = Instance.new(instance)

        for i, v in pairs(properties or {}) do
            object[i] = v

            if typeof(v) == "Color3" then -- save for theme changer later
                local theme = utility:Find(themes, v)

                if theme then
                    objects[theme] = objects[theme] or {}
                    objects[theme][i] = objects[theme][i] or setmetatable({}, {_mode = "k"})

                    table.insert(objects[theme][i], object)
                end
            end
        end

        for i, module in pairs(children or {}) do
            module.Parent = object
        end

        return object
    end

    function utility:Tween(instance, properties, duration, ...)
        tween:Create(instance, tweeninfo(duration, ...), properties):Play()
    end

    function utility:Wait()
        run.RenderStepped:Wait()
        return true
    end

    function utility:Find(table, value) -- table.find doesn't work for dictionaries
        for i, v in  pairs(table) do
            if v == value then
                return i
            end
        end
    end

    function utility:Sort(pattern, values)
        local new = {}
        pattern = pattern:lower()

        if pattern == "" then
            return values
        end

        for i, value in pairs(values) do
            if tostring(value):lower():find(pattern) then
                table.insert(new, value)
            end
        end

        return new
    end

    function utility:Pop(object, shrink)
        local clone = object:Clone()

        clone.AnchorPoint = Vector2.new(0.5, 0.5)
        clone.Size = clone.Size - UDim2.new(0, shrink, 0, shrink)
        clone.Position = UDim2.new(0.5, 0, 0.5, 0)

        clone.Parent = object
        clone:ClearAllChildren()

        object.ImageTransparency = 1
        utility:Tween(clone, {Size = object.Size}, 0.2)

        spawn(function()
            wait(0.2)

            object.ImageTransparency = 0
            clone:Destroy()
        end)

        return clone
    end

    function utility:InitializeKeybind()
        self.keybinds = {}
        self.ended = {}

        input.InputBegan:Connect(function(key)
            if self.keybinds[key.KeyCode] then
                for i, bind in pairs(self.keybinds[key.KeyCode]) do
                    bind()
                end
            end
        end)

        input.InputEnded:Connect(function(key)
            if key.UserInputType == Enum.UserInputType.MouseButton1 then
                for i, callback in pairs(self.ended) do
                    callback()
                end
            end
        end)
    end

    function utility:BindToKey(key, callback)

        self.keybinds[key] = self.keybinds[key] or {}

        table.insert(self.keybinds[key], callback)

        return {
            UnBind = function()
                for i, bind in pairs(self.keybinds[key]) do
                    if bind == callback then
                        table.remove(self.keybinds[key], i)
                    end
                end
            end
        }
    end

    function utility:KeyPressed() -- yield until next key is pressed
        local key = input.InputBegan:Wait()

        while key.UserInputType ~= Enum.UserInputType.Keyboard	 do
            key = input.InputBegan:Wait()
        end

        wait() -- overlapping connection

        return key
    end

    function utility:DraggingEnabled(frame, parent)

        parent = parent or frame

        -- stolen from wally or kiriot, kek
        local dragging = false
        local dragInput, mousePos, framePos

        frame.InputBegan:Connect(function(input)
            if input.UserInputType == Enum.UserInputType.MouseButton1 then
                dragging = true
                mousePos = input.Position
                framePos = parent.Position

                input.Changed:Connect(function()
                    if input.UserInputState == Enum.UserInputState.End then
                        dragging = false
                    end
                end)
            end
        end)

        frame.InputChanged:Connect(function(input)
            if input.UserInputType == Enum.UserInputType.MouseMovement then
                dragInput = input
            end
        end)

        input.InputChanged:Connect(function(input)
            if input == dragInput and dragging then
                local delta = input.Position - mousePos
                parent.Position  = UDim2.new(framePos.X.Scale, framePos.X.Offset + delta.X, framePos.Y.Scale, framePos.Y.Offset + delta.Y)
            end
        end)

    end

    function utility:DraggingEnded(callback)
        table.insert(self.ended, callback)
    end

end

-- classes

local library = {} -- main
local page = {}
local section = {}

do
    library.__index = library
    page.__index = page
    section.__index = section

    -- new classes

    function library.new(title)
        local container = utility:Create("ScreenGui", {
            Name = title,
            Parent = game.CoreGui
        }, {
            utility:Create("ImageLabel", {
                Name = "Main",
                BackgroundTransparency = 1,
                Position = UDim2.new(0.25, 0, 0.052435593, 0),
                Size = UDim2.new(0, 511, 0, 390),
                Image = "rbxassetid://4641149554",
                ImageColor3 = themes.Background,
                ScaleType = Enum.ScaleType.Slice,
                SliceCenter = Rect.new(4, 4, 296, 296)
            }, {
                utility:Create("ImageLabel", {
                    Name = "Glow",
                    BackgroundTransparency = 1,
                    Position = UDim2.new(0, -15, 0, -15),
                    Size = UDim2.new(1, 30, 1, 30),
                    ZIndex = 0,
                    Image = "rbxassetid://5028857084",
                    ImageColor3 = themes.Glow,
                    ScaleType = Enum.ScaleType.Slice,
                    SliceCenter = Rect.new(24, 24, 276, 276)
                }),
                utility:Create("ImageLabel", {
                    Name = "Pages",
                    BackgroundTransparency = 1,
                    ClipsDescendants = true,
                    Position = UDim2.new(0, 0, 0, 38),
                    Size = UDim2.new(0, 126, 1, -38),
                    ZIndex = 3,
                    Image = "rbxassetid://5012534273",
                    ImageColor3 = themes.DarkContrast,
                    ScaleType = Enum.ScaleType.Slice,
                    SliceCenter = Rect.new(4, 4, 296, 296)
                },
                {
                    utility:Create("Frame", {
                        Name = "sadsad",
                        Parent = library.pagesContainer,
                        BackgroundTransparency = 0,
                        BackgroundColor3 = themes.LightContrast,
                        BorderSizePixel = 0,
                        AnchorPoint = Vector2.new(0.5,0),
                        Position = UDim2.new(0.5, 0, 0, 65),
                        Size = UDim2.new(0,60,0,2),
                        ZIndex = 5,
            
                    }),
                    utility:Create("ImageLabel", {
                        Name = "HubLogo",
                        Parent = library.pagesContainer,
                        BackgroundTransparency = 1,
                        AnchorPoint = Vector2.new(0.5,0),
                        Position = UDim2.new(0.5, 0, 0, 5),
                        Size = UDim2.new(0,70,0,70),
                        ZIndex = 5,
                        ImageColor3 = Color3.new(1,1,1),
                        Image = "http://www.roblox.com/asset/?id=8631982009",
                
                    }),
            

                    utility:Create("ScrollingFrame", {
                        Name = "Pages_Container",
                        Active = true,
                        BackgroundTransparency = 1,
                        Position = UDim2.new(0, 0, 0, 80),
                        Size = UDim2.new(1, 0, 1, -20),
                        CanvasSize = UDim2.new(0, 0, 0, 480),
                        ScrollBarThickness = 5,
                        ScrollBarImageTransparency = 0,
                        ScrollBarImageColor3 = themes.LightContrast
                    }, {
                        utility:Create("UIListLayout", {
                            SortOrder = Enum.SortOrder.LayoutOrder,
                            Padding = UDim.new(0, 10)
                        })
                    })
                }

                ),
                utility:Create("ImageLabel", {
                    Name = "TopBar",
                    BackgroundTransparency = 1,
                    ClipsDescendants = true,
                    Size = UDim2.new(1, 0, 0, 38),
                    ZIndex = 5,
                    Image = "rbxassetid://4595286933",
                    ImageColor3 = themes.TopBarColor,
                    ScaleType = Enum.ScaleType.Slice,
                    SliceCenter = Rect.new(4, 4, 296, 296)
                }, {
                    utility:Create("TextLabel", { -- title
                        Name = "Title",
                        AnchorPoint = Vector2.new(0, 0.5),
                        BackgroundTransparency = 1,
                        Position = UDim2.new(0, 12, 0, 19),
                        Size = UDim2.new(1, -46, 0, 16),
                        ZIndex = 5,
                        Font = Enum.Font.GothamBold,
                        Text = title,
                        RichText = true , 
                        TextColor3 = themes.TextColor,
                        TextSize = 14,
                        TextXAlignment = Enum.TextXAlignment.Center
                    }),
                })
            })
        })


        utility:InitializeKeybind()
        utility:DraggingEnabled(container.Main.TopBar, container.Main)
        

        return setmetatable({
            container = container,
            pagesContainer = container.Main.Pages.Pages_Container,
            pages = {}
        }, library)
    end
    
    function page.new(library, title, icon)
        
        local button = utility:Create("TextButton", {
            Name = title,
            Parent = library.pagesContainer,
            BackgroundTransparency = 1,
            BorderSizePixel = 0,
            Size = UDim2.new(1, 0, 0, 26),
            ZIndex = 3,
            AutoButtonColor = false,
            Font = Enum.Font.Gotham,
            Text = "",
            TextSize = 14
        }, {
            utility:Create("TextLabel", {
                Name = "Title",
                AnchorPoint = Vector2.new(0, 0.5),
                BackgroundTransparency = 1,
                Position = UDim2.new(0, 40, 0.5, 0),
                Size = UDim2.new(0, 76, 1, 0),
                ZIndex = 3,
                Font = Enum.Font.Gotham,
                Text = title,
                TextColor3 = themes.TextColor,
                TextSize = 12,
                TextTransparency = 0.65,
                TextXAlignment = Enum.TextXAlignment.Left
            }),
            icon and utility:Create("ImageLabel", {
                Name = "Icon",
                AnchorPoint = Vector2.new(0, 0.5),
                BackgroundTransparency = 1,
                Position = UDim2.new(0, 12, 0.5, 0),
                Size = UDim2.new(0, 16, 0, 16),
                ZIndex = 3,
                Image = "rbxassetid://" .. tostring(icon),
                ImageColor3 = themes.TextColor,
                ImageTransparency = 0.64,
                ScaleType = Enum.ScaleType.Fit
            }) or {}
        })

        local container = utility:Create("ScrollingFrame", {
            Name = title,
            Parent = library.container.Main,
            Active = true,
            BackgroundTransparency = 1,
            BorderSizePixel = 0,
            Position = UDim2.new(0, 134, 0, 46),
            Size = UDim2.new(1, -142, 1, -56),
            CanvasSize = UDim2.new(0, 0, 0, 0),
            ScrollBarThickness = 3,
            ScrollBarImageColor3 = themes.DarkContrast,
            Visible = false
        })
        local uilist =  utility:Create("UIListLayout", {
            SortOrder = Enum.SortOrder.LayoutOrder,
            Padding = UDim.new(0, 10),
            Parent = container, 
        })
        --[[

        uilist:GetPropertyChangedSignal('AbsoluteContentSize'):Connect(function()
            container.CanvasSize = UDim2.new(0, 0, 0, uilist.AbsoluteContentSize.Y + 10)
        end) 
        ]]

        return setmetatable({
            library = library,
            container = container,
            button = button,
            sections = {}
        }, page)
    end

    function section.new(page, title)
        local container = utility:Create("ImageLabel", {
            Name = title,
            Parent = page.container,
            BackgroundTransparency = 1,
            Size = UDim2.new(1, -10, 0, 28),
            ZIndex = 2,
            Image = "rbxassetid://5028857472",
            ImageColor3 = themes.LightContrast,
            ScaleType = Enum.ScaleType.Slice,
            SliceCenter = Rect.new(4, 4, 296, 296),
            ClipsDescendants = true
        }, {
            utility:Create("Frame", {
                Name = "Container",
                Active = true,
                BackgroundTransparency = 1,
                BorderSizePixel = 0,
                Position = UDim2.new(0, 8, 0, 8),
                Size = UDim2.new(1, -16, 1, -16)
            }, {
                utility:Create("TextLabel", {
                    Name = "Title",
                    BackgroundTransparency = 1,
                    Size = UDim2.new(1, 0, 0, 20),
                    ZIndex = 2,
                    Font = Enum.Font.Gotham,
                    Text =  title,
                    TextColor3 = themes.Accent,
                    TextSize = 14,
                    TextXAlignment = Enum.TextXAlignment.Center,
                    TextTransparency = 1
                }),
                utility:Create("UIListLayout", {
                    SortOrder = Enum.SortOrder.LayoutOrder,
                    Padding = UDim.new(0, 4)
                })
            })
        })


        return setmetatable({
            page = page,
            container = container.Container,
            colorpickers = {},
            modules = {},
            binds = {},
            lists = {},
        }, section)
    end

    function library:NewPage(...)

        local page = page.new(self, ...)
        local button = page.button

        table.insert(self.pages, page)

        button.MouseButton1Click:Connect(function()
            self:SelectPage(page, true)
        end)

        return page
    end

    function page:NewSecction(...)
        local section = section.new(self, ...)

        table.insert(self.sections, section)

        return section
    end

    -- functions

    function library:setTheme(theme, color3)
        themes[theme] = color3

        for property, objects in pairs(objects[theme]) do
            for i, object in pairs(objects) do
                if not object.Parent or (object.Name == "Button" and object.Parent.Name == "ColorPicker") then
                    objects[i] = nil -- i can do this because weak tables :D
                else
                    object[property] = color3
                end
            end
        end
    end

    function library:toggle()

        if self.toggling then
            return
        end

        self.toggling = true

        local container = self.container.Main
        local topbar = container.TopBar

        if self.position then
            utility:Tween(container, {
                Size = UDim2.new(0, 511, 0, 428),
                Position = self.position
            }, 0.2)
            wait(0.2)

            utility:Tween(topbar, {Size = UDim2.new(1, 0, 0, 38)}, 0.2)
            wait(0.2)

            container.ClipsDescendants = false
            self.position = nil
        else
            self.position = container.Position
            container.ClipsDescendants = true

            utility:Tween(topbar, {Size = UDim2.new(1, 0, 1, 0)}, 0.2)
            wait(0.2)

            utility:Tween(container, {
                Size = UDim2.new(0, 511, 0, 0),
                Position = self.position + UDim2.new(0, 0, 0, 428)
            }, 0.2)
            wait(0.2)
        end

        self.toggling = false
    end

    -- new modules

    function library:Notify(title, text, callback)

        -- overwrite last notification
        if self.activeNotification then
            self.activeNotification = self.activeNotification()
        end

        -- standard create
        local notification = utility:Create("ImageLabel", {
            Name = "Notification",
            Parent = self.container,
            BackgroundTransparency = 1,
            Size = UDim2.new(0, 200, 0, 60),
            Image = "rbxassetid://5028857472",
            ImageColor3 = themes.Background,
            ScaleType = Enum.ScaleType.Slice,
            SliceCenter = Rect.new(4, 4, 296, 296),
            ZIndex = 3,
            ClipsDescendants = true
        }, {
            utility:Create("ImageLabel", {
                Name = "Flash",
                Size = UDim2.new(1, 0, 1, 0),
                BackgroundTransparency = 1,
                Image = "rbxassetid://4641149554",
                ImageColor3 = themes.TextColor,
                ZIndex = 5
            }),
            utility:Create("ImageLabel", {
                Name = "Glow",
                BackgroundTransparency = 1,
                Position = UDim2.new(0, -15, 0, -15),
                Size = UDim2.new(1, 30, 1, 30),
                ZIndex = 2,
                Image = "rbxassetid://5028857084",
                ImageColor3 = themes.Glow,
                ScaleType = Enum.ScaleType.Slice,
                SliceCenter = Rect.new(24, 24, 276, 276)
            }),
            utility:Create("TextLabel", {
                Name = "Title",
                BackgroundTransparency = 1,
                Position = UDim2.new(0, 10, 0, 8),
                Size = UDim2.new(1, -40, 0, 16),
                ZIndex = 4,
                Font = Enum.Font.GothamSemibold,
                TextColor3 = themes.TextColor,
                TextSize = 14.000,
                TextXAlignment = Enum.TextXAlignment.Left
            }),
            utility:Create("TextLabel", {
                Name = "Text",
                BackgroundTransparency = 1,
                Position = UDim2.new(0, 10, 1, -24),
                Size = UDim2.new(1, -40, 0, 16),
                ZIndex = 4,
                Font = Enum.Font.Gotham,
                TextColor3 = themes.TextColor,
                TextSize = 12.000,
                TextXAlignment = Enum.TextXAlignment.Left
            }),
            utility:Create("ImageButton", {
                Name = "Accept",
                BackgroundTransparency = 1,
                Position = UDim2.new(1, -26, 0, 8),
                Size = UDim2.new(0, 16, 0, 16),
                Image = "rbxassetid://5012538259",
                ImageColor3 = themes.TextColor,
                ZIndex = 4
            }),
            utility:Create("ImageButton", {
                Name = "Decline",
                BackgroundTransparency = 1,
                Position = UDim2.new(1, -26, 1, -24),
                Size = UDim2.new(0, 16, 0, 16),
                Image = "rbxassetid://5012538583",
                ImageColor3 = themes.TextColor,
                ZIndex = 4
            })
        })

        -- dragging
        utility:DraggingEnabled(notification)

        -- position and size
        title = title or "Notification"
        text = text or ""

        notification.Title.Text = title
        notification.Text.Text = text

        local padding = 10
        local textSize = game:GetService("TextService"):GetTextSize(text, 12, Enum.Font.Gotham, Vector2.new(math.huge, 16))

        notification.Position = library.lastNotification or UDim2.new(0, padding, 1, -(notification.AbsoluteSize.Y + padding))
        notification.Size = UDim2.new(0, 0, 0, 60)

        utility:Tween(notification, {Size = UDim2.new(0, textSize.X + 70, 0, 60)}, 0.2)
        wait(0.2)

        notification.ClipsDescendants = false
        utility:Tween(notification.Flash, {
            Size = UDim2.new(0, 0, 0, 60),
            Position = UDim2.new(1, 0, 0, 0)
        }, 0.2)

        -- callbacks
        local active = true
        local close = function()

            if not active then
                return
            end

            active = false
            notification.ClipsDescendants = true

            library.lastNotification = notification.Position
            notification.Flash.Position = UDim2.new(0, 0, 0, 0)
            utility:Tween(notification.Flash, {Size = UDim2.new(1, 0, 1, 0)}, 0.2)

            wait(0.2)
            utility:Tween(notification, {
                Size = UDim2.new(0, 0, 0, 60),
                Position = notification.Position + UDim2.new(0, textSize.X + 70, 0, 0)
            }, 0.2)

            wait(0.2)
            notification:Destroy()
        end

        self.activeNotification = close

        notification.Accept.MouseButton1Click:Connect(function()

            if not active then
                return
            end

            if callback then
                callback(true)
            end

            close()
        end)

        notification.Decline.MouseButton1Click:Connect(function()

            if not active then
                return
            end

            if callback then
                callback(false)
            end

            close()
        end)
    end

    function section:Button(title, callback)
        local button = utility:Create("ImageButton", {
            Name = "Button",
            Parent = self.container,
            BackgroundTransparency = 1,
            BorderSizePixel = 0,
            Size = UDim2.new(1, 0, 0, 30),
            ZIndex = 2,
            Image = "rbxassetid://5028857472",
            ImageColor3 = themes.ButtonColor,
            ScaleType = Enum.ScaleType.Slice,
            SliceCenter = Rect.new(2, 2, 298, 298)
        }, {
            utility:Create("TextLabel", {
                Name = "Title",
                BackgroundTransparency = 1,
                Size = UDim2.new(1, 0, 1, 0),
                ZIndex = 3,
                Font = Enum.Font.Gotham,
                Text = title,
                TextColor3 = themes.TextColor,
                TextSize = 12,
                TextTransparency = 0.10000000149012
            })
        })

        table.insert(self.modules, button)
        --self:Resize()

        local text = button.Title
        local debounce

        button.MouseButton1Click:Connect(function()

            if debounce then
                return
            end

            -- animation
            utility:Pop(button, 10)

            debounce = true
            text.TextSize = 0
            utility:Tween(button.Title, {TextSize = 14}, 0.2)

            wait(0.2)
            utility:Tween(button.Title, {TextSize = 12}, 0.2)

            if callback then
                callback(function(...)
                    self:updateButton(button, ...)
                end)
            end

            debounce = false
        end)
        local buttonfunc = {}
        function buttonfunc:SetText()
            print("yo")
        end 

        return buttonfunc,button
    end

    function section:Toggle(title, default, callback)
        local sec = self 

        -- local title = t or "Toggle"
        -- local default = typeof(d) == 'bool' and d or false
        -- local callback = typeof(d) == 'function' and d or typeof(c) == 'function' and c or function() end

        local toggle = utility:Create("ImageButton", {
            Name = "Toggle",
            Parent = self.container,
            BackgroundTransparency = 1,
            BorderSizePixel = 0,
            Size = UDim2.new(1, 0, 0, 30),
            ZIndex = 2,
            Image = "rbxassetid://5028857472",
            ImageColor3 = themes.DarkContrast,
            ScaleType = Enum.ScaleType.Slice,
            SliceCenter = Rect.new(2, 2, 298, 298)
        },{
            utility:Create("TextLabel", {
                Name = "Title",
                AnchorPoint = Vector2.new(0, 0.5),
                BackgroundTransparency = 1,
                Position = UDim2.new(0, 10, 0.5, 1),
                Size = UDim2.new(0.5, 0, 1, 0),
                ZIndex = 3,
                Font = Enum.Font.Gotham,
                Text = title,
                TextColor3 = themes.TextColor,
                TextSize = 12,
                TextTransparency = 0.10000000149012,
                TextXAlignment = Enum.TextXAlignment.Left
            }),
            utility:Create("ImageLabel", {
                Name = "Button",
                BackgroundTransparency = 1,
                BorderSizePixel = 0,
                Position = UDim2.new(1, -50, 0.5, -8),
                Size = UDim2.new(0, 40, 0, 16),
                ZIndex = 2,
                Image = "rbxassetid://5028857472",
                ImageColor3 = themes.LightContrast,
                ScaleType = Enum.ScaleType.Slice,
                SliceCenter = Rect.new(2, 2, 298, 298)
            }, {
                utility:Create("ImageLabel", {
                    Name = "Frame",
                    BackgroundTransparency = 1,
                    Position = UDim2.new(0, 2, 0.5, -6),
                    Size = UDim2.new(1, -22, 1, -4),
                    ZIndex = 2,
                    Image = "rbxassetid://5028857472",
                    ImageColor3 = themes.TextColor,
                    ScaleType = Enum.ScaleType.Slice,
                    SliceCenter = Rect.new(2, 2, 298, 298)
                })
            })
        })

        table.insert(self.modules, toggle)
        --self:Resize()

        local active = default
        self:updateToggle(toggle, nil, active)

        toggle.MouseButton1Click:Connect(function()
            active = not active
            self:updateToggle(toggle, nil, active)

            if callback then
                callback(active, function(...)
                    self:updateToggle(toggle, ...)
                end)
            end
        end)
        local togglefunc = {}
        function togglefunc:Set(bool)
            active =  bool
            sec:updateToggle(toggle,nil,active)
            if callback then
                callback(active, function(...)
                    sec:updateToggle(toggle, ...)
                end)
            end

        end 

        

        return togglefunc,toggle
    end

    function section:Textbox(title, default, callback)
        local textbox = utility:Create("ImageButton", {
            Name = "Textbox",
            Parent = self.container,
            BackgroundTransparency = 1,
            BorderSizePixel = 0,
            Size = UDim2.new(1, 0, 0, 30),
            ZIndex = 2,
            Image = "rbxassetid://5028857472",
            ImageColor3 = themes.DarkContrast,
            ScaleType = Enum.ScaleType.Slice,
            SliceCenter = Rect.new(2, 2, 298, 298)
        }, {
            utility:Create("TextLabel", {
                Name = "Title",
                AnchorPoint = Vector2.new(0, 0.5),
                BackgroundTransparency = 1,
                Position = UDim2.new(0, 10, 0.5, 1),
                Size = UDim2.new(0.5, 0, 1, 0),
                ZIndex = 3,
                Font = Enum.Font.Gotham,
                Text = title,
                TextColor3 = themes.TextColor,
                TextSize = 12,
                TextTransparency = 0.10000000149012,
                TextXAlignment = Enum.TextXAlignment.Left
            }),
            utility:Create("ImageLabel", {
                Name = "Button",
                BackgroundTransparency = 1,
                Position = UDim2.new(1, -110, 0.5, -8),
                Size = UDim2.new(0, 100, 0, 16),
                ZIndex = 2,
                Image = "rbxassetid://5028857472",
                ImageColor3 = themes.LightContrast,
                ScaleType = Enum.ScaleType.Slice,
                SliceCenter = Rect.new(2, 2, 298, 298)
            }, {
                utility:Create("TextBox", {
                    Name = "Textbox",
                    BackgroundTransparency = 1,
                    TextTruncate = Enum.TextTruncate.AtEnd,
                    Position = UDim2.new(0, 5, 0, 0),
                    Size = UDim2.new(1, -10, 1, 0),
                    ZIndex = 3,
                    Font = Enum.Font.GothamSemibold,
                    Text = default or "",
                    TextColor3 = themes.TextColor,
                    TextSize = 11
                })
            })
        })

        table.insert(self.modules, textbox)
        --self:Resize()

        local button = textbox.Button
        local input = button.Textbox

        textbox.MouseButton1Click:Connect(function()

            if textbox.Button.Size ~= UDim2.new(0, 100, 0, 16) then
                return
            end

            utility:Tween(textbox.Button, {
                Size = UDim2.new(0, 200, 0, 16),
                Position = UDim2.new(1, -210, 0.5, -8)
            }, 0.2)

            wait()

            input.TextXAlignment = Enum.TextXAlignment.Left
            input:CaptureFocus()
        end)

        input:GetPropertyChangedSignal("Text"):Connect(function()

            if button.ImageTransparency == 0 and (button.Size == UDim2.new(0, 200, 0, 16) or button.Size == UDim2.new(0, 100, 0, 16)) then -- i know, i dont like this either
                utility:Pop(button, 10)
            end

            if callback then
                callback(input.Text, nil, function(...)
                    self:updateTextbox(textbox, ...)
                end)
            end
        end)

        input.FocusLost:Connect(function()

            input.TextXAlignment = Enum.TextXAlignment.Center

            utility:Tween(textbox.Button, {
                Size = UDim2.new(0, 100, 0, 16),
                Position = UDim2.new(1, -110, 0.5, -8)
            }, 0.2)

            if callback then
                callback(input.Text, true, function(...)
                    self:updateTextbox(textbox, ...)
                end)
            end
        end)

        return textbox
    end

    function section:Keybind(title, default, callback, changedCallback)
        local keybind = utility:Create("ImageButton", {
            Name = "Keybind",
            Parent = self.container,
            BackgroundTransparency = 1,
            BorderSizePixel = 0,
            Size = UDim2.new(1, 0, 0, 30),
            ZIndex = 2,
            Image = "rbxassetid://5028857472",
            ImageColor3 = themes.DarkContrast,
            ScaleType = Enum.ScaleType.Slice,
            SliceCenter = Rect.new(2, 2, 298, 298)
        }, {
            utility:Create("TextLabel", {
                Name = "Title",
                AnchorPoint = Vector2.new(0, 0.5),
                BackgroundTransparency = 1,
                Position = UDim2.new(0, 10, 0.5, 1),
                Size = UDim2.new(1, 0, 1, 0),
                ZIndex = 3,
                Font = Enum.Font.Gotham,
                Text = title,
                TextColor3 = themes.TextColor,
                TextSize = 12,
                TextTransparency = 0.10000000149012,
                TextXAlignment = Enum.TextXAlignment.Left
            }),
            utility:Create("ImageLabel", {
                Name = "Button",
                BackgroundTransparency = 1,
                Position = UDim2.new(1, -110, 0.5, -8),
                Size = UDim2.new(0, 100, 0, 16),
                ZIndex = 2,
                Image = "rbxassetid://5028857472",
                ImageColor3 = themes.LightContrast,
                ScaleType = Enum.ScaleType.Slice,
                SliceCenter = Rect.new(2, 2, 298, 298)
            }, {
                utility:Create("TextLabel", {
                    Name = "Text",
                    BackgroundTransparency = 1,
                    ClipsDescendants = true,
                    Size = UDim2.new(1, 0, 1, 0),
                    ZIndex = 3,
                    Font = Enum.Font.GothamSemibold,
                    Text = default and default.Name or "None",
                    TextColor3 = themes.TextColor,
                    TextSize = 11
                })
            })
        })

        table.insert(self.modules, keybind)
        --self:Resize()

        local text = keybind.Button.Text
        local button = keybind.Button

        local animate = function()
            if button.ImageTransparency == 0 then
                utility:Pop(button, 10)
            end
        end

        self.binds[keybind] = {callback = function()
            animate()

            if callback then
                callback(function(...)
                    self:updateKeybind(keybind, ...)
                end)
            end
        end}

        if default and callback then
            self:updateKeybind(keybind, nil, default)
        end

        keybind.MouseButton1Click:Connect(function()

            animate()

            if self.binds[keybind].connection then -- unbind
                return self:updateKeybind(keybind)
            end

            if text.Text == "None" then -- new bind
                text.Text = "..."

                local key = utility:KeyPressed()

                self:updateKeybind(keybind, nil, key.KeyCode)
                animate()

                if changedCallback then
                    changedCallback(key, function(...)
                        self:updateKeybind(keybind, ...)
                    end)
                end
            end
        end)

        return keybind
    end

    function section:ColorPicker(title, default, callback)
        local colorpicker = utility:Create("ImageButton", {
            Name = "ColorPicker",
            Parent = self.container,
            BackgroundTransparency = 1,
            BorderSizePixel = 0,
            Size = UDim2.new(1, 0, 0, 30),
            ZIndex = 2,
            Image = "rbxassetid://5028857472",
            ImageColor3 = themes.DarkContrast,
            ScaleType = Enum.ScaleType.Slice,
            SliceCenter = Rect.new(2, 2, 298, 298)
        },{
            utility:Create("TextLabel", {
                Name = "Title",
                AnchorPoint = Vector2.new(0, 0.5),
                BackgroundTransparency = 1,
                Position = UDim2.new(0, 10, 0.5, 1),
                Size = UDim2.new(0.5, 0, 1, 0),
                ZIndex = 3,
                Font = Enum.Font.Gotham,
                Text = title,
                TextColor3 = themes.TextColor,
                TextSize = 12,
                TextTransparency = 0.10000000149012,
                TextXAlignment = Enum.TextXAlignment.Left
            }),
            utility:Create("ImageButton", {
                Name = "Button",
                BackgroundTransparency = 1,
                BorderSizePixel = 0,
                Position = UDim2.new(1, -50, 0.5, -7),
                Size = UDim2.new(0, 40, 0, 14),
                ZIndex = 2,
                Image = "rbxassetid://5028857472",
                ImageColor3 = Color3.fromRGB(255, 255, 255),
                ScaleType = Enum.ScaleType.Slice,
                SliceCenter = Rect.new(2, 2, 298, 298)
            })
        })

        local tab = utility:Create("ImageLabel", {
            Name = "ColorPicker",
            Parent = self.page.library.container,
            BackgroundTransparency = 1,
            Position = UDim2.new(0.75, 0, 0.400000006, 0),
            Selectable = true,
            AnchorPoint = Vector2.new(0.5, 0.5),
            Size = UDim2.new(0, 162, 0, 169),
            Image = "rbxassetid://5028857472",
            ImageColor3 = themes.Background,
            ScaleType = Enum.ScaleType.Slice,
            SliceCenter = Rect.new(2, 2, 298, 298),
            Visible = false,
        }, {
            utility:Create("ImageLabel", {
                Name = "Glow",
                BackgroundTransparency = 1,
                Position = UDim2.new(0, -15, 0, -15),
                Size = UDim2.new(1, 30, 1, 30),
                ZIndex = 0,
                Image = "rbxassetid://5028857084",
                ImageColor3 = themes.Glow,
                ScaleType = Enum.ScaleType.Slice,
                SliceCenter = Rect.new(22, 22, 278, 278)
            }),
            utility:Create("TextLabel", {
                Name = "Title",
                BackgroundTransparency = 1,
                Position = UDim2.new(0, 10, 0, 8),
                Size = UDim2.new(1, -40, 0, 16),
                ZIndex = 2,
                Font = Enum.Font.GothamSemibold,
                Text = title,
                TextColor3 = themes.TextColor,
                TextSize = 14,
                TextXAlignment = Enum.TextXAlignment.Left
            }),
            utility:Create("ImageButton", {
                Name = "Close",
                BackgroundTransparency = 1,
                Position = UDim2.new(1, -26, 0, 8),
                Size = UDim2.new(0, 16, 0, 16),
                ZIndex = 2,
                Image = "rbxassetid://5012538583",
                ImageColor3 = themes.TextColor
            }),
            utility:Create("Frame", {
                Name = "Container",
                BackgroundTransparency = 1,
                Position = UDim2.new(0, 8, 0, 32),
                Size = UDim2.new(1, -18, 1, -40)
            }, {
                utility:Create("UIListLayout", {
                    SortOrder = Enum.SortOrder.LayoutOrder,
                    Padding = UDim.new(0, 6)
                }),
                utility:Create("ImageButton", {
                    Name = "Canvas",
                    BackgroundTransparency = 1,
                    BorderColor3 = themes.LightContrast,
                    Size = UDim2.new(1, 0, 0, 60),
                    AutoButtonColor = false,
                    Image = "rbxassetid://5108535320",
                    ImageColor3 = Color3.fromRGB(255, 0, 0),
                    ScaleType = Enum.ScaleType.Slice,
                    SliceCenter = Rect.new(2, 2, 298, 298)
                }, {
                    utility:Create("ImageLabel", {
                        Name = "White_Overlay",
                        BackgroundTransparency = 1,
                        Size = UDim2.new(1, 0, 0, 60),
                        Image = "rbxassetid://5107152351",
                        SliceCenter = Rect.new(2, 2, 298, 298)
                    }),
                    utility:Create("ImageLabel", {
                        Name = "Black_Overlay",
                        BackgroundTransparency = 1,
                        Size = UDim2.new(1, 0, 0, 60),
                        Image = "rbxassetid://5107152095",
                        SliceCenter = Rect.new(2, 2, 298, 298)
                    }),
                    utility:Create("ImageLabel", {
                        Name = "Cursor",
                        BackgroundColor3 = themes.TextColor,
                        AnchorPoint = Vector2.new(0.5, 0.5),
                        BackgroundTransparency = 1.000,
                        Size = UDim2.new(0, 10, 0, 10),
                        Position = UDim2.new(0, 0, 0, 0),
                        Image = "rbxassetid://5100115962",
                        SliceCenter = Rect.new(2, 2, 298, 298)
                    })
                }),
                utility:Create("ImageButton", {
                    Name = "Color",
                    BackgroundTransparency = 1,
                    BorderSizePixel = 0,
                    Position = UDim2.new(0, 0, 0, 4),
                    Selectable = false,
                    Size = UDim2.new(1, 0, 0, 16),
                    ZIndex = 2,
                    AutoButtonColor = false,
                    Image = "rbxassetid://5028857472",
                    ScaleType = Enum.ScaleType.Slice,
                    SliceCenter = Rect.new(2, 2, 298, 298)
                }, {
                    utility:Create("Frame", {
                        Name = "Select",
                        BackgroundColor3 = themes.TextColor,
                        BorderSizePixel = 1,
                        Position = UDim2.new(1, 0, 0, 0),
                        Size = UDim2.new(0, 2, 1, 0),
                        ZIndex = 2
                    }),
                    utility:Create("UIGradient", { -- rainbow canvas
                        Color = ColorSequence.new({
                            ColorSequenceKeypoint.new(0.00, Color3.fromRGB(255, 0, 0)),
                            ColorSequenceKeypoint.new(0.17, Color3.fromRGB(255, 255, 0)),
                            ColorSequenceKeypoint.new(0.33, Color3.fromRGB(0, 255, 0)),
                            ColorSequenceKeypoint.new(0.50, Color3.fromRGB(0, 255, 255)),
                            ColorSequenceKeypoint.new(0.66, Color3.fromRGB(0, 0, 255)),
                            ColorSequenceKeypoint.new(0.82, Color3.fromRGB(255, 0, 255)),
                            ColorSequenceKeypoint.new(1.00, Color3.fromRGB(255, 0, 0))
                        })
                    })
                }),
                utility:Create("Frame", {
                    Name = "Inputs",
                    BackgroundTransparency = 1,
                    Position = UDim2.new(0, 10, 0, 158),
                    Size = UDim2.new(1, 0, 0, 16)
                }, {
                    utility:Create("UIListLayout", {
                        FillDirection = Enum.FillDirection.Horizontal,
                        SortOrder = Enum.SortOrder.LayoutOrder,
                        Padding = UDim.new(0, 6)
                    }),
                    utility:Create("ImageLabel", {
                        Name = "R",
                        BackgroundTransparency = 1,
                        BorderSizePixel = 0,
                        Size = UDim2.new(0.305, 0, 1, 0),
                        ZIndex = 2,
                        Image = "rbxassetid://5028857472",
                        ImageColor3 = themes.DarkContrast,
                        ScaleType = Enum.ScaleType.Slice,
                        SliceCenter = Rect.new(2, 2, 298, 298)
                    }, {
                        utility:Create("TextLabel", {
                            Name = "Text",
                            BackgroundTransparency = 1,
                            Size = UDim2.new(0.400000006, 0, 1, 0),
                            ZIndex = 2,
                            Font = Enum.Font.Gotham,
                            Text = "R:",
                            TextColor3 = themes.TextColor,
                            TextSize = 10.000
                        }),
                        utility:Create("TextBox", {
                            Name = "Textbox",
                            BackgroundTransparency = 1,
                            Position = UDim2.new(0.300000012, 0, 0, 0),
                            Size = UDim2.new(0.600000024, 0, 1, 0),
                            ZIndex = 2,
                            Font = Enum.Font.Gotham,
                            PlaceholderColor3 = themes.DarkContrast,
                            Text = "255",
                            TextColor3 = themes.TextColor,
                            TextSize = 10.000
                        })
                    }),
                    utility:Create("ImageLabel", {
                        Name = "G",
                        BackgroundTransparency = 1,
                        BorderSizePixel = 0,
                        Size = UDim2.new(0.305, 0, 1, 0),
                        ZIndex = 2,
                        Image = "rbxassetid://5028857472",
                        ImageColor3 = themes.DarkContrast,
                        ScaleType = Enum.ScaleType.Slice,
                        SliceCenter = Rect.new(2, 2, 298, 298)
                    }, {
                        utility:Create("TextLabel", {
                            Name = "Text",
                            BackgroundTransparency = 1,
                            ZIndex = 2,
                            Size = UDim2.new(0.400000006, 0, 1, 0),
                            Font = Enum.Font.Gotham,
                            Text = "G:",
                            TextColor3 = themes.TextColor,
                            TextSize = 10.000
                        }),
                        utility:Create("TextBox", {
                            Name = "Textbox",
                            BackgroundTransparency = 1,
                            Position = UDim2.new(0.300000012, 0, 0, 0),
                            Size = UDim2.new(0.600000024, 0, 1, 0),
                            ZIndex = 2,
                            Font = Enum.Font.Gotham,
                            Text = "255",
                            TextColor3 = themes.TextColor,
                            TextSize = 10.000
                        })
                    }),
                    utility:Create("ImageLabel", {
                        Name = "B",
                        BackgroundTransparency = 1,
                        BorderSizePixel = 0,
                        Size = UDim2.new(0.305, 0, 1, 0),
                        ZIndex = 2,
                        Image = "rbxassetid://5028857472",
                        ImageColor3 = themes.DarkContrast,
                        ScaleType = Enum.ScaleType.Slice,
                        SliceCenter = Rect.new(2, 2, 298, 298)
                    }, {
                        utility:Create("TextLabel", {
                            Name = "Text",
                            BackgroundTransparency = 1,
                            Size = UDim2.new(0.400000006, 0, 1, 0),
                            ZIndex = 2,
                            Font = Enum.Font.Gotham,
                            Text = "B:",
                            TextColor3 = themes.TextColor,
                            TextSize = 10.000
                        }),
                        utility:Create("TextBox", {
                            Name = "Textbox",
                            BackgroundTransparency = 1,
                            Position = UDim2.new(0.300000012, 0, 0, 0),
                            Size = UDim2.new(0.600000024, 0, 1, 0),
                            ZIndex = 2,
                            Font = Enum.Font.Gotham,
                            Text = "255",
                            TextColor3 = themes.TextColor,
                            TextSize = 10.000
                        })
                    }),
                }),
                utility:Create("ImageButton", {
                    Name = "Button",
                    BackgroundTransparency = 1,
                    BorderSizePixel = 0,
                    Size = UDim2.new(1, 0, 0, 20),
                    ZIndex = 2,
                    Image = "rbxassetid://5028857472",
                    ImageColor3 = themes.DarkContrast,
                    ScaleType = Enum.ScaleType.Slice,
                    SliceCenter = Rect.new(2, 2, 298, 298)
                }, {
                    utility:Create("TextLabel", {
                        Name = "Text",
                        BackgroundTransparency = 1,
                        Size = UDim2.new(1, 0, 1, 0),
                        ZIndex = 3,
                        Font = Enum.Font.Gotham,
                        Text = "Submit",
                        TextColor3 = themes.TextColor,
                        TextSize = 11.000
                    })
                })
            })
        })

        utility:DraggingEnabled(tab)
        table.insert(self.modules, colorpicker)
        --self:Resize()

        local allowed = {
            [""] = true
        }

        local canvas = tab.Container.Canvas
        local color = tab.Container.Color

        local canvasSize, canvasPosition = canvas.AbsoluteSize, canvas.AbsolutePosition
        local colorSize, colorPosition = color.AbsoluteSize, color.AbsolutePosition

        local draggingColor, draggingCanvas

        local color3 = default or Color3.fromRGB(255, 255, 255)
        local hue, sat, brightness = 0, 0, 1
        local rgb = {
            r = 255,
            g = 255,
            b = 255
        }

        self.colorpickers[colorpicker] = {
            tab = tab,
            callback = function(prop, value)
                rgb[prop] = value
                hue, sat, brightness = Color3.toHSV(Color3.fromRGB(rgb.r, rgb.g, rgb.b))
            end
        }

        local callback = function(value)
            if callback then
                callback(value, function(...)
                    self:updateColorPicker(colorpicker, ...)
                end)
            end
        end

        utility:DraggingEnded(function()
            draggingColor, draggingCanvas = false, false
        end)

        if default then
            self:updateColorPicker(colorpicker, nil, default)

            hue, sat, brightness = Color3.toHSV(default)
            default = Color3.fromHSV(hue, sat, brightness)

            for i, prop in pairs({"r", "g", "b"}) do
                rgb[prop] = default[prop:upper()] * 255
            end
        end

        for i, container in pairs(tab.Container.Inputs:GetChildren()) do -- i know what you are about to say, so shut up
            if container:IsA("ImageLabel") then
                local textbox = container.Textbox
                local focused

                textbox.Focused:Connect(function()
                    focused = true
                end)

                textbox.FocusLost:Connect(function()
                    focused = false

                    if not tonumber(textbox.Text) then
                        textbox.Text = math.floor(rgb[container.Name:lower()])
                    end
                end)

                textbox:GetPropertyChangedSignal("Text"):Connect(function()
                    local text = textbox.Text

                    if not allowed[text] and not tonumber(text) then
                        textbox.Text = text:sub(1, #text - 1)
                    elseif focused and not allowed[text] then
                        rgb[container.Name:lower()] = math.clamp(tonumber(textbox.Text), 0, 255)

                        local color3 = Color3.fromRGB(rgb.r, rgb.g, rgb.b)
                        hue, sat, brightness = Color3.toHSV(color3)

                        self:updateColorPicker(colorpicker, nil, color3)
                        callback(color3)
                    end
                end)
            end
        end

        canvas.MouseButton1Down:Connect(function()
            draggingCanvas = true

            while draggingCanvas do

                local x, y = mouse.X, mouse.Y

                sat = math.clamp((x - canvasPosition.X) / canvasSize.X, 0, 1)
                brightness = 1 - math.clamp((y - canvasPosition.Y) / canvasSize.Y, 0, 1)

                color3 = Color3.fromHSV(hue, sat, brightness)

                for i, prop in pairs({"r", "g", "b"}) do
                    rgb[prop] = color3[prop:upper()] * 255
                end

                self:updateColorPicker(colorpicker, nil, {hue, sat, brightness}) -- roblox is literally retarded
                utility:Tween(canvas.Cursor, {Position = UDim2.new(sat, 0, 1 - brightness, 0)}, 0.1) -- overwrite

                callback(color3)
                utility:Wait()
            end
        end)

        color.MouseButton1Down:Connect(function()
            draggingColor = true

            while draggingColor do

                hue = 1 - math.clamp(1 - ((mouse.X - colorPosition.X) / colorSize.X), 0, 1)
                color3 = Color3.fromHSV(hue, sat, brightness)

                for i, prop in pairs({"r", "g", "b"}) do
                    rgb[prop] = color3[prop:upper()] * 255
                end

                local x = hue -- hue is updated
                self:updateColorPicker(colorpicker, nil, {hue, sat, brightness}) -- roblox is literally retarded
                utility:Tween(tab.Container.Color.Select, {Position = UDim2.new(x, 0, 0, 0)}, 0.1) -- overwrite

                callback(color3)
                utility:Wait()
            end
        end)

        -- click events
        local button = colorpicker.Button
        local toggle, debounce, animate

        lastColor = Color3.fromHSV(hue, sat, brightness)
        animate = function(visible, overwrite)

            if overwrite then

                if not toggle then
                    return
                end

                if debounce then
                    while debounce do
                        utility:Wait()
                    end
                end
            elseif not overwrite then
                if debounce then
                    return
                end

                if button.ImageTransparency == 0 then
                    utility:Pop(button, 10)
                end
            end

            toggle = visible
            debounce = true

            if visible then

                if self.page.library.activePicker and self.page.library.activePicker ~= animate then
                    self.page.library.activePicker(nil, true)
                end

                self.page.library.activePicker = animate
                lastColor = Color3.fromHSV(hue, sat, brightness)

                local x1, x2 = button.AbsoluteSize.X / 2, 162--tab.AbsoluteSize.X
                local px, py = button.AbsolutePosition.X, button.AbsolutePosition.Y

                tab.ClipsDescendants = true
                tab.Visible = true
                tab.Size = UDim2.new(0, 0, 0, 0)

                tab.Position = UDim2.new(0, x1 + x2 + px, 0, py)
                utility:Tween(tab, {Size = UDim2.new(0, 162, 0, 169)}, 0.2)

                -- update size and position
                wait(0.2)
                tab.ClipsDescendants = false

                canvasSize, canvasPosition = canvas.AbsoluteSize, canvas.AbsolutePosition
                colorSize, colorPosition = color.AbsoluteSize, color.AbsolutePosition
            else
                utility:Tween(tab, {Size = UDim2.new(0, 0, 0, 0)}, 0.2)
                tab.ClipsDescendants = true

                wait(0.2)
                tab.Visible = false
            end

            debounce = false
        end

        local toggleTab = function()
            animate(not toggle)
        end

        button.MouseButton1Click:Connect(toggleTab)
        colorpicker.MouseButton1Click:Connect(toggleTab)

        tab.Container.Button.MouseButton1Click:Connect(function()
            animate()
        end)

        tab.Close.MouseButton1Click:Connect(function()
            self:updateColorPicker(colorpicker, nil, lastColor)
            animate()
        end)

        return colorpicker
    end

    function section:Slider(title, min, default, max, callback)
        local sel = self 
        local slider = utility:Create("ImageButton", {
            Name = "Slider",
            Parent = self.container,
            BackgroundTransparency = 1,
            BorderSizePixel = 0,
            Position = UDim2.new(0.292817682, 0, 0.299145311, 0),
            Size = UDim2.new(1, 0, 0, 50),
            ZIndex = 2,
            Image = "rbxassetid://5028857472",
            ImageColor3 = themes.DarkContrast,
            ScaleType = Enum.ScaleType.Slice,
            SliceCenter = Rect.new(2, 2, 298, 298)
        }, {
            utility:Create("TextLabel", {
                Name = "Title",
                BackgroundTransparency = 1,
                Position = UDim2.new(0, 10, 0, 6),
                Size = UDim2.new(0.5, 0, 0, 16),
                ZIndex = 3,
                Font = Enum.Font.Gotham,
                Text = title,
                TextColor3 = themes.TextColor,
                TextSize = 12,
                TextTransparency = 0.10000000149012,
                TextXAlignment = Enum.TextXAlignment.Left
            }),
            utility:Create("TextBox", {
                Name = "TextBox",
                BackgroundTransparency = 1,
                BorderSizePixel = 0,
                Position = UDim2.new(1, -30, 0, 6),
                Size = UDim2.new(0, 20, 0, 16),
                ZIndex = 3,
                Font = Enum.Font.GothamSemibold,
                Text = default or min,
                TextColor3 = themes.TextColor,
                TextSize = 12,
                TextXAlignment = Enum.TextXAlignment.Right
            }),
            utility:Create("TextLabel", {
                Name = "Slider",
                BackgroundTransparency = 1,
                Position = UDim2.new(0, 10, 0, 28),
                Size = UDim2.new(1, -20, 0, 16),
                ZIndex = 3,
                Text = "",
            }, {
                utility:Create("ImageLabel", {
                    Name = "Bar",
                    AnchorPoint = Vector2.new(0, 0.5),
                    BackgroundTransparency = 1,
                    Position = UDim2.new(0, 0, 0.5, 0),
                    Size = UDim2.new(1, 0, 0, 4),
                    ZIndex = 3,
                    Image = "rbxassetid://5028857472",
                    ImageColor3 = themes.LightContrast,
                    ScaleType = Enum.ScaleType.Slice,
                    SliceCenter = Rect.new(2, 2, 298, 298)
                }, {
                    utility:Create("ImageLabel", {
                        Name = "Fill",
                        BackgroundTransparency = 1,
                        Size = UDim2.new(0.8, 0, 1, 0),
                        ZIndex = 3,
                        Image = "rbxassetid://5028857472",
                        ImageColor3 = themes.TextColor,
                        ScaleType = Enum.ScaleType.Slice,
                        SliceCenter = Rect.new(2, 2, 298, 298)
                    }, {
                        utility:Create("ImageLabel", {
                            Name = "Circle",
                            AnchorPoint = Vector2.new(0.5, 0.5),
                            BackgroundTransparency = 1,
                            ImageTransparency = 1.000,
                            ImageColor3 = themes.TextColor,
                            Position = UDim2.new(1, 0, 0.5, 0),
                            Size = UDim2.new(0, 10, 0, 10),
                            ZIndex = 3,
                            Image = "rbxassetid://4608020054"
                        })
                    })
                })
            })
        })

        table.insert(self.modules, slider)
        --self:Resize()

        local allowed = {
            [""] = true,
            ["-"] = true
        }

        local textbox = slider.TextBox
        local circle = slider.Slider.Bar.Fill.Circle

        local value = default or min
        local dragging, last

        local callback = function(value)
            if callback then
                callback(value, function(...)
                    self:updateSlider(slider, ...)
                end)
            end
        end

        self:updateSlider(slider, nil, value, min, max)

        utility:DraggingEnded(function()
            dragging = false
        end)

        slider.MouseButton1Down:Connect(function(input)
            dragging = true

            while dragging do
                utility:Tween(circle, {ImageTransparency = 0}, 0.1)

                value = self:updateSlider(slider, nil, nil, min, max, value)
                callback(value)

                utility:Wait()
            end

            wait(0.5)
            utility:Tween(circle, {ImageTransparency = 1}, 0.2)
        end)

        textbox.FocusLost:Connect(function()
            if not tonumber(textbox.Text) then
                value = self:updateSlider(slider, nil, default or min, min, max)
                callback(value)
            end
        end)

        textbox:GetPropertyChangedSignal("Text"):Connect(function()
            local text = textbox.Text

            if not allowed[text] and not tonumber(text) then
                textbox.Text = text:sub(1, #text - 1)
            elseif not allowed[text] then
                value = self:updateSlider(slider, nil, tonumber(text) or value, min, max)
                callback(value)
            end
        end)

        local sliderfunc = {}
        function sliderfunc:Set(newva)
            local text = tonumber(newva)

            if not allowed[text] and not tonumber(text) then
                textbox.Text = text:sub(1, #text - 1)
            elseif not allowed[text] then
                value = sel:updateSlider(slider, nil, tonumber(text) or value, min, max)
                callback(value)
            end
        end 

        return sliderfunc,slider
    end

    function section:Dropdown(title, list, callback)
        local dropdown = utility:Create("Frame", {
            Name = "Dropdown",
            Parent = self.container,
            BackgroundTransparency = 1,
            Size = UDim2.new(1, 0, 0, 30),
            ClipsDescendants = true
        }, {
            
        
    
            utility:Create("UIListLayout", {
                SortOrder = Enum.SortOrder.LayoutOrder,
                Padding = UDim.new(0, 4)
            }),
            utility:Create("ImageLabel", {
                Name = "Search",
                BackgroundTransparency = 1,
                BorderSizePixel = 0,
                Size = UDim2.new(1, 0, 0, 30),
                ZIndex = 2,
                Image = "rbxassetid://5028857472",
                ImageColor3 = themes.DarkContrast,
                ScaleType = Enum.ScaleType.Slice,
                SliceCenter = Rect.new(2, 2, 298, 298)
            }, {
            
                utility:Create("TextBox", {
                    Name = "TextBox",
                    AnchorPoint = Vector2.new(0, 0.5),
                    BackgroundTransparency = 1,
                    TextTruncate = Enum.TextTruncate.AtEnd,
                    Position = UDim2.new(0, 10, 0.5, 1),
                    Size = UDim2.new(1, -42, 1, 0),
                    ZIndex = 3,
                    Font = Enum.Font.Gotham,
                    Text = title,
                    TextColor3 = themes.TextColor,
                    TextSize = 12,
                    TextTransparency = 0.10000000149012,
                    TextXAlignment = Enum.TextXAlignment.Left
                }),
                utility:Create("ImageButton", {
                    Name = "Button",
                    BackgroundTransparency = 1,
                    BorderSizePixel = 0,
                    Position = UDim2.new(1, -28, 0.5, -9),
                    Size = UDim2.new(0, 18, 0, 18),
                    ZIndex = 3,
                    Image = "rbxassetid://5012539403",
                    ImageColor3 = themes.TextColor,
                    SliceCenter = Rect.new(2, 2, 298, 298)
                })
            }),
            utility:Create("ImageLabel", {
                Name = "List",
                BackgroundTransparency = 1,
                BorderSizePixel = 0,
                Size = UDim2.new(1, 0, 1, -34),
                ZIndex = 2,
                Image = "rbxassetid://5028857472",
                ImageColor3 = themes.Background,
                ScaleType = Enum.ScaleType.Slice,
                SliceCenter = Rect.new(2, 2, 298, 298)
            }, {
                
                utility:Create("ScrollingFrame", {
                    Name = "Frame",
                    Active = true,
                    BackgroundTransparency = 1,
                    BorderSizePixel = 0,
                    Position = UDim2.new(0, 4, 0, 4),
                    Size = UDim2.new(1, -8, 1, -8),
                    CanvasPosition = Vector2.new(0, 28),
                    CanvasSize = UDim2.new(0, 0, 0, 120),
                    ZIndex = 2,
                    ScrollBarThickness = 3,
                    ScrollBarImageColor3 = themes.DarkContrast
                }, {
                    utility:Create("UIListLayout", {
                        SortOrder = Enum.SortOrder.LayoutOrder,
                        Padding = UDim.new(0, 4)
                    })
                })
            })
        })

        table.insert(self.modules, dropdown)
        --self:Resize()

        local search = dropdown.Search
        local focused

        list = list or {}

        search.Button.MouseButton1Click:Connect(function()
            if search.Button.Rotation == 0 then
                self:updateDropdown(dropdown, nil, list, callback)
            else
                self:updateDropdown(dropdown, nil, nil, callback)
            end
        end)

        search.TextBox.Focused:Connect(function()
            if search.Button.Rotation == 0 then
                self:updateDropdown(dropdown, nil, list, callback)
            end

            focused = true
        end)

        search.TextBox.FocusLost:Connect(function()
            focused = false
            wait(0.2)
            if search.TextBox.Text == ""  then
                search.TextBox.Text = title
                self:updateDropdown(dropdown, nil, nil, callback)

            end
        end)

        search.TextBox:GetPropertyChangedSignal("Text"):Connect(function()
            if focused then
                local list = utility:Sort(search.TextBox.Text, list)
                list = #list ~= 0 and list

                self:updateDropdown(dropdown, nil, list, callback)
            end

        end)

        dropdown:GetPropertyChangedSignal("Size"):Connect(function()
            self:Resize()
        end)

        return dropdown
    end

    -- class functions

    function library:SelectPage(page, toggle)

        if toggle and self.focusedPage == page then -- already selected
            return
        end

        local button = page.button

        if toggle then
            -- page button
            button.Title.TextTransparency = 0
            button.Title.Font = Enum.Font.GothamSemibold

            if button:FindFirstChild("Icon") then
                button.Icon.ImageTransparency = 0
            end

            -- update selected page
            local focusedPage = self.focusedPage
            self.focusedPage = page

            if focusedPage then
                self:SelectPage(focusedPage)
            end

            -- sections
            local existingSections = focusedPage and #focusedPage.sections or 0
            local sectionsRequired = #page.sections - existingSections

            page:Resize()

            for i, section in pairs(page.sections) do
                section.container.Parent.ImageTransparency = 0
            end

            if sectionsRequired < 0 then -- "hides" some sections
                for i = existingSections, #page.sections + 1, -1 do
                    local section = focusedPage.sections[i].container.Parent

                    utility:Tween(section, {ImageTransparency = 1}, 0.1)
                end
            end

            wait(0.1)
            page.container.Visible = true

            if focusedPage then
                focusedPage.container.Visible = false
            end

            if sectionsRequired > 0 then -- "creates" more section
                for i = existingSections + 1, #page.sections do
                    local section = page.sections[i].container.Parent

                    section.ImageTransparency = 1
                    utility:Tween(section, {ImageTransparency = 0}, 0.05)
                end
            end

            wait(0.05)

            for i, section in pairs(page.sections) do

                utility:Tween(section.container.Title, {TextTransparency = 0}, 0.1)
                section:Resize(true)

                wait(0.05)
            end

            wait(0.05)
            page:Resize(true)
        else
            -- page button
            button.Title.Font = Enum.Font.Gotham
            button.Title.TextTransparency = 0.65

            if button:FindFirstChild("Icon") then
                button.Icon.ImageTransparency = 0.65
            end

            -- sections
            for i, section in pairs(page.sections) do
                utility:Tween(section.container.Parent, {Size = UDim2.new(1, -10, 0, 28)}, 0.1)
                utility:Tween(section.container.Title, {TextTransparency = 1}, 0.1)
            end

            wait(0.1)

            page.lastPosition = page.container.CanvasPosition.Y
            page:Resize()
        end
    end

    function page:Resize(scroll)
        local padding = 10
        local size = 0

        for i, section in pairs(self.sections) do
            size = size + section.container.Parent.AbsoluteSize.Y + padding
        end

        self.container.CanvasSize = UDim2.new(0, 0, 0, size)
        self.container.ScrollBarImageTransparency = size > self.container.AbsoluteSize.Y

        if scroll then
            utility:Tween(self.container, {CanvasPosition = Vector2.new(0, self.lastPosition or 0)}, 0.2)
        end
    end

    function section:Resize(smooth)

        if self.page.library.focusedPage ~= self.page then
            return
        end

        local padding = 4
        local size = (4 * padding) + self.container.Title.AbsoluteSize.Y -- offset

        for i, module in pairs(self.modules) do
            size = size + module.AbsoluteSize.Y + padding
        end

        if smooth then
            utility:Tween(self.container.Parent, {Size = UDim2.new(1, -10, 0, size)}, 0.05)
        else
            self.container.Parent.Size = UDim2.new(1, -10, 0, size)
            self.page:Resize()
        end
    end

    function section:getModule(info)

        if table.find(self.modules, info) then
            return info
        end

        for i, module in pairs(self.modules) do
            if (module:FindFirstChild("Title") or module:FindFirstChild("TextBox", true)).Text == info then
                return module
            end
        end

        error("No module found under "..tostring(info))
    end

    -- updates

    function section:updateButton(button, title)
        button = self:getModule(button)

        button.Title.Text = title
    end

    function section:updateToggle(toggle, title, value)
        spawn(function()
            toggle = self:getModule(toggle)

            local position = {
                In = UDim2.new(0, 2, 0.5, -6),
                Out = UDim2.new(0, 20, 0.5, -6)
            }
            local color = {
                In = themes.NotToggledColor,
                Out = themes.ToggledColor
            }

            local frame = toggle.Button.Frame
            local btn = toggle.Button
            value = value and "Out" or "In"

            if title then
                toggle.Title.Text = title
            end

            utility:Tween(frame, {
                Size = UDim2.new(1, -22, 1, -9),
                Position = position[value] + UDim2.new(0, 0, 0, 2.5)
            }, 0.2)

            utility:Tween(btn, {
                ImageColor3 = color[value]
            }, 0.2)

            wait(0.1)
            utility:Tween(frame, {
                Size = UDim2.new(1, -22, 1, -4),
                Position = position[value]
            }, 0.1)
        end)
    end

    function section:updateTextbox(textbox, title, value)
        textbox = self:getModule(textbox)

        if title then
            textbox.Title.Text = title
        end

        if value then
            textbox.Button.Textbox.Text = value
        end

    end

    function section:updateKeybind(keybind, title, key)
        keybind = self:getModule(keybind)

        local text = keybind.Button.Text
        local bind = self.binds[keybind]

        if title then
            keybind.Title.Text = title
        end

        if bind.connection then
            bind.connection = bind.connection:UnBind()
        end

        if key then
            self.binds[keybind].connection = utility:BindToKey(key, bind.callback)
            text.Text = key.Name
        else
            text.Text = "None"
        end
    end

    function section:updateColorPicker(colorpicker, title, color)
        colorpicker = self:getModule(colorpicker)

        local picker = self.colorpickers[colorpicker]
        local tab = picker.tab
        local callback = picker.callback

        if title then
            colorpicker.Title.Text = title
            tab.Title.Text = title
        end

        local color3
        local hue, sat, brightness

        if type(color) == "table" then -- roblox is literally retarded x2
            hue, sat, brightness = unpack(color)
            color3 = Color3.fromHSV(hue, sat, brightness)
        else
            color3 = color
            hue, sat, brightness = Color3.toHSV(color3)
        end

        utility:Tween(colorpicker.Button, {ImageColor3 = color3}, 0.5)
        utility:Tween(tab.Container.Color.Select, {Position = UDim2.new(hue, 0, 0, 0)}, 0.1)

        utility:Tween(tab.Container.Canvas, {ImageColor3 = Color3.fromHSV(hue, 1, 1)}, 0.5)
        utility:Tween(tab.Container.Canvas.Cursor, {Position = UDim2.new(sat, 0, 1 - brightness)}, 0.5)

        for i, container in pairs(tab.Container.Inputs:GetChildren()) do
            if container:IsA("ImageLabel") then
                local value = math.clamp(color3[container.Name], 0, 1) * 255

                container.Textbox.Text = math.floor(value)
                --callback(container.Name:lower(), value)
            end
        end
    end

    function section:updateSlider(slider, title, value, min, max, lvalue)
        slider = self:getModule(slider)

        if title then
            slider.Title.Text = title
        end

        local bar = slider.Slider.Bar
        local percent = (mouse.X - bar.AbsolutePosition.X) / bar.AbsoluteSize.X

        if value then -- support negative ranges
            percent = (value - min) / (max - min)
        end

        percent = math.clamp(percent, 0, 1)
        value = value or math.floor(min + (max - min) * percent)

        slider.TextBox.Text = value
        utility:Tween(bar.Fill, {
            Size = UDim2.new(percent, 0, 1, 0),
            ImageColor3 = themes.Slider
        }, 0.1)

        if value ~= lvalue and slider.ImageTransparency == 0 then
            utility:Pop(slider, 10)
        end

        return value
    end
    function section:clearDropdown(dropdown)
        dropdown = self:getModule(dropdown)

        if title then
            dropdown.Search.TextBox.Text = title
        end

    
        for i, button in pairs(dropdown.List.Frame:GetChildren()) do
            if button:IsA("ImageButton") then
                button:Destroy()
            end
        end

    end 
    function section:updateDropdown(dropdown, title, list, callback)
        spawn(function()
            dropdown = self:getModule(dropdown)

            if title then
                dropdown.Search.TextBox.Text = title
            end

            local entries = 0

            utility:Pop(dropdown.Search, 10)



            for i, value in pairs(list or {}) do
                local button = utility:Create("ImageButton", {
                    Parent = dropdown.List.Frame,
                    BackgroundTransparency = 1,
                    BorderSizePixel = 0,
                    Size = UDim2.new(1, 0, 0, 30),
                    ZIndex = 2,
                    Image = "rbxassetid://5028857472",
                    ImageColor3 = themes.DarkContrast,
                    ScaleType = Enum.ScaleType.Slice,
                    SliceCenter = Rect.new(2, 2, 298, 298)
                }, {
                    utility:Create("TextLabel", {
                        BackgroundTransparency = 1,
                        Position = UDim2.new(0, 10, 0, 0),
                        Size = UDim2.new(1, -10, 1, 0),
                        ZIndex = 3,
                        Font = Enum.Font.Gotham,
                        Text = value,
                        TextColor3 = themes.TextColor,
                        TextSize = 12,
                        TextXAlignment = "Left",
                        TextTransparency = 0.10000000149012
                    })
                })

                button.MouseButton1Click:Connect(function()
                    if callback then
                        callback(value, function(...)
                            self:updateDropdown(dropdown, ...)
                        end)
                    end

                    self:updateDropdown(dropdown, value, nil, callback)
                end)

                entries = entries + 1
            end

            local frame = dropdown.List.Frame

            utility:Tween(dropdown, {Size = UDim2.new(1, 0, 0, (entries == 0 and 30) or math.clamp(entries, 0, 3) * 34 + 38)}, 0.3)
            utility:Tween(dropdown.Search.Button, {Rotation = list and 180 or 0}, 0.3)

            if entries > 3 then

                for i, button in pairs(dropdown.List.Frame:GetChildren()) do
                    if button:IsA("ImageButton") then
                        button.Size = UDim2.new(1, -6, 0, 30)
                    end
                end

                frame.CanvasSize = UDim2.new(0, 0, 0, (entries * 34) - 4)
                frame.ScrollBarImageTransparency = 0
            else
                frame.CanvasSize = UDim2.new(0, 0, 0, 0)
                frame.ScrollBarImageTransparency = 1
            end
        end)

    end
end

local win = library.new("Sleep Hub")

local page1 = win:NewPage("Main")
local section1 = page1:NewSecction("Auto_Farm")
local section2 = page1:NewSecction("Test2")
local MainAutoFarmFunction = AutoFarm(Ms,NameQuest,LevelQuest,NameMon,CFrameMon,CFrameQuest,"AutoFarmLevel")
spawn(function()
    while true do CheckQuest()
        if Auto_Farm then
            MainAutoFarmFunction:Update(Ms,NameQuest,LevelQuest,NameMon,CFrameMon,CFrameQuest)
        end
        fastWait(.05)
    end
end)

section1:Toggle("Auto Farm Level", getgenv().Setting["Auto Farm Level"],function(a)
    Auto_Farm = a
    MainAutoFarmFunction:UpdateFarmMode("AutoFarmLevel")
    if Auto_Farm then
        MainAutoFarmFunction:Start()
    else
        MainAutoFarmFunction:Stop()
    end
end)
FastTween = false
section1:Toggle("Very Fast Tween ( Not Recommend For KaiTun )", false,function(a)
    FastTween = a
end)

fastattack = true
section1:Toggle("Fast Attack", true,function(a)
    fastattack = a
end)

section1:ToggleToggle("Auto New World", getgenv().Setting["Auto New World"],function(vu)
    AutoNew = vu
end)
spawn(function()
    while wait() do
        if AutoNew then
            local MyLevel = game.Players.localPlayer.Data.Level.Value
            if MyLevel >= 700 and OldWorld and AutoNew then
                if Auto_Farm then
                    MainAutoFarmFunction:Stop()
                end
                if game.ReplicatedStorage.Remotes.CommF_:InvokeServer("DressrosaQuestProgress", "Dressrosa") ~= 0 then
                    if Workspace.Map.Ice.Door.Transparency == 1 then
                        if (CFrame.new(1347.7124, 37.3751602, -1325.6488).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 250 then
                            if game.Players.LocalPlayer.Backpack:FindFirstChild("Key") then
                                local tool = game.Players.LocalPlayer.Backpack:FindFirstChild("Key")
                                wait(.4)
                                game.Players.LocalPlayer.Character.Humanoid:EquipTool(tool)
                            end
                            DoorNewWorldTween = toTarget(CFrame.new(1347.7124, 37.3751602, -1325.6488).Position,CFrame.new(1347.7124, 37.3751602, -1325.6488))
                            if (CFrame.new(1347.7124, 37.3751602, -1325.6488).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 250 then
                                if DoorNewWorldTween then DoorNewWorldTween:Stop() end
                                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(1347.7124, 37.3751602, -1325.6488)
                            end
                        elseif game.Workspace.Enemies:FindFirstChild("Ice Admiral [Lv. 700] [Boss]") and game.Workspace.Map.Ice.Door.CanCollide == false and game.Workspace.Map.Ice.Door.Transparency == 1 and (CFrame.new(1347.7124, 37.3751602, -1325.6488).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 350 then
                            if DoorNewWorldTween then DoorNewWorldTween:Stop() end
                            CheckBoss = true
                            for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
                                if CheckBoss and v:IsA("Model") and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 and v.Name == "Ice Admiral [Lv. 700] [Boss]" then
                                    repeat wait()
                                        if (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 300 then
                                            Farmtween = toTarget(v.HumanoidRootPart.Position,v.HumanoidRootPart.CFrame)
                                        elseif (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
                                            if Farmtween then
                                                Farmtween:Stop()
                                            end
                                            EquipWeapon(SelectToolWeapon)
                                            Usefastattack = true
                                            if not game.Players.LocalPlayer.Character:FindFirstChild("HasBuso") then
                                                local args = {
                                                    [1] = "Buso"
                                                }
                                                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
                                            end
                                            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0)
                                            Click()
                                        end 
                                    until not CheckBoss or not v.Parent or v.Humanoid.Health <= 0 or AutoNew == false
                                    Usefastattack = false
                                end
                            end
                            CheckBoss = false
                        end 
                    else
                        if game.Players.LocalPlayer.Backpack:FindFirstChild("Key") or game.Players.LocalPlayer.Character:FindFirstChild("Key") then
                            DoorNewWorldTween = toTarget(CFrame.new(1347.7124, 37.3751602, -1325.6488).Position,CFrame.new(1347.7124, 37.3751602, -1325.6488))
                            if (CFrame.new(1347.7124, 37.3751602, -1325.6488).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 250 then
                                if DoorNewWorldTween then DoorNewWorldTween:Stop() end
                                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(1347.7124, 37.3751602, -1325.6488)
                                local args = {
                                    [1] = "DressrosaQuestProgress",
                                    [2] = "Detective"
                                }
                                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
                                wait(0.5)
                                if game.Players.LocalPlayer.Backpack:FindFirstChild("Key") then
                                    local tool = game.Players.LocalPlayer.Backpack:FindFirstChild("Key")
                                    wait(.4)
                                    game.Players.LocalPlayer.Character.Humanoid:EquipTool(tool)
                                end
                            end
                        else
                            AutoNewWorldTween = toTarget(CFrame.new(4849.29883, 5.65138149, 719.611877).Position,CFrame.new(4849.29883, 5.65138149, 719.611877))
                            if (CFrame.new(4849.29883, 5.65138149, 719.611877).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 250 then
                                if DoorNewWorldTween then DoorNewWorldTween:Stop() end
                                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(4849.29883, 5.65138149, 719.611877)
                                local args = {
                                    [1] = "DressrosaQuestProgress",
                                    [2] = "Detective"
                                }
                                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
                                wait(0.5)
                                if game.Players.LocalPlayer.Backpack:FindFirstChild("Key") then
                                    local tool = game.Players.LocalPlayer.Backpack:FindFirstChild("Key")
                                    wait(.4)
                                    game.Players.LocalPlayer.Character.Humanoid:EquipTool(tool)
                                end
                            end
                        end
                    end
                else
                    local args = {
                        [1] = "TravelDressrosa" -- OLD WORLD to NEW WORLD
                    }
                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
                end
            end
        end
    end
end)
elseif NewWorld then
    section1:Line()
    section1:Toggle("Auto Factory", getgenv().Setting["Auto Factory"],function(A)
        Factory = A
        if not Factory then
            FactoryCore = false
        end
    end)
    spawn(function()
        while wait() do
            if Factory then
                if game.Workspace.Enemies:FindFirstChild("Core") then
                    FactoryCore = true
                    MainAutoFarmFunction:Stop()
                    for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
                        if FactoryCore and v.Name == "Core" and v.Humanoid.Health > 0 then
                            repeat wait(.1)
                                if (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 350 then
                                    Farmtween = toTarget(v.HumanoidRootPart.Position,v.HumanoidRootPart.CFrame)
                                elseif (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 350 then
                                    if Farmtween then
                                        Farmtween:Stop()
                                    end
                                    EquipWeapon(SelectToolWeapon)
                                    Usefastattack = true
                                    if not game.Players.LocalPlayer.Character:FindFirstChild("HasBuso") then
                                        local args = {
                                            [1] = "Buso"
                                        }
                                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
                                    end
                                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame * CFrame.new(0, 10, 10)
                                    Click()
                                end
                            until not FactoryCore or v.Humanoid.Health <= 0 or Factory == false
                            Usefastattack = false
                        end
                    end
                elseif game.ReplicatedStorage:FindFirstChild("Core") and game.ReplicatedStorage:FindFirstChild("Core"):FindFirstChild("Humanoid") then
                    FactoryCore = true
                    MainAutoFarmFunction:Stop()
                    GOtween = toTarget(CFrame.new(448.46756, 199.356781, -441.389252).Position,CFrame.new(448.46756, 199.356781, -441.389252).CFrame)
                    if (CFrame.new(448.46756, 199.356781, -441.389252).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 350 then
                        if Farmtween then
                            GOtween:Stop()
                        end
                        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(448.46756, 199.356781, -441.389252)
                    end
                elseif Auto_Farm then
                    FactoryCore = false
                    MainAutoFarmFunction:Start()
                end
            end
        end
    end)
    section1:Toggle("Auto third World", getgenv().Setting["Auto third World"],function(vu)
        if SelectToolWeapon == "" and vu then
            Flux:Notification("Select Weapon First in Tab Auto Farm")
        else
            OldSelectToolWeapon = SelectToolWeapon
            Autothird = vu
        end	
    end)
    spawn(function()
        while wait() do
            if Autothird then
                local MyLevel = game.Players.localPlayer.Data.Level.Value
                if MyLevel >= 1500 and NewWorld and Autothird then
                    if Auto_Farm then
                        MainAutoFarmFunction:Stop()
                    end
                    if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BartiloQuestProgress","Bartilo") == 3 then
                        if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("GetUnlockables").FlamingoAccess ~= nil then
                            local args = {
                                [1] = "TravelZou" -- OLD WORLD to NEW WORLD
                            }
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
                            
                            if game:GetService("ReplicatedStorage").Remotes["CommF_"]:InvokeServer("ZQuestProgress", "Check") == 0 then
                                if game.Workspace.Enemies:FindFirstChild("rip_indra [Lv. 1500] [Boss]") then 	
                                    for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
                                        if v.Name == "rip_indra [Lv. 1500] [Boss]" and v:FindFirstChild("Humanoid")and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
                                            repeat wait()
                                                if (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 300 then
                                                    Farmtween = toTarget(v.HumanoidRootPart.Position,v.HumanoidRootPart.CFrame)
                                                elseif (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
                                                    if Farmtween then
                                                        Farmtween:Stop()
                                                    end
                                                    EquipWeapon(SelectToolWeapon)
                                                    Usefastattack = true
                                                    if not game.Players.LocalPlayer.Character:FindFirstChild("HasBuso") then
                                                        local args = {
                                                            [1] = "Buso"
                                                        }
                                                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
                                                    end
                                                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0)
                                                    Click()
                                                end 
                                            until not Autothird or not v.Parent or v.Humanoid.Health <= 0 
                                            wait(.5)
                                            asmrqq = 2
                                            repeat wait()
                                                local args = {
                                                    [1] = "TravelZou" -- OLD WORLD to NEW WORLD
                                                }
                                                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
                                            until asmrqq == 1
                                            Usefastattack = false
                                        end
                                    end
                                else -- SlashHit : rbxassetid://2453605589
                                    local string_1 = "ZQuestProgress";
                                    local string_2 = "Check";
                                    local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
                                    Target:InvokeServer(string_1, string_2);
                                    wait()
                                    local string_1 = "ZQuestProgress";
                                    local string_2 = "Begin";
                                    local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
                                    Target:InvokeServer(string_1, string_2);
                                end
                            elseif game:GetService("ReplicatedStorage").Remotes["CommF_"]:InvokeServer("ZQuestProgress", "Check") == 1 then
                                local args = {
                                    [1] = "TravelZou" -- OLD WORLD to NEW WORLD
                                }
                                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
                            else
                                if game.Workspace.Enemies:FindFirstChild("Don Swan [Lv. 1000] [Boss]") then 	
                                    for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
                                        if v.Name == "Don Swan [Lv. 1000] [Boss]" and v:FindFirstChild("Humanoid")and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
                                            repeat wait()
                                                if (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 300 then
                                                    Farmtween = toTarget(v.HumanoidRootPart.Position,v.HumanoidRootPart.CFrame)
                                                elseif (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
                                                    if Farmtween then
                                                        Farmtween:Stop()
                                                    end
                                                    EquipWeapon(SelectToolWeapon)
                                                    Usefastattack = true
                                                    if not game.Players.LocalPlayer.Character:FindFirstChild("HasBuso") then
                                                        local args = {
                                                            [1] = "Buso"
                                                        }
                                                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
                                                    end
                                                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0)
                                                    Click()
                                                end 
                                            until not Autothird or not v.Parent or v.Humanoid.Health <= 0 
                                            Usefastattack = false
                                        end
                                    end
                                else -- SlashHit : rbxassetid://2453605589
                                    TweenDonSwanthireworld = toTarget(CFrame.new(2288.802, 15.1870775, 863.034607).Position,CFrame.new(2288.802, 15.1870775, 863.034607))
                                    if (CFrame.new(2288.802, 15.1870775, 863.034607).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
                                        if TweenDonSwanthireworld then
                                            TweenDonSwanthireworld:Stop()
                                            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(2288.802, 15.1870775, 863.034607)
                                        end
                                    end
                                end
                            end
                        else
                            if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("GetUnlockables").FlamingoAccess == nil then
                                TabelDevilFruitStore = {}
                                TabelDevilFruitOpen = {}

                                for i,v in pairs(game:GetService("ReplicatedStorage").Remotes["CommF_"]:InvokeServer("getInventoryFruits")) do
                                    for i1,v1 in pairs(v) do
                                        if i1 == "Name" then 
                                            table.insert(TabelDevilFruitStore,v1)
                                        end
                                    end
                                end

                                for i,v in next,game.ReplicatedStorage:WaitForChild("Remotes").CommF_:InvokeServer("GetFruits") do
                                    if v.Price >= 1000000 then  
                                        table.insert(TabelDevilFruitOpen,v.Name)
                                    end
                                end

                                for i,DevilFruitOpenDoor in pairs(TabelDevilFruitOpen) do
                                    for i1,DevilFruitStore in pairs(TabelDevilFruitStore) do
                                        if DevilFruitOpenDoor == DevilFruitStore and game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("GetUnlockables").FlamingoAccess == nil then    
                                            if not game.Players.LocalPlayer.Backpack:FindFirstChild(DevilFruitStore) then   
                                                local string_1 = "LoadFruit";
                                                local string_2 = DevilFruitStore;
                                                local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
                                                Target:InvokeServer(string_1, string_2);
                                            else
                                                local string_1 = "TalkTrevor";
                                                local string_2 = "1";
                                                local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
                                                Target:InvokeServer(string_1, string_2);
                                                local string_1 = "TalkTrevor";
                                                local string_2 = "2";
                                                local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
                                                Target:InvokeServer(string_1, string_2);
                                                local string_1 = "TalkTrevor";
                                                local string_2 = "3";
                                                local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
                                                Target:InvokeServer(string_1, string_2);
                                            end
                                        end
                                    end
                                end

                                local string_1 = "TalkTrevor";
                                local string_2 = "1";
                                local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
                                Target:InvokeServer(string_1, string_2);
                                local string_1 = "TalkTrevor";
                                local string_2 = "2";
                                local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
                                Target:InvokeServer(string_1, string_2);
                                local string_1 = "TalkTrevor";
                                local string_2 = "3";
                                local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
                                Target:InvokeServer(string_1, string_2);
                            end
                        end
                    else
                        if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BartiloQuestProgress","Bartilo") == 0 then
                            if string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, "Swan Pirates") and string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, "50") and game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible == true then 
                                if game.Workspace.Enemies:FindFirstChild("Swan Pirate [Lv. 775]") then
                                    for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
                                        if v.Name == "Swan Pirate [Lv. 775]" then
                                            pcall(function()
                                                repeat wait()
                                                    if (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 300 then
                                                        Farmtween = toTarget(v.HumanoidRootPart.Position,v.HumanoidRootPart.CFrame)
                                                    elseif (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
                                                        if Farmtween then
                                                            Farmtween:Stop()
                                                        end
                                                        EquipWeapon(SelectToolWeapon)
                                                        Usefastattack = true
                                                        if not game.Players.LocalPlayer.Character:FindFirstChild("HasBuso") then
                                                            local args = {
                                                                [1] = "Buso"
                                                            }
                                                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
                                                        end
                                                        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0)
                                                        Click()
                                                    end 
                                                until not v.Parent or v.Humanoid.Health <= 0 or Autothird == false or game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible == false
                                                AutoBartiloBring = false
                                                Usefastattack = false
                                            end)
                                        end
                                    end
                                else
                                    Questtween = toTarget(CFrame.new(1057.92761, 137.614319, 1242.08069).Position,CFrame.new(1057.92761, 137.614319, 1242.08069))
                                    if (CFrame.new(1057.92761, 137.614319, 1242.08069).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
                                        if Questtween then
                                            Questtween:Stop()
                                        end
                                        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(1057.92761, 137.614319, 1242.08069)
                                    end
                                end
                            else
                                Bartilotween = toTarget(CFrame.new(-456.28952, 73.0200958, 299.895966).Position,CFrame.new(-456.28952, 73.0200958, 299.895966))
                                if ( CFrame.new(-456.28952, 73.0200958, 299.895966).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
                                    if Bartilotween then
                                        Bartilotween:Stop()
                                    end
                                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame =  CFrame.new(-456.28952, 73.0200958, 299.895966)
                                    local args = {
                                        [1] = "StartQuest",
                                        [2] = "BartiloQuest",
                                        [3] = 1
                                    }
                                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
                                end
                            end 
                        elseif game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BartiloQuestProgress","Bartilo") == 1 then
                            if game.Workspace.Enemies:FindFirstChild("Jeremy [Lv. 850] [Boss]") then
                                Ms = "Jeremy [Lv. 850] [Boss]"
                                for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
                                    if v.Name == Ms then
                                        repeat wait()
                                            if (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 300 then
                                                Farmtween = toTarget(v.HumanoidRootPart.Position,v.HumanoidRootPart.CFrame)
                                            elseif (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
                                                if Farmtween then
                                                    Farmtween:Stop()
                                                end
                                                EquipWeapon(SelectToolWeapon)
                                                Usefastattack = true
                                                if not game.Players.LocalPlayer.Character:FindFirstChild("HasBuso") then
                                                    local args = {
                                                        [1] = "Buso"
                                                    }
                                                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
                                                end
                                                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0)
                                                Click()
                                            end 
                                        until not v.Parent or v.Humanoid.Health <= 0 or Autothird == false
                                        Usefastattack = false
                                    end
                                end
                            else
                                Bartilotween = toTarget(CFrame.new(2099.88159, 448.931, 648.997375).Position,CFrame.new(2099.88159, 448.931, 648.997375))
                                if (CFrame.new(2099.88159, 448.931, 648.997375).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
                                    if Bartilotween then
                                        Bartilotween:Stop()
                                    end
                                    game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(2099.88159, 448.931, 648.997375)
                                end
                            end
                        elseif game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BartiloQuestProgress","Bartilo") == 2 then
                            if (CFrame.new(-1836, 11, 1714).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 300 then
                                Bartilotween = toTarget(CFrame.new(-1836, 11, 1714).Position,CFrame.new(-1836, 11, 1714))
                            elseif (CFrame.new(-1836, 11, 1714).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
                                if Bartilotween then
                                    Bartilotween:Stop()
                                end
                                game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1836, 11, 1714)
                                wait(.5)
                                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1850.49329, 13.1789551, 1750.89685)
                                wait(.1)
                                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1858.87305, 19.3777466, 1712.01807)
                                wait(.1)
                                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1803.94324, 16.5789185, 1750.89685)
                                wait(.1)
                                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1858.55835, 16.8604317, 1724.79541)
                                wait(.1)
                                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1869.54224, 15.987854, 1681.00659)
                                wait(.1)
                                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1800.0979, 16.4978027, 1684.52368)
                                wait(.1)
                                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1819.26343, 14.795166, 1717.90625)
                                wait(.1)
                                game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1813.51843, 14.8604736, 1724.79541)
                            end
                        end
                    end
                end
            end
        end
    end)
end


--AutoSuperHuman
section1:Line()
section1:Toggle("Auto Superhuman", getgenv().Setting["Auto Superhuman"],function(vu)
    Superhuman = vu
    if vu then
        local args = {
            [1] = "BuyElectro"
        }
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
    end
end)
AutoFarmTab:Toggle("Auto Superhuman [Full]", getgenv().Setting["Auto Superhuman [Full]"],function(vu)
    SuperhumanFull = vu
end)
--Auto Death step
section1:Toggle("Auto Death Step",getgenv().Setting["Auto Death Step"],function(vu)
    DeathStep = vu
    if vu then
        local args = {
            [1] = "BuyBlackLeg"
        }
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
    end
end)
	-- Auto Dargon Talon
	section1:Toggle("Auto Dragon Talon", getgenv().Setting["Auto Dragon Talon"],function(vu)
		DargonTalon = vu
		if vu then
			local args = {
				[1] = "BlackbeardReward",
				[2] = "DragonClaw",
				[3] = "2"
			}
			game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
		end
	end)
	-- Auto Electric clow
	section1:Toggle("Auto Electric Clow", getgenv().Setting["Auto Electric Clow"],function(vu)
		Electricclow = vu
		if vu then
			local args = {
				[1] = "BuyElectro"
			}
			game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
		end
	end)
    spawn(function()
		while wait(.25) do
			if Superhuman or SuperhumanFull and game.Players.LocalPlayer:FindFirstChild("WeaponAssetCache") then 
				if game.Players.LocalPlayer.Backpack:FindFirstChild("Combat") or game.Players.LocalPlayer.Character:FindFirstChild("Combat") then
					local args = {
						[1] = "BuyElectro"
					}
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
				end   
				if game.Players.LocalPlayer.Character:FindFirstChild("Superhuman") or game.Players.LocalPlayer.Backpack:FindFirstChild("Superhuman") then
					SelectToolWeapon = "Superhuman"
				end  
				if game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg") and game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg").Level.Value <= 299  then
					SelectToolWeapon = "Black Leg"
				end
				if game.Players.LocalPlayer.Backpack:FindFirstChild("Electro") and game.Players.LocalPlayer.Backpack:FindFirstChild("Electro").Level.Value <= 299  then
					SelectToolWeapon = "Electro"
				end
				if game.Players.LocalPlayer.Backpack:FindFirstChild("Fishman Karate") and game.Players.LocalPlayer.Backpack:FindFirstChild("Fishman Karate").Level.Value <= 299  then
					SelectToolWeapon = "Fishman Karate"
				end
				if game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Claw") and game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Claw").Level.Value <= 299  then
					SelectToolWeapon = "Dragon Claw"
				end
				if game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg") and game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg").Level.Value >= 300  then
					local args = {
						[1] = "BuyFishmanKarate"
					}
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
				end
				if game.Players.LocalPlayer.Character:FindFirstChild("Black Leg") and game.Players.LocalPlayer.Character:FindFirstChild("Black Leg").Level.Value >= 300  then
					local args = {
						[1] = "BuyFishmanKarate"
					}
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
				end
				if game.Players.LocalPlayer.Backpack:FindFirstChild("Electro") and game.Players.LocalPlayer.Backpack:FindFirstChild("Electro").Level.Value >= 100  then
					local args = {
						[1] = "BuyBlackLeg"
					}
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
				end
				if game.Players.LocalPlayer.Character:FindFirstChild("Electro") and game.Players.LocalPlayer.Character:FindFirstChild("Electro").Level.Value >= 300  then
					local args = {
						[1] = "BuyBlackLeg"
					}
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
				end
				if game.Players.LocalPlayer.Backpack:FindFirstChild("Fishman Karate") and game.Players.LocalPlayer.Backpack:FindFirstChild("Fishman Karate").Level.Value >= 300  then
					if SuperhumanFull and game.Players.LocalPlayer.Data.Fragments.Value < 1500 then
						if game.Players.LocalPlayer.Data.Level.Value > 1100 then
							RaidsSelected = "Flame"
							AutoRaids = true
							RaidsArua = true
						end
					else
						AutoRaids = false
						RaidsArua = false
						local args = {
							[1] = "BlackbeardReward",
							[2] = "DragonClaw",
							[3] = "2"
						}
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
					end
				end
				if game.Players.LocalPlayer.Character:FindFirstChild("Fishman Karate") and game.Players.LocalPlayer.Character:FindFirstChild("Fishman Karate").Level.Value >= 300  then
					if SuperhumanFull and game.Players.LocalPlayer.Data.Fragments.Value < 1500 then
						if game.Players.LocalPlayer.Data.Level.Value > 1100 then
							RaidsSelected = "Flame"
							AutoRaids = true
							RaidsArua = true
						end
					else
						AutoRaids = false
						RaidsArua = false
						local args = {
							[1] = "BlackbeardReward",
							[2] = "DragonClaw",
							[3] = "2"
						}
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
					end
				end
				if game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Claw") and game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Claw").Level.Value >= 300  then
					local args = {
						[1] = "BuySuperhuman"
					}
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
				end
				if game.Players.LocalPlayer.Character:FindFirstChild("Dragon Claw") and game.Players.LocalPlayer.Character:FindFirstChild("Dragon Claw").Level.Value >= 300  then
					local args = {
						[1] = "BuySuperhuman"
					}
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
				end 
			end
			if DeathStep and game.Players.LocalPlayer:FindFirstChild("WeaponAssetCache") then
				if game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg") and game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg").Level.Value >= 400 then
					local args = {
						[1] = "BuyDeathStep"
					}
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
					SelectToolWeapon = "Death Step"
				end  
				if game.Players.LocalPlayer.Character:FindFirstChild("Black Leg") and game.Players.LocalPlayer.Character:FindFirstChild("Black Leg").Level.Value >= 400 then
					local args = {
						[1] = "BuyDeathStep"
					}
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
					
					SelectToolWeapon = "Death Step"
				end  
				if game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg") and game.Players.LocalPlayer.Backpack:FindFirstChild("Black Leg").Level.Value < 400 then
					SelectToolWeapon = "Black Leg"
				end 
			end
			if DargonTalon and game.Players.LocalPlayer:FindFirstChild("WeaponAssetCache") then
				if game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Claw") and game.Players.LocalPlayer.Backpack:FindFirstChild("Dragon Claw").Level.Value <= 399 and game.Players.LocalPlayer.Character.Humanoid.Health > 0 then
					SelectToolWeapon = "Dragon Claw"
				end
				if game.Players.LocalPlayer.Character:FindFirstChild("Dragon Claw") and game.Players.LocalPlayer.Character:FindFirstChild("Dragon Claw").Level.Value <= 399 and game.Players.LocalPlayer.Character.Humanoid.Health > 0 then
					SelectToolWeapon = "Dragon Claw"
				end
	
				if game.Players.LocalPlayer.Character:FindFirstChild("Dragon Claw") and game.Players.LocalPlayer.Character:FindFirstChild("Dragon Claw").Level.Value >= 400 and game.Players.LocalPlayer.Character.Humanoid.Health > 0 then
					SelectToolWeapon = "Dragon Claw"
					if game.ReplicatedStorage.Remotes.CommF_:InvokeServer("BuyDragonTalon", true) == 3 then
						local string_1 = "Bones";
						local string_2 = "Buy";
						local number_1 = 1;
						local number_2 = 1;
						local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
						Target:InvokeServer(string_1, string_2, number_1, number_2);
	
						local string_1 = "BuyDragonTalon";
						local bool_1 = true;
						local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
						Target:InvokeServer(string_1, bool_1);
					elseif game.ReplicatedStorage.Remotes.CommF_:InvokeServer("BuyDragonTalon", true) == 1 then
						game.ReplicatedStorage.Remotes.CommF_:InvokeServer("BuyDragonTalon")
					else
						local string_1 = "BuyDragonTalon";
						local bool_1 = true;
						local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
						Target:InvokeServer(string_1, bool_1);
						local string_1 = "BuyDragonTalon";
						local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
						Target:InvokeServer(string_1);
					end 
				end
			end
			if Electricclow and game.Players.LocalPlayer:FindFirstChild("WeaponAssetCache") then
				if game.Players.LocalPlayer.Backpack:FindFirstChild("Electro") and game.Players.LocalPlayer.Backpack:FindFirstChild("Electro").Level.Value < 400 then
					SelectToolWeapon = "Electro"
				end  
				if game.Players.LocalPlayer.Character:FindFirstChild("Electro") and game.Players.LocalPlayer.Character:FindFirstChild("Electro").Level.Value < 400 then
					SelectToolWeapon = "Electro"
				end  
				if game.Players.LocalPlayer.Backpack:FindFirstChild("Electro") and game.Players.LocalPlayer.Backpack:FindFirstChild("Electro").Level.Value >= 400 then
					local v175 = game.ReplicatedStorage.Remotes.CommF_:InvokeServer("BuyElectricClaw", true);
					if v175 == 4 then
						local v176 = game.ReplicatedStorage.Remotes.CommF_:InvokeServer("BuyElectricClaw", "Start");
						if v176 == nil then
							game.Players.localPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-12548, 337, -7481)
						end
					else
						local string_1 = "BuyElectricClaw";
						local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
						Target:InvokeServer(string_1);
					end
				end
				if game.Players.LocalPlayer.Character:FindFirstChild("Electro") and game.Players.LocalPlayer.Character:FindFirstChild("Electro").Level.Value >= 400 then
					local v175 = game.ReplicatedStorage.Remotes.CommF_:InvokeServer("BuyElectricClaw", true);
					if v175 == 4 then
						local v176 = game.ReplicatedStorage.Remotes.CommF_:InvokeServer("BuyElectricClaw", "Start");
						if v176 == nil then
							game.Players.localPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-12548, 337, -7481)
						end
					else
						local string_1 = "BuyElectricClaw";
						local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
						Target:InvokeServer(string_1);
					end
				end
			end
		end
	end)
	-- Auto Buy Legendary Sword
	section1:Toggle("Auto Buy Legendary Sword", getgenv().Setting["Auto Buy Legendary Sword"],function(Value)
		Legendary = Value    
	end)
	section1:Toggle("Auto Buy Legendary Sword Hop", getgenv().Setting["Auto Buy Legendary Sword Hop"],function(Value)
		LegendaryHop = Value    
	end)
	-- Auto Buy Enhancement
	section1:Toggle("Auto Buy Enhancement", getgenv().Setting["Auto Buy Enhancement"],function(Value)
		Enhancement = Value    
	end)
    spawn(function()
		while wait() do
			if Legendary then
				local args = {
					[1] = "LegendarySwordDealer",
					[2] = "2"
				}
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
			end 
			if LegendaryHop then
				local args = {
					[1] = "LegendarySwordDealer",
					[2] = "2"
				}
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
				wait(7)
				local args = {
					[1] = "LegendarySwordDealer",
					[2] = "2"
				}
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
				wait()
				local PlaceID = game.PlaceId
				local AllIDs = {}
				local foundAnything = ""
				local actualHour = os.date("!*t").hour
				local Deleted = false
				function TPReturner()
					local Site;
					if foundAnything == "" then
						Site = game.HttpService:JSONDecode(game:HttpGet('https://games.roblox.com/v1/games/' .. PlaceID .. '/servers/Public?sortOrder=Asc&limit=100'))
					else
						Site = game.HttpService:JSONDecode(game:HttpGet('https://games.roblox.com/v1/games/' .. PlaceID .. '/servers/Public?sortOrder=Asc&limit=100&cursor=' .. foundAnything))
					end
					local ID = ""
					if Site.nextPageCursor and Site.nextPageCursor ~= "null" and Site.nextPageCursor ~= nil then
						foundAnything = Site.nextPageCursor
					end
					local num = 0;
					for i,v in pairs(Site.data) do
						local Possible = true
						ID = tostring(v.id)
						if tonumber(v.maxPlayers) > tonumber(v.playing) then
							for _,Existing in pairs(AllIDs) do
								if num ~= 0 then
									if ID == tostring(Existing) then
										Possible = false
									end
								else
									if tonumber(actualHour) ~= tonumber(Existing) then
										local delFile = pcall(function()
											-- delfile("NotSameServers.json")
											AllIDs = {}
											table.insert(AllIDs, actualHour)
										end)
									end
								end
								num = num + 1
							end
							if Possible == true then
								table.insert(AllIDs, ID)
								wait()
								pcall(function()
									-- writefile("NotSameServers.json", game:GetService('HttpService'):JSONEncode(AllIDs))
									wait()
									game:GetService("TeleportService"):TeleportToPlaceInstance(PlaceID, ID, game.Players.LocalPlayer)
								end)
								wait(.1)
							end
						end
					end
				end
				function Teleport() 
					while wait() do
						pcall(function()
							TPReturner()
							if foundAnything ~= "" then
								TPReturner()
							end
						end)
					end
				end
				Teleport()
				wait(3)
			end 
			if Enhancement then
				local args = {
					[1] = "ColorsDealer",
					[2] = "2"
				}
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
			end 
		end
	end) 
    section2:Toogle("Auto Farm Devil Fruit Mastery",autofarmmasterybf,function(v)
		if SelectToolWeapon == "" and v then
			VLib:Notification("Select Weapon First")
		else
			MasteryDevilFruit = v
			MainAutoFarmFunction:UpdateFarmMode("AutoFarmDevilfruit")
			if MasteryDevilFruit then
				MainAutoFarmFunction:Start()
			else
				MainAutoFarmFunction:Stop()
			end
		end	
	end)
    section2:Toggle("Auto Farm Gun Mastery",autofarmmasterybf,function(v)
		if SelectToolWeapon == "" and v then
			VLib:Notification("Select Weapon First")
		else
			MasteryGun = v
			MainAutoFarmFunction:UpdateFarmMode("AutoFarmGun")
			if MasteryGun then
				MainAutoFarmFunction:Start()
			else
				MainAutoFarmFunction:Stop()
			end
		end	
	end)
    



















section1:Button("Button", function(t)
    print("asd")
end)

section1:Textbox("Notification", "Default", function(value, kuy)
    print("Input", value)

if focusLost then
    win:Notify("Test1", "Hello", value)
    end
end)
     
section2:Keybind("Toggle Keybind", Enum.KeyCode.RightControl, function()
    print("Activated Keybind")
    win:toggle()
end, function()
    print("Changed Keybind")
end)

return library
