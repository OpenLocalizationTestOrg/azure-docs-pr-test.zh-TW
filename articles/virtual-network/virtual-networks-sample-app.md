---
title: "搭配 Dmz aaaAzure 範例應用程式 |Microsoft 文件"
description: "部署之後建立 DMZ tootest 流量流程案例這個簡單的 web 應用程式"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: 60340ab7-b82b-40e0-bd87-83e41fe4519c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: e0d9cf14590f75b50c64b677efce2c5425b83ec6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sample-application-for-use-with-dmzs"></a>與 DMZ 搭配使用的範例應用程式
[傳回 toohello 安全性界限最佳作法頁面][HOME]

這些 PowerShell 指令碼可以在 hello IIS01 和 AppVM01 伺服器 tooinstall 本機執行和設定會顯示從前端 IIS01 伺服器 hello 的 html 頁面的 hello 後端 AppVM01 伺服器內容的簡單 web 應用程式。

此應用程式提供簡單的測試環境的 hello DMZ 範例及如何變更 hello 端點、 Nsg、 UDR，許多與防火牆規則可能會影響流量。

## <a name="firewall-rule-tooallow-icmp"></a>防火牆規則 tooallow ICMP
這個簡單的 PowerShell 陳述式可以執行任何 Windows VM tooallow ICMP (Ping) 流量。 此防火牆的更新可讓您更輕鬆測試及疑難排解藉由使用 hello ping 通訊協定 toopass 通過 hello （適用於大部分 ICMP 預設為開啟的 Linux 散發版本） 的 windows 防火牆。

```PowerShell
# Turn On ICMPv4
New-NetFirewallRule -Name Allow_ICMPv4 -DisplayName "Allow ICMPv4" `
    -Protocol ICMPv4 -Enabled True -Profile Any -Action Allow
```

如果您使用下列指令碼的 hello，此防火牆規則加入動作 hello 第一個陳述式。

## <a name="iis01---web-application-installation-script"></a>IIS01 - Web 應用程式安裝指令碼
此指令碼會：

1. 開啟 IMCPv4 (Ping) 您更輕鬆測試 hello 本機伺服器 windows 防火牆
2. 安裝 IIS 和 hello.Net Framework 4.5 版
3. 建立 ASP.NET 網頁和 Web.config 檔案
4. 變更 hello 預設應用程式集區 toomake 檔案存取更容易
5. 設定 hello 匿名使用者 tooyour 系統管理員帳戶和密碼

在透過遠端桌面 (RDP) 存取 IIS01 時，這個 PowerShell 指令碼應該會在本機執行。

```PowerShell
# IIS Server Post Build Config Script
# Get Admin Account and Password
    Write-Host "Please enter hello admin account information used toocreate this VM:" -ForegroundColor Cyan
    $theAdmin = Read-Host -Prompt "hello Admin Account Name (no domain or machine name)"
    $thePassword = Read-Host -Prompt "hello Admin Password"

# Turn On ICMPv4
    Write-Host "Creating ICMP Rule in Windows Firewall" -ForegroundColor Cyan
    New-NetFirewallRule -Name Allow_ICMPv4 -DisplayName "Allow ICMPv4" -Protocol ICMPv4 -Enabled True -Profile Any -Action Allow

# Install IIS
    Write-Host "Installing IIS and .Net 4.5, this can take some time, like 15+ minutes..." -ForegroundColor Cyan
    add-windowsfeature Web-Server, Web-WebServer, Web-Common-Http, Web-Default-Doc, Web-Dir-Browsing, Web-Http-Errors, Web-Static-Content, Web-Health, Web-Http-Logging, Web-Performance, Web-Stat-Compression, Web-Security, Web-Filtering, Web-App-Dev, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Net-Ext, Web-Net-Ext45, Web-Asp-Net45, Web-Mgmt-Tools, Web-Mgmt-Console

# Create Web App Pages
    Write-Host "Creating Web page and Web.Config file" -ForegroundColor Cyan
    $MainPage = '<%@ Page Language="vb" AutoEventWireup="false" %>
    <%@ Import Namespace="System.IO" %>
    <script language="vb" runat="server">
        Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs) Handles Me.Load
            Dim FILENAME As String = "\\10.0.2.5\WebShare\Rand.txt"
            Dim objStreamReader As StreamReader
            objStreamReader = File.OpenText(FILENAME)
            Dim contents As String = objStreamReader.ReadToEnd()
            lblOutput.Text = contents
            objStreamReader.Close()
            lblTime.Text = Now()
        End Sub
    </script>

    <!DOCTYPE html>
    <html xmlns="http://www.w3.org/1999/xhtml">
    <head runat="server">
        <title>DMZ Example App</title>
    </head>
    <body style="font-family: Optima,Segoe,Segoe UI,Candara,Calibri,Arial,sans-serif;">
      <form id="frmMain" runat="server">
        <div>
          <h1>Looks like you made it!</h1>
          This is a page from hello inside (a web server on a private network),<br />
          and it is making its way toohello outside! (If you are viewing this from hello internet)<br />
          <br />
          hello following sections show:
          <ul style="margin-top: 0px;">
            <li> Local Server Time - Shows if this page is or isnt cached anywhere</li>
            <li> File Output - Shows that hello web server is reaching AppVM01 on hello backend subnet and successfully returning content</li>
            <li> Image from hello Internet - Doesnt really show anything, but it made me happy toosee this when hello app worked</li>
          </ul>
          <div style="border: 2px solid #8AC007; border-radius: 25px; padding: 20px; margin: 10px; width: 650px;">
            <b>Local Web Server Time</b>: <asp:Label runat="server" ID="lblTime" /></div>
          <div style="border: 2px solid #8AC007; border-radius: 25px; padding: 20px; margin: 10px; width: 650px;">
            <b>File Output from AppVM01</b>: <asp:Label runat="server" ID="lblOutput" /></div>
          <div style="border: 2px solid #8AC007; border-radius: 25px; padding: 20px; margin: 10px; width: 650px;">
            <b>Image File Linked from hello Internet</b>:<br />
            <br />
            <img src="http://sd.keepcalm-o-matic.co.uk/i/keep-calm-you-made-it-7.png" alt="You made it!" width="150" length="175"/></div>
        </div>
      </form>
    </body>
    </html>'

    $WebConfig ='<?xml version="1.0" encoding="utf-8"?>
    <configuration>
      <system.web>
        <compilation debug="true" strict="false" explicit="true" targetFramework="4.5" />
        <httpRuntime targetFramework="4.5" />
        <identity impersonate="true" />
        <customErrors mode="Off"/>
      </system.web>
      <system.webServer>
        <defaultDocument>
          <files>
            <add value="Home.aspx" />
          </files>
        </defaultDocument>
      </system.webServer>
    </configuration>'

    $MainPage | Out-File -FilePath "C:\inetpub\wwwroot\Home.aspx" -Encoding ascii
    $WebConfig | Out-File -FilePath "C:\inetpub\wwwroot\Web.config" -Encoding ascii

# Set App Pool tooClasic Pipeline tooremote file access will work easier
    Write-Host "Updaing IIS Settings" -ForegroundColor Cyan
    c:\windows\system32\inetsrv\appcmd.exe set app "Default Web Site/" /applicationPool:".NET v4.5 Classic"
    c:\windows\system32\inetsrv\appcmd.exe set config "Default Web Site/" /section:system.webServer/security/authentication/anonymousAuthentication /userName:$theAdmin /password:$thePassword /commit:apphost

# Make sure hello IIS settings take
    Write-Host "Restarting hello W3SVC" -ForegroundColor Cyan
    Restart-Service -Name W3SVC

    Write-Host
    Write-Host "Web App Creation Successfull!" -ForegroundColor Green
    Write-Host
```

## <a name="appvm01---file-server-installation-script"></a>AppVM01 - 檔案伺服器安裝指令碼
此指令碼設定 hello 後端的這個簡單的應用程式。 此指令碼會：

1. 開啟 IMCPv4 (Ping) 您更輕鬆測試 hello 防火牆上
2. 建立 hello 網站的目錄
3. 遠端建立文字檔案 toobe hello 網頁存取
4. 設定權限 hello 目錄和檔案 tooAnonymous tooallow 存取
5. 關閉 IE 增強式安全性 tooallow 更容易從這部伺服器瀏覽 

> [!IMPORTANT]
> **最佳作法**： 永遠不會關閉 IE 增強式安全性，在實際執行伺服器上，再加上通常是不好的主意 toosurf hello web 從實際執行伺服器。 此外，最好不要開啟檔案共用來供匿名存取，這裡這樣做是為了簡單起見。
> 
> 

在透過遠端桌面 (RDP) 存取 AppVM01 時，這個 PowerShell 指令碼應該會在本機執行。 PowerShell 是必要的 toobe tooensure 成功執行時，系統管理員身分執行。

```PowerShell
# AppVM01 Server Post Build Config Script
# PowerShell must be run as Administrator for Net Share commands toowork

# Turn On ICMPv4
    New-NetFirewallRule -Name Allow_ICMPv4 -DisplayName "Allow ICMPv4" -Protocol ICMPv4 -Enabled True -Profile Any -Action Allow

# Create Directory
    New-Item "C:\WebShare" -ItemType Directory

# Write out Rand.txt
    $FileContent = "Hello, I'm hello contents of a remote file on AppVM01."
    $FileContent | Out-File -FilePath "C:\WebShare\Rand.txt" -Encoding ascii

# Set Permissions on share
    $Acl = Get-Acl "C:\WebShare"
    $AccessRule = New-Object system.security.accesscontrol.filesystemaccessrule("Everyone","ReadAndExecute, Synchronize","ContainerInherit, ObjectInherit","InheritOnly","Allow")
    $Acl.SetAccessRule($AccessRule)
    Set-Acl "C:\WebShare" $Acl

# Create network share
    Net Share WebShare=C:\WebShare "/grant:Everyone,READ"

# Turn Off IE Enhanced Security Configuration for Admins
    Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Active Setup\Installed Components\{A509B1A7-37EF-4b3f-8CFC-4F3A74704073}" -Name "IsInstalled" -Value 0

    Write-Host
    Write-Host "File Server Set up Successfull!" -ForegroundColor Green
    Write-Host
```

## <a name="dns01---dns-server-installation-script"></a>DNS01 - DNS 伺服器安裝指令碼
沒有任何指令碼包含在此範例應用程式 tooset，hello DNS 伺服器。 如果測試 hello 防火牆規則、 NSG，或 UDR 需要 tooinclude DNS 流量，hello DNS01 伺服器需要 toobe 手動設定。 hello 網路組態 xml 檔案，以及這兩個範例為 Resource Manager 範本包括 DNS01 為 hello 主要 DNS 伺服器及 hello 裝載為 hello 備份的 DNS 伺服器層級 3 的公用 DNS 伺服器。 hello 層級 3 DNS 伺服器會 hello 非本機流量使用實際 DNS 伺服器，而且與 DNS01 不安裝程式中，DNS 會發生任何區域網路。

## <a name="next-steps"></a>後續步驟
* 在 IIS 伺服器上執行 hello IIS01 指令碼
* 在 AppVM01 上執行檔案伺服器指令碼
* 瀏覽 toohello 公用 IP 上 IIS01 toovalidate 組建

<!--Link References-->
[HOME]: ../best-practices-network-security.md
