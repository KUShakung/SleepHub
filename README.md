local placeId = game.PlaceId
if placeId == 2753915549 or placeId == 4442272183 or placeId == 7449423635 then
    BF = true
elseif placeId == 3237168 then
    OPL = true
elseif placeId == 914010731 then
    RO = true
elseif placeId == 6299805723 then
    AFS = true
elseif placeId == 4520749081 or placeId == 6381829480 or placeId == 5931540094 then
	KL = true
elseif placeId == 4042427666 then
    ANS = true
elseif placeId == 2809202155 then
    YBA = true
    print("\n game not support")
end
spawn(function()
	while wait() do 
		print("JayKung#8973 ")
	end
end)
if BF then
	repeat wait() until game:IsLoaded()
	if getgenv().Setting then else
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
    
    if not game:IsLoaded() then game.Loaded:Wait() end
	repeat wait() until game.Players
	repeat wait() until game.Players.LocalPlayer
	repeat wait() until game.ReplicatedStorage
	repeat wait() until game.ReplicatedStorage:FindFirstChild("Remotes");
	repeat wait() until game.Players.LocalPlayer:FindFirstChild("PlayerGui");
	repeat wait() until game.Players.LocalPlayer.PlayerGui:FindFirstChild("Main");
	repeat wait()
		if game:GetService("Players").LocalPlayer.PlayerGui:WaitForChild("Main").ChooseTeam.Visible == true then
			if getgenv().Setting["Join Team"] == "Pirate" then
				game:GetService("Players")["LocalPlayer"].PlayerGui.Main.ChooseTeam.Container.Pirates.Frame.ViewportFrame.TextButton.Size = UDim2.new(0, 10000, 0, 10000)
				game:GetService("Players")["LocalPlayer"].PlayerGui.Main.ChooseTeam.Container.Pirates.Frame.ViewportFrame.TextButton.Position = UDim2.new(-4, 0, -5, 0)
				game:GetService("Players")["LocalPlayer"].PlayerGui.Main.ChooseTeam.Container.Pirates.Frame.ViewportFrame.TextButton.BackgroundTransparency = 1
				wait(.5)
				game:GetService'VirtualUser':Button1Down(Vector2.new(99,99))
				game:GetService'VirtualUser':Button1Up(Vector2.new(99,99))
			elseif getgenv().Setting["Join Team"] == "Marine" then
				game:GetService("Players")["LocalPlayer"].PlayerGui.Main.ChooseTeam.Container.Marines.Frame.ViewportFrame.TextButton.Size = UDim2.new(0, 10000, 0, 10000)
				game:GetService("Players")["LocalPlayer"].PlayerGui.Main.ChooseTeam.Container.Marines.Frame.ViewportFrame.TextButton.Position = UDim2.new(-4, 0, -5, 0)
				game:GetService("Players")["LocalPlayer"].PlayerGui.Main.ChooseTeam.Container.Marines.Frame.ViewportFrame.TextButton.BackgroundTransparency = 1
				wait(.5)
				game:GetService'VirtualUser':Button1Down(Vector2.new(99,99))
				game:GetService'VirtualUser':Button1Up(Vector2.new(99,99))
			else
				game:GetService("Players")["LocalPlayer"].PlayerGui.Main.ChooseTeam.Container.Pirates.Frame.ViewportFrame.TextButton.Size = UDim2.new(0, 10000, 0, 10000)
				game:GetService("Players")["LocalPlayer"].PlayerGui.Main.ChooseTeam.Container.Pirates.Frame.ViewportFrame.TextButton.Position = UDim2.new(-4, 0, -5, 0)
				game:GetService("Players")["LocalPlayer"].PlayerGui.Main.ChooseTeam.Container.Pirates.Frame.ViewportFrame.TextButton.BackgroundTransparency = 1
				wait(.5)
				game:GetService'VirtualUser':Button1Down(Vector2.new(99,99))
				game:GetService'VirtualUser':Button1Up(Vector2.new(99,99))
			end
		end
	until game.Players.LocalPlayer.Team ~= nil and game:IsLoaded() 
	
	wait(1)

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

	--------------------------------------------------------------------------------------------------------------------------------
	-- Function
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

            local win = library.new("Sleep Hub")

            local page1 = win:NewPage("AutoFarm")
            local section1 = page1:NewSecction("AutoFarm")
            local section3 = page1:NewSecction("AutoFarm")
            local section4 = page1:NewSecction("AutoFarm")
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

            if OldWorld then

                -- Auto New World
                section2:Toggle("Auto New World", getgenv().Setting["Auto New World"],function(vu)
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
                section3:Toggle("Auto Factory", getgenv().Setting["Auto Factory"],function(A)
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
                AutoFarmTab:Toggle("Auto third World", getgenv().Setting["Auto third World"],function(vu)
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
            local page2 = win:NewPage("AutoFarmMisc")
            local section2 = page2:NewSecction("Auto Quest Flower",true)
            section2:Toggle("Auto Quest Flower",_G.AutoQuestFlower,function(Bool)
                if game.Players.LocalPlayer.Data.Level.Value < 850 and Bool then
                    Flux:Notification("Need Level More 850")
                else
                    if SelectToolWeapon == "" and Bool then
                        Flux:Notification("Selected Weapon First")
                    elseif  game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BartiloQuestProgress","Bartilo") ~= 3 and Bool == true then
                        Flux:Notification("Quest Bartilo Not Successfully")
                    elseif game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Alchemist","3") == -2 and Bool == true then
                        Flux:Notification("Evo Race V.2 Successfully")
                    else
                        AutoEvoRace2 = Bool
                    end
                end
            end)
            spawn(function()
                while wait() do
                    if AutoEvoRace2 then
                        if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Alchemist","3") ~= -2 then
                            if game.Players.LocalPlayer.Backpack:FindFirstChild("Flower 1") and game.Players.LocalPlayer.Backpack:FindFirstChild("Flower 2") and game.Players.LocalPlayer.Backpack:FindFirstChild("Flower 3") then
                                if (CFrame.new(-2777.6001, 72.9661407, -3571.42285).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 300 then
                                    Farmtween = toTarget(CFrame.new(-2777.6001, 72.9661407, -3571.42285).Position,CFrame.new(-2777.6001, 72.9661407, -3571.42285))
                                elseif (CFrame.new(-2777.6001, 72.9661407, -3571.42285).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
                                    if Farmtween then
                                        Farmtween:Stop()
                                    end
                                    game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-2777.6001, 72.9661407, -3571.42285)
                                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Alchemist","3")
                                end 
                            else
                                game.ReplicatedStorage.Remotes.CommF_:InvokeServer("Alchemist", "1")
                                game.ReplicatedStorage.Remotes.CommF_:InvokeServer("Alchemist", "2")
                                if not game.Players.LocalPlayer.Backpack:FindFirstChild("Flower 1") then
                                    if workspace.Flower1.Transparency ~= 1 then
                                        if (workspace.Flower1.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 300 then
                                            Farmtween = toTarget(workspace.Flower1.Position,workspace.Flower1.CFrame)
                                        elseif (workspace.Flower1.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
                                            if Farmtween then
                                                Farmtween:Stop()
                                            end
                                            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = workspace.Flower1.CFrame
                                        end 
                                    end
                                end 
                                if not game.Players.LocalPlayer.Backpack:FindFirstChild("Flower 2") then
                                    if workspace.Flower2.Transparency ~= 1 then
                                        if (workspace.Flower2.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 300 then
                                            Farmtween = toTarget(workspace.Flower2.Position,workspace.Flower2.CFrame)
                                        elseif (workspace.Flower2.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
                                            if Farmtween then
                                                Farmtween:Stop()
                                            end
                                            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = workspace.Flower2.CFrame
                                        end 
                                    end
                                end
                                if not game.Players.LocalPlayer.Backpack:FindFirstChild("Flower 3") then
                                    if game.Workspace.Enemies:FindFirstChild("Swan Pirate [Lv. 775]") then
                                        for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
                                            if v.Name == "Swan Pirate [Lv. 775]" and v:FindFirstChild("Humanoid") and v.Humanoid.Health >= 0 then
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
                                                            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame * CFrame.new(0, 10, 10)
                                                            Click()
                                                        end 
                                                    until not v.Parent or v.Humanoid.Health <= 0 or AutoEvoRace2 == false or LocalPlayer.Backpack:FindFirstChild("Flower 3")
                                                    AutoEvoBring = false
                                                    Usefastattack = false
                                                end)
                                            end
                                        end
                                    else
                                        if (CFrame.new(1057.92761, 137.614319, 1242.08069).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 300 then
                                            Farmtween = toTarget(CFrame.new(1057.92761, 137.614319, 1242.08069).Position,CFrame.new(1057.92761, 137.614319, 1242.08069))
                                        elseif (CFrame.new(1057.92761, 137.614319, 1242.08069).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
                                            if Farmtween then
                                                Farmtween:Stop()
                                            end
                                            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(1057.92761, 137.614319, 1242.08069)
                                        end 
                                    end
                                end
                            end
                        end
                    end
                end
            end)
            local section3 = page2:NewSecction("Auto true triple Katana",true)
            section3:Toggle("Auto true triple Katana",false,function(Value)
                truetripleKatana = Value    
            end)
            spawn(function()
                while wait() do
                    if truetripleKatana then
                        local string_1 = "MysteriousMan";
                        local string_2 = "2";
                        local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
                        Target:InvokeServer(string_1, string_2);   
                    end 
                end
            end)
	-- Auto Rengoku
	RengokuWeapon = ""
    local section4 = page2:NewSecction("Auto Rengoku",true)
	section4:Toggle("Auto Rengoku",_G.AutoRengoku,function(v)
		if not NewWorld then
			Flux:Notification("Use in New World")
		elseif SelectToolWeapon == "" and v then
			Flux:Notification("Select Wapon First")
		else
			AutoRengoku = v
		end 
	end)
	spawn(function()
		while wait() do
			if AutoRengoku then
				if game.Players.LocalPlayer.Backpack:FindFirstChild("Hidden Key") or  game.Players.LocalPlayer.Character:FindFirstChild("Hidden Key") then
					EquipWeapon("Hidden Key")
					if (CFrame.new(6571.81885, 296.689758, -6966.76514).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 300 then
						Farmtween = toTarget(CFrame.new(6571.81885, 296.689758, -6966.76514).Position,CFrame.new(6571.81885, 296.689758, -6966.76514))
					elseif (CFrame.new(6571.81885, 296.689758, -6966.76514).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
						if Farmtween then
							Farmtween:Stop()
						end
						game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(6571.81885, 296.689758, -6966.76514, 0.825126112, 8.412257e-10, 0.564948559, -2.42370835e-08, 1, 3.39100339e-08, -0.564948559, -4.16727595e-08, 0.825126112)
					end 
				elseif game.Workspace.Enemies:FindFirstChild("Snow Lurker [Lv. 1375]") then
					for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
						if AutoRengoku and v.Name == "Snow Lurker [Lv. 1375]" and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
							repeat wait()
								if (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 300 then
									Farmtween = toTarget(v.HumanoidRootPart.Position,v.HumanoidRootPart.CFrame)
									StatrMagnetRengoku = false
								elseif (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
									if Farmtween then
										Farmtween:Stop()
									end
									PosMonRengoku = v.HumanoidRootPart.CFrame
									EquipWeapon(SelectToolWeapon)
									Usefastattack = true
									StatrMagnetRengoku = true
									if not game.Players.LocalPlayer.Character:FindFirstChild("HasBuso") then
										local args = {
											[1] = "Buso"
										}
										game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
									end
									game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame * CFrame.new(0, 10, 10)
									Click()
								end 
							until game.Players.LocalPlayer.Backpack:FindFirstChild("Hidden Key") or AutoRengoku == false or not v.Parent or v.Humanoid.Health <= 0
							StatrMagnetRengoku = false
							Usefastattack = false
							if (CFrame.new(5518.00684, 60.5559731, -6828.80518).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 300 then
								Farmtween = toTarget(CFrame.new(5518.00684, 60.5559731, -6828.80518).Position,CFrame.new(5518.00684, 60.5559731, -6828.80518))
							elseif (CFrame.new(5518.00684, 60.5559731, -6828.80518).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
								if Farmtween then
									Farmtween:Stop()
								end
								game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(5518.00684, 60.5559731, -6828.80518, 0.825126112, 8.412257e-10, 0.564948559, -2.42370835e-08, 1, 3.39100339e-08, -0.564948559, -4.16727595e-08, 0.825126112)
							end 
						end
					end
				else
					StatrMagnetRengoku = false
					if (CFrame.new(5518.00684, 60.5559731, -6828.80518).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 300 then
						Farmtween = toTarget(CFrame.new(5518.00684, 60.5559731, -6828.80518).Position,CFrame.new(5518.00684, 60.5559731, -6828.80518))
					elseif (CFrame.new(5518.00684, 60.5559731, -6828.80518).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
						if Farmtween then
							Farmtween:Stop()
						end
						game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame =CFrame.new(5518.00684, 60.5559731, -6828.80518, -0.650781393, -3.64292951e-08, 0.759265184, -4.07668654e-09, 1, 4.44854642e-08, -0.759265184, 2.58550248e-08, -0.650781393)
					end 
				end
			end
		end
	end)
	-- Auto Farm Ectoplasm
    local section5 = page2:NewSecction("Auto Farm Ectoplasm",true)
	section5:Toggle("Auto Farm Ectoplasm",_G.AutoFarmEctoplasm,function(A)
		if NewWorld then
			AutoFramEctoplasm = A
		else
			Flux:Notification("Use in New World")
		end
	end)
	spawn(function()
		while wait() do
			if AutoFramEctoplasm then
				if game.Workspace.Enemies:FindFirstChild("Ship Deckhand [Lv. 1250]") or game.Workspace.Enemies:FindFirstChild("Ship Engineer [Lv. 1275]") or game.Workspace.Enemies:FindFirstChild("Ship Steward [Lv. 1300]") or game.Workspace.Enemies:FindFirstChild("Ship Officer [Lv. 1325]") then
					for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
						if string.find(v.Name, "Ship") then
							repeat wait()
								Usefastattack = true
								if string.find(v.Name, "Ship") then
									if (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 300 then
										Farmtween = toTarget(v.HumanoidRootPart.Position,v.HumanoidRootPart.CFrame)
										StatrMagnetEctoplasm = false
									elseif (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
										if Farmtween then
											Farmtween:Stop()
										end
										EquipWeapon(SelectToolWeapon)
										PosMonEctoplasm = v.HumanoidRootPart.CFrame
										Usefastattack = true
										if not game.Players.LocalPlayer.Character:FindFirstChild("HasBuso") then
											local args = {
												[1] = "Buso"
											}
											game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
										end
										StatrMagnetEctoplasm = true
										game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame * CFrame.new(0, 10, 10)
										Click()
									end 
								else
									StatrMagnetEctoplasm = false
									if (CFrame.new(920.14447, 129.581833, 33442.168).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 300 then
										Farmtween = toTarget(CFrame.new(920.14447, 129.581833, 33442.168).Position,CFrame.new(920.14447, 129.581833, 33442.168))
									elseif (CFrame.new(920.14447, 129.581833, 33442.168).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
										if Farmtween then
											Farmtween:Stop()
										end
										game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(920.14447, 129.581833, 33442.168, -0.999913812, 0, -0.0131403487, 0, 1, 0, 0.0131403487, 0, -0.999913812)
									end 
								end
							until AutoFramEctoplasm == false or not v.Parent or v.Humanoid.Health <= 0
							Usefastattack = false
							StatrMagnetEctoplasm = false
							if (CFrame.new(920.14447, 129.581833, 33442.168).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 300 then
								Farmtween = toTarget(CFrame.new(920.14447, 129.581833, 33442.168).Position,CFrame.new(920.14447, 129.581833, 33442.168))
							elseif (CFrame.new(920.14447, 129.581833, 33442.168).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
								if Farmtween then
									Farmtween:Stop()
								end
								game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(920.14447, 129.581833, 33442.168, -0.999913812, 0, -0.0131403487, 0, 1, 0, 0.0131403487, 0, -0.999913812)
							end 
						end
					end
				else
					if (CFrame.new(920.14447, 129.581833, 33442.168).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 300 then
						Farmtween = toTarget(CFrame.new(920.14447, 129.581833, 33442.168).Position,CFrame.new(920.14447, 129.581833, 33442.168))
					elseif (CFrame.new(920.14447, 129.581833, 33442.168).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
						if Farmtween then
							Farmtween:Stop()
						end
						game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(920.14447, 129.581833, 33442.168, -0.999913812, 0, -0.0131403487, 0, 1, 0, 0.0131403487, 0, -0.999913812)
					end 
				end
			end
		end
	end)
    local section6 = page2:NewSecction("Auto Buy Bizarre Rifle")
	section6:Toggle("Auto Buy Bizarre Rifle",_G.AutoBuyBizarreRifle,function(A)
		if NewWorld then
			AutoBuyBizarreRifle = A
		else
			Flux:Notification("Use in New World")
		end
	end)
	section6:Toggle("Auto Buy Ghoul Mask",_G.AutoBuyGhoulMask,function(A)
		if NewWorld then
			AutoBuyGhoulMask = A
		else
			Flux:Notification("Use in New World")
		end
	end)
	section6:Toggle("Auto Buy Midnight Blade",_G.AutoBuyMidnightBlade,function(A)
		if NewWorld then
			AutoBuyMidnightBlade = A
		else
			Flux:Notification("Use in New World")
		end
	end)
	spawn(function()
		while wait() do
			if AutoBuyBizarreRifle then
				local args = {
					[1] = "Ectoplasm",
					[2] = "Buy",
					[3] = 1
				}
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
			end
			if AutoBuyGhoulMask then
				local args = {
					[1] = "Ectoplasm",
					[2] = "Buy",
					[3] = 2
				}
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
			end
			if AutoBuyMidnightBlade then
				local args = {
					[1] = "Ectoplasm",
					[2] = "Buy",
					[3] = 3
				}
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
			end
		end
	end)
    local section7 = page2:NewSecction("Sea 3 (Thire World)",true)
	-- Auto Buddy Swords
	local section7 = page2:NewSecction("🍬 Buddy Swords 🍬")
	section7:Toggle("Auto Buddy Swords",_G.AutoBuddySwords,function(v)
		if not ThreeWorld then
			library:Notification("Notification","Use In Thire World","Okey")    
		else
			AutoBuddySwords = v
		end 
	end)
	section7:Toggle("Auto Buddy Swords HOP",_G.AutoBuddySwordsHop,function(v)
		if not ThreeWorld then
			library:Notification("Notification","Use In Thire World","Okey")    
		else
			AutoBuddySwords = v
			AutoBuddySwordsHOP = v
		end 
	end)
	spawn(function()
		while wait() do
			if AutoBuddySwords then
				if game.ReplicatedStorage:FindFirstChild("Cake Queen [Lv. 2175] [Boss]") or game.Workspace.Enemies:FindFirstChild("Cake Queen [Lv. 2175] [Boss]") then
					if game.Workspace.Enemies:FindFirstChild("Cake Queen [Lv. 2175] [Boss]") then
						for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
							if AutoBuddySwords and v.Name == "Cake Queen [Lv. 2175] [Boss]" and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
								repeat wait()
									Farmtween = toTarget(v.HumanoidRootPart.Position,v.HumanoidRootPart.CFrame)
									if (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
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
										game:GetService'VirtualUser':CaptureController()
										game:GetService'VirtualUser':Button1Down(Vector2.new(1280, 672))
									end 
								until not AutoBuddySwords or v.Humanoid.Health <= 0 or not v.Parent
								Usefastattack = false
							end
						end
					else
						BuddySwordsTween = toTarget(CFrame.new(-821, 66, -10965).Position,CFrame.new(-821, 66, -10965))
						if (CFrame.new(-821, 66, -10965).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 250 then
							if BuddySwordsTween then
								BuddySwordsTween:Stop()
							end
							game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-821, 66, -10965)
						end
					end
				elseif AutoBuddySwordsHOP then
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
									wait(1)
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
				end
			end
		end
	end)
	local section8 = page2:NewSecction("🎃 Hallow Ween 🎃")
	section8:Toggle("Auto Farm Bone",_G.AutoFarmBone,function(vu)
		if not ThreeWorld and vu then
			Flux:Notification('Use In Sea 3 (Three World)')
		else 
			AutoFarmBone = vu
			MainAutoFarmBone = vu
		end  
	end)
	spawn(function()
		while wait() do
			if AutoFarmBone then
				if game:GetService("Workspace").Enemies:FindFirstChild("Reborn Skeleton [Lv. 1975]") or game:GetService("Workspace").Enemies:FindFirstChild("Living Zombie [Lv. 2000]") or game:GetService("Workspace").Enemies:FindFirstChild("Demonic Soul [Lv. 2025]") or game:GetService("Workspace").Enemies:FindFirstChild("Posessed Mummy [Lv. 2050]") then
					for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
						if AutoFarmBone and (v.Name == "Reborn Skeleton [Lv. 1975]" or v.Name == "Living Zombie [Lv. 2000]" or v.Name == "Demonic Soul [Lv. 2025]" or v.Name == "Posessed Mummy [Lv. 2050]") and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 then
							repeat wait()
								if (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 300 then
									Farmtween = toTarget(v.HumanoidRootPart.Position,v.HumanoidRootPart.CFrame)
									MagnetFarmBone = false
									Usefastattack = false
								elseif (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
									if Farmtween then
										Farmtween:Stop()
									end
									Usefastattack = true
									PosFarmBone = v.HumanoidRootPart.CFrame
									EquipWeapon(SelectToolWeapon)
									if not game.Players.LocalPlayer.Character:FindFirstChild("HasBuso") then
										local args = {
											[1] = "Buso"
										}
										game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
									end
									game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0)
									Click()
									MagnetFarmBone = true
								end
							until not AutoFarmBone or not v.Parent or v.Humanoid.Health <= 0
							Usefastattack = false
							MagnetFarmBone = false
						end
					end
				else
					MagnetFarmBone = false
					Usefastattack = false
					Questtween = toTarget(CFrame.new(-9506.14648, 172.130661, 6101.79053).Position,CFrame.new(-9506.14648, 172.130661, 6101.79053))
					if (CFrame.new(-9506.14648, 172.130661, 6101.79053).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
						if Questtween then
							Questtween:Stop()
						end
						game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-9506.14648, 172.130661, 6101.79053, -0.999731541, 0, -0.0231563263, 0, 1, 0, 0.0231563263, 0, -0.999731541)
					end
				end
			end
		end
	end)
	spawn(function()
		while wait() do
			if MagnetFarmBone and AutoFarmBone then
				for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
					if MagnetFarmBone  and AutoFarmBone and (v.Name == "Reborn Skeleton [Lv. 1975]" or v.Name == "Living Zombie [Lv. 2000]" or v.Name == "Demonic Soul [Lv. 2025]" or v.Name == "Posessed Mummy [Lv. 2050]") and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 and (v.HumanoidRootPart.Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 350 then
						v.HumanoidRootPart.CFrame = PosFarmBone
						v.HumanoidRootPart.CanCollide = false
					end
				end
			end
		end
	end)
	local string_1 = "getInventoryWeapons";
	local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
	local ListInventoryWeapons = Target:InvokeServer(string_1);
	AutoFarmMiscTab:Toggle("Auto Hallow Scythe",_G.AutoHallowScythe,function(a)
		HaveHallowScythe = false
		for i,v in pairs(ListInventoryWeapons) do
			if v.Name == "Hallow Scythe" then   
				HaveHallowScythe = true
			end
		end
		if not ThreeWorld and a then
			Flux:Notification('Use In Sea 3 (Three World)')
		elseif HaveHallowScythe and a then
			Flux:Notification('You Have Hallow Scythe')
		else    
			AutoHallowScythe = a
		end 
	end)
	spawn(function()
		while wait() do
			if AutoHallowScythe then
				if game.Players.LocalPlayer.Backpack:FindFirstChild("Hallow Essence") then
					if MainAutoFarmBone then
						AutoFarmBone = false
					end
					Questtween = toTarget(game:GetService("Workspace").Map["Haunted Castle"].Summoner.Detection.Position,game:GetService("Workspace").Map["Haunted Castle"].Summoner.Detection.CFrame)
					if (game:GetService("Workspace").Map["Haunted Castle"].Summoner.Detection.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
						if Questtween then
							Questtween:Stop()
						end
						game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace").Map["Haunted Castle"].Summoner.Detection.CFrame
					end
				elseif game:GetService("Workspace").Enemies:FindFirstChild("Soul Reaper [Lv. 2100] [Raid Boss]") or game.ReplicatedStorage:FindFirstChild("Soul Reaper [Lv. 2100] [Raid Boss]") then
					if MainAutoFarmBone then
						AutoFarmBone = false
					end
					if game:GetService("Workspace").Enemies:FindFirstChild("Soul Reaper [Lv. 2100] [Raid Boss]") then
						for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
							if AutoHallowScythe and v.Name == "Soul Reaper [Lv. 2100] [Raid Boss]" and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 then
								repeat wait()
									if (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 300 then
										Farmtween = toTarget(v.HumanoidRootPart.Position,v.HumanoidRootPart.CFrame)
									elseif (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
										if Farmtween then
											Farmtween:Stop()
										end
										PosFarmBone = v.HumanoidRootPart.CFrame
										EquipWeapon(SelectToolWeapon)
										
										if not game.Players.LocalPlayer.Character:FindFirstChild("HasBuso") then
											local args = {
												[1] = "Buso"
											}
											game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
										end
										game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0)
										Click()
									end
								until not AutoHallowScythe or not v.Parent or v.Humanoid.Health <= 0
								
							end
						end
					else
						Questtween = toTarget(CFrame.new(-9521, 316, 6684).Position,CFrame.new(-9521, 316, 6684))
						if (CFrame.new(-9521, 316, 6684).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
							if Questtween then
								Questtween:Stop()
							end
							game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-9521, 316, 6684)
						end
					end 
				else
					if MainAutoFarmBone then
						AutoFarmBone = true
					end
					local string_1 = "Bones";
					local string_2 = "Buy";
					local number_1 = 1;
					local number_2 = 1;
					local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
					Target:InvokeServer(string_1, string_2, number_1, number_2);
				end
			end
		end
	end)
    section8:Toggle("Auto Farm Soul Reaper",_G.AutoFarmSoulReaper,function(a)
		if not ThreeWorld and a then
			Flux:Notification('Use In Sea 3 (Three World)')
		else    
			AutoSoulReaper = a
		end 
	end)
	spawn(function()
		while wait() do
			if AutoSoulReaper then
				if game.Players.LocalPlayer.Backpack:FindFirstChild("Hallow Essence") then
					if MainAutoFarmBone then
						AutoFarmBone = false
					end
					Questtween = toTarget(game:GetService("Workspace").Map["Haunted Castle"].Summoner.Detection.Position,game:GetService("Workspace").Map["Haunted Castle"].Summoner.Detection.CFrame)
					if (game:GetService("Workspace").Map["Haunted Castle"].Summoner.Detection.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
						if Questtween then
							Questtween:Stop()
						end
						game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace").Map["Haunted Castle"].Summoner.Detection.CFrame
					end
				elseif game:GetService("Workspace").Enemies:FindFirstChild("Soul Reaper [Lv. 2100] [Raid Boss]") or game.ReplicatedStorage:FindFirstChild("Soul Reaper [Lv. 2100] [Raid Boss]") then
					if MainAutoFarmBone then
						AutoFarmBone = false
					end
					if game:GetService("Workspace").Enemies:FindFirstChild("Soul Reaper [Lv. 2100] [Raid Boss]") then
						for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
							if AutoHallowScythe and v.Name == "Soul Reaper [Lv. 2100] [Raid Boss]" and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 then
								repeat wait()
									if (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 300 then
										Farmtween = toTarget(v.HumanoidRootPart.Position,v.HumanoidRootPart.CFrame)
									elseif (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
										if Farmtween then
											Farmtween:Stop()
										end
										PosFarmBone = v.HumanoidRootPart.CFrame
										EquipWeapon(SelectToolWeapon)
										
										if not game.Players.LocalPlayer.Character:FindFirstChild("HasBuso") then
											local args = {
												[1] = "Buso"
											}
											game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
										end
										game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0)
										Click()
									end
								until not AutoSoulReaper or not v.Parent or v.Humanoid.Health <= 0
								
							end
						end
					else
						Questtween = toTarget(CFrame.new(-9521, 316, 6684).Position,CFrame.new(-9521, 316, 6684))
						if (CFrame.new(-9521, 316, 6684).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
							if Questtween then
								Questtween:Stop()
							end
							game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-9521, 316, 6684)
						end
					end 
				else
					if MainAutoFarmBone then
						AutoFarmBone = true
					end
					local string_1 = "Bones";
					local string_2 = "Buy";
					local number_1 = 1;
					local number_2 = 1;
					local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
					Target:InvokeServer(string_1, string_2, number_1, number_2);
				end
			end
		end
	end)
	section8:Toggle("Auto Random bone",_G.AutoRandombone,function(value)
		brandom = value
	end)
	spawn(function()
		while wait() do
			if brandom then
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Bones","Buy",1,1)
			end
		end
	end)
	local section9 = page2:NewSecction("🌀 Portal 🌀")
	PortalKill = section9 = page2:NewSecction("N/S")
	spawn(function()
		while wait() do
			if game.ReplicatedStorage:FindFirstChild("Cake Prince [Lv. 2300] [Raid Boss]") or game:GetService("Workspace").Enemies:FindFirstChild("Cake Prince [Lv. 2300] [Raid Boss]") then
				PortalKill:Refresh("Can Open Door To Kill Cake Prince")
			else
				PortalKill:Refresh("Need Kill Mods : " .. string.match(game.ReplicatedStorage.Remotes.CommF_:InvokeServer("CakePrinceSpawner", true), "%d+") .. " To Open Kill Cake Prince")
			end
		end
	end)
	section9:Toggle("Auto Farm Cake Prince",_G.AutoFarmCakePrince,function(vu)
		if not ThreeWorld and vu then
			VLib:Notification('Use In Sea 3 (Three World)')
		else 
			AutoFarmCakePrince = vu
		end  
	end)
	spawn(function()
		while wait() do
			if AutoFarmCakePrince then
				game.ReplicatedStorage.Remotes.CommF_:InvokeServer("CakePrinceSpawner")
				if game.ReplicatedStorage:FindFirstChild("Cake Prince [Lv. 2300] [Raid Boss]") or game:GetService("Workspace").Enemies:FindFirstChild("Cake Prince [Lv. 2300] [Raid Boss]") then
					if game:GetService("Workspace").Enemies:FindFirstChild("Cake Prince [Lv. 2300] [Raid Boss]") then
						for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
							if AutoFarmCakePrince and v.Name == "Cake Prince [Lv. 2300] [Raid Boss]" and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 then
								repeat wait()
									if (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 300 then
										Farmtween = toTarget(v.HumanoidRootPart.Position,v.HumanoidRootPart.CFrame)
										Usefastattack = false
									elseif (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
										if Farmtween then
											Farmtween:Stop()
										end
										PosFarmBone = v.HumanoidRootPart.CFrame
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
								until not AutoFarmCakePrince or not v.Parent or v.Humanoid.Health <= 0 or game.ReplicatedStorage:FindFirstChild("Cake Prince [Lv. 2300] [Raid Boss]")
								Usefastattack = false
							end
						end
					else
						Usefastattack = false
						Questtween = toTarget(CFrame.new(-2151.82153, 149.315704, -12404.9053).Position,CFrame.new(-2151.82153, 149.315704, -12404.9053))
						if (CFrame.new(-2151.82153, 149.315704, -12404.9053).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
							if Questtween then Questtween:Stop() end
							game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-2151.82153, 149.315704, -12404.9053)
						end
					end
				else
					if game:GetService("Workspace").Enemies:FindFirstChild("Cookie Crafter [Lv. 2200]") or game:GetService("Workspace").Enemies:FindFirstChild("Cake Guard [Lv. 2225]") or game:GetService("Workspace").Enemies:FindFirstChild("Baking Staff [Lv. 2250]") or game:GetService("Workspace").Enemies:FindFirstChild("Head Baker [Lv. 2275]") then
						for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
							if 0 and (v.Name == "Cookie Crafter [Lv. 2200]" or v.Name == "Cake Guard [Lv. 2225]" or v.Name == "Baking Staff [Lv. 2250]" or v.Name == "Head Baker [Lv. 2275]") and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 then
								repeat wait()
									if (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 300 then
										Farmtween = toTarget(v.HumanoidRootPart.Position,v.HumanoidRootPart.CFrame)
										MagnetFarmCakePrince = false
										Usefastattack = false
									elseif (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
										if Farmtween then Farmtween:Stop() end
										Usefastattack = true
										PosFarmCakePrince = v.HumanoidRootPart.CFrame
										EquipWeapon(SelectToolWeapon)
										if not game.Players.LocalPlayer.Character:FindFirstChild("HasBuso") then
											local args = {
												[1] = "Buso"
											}
											game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
										end
										game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0)
										Click()
										MagnetFarmCakePrince = true
									end
								until not AutoFarmCakePrince or not v.Parent or v.Humanoid.Health <= 0
								Usefastattack = false
								MagnetFarmBone = false
							end
						end
					else
						MagnetFarmCakePrince = false
						Usefastattack = false
						Questtween = toTarget(CFrame.new(-2077, 252, -12373).Position,CFrame.new(-2077, 252, -12373))
						if (CFrame.new(-2077, 252, -12373).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
							if Questtween then Questtween:Stop() end
							game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-2077, 252, -12373)
						end
					end
				end
			end
		end
	end)
	spawn(function()
		while wait() do
			if MagnetFarmCakePrince and AutoFarmCakePrince then
				for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
					if MagnetFarmCakePrince  and AutoFarmCakePrince and (v.Name == "Cookie Crafter [Lv. 2200]" or v.Name == "Cake Guard [Lv. 2225]" or v.Name == "Baking Staff [Lv. 2250]" or v.Name == "Head Baker [Lv. 2275]") and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 and (v.HumanoidRootPart.Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 350 then
						v.HumanoidRootPart.CFrame = PosFarmCakePrince
						v.HumanoidRootPart.CanCollide = false
					end
				end
			end
		end
	end)

	local section9 = page2:NewSecction("Auto Tushita",true)
	section9:Toggle("Auto Tushita",_G.AutoEnma,function(v)
		if NewWorld or OldWorld then
			VLib:Notification("Use In Thire World")    
		else
			AutoTushitaSword = v
		end 
	end)
	section9:Toggle("Auto Tushita Hop",_G.AutoEnmaHop,function(v)
		if NewWorld or OldWorld then
			VLib:Notification("Use In Thire World")    
		else
			AutoTushitaSword = v
			HopFunction = v
		end 
	end)
	spawn(function()
		while wait(.1) do
			if AutoTushitaSword then
				autoTushita()
			end
		end
	end)
	function enemyrip()
		repeat 
			MytoTarget(CFrame.new(-5332.30371, 423.985413, -2673.48218)) 
			wait() 
		until _G.StopTween == true or (game.Players.LocalPlayer.Character.HumanoidRootPart.Position-Vector3.new(-5332.30371, 423.985413, -2673.48218)).Magnitude <= 10
		wait()
		if game.Workspace.Enemies:FindFirstChild("rip_indra True Form [Lv. 5000] [Raid Boss]") then
			local mobs = game.Workspace.Enemies:GetChildren()
			for i,v in pairs(mobs) do
				if v.Name == "rip_indra True Form [Lv. 5000] [Raid Boss]" and v:IsA("Model") and v:FindFirstChild("Humanoid") and
					v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
					return v
				end
			end
		end
		return game.ReplicatedStorage:FindFirstChild("rip_indra True Form [Lv. 5000] [Raid Boss]")
	end
	function enemyEliteBoss()
		if game.Workspace.Enemies:FindFirstChild("Deandre [Lv. 1750]") or game.Workspace.Enemies:FindFirstChild("Urban [Lv. 1750]") or game.Workspace.Enemies:FindFirstChild("Diablo [Lv. 1750]") then
			local mobs = game.Workspace.Enemies:GetChildren()
			for i,v in pairs(mobs) do
				if v.Name == "Deandre [Lv. 1750]" or v.Name == "Diablo [Lv. 1750]" or v.Name == "Urban [Lv. 1750]"  and v:IsA("Model") and v:FindFirstChild("Humanoid") and
					v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
					return v
				end
			end
		end
		return game.ReplicatedStorage:FindFirstChild("Deandre [Lv. 1750]") or game.ReplicatedStorage:FindFirstChild("Urban [Lv. 1750]") or game.ReplicatedStorage:FindFirstChild("Diablo [Lv. 1750]")
	end
	
	function enemylongma()
		repeat 
			MytoTarget(CFrame.new(-10171.7051, 406.981995, -9552.31738)) 
			wait() 
		until _G.StopTween == true or not _G.AutoYamaSword or (game.Players.LocalPlayer.Character.HumanoidRootPart.Position-Vector3.new(-10171.7051, 406.981995, -9552.31738)).Magnitude <= 10
		if game.Workspace.Enemies:FindFirstChild("Longma [Lv. 2000] [Boss]") then
			local mobs = game.Workspace.Enemies:GetChildren()
			for i,v in pairs(mobs) do
				if v.Name == "Longma [Lv. 2000] [Boss]" and v:IsA("Model") and v:FindFirstChild("Humanoid") and
					v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
					return v
				end
			end
		end
		return game.ReplicatedStorage:FindFirstChild("Longma [Lv. 2000] [Boss]")
	end
	
	_G.checkup = true
	function autoTushita()
		if _G.checkup and not game.Players.LocalPlayer.Backpack:FindFirstChild("God's Chalice") and not game.Players.LocalPlayer.Character:FindFirstChild("God's Chalice") then
			if game.Workspace.Enemies:FindFirstChild("Deandre [Lv. 1750]") or game.Workspace.Enemies:FindFirstChild("Urban [Lv. 1750]") or game.Workspace.Enemies:FindFirstChild("Diablo [Lv. 1750]") or game.ReplicatedStorage:FindFirstChild("Deandre [Lv. 1750]") or game.ReplicatedStorage:FindFirstChild("Urban [Lv. 1750]") or game.ReplicatedStorage:FindFirstChild("Diablo [Lv. 1750]") then
				if game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Visible == false then
					repeat 
						MytoTarget(CFrame.new(-5420.49219, 314.446045, -2823.07373)) 
						wait() 
					until _G.StopTween == true or not _G.AutoYamaSword or (game.Players.LocalPlayer.Character.HumanoidRootPart.Position-Vector3.new(-5420.49219, 314.446045, -2823.07373)).Magnitude <= 10
					wait(1.1)
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("EliteHunter")
					wait(1)
				elseif game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Visible == true then
					CheckQuest()
					pcall(function()
						EquipWeapon(_G.SelectWeapon)
						pcall(function()
							local v = enemyEliteBoss()
							v.HumanoidRootPart.CanCollide = false
							v.HumanoidRootPart.Size = Vector3.new(50, 50, 50)
							MytoTarget(v.HumanoidRootPart.CFrame * CFrame.new(1,20,1)) 
						end)
					end)
				end
			elseif HopFunction then
				MytoTarget(CFrame.new(-12554.9443, 337.194092, -7501.44727, 0.906377554, 4.23948272e-08, -0.422468632, -1.89128269e-08, 1, 5.97740595e-08, 0.422468632, -4.61877896e-08, 0.906377554))				wait(1)
				HopServer()
			end
		elseif game.Players.LocalPlayer.Backpack:FindFirstChild("God's Chalice") or game.Players.LocalPlayer.Character:FindFirstChild("God's Chalice") then
			_G.checkup = false
			game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("activateColor","Winter Sky")
			wait(0.5)
			repeat 
				MytoTarget(CFrame.new(-5420.16602, 1084.9657, -2666.8208)) 
				wait() 
			until _G.StopTween == true or not _G.AutoYamaSword or (game.Players.LocalPlayer.Character.HumanoidRootPart.Position-Vector3.new(-5420.16602, 1084.9657, -2666.8208)).Magnitude <= 10
			wait(0.5)
			game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("activateColor","Pure Red")
			wait(0.5)
			repeat 
				MytoTarget(CFrame.new(-5414.41357, 309.865753, -2212.45776)) 
				wait() 
			until _G.StopTween == true or not _G.AutoYamaSword or (game.Players.LocalPlayer.Character.HumanoidRootPart.Position-Vector3.new(-5414.41357, 309.865753, -2212.45776)).Magnitude <= 10
			wait(0.5)
			game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("activateColor","Snow White")
			wait(0.5)
			repeat 
				MytoTarget(CFrame.new(-4971.47559, 331.565765, -3720.02954)) 
				wait() 
			until _G.StopTween == true or not _G.AutoYamaSword or (game.Players.LocalPlayer.Character.HumanoidRootPart.Position-Vector3.new(-4971.47559, 331.565765, -3720.02954)).Magnitude <= 10
			wait(0.5)
			EquipWeapon("God's Chalice")
			wait(0.5)
			repeat 
				MytoTarget(CFrame.new(-5560.27295, 313.915466, -2663.89795)) 
				wait() 
			until _G.StopTween == true or not _G.AutoYamaSword or (game.Players.LocalPlayer.Character.HumanoidRootPart.Position-Vector3.new(-5560.27295, 313.915466, -2663.89795)).Magnitude <= 10
			wait(0.5)
			repeat 
				MytoTarget(CFrame.new(-5561.37451, 313.342529, -2663.49487)) 
				wait() 
			until _G.StopTween == true or not _G.AutoYamaSword or (game.Players.LocalPlayer.Character.HumanoidRootPart.Position-Vector3.new(-5561.37451, 313.342529, -2663.49487)).Magnitude <= 10
			wait(1)
			repeat 
				MytoTarget(CFrame.new(5154.17676, 141.786423, 911.046326)) 
				wait() 
			until _G.StopTween == true or not _G.AutoYamaSword or (game.Players.LocalPlayer.Character.HumanoidRootPart.Position-Vector3.new(5154.17676, 141.786423, 911.046326)).Magnitude <= 10
			wait(0.2)
			repeat 
				MytoTarget(CFrame.new(5148.03613, 162.352493, 910.548218)) 
				wait() 
			until _G.StopTween == true or not _G.AutoYamaSword or (game.Players.LocalPlayer.Character.HumanoidRootPart.Position-Vector3.new(5148.03613, 162.352493, 910.548218)).Magnitude <= 10
			wait(1)
			EquipWeapon("Holy Torch")
			wait(1)
			wait(0.4)
			repeat 
				MytoTarget(CFrame.new(-10752.7695, 412.229523, -9366.36328)) 
				wait() 
			until _G.StopTween == true or not _G.AutoYamaSword or (game.Players.LocalPlayer.Character.HumanoidRootPart.Position-Vector3.new(-10752.7695, 412.229523, -9366.36328)).Magnitude <= 10
			wait(0.4)
			repeat 
				MytoTarget(CFrame.new(-11673.4111, 331.749023, -9474.34668)) 
				wait() 
			until _G.StopTween == true or not _G.AutoYamaSword or (game.Players.LocalPlayer.Character.HumanoidRootPart.Position-Vector3.new(-11673.4111, 331.749023, -9474.34668)).Magnitude <= 10
			wait(0.4)
			repeat 
				MytoTarget(CFrame.new(-12133.3389, 519.47522, -10653.1904)) 
				wait() 
			until _G.StopTween == true or not _G.AutoYamaSword or (game.Players.LocalPlayer.Character.HumanoidRootPart.Position-Vector3.new(-12133.3389, 519.47522, -10653.1904)).Magnitude <= 10
			wait(0.4)
			repeat 
				MytoTarget(CFrame.new(-13336.5, 485.280396, -6983.35254, 0.912677109)) 
				wait() 
			until _G.StopTween == true or not _G.AutoYamaSword or (game.Players.LocalPlayer.Character.HumanoidRootPart.Position-Vector3.new(-13336.5, 485.280396, -6983.35254, 0.912677109)).Magnitude <= 10
			wait(0.4)
			repeat 
				MytoTarget(CFrame.new(-13487.4131, 334.84845, -7926.34863)) 
				wait() 
			until _G.StopTween == true or not _G.AutoYamaSword or (game.Players.LocalPlayer.Character.HumanoidRootPart.Position-Vector3.new(-13487.4131, 334.84845, -7926.34863)).Magnitude <= 10
			wait(1)
		elseif game.Workspace.Enemies:FindFirstChild("Longma [Lv. 2000] [Boss]") or game.ReplicatedStorage:FindFirstChild("Longma [Lv. 2000] [Boss]") then
			pcall(function()
				EquipWeapon(_G.SelectWeapon)
				pcall(function()
					local v = enemylongma()
					v.HumanoidRootPart.CanCollide = false
					v.HumanoidRootPart.Size = Vector3.new(50, 50, 50)
					MytoTarget(v.HumanoidRootPart.CFrame * CFrame.new(1, _G.DistanceFarm, 0))
				end)
			end)
		elseif game.Workspace.Enemies:FindFirstChild("rip_indra True Form [Lv. 5000] [Raid Boss]")  or game.ReplicatedStorage:FindFirstChild("rip_indra True Form [Lv. 5000] [Raid Boss]") then
			pcall(function()
				EquipWeapon(_G.SelectWeapon)
				pcall(function()
					local v = enemyrip()
					v.HumanoidRootPart.CanCollide = false
					v.HumanoidRootPart.Size = Vector3.new(50, 50, 50)
					MytoTarget(v.HumanoidRootPart.CFrame * CFrame.new(1, _G.DistanceFarm, 0))
				end)
			end)
		elseif HopFunction then
			MytoTarget(CFrame.new(-12554.9443, 337.194092, -7501.44727, 0.906377554, 4.23948272e-08, -0.422468632, -1.89128269e-08, 1, 5.97740595e-08, 0.422468632, -4.61877896e-08, 0.906377554))
			wait(1)
			HopServer()
		end
	end
    local section10 = page2:NewSecction("Auto Enma/Yama",true)
	section10:Toggle("Auto Enma/Yama",_G.AutoEnma,function(v)
		if NewWorld or OldWorld then
			VLib:Notification("Use In Thire World")    
		else
			AutoYama = v
		end 
	end)
	section10:Toggle("Auto Enma/Yama HOP",_G.AutoEnmaHop,function(v)
		if NewWorld or OldWorld then
			VLib:Notification("Use In Thire World")    
		else
			AutoYama = v
			AutoYamaHOP = v
		end 
	end)
	spawn(function()
		while wait() do
			if AutoYama then
				if game:GetService("ReplicatedStorage").Remotes["CommF_"]:InvokeServer("EliteHunter", "Progress") < 30 then
					if game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible == true then
						if string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, "Diablo") or string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, "Urban") or string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, "Deandre") then
							for i,v in pairs(game.ReplicatedStorage:GetChildren()) do
								if string.find(v.Name,"Diablo") then
									YemaTween = toTarget(v.HumanoidRootPart.Position,v.HumanoidRootPart.CFrame)
									if (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 250 then
										if YemaTween then
											YemaTween:Stop()
										end
										game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame
									end
								end	
								if string.find(v.Name,"Urban") then
									YemaTween = toTarget(v.HumanoidRootPart.Position,v.HumanoidRootPart.CFrame)
									if (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 250 then
										if YemaTween then
											YemaTween:Stop()
										end
										game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame
									end
								end	
								if string.find(v.Name,"Deandre") then
									YemaTween = toTarget(v.HumanoidRootPart.Position,v.HumanoidRootPart.CFrame)
									if (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 250 then
										if YemaTween then
											YemaTween:Stop()
										end
										game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame
									end
								end	
							end
							for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
								if AutoYama and string.find(v.Name,"Diablo") and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
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
									until not AutoYama or not v.Parent or v.Humanoid.Health <= 0
									Usefastattack = false
								end
								if AutoYama and string.find(v.Name,"Urban") and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
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
									until not AutoYama or not v.Parent or v.Humanoid.Health <= 0
									Usefastattack = false
								end
								if AutoYama and string.find(v.Name,"Deandre") and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
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
									until not AutoYama or not v.Parent or v.Humanoid.Health <= 0
									Usefastattack = false
								end
							end
						else
							local string_1 = "EliteHunter";
							local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
							Target:InvokeServer(string_1);
						end
					else
						if AutoYamaHOP and game:GetService("ReplicatedStorage").Remotes["CommF_"]:InvokeServer("EliteHunter") == "I don't have anything for you right now. Come back later." then
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
											wait(1)
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
						else
							local string_1 = "EliteHunter";
							local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
							Target:InvokeServer(string_1);
						end
					end
				else
					TweenYema = toTarget(game.Workspace.Map.Waterfall.SealedKatana.Handle.Position,game.Workspace.Map.Waterfall.SealedKatana.Handle.CFrame)
					if (game.Workspace.Map.Waterfall.SealedKatana.Handle.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
						if TweenYema then
							TweenYema:Stop()
						end
						if game.Workspace.Enemies:FindFirstChild("Ghost [Lv. 1500]") then
							for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
								if AutoYama and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 and v.Name == "Ghost [Lv. 1500]" then
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
									until not AutoYama or not v.Parent or v.Humanoid.Health <= 0
									Usefastattack = false
								end
							end
						else
							if TweenYema then
								TweenYema:Stop()
							end
							fireclickdetector(game.Workspace.Map.Waterfall.SealedKatana.Handle.ClickDetector)
						end
					end
				end
			end
		end
	end)
	-- Auto Holy Torch
	local section11 = page2:NewSecction("Auto Holy Torch",true)
	section11:Toggle("Auto Holy Torch",_G.AutoHolyTorch,function(v)
		if NewWorld or OldWorld then
			VLib:Notification("Use In Thire World")    
		else
			HolyTorch = v
		end 
	end)
	spawn(function()
		while wait() do
			if HolyTorch then
				if game.ReplicatedStorage:FindFirstChild("rip_indra True Form [Lv. 5000] [Raid Boss]") or game.Workspace.Enemies:FindFirstChild("rip_indra True Form [Lv. 5000] [Raid Boss]") and game:GetService("Workspace").Map.Turtle.TushitaGate.TushitaGate.Transparency == 1 then
					if game.Players.LocalPlayer.Backpack:FindFirstChild("Holy Torch") then
						EquipWeapon("Holy Torch")
					elseif game.Players.LocalPlayer.Character:FindFirstChild("Holy Torch") then
						if game:GetService("Workspace").Map.Turtle.QuestTorches.Torch1.Particles.Main.Enabled ~= true then
							if (game:GetService("Workspace").Map.Turtle.QuestTorches.Torch1.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 300 then
								HolyTorchtween = toTarget(game:GetService("Workspace").Map.Turtle.QuestTorches.Torch1.Position,game:GetService("Workspace").Map.Turtle.QuestTorches.Torch1.CFrame)
							elseif (game:GetService("Workspace").Map.Turtle.QuestTorches.Torch1.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
								if HolyTorchtween then
									HolyTorchtween:Stop()
								end
								game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame = game.Workspace.Map.Turtle.QuestTorches.Torch1.CFrame
							end
						elseif game:GetService("Workspace").Map.Turtle.QuestTorches.Torch2.Particles.Main.Enabled ~= true then
							if (game:GetService("Workspace").Map.Turtle.QuestTorches.Torch2.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 300 then
								HolyTorchtween = toTarget(game:GetService("Workspace").Map.Turtle.QuestTorches.Torch2.Position,game:GetService("Workspace").Map.Turtle.QuestTorches.Torch2.CFrame)
							elseif (game:GetService("Workspace").Map.Turtle.QuestTorches.Torch2.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
								if HolyTorchtween then
									HolyTorchtween:Stop()
								end
								game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame = game.Workspace.Map.Turtle.QuestTorches.Torch2.CFrame
							end
						elseif game:GetService("Workspace").Map.Turtle.QuestTorches.Torch3.Particles.Main.Enabled ~= true then
							if (game:GetService("Workspace").Map.Turtle.QuestTorches.Torch3.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 300 then
								HolyTorchtween = toTarget(game:GetService("Workspace").Map.Turtle.QuestTorches.Torch3.Position,game:GetService("Workspace").Map.Turtle.QuestTorches.Torch3.CFrame)
							elseif (game:GetService("Workspace").Map.Turtle.QuestTorches.Torch3.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
								if HolyTorchtween then
									HolyTorchtween:Stop()
								end
								game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame = game.Workspace.Map.Turtle.QuestTorches.Torch3.CFrame
							end
						elseif game:GetService("Workspace").Map.Turtle.QuestTorches.Torch4.Particles.Main.Enabled ~= true then
							if (game:GetService("Workspace").Map.Turtle.QuestTorches.Torch4.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 300 then
								HolyTorchtween = toTarget(game:GetService("Workspace").Map.Turtle.QuestTorches.Torch4.Position,game:GetService("Workspace").Map.Turtle.QuestTorches.Torch4.CFrame)
							elseif (game:GetService("Workspace").Map.Turtle.QuestTorches.Torch4.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
								if HolyTorchtween then
									HolyTorchtween:Stop()
								end
								game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame = game.Workspace.Map.Turtle.QuestTorches.Torch4.CFrame
							end
						elseif game:GetService("Workspace").Map.Turtle.QuestTorches.Torch5.Particles.Main.Enabled ~= true then
							if (game:GetService("Workspace").Map.Turtle.QuestTorches.Torch5.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 300 then
								HolyTorchtween = toTarget(game:GetService("Workspace").Map.Turtle.QuestTorches.Torch5.Position,game:GetService("Workspace").Map.Turtle.QuestTorches.Torch5.CFrame)
							elseif (game:GetService("Workspace").Map.Turtle.QuestTorches.Torch5.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
								if HolyTorchtween then
									HolyTorchtween:Stop()
								end
								game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame = game.Workspace.Map.Turtle.QuestTorches.Torch5.CFrame
							end
						end
					else
						game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace").Map.Waterfall.SecretRoom.Room.Door.Door.Hitbox.CFrame
					end
				end
			end
		end
	end)
	-- Auto Fram Elite Hunter
	local CheckEliteHunter = AutoFarmMiscTab:Label("Kill " .. game.ReplicatedStorage.Remotes.CommF_:InvokeServer("EliteHunter", "Progress") .. " Elite Enemies",true)
	spawn(function()
		while wait() do
			CheckEliteHunter:Refresh("Kill " .. game.ReplicatedStorage.Remotes.CommF_:InvokeServer("EliteHunter", "Progress") .. " Elite Enemies")
		end
	end)
	section11:Toggle("Auto Elite Hunter",_G.AutoEliteHunter,function(a)
		if ThreeWorld then
			AutoEliteHunter = a
		else
			VLib:Notification("Use In Thire World")
		end
	end)
	section11:Toggle("Auto Elite Hunter HOP",_G.AutoEliteHunterHop,function(a)
		if ThreeWorld then
			AutoEliteHunter = a
			AutoEliteHunterHOP = a
		else
			VLib:Notification("Use In Thire World")
		end
	end)
	spawn(function()
		while wait() do
			if AutoEliteHunter then
				if game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible == true then
					if string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, "Diablo") or string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, "Urban") or string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, "Deandre") then
						for i,v in pairs(game.ReplicatedStorage:GetChildren()) do
							if string.find(v.Name,"Diablo") then
								EliteHunter = toTarget(v.HumanoidRootPart.Position,v.HumanoidRootPart.CFrame)
								if (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 250 then
									if EliteHunter then
										EliteHunter:Stop()
									end
									game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame
								end
							end	
							if string.find(v.Name,"Urban") then
								EliteHunter = toTarget(v.HumanoidRootPart.Position,v.HumanoidRootPart.CFrame)
								if (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 250 then
									if EliteHunter then
										EliteHunter:Stop()
									end
									game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame
								end
							end	
							if string.find(v.Name,"Deandre") then
								EliteHunter = toTarget(v.HumanoidRootPart.Position,v.HumanoidRootPart.CFrame)
								if (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 250 then
									if EliteHunter then
										EliteHunter:Stop()
									end
									game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame
								end
							end	
						end
						for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
							if AutoEliteHunter and string.find(v.Name,"Diablo") and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
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
								until not AutoEliteHunter or not v.Parent or v.Humanoid.Health <= 0
								Usefastattack = false
							end
							if AutoEliteHunter and string.find(v.Name,"Urban") and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
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
								until not AutoEliteHunter or not v.Parent or v.Humanoid.Health <= 0
								Usefastattack = false
							end
							if AutoEliteHunter and string.find(v.Name,"Deandre") and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
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
								until not AutoEliteHunter or not v.Parent or v.Humanoid.Health <= 0
								Usefastattack = false
							end
						end
					else
						if AutoEliteHunterHOP and game:GetService("ReplicatedStorage").Remotes["CommF_"]:InvokeServer("EliteHunter") == "I don't have anything for you right now. Come back later." then
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
									if tonumber(4) > tonumber(v.playing) then
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
											wait(1)
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
						else
							local string_1 = "EliteHunter";
							local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
							Target:InvokeServer(string_1);
						end
					end
				else
					if AutoEliteHunterHOP and game:GetService("ReplicatedStorage").Remotes["CommF_"]:InvokeServer("EliteHunter") == "I don't have anything for you right now. Come back later." then
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
								if tonumber(4) > tonumber(v.playing) then
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
										wait(1)
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
					else
						local string_1 = "EliteHunter";
						local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
						Target:InvokeServer(string_1);
					end
				end
			end
		end	
	end)

	local section12 = page2:NewSecction("Auto Haki Rainbow",true)
	section12:Toggle("Auto Haki Rainbow",_G.AutoHakiRainbow,function(a)
		if ThreeWorld then
			AutoHakiRainbow = a
		else
			Flux:Notification("Use In Three World")
		end
	end)
	spawn(function()
		while wait() do
			if AutoHakiRainbow then
				if game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible == true then
					if string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, "Stone") or string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, "Island Empress") or string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, "Kilo Admiral") or string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, "Captain Elephant") or string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, "Beautiful Pirate") then
						if string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, "Stone") then
							if game.Workspace.Enemies:FindFirstChild("Stone [Lv. 1550] [Boss]") then
								for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
									if AutoHakiRainbow and v.Name == "Stone [Lv. 1550] [Boss]" and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
										repeat
											pcall(function() wait() 
												local string_1 = "HornedMan";
												local string_2 = "Bet";
												local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
												Target:InvokeServer(string_1, string_2);
												local string_1 = "HornedMan";
												local string_2 = "Bet";
												local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
												Target:InvokeServer(string_1, string_2);
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
											end)
										until not AutoHakiRainbow or not v.Parent or v.Humanoid.Health <= 0 or game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible == false
										Usefastattack = true
									end
								end
							else 
								if (CFrame.new(-1134, 40, 6877).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 250 then
									HakiRainbowTween = toTarget(CFrame.new(-1134, 40, 6877).Position,CFrame.new(-1134, 40, 6877))
								elseif (CFrame.new(-1134, 40, 6877).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 250 then
									if HakiRainbowTween then
										HakiRainbowTween:Stop()
									end
									game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-1134, 40, 6877)
								end
							end
						elseif string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, "Island Empress") then
							if game.Workspace.Enemies:FindFirstChild("Island Empress [Lv. 1675] [Boss]") then
								for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
									if AutoHakiRainbow and v.Name == "Island Empress [Lv. 1675] [Boss]" and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
										repeat
											pcall(function() wait() 
												local string_1 = "HornedMan";
												local string_2 = "Bet";
												local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
												Target:InvokeServer(string_1, string_2);
												local string_1 = "HornedMan";
												local string_2 = "Bet";
												local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
												Target:InvokeServer(string_1, string_2);
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
											end)
										until not AutoHakiRainbow or not v.Parent or v.Humanoid.Health <= 0 or game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible == false
										Usefastattack = true
									end
								end
							else
								if (CFrame.new(5614, 603, 339).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 250 then
									HakiRainbowTween = toTarget(CFrame.new(5614, 603, 339).Position,CFrame.new(5614, 603, 339))
								elseif (CFrame.new(5614, 603, 339).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 250 then
									if HakiRainbowTween then
										HakiRainbowTween:Stop()
									end
									game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(5614, 603, 339)
								end
							end	
						elseif string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, "Kilo Admiral") then
							if game.Workspace.Enemies:FindFirstChild("Kilo Admiral [Lv. 1750] [Boss]") then
								for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
									if AutoHakiRainbow and v.Name == "Kilo Admiral [Lv. 1750] [Boss]" and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
										repeat
											pcall(function() wait() 
												local string_1 = "HornedMan";
												local string_2 = "Bet";
												local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
												Target:InvokeServer(string_1, string_2);
												local string_1 = "HornedMan";
												local string_2 = "Bet";
												local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
												Target:InvokeServer(string_1, string_2);
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
											end)
										until not AutoHakiRainbow or not v.Parent or v.Humanoid.Health <= 0 or game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible == false
										Usefastattack = true
									end
								end
							else
								if (CFrame.new(2879, 433, -7090).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 250 then
									HakiRainbowTween = toTarget(CFrame.new(2879, 433, -7090).Position,CFrame.new(2879, 433, -7090))
								elseif (CFrame.new(2879, 433, -7090).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 250 then
									if HakiRainbowTween then
										HakiRainbowTween:Stop()
									end
									game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(2879, 433, -7090)
								end
							end	
						elseif string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, "Captain Elephant") then
							if game.Workspace.Enemies:FindFirstChild("Captain Elephant [Lv. 1875] [Boss]") then
								for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
									if AutoHakiRainbow and v.Name == "Captain Elephant [Lv. 1875] [Boss]" and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
										repeat
											pcall(function() wait() 
												local string_1 = "HornedMan";
												local string_2 = "Bet";
												local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
												Target:InvokeServer(string_1, string_2);
												local string_1 = "HornedMan";
												local string_2 = "Bet";
												local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
												Target:InvokeServer(string_1, string_2);
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
											end)
										until not AutoHakiRainbow or not v.Parent or v.Humanoid.Health <= 0 or game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible == false
										Usefastattack = true
									end
								end
							else
								if (CFrame.new(-13348, 406, -8574).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 250 then
									HakiRainbowTween = toTarget(CFrame.new(-13348, 406, -8574).Position,CFrame.new(-13348, 406, -8574))
								elseif (CFrame.new(-13348, 406, -8574).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 250 then
									if HakiRainbowTween then
										HakiRainbowTween:Stop()
									end
									game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-13348, 406, -8574)
								end
							end	
						elseif string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, "Beautiful Pirate") then
							if game.Workspace.Enemies:FindFirstChild("Beautiful Pirate [Lv. 1950] [Boss]") then
								for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
									if AutoHakiRainbow and v.Name == "Beautiful Pirate [Lv. 1950] [Boss]" and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
										repeat
											pcall(function() wait() 
												local string_1 = "HornedMan";
												local string_2 = "Bet";
												local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
												Target:InvokeServer(string_1, string_2);
												local string_1 = "HornedMan";
												local string_2 = "Bet";
												local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
												Target:InvokeServer(string_1, string_2);
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
											end)
										until not AutoHakiRainbow or not v.Parent or v.Humanoid.Health <= 0 or game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible == false
										Usefastattack = true
									end
								end
							else
								if (CFrame.new(5206, 23, -80).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 250 then
									HakiRainbowTween = toTarget(CFrame.new(5206, 23, -80).Position,CFrame.new(5206, 23, -80))
								elseif (CFrame.new(5206, 23, -80).Position - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).magnitude > 20000 then
									if HakiRainbowTween then
										HakiRainbowTween:Stop()
									end
									local TouchInterest = game:GetService("Workspace").Map.Turtle.Entrance.Door.BossDoor.Hitbox
									game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = TouchInterest.CFrame
								elseif (CFrame.new(5206, 23, -80).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 250 then
									if HakiRainbowTween then
										HakiRainbowTween:Stop()
									end
									game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(5206, 23, -80)
								end
							end	
						end
					else
						local string_1 = "HornedMan";
						local string_2 = "Bet";
						local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
						Target:InvokeServer(string_1, string_2);
						local string_1 = "HornedMan";
						local string_2 = "Bet";
						local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
						Target:InvokeServer(string_1, string_2);
					end
				else
					local string_1 = "HornedMan";
					local string_2 = "Bet";
					local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
					Target:InvokeServer(string_1, string_2);
					local string_1 = "HornedMan";
					local string_2 = "Bet";
					local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
					Target:InvokeServer(string_1, string_2);
				end
			end
		end
	end)
	local section13 = page2:NewSecction("Auto Musketee Hat " )
	AutoFarmMiscTab:Toggle("Auto Musketee Hat",_G.AutoMusketeeHat,function(a)
		if ThreeWorld then
			MusketeeHat = a
		else
			Flux:Notification("Use In Three World")
		end
	end)
	spawn(function()
		while wait() do
			if MusketeeHat then
				local v86 = game.ReplicatedStorage.Remotes.CommF_:InvokeServer("CitizenQuestProgress", "Citizen");
				if v86 == 0 then
					if not string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, "50 Forest Pirates") then
						local string_1 = "StartQuest";
						local string_2 = "CitizenQuest";
						local number_1 = 1;
						local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
						Target:InvokeServer(string_1, string_2, number_1);
					else
						if game.Workspace.Enemies:FindFirstChild("Forest Pirate [Lv. 1825]") then
							for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
								if v.Name == "Forest Pirate [Lv. 1825]" and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
									repeat wait() 
										MusketeeHatPos = v.HumanoidRootPart.CFrame
										if (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 300 then
											Farmtween = toTarget(v.HumanoidRootPart.Position,v.HumanoidRootPart.CFrame)
											MusketeeHatMagnet = false
										elseif (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 300 then
											if Farmtween then
												Farmtween:Stop()
											end
											EquipWeapon(SelectToolWeapon)
											Usefastattack = true
											MusketeeHatMagnet = true
											if not game.Players.LocalPlayer.Character:FindFirstChild("HasBuso") then
												local args = {
													[1] = "Buso"
												}
												game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
											end
											game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0)
											Click()
										end 
									until not MusketeeHat or v.Humanoid.Health <= 0 or game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text == "Defeat 50 Forest Pirates (50/50)"
									Usefastattack = false
									MusketeeHatMagnet = false
								end 
							end
						else
							if (CFrame.new(-13265, 428, -7781).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 250 then
								MusketeeTween = toTarget(CFrame.new(-13265, 428, -7781).Position,CFrame.new(-13265, 428, -7781))
							elseif (CFrame.new(-13265, 428, -7781).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 250 then
								if MusketeeTween then
									MusketeeTween:Stop()
								end
								game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-13265, 428, -7781)
							end
						end
					end
				elseif v86 == 1 then
					MusketeeHatMagnet = false
					if not string.find(game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, "Captain Elephant") then
						game.ReplicatedStorage.Remotes.CommF_:InvokeServer("CitizenQuestProgress", "Citizen");
						game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-13350, 406, -8573)
					else
						if game.Workspace.Enemies:FindFirstChild("Captain Elephant [Lv. 1875] [Boss]") then
							for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
								if v.Name == "Captain Elephant [Lv. 1875] [Boss]" and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and v.Humanoid.Health > 0 then
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
									until not MusketeeHat or v.Humanoid.Health <= 0 or game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text == "Defeat  Captain Elephant (1/1)"
									Usefastattack = false
								end 
							end
						else
							if (CFrame.new(-13350, 406, -8573).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 250 then
								MusketeeTween = toTarget(CFrame.new(-13350, 406, -8573).Position,CFrame.new(-13350, 406, -8573))
							elseif (CFrame.new(-13350, 406, -8573).Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 250 then
								if MusketeeTween then
									MusketeeTween:Stop()
								end
								game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-13350, 406, -8573)
							end
						end
					end
				elseif v86 == 2 then
					if game.Workspace.Map.Turtle:FindFirstChild("Treasure") then
						if (game.Workspace.Map.Turtle:FindFirstChild("Treasure").Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 250 then
							MusketeeTween = toTarget(game.Workspace.Map.Turtle:FindFirstChild("Treasure").Position,game.Workspace.Map.Turtle:FindFirstChild("Treasure").CFrame)
						elseif (game.Workspace.Map.Turtle:FindFirstChild("Treasure").Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 250 then
							if MusketeeTween then
								MusketeeTween:Stop()
							end
							game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Workspace.Map.Turtle:FindFirstChild("Treasure").CFrame
						end
					end
				end
			end
		end
	end)
	local section14 = page2:NewSecction("Auto Observation Haki V2" )
	section14:Toggle("Auto Observation Haki V2",_G.AutoObservationHakiV2,function(a)
		if ThreeWorld then
			if game.ReplicatedStorage.Remotes.CommF_:InvokeServer("CitizenQuestProgress", "Citizen") == 4 or game.ReplicatedStorage.Remotes.CommF_:InvokeServer("CitizenQuestProgress", "Citizen") == 3 and game:GetService("Players").LocalPlayer.VisionRadius == 3000 then
				AutoObservationHakiV2 = a
			elseif game:GetService("Players").LocalPlayer.VisionRadius < 3000 then
				Flux:Notification("Observation Haki Not Max")
			else
				Flux:Notification("Quest Musketee Hat No Compete")
			end 
		else
			Flux:Notification("Use In Three World")
		end
	end)
	spawn(function()
		while wait() do
			if AutoObservationHakiV2 then
				if game.ReplicatedStorage.Remotes.CommF_:InvokeServer("CitizenQuestProgress", "Citizen") == 4 or game.ReplicatedStorage.Remotes.CommF_:InvokeServer("CitizenQuestProgress", "Citizen") == 3  then
					if game.Players.LocalPlayer.Backpack:FindFirstChild("Fruit Bowl") or game.Players.LocalPlayer.Character:FindFirstChild("Fruit Bowl") then
						game.ReplicatedStorage.Remotes.CommF_:InvokeServer("KenTalk2", "Start")
						game.ReplicatedStorage.Remotes.CommF_:InvokeServer("KenTalk2", "Buy")
					else
						if ( game.Players.LocalPlayer.Character:FindFirstChild("Pineapple") or game.Players.LocalPlayer.Backpack:FindFirstChild("Pineapple") ) and ( game.Players.LocalPlayer.Character:FindFirstChild("Banana") or game.Players.LocalPlayer.Backpack:FindFirstChild("Banana") ) and ( game.Players.LocalPlayer.Character:FindFirstChild("Apple") or game.Players.LocalPlayer.Backpack:FindFirstChild("Apple") ) then
							game.ReplicatedStorage.Remotes.CommF_:InvokeServer("CitizenQuestProgress", "Citizen")
						else
							if game:GetService("Workspace").AppleSpawner:FindFirstChild("Apple") and not ( game.Players.LocalPlayer.Character:FindFirstChild("Apple") or game.Players.LocalPlayer.Backpack:FindFirstChild("Apple") ) then  
								for i,v in pairs(game:GetService("Workspace").AppleSpawner:GetChildren()) do
									if v:IsA("Tool") then wait(1)
										firetouchinterest(game.Players.LocalPlayer.Character.HumanoidRootPart,v.Handle,0)    
									end
								end
							end 
							if game:GetService("Workspace").PineappleSpawner:FindFirstChild("Pineapple") and not ( game.Players.LocalPlayer.Character:FindFirstChild("Pineapple") or game.Players.LocalPlayer.Backpack:FindFirstChild("Pineapple") ) then  
								for i,v in pairs(game:GetService("Workspace").PineappleSpawner:GetChildren()) do
									if v:IsA("Tool") then wait(1)
										firetouchinterest(game.Players.LocalPlayer.Character.HumanoidRootPart,v.Handle,0)    
									end
								end
							end 
							if game:GetService("Workspace").BananaSpawner:FindFirstChild("Banana") and not ( game.Players.LocalPlayer.Character:FindFirstChild("Banana") or game.Players.LocalPlayer.Backpack:FindFirstChild("Banana") ) then  
								for i,v in pairs(game:GetService("Workspace").BananaSpawner:GetChildren()) do
									if v:IsA("Tool") then wait(1)
										firetouchinterest(game.Players.LocalPlayer.Character.HumanoidRootPart,v.Handle,0)    
									end
								end
							end 
						end
					end
				end
			end
		end
	end)
	----------------------------------------------------------------------------------------------------------------------------
    local page3 = win:NewPage("stats")
	PlayerServer = StatsTab:Label("Players in Server : "..game.Players.NumPlayers .. "/"..game.Players.MaxPlayers)
	Fruit = StatsTab:Label("Fruit : 0")
	Chest = StatsTab:Label("Chest : 0")
	spawn(function()
		while wait() do
			local count10 = 0
			local count = 0
			for i,v in pairs(game.workspace:GetChildren()) do
				if string.find(v.Name,"Chest") and v:IsA("Part") then
					count10 = count10 + 1
				end
			end
			for i,v in pairs(game.Workspace:GetChildren()) do
				if v.Name == "Blox Fruit Dealer" then
				else
					if string.find(v.Name, "Fruit") and v:IsA("Tool") then
						count = count + 1
					end
					if string.find(v.Name, "Fruit") and v:IsA("Model") then
						count = count + 1
					end
				end
			end
			Fruit:Refresh("Fruit : "..count)
			Chest:Refresh("Chest : "..count10)
			PlayerServer:Refresh("Players in Server : "..game.Players.NumPlayers .. "/"..game.Players.MaxPlayers)
			wait(5)
		end
	end)
    local stats = page3:NewSecction("Stats")
	local Point = page3:NewSecction("Point :")
	Point:Refresh("Point : "..game.Players.localPlayer.Data.Points.Value)
	local MeleeStats = StatsTab:Toggle("Melee",getgenv().Setting["Melee"],function(value)
		melee = value    
	end)
	local DefenseStats = StatsTab:Toggle("Defense",getgenv().Setting["Defense"],function(value)
		defense = value
	end)
	local SwordStats = StatsTab:Toggle("Sword",getgenv().Setting["Sword"],function(value)
		sword = value
	end)
	local GunStats = StatsTab:Toggle("Gun",getgenv().Setting["Gun"],function(value)
		gun = value
	end)
	local DemonFruitStats = StatsTab:Toggle("Demon Fruit",getgenv().Setting["Demon Fruit"],function(value)
		demonfruit = value
	end)
	PointStats = 1
	StatsTab:Slider("Point",1,10,PointStats,nil,function(a)
		PointStats = a
	end)
	spawn(function()
		while wait() do
			pcall(function()
				MeleeStats:Refresh("Melee : " .. game:GetService("Players").LocalPlayer.Data.Stats.Melee.Level.Value )
				DefenseStats:Refresh("Defense : " .. game:GetService("Players").LocalPlayer.Data.Stats.Defense.Level.Value )
				SwordStats:Refresh("Sword : " .. game:GetService("Players").LocalPlayer.Data.Stats.Sword.Level.Value )
				GunStats:Refresh("Gun : " .. game:GetService("Players").LocalPlayer.Data.Stats.Gun.Level.Value )
				DemonFruitStats:Refresh("Demon Fruit : " .. game:GetService("Players").LocalPlayer.Data.Stats["Demon Fruit"].Level.Value )
			end)
			if game.Players.localPlayer.Data.Points.Value >= PointStats then
				if melee then
					local args = {
						[1] = "AddPoint",
						[2] = "Melee",
						[3] = PointStats
					}
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
				end 
				if defense then
					local args = {
						[1] = "AddPoint",
						[2] = "Defense",
						[3] = PointStats
					}
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
				end 
				if sword then
					local args = {
						[1] = "AddPoint",
						[2] = "Sword",
						[3] = PointStats
					}
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
				end 
				if gun then
					local args = {
						[1] = "AddPoint",
						[2] = "Gun",
						[3] = PointStats
					}
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
				end 
				if demonfruit then
					local args = {
						[1] = "AddPoint",
						[2] = "Demon Fruit",
						[3] = PointStats
					}
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
				end
			end
			Point:Refresh("Point : "..game.Players.localPlayer.Data.Points.Value) 
		end
	end)
	----------------------------------------------------------------------------------------------------------------------------
    local page4 = win:NewPage("Teleport")
	TeleportTab:Button("Teleport To Sea 1" ,function()
		local args = {
			[1] = "TravelMain" -- OLD WORLD to NEW WORLD
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	end)
	TeleportTab:Button("Teleport To Sea 2" ,function()
		local args = {
			[1] = "TravelDressrosa" -- NEW WORLD to OLD WORLD
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	end)
	
	TeleportTab:Button("Teleport To Sea 3" ,function()
		local args = {
			[1] = "TravelZou" -- OLD WORLD to NEW WORLD
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	end)
	TeleportTab:Line()
	if OldWorld then
		Island = {
			["Start Island"] = CFrame.new(1071.2832, 16.3085976, 1426.86792),
			["Marine Start"] = CFrame.new(-2573.3374, 6.88881969, 2046.99817),
			["Middle Town"] = CFrame.new(-655.824158, 7.88708115, 1436.67908),
			["Jungle"] = CFrame.new(-1249.77222, 11.8870859, 341.356476),
			["Pirate Village"] = CFrame.new(-1122.34998, 4.78708982, 3855.91992),
			["Desert"] = CFrame.new(1094.14587, 6.47350502, 4192.88721),
			["Frozen Village"] = CFrame.new(1198.00928, 27.0074959, -1211.73376),
			["MarineFord"] = CFrame.new(-4505.375, 20.687294, 4260.55908),
			["Colosseum"] = CFrame.new(-1428.35474, 7.38933945, -3014.37305),
			["Sky 1st Floor"] = CFrame.new(-4970.21875, 717.707275, -2622.35449),
			["Sky 2st Floor"] = CFrame.new(-4813.0249, 903.708557, -1912.69055),
			["Sky 3st Floor"] = CFrame.new(-7952.31006, 5545.52832, -320.704956),
			["Prison"] = CFrame.new(4854.16455, 5.68742752, 740.194641),
			["Magma Village"] = CFrame.new(-5231.75879, 8.61593437, 8467.87695),
			["UndeyWater City"] = CFrame.new(61163.8516, 11.7796879, 1819.78418),
			["Fountain City"] = CFrame.new(5132.7124, 4.53632832, 4037.8562),
			["House Cyborg's"] = CFrame.new(6262.72559, 71.3003616, 3998.23047),
			["Shank's Room"] = CFrame.new(-1442.16553, 29.8788261, -28.3547478),
			["Mob Island"] = CFrame.new(-2850.20068, 7.39224768, 5354.99268),
		}
		-- NPC
		NPC = {
			["Random Devil Fruit"] = CFrame.new(-1436.19727, 61.8777695, 4.75247526, -0.557794094, 2.74216543e-08, 0.829979479, 5.83273234e-08, 1, 6.16037932e-09, -0.829979479, 5.18467118e-08, -0.557794094),
			["Blox Fruits Dealer"] = CFrame.new(-923.255066, 7.67800522, 1608.61011, 1, 0, 0, 0, 1, 0, 0, 0, 1),
			["Remove Devil Fruit"] = CFrame.new(5664.80469, 64.677681, 867.85907, 1, 0, 0, 0, 1, 0, 0, 0, 1),
			["Ability Teacher"] = CFrame.new(-1057.67822, 9.65220833, 1799.49146, -0.865874112, -9.26330159e-08, 0.500262439, -7.33759435e-08, 1, 5.816689e-08, -0.500262439, 1.36579752e-08, -0.865874112),
			["Dark Step"] = CFrame.new(-987.873047, 13.7778397, 3989.4978, 1, 0, 0, 0, 1, 0, 0, 0, 1),
			["Electro"] = CFrame.new(-5389.49561, 13.283, -2149.80151, 1, 0, 0, 0, 1, 0, 0, 0, 1),
			["Fishman Karate"] = CFrame.new(61581.8047, 18.8965912, 987.832703, 1, 0, 0, 0, 1, 0, 0, 0, 1),
		}
	elseif NewWorld then
		Island = {
			["First Spot"] = CFrame.new(82.9490662, 18.0710983, 2834.98779),
			["Kingdom of Rose"] = game.Workspace["_WorldOrigin"].Locations["Kingdom of Rose"].CFrame,
			["Dark Ares"] = game.Workspace["_WorldOrigin"].Locations["Dark Arena"].CFrame,
			["Flamingo Mansion"] = CFrame.new(-390.096313, 331.886475, 673.464966),
			["Flamingo Room"] = CFrame.new(2302.19019, 15.1778421, 663.811035),
			["Green bit"] = CFrame.new(-2372.14697, 72.9919434, -3166.51416),
			["Cafe"] = CFrame.new(-385.250916, 73.0458984, 297.388397),
			["Factroy"] = CFrame.new(430.42569, 210.019623, -432.504791),
			["Colosseum"] = CFrame.new(-1836.58191, 44.5890656, 1360.30652),
			["Ghost Island"] = CFrame.new(-5571.84424, 195.182297, -795.432922),
			["Ghost Island 2nd"] = CFrame.new(-5931.77979, 5.19706631, -1189.6908),
			["Snow Mountain"] = CFrame.new(1384.68298, 453.569031, -4990.09766),
			["Hot and Cold"] = CFrame.new(-6026.96484, 14.7461271, -5071.96338),
			["Magma Side"] = CFrame.new(-5478.39209, 15.9775667, -5246.9126),
			["Cursed Ship"] = CFrame.new(902.059143, 124.752518, 33071.8125),
			["Frosted Island"] = CFrame.new(5400.40381, 28.21698, -6236.99219),
			["Forgotten Island"] = CFrame.new(-3043.31543, 238.881271, -10191.5791),
			["Usoapp Island"] = CFrame.new(4748.78857, 8.35370827, 2849.57959),
			["Raids Low"] = CFrame.new(-5554.95313, 329.075623, -5930.31396),
			["Minisky"] = CFrame.new(-260.358917, 49325.7031, -35259.3008),
		}
		-- NPC
		NPC = {
			["Dargon Berath"] = CFrame.new(703.372986, 186.985519, 654.522034, 1, 0, 0, 0, 1, 0, 0, 0, 1),
			["Mtsterious Man"] = CFrame.new(-2574.43335, 1627.92371, -3739.35767, 0.378697902, -9.06400288e-09, 0.92552036, -8.95582009e-09, 1, 1.34578926e-08, -0.92552036, -1.33852689e-08, 0.378697902),
			["Mysterious Scientist"] = CFrame.new(-6437.87793, 250.645355, -4498.92773, 0.502376854, -1.01223634e-08, -0.864648759, 2.34106086e-08, 1, 1.89508653e-09, 0.864648759, -2.11940012e-08, 0.502376854),
			["Awakening Expert"] = CFrame.new(-408.098846, 16.0459061, 247.432846, 0.028394036, 6.17599138e-10, 0.999596894, -5.57905944e-09, 1, -4.59372484e-10, -0.999596894, -5.56376767e-09, 0.028394036),
			["Nerd"] = CFrame.new(-401.783722, 73.0859299, 262.306702, 1, 0, 0, 0, 1, 0, 0, 0, 1),
			["Bar Manager"] = CFrame.new(-385.84726, 73.0458984, 316.088806, 1, 0, 0, 0, 1, 0, 0, 0, 1),
			["Blox Fruits Dealer"] = CFrame.new(-450.725464, 73.0458984, 355.636902, -0.780352175, -2.7266168e-08, 0.625340283, 9.78516468e-09, 1, 5.58128797e-08, -0.625340283, 4.96727601e-08, -0.780352175),
			["Trevor"] = CFrame.new(-341.498322, 331.886444, 643.024963, 1, 0, 0, 0, 1, 0, 0, 0, 1),
			["Plokster"] = CFrame.new(-1885.16016, 88.3838196, -1912.28723, -0.513468027, 0, 0.858108759, 0, 1, 0, -0.858108759, 0, -0.513468027),
			["Enhancement Editor"] = CFrame.new(-346.820221, 72.9856339, 1194.36218, 1, 0, 0, 0, 1, 0, 0, 0, 1),
			["Pirate Recruiter"] = CFrame.new(-428.072998, 72.9495239, 1445.32422, 1, 0, 0, 0, 1, 0, 0, 0, 1),
			["Marines Recruiter"] = CFrame.new(-1349.77295, 72.9853363, -1045.12964, 0.866493046, 0, -0.499189168, 0, 1, 0, 0.499189168, 0, 0.866493046),
			["Chemist"] = CFrame.new(-2777.45288, 72.9919434, -3572.25732, 1, 0, 0, 0, 1, 0, 0, 0, 1),
			["Cyborg"] = CFrame.new(629.146851, 312.307373, -531.624146, 1, 0, 0, 0, 1, 0, 0, 0, 1),
			["Ghoul Mark"] = CFrame.new(635.172546, 125.976357, 33219.832, 1, 0, 0, 0, 1, 0, 0, 0, 1),
			["Guashiem"] = CFrame.new(937.953003, 181.083359, 33277.9297, 1, -8.60126406e-08, 3.81773896e-17, 8.60126406e-08, 1, -1.89969598e-16, -3.8177373e-17, 1.89969598e-16, 1),
			["El Admin"] = CFrame.new(1322.80835, 126.345039, 33135.8789, 0.988783717, -8.69797603e-08, -0.149354503, 8.62223786e-08, 1, -1.15461916e-08, 0.149354503, -1.46101409e-09, 0.988783717),
			["El Rodolfo"] = CFrame.new(941.228699, 40.4686775, 32778.9922, -0.818029106, -1.19524382e-08, 0.575176775, -1.28741648e-08, 1, 2.47053866e-09, -0.575176775, -5.38394795e-09, -0.818029106),
			["Arowe"] = CFrame.new(-1994.51038, 125.519142, -72.2622986, -0.16715166, -6.55417338e-08, -0.985931218, -7.13315558e-08, 1, -5.43836585e-08, 0.985931218, 6.12376851e-08, -0.16715166),
		} 
	elseif ThreeWorld then
		Island = {
			["Prot Town"] = CFrame.new(-287, 30, 5388),
			["Hydar Island"] = CFrame.new(3399.32227, 72.4142914, 1572.99963, -0.809679806, -4.48284467e-08, 0.586871922, 2.42332163e-08, 1, 1.09818842e-07, -0.586871922, 1.0313989e-07, -0.809679806),
			["Room Enma/Yama & Secret Temple"] = CFrame.new(5247, 7, 1097),
			["House Hydar Island"] = CFrame.new(5245, 602, 251),
			["Great Tree"] = CFrame.new(2443, 36, -6573),
			["Castle on the sea"] = CFrame.new(-5500, 314, -2855),
			["Mansion"] = CFrame.new(-12548, 337, -7481),
			["Floating Turtlea"] = CFrame.new(-10016, 332, -8326),
			["Haunted Castle"] = CFrame.new(-9509.34961, 142.130661, 5535.16309),
			["Peanut Island"] = CFrame.new(-2131, 38, -10106),
			["Ice Cream Island"] = CFrame.new(-950, 59, -10907),
			["CakeLoaf"] = CFrame.new(-1762, 38, -11878)
		}
		-- NPC
		NPC = {
			["Random Devil Fruit"] = CFrame.new(-12491, 337, -7449),
			["Blox Fruits Dealer"] = CFrame.new(-12511, 337, -7448),
			["Remove Devil Fruit"] = CFrame.new(-5571, 1089, -2661),
			["Horned Man"] = CFrame.new(-11890, 931, -8760),
			["Hungey Man"] = CFrame.new(-10919, 624, -10268),
			["Previous Hero"] = CFrame.new(-10368, 332, -10128),
			["Butler"] = CFrame.new(-5125, 316, -3130),
			["Lunoven"] = CFrame.new(-5117, 316, -3093),
			["Elite Hunter"] = CFrame.new(-5420, 314, -2828),
			["Player Hunter"] = CFrame.new(-5559, 314, -2840),
			["Uzoth"] = CFrame.new(-9785, 852, 6667),
		}
	end
	SelectedNPC = ""
	SelectedIsland = ""
    local section1 = page4:NewSecction(Teleport Island)
	
	section1:NewDropdown("Selected Island",Island,0,function(a)
		SelectedIsland = a
	end)
	function tweenTarget(targetPos, targetCFrame)
		local tweenfunc = {}
		local tween_s = game:service"TweenService"
		local info = TweenInfo.new((targetPos - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).Magnitude/325, Enum.EasingStyle.Linear)
		local tween = tween_s:Create(game:GetService("Players").LocalPlayer.Character["HumanoidRootPart"], info, {CFrame = targetCFrame * CFrame.fromAxisAngle(Vector3.new(1,0,0), math.rad(0))})
		tween:Play()
	
		function tweenfunc:Stop()
			tween:Cancel()
			return tween
		end
	
		if not tween then return tween end
		return tweenfunc
	end
	spawn(function()
		while true do wait()
			if TweenIsland then
				TweenIslandWork = tweenTarget(Island[SelectedIsland].Position,Island[SelectedIsland])
				if (Island[SelectedIsland].Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 350 then
					if TweenIslandWork then
						TweenIslandWork:Stop()
					end
					game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = Island[SelectedIsland]
				end
			end
			if TweenNPC then
				TweenNPCWork = tweenTarget(NPC[SelectedNPC].Position,Island[SelectedIsland])
				if (Island[SelectedIsland].Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 350 then
					if TweenNPCWork then
						TweenNPCWork:Stop()
					end
					game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = Island[SelectedIsland]
				end
			end
		end
	end)
	section1:Toggle("Teleport Island",false,function(a)
		TweenIsland = a
		if not TweenIsland then
			if TweenIslandWork then
				TweenIslandWork:Stop()
			end
		end
	end)
	local section2 = page4:NewSecction("Teleport NPCs")
	section2:NewDropdown("Selected NPC",NPC,0,function(a)
		SelectedNPC = a
	end)
	section2:Toggle("Teleport NPC",false,function(a)
		TweenNPC = a
		if not TweenNPC then
			if TweenNPCWork then
				TweenNPCWork:Stop()
			end
		end
	end)
	----------------------------------------------------------------------------------------------------------------------------
    local page5 = win:NewPage("Player-Esp")
	local SelectedPly = PlayerEspTab:NewSecction("Selected Player : nil")
	PlayerName = {}
	for i,v in pairs(game.Players:GetChildren()) do  
		table.insert(PlayerName ,v.Name)
	end
	SelectedKillPlayer = ""
	local Player = PlayerEspTab:Dropdown("Selected Player",PlayerName,0,function(plys) --true/false, replaces the current title "Dropdown" with the option that t
		SelectedKillPlayer = plys
		SelectedPly:Refresh("Selected Player : "..SelectedKillPlayer)
	end)
	PlayerEspTab:Button("Refrsh Player",function()
		PlayerName = {}
		for i,v in pairs(game.Players:GetChildren()) do  
			table.insert(PlayerName ,v.Name)
		end
		Player:Refresh(PlayerName,0)
	end)
	PlayerEspTab:Toggle("Kill Player",false,function(bool)
		KillPlayer = bool
	end)
	
	PlayerEspTab:Toggle("Bounty Hop Only Melee",getgenv().Setting["Bounty Hop"],function(bool)
		BountyHop = bool
	end)
	
	spawn(function()
		while wait() do
			for i,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do  
				if v:IsA("Tool") then
					if v:FindFirstChild("RemoteFunctionShoot") then 
						_G.WeaponUseKillGun = v.Name
					end
				end
			end
		end
	end)
	
	spawn(function()
		game:GetService("RunService").Heartbeat:connect(function()
			pcall(function()
				if BountyHop == true or _G.HopServerOn == true then
					if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Humanoid") then
						if syn then
							game:GetService("Players").LocalPlayer.Character.Humanoid:ChangeState(11)
						else
							for _, v in pairs(game.Players.LocalPlayer.Character:GetDescendants()) do
								if v:IsA("BasePart") then
									v.CanCollide = false    
								end
							end
						end
					end
				end
			end)
		end)
	end)
	
	spawn(function()
		while wait() do
			pcall(function()
				if BountyHop then
					wait(120)
					_G.HopServerOn = true
				end
			end)
		end
	end)
	
	spawn(function()
		while wait(1) do
			pcall(function()
				if BountyHop then
					if game:GetService("Players")["LocalPlayer"].PlayerGui.Main.PvpDisabled.Visible == true then
						local args = {
							[1] = "EnablePvp"
						}
	
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
					end
				end
			end)
		end
	end)
	spawn(function()
		if BountyHop then
			if not game.Players.LocalPlayer.Character:FindFirstChild("HasBuso") then
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Buso")
			end
		end
	end)
	
	spawn(function()
		while wait(1) do
			pcall(function()
				if BountyHop then
					if not game.Players.LocalPlayer.Character:FindFirstChild("HasBuso") then
						game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Buso")
					end
				end
			end)
		end
	end)
	
	spawn(function()
		while wait() do
			pcall(function()
				if BountyHop then
					game:GetService'VirtualUser':CaptureController()
					game:GetService'VirtualUser':Button1Down(Vector2.new(1280, 672))
				end
			end)
		end
	end)
	
	spawn(function()
		while wait(1) do
			if BountyHop then
				if OldWorld then
					game.Players.LocalPlayer:Kick("Not Support First Sea")
					break
				end
			end
		end
	end)
	_G.GodModeOn = false
	
	spawn(function()
		while wait() do
			if BountyHop then
				wait(.1)
				if OldWorld then
					game.Players.LocalPlayer:Kick("\n Not Support First Sea ")
				end
				if game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("CrewBBG") then
					game.Players.LocalPlayer.Character.HumanoidRootPart.CrewBBG:Destroy()
				end
				wait(.1)
				_G.GodModeOn = true
				break
			end
		end
	end)
	
	if _G.DistancePlayers == nil then
		_G.DistancePlayers = 10
	end
	
	killandhopsize = false
	
	spawn(function()
		while wait() do
			pcall(function()
				if BountyHop and killandhopsize then
					for i, v in pairs(game:GetService("Workspace").Characters:GetChildren()) do
						if v.Name == NameKill then
							v.HumanoidRootPart.CanCollide = false
							v.HumanoidRootPart.Size = Vector3.new(120,120,120)
						end
					end
				end
			end)
		end
	end)
	
	spawn(function()
		while wait() do
			if _G.SelectWeaponKillHop == nil or _G.SelectWeaponKillHop == "" then
				for i ,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
					if v.ToolTip == "Melee" then
						_G.SelectWeaponKillHop = v.Name
					end
				end
				for i ,v in pairs(game.Players.LocalPlayer.Character:GetChildren()) do
					if v.ToolTip == "Melee" then
						_G.SelectWeaponKillHop = v.Name
					end
				end
			end
		end
	end)
	
	spawn(function()
		while wait() do
			pcall(function()
				if BountyHop then
					for i, v in pairs(game:GetService("Workspace").Characters:GetChildren()) do
						if game:GetService("Players")[v.Name].Data.Level.Value >= 1200 and v.Name ~= game.Players.LocalPlayer.Name and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") then
							repeat game:GetService('RunService').Stepped:wait()
								if _G.GodModeOn then
									if game.Players.LocalPlayer.Backpack:FindFirstChild(_G.SelectWeaponKillHop) or game.Players.LocalPlayer.Character:FindFirstChild(_G.SelectWeaponKillHop) then
										if not game.Players.LocalPlayer.Character:FindFirstChild("HasBuso") then
											game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Buso")
										end
										EquipWeapon(_G.SelectWeaponKillHop)
										spawn(function()
											if (v.HumanoidRootPart.Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 75 then
												game:service('VirtualInputManager'):SendKeyEvent(true, "X", false, game)
												wait()
												game:service('VirtualInputManager'):SendKeyEvent(false, "X", false, game)
											end
										end)
										NameKill = v.Name
										KillHealt = v.Humanoid.Health
										MaxKillHealt = v.Humanoid.MaxHealth
										killandhopsize = true
										MytoTarget(v.HumanoidRootPart.CFrame * CFrame.new(0,_G.DistancePlayers,-15))
									end
								end
							until not v.Parent or not v or not v:FindFirstChild("Humanoid") or not v:FindFirstChild("HumanoidRootPart") or BountyHop == false or v.Humanoid.Health <= 0 or NextPlayer == true or _G.HopServerOn == true
							NextPlayer = false
							killandhopsize = false
						end
					end
				elseif _G.HopServerOn == true then
					repeat wait()
						killandhopsize = false
						MytoTarget(CFrame.new(-390.096313, 331.886475, 673.464966))
					until BountyHop == false or _G.HopServerOn == false
				end
			end)
		end
	end)
	
	spawn(function()
		while wait() do
			if _G.HopServerOn == true then
				pcall(function()
					BountyHop = false
					killandhopsize = false
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
				end)
			end
		end
	end)
	
	PlayerEspTab:Toggle("Spectate Player",false,function(bool)
		Sp = bool
		local plr1 = game.Players.LocalPlayer.Character.Humanoid
		local plr2 = game.Players:FindFirstChild(SelectedKillPlayer)
		repeat wait(.1)
			game.Workspace.Camera.CameraSubject = plr2.Character.Humanoid
		until Sp == false 
		game.Workspace.Camera.CameraSubject = game.Players.LocalPlayer.Character.Humanoid
	end)
	PlayerEspTab:Button("Teleport Player",function()
		local plr1 = game.Players.LocalPlayer.Character
		local plr2 = game.Players:FindFirstChild(SelectedKillPlayer)
		plr1.HumanoidRootPart.CFrame = plr2.Character.HumanoidRootPart.CFrame
	end)
	PlayerEspTab:Toggle("Aimbot Gun",false,function(bool)
		if SelectedKillPlayer == "" and bool then
			library:Notification("Select Player to Aim")
		else
			Aimbot = bool
		end
	end)
	local lp = game:GetService('Players').LocalPlayer
	local mouse = lp:GetMouse()
	mouse.Button1Down:Connect(function()
		if Aimbot and game.Players.LocalPlayer.Character:FindFirstChild(SelectToolWeaponGun) and game:GetService("Players"):FindFirstChild(SelectedKillPlayer) then
			tool = game:GetService("Players").LocalPlayer.Character[SelectToolWeaponGun]
			v17 = workspace:FindPartOnRayWithIgnoreList(Ray.new(tool.Handle.CFrame.p, (game:GetService("Players"):FindFirstChild(SelectedKillPlayer).Character.HumanoidRootPart.Position - tool.Handle.CFrame.p).unit * 100), { game.Players.LocalPlayer.Character, workspace._WorldOrigin });
			game:GetService("Players").LocalPlayer.Character[SelectToolWeaponGun].RemoteFunctionShoot:InvokeServer(game:GetService("Players"):FindFirstChild(SelectedKillPlayer).Character.HumanoidRootPart.Position, (require(game.ReplicatedStorage.Util).Other.hrpFromPart(v17)));
		end 
	end)
	PlayerEspTab:Toggle("Aimbot Skill",false,function(bool)
		if SelectedKillPlayer == "" and bool then
			library:Notification("Select Player to Aim")
		else
			Skillaimbot = bool
		end
	end)
	spawn(function()
		while wait() do
			if KillPlayer then
				if game.Players:FindFirstChild(SelectedKillPlayer) and (game.Players:FindFirstChild(SelectedKillPlayer).Character.HumanoidRootPart.Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).magnitude >= 300 then
					KillTween = toTarget(game.Players:FindFirstChild(SelectedKillPlayer).Character.HumanoidRootPart.Position,game.Players:FindFirstChild(SelectedKillPlayer).Character.HumanoidRootPart.CFrame)
				elseif game.Players:FindFirstChild(SelectedKillPlayer) and (game.Players:FindFirstChild(SelectedKillPlayer).Character.HumanoidRootPart.Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).magnitude >= 300 then
					game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players:FindFirstChild(SelectedKillPlayer).Character.HumanoidRootPart.CFrame * CFrame.new(0,25,0)
					game.Players:FindFirstChild(SelectedKillPlayer).Character.HumanoidRootPart.CanCollide = false
					game.Players:FindFirstChild(SelectedKillPlayer).Character.HumanoidRootPart.Size = Vector3.new(50,50,50)
					EquipWeapon(SelectToolWeaponGun)
					if game.Players.LocalPlayer.Character:FindFirstChild(SelectToolWeaponGun) then
						spawn(function()
							pcall(function()
								local args = {
									[1] = v.HumanoidRootPart.Position,
									[2] = v.HumanoidRootPart
								}
								game:GetService("Players").LocalPlayer.Character[SelectToolWeaponGun].RemoteFunctionShoot:InvokeServer(unpack(args))
							end)
						end)
					end 
				end
			end 
			if Skillaimbot then
				if game.Players:FindFirstChild(SelectedKillPlayer) and game.Players:FindFirstChild(SelectedKillPlayer).Character:FindFirstChild("HumanoidRootPart") and game.Players:FindFirstChild(SelectedKillPlayer).Character:FindFirstChild("Humanoid") and game.Players:FindFirstChild(SelectedKillPlayer).Character.Humanoid.Health > 0 then
					AimBotSkillPosition = game.Players:FindFirstChild(SelectedKillPlayer).Character:FindFirstChild("HumanoidRootPart").Position
				end
			end
		end
	end)
	-- ESP
	function isnil(thing)
		return (thing == nil)
	end
	local function round(n)
		return math.floor(tonumber(n) + 0.5)
	end
	Number = math.random(1, 1000000)
	function UpdatePlayerChams()
		for i,v in pairs(game:GetService'Players':GetChildren()) do
			pcall(function()
				if not isnil(v.Character) then
					if ESPPlayer then
						if not isnil(v.Character.Head) and not v.Character.Head:FindFirstChild('NameEsp'..Number) then
							local bill = Instance.new('BillboardGui',v.Character.Head)
							bill.Name = 'NameEsp'..Number
							bill.ExtentsOffset = Vector3.new(0, 1, 0)
							bill.Size = UDim2.new(1,200,1,30)
							bill.Adornee = v.Character.Head
							bill.AlwaysOnTop = true
							local name = Instance.new('TextLabel',bill)
							name.Font = "GothamBold"
							name.FontSize = "Size14"
							name.TextWrapped = true
							name.Text = (v.Name ..' \n'.. round((game:GetService('Players').LocalPlayer.Character.Head.Position - v.Character.Head.Position).Magnitude/3) ..' M')
							name.Size = UDim2.new(1,0,1,0)
							name.TextYAlignment = 'Top'
							name.BackgroundTransparency = 1
							name.TextStrokeTransparency = 0.5
							if v.Team == game.Players.LocalPlayer.Team then
								name.TextColor3 = Color3.new(0,255,0)
							else
								name.TextColor3 = Color3.new(255,0,0)
							end
						else
							v.Character.Head['NameEsp'..Number].TextLabel.Text = (v.Name ..' | '.. round((game:GetService('Players').LocalPlayer.Character.Head.Position - v.Character.Head.Position).Magnitude/3) ..' M\nHealth : ' .. round(v.Character.Humanoid.Health*100/v.Character.Humanoid.MaxHealth) .. '%')
						end
					else
						if v.Character.Head:FindFirstChild('NameEsp'..Number) then
							v.Character.Head:FindFirstChild('NameEsp'..Number):Destroy()
						end
					end
				end
			end)
		end
	end
	function UpdateChestChams() 
		for i,v in pairs(game.Workspace:GetChildren()) do
			pcall(function()
				if string.find(v.Name,"Chest") then
					if ChestESP then
						if string.find(v.Name,"Chest") then
							if not v:FindFirstChild('NameEsp'..Number) then
								local bill = Instance.new('BillboardGui',v)
								bill.Name = 'NameEsp'..Number
								bill.ExtentsOffset = Vector3.new(0, 1, 0)
								bill.Size = UDim2.new(1,200,1,30)
								bill.Adornee = v
								bill.AlwaysOnTop = true
								local name = Instance.new('TextLabel',bill)
								name.Font = "GothamBold"
								name.FontSize = "Size14"
								name.TextWrapped = true
								name.Size = UDim2.new(1,0,1,0)
								name.TextYAlignment = 'Top'
								name.BackgroundTransparency = 1
								name.TextStrokeTransparency = 0.5
								if v.Name == "Chest1" then
									name.TextColor3 = Color3.fromRGB(109, 109, 109)
									name.Text = ("Chest 1" ..' \n'.. round((game:GetService('Players').LocalPlayer.Character.Head.Position - v.Position).Magnitude/3) ..' M')
								end
								if v.Name == "Chest2" then
									name.TextColor3 = Color3.fromRGB(173, 158, 21)
									name.Text = ("Chest 2" ..' \n'.. round((game:GetService('Players').LocalPlayer.Character.Head.Position - v.Position).Magnitude/3) ..' M')
								end
								if v.Name == "Chest3" then
									name.TextColor3 = Color3.fromRGB(85, 255, 255)
									name.Text = ("Chest 3" ..' \n'.. round((game:GetService('Players').LocalPlayer.Character.Head.Position - v.Position).Magnitude/3) ..' M')
								end
							else
								v['NameEsp'..Number].TextLabel.Text = (v.Name ..'   \n'.. round((game:GetService('Players').LocalPlayer.Character.Head.Position - v.Position).Magnitude/3) ..' M')
							end
						end
					else
						if v:FindFirstChild('NameEsp'..Number) then
							v:FindFirstChild('NameEsp'..Number):Destroy()
						end
					end
				end
			end)
		end
	end
	function UpdateDevilChams() 
		for i,v in pairs(game.Workspace:GetChildren()) do
			pcall(function()
				if DevilFruitESP then
					if string.find(v.Name, "Fruit") then   
						if not v.Handle:FindFirstChild('NameEsp'..Number) then
							local bill = Instance.new('BillboardGui',v.Handle)
							bill.Name = 'NameEsp'..Number
							bill.ExtentsOffset = Vector3.new(0, 1, 0)
							bill.Size = UDim2.new(1,200,1,30)
							bill.Adornee = v.Handle
							bill.AlwaysOnTop = true
							local name = Instance.new('TextLabel',bill)
							name.Font = "GothamBold"
							name.FontSize = "Size14"
							name.TextWrapped = true
							name.Size = UDim2.new(1,0,1,0)
							name.TextYAlignment = 'Top'
							name.BackgroundTransparency = 1
							name.TextStrokeTransparency = 0.5
							name.TextColor3 = Color3.fromRGB(255, 0, 0)
							name.Text = (v.Name ..' \n'.. round((game:GetService('Players').LocalPlayer.Character.Head.Position - v.Handle.Position).Magnitude/3) ..' M')
						else
							v.Handle['NameEsp'..Number].TextLabel.Text = (v.Name ..'   \n'.. round((game:GetService('Players').LocalPlayer.Character.Head.Position - v.Handle.Position).Magnitude/3) ..' M')
						end
					end
				else
					if v.Handle:FindFirstChild('NameEsp'..Number) then
						v.Handle:FindFirstChild('NameEsp'..Number):Destroy()
					end
				end
			end)
		end
	end
	function UpdateFlowerChams() 
		for i,v in pairs(game.Workspace:GetChildren()) do
			pcall(function()
				if v.Name == "Flower2" or v.Name == "Flower1" then
					if FlowerESP then 
						if not v:FindFirstChild('NameEsp'..Number) then
							local bill = Instance.new('BillboardGui',v)
							bill.Name = 'NameEsp'..Number
							bill.ExtentsOffset = Vector3.new(0, 1, 0)
							bill.Size = UDim2.new(1,200,1,30)
							bill.Adornee = v
							bill.AlwaysOnTop = true
							local name = Instance.new('TextLabel',bill)
							name.Font = "GothamBold"
							name.FontSize = "Size14"
							name.TextWrapped = true
							name.Size = UDim2.new(1,0,1,0)
							name.TextYAlignment = 'Top'
							name.BackgroundTransparency = 1
							name.TextStrokeTransparency = 0.5
							name.TextColor3 = Color3.fromRGB(255, 0, 0)
							if v.Name == "Flower1" then 
								name.Text = ("Blue Flower" ..' \n'.. round((game:GetService('Players').LocalPlayer.Character.Head.Position - v.Position).Magnitude/3) ..' M')
								name.TextColor3 = Color3.fromRGB(0, 0, 255)
							end
							if v.Name == "Flower2" then
								name.Text = ("Red Flower" ..' \n'.. round((game:GetService('Players').LocalPlayer.Character.Head.Position - v.Position).Magnitude/3) ..' M')
								name.TextColor3 = Color3.fromRGB(255, 0, 0)
							end
						else
							v['NameEsp'..Number].TextLabel.Text = (v.Name ..'   \n'.. round((game:GetService('Players').LocalPlayer.Character.Head.Position - v.Position).Magnitude/3) ..' M')
						end
					else
						if v:FindFirstChild('NameEsp'..Number) then
						v:FindFirstChild('NameEsp'..Number):Destroy()
						end
					end
				end   
			end)
		end
	end
	function UpdateRealFruitChams() 
		for i,v in pairs(game.Workspace.AppleSpawner:GetChildren()) do
			if v:IsA("Tool") then
				if RealFruitESP then 
					if not v.Handle:FindFirstChild('NameEsp'..Number) then
						local bill = Instance.new('BillboardGui',v.Handle)
						bill.Name = 'NameEsp'..Number
						bill.ExtentsOffset = Vector3.new(0, 1, 0)
						bill.Size = UDim2.new(1,200,1,30)
						bill.Adornee = v.Handle
						bill.AlwaysOnTop = true
						local name = Instance.new('TextLabel',bill)
						name.Font = "GothamBold"
						name.FontSize = "Size14"
						name.TextWrapped = true
						name.Size = UDim2.new(1,0,1,0)
						name.TextYAlignment = 'Top'
						name.BackgroundTransparency = 1
						name.TextStrokeTransparency = 0.5
						name.TextColor3 = Color3.fromRGB(255, 0, 0)
						name.Text = (v.Name ..' \n'.. round((game:GetService('Players').LocalPlayer.Character.Head.Position - v.Handle.Position).Magnitude/3) ..' M')
					else
						v.Handle['NameEsp'..Number].TextLabel.Text = (v.Name ..' '.. round((game:GetService('Players').LocalPlayer.Character.Head.Position - v.Handle.Position).Magnitude/3) ..' M')
					end
				else
					if v.Handle:FindFirstChild('NameEsp'..Number) then
						v.Handle:FindFirstChild('NameEsp'..Number):Destroy()
					end
				end 
			end
		end
		for i,v in pairs(game.Workspace.PineappleSpawner:GetChildren()) do
			if v:IsA("Tool") then
				if RealFruitESP then 
					if not v.Handle:FindFirstChild('NameEsp'..Number) then
						local bill = Instance.new('BillboardGui',v.Handle)
						bill.Name = 'NameEsp'..Number
						bill.ExtentsOffset = Vector3.new(0, 1, 0)
						bill.Size = UDim2.new(1,200,1,30)
						bill.Adornee = v.Handle
						bill.AlwaysOnTop = true
						local name = Instance.new('TextLabel',bill)
						name.Font = "GothamBold"
						name.FontSize = "Size14"
						name.TextWrapped = true
						name.Size = UDim2.new(1,0,1,0)
						name.TextYAlignment = 'Top'
						name.BackgroundTransparency = 1
						name.TextStrokeTransparency = 0.5
						name.TextColor3 = Color3.fromRGB(255, 174, 0)
						name.Text = (v.Name ..' \n'.. round((game:GetService('Players').LocalPlayer.Character.Head.Position - v.Handle.Position).Magnitude/3) ..' M')
					else
						v.Handle['NameEsp'..Number].TextLabel.Text = (v.Name ..' '.. round((game:GetService('Players').LocalPlayer.Character.Head.Position - v.Handle.Position).Magnitude/3) ..' M')
					end
				else
					if v.Handle:FindFirstChild('NameEsp'..Number) then
						v.Handle:FindFirstChild('NameEsp'..Number):Destroy()
					end
				end 
			end
		end
		for i,v in pairs(game.Workspace.BananaSpawner:GetChildren()) do
			if v:IsA("Tool") then
				if RealFruitESP then 
					if not v.Handle:FindFirstChild('NameEsp'..Number) then
						local bill = Instance.new('BillboardGui',v.Handle)
						bill.Name = 'NameEsp'..Number
						bill.ExtentsOffset = Vector3.new(0, 1, 0)
						bill.Size = UDim2.new(1,200,1,30)
						bill.Adornee = v.Handle
						bill.AlwaysOnTop = true
						local name = Instance.new('TextLabel',bill)
						name.Font = "GothamBold"
						name.FontSize = "Size14"
						name.TextWrapped = true
						name.Size = UDim2.new(1,0,1,0)
						name.TextYAlignment = 'Top'
						name.BackgroundTransparency = 1
						name.TextStrokeTransparency = 0.5
						name.TextColor3 = Color3.fromRGB(251, 255, 0)
						name.Text = (v.Name ..' \n'.. round((game:GetService('Players').LocalPlayer.Character.Head.Position - v.Handle.Position).Magnitude/3) ..' M')
					else
						v.Handle['NameEsp'..Number].TextLabel.Text = (v.Name ..' '.. round((game:GetService('Players').LocalPlayer.Character.Head.Position - v.Handle.Position).Magnitude/3) ..' M')
					end
				else
					if v.Handle:FindFirstChild('NameEsp'..Number) then
						v.Handle:FindFirstChild('NameEsp'..Number):Destroy()
					end
				end 
			end
		end
	end
	PlayerEspTab:Line()
	PlayerEspTab:Label("ESP")
	PlayerEspTab:Toggle("ESP Player",espplyer,function(a)
		ESPPlayer = a
		UpdatePlayerChams()
	end)
	PlayerEspTab:Toggle("ESP Chest",espchest,function(a)
		ChestESP = a
		UpdateChestChams() 
	end)
	PlayerEspTab:Toggle("ESP Devil Fruit",espdevilfruit,function(a)
		DevilFruitESP = a
		UpdateDevilChams() 
	end)
	PlayerEspTab:Toggle("ESP Flower",espflower,function(a)
		FlowerESP = a
		UpdateFlowerChams() 
	end)
	PlayerEspTab:Toggle("ESP Real Fruit",esprealfruit,function(a)
		RealFruitESP = a
		UpdateRealFruitChams() 
	end)
	spawn(function()
		while wait() do
			if FlowerESP then
				UpdateFlowerChams() 
			end
			if DevilFruitESP then
				UpdateDevilChams() 
			end
			if ChestESP then
				UpdateChestChams() 
			end
			if ESPPlayer then
				UpdatePlayerChams()
			end
			if RealFruitESP then
				UpdateRealFruitChams()
			end
		end
	end)
	----------------------------------------------------------------------------------------------------------------------------
	local MiscTab = page6:NewSecction("Misc")
	MiscTab:Label("Server Time")
	Time = MiscTab:Label("Server Time")
	local function UpdateTime()
		local GameTime = math.floor(workspace.DistributedGameTime+0.5)
		local Hour = math.floor(GameTime/(60^2))%24
		local Minute = math.floor(GameTime/(60^1))%60
		local Second = math.floor(GameTime/(60^0))%60
		Time:Refresh("Hour : "..Hour.." Minute : "..Minute.." Second : "..Second)
	end
	spawn(function()
		while true do
			UpdateTime()
			game:GetService("RunService").RenderStepped:Wait()
		end
	end)
	MiscTab:Line()
	MiscTab:Label("Auto Farm Level Lock")
	LockLevelValue = 2300
	OldLevel = game.Players.localPlayer.Data.Level.Value
	MiscTab:Slider("Select Level Lock",1,LockLevelValue,LockLevelValue,nil,function(value)
		LockLevelValue = value
	end)
	MiscTab:Toggle("Lock Level",locklevel,function(value)
		LockLevel = value
	end)
	spawn(function()
		while wait(.1) do
			if LockLevel then
				if game.Players.localPlayer.Data.Level.Value >= LockLevelValue then
					game.Players.localPlayer:Kick("\n Auto Farm Completed Level : "..game.Players.localPlayer.Data.Level.Value.."\n Old Level : "..OldLevel.."\nUsername : "..game.Players.LocalPlayer.Name)
				end
			end
		end
	end)
	MiscTab:Line()
	MiscTab:Button("Join Pirates Team",function()
		local args = {
			[1] = "SetTeam",
			[2] = "Pirates"
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args)) 
		local args = {
			[1] = "BartiloQuestProgress"
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
		local args = {
			[1] = "Buso"
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	end)
	MiscTab:Button("Join Marines Team",function()
		local args = {
			[1] = "SetTeam",
			[2] = "Marines"
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
		local args = {
			[1] = "BartiloQuestProgress"
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
		local args = {
			[1] = "Buso"
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	end)
	MiscTab:Line()
	MiscTab:Button("Check Ectoplasm",function()
		VLib:Notification("You have "..game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Ectoplasm","Check").." Ectoplasm")
	end)
	MiscTab:Button("Open Devil Shop",function()
		local args = {
			[1] = "GetFruits"
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
		game.Players.localPlayer.PlayerGui.Main.FruitShop.Visible = true
	end)
	MiscTab:Button("Open Inventory",function()
		local args = {
			[1] = "getInventoryWeapons"
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
		game.Players.localPlayer.PlayerGui.Main.Inventory.Visible = true
	end)
	MiscTab:Button("Open Fruit Inventory",function()
		game.Players.localPlayer.PlayerGui.Main.FruitInventory.Visible = true
	end)
	MiscTab:Button("Open Color Haki",function()
		game.Players.localPlayer.PlayerGui.Main.Colors.Visible = true
	end)
	MiscTab:Button("Open Title Name",function()
		local args = {
			[1] = "getTitles"
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
		game.Players.localPlayer.PlayerGui.Main.Titles.Visible = true
	end)
	MiscTab:Line()
	
	local LocalPlayer = game:GetService'Players'.LocalPlayer
	local originalstam = LocalPlayer.Character.Energy.Value
	function infinitestam()
		game:GetService'Players'.LocalPlayer.Character.Energy.Changed:connect(function()
			if InfinitsEnergy then
				LocalPlayer.Character.Energy.Value = originalstam
			end 
		end)
	end
	nododgecool = false
	function NoDodgeCool()
		if nododgecool then
			for i,v in next, getgc() do
				if game.Players.LocalPlayer.Character.Dodge then
					if typeof(v) == "function" and getfenv(v).script == game.Players.LocalPlayer.Character.Dodge then
						for i2,v2 in next, getupvalues(v) do
							if tostring(v2) == "0.4" then
								repeat wait(.1)
									setupvalue(v,i2,0)
								until not nododgecool
							end
						end
					end
				end
			end
		end
	end
	function NoGeppoCool()
		if noGeppocool then
			for i,v in next, getgc() do
				if game.Players.LocalPlayer.Character.Geppo then
					if typeof(v) == "function" and getfenv(v).script == game.Players.LocalPlayer.Character.Geppo then
						for i2,v2 in next, getupvalues(v) do
							if tostring(v2) == "0" then
								repeat wait(.1)
									setupvalue(v,i2,0)
								until not noGeppocool
							end
						end
					end
				end
			end
		end
	end
	function NoSoruCool()
		for i, v in pairs(getgc()) do
			if type(v) == "function" and getfenv(v).script == game.Players.LocalPlayer.Character:WaitForChild("Soru") then
				for i2,v2 in pairs(debug.getupvalues(v)) do
					if type(v2) == 'table' then
						if v2.LastUse then
							repeat wait()
								setupvalue(v, i2, {LastAfter = 0,LastUse = 0})
							until not Sorunocool
						end
					end
				end
			end
		end
	end
	MiscTab:Button("Dodge No Cooldown",function()
		loadstring(game:HttpGet("https://raw.githubusercontent.com/NightsTimeZ/Donate-Me/main/Thx.lua"))()
	end)
	MiscTab:Toggle("Dodge No Cooldown",false,function(Value)
		nododgecool = Value
		NoDodgeCool()
	end)
	MiscTab:Toggle("Soru No Cooldown",false,function(Value)
		Sorunocool = Value
		NoSoruCool()
	end)
	MiscTab:Toggle("Infinits Geppo",false,function(Value)
		noGeppocool = Value
		NoGeppoCool()
	end)
	MiscTab:Toggle("Infinits Energy",infengergy,function(value)
		InfinitsEnergy = value
		infinitestam()
	end)
	MiscTab:Toggle("Infinits Range observations haki",false,function(Value)
		infobservations = Value
	end)
	spawn(function()
		while wait() do
			if infobservations then
				game.Players.LocalPlayer.VisionRadius.Value = math.huge
			end
		end
	end)
	MiscTab:Toggle("Auto Click",autoclick,function(value)
		AuctoClick = value
	end)
	spawn(function()
		while wait() do
			if AuctoClick then
				Click()
			end
		end
	end)
	Fly = false  
	function activatefly()
		local mouse=game.Players.LocalPlayer:GetMouse''
		localplayer=game.Players.LocalPlayer
		game.Players.LocalPlayer.Character:WaitForChild("HumanoidRootPart")
		local torso = game.Players.LocalPlayer.Character.HumanoidRootPart
		local speedSET=25
		local keys={a=false,d=false,w=false,s=false}
		local e1
		local e2
		local function start()
			local pos = Instance.new("BodyPosition",torso)
			local gyro = Instance.new("BodyGyro",torso)
			pos.Name="EPIXPOS"
			pos.maxForce = Vector3.new(math.huge, math.huge, math.huge)
			pos.position = torso.Position
			gyro.maxTorque = Vector3.new(9e9, 9e9, 9e9)
			gyro.cframe = torso.CFrame
			repeat
				wait()
				localplayer.Character.Humanoid.PlatformStand=true
				local new=gyro.cframe - gyro.cframe.p + pos.position
				if not keys.w and not keys.s and not keys.a and not keys.d then
					speed=1
				end
				if keys.w then
					new = new + workspace.CurrentCamera.CoordinateFrame.lookVector * speed
					speed=speed+speedSET
				end
				if keys.s then
					new = new - workspace.CurrentCamera.CoordinateFrame.lookVector * speed
					speed=speed+speedSET
				end
				if keys.d then
					new = new * CFrame.new(speed,0,0)
					speed=speed+speedSET
				end
				if keys.a then
					new = new * CFrame.new(-speed,0,0)
					speed=speed+speedSET
				end
				if speed>speedSET then
					speed=speedSET
				end
					pos.position=new.p
				if keys.w then
					gyro.cframe = workspace.CurrentCamera.CoordinateFrame*CFrame.Angles(-math.rad(speed*15),0,0)
				elseif keys.s then
					gyro.cframe = workspace.CurrentCamera.CoordinateFrame*CFrame.Angles(math.rad(speed*15),0,0)
				else
					gyro.cframe = workspace.CurrentCamera.CoordinateFrame
				end
			until not Fly
			if gyro then 
				gyro:Destroy() 
			end
			if pos then 
				pos:Destroy() 
			end
			flying=false
			localplayer.Character.Humanoid.PlatformStand=false
			speed=0
		end
		e1=mouse.KeyDown:connect(function(key)
			if not torso or not torso.Parent then 
				flying=false e1:disconnect() e2:disconnect() return 
			end
			if key=="w" then
				keys.w=true
			elseif key=="s" then
				keys.s=true
			elseif key=="a" then
				keys.a=true
			elseif key=="d" then
				keys.d=true
			end
		end)
		e2=mouse.KeyUp:connect(function(key)
			if key=="w" then
				keys.w=false
			elseif key=="s" then
				keys.s=false
			elseif key=="a" then
				keys.a=false
			elseif key=="d" then
				keys.d=false
			end
		end)
		start()
	end
	MiscTab:Toggle("Fly",false,function(Value)
		Fly = Value
		activatefly()
	end)
	MiscTab:Toggle("No Clip",false,function(value)
		NoClip = value
	end)
	if game.workspace:FindFirstChild("WaterWalk") then
		game.workspace:FindFirstChild("WaterWalk"):Destroy()
	end
	platform = Instance.new("Part")
	platform.Name = "WaterWalk"
	platform.Size = Vector3.new(math.huge, 1, math.huge)
	platform.Transparency = 1
	platform.Anchored = true
	platform.Parent = game.workspace
	MiscTab:Toggle("Water Walk",waterwalk,function(value)
		WaterWalk = value
	end)
	spawn(function()
		while wait() do
			if WaterWalk then
				platform.CanCollide = true
				platform.Position = Vector3.new(game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position.X,game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position.Y * 0 -5, game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position.Z)
			else
				platform.CanCollide = false
				platform.Position = Vector3.new(game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position.X,game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position.Y * 0 -6, game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position.Z)
			end
		end
	end)
	MiscTab:Button("Remove Lave",function()
		for i,v in pairs(game.Workspace:GetDescendants()) do
			if v.Name == "Lava" then   
				v:Destroy()
			end
		end
		for i,v in pairs(game.ReplicatedStorage:GetDescendants()) do
			if v.Name == "Lava" then   
				v:Destroy()
			end
		end
	end)
	MiscTab:Button("Redeem All Code",function()
		function UseCode(Text)
			game:GetService("ReplicatedStorage").Remotes.Redeem:InvokeServer(Text)
		end
		UseCode("SUB2GAMERROBOT_EXP1")
		UseCode("StrawHatMaine")
		UseCode("Sub2OfficialNoobie")
		UseCode("FUDD10")
		UseCode("BIGNEWS")
		UseCode("THEGREATACE")
		UseCode("SUB2NOOBMASTER123")
		UseCode("Sub2Daigrock")
		UseCode("Axiore")
		UseCode("TantaiGaming")
		UseCode("STRAWHATMAINE")
	end)
	MiscTab:Button("FPS Boost",function()
		local decalsyeeted = true -- Leaving this on makes games look shitty but the fps goes up by at least 20.
		local g = game
		local w = g.Workspace
		local l = g.Lighting
		local t = w.Terrain
		t.WaterWaveSize = 0
		t.WaterWaveSpeed = 0
		t.WaterReflectance = 0
		t.WaterTransparency = 0
		l.GlobalShadows = false
		l.FogEnd = 9e9
		l.Brightness = 0
		settings().Rendering.QualityLevel = "Level01"
		for i, v in pairs(g:GetDescendants()) do
			if v:IsA("Part") or v:IsA("Union") or v:IsA("CornerWedgePart") or v:IsA("TrussPart") then 
				v.Material = "Plastic"
				v.Reflectance = 0
			elseif v:IsA("Decal") or v:IsA("Texture") and decalsyeeted then
				v.Transparency = 1
			elseif v:IsA("ParticleEmitter") or v:IsA("Trail") then
				v.Lifetime = NumberRange.new(0)
			elseif v:IsA("Explosion") then
				v.BlastPressure = 1
				v.BlastRadius = 1
			elseif v:IsA("Fire") or v:IsA("SpotLight") or v:IsA("Smoke") or v:IsA("Sparkles") then
				v.Enabled = false
			elseif v:IsA("MeshPart") then
				v.Material = "Plastic"
				v.Reflectance = 0
				v.TextureID = 10385902758728957
			end
		end
		for i, e in pairs(l:GetChildren()) do
			if e:IsA("BlurEffect") or e:IsA("SunRaysEffect") or e:IsA("ColorCorrectionEffect") or e:IsA("BloomEffect") or e:IsA("DepthOfFieldEffect") then
				e.Enabled = false
			end
		end
	end)
	----------------------------------------------------------------------------------------------------------------------------
	local RaidsTab = page7:NewSecction("Raids")
	RaidsTab:Label("Use In Raid Only",true)
	Distance = 500
	RaidsTab:Toggle("Kill Arua",killaura,function(value)
		if NewWorld or ThreeWorld then
			RaidsArua = value
		elseif OldWorld then
			VLib:Notification("Use In New World")
		end
	end)
	RaidsTab:Toggle("Auto Next Island",autonextisland,function(value)
		if NewWorld or ThreeWorld then
			NextIsland = value
		elseif OldWorld then
			VLib:Notification("Use In New World")
		end
	end)
	RaidsTab:Toggle("Auto Awakener",autoAwakener,function(value)
		if NewWorld or ThreeWorld then
			Awakener = value
		elseif OldWorld then
			VLib:Notification("Use In New World")
		end
	end)
	spawn(function()
		while wait() do
			if Awakener and (game:GetService("Workspace")["_WorldOrigin"].Locations["l'Ã‰glise de ProphÃ©tie"].Position - game.Players.localPlayer.Character.HumanoidRootPart.Position).magnitude <= 100 then
				local string_1 = "Awakener";
				local string_2 = "Check";
				local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
				Target:InvokeServer(string_1, string_2);
				
				local string_1 = "Awakener";
				local string_2 = "Awaken";
				local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
				Target:InvokeServer(string_1, string_2);
			end
		end
	end)
	RaidsTab:Button("Dungeon",function()
		if NewWorld then
			if StatsBypassTP == "Bypassed" and UseTP then
				game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-6438.73535, 250.645355, -4501.50684)
			else
				TP(CFrame.new(-6438.73535, 250.645355, -4501.50684))
			end
		elseif ThreeWorld then
			if StatsBypassTP == "Bypassed" and UseTP then
				game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-5013.64941, 314.843842, -2817.8042)
			else
				TP(CFrame.new(-5013.64941, 314.843842, -2817.8042))
			end
		elseif OldWorld then
			VLib:Notification("Use In New World","Button")
		end
	end)
	RaidsTab:Button("Awakening Room",function()
		if NewWorld then
			if StatsBypassTP == "Bypassed" and UseTP then
				game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace")["_WorldOrigin"].Locations["l'Ã‰glise de ProphÃ©tie"].CFrame
			else
				TP(CFrame.new(266.227783, 1.39509034, 1857.00732))
			end
		elseif ThreeWorld then
			if StatsBypassTP == "Bypassed" and UseTP then
				game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace")["_WorldOrigin"].Locations["l'Ã‰glise de ProphÃ©tie"].CFrame
			else
				TP(CFrame.new(266.227783, 1.39509034, 1857.00732))
			end
		elseif OldWorld then
			VLib:Notification("Use In New World","Button")
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
	RaidsTab:Line()
	RaidsTab:Label("Auto Raids")
	RaidsSelected = selectraids or ""
	Raidslist = {}
	RaidsModule = require(game.ReplicatedStorage.Raids)
	for i,v in pairs(RaidsModule.raids) do
		table.insert(Raidslist,v)
	end
	for i,v in pairs(RaidsModule.advancedRaids) do
		table.insert(Raidslist,v)
	end
	RaidsTab:Dropdown("Select Raids",Raidslist,0,function(A)
		RaidsSelected = A
	end)
	RaidsTab:Toggle("Auto Raids",autoraids,function(A)
		if OldWorld then
			VLib:Notification("Use In New World & Thire World")
		else
			if RaidsSelected == "" and A then
				VLib:Notification("Select Auto Raids First")
			else
				AutoRaids = A
			end
		end
	end)
	InRaids = true
	spawn(function()
		while wait() do
			if NextIsland then
				if StatsBypassTP == "Bypassed" and UseTP and ( game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 5") or game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 4") or game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 3") or game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 2") or game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1") ) then
					if game.Players.LocalPlayer.PlayerGui.Main.Timer.Visible == false then
					elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 5") then
						game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 5").CFrame = CFrame.new(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 5").CFrame.x,60,game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 5").CFrame.z)
						game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 5").CFrame
					elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 4") then
						game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 4").CFrame = CFrame.new(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 4").CFrame.x,60,game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 4").CFrame.z)
						game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 4").CFrame
					elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 3") then
						game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 3").CFrame = CFrame.new(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 3").CFrame.x,60,game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 3").CFrame.z)
						game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 3").CFrame
					elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 2") then
						game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 2").CFrame = CFrame.new(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 2").CFrame.x,60,game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 2").CFrame.z)
						game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 2").CFrame
					elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1") then
						game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1").CFrame = CFrame.new(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1").CFrame.x,60,game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1").CFrame.z)
						game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1").CFrame
					end
				else
					if game.Players.LocalPlayer.PlayerGui.Main.Timer.Visible == false then
					elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 5") then
						game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 5").CFrame = CFrame.new(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 5").CFrame.x,60,game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 5").CFrame.z)
						if (game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 5").Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 350 then
							Farmtween = toTarget(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 5").Position,game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 5").CFrame)
						elseif (game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 5").Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 350 then
							if Farmtween then
								Farmtween:Stop()
							end
							game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 5").CFrame
						end
					elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 4") then
						game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 4").CFrame = CFrame.new(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 4").CFrame.x,60,game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 4").CFrame.z)
						if (game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 4").Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 350 then
							Farmtween = toTarget(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 4").Position,game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 4").CFrame)
						elseif (game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 4").Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 350 then
							if Farmtween then
								Farmtween:Stop()
							end
							game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 4").CFrame
						end
					elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 3") then
						game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 3").CFrame = CFrame.new(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 3").CFrame.x,60,game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 3").CFrame.z)
						
						if (game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 3").Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 350 then
							Farmtween = toTarget(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 3").Position,game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 3").CFrame)
						elseif (game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 3").Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 350 then
							if Farmtween then
								Farmtween:Stop()
							end
							game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 3").CFrame
						end
					elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 2") then
						game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 2").CFrame = CFrame.new(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 2").CFrame.x,60,game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 2").CFrame.z)
						
						if (game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 2").Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 350 then
							Farmtween = toTarget(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 2").Position,game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 2").CFrame)
						elseif (game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 2").Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 350 then
							if Farmtween then
								Farmtween:Stop()
							end
							game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 2").CFrame
						end
					elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1") then
						game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1").CFrame = CFrame.new(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1").CFrame.x,60,game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1").CFrame.z)
						if (game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1").Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 350 then
							Farmtween = toTarget(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1").Position,game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1").CFrame)
						elseif (game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1").Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 350 then
							if Farmtween then
								Farmtween:Stop()
							end
							game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1").CFrame
						end
					end
				end
			end
			if RaidsArua then
				for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
					if RaidsArua and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and (v.HumanoidRootPart.Position-game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 400 then
						pcall(function()
							repeat wait()
								v.Humanoid.Health = 0
							until not RaidsArua or v.Humanoid.Health <= 0 or not v.Parent
						end)
					end
				end
			end
			if AutoRaids then
				if game.Players.LocalPlayer.Backpack:FindFirstChild("Special Microchip") or game.Players.LocalPlayer.Character:FindFirstChild("Special Microchip") or game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 5") or game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 4") or game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 3") or game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 2") or game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1") then
					if game.Players.LocalPlayer.Backpack:FindFirstChild("Special Microchip") or game.Players.LocalPlayer.Character:FindFirstChild("Special Microchip") and game.Players.LocalPlayer.PlayerGui.Main.Timer.Visible == false then
						
						if NewWorld then
							fireclickdetector(Workspace.Map.CircleIsland.RaidSummon2.Button.Main.ClickDetector)
						elseif ThreeWorld then
							fireclickdetector(Workspace.Map["Boat Castle"].RaidSummon2.Button.Main.ClickDetector)
						end
						wait(16)
					elseif game.Players.LocalPlayer.PlayerGui.Main.Timer.Visible == true then
						Useraids = true
						pcall(function()
							repeat wait()
								if StatsBypassTP == "Bypassed" and UseTP and ( game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 5") or game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 4") or game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 3") or game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 2") or game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1") ) then
									if game.Players.LocalPlayer.PlayerGui.Main.Timer.Visible == false then
									elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 5") then
										game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 5").CFrame = CFrame.new(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 5").CFrame.x,60,game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 5").CFrame.z)
										game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 5").CFrame
									elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 4") then
										game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 4").CFrame = CFrame.new(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 4").CFrame.x,60,game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 4").CFrame.z)
										game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 4").CFrame
									elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 3") then
										game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 3").CFrame = CFrame.new(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 3").CFrame.x,60,game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 3").CFrame.z)
										game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 3").CFrame
									elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 2") then
										game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 2").CFrame = CFrame.new(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 2").CFrame.x,60,game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 2").CFrame.z)
										game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 2").CFrame
									elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1") then
										game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1").CFrame = CFrame.new(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1").CFrame.x,60,game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1").CFrame.z)
										game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1").CFrame
									end
								else
									if game.Players.LocalPlayer.PlayerGui.Main.Timer.Visible == false then
									elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 5") then
										game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 5").CFrame = CFrame.new(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 5").CFrame.x,60,game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 5").CFrame.z)
										if (game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 5").Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 350 then
											Farmtween = toTarget(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 5").Position,game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 5").CFrame)
										elseif (game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 5").Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 350 then
											if Farmtween then
												Farmtween:Stop()
											end
											game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 5").CFrame
										end
									elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 4") then
										game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 4").CFrame = CFrame.new(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 4").CFrame.x,60,game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 4").CFrame.z)
										if (game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 4").Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 350 then
											Farmtween = toTarget(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 4").Position,game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 4").CFrame)
										elseif (game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 4").Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 350 then
											if Farmtween then
												Farmtween:Stop()
											end
											game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 4").CFrame
										end
									elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 3") then
										game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 3").CFrame = CFrame.new(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 3").CFrame.x,60,game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 3").CFrame.z)
										
										if (game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 3").Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 350 then
											Farmtween = toTarget(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 3").Position,game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 3").CFrame)
										elseif (game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 3").Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 350 then
											if Farmtween then
												Farmtween:Stop()
											end
											game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 3").CFrame
										end
									elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 2") then
										game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 2").CFrame = CFrame.new(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 2").CFrame.x,60,game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 2").CFrame.z)
										
										if (game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 2").Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 350 then
											Farmtween = toTarget(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 2").Position,game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 2").CFrame)
										elseif (game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 2").Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 350 then
											if Farmtween then
												Farmtween:Stop()
											end
											game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 2").CFrame
										end
									elseif game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1") then
										game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1").CFrame = CFrame.new(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1").CFrame.x,60,game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1").CFrame.z)
										if (game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1").Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude > 350 then
											Farmtween = toTarget(game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1").Position,game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1").CFrame)
										elseif (game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1").Position - game.Players.LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 350 then
											if Farmtween then
												Farmtween:Stop()
											end
											game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1").CFrame
										end
									end
								end
								for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
									if AutoRaids and v:FindFirstChild("Humanoid") and v:FindFirstChild("HumanoidRootPart") and (v.HumanoidRootPart.Position-game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 400 then
										pcall(function()
											repeat wait()
												v.HumanoidRootPart.Transparency = 0.75
												v.Humanoid.Health = 0
											until not AutoRaids or v.Humanoid.Health <= 0 or not v.Parent
										end)
									end
								end
							until AutoRaids == false or not game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 5") or not game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 4") or not game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 3") or not game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 2") or not game:GetService("Workspace")["_WorldOrigin"].Locations:FindFirstChild("Island 1") or game.Players.LocalPlayer.PlayerGui.Main.Timer.Visible == false
						end)
					end
				else
					Useraids = false
					local args = {
						[1] = "RaidsNpc",
						[2] = "Select",
						[3] = RaidsSelected
					}
					game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
				end
			end
		end
	end)
	----------------------------------------------------------------------------------------------------------------------------
	local ShopTab = page8:NewSecction("Shop")
	if game:GetService("ReplicatedStorage").Remotes["CommF_"]:InvokeServer("Candies","Check") then
		ShopTab:Label("Candy",true)
		local string_1 = "Candies";
		local string_2 = "Check";
		local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
		BonePoint = ShopTab:Label("You Have ".. Target:InvokeServer(string_1, string_2) .." Candy",true)
		spawn(function()
			while wait() do
				BonePoint:Refresh("You Have ".. Target:InvokeServer(string_1, string_2) .." Candy")
			end
		end)
		local v237, v238 = game.ReplicatedStorage.Remotes.CommF_:InvokeServer("Candies", "Check");
		for i,v in pairs(v238[1]) do
			ShopTab:Button(v[1] .. " [ ".. v[2] .. " Candy ]",function()
				local args = {
					[1] = "Candies",
					[2] = "Buy",
					[3] = 1,
					[4] = i
				}
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
			end)
		end
		for i,v in pairs(v238[2]) do
			ShopTab:Button(v[1] .. " [ ".. v[2] .. " Candy ]",function()
				local args = {
					[1] = "Candies",
					[2] = "Buy",
					[3] = 2,
					[4] = i
				}
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
			end)
		end
		for i,v in pairs(v238[3]) do
			ShopTab:Button(v[1] .. " [ ".. v[2] .. " Candy ]",function()
				local args = {
					[1] = "Candies",
					[2] = "Buy",
					[3] = 3,
					[4] = i
				}
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
			end)
		end
		ShopTab:Line()
	end
	ShopTab:Label("Abilities",true)
	ShopTab:Button("Skyjump [ $10,000 Beli ]",function()
		local args = {
			[1] = "BuyHaki",
			[2] = "Geppo"
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	end)
	ShopTab:Button("Buso Haki [ $25,000 Beli ]",function()
		local args = {
			[1] = "BuyHaki",
			[2] = "Buso"
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	end)
	ShopTab:Button("Observation haki [ $750,000 Beli ]",function()
		local args = {
			[1] = "KenTalk",
			[2] = "Buy"
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	end)
	ShopTab:Button("Soru [ $100,000 Beli ]",function()
		local args = {
			[1] = "BuyHaki",
			[2] = "Soru"
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	end)
	ShopTab:Button("Buy Random Devil Fruit",function()
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Cousin","Buy")
	end)
	ShopTab:Toggle("Auto Random Devil Fruit",false,function(v)
		DevilAutoBuy = v
	end)
	spawn(function()
		while wait() do 
			if DevilAutoBuy then
				game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Cousin","Buy")
			end
		end
	end)
	ShopTab:Line()
	ShopTab:Label("Fighting Style",true)
	ShopTab:Button("Black Leg",function()
		local args = {
			[1] = "BuyBlackLeg"
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	end)
	ShopTab:Button("Electro",function()
		local args = {
			[1] = "BuyElectro"
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	end)
	ShopTab:Button("Fishman Karate",function()
		local args = {
			[1] = "BuyFishmanKarate"
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	end)
	ShopTab:Button("Dragon Claw",function()
		local args = {
			[1] = "BlackbeardReward",
			[2] = "DragonClaw",
			[3] = "2"
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	end)
	ShopTab:Button("Superhuman",function()
		local args = {
			[1] = "BuySuperhuman"
		}
		
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	end)
	ShopTab:Button("Death Step",function()
		local args = {
			[1] = "BuyDeathStep"
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	end)
	ShopTab:Button("Sharkman Karate",function()
		local args = {
			[1] = "BuySharkmanKarate",
			[2] = true
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
		local args = {
			[1] = "BuySharkmanKarate"
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	end)
	ShopTab:Button("Electric Claw",function()
		local string_1 = "BuyElectricClaw";
		local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
		Target:InvokeServer(string_1);
	end)
	ShopTab:Button("Dragon Talon",function()
		local string_1 = "BuyDragonTalon";
		local bool_1 = true;
		local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
		Target:InvokeServer(string_1, bool_1);
		local string_1 = "BuyDragonTalon";
		local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
		Target:InvokeServer(string_1);
	end)
	ShopTab:Line()
	ShopTab:Label("Sword",true)
	ShopTab:Button("Katana [ $1,000 Beli ]",function()
		local args = {
			[1] = "BuyItem",
			[2] = "Katana"
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	end)
	ShopTab:Button("Cutlass [ $1,000 Beli ]",function()
		local args = {
			[1] = "BuyItem",
			[2] = "Cutlass"
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	end)  
	ShopTab:Button("Dual Katana [ $12,000 Beli ]",function()
		local args = {
			[1] = "BuyItem",
			[2] = "Dual Katana"
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	end)
	ShopTab:Button("Iron Mace [ $25,000 Beli ]",function()
		local args = {
			[1] = "BuyItem",
			[2] = "Iron Mace"
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	end)
	ShopTab:Button("Triple Katana [ $60,000 Beli ]",function()
		local args = {
			[1] = "BuyItem",
			[2] = "Triple Katana"
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	end)
	ShopTab:Button("Pipe [ $100,000 Beli ]",function()
		local args = {
			[1] = "BuyItem",
			[2] = "Pipe"
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	end)
	ShopTab:Button("Soul Cane [ $750,000 Beli ]",function()
		local args = {
			[1] = "BuyItem",
			[2] = "Soul Cane"
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	end)
	ShopTab:Button("Dual-Headed Blade [ $400,000 Beli ]",function()
		local args = {
			[1] = "BuyItem",
			[2] = "Dual-Headed Blade"
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	end)
	ShopTab:Button("Bisento [ $1,200,000 Beli ]",function()
		local args = {
			[1] = "BuyItem",
			[2] = "Bisento"
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	end)
	ShopTab:Button("Pole v.2 [ 5,000 Fragments )",function()
		game.ReplicatedStorage.Remotes.CommF_:InvokeServer("ThunderGodTalk")
	end)
	ShopTab:Line()
	ShopTab:Label("Gun",true)
	ShopTab:Button("Slingshot [ $5,000 Beli ]",function()
		local args = {
			[1] = "BuyItem",
			[2] = "Slingshot"
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	end)
	ShopTab:Button("Musket [ $8,000 Beli ]",function()
		local args = {
			[1] = "BuyItem",
			[2] = "Musket"
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	end)
	ShopTab:Button("Flintlock [ $10,500 Beli ]",function()
		local args = {
			[1] = "BuyItem",
			[2] = "Flintlock"
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	end)
	ShopTab:Button("Refined Slingshot [ $30,000 Beli ]",function()
		local args = {
			[1] = "BuyItem",
			[2] = "Refined Slingshot"
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	end)
	ShopTab:Button("Refined Flintlock [ $65,000 Beli ]",function()
		local args = {
			[1] = "BuyItem",
			[2] = "Refined Flintlock"
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	end)
	ShopTab:Button("Kabucha [ 1,500 Fragments)",function()
		game.ReplicatedStorage.Remotes.CommF_:InvokeServer("BlackbeardReward", "Slingshot", "2")
	end)
	ShopTab:Line()
	ShopTab:Label("Accessories",true)
	ShopTab:Button("Black Cape [ $50,000 Beli ]",function()
		local args = {
			[1] = "BuyItem",
			[2] = "Black Cape"
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	end)
	ShopTab:Button("Swordsman Hat [ 150k Beli ]",function()
		local args = {
			[1] = "BuyItem",
			[2] = "Swordsman Hat"
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	end)
	ShopTab:Button("Tomoe Ring [ $500k Beli ]",function()
		local args = {
			[1] = "BuyItem",
			[2] = "Tomoe Ring"
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	end)
	ShopTab:Line()
	ShopTab:Label("Race & etc.",true)
	ShopTab:Button("Race Ghoul",function()
		local args = {
			[1] = "Ectoplasm",
			[2] = "BuyCheck",
			[3] = 4
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
		local args = {
			[1] = "Ectoplasm",
			[2] = "Change",
			[3] = 4
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	end)
	ShopTab:Button("Race Cyborg",function()
		local args = {
			[1] = "CyborgTrainer",
			[2] = "Buy"
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	end)
	ShopTab:Button("Random Race (Use 3K Fragments)",function()
		local args = {
			[1] = "BlackbeardReward",
			[2] = "Reroll",
			[3] = "2"
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	end)
	ShopTab:Button("Reset Stats (Use 2.5K Fragments)",function()
		local args = {
			[1] = "BlackbeardReward",
			[2] = "Refund",
			[3] = "2"
		}
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer(unpack(args))
	end)
	
	----------------------------------------------------------------------------------------------------------------------------
	local Devil_Fruit_Sniper_Tab = page9:NewSecction("Devil Fruit Sniper")
	local Remote_GetFruits = game.ReplicatedStorage:FindFirstChild("Remotes").CommF_:InvokeServer("GetFruits");
	Table_DevilFruitSniper = {}
	ShopDevilSell = {}
	for i,v in next,Remote_GetFruits do
		table.insert(Table_DevilFruitSniper,v.Name)
		if v.OnSale then 
			table.insert(ShopDevilSell,v.Name)
		end
	end
	Devil_Fruit_Sniper_Tab:Label("Devil Fruit Sniper")
	SelectDevil = ""
	Devil_Fruit_Sniper_Tab:Dropdown("Select Devil Fruit Sniper",Table_DevilFruitSniper,0,function(a)
		SelectDevil = a
	end)
	Devil_Fruit_Sniper_Tab:Toggle("Buy Devil Fruit Sinper",false,function(value)
		if SelectDevil == "" and value then
			VLib:Notification("Select Devil Fruit")
		else
			BuyFruitSinper = value
		end	
	end)
	Devil_Fruit_Sniper_Tab:Toggle("Bring Devil Fruit",bringdevilfruit,function(value)
		TeleportDF = value
	end)
	spawn(function()
		while wait() do
			if BuyFruitSinper then
				local string_1 = "PurchaseRawFruit";
				local string_2 = SelectDevil;
				local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
				Target:InvokeServer(string_1, string_2);
			end   
			if TeleportDF then
				for i,v in pairs(game:GetService("Workspace"):GetChildren()) do
					if v:IsA("Tool") and string.find(v.Name,"Fruit") then wait(5)
						firetouchinterest(game.Players.LocalPlayer.Character.HumanoidRootPart,v.Handle,0)    
					end
				end
			end                              
		end
	end)
	Devil_Fruit_Sniper_Tab:Line()
	Devil_Fruit_Sniper_Tab:Label("Shop Devil Sell")
	SelectedShopDevilSell = ""
	local RefreshDevilFruitShop = Devil_Fruit_Sniper_Tab:Dropdown("Shop Devil Sell Now",ShopDevilSell,0,function(a)
		SelectedShopDevilSell = a
	end)
	Devil_Fruit_Sniper_Tab:Button("Buy Devil Fruit",function()
		local string_1 = "PurchaseRawFruit";
		local string_2 = SelectedShopDevilSell;
		local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
		Target:InvokeServer(string_1, string_2);
	end)
	
	local function RemoveSpaces(str)
		return str:gsub(" Fruit", "")
	end
	Devil_Fruit_Sniper_Tab:Toggle("Auto Store Fruits",false,function(a)
		AutoStoreFruits = a
		if AutoStoreFruits then
			for i,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
				if string.find(v.Name,"Fruit") then
					local FruitName = RemoveSpaces(v.Name)
					if v.Name == "Bird: Falcon Fruit" then
						NameFruit = "Bird-Bird: Falcon"
					elseif v.Name == "Bird: Phoenix Fruit" then
						NameFruit = "Bird-Bird: Phoenix"
					elseif v.Name == "Human: Buddha Fruit" then
						NameFruit = "Human-Human: Buddha"
					else
						NameFruit = FruitName.."-"..FruitName
					end
				end
			end
			
			local string_1 = "StoreFruit";
			local string_2 = NameFruit;
			local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
			Target:InvokeServer(string_1, string_2);
		end
	end)
	spawn(function()
		while wait() do
			if AutoStoreFruits then wait()
				for i,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
					if string.find(v.Name,"Fruit") then
						local FruitName = RemoveSpaces(v.Name)
						if v.Name == "Bird: Falcon Fruit" then
							NameFruit = "Bird-Bird: Falcon"
						elseif v.Name == "Bird: Phoenix Fruit" then
							NameFruit = "Bird-Bird: Phoenix"
						elseif v.Name == "Human: Buddha Fruit" then
							NameFruit = "Human-Human: Buddha"
						else
							NameFruit = FruitName.."-"..FruitName
						end
	
						local string_1 = "getInventoryFruits";
						local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
						for i1,v1 in pairs(Target:InvokeServer(string_1)) do
							if v1.Name == NameFruit then
								HaveFruitInStore = true
							end
						end
						if not Have then
							local string_1 = "StoreFruit";
							local string_2 = NameFruit;
							local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
							Target:InvokeServer(string_1, string_2);
						end
						HaveFruitInStore = false
					end
				end
			end
		end
	end)
	Devil_Fruit_Sniper_Tab:Line()
	Devil_Fruit_Sniper_Tab:Label("List Store Fruits")
	
	local string_1 = "getInventoryFruits";
	local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
	TabelDevilFruitStore = {}
	for i,v in pairs(Target:InvokeServer(string_1)) do
		for i1,v1 in pairs(v) do
			if i1 == "Name" then 
				table.insert(TabelDevilFruitStore,v1)
			end
		end
	end
	
	SelectedShopDevilStore = ""
	local RefreshDevilFruitStore = Devil_Fruit_Sniper_Tab:Dropdown("List Store Fruits",TabelDevilFruitStore,0,function(a)
		SelectedShopDevilStore = a
	end)
	Devil_Fruit_Sniper_Tab:Button("Load Store Devil Fruits Sele",function()
		local string_1 = "LoadFruit";
		local string_2 = SelectedShopDevilStore;
		local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
		Target:InvokeServer(string_1, string_2);
	end)
										
	spawn(function()
		while wait() do
			local string_1 = "getInventoryFruits";
			local Target = game:GetService("ReplicatedStorage").Remotes["CommF_"];
			TabelDevilFruitStore = {}
			ShopDevilSell = {}
			for i,v in next,Remote_GetFruits do
				if v.OnSale then 
					table.insert(ShopDevilSell,v.Name)
				end
			end
			for i,v in pairs(Target:InvokeServer(string_1)) do
				for i1,v1 in pairs(v) do
					if i1 == "Name" then 
						table.insert(TabelDevilFruitStore,v1)
					end
				end
			end
			wait(20)
			RefreshDevilFruitShop:Refresh(ShopDevilSell,0)
			RefreshDevilFruitStore:Refresh(TabelDevilFruitStore,0)
		end
	end)
	
	----------------------------------------------------------------------------------------------------------------------------
	local SettingTab = page10:NewSecction("Setting")
	SettingTab:Button("Rejoin",function()
		local ts = game:GetService("TeleportService")
		local p = game:GetService("Players").LocalPlayer
		ts:Teleport(game.PlaceId, p)
	end)
	local function HttpGet(url)
		return game:GetService("HttpService"):JSONDecode(htgetf(url))
	end
	SettingTab:Button("Server Hop",function()
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
	end)
	Server_Hop_LessPeople = SettingTab:Button("Server Hop (Less People)",function()
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
				if tonumber(2) > tonumber(v.playing) then
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
						wait(1)
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
	end)
	-- Server_Hop_LessPeople:Lock()
	SettingTab:Line()
	SettingTab:Button("Join discord",function()
		local request = request or http_request or (syn and syn.request)
		if not request then return end
		local start = 6463
		local invCode = 'QgQdx7uCUT'
		for i = start-10, start+1 do
			spawn(function()
				pcall(function()
					request({Url = "http://127.0.0.1:"..tostring(i).."/rpc?v=1",Method = "POST",Headers = {["Content-Type"] = "application/json",["Origin"] = "https://discord.com"},Body = game:GetService("HttpService"):JSONEncode({["cmd"] = "INVITE_BROWSER",["nonce"] = game:GetService("HttpService"):GenerateGUID(false),["args"] = {["invite"] = {["code"] = invCode,},["code"] = invCode}})})
				end)
			end)
		end
	end)
	SettingTab:DestroyGui()
	
	local SecretTab = Main:Tab("Secret PVP",true)
	
	SecretTab:Toggle("Aim Bot Skill And Gun Fov Fully",false,function(a)
		AimBotFullFunction = a
	end)
	
	SecretTab:Toggle("Show Fov",false,function(a)
		ShowFov = a
	end)
	
	_G.FOVSize = 200
	
	SecretTab:Slider("Fov Size",1,700,_G.FOVSize,nil,function(v)
		_G.FOVSize = v
	end)
	
	local FOVCircle = Drawing.new("Circle")
	FOVCircle.Thickness = 2
	FOVCircle.NumSides = 460
	FOVCircle.Filled = false
	FOVCircle.Transparency = 0.5
	FOVCircle.Radius = 200
	FOVCircle.Color = Color3.fromRGB(255, 0, 0)
	
	game:GetService("RunService").Stepped:Connect(function()
		FOVCircle.Radius = _G.FOVSize
		FOVCircle.Thickness = 1
		FOVCircle.NumSides = 11
		FOVCircle.Position = game:GetService('UserInputService'):GetMouseLocation()
		if ShowFov then
			FOVCircle.Visible = true
		else
			FOVCircle.Visible = false
		end
	end)
	
	local lp = game:GetService('Players').LocalPlayer
	local mouse = lp:GetMouse()
	spawn(function()
		while wait() do
			if AimBotFullFunction then
				pcall(function()
					local MaxDist, Closest = math.huge
					for i,v in pairs(game:GetService("Players"):GetChildren()) do 
						local Head = v.Character:FindFirstChild("HumanoidRootPart")
						local Pos, Vis = game.Workspace.CurrentCamera.WorldToScreenPoint(game.Workspace.CurrentCamera, Head.Position)
						local MousePos, TheirPos = Vector2.new(mouse.X, mouse.Y), Vector2.new(Pos.X, Pos.Y)
						local Dist = (TheirPos - MousePos).Magnitude
						if Dist < MaxDist and Dist <= _G.FOVSize and v.Name ~= game.Players.LocalPlayer.Name then
							MaxDist = Dist
							_G.CharacterAimBot = v
						end
					end
				end)
			end
		end
	end)
	
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
						if AimBotFullFunction then
							args[2] = _G.CharacterAimBot.Character.HumanoidRootPart.Position
							return old(unpack(args))
						end
					end
				end
			end
			return old(...)
		end)
	end)
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
		mouse.Button1Down:Connect(function()
			if SelectToolWeaponGun ~= nil then
				if AimBotFullFunction and game.Players.LocalPlayer.Character:FindFirstChild(SelectToolWeaponGun) and game:GetService("Players"):FindFirstChild(_G.CharacterAimBot.Name) then
					tool = game:GetService("Players").LocalPlayer.Character[SelectToolWeaponGun]
					v17 = workspace:FindPartOnRayWithIgnoreList(Ray.new(tool.Handle.CFrame.p, (game:GetService("Players"):FindFirstChild(_G.CharacterAimBot.Name).Character.HumanoidRootPart.Position - tool.Handle.CFrame.p).unit * 100), { game.Players.LocalPlayer.Character, workspace._WorldOrigin });
					game:GetService("Players").LocalPlayer.Character[SelectToolWeaponGun].RemoteFunctionShoot:InvokeServer(game:GetService("Players"):FindFirstChild(_G.CharacterAimBot.Name).Character.HumanoidRootPart.Position, (require(game.ReplicatedStorage.Util).Other.hrpFromPart(v17)));
				end 
			end
		end)
	end)
    return library
end


