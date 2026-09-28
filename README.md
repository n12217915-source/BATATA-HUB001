local ok, err = pcall(function()
	loadstring(game:HttpGet("https://raw.githubusercontent.com/n12217915-source/Batata-Hub/refs/heads/main/README.md"))()
end)

print("Hub resultado:", ok, err)

task.wait(2.5)

local ok2, err2 = pcall(function()
	loadstring(game:HttpGet("https://raw.githubusercontent.com/n12217915-source/BATATA-CENTRAL-1/refs/heads/main/README.md"))()
end)

print("AIM resultado:", ok2, err2)

task.wait(2.5)

local ok3, err3 = pcall(function()
	loadstring(game:HttpGet("https://raw.githubusercontent.com/n12217915-source/BATATA-CENTRAL2/refs/heads/main/README.md"))()
end)

print("ESP resultado:", ok3, err3)
