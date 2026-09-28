--// ============================================================
--// LOADER UNIVERSAL — Batata Hub (Hub + AIM + ESP)
--// ============================================================

local HttpService = game:GetService("HttpService")

local URLs = {
	Interface = "https://raw.githubusercontent.com/n12217915-source/Batata-Hub/refs/heads/main/README.md",
	AIM = "https://raw.githubusercontent.com/n12217915-source/BATATA-CENTRAL-1/refs/heads/main/README.md",
	ESP = "https://raw.githubusercontent.com/n12217915-source/BATATA-CENTRAL2/refs/heads/main/README.md",
}

-- Baixa os três
local interfaceSrc = game:HttpGet(URLs.Interface, true)
local aimSrc = game:HttpGet(URLs.AIM, true)
local espSrc = game:HttpGet(URLs.ESP, true)

-- Junta tudo numa string só (ordem importa!)
local combined = interfaceSrc .. "\n\n" .. aimSrc .. "\n\n" .. espSrc

-- Executa UMA VEZ
loadstring(combined)()
