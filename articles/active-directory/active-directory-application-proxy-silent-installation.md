---
title: "aaaSilent 安裝 Azure AD 應用程式 Proxy 連接器 |Microsoft 文件"
description: "涵蓋如何 tooperform 自動安裝的 Azure AD 應用程式 Proxy 連接器 tooprovide 安全遠端存取 tooyour 內部部署應用程式。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 3aa1c7f2-fb2a-4693-abd5-95bb53700cbb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: ce796ff45a65ba7d5f0f63c02085bdc6af494548
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="silently-install-hello-azure-ad-application-proxy-connector"></a><span data-ttu-id="886d8-103">無訊息方式安裝 hello Azure AD 應用程式 Proxy 連接器</span><span class="sxs-lookup"><span data-stu-id="886d8-103">Silently install hello Azure AD Application Proxy Connector</span></span>
<span data-ttu-id="886d8-104">您想 toobe 無法 toosend toomultiple Windows 伺服器或 tooWindows 伺服器沒有啟用的使用者介面，安裝指令碼。</span><span class="sxs-lookup"><span data-stu-id="886d8-104">You want toobe able toosend an installation script toomultiple Windows servers or tooWindows Servers that don't have user interface enabled.</span></span> <span data-ttu-id="886d8-105">本主題會協助您建立 Windows PowerShell 指令碼，以便自動安裝和註冊 Azure AD 應用程式 Proxy 連接器。</span><span class="sxs-lookup"><span data-stu-id="886d8-105">This topic helps you create a Windows PowerShell script that enables unattended installation and registration for your Azure AD Application Proxy Connector.</span></span>

<span data-ttu-id="886d8-106">當您想要執行下列工作時，此功能很實用︰</span><span class="sxs-lookup"><span data-stu-id="886d8-106">This capability is useful when you want to:</span></span>

* <span data-ttu-id="886d8-107">沒有 UI 層，或您不能 RDP toohello 機器電腦上安裝 hello 連接器。</span><span class="sxs-lookup"><span data-stu-id="886d8-107">Install hello connector on machines with no UI layer or when you cannot RDP toohello machine.</span></span>
* <span data-ttu-id="886d8-108">一次安裝並註冊許多連接器。</span><span class="sxs-lookup"><span data-stu-id="886d8-108">Install and register many connectors at once.</span></span>
* <span data-ttu-id="886d8-109">整合 hello 連接器安裝和註冊另一個程序的一部分。</span><span class="sxs-lookup"><span data-stu-id="886d8-109">Integrate hello connector installation and registration as part of another procedure.</span></span>
* <span data-ttu-id="886d8-110">建立標準的伺服器映像，且包含 hello 連接器位元，但未註冊。</span><span class="sxs-lookup"><span data-stu-id="886d8-110">Create a standard server image that contains hello connector bits but is not registered.</span></span>

<span data-ttu-id="886d8-111">應用程式 Proxy 的運作方式是呼叫您網路中的 hello 連接器輕薄 Windows Server 服務安裝。</span><span class="sxs-lookup"><span data-stu-id="886d8-111">Application Proxy works by installing a slim Windows Server service called hello Connector inside your network.</span></span> <span data-ttu-id="886d8-112">Hello 應用程式 Proxy 連接器 toowork 它具有 toobe 向 Azure AD 目錄使用的全域管理員和密碼。</span><span class="sxs-lookup"><span data-stu-id="886d8-112">For hello Application Proxy Connector toowork it has toobe registered with your Azure AD directory using a global administrator and password.</span></span> <span data-ttu-id="886d8-113">通常，此資訊是在連接器安裝期間於一個快顯對話方塊中輸入的。</span><span class="sxs-lookup"><span data-stu-id="886d8-113">Ordinarily this information is entered during Connector installation in a pop-up dialog box.</span></span> <span data-ttu-id="886d8-114">不過，您可以使用 Windows PowerShell toocreate 認證物件 tooenter 註冊資訊。</span><span class="sxs-lookup"><span data-stu-id="886d8-114">However, you can use Windows PowerShell toocreate a credential object tooenter your registration information.</span></span> <span data-ttu-id="886d8-115">您可以建立您自己的權杖，並使用它 tooenter 或您的註冊資訊。</span><span class="sxs-lookup"><span data-stu-id="886d8-115">Or you can create your own token and use it tooenter your registration information.</span></span>

## <a name="install-hello-connector"></a><span data-ttu-id="886d8-116">安裝 hello 連接器</span><span class="sxs-lookup"><span data-stu-id="886d8-116">Install hello connector</span></span>
<span data-ttu-id="886d8-117">安裝 hello 連接器 Msi，而不註冊 hello 連接器，如下所示：</span><span class="sxs-lookup"><span data-stu-id="886d8-117">Install hello Connector MSIs without registering hello Connector as follows:</span></span>

1. <span data-ttu-id="886d8-118">開啟命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="886d8-118">Open a command prompt.</span></span>
2. <span data-ttu-id="886d8-119">執行下列的命令中的 hello /q 表示無訊息安裝的 hello-hello 安裝不會提示您 tooaccept hello 使用者授權合約。</span><span class="sxs-lookup"><span data-stu-id="886d8-119">Run hello following command in which hello /q means quiet installation - hello installation doesn't prompt you tooaccept hello End-User License Agreement.</span></span>
   
        AADApplicationProxyConnectorInstaller.exe REGISTERCONNECTOR="false" /q

## <a name="register-hello-connector-with-azure-ad"></a><span data-ttu-id="886d8-120">使用 Azure AD 註冊 hello 連接器</span><span class="sxs-lookup"><span data-stu-id="886d8-120">Register hello connector with Azure AD</span></span>
<span data-ttu-id="886d8-121">有兩種方法，您可以使用 tooregister hello 連接器：</span><span class="sxs-lookup"><span data-stu-id="886d8-121">There are two methods you can use tooregister hello connector:</span></span>

* <span data-ttu-id="886d8-122">註冊使用 Windows PowerShell 認證物件的 hello 連接器</span><span class="sxs-lookup"><span data-stu-id="886d8-122">Register hello connector using a Windows PowerShell credential object</span></span>
* <span data-ttu-id="886d8-123">註冊使用離線時建立的語彙基元的 hello 連接器</span><span class="sxs-lookup"><span data-stu-id="886d8-123">Register hello connector using a token created offline</span></span>

### <a name="register-hello-connector-using-a-windows-powershell-credential-object"></a><span data-ttu-id="886d8-124">註冊使用 Windows PowerShell 認證物件的 hello 連接器</span><span class="sxs-lookup"><span data-stu-id="886d8-124">Register hello connector using a Windows PowerShell credential object</span></span>
1. <span data-ttu-id="886d8-125">執行此命令建立 hello Windows PowerShell 認證物件。</span><span class="sxs-lookup"><span data-stu-id="886d8-125">Create hello Windows PowerShell Credentials object by running this command.</span></span> <span data-ttu-id="886d8-126">取代 *\<username\>* 和*\<密碼\>* hello 使用者名稱和密碼為您的目錄：</span><span class="sxs-lookup"><span data-stu-id="886d8-126">Replace *\<username\>* and *\<password\>* with hello username and password for your directory:</span></span>
   
        $User = "<username>"
        $PlainPassword = '<password>'
        $SecurePassword = $PlainPassword | ConvertTo-SecureString -AsPlainText -Force
        $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $User, $SecurePassword
2. <span data-ttu-id="886d8-127">跳過**C:\Program Files\Microsoft AAD 應用程式 Proxy 連接器**hello 使用執行指令碼 hello PowerShell 認證物件和您所建立。</span><span class="sxs-lookup"><span data-stu-id="886d8-127">Go too**C:\Program Files\Microsoft AAD App Proxy Connector** and run hello script using hello PowerShell credentials object you created.</span></span> <span data-ttu-id="886d8-128">取代*$cred* hello 名稱 hello PowerShell 認證物件所建立：</span><span class="sxs-lookup"><span data-stu-id="886d8-128">Replace *$cred* with hello name of hello PowerShell credentials object you created:</span></span>
   
        RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Credentials -Usercredentials $cred

### <a name="register-hello-connector-using-a-token-created-offline"></a><span data-ttu-id="886d8-129">註冊使用離線時建立的語彙基元的 hello 連接器</span><span class="sxs-lookup"><span data-stu-id="886d8-129">Register hello connector using a token created offline</span></span>
1. <span data-ttu-id="886d8-130">建立離線權杖使用 hello AuthenticationContext 類別 hello 程式碼片段中使用 hello 值：</span><span class="sxs-lookup"><span data-stu-id="886d8-130">Create an offline token using hello AuthenticationContext class using hello values in hello code snippet:</span></span>

        using System;
        using System.Diagnostics;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;

        class Program
        {
        #region constants
        /// <summary>
        /// hello AAD authentication endpoint uri
        /// </summary>
        static readonly Uri AadAuthenticationEndpoint = new Uri("https://login.microsoftonline.com/common/oauth2/token?api-version=1.0");

        /// <summary>
        /// hello application ID of hello connector in AAD
        /// </summary>
        static readonly string ConnectorAppId = "55747057-9b5d-4bd4-b387-abf52a8bd489";

        /// <summary>
        /// hello reply address of hello connector application in AAD
        /// </summary>
        static readonly Uri ConnectorRedirectAddress = new Uri("urn:ietf:wg:oauth:2.0:oob");

        /// <summary>
        /// hello AppIdUri of hello registration service in AAD
        /// </summary>
        static readonly Uri RegistrationServiceAppIdUri = new Uri("https://proxy.cloudwebappproxy.net/registerapp");

        #endregion

        #region private members
        private string token;
        private string tenantID;
        #endregion

        public void GetAuthenticationToken()
        {
            AuthenticationContext authContext = new AuthenticationContext(AadAuthenticationEndpoint.AbsoluteUri);

            AuthenticationResult authResult = authContext.AcquireToken(RegistrationServiceAppIdUri.AbsoluteUri,
                ConnectorAppId,
                ConnectorRedirectAddress,
                PromptBehavior.Always);

            if (authResult == null || string.IsNullOrEmpty(authResult.AccessToken) || string.IsNullOrEmpty(authResult.TenantId))
            {
                Trace.TraceError("Authentication result, token or tenant id returned are null");
                throw new InvalidOperationException("Authentication result, token or tenant id returned are null");
            }

            token = authResult.AccessToken;
            tenantID = authResult.TenantId;
        }


2. <span data-ttu-id="886d8-131">一旦您擁有 hello 語彙基元，建立使用 hello 語彙基元 securestring 的形式：</span><span class="sxs-lookup"><span data-stu-id="886d8-131">Once you have hello token, create a SecureString using hello token:</span></span>

   `$SecureToken = $Token | ConvertTo-SecureString -AsPlainText -Force`

3. <span data-ttu-id="886d8-132">下列 Windows PowerShell 命令，取代執行的 hello\<租用戶 GUID\>目錄識別碼：</span><span class="sxs-lookup"><span data-stu-id="886d8-132">Run hello following Windows PowerShell command, replacing \<tenant GUID\> with your directory ID:</span></span>

   `RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Token -Token $SecureToken -TenantId <tenant GUID>`

## <a name="next-steps"></a><span data-ttu-id="886d8-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="886d8-133">Next steps</span></span> 
* [<span data-ttu-id="886d8-134">使用您自己的網域名稱發行應用程式</span><span class="sxs-lookup"><span data-stu-id="886d8-134">Publish applications using your own domain name</span></span>](active-directory-application-proxy-custom-domains.md)
* [<span data-ttu-id="886d8-135">啟用單一登入</span><span class="sxs-lookup"><span data-stu-id="886d8-135">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
* [<span data-ttu-id="886d8-136">使用應用程式 Proxy 疑難排解您遇到的問題</span><span class="sxs-lookup"><span data-stu-id="886d8-136">Troubleshoot issues you're having with Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)


