game:GetService("StarterGui"):SetCore("SendNotification", {
    Title = "Project Hook";
    Text = "Link has changed. \n\nTo find the new one join\n discord.gg/A6N3nJeEsR\n";
    Duration = 15;
})

if setclipboard then setclipboard('discord.gg/A6N3nJeEsR') end

if syn then
    local Inv, ServerInfo, ServerName = syn.request({Url = "https://projecthook.xyz/requirements/discord.txt"; Method = "GET"}).Body, nil, ""

    ServerInfo = syn.request({
        Url = 'https://discord.com/api/v6/invite/'..Inv,
        Method = 'GET'
    })

    if ServerInfo.Success then ServerInfo = game:GetService("HttpService"):JSONDecode(ServerInfo.Body) else return end

    syn.request({
        Url = 'http://127.0.0.1:6463/rpc?v=1',
        Method = 'POST',
        Headers = {
            ['Content-Type'] = 'application/json',
            ['origin'] = 'https://ptb.discord.com',
        },
        Body = game:GetService("HttpService"):JSONEncode({
            ['args'] = {
                ['code'] = Inv,
            },
            ['cmd'] = 'INVITE_BROWSER',
            ['nonce'] = tostring(math.random(11111,99999))
        })
    })
end
