--// ============================================================
--// LOADER UNIVERSAL — Batata Hub + AIM
--// ============================================================

local HttpService = game:GetService("HttpService")
local ReplicatedStorage = game:GetService("ReplicatedStorage")

local URLs = {
	Interface = "https://raw.githubusercontent.com/n12217915-source/Batata-Hub/refs/heads/main/README.md",
	AIM = "https://raw.githubusercontent.com/n12217915-source/BATATA-CENTRAL-1/refs/heads/main/README.md",
}

local function notify(title, text)
	pcall(function()
		game:GetService("StarterGui"):SetCore("SendNotification", {
			Title = title,
			Text = text,
			Duration = 3,
		})
	end)
end

local function loadURL(url)
	local ok, source = pcall(function()
		return game:HttpGet(url, true)
	end)
	if not ok or not source or #source < 10 then return false end

	local chunk = loadstring(source)
	if not chunk then return false end

	local runOk = pcall(chunk)
	return runOk
end

-- 1. Interface
notify("Batata Hub", "📦 Carregando interface...")
local ok1 = loadURL(URLs.Interface)

if not ok1 then
	notify("Batata Hub", "❌ Falha ao carregar interface")
	return
end

notify("Batata Hub", "✅ Interface carregada")

-- 2. Espera a API existir
local tries = 0
while not ReplicatedStorage:FindFirstChild("BatataHub_RegisterTab") do
	tries = tries + 1
	if tries > 100 then
		notify("Batata Hub", "❌ Timeout: API não criada")
		return
	end
	task.wait(0.1)
end

task.wait(0.5) -- deixa o BindableFunction estabilizar

-- 3. AIM
notify("Batata Hub", "🔧 Carregando módulo AIM...")
local ok2 = loadURL(URLs.AIM)

if ok2 then
	notify("Batata Hub", "✅ Módulo carregado!")
else
	notify("Batata Hub", "❌ Falha ao carregar módulo")
end
