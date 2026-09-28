--// ============================================================
--// LOADER UNIVERSAL — Batata Hub (Hub + AIM + ESP)
--// Junta tudo em 1 loadstring só (evita bloqueio de loadstring aninhado)
--// ============================================================

local HttpService = game:GetService("HttpService")
local StarterGui = game:GetService("StarterGui")

local URLs = {
	Hub = "https://raw.githubusercontent.com/n12217915-source/Batata-Hub/refs/heads/main/README.md",
	AIM = "https://raw.githubusercontent.com/n12217915-source/BATATA-CENTRAL-1/refs/heads/main/README.md",
	ESP = "https://raw.githubusercontent.com/n12217915-source/BATATA-CENTRAL2/refs/heads/main/README.md",
}

--// Notificação rápida
local function quickNotify(text, duration)
	pcall(function()
		StarterGui:SetCore("SendNotification", {
			Title = "Batata Hub",
			Text = text,
			Duration = duration or 3,
		})
	end)
end

--// Baixa um script (com cache-buster pra sempre pegar versão nova)
local function download(url)
	local ok, src = pcall(function()
		return game:HttpGet(url .. "?t=" .. tick(), true)
	end)
	if ok and src and #src > 10 then
		return src
	end
	return nil
end

--// Início
quickNotify("📦 Baixando scripts...", 3)

local hubSrc = download(URLs.Hub)
if not hubSrc then
	quickNotify("❌ Falha ao baixar Hub", 5)
	return
end

local aimSrc = download(URLs.AIM)
if not aimSrc then
	warn("[Loader] AIM não encontrado, continuando só com Hub + ESP")
	aimSrc = ""
end

local espSrc = download(URLs.ESP)
if not espSrc then
	warn("[Loader] ESP não encontrado, continuando só com Hub + AIM")
	espSrc = ""
end

--// Junta tudo numa string só
-- Ordem importa: Hub primeiro (cria a API), depois os módulos (usam a API)
local combined = hubSrc .. "\n\n" .. aimSrc .. "\n\n" .. espSrc

--// Executa UMA VEZ (evita bloqueio de loadstring aninhado)
quickNotify("⚡ Executando 3 scripts...", 3)

local chunk = loadstring(combined)
if not chunk then
	quickNotify("❌ Erro ao compilar scripts", 5)
	return
end

local runOk, err = pcall(chunk)
if not runOk then
	quickNotify("❌ Erro: " .. tostring(err):sub(1, 40), 5)
	warn("[Loader] Erro em runtime: " .. tostring(err))
	return
end

quickNotify("✅ Tudo carregado!", 3)
print("[Loader] Hub + AIM + ESP carregados com sucesso!")
