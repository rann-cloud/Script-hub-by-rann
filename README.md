local Rayfield = loadstring(game:HttpGet('https://sirius.menu/rayfield'))()

-- [ KONFIGURASI LOGIN ]
local OWNER_USER = "rangga"
local OWNER_PASS = "Rangga"
local CORRECT_KEY = "RANN-FREE-KEY" -- Ganti sesuai keinginanmu

local Window = Rayfield:CreateWindow({
   Name = "RANN HUB | Private Edition",
   LoadingTitle = "Menghubungkan ke Server...",
   LoadingSubtitle = "by Rangga",
   ConfigurationSaving = {
      Enabled = true,
      FolderName = "RannHubConfig",
      FileName = "MainHub"
   },
   KeySystem = true, -- Mengaktifkan Key System
   KeySettings = {
      Title = "Key System | RANN HUB",
      Subtitle = "Masukkan Key untuk Melanjutkan",
      Note = "Key bisa didapatkan di Discord/Linkvertise",
      FileName = "RannKey",
      SaveKey = true,
      GrabKeyFromSite = false, 
      Key = {CORRECT_KEY} 
   }
})

-- [ TAB LOGIN OWNER ]
-- Tab ini akan muncul setelah Key benar, sebagai proteksi tambahan
local LoginTab = Window:CreateTab("Owner Login", 4483362458)
local MainTab = nil
local TrollTab = nil

local InputUser = ""
local InputPass = ""

LoginTab:CreateInput({
   Name = "Username",
   PlaceholderText = "Masukkan Username Owner...",
   RemoveTextAfterFocusLost = false,
   Callback = function(Text)
      InputUser = Text
   end,
})

LoginTab:CreateInput({
   Name = "Password",
   PlaceholderText = "Masukkan Password Owner...",
   RemoveTextAfterFocusLost = false,
   Callback = function(Text)
      InputPass = Text
   end,
})

LoginTab:CreateButton({
   Name = "Login sebagai Owner",
   Callback = function()
      if InputUser == OWNER_USER and InputPass == OWNER_PASS then
         Rayfield:Notify({Title = "Login Berhasil", Content = "Selamat Datang, Rangga!", Duration = 5})
         
         -- Munculkan Fitur Utama setelah login berhasil
         if not MainTab then
            MainTab = Window:CreateTab("Main Cheats", 4483362458)
            TrollTab = Window:CreateTab("Troll/Fun", 4483362458)
            
            -- [ ISI FITUR MAIN ]
            MainTab:CreateSlider({
               Name = "Jump Power",
               Range = {50, 500},
               Increment = 10,
               CurrentValue = 50,
               Callback = function(Value)
                  game.Players.LocalPlayer.Character.Humanoid.JumpPower = Value
               end,
            })

            MainTab:CreateButton({
               Name = "Enable Fly (E)",
               Callback = function()
                  loadstring(game:HttpGet("https://raw.githubusercontent.com/XNEOFF/FlyGuiV3/main/FlyGuiV3.lua"))()
               end,
            })

            local TargetPlayer = ""
            MainTab:CreateInput({
               Name = "Nama Player Teleport",
               PlaceholderText = "Nama...",
               Callback = function(Text) TargetPlayer = Text end,
            })

            MainTab:CreateButton({
               Name = "Teleport Sekarang",
               Callback = function()
                  local p1 = game.Players.LocalPlayer.Character.HumanoidRootPart
                  local p2 = game.Players:FindFirstChild(TargetPlayer)
                  if p2 then p1.CFrame = p2.Character.HumanoidRootPart.CFrame end
               end,
            })

            -- [ ISI FITUR TROLL ]
            TrollTab:CreateButton({
               Name = "Jumpscare (Local)",
               Callback = function()
                  local gui = Instance.new("ScreenGui", game.CoreGui)
                  local img = Instance.new("ImageLabel", gui)
                  img.Size = UDim2.new(1, 0, 1, 0)
                  img.Image = "rbxassetid://6030799958"
                  img.BackgroundTransparency = 1
                  local sound = Instance.new("Sound", game.Workspace)
                  sound.SoundId = "rbxassetid://4595235440"
                  sound:Play()
                  task.wait(2)
                  gui:Destroy()
               end,
            })
         end
      else
         Rayfield:Notify({Title = "Login Gagal", Content = "Username atau Password salah!", Duration = 3})
      end
   end,
})
