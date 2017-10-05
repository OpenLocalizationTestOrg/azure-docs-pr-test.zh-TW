---
title: "與 DMZ 搭配使用的 Azure 範例應用程式 | Microsoft Docs"
description: "在建立 DMZ 來測試流量案例後部署這個簡單的 Web 應用程式"
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
ms.openlocfilehash: 8506238e41c5d9dac8d76d729d4919b30a0528b9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="sample-application-for-use-with-dmzs"></a><span data-ttu-id="349ee-103">與 DMZ 搭配使用的範例應用程式</span><span class="sxs-lookup"><span data-stu-id="349ee-103">Sample application for use with DMZs</span></span>
<span data-ttu-id="349ee-104">[返回 [安全性界限最佳作法] 頁面][HOME]</span><span class="sxs-lookup"><span data-stu-id="349ee-104">[Return to the Security Boundary Best Practices Page][HOME]</span></span>

<span data-ttu-id="349ee-105">這些 PowerShell 指令碼可在 IIS01 和 AppVM01 伺服器本機上執行，用來安裝和設定一個簡單的 Web 應用程式，以顯示一個來自前端 IIS01 伺服器而內容來自後端 AppVM01 的 html 頁面。</span><span class="sxs-lookup"><span data-stu-id="349ee-105">These PowerShell scripts can be run locally on the IIS01 and AppVM01 servers to install and set up a simple web application that displays an html page from the front-end IIS01 server with content from the back-end AppVM01 server.</span></span>

<span data-ttu-id="349ee-106">此應用程式提供簡單的測試環境，可測試許多 DMZ 範例，以及端點、NSG、UDR 及防火牆規則的變更對流量的影響。</span><span class="sxs-lookup"><span data-stu-id="349ee-106">This application provides a simple testing environment for many of the DMZ Examples and how changes on the Endpoints, NSGs, UDR, and Firewall rules can affect traffic flows.</span></span>

## <a name="firewall-rule-to-allow-icmp"></a><span data-ttu-id="349ee-107">允許 ICMP 的防火牆規則</span><span class="sxs-lookup"><span data-stu-id="349ee-107">Firewall rule to allow ICMP</span></span>
<span data-ttu-id="349ee-108">這個簡單的 PowerShell 陳述式可以在任何 Windows VM 上執行，以允許 ICMP (Ping) 流量。</span><span class="sxs-lookup"><span data-stu-id="349ee-108">This simple PowerShell statement can be run on any Windows VM to allow ICMP (Ping) traffic.</span></span> <span data-ttu-id="349ee-109">此防火牆更新藉由允許 ping 通訊協定通過 Windows 防火牆，讓您能夠更輕鬆進行測試和疑難排解 (ICMP 在大多數 Linux 散發版本上預設為開啟)。</span><span class="sxs-lookup"><span data-stu-id="349ee-109">This firewall update allows for easier testing and troubleshooting by allowing the ping protocol to pass through the windows firewall (for most Linux distros ICMP is on by default).</span></span>

```PowerShell
# Turn On ICMPv4
New-NetFirewallRule -Name Allow_ICMPv4 -DisplayName "Allow ICMPv4" `
    -Protocol ICMPv4 -Enabled True -Profile Any -Action Allow
```

<span data-ttu-id="349ee-110">如果您使用下列指令碼，則這個新增的防火牆規則是第一個陳述式。</span><span class="sxs-lookup"><span data-stu-id="349ee-110">If you use the following scripts, this firewall rule addition is the first statement.</span></span>

## <a name="iis01---web-application-installation-script"></a><span data-ttu-id="349ee-111">IIS01 - Web 應用程式安裝指令碼</span><span class="sxs-lookup"><span data-stu-id="349ee-111">IIS01 - Web application installation script</span></span>
<span data-ttu-id="349ee-112">此指令碼會：</span><span class="sxs-lookup"><span data-stu-id="349ee-112">This script will:</span></span>

1. <span data-ttu-id="349ee-113">在本機伺服器 Windows 防火牆開啟 IMCPv4 (Ping) 以方便測試</span><span class="sxs-lookup"><span data-stu-id="349ee-113">Open IMCPv4 (Ping) on the local server windows firewall for easier testing</span></span>
2. <span data-ttu-id="349ee-114">安裝 IIS 和 .Net Framework v4.5</span><span class="sxs-lookup"><span data-stu-id="349ee-114">Install IIS and the .Net Framework v4.5</span></span>
3. <span data-ttu-id="349ee-115">建立 ASP.NET 網頁和 Web.config 檔案</span><span class="sxs-lookup"><span data-stu-id="349ee-115">Create an ASP.NET web page and a Web.config file</span></span>
4. <span data-ttu-id="349ee-116">變更預設應用程式集區以方便存取檔案</span><span class="sxs-lookup"><span data-stu-id="349ee-116">Change the Default application pool to make file access easier</span></span>
5. <span data-ttu-id="349ee-117">將匿名使用者設定為您的系統管理員帳戶和密碼</span><span class="sxs-lookup"><span data-stu-id="349ee-117">Set the Anonymous user to your admin account and password</span></span>

<span data-ttu-id="349ee-118">在透過遠端桌面 (RDP) 存取 IIS01 時，這個 PowerShell 指令碼應該會在本機執行。</span><span class="sxs-lookup"><span data-stu-id="349ee-118">This PowerShell script should be run locally while RDP’d into IIS01.</span></span>

```PowerShell
# IIS Server Post Build Config Script
# Get Admin Account and Password
    Write-Host "Please enter the admin account information used to create this VM:" -ForegroundColor Cyan
    $theAdmin = Read-Host -Prompt "The Admin Account Name (no domain or machine name)"
    $thePassword = Read-Host -Prompt "The Admin Password"

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
          This is a page from the inside (a web server on a private network),<br />
          and it is making its way to the outside! (If you are viewing this from the internet)<br />
          <br />
          The following sections show:
          <ul style="margin-top: 0px;">
            <li> Local Server Time - Shows if this page is or isnt cached anywhere</li>
            <li> File Output - Shows that the web server is reaching AppVM01 on the backend subnet and successfully returning content</li>
            <li> Image from the Internet - Doesnt really show anything, but it made me happy to see this when the app worked</li>
          </ul>
          <div style="border: 2px solid #8AC007; border-radius: 25px; padding: 20px; margin: 10px; width: 650px;">
            <b>Local Web Server Time</b>: <asp:Label runat="server" ID="lblTime" /></div>
          <div style="border: 2px solid #8AC007; border-radius: 25px; padding: 20px; margin: 10px; width: 650px;">
            <b>File Output from AppVM01</b>: <asp:Label runat="server" ID="lblOutput" /></div>
          <div style="border: 2px solid #8AC007; border-radius: 25px; padding: 20px; margin: 10px; width: 650px;">
            <b>Image File Linked from the Internet</b>:<br />
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

# Set App Pool to Clasic Pipeline to remote file access will work easier
    Write-Host "Updaing IIS Settings" -ForegroundColor Cyan
    c:\windows\system32\inetsrv\appcmd.exe set app "Default Web Site/" /applicationPool:".NET v4.5 Classic"
    c:\windows\system32\inetsrv\appcmd.exe set config "Default Web Site/" /section:system.webServer/security/authentication/anonymousAuthentication /userName:$theAdmin /password:$thePassword /commit:apphost

# Make sure the IIS settings take
    Write-Host "Restarting the W3SVC" -ForegroundColor Cyan
    Restart-Service -Name W3SVC

    Write-Host
    Write-Host "Web App Creation Successfull!" -ForegroundColor Green
    Write-Host
```

## <a name="appvm01---file-server-installation-script"></a><span data-ttu-id="349ee-119">AppVM01 - 檔案伺服器安裝指令碼</span><span class="sxs-lookup"><span data-stu-id="349ee-119">AppVM01 - File server installation script</span></span>
<span data-ttu-id="349ee-120">此指令碼會設定這個簡單應用程式的後端。</span><span class="sxs-lookup"><span data-stu-id="349ee-120">This script sets up the back-end for this simple application.</span></span> <span data-ttu-id="349ee-121">此指令碼會：</span><span class="sxs-lookup"><span data-stu-id="349ee-121">This script will:</span></span>

1. <span data-ttu-id="349ee-122">在防火牆開啟 IMCPv4 (Ping) 以方便測試</span><span class="sxs-lookup"><span data-stu-id="349ee-122">Open IMCPv4 (Ping) on the firewall for easier testing</span></span>
2. <span data-ttu-id="349ee-123">建立網站的目錄</span><span class="sxs-lookup"><span data-stu-id="349ee-123">Create a directory for the web site</span></span>
3. <span data-ttu-id="349ee-124">建立網頁所要遠端存取的文字檔</span><span class="sxs-lookup"><span data-stu-id="349ee-124">Create a text file to be remotely access by the web page</span></span>
4. <span data-ttu-id="349ee-125">將目錄和檔案的權限設為匿名以允許存取</span><span class="sxs-lookup"><span data-stu-id="349ee-125">Set permissions on the directory and file to Anonymous to allow access</span></span>
5. <span data-ttu-id="349ee-126">關閉 IE 增強式安全性以允許更輕鬆地從這部伺服器瀏覽</span><span class="sxs-lookup"><span data-stu-id="349ee-126">Turn off IE Enhanced Security to allow easier browsing from this server</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="349ee-127">**最佳做法**：永遠不要關閉實際執行伺服器上的「IE 增強式安全性」，而且從實際執行伺服器上網通常不是個好主意。</span><span class="sxs-lookup"><span data-stu-id="349ee-127">**Best Practice**: Never turn off IE Enhanced Security on a production server, plus it's generally a bad idea to surf the web from a production server.</span></span> <span data-ttu-id="349ee-128">此外，最好不要開啟檔案共用來供匿名存取，這裡這樣做是為了簡單起見。</span><span class="sxs-lookup"><span data-stu-id="349ee-128">Also, opening up file shares for anonymous access is a bad idea, but done here for simplicity.</span></span>
> 
> 

<span data-ttu-id="349ee-129">在透過遠端桌面 (RDP) 存取 AppVM01 時，這個 PowerShell 指令碼應該會在本機執行。</span><span class="sxs-lookup"><span data-stu-id="349ee-129">This PowerShell script should be run locally while RDP’d into AppVM01.</span></span> <span data-ttu-id="349ee-130">PowerShell 必須以系統管理員身分執行，才能成功執行。</span><span class="sxs-lookup"><span data-stu-id="349ee-130">PowerShell is required to be run as Administrator to ensure successful execution.</span></span>

```PowerShell
# AppVM01 Server Post Build Config Script
# PowerShell must be run as Administrator for Net Share commands to work

# Turn On ICMPv4
    New-NetFirewallRule -Name Allow_ICMPv4 -DisplayName "Allow ICMPv4" -Protocol ICMPv4 -Enabled True -Profile Any -Action Allow

# Create Directory
    New-Item "C:\WebShare" -ItemType Directory

# Write out Rand.txt
    $FileContent = "Hello, I'm the contents of a remote file on AppVM01."
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

## <a name="dns01---dns-server-installation-script"></a><span data-ttu-id="349ee-131">DNS01 - DNS 伺服器安裝指令碼</span><span class="sxs-lookup"><span data-stu-id="349ee-131">DNS01 - DNS server installation script</span></span>
<span data-ttu-id="349ee-132">此範例應用程式中未包含任何要設定 DNS 伺服器的指令碼。</span><span class="sxs-lookup"><span data-stu-id="349ee-132">There is no script included in this sample application to set up the DNS server.</span></span> <span data-ttu-id="349ee-133">如果防火牆規則、NSG 或 UDR 的測試需要包含 DNS 流量，就必須手動安裝 DNS01 伺服器。</span><span class="sxs-lookup"><span data-stu-id="349ee-133">If testing of the firewall rules, NSG, or UDR needs to include DNS traffic, the DNS01 server needs to be set up manually.</span></span> <span data-ttu-id="349ee-134">這兩個範例的「網路組態」XML 檔案和「Resource Manager 範本」都包含 DNS01 作為主要 DNS 伺服器，而由「層級 3」裝載的公用 DNS 伺服器則作為備份 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="349ee-134">The Network Configuration xml file and Resource Manager Template for both examples includes DNS01 as the primary DNS server and the public DNS server hosted by Level 3 as the backup DNS server.</span></span> <span data-ttu-id="349ee-135">「層級 3」DNS 伺服器會是非本機流量所使用的實際 DNS 伺服器，而如果未安裝 DNS01，則不會發生區域網路 DNS。</span><span class="sxs-lookup"><span data-stu-id="349ee-135">The Level 3 DNS server would be the actual DNS server used for non-local traffic, and with DNS01 not setup, no local network DNS would occur.</span></span>

## <a name="next-steps"></a><span data-ttu-id="349ee-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="349ee-136">Next steps</span></span>
* <span data-ttu-id="349ee-137">在 IIS 伺服器上執行 IIS01 指令碼</span><span class="sxs-lookup"><span data-stu-id="349ee-137">Run the IIS01 script on an IIS server</span></span>
* <span data-ttu-id="349ee-138">在 AppVM01 上執行檔案伺服器指令碼</span><span class="sxs-lookup"><span data-stu-id="349ee-138">Run File Server script on AppVM01</span></span>
* <span data-ttu-id="349ee-139">瀏覽至 IIS01 上的公用 IP 以驗證您的組建</span><span class="sxs-lookup"><span data-stu-id="349ee-139">Browse to the Public IP on IIS01 to validate your build</span></span>

<!--Link References-->
[HOME]: ../best-practices-network-security.md
