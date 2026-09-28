--// ============================================================
--// LOADER UNIVERSAL — Batata Hub (Hub + AIM + ESP)
--// Executa cada script com pcall individual e delay
--// ============================================================

local HttpService = game:GetService("HttpService")
local StarterGui = game:GetService("StarterGui")

local URLs = {
	Hub = "https://raw.githubusercontent.com/n12217915-source/Batata-Hub/refs/heads/main/README.md",
	AIM = "https://raw.githubusercontent.com/n12217915-source/BATATA-CENTRAL-1/refs/heads/main/README.md",
	ESP = "https://raw.githubusercontent.com/n12217915-source/BATATA-CENTRAL2/refs/heads/main/README.md",
}

local function notify(text, duration)
	pcall(function()
		StarterGui:SetCore("SendNotification", {
			Title = "Batata Hub",
			Text = text,
			Duration = duration or 3,
		})
	end)
end

local function download(url)
	local ok, src = pcall(function()
		return game:HttpGet(url, true)
	end)
	if ok and src and #src > 10 then
		return src
	end
	return nil
end

--// 1. HUB
notify("📦 Baixando Hub...", 2)
local hubSrc = download(URLs.Hub)

if not hubSrc then
	notify("❌ Falha ao baixar Hub", 5)
	return
end

local hubOk, hubErr = pcall(function()
	loadstring(hubSrc)()
end)

if not hubOk then
	notify("❌ Erro no Hub: " .. tostring(hubErr):sub(1, 40), 5)
	warn("[Loader] Erro no Hub:", hubErr)
	return
end

notify("✅ Hub carregado", 2)
task.wait(2.5)

--// 2. AIM
notify("📦 Baixando AIM...", 2)
local aimSrc = download(URLs.AIM)

if aimSrc then
	local aimOk, aimErr = pcall(function()
		loadstring(aimSrc)()
	end)

	if aimOk then
		notify("✅ AIM carregado", 2)
	else
		warn("[Loader] Erro no AIM:", aimErr)
		notify("⚠️ Falha no AIM", 4)
	end
else
	notify("⚠️ AIM não encontrado", 3)
end

task.wait(2.5)

--// 3. ESP
notify("📦 Baixando ESP...", 2)
local espSrc = download(URLs.ESP)

if espSrc then
	local espOk, espErr = pcall(function()
		loadstring(espSrc)()
	end)

	if espOk then
		notify("✅ ESP carregado", 2)
	else
		warn("[Loader] Erro no ESP:", espErr)
		notify("⚠️ Falha no ESP", 4)
	end
else
	notify("⚠️ ESP não encontrado", 3)
end

task.wait(1)
notify("🎉 Loader concluído!", 3)
