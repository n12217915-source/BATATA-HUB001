--// ============================================================
--// LOADER UNIVERSAL — Batata Hub
--// Junta interface + módulo em 1 loadstring só
--// ============================================================

local HttpService = game:GetService("HttpService")

local URLs = {
	Interface = "https://raw.githubusercontent.com/n12217915-source/Batata-Hub/refs/heads/main/README.md",
	AIM = "https://raw.githubusercontent.com/n12217915-source/BATATA-CENTRAL-1/refs/heads/main/README.md",
}

-- Baixa os dois
local interfaceSrc = game:HttpGet(URLs.Interface, true)
local aimSrc = game:HttpGet(URLs.AIM, true)

-- Junta tudo numa string só
local combined = interfaceSrc .. "\n\n" .. aimSrc

-- Executa UMA VEZ
loadstring(combined)()
