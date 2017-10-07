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
# <a name="silently-install-hello-azure-ad-application-proxy-connector"></a>無訊息方式安裝 hello Azure AD 應用程式 Proxy 連接器
您想 toobe 無法 toosend toomultiple Windows 伺服器或 tooWindows 伺服器沒有啟用的使用者介面，安裝指令碼。 本主題會協助您建立 Windows PowerShell 指令碼，以便自動安裝和註冊 Azure AD 應用程式 Proxy 連接器。

當您想要執行下列工作時，此功能很實用︰

* 沒有 UI 層，或您不能 RDP toohello 機器電腦上安裝 hello 連接器。
* 一次安裝並註冊許多連接器。
* 整合 hello 連接器安裝和註冊另一個程序的一部分。
* 建立標準的伺服器映像，且包含 hello 連接器位元，但未註冊。

應用程式 Proxy 的運作方式是呼叫您網路中的 hello 連接器輕薄 Windows Server 服務安裝。 Hello 應用程式 Proxy 連接器 toowork 它具有 toobe 向 Azure AD 目錄使用的全域管理員和密碼。 通常，此資訊是在連接器安裝期間於一個快顯對話方塊中輸入的。 不過，您可以使用 Windows PowerShell toocreate 認證物件 tooenter 註冊資訊。 您可以建立您自己的權杖，並使用它 tooenter 或您的註冊資訊。

## <a name="install-hello-connector"></a>安裝 hello 連接器
安裝 hello 連接器 Msi，而不註冊 hello 連接器，如下所示：

1. 開啟命令提示字元。
2. 執行下列的命令中的 hello /q 表示無訊息安裝的 hello-hello 安裝不會提示您 tooaccept hello 使用者授權合約。
   
        AADApplicationProxyConnectorInstaller.exe REGISTERCONNECTOR="false" /q

## <a name="register-hello-connector-with-azure-ad"></a>使用 Azure AD 註冊 hello 連接器
有兩種方法，您可以使用 tooregister hello 連接器：

* 註冊使用 Windows PowerShell 認證物件的 hello 連接器
* 註冊使用離線時建立的語彙基元的 hello 連接器

### <a name="register-hello-connector-using-a-windows-powershell-credential-object"></a>註冊使用 Windows PowerShell 認證物件的 hello 連接器
1. 執行此命令建立 hello Windows PowerShell 認證物件。 取代 *\<username\>* 和*\<密碼\>* hello 使用者名稱和密碼為您的目錄：
   
        $User = "<username>"
        $PlainPassword = '<password>'
        $SecurePassword = $PlainPassword | ConvertTo-SecureString -AsPlainText -Force
        $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $User, $SecurePassword
2. 跳過**C:\Program Files\Microsoft AAD 應用程式 Proxy 連接器**hello 使用執行指令碼 hello PowerShell 認證物件和您所建立。 取代*$cred* hello 名稱 hello PowerShell 認證物件所建立：
   
        RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Credentials -Usercredentials $cred

### <a name="register-hello-connector-using-a-token-created-offline"></a>註冊使用離線時建立的語彙基元的 hello 連接器
1. 建立離線權杖使用 hello AuthenticationContext 類別 hello 程式碼片段中使用 hello 值：

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


2. 一旦您擁有 hello 語彙基元，建立使用 hello 語彙基元 securestring 的形式：

   `$SecureToken = $Token | ConvertTo-SecureString -AsPlainText -Force`

3. 下列 Windows PowerShell 命令，取代執行的 hello\<租用戶 GUID\>目錄識別碼：

   `RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Token -Token $SecureToken -TenantId <tenant GUID>`

## <a name="next-steps"></a>後續步驟 
* [使用您自己的網域名稱發行應用程式](active-directory-application-proxy-custom-domains.md)
* [啟用單一登入](active-directory-application-proxy-sso-using-kcd.md)
* [使用應用程式 Proxy 疑難排解您遇到的問題](active-directory-application-proxy-troubleshoot.md)


