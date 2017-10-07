---
title: "從 Web 應用程式的 Azure 金鑰保存庫 aaaUse |Microsoft 文件"
description: "使用此教學課程 toohelp 您學習如何 toouse Azure 金鑰保存庫的 web 應用程式。"
services: key-vault
documentationcenter: 
author: adhurwit
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 9b7d065e-1979-4397-8298-eeba3aec4792
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: adhurwit
ms.openlocfilehash: d5e2299e60b379c4e234d5cd6be03411c5a5c958
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-key-vault-from-a-web-application"></a>從 Web 應用程式使用 Azure 金鑰保存庫
## <a name="introduction"></a>簡介
使用此教學課程 toohelp 您學習如何 toouse Azure 金鑰保存庫在 Azure 中的 web 應用程式。 它會引導您完成存取 Azure 金鑰保存庫中的密碼，使其可以用於 web 應用程式中的 hello 程序。

**估計時間 toocomplete:** 15 分鐘

如需 Azure 金鑰保存庫的概觀資訊，請參閱 [什麼是 Azure 金鑰保存庫？](key-vault-whatis.md)

## <a name="prerequisites"></a>必要條件
toocomplete 本教學課程中，您必須擁有下列 hello:

* 在 Azure 金鑰保存庫 URI tooa 密碼
* 用戶端識別碼和用戶端秘密 web 應用程式向 Azure Active Directory 具有存取 tooyour 金鑰保存庫
* Web 應用程式。 我們將說明 ASP.NET MVC 應用程式部署在 Azure Web 應用程式中的 hello 步驟。

> [!NOTE]
> 您已完成 hello 步驟中所列務必[開始使用 Azure 金鑰保存庫](key-vault-get-started.md)本教學課程中，讓您擁有 hello URI tooa 密碼和 hello 用戶端識別碼和用戶端密碼是 web 應用程式。
> 
> 

將用來存取 hello 金鑰保存庫的 hello web 應用程式為 hello 其中一個 Azure Active Directory 中註冊且已被授與存取 tooyour 金鑰保存庫。 如果這不是 hello 案例，請返回 tooRegister hello 快速入門教學課程中的應用程式，並重複 hello 步驟所列。

本教學課程是針對 web 程式開發人員了解 hello 基本概念，在 Azure 上建立 web 應用程式的設計。 如需有關 Azure Web Apps 的詳細資訊，請參閱 [Web Apps 概觀](../app-service-web/app-service-web-overview.md)。

## <a id="packages"></a>新增 Nuget 封裝
有兩個 web 應用程式需要 toohave 安裝的封裝。

* Active Directory 驗證程式庫 - 包含與 Azure Active Directory 互動及管理使用者身分識別的方法
* Azure 金鑰保存庫資源庫 - 包含與 Azure 金鑰保存庫互動的方法

這兩個這些封裝可以使用安裝 hello Package Manager Console 使用 hello Install-package 命令。

    // this is currently hello latest stable version of ADAL
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

    Install-Package Microsoft.Azure.KeyVault


## <a id="webconfig"></a>修改 Web.Config
有三個應用程式設定需要 toobe 加入的 toohello web.config 檔案，如下所示。

    <!-- ClientId and ClientSecret refer toohello web application registration with Azure Active Directory -->
    <add key="ClientId" value="clientid" />
    <add key="ClientSecret" value="clientsecret" />

    <!-- SecretUri is hello URI for hello secret in Azure Key Vault -->
    <add key="SecretUri" value="secreturi" />


如果您不會 toohost 您應用程式當做 Azure Web 應用程式，您應該加入 hello 實際 ClientId、 用戶端密碼和密碼 URI 值 toohello web.config。因為我們將會獲得一層額外的安全性 hello Azure 入口網站中加入 hello 實際值，否則保留這些空值。

## <a id="gettoken"></a>加入方法 tooGet 存取權杖
在訂單 toouse hello 金鑰保存庫 API 中，您需要存取權杖。 金鑰保存庫用戶端 hello 處理呼叫 toohello 金鑰保存庫 API，但需要 toosupply 取得 hello 存取語彙基元函式使用。  

以下是 hello 程式碼 tooget 從 Azure Active Directory 存取權杖。 此程式碼可以放置在應用程式的任何位置。 我喜歡 tooadd 公用程式或 EncryptionHelper 類別。  

    //add these using statements
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using System.Threading.Tasks;
    using System.Web.Configuration;

    //this is an optional property toohold hello secret after it is retrieved
    public static string EncryptSecret { get; set; }

    //hello method that will be provided toohello KeyVaultClient
    public static async Task<string> GetToken(string authority, string resource, string scope)
    {
        var authContext = new AuthenticationContext(authority);
        ClientCredential clientCred = new ClientCredential(WebConfigurationManager.AppSettings["ClientId"],
                    WebConfigurationManager.AppSettings["ClientSecret"]);
        AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

        if (result == null)
            throw new InvalidOperationException("Failed tooobtain hello JWT token");

        return result.AccessToken;
    }

> [!NOTE]
> 使用用戶端識別碼和用戶端密碼是最簡單方式 tooauthenticate hello Azure AD 應用程式。 此外，如果在 Web 應用程式中使用該密碼，您將能夠區分職責，並充分掌控您的金鑰管理。 但是，它會依賴置於您的組態設定其中部分可能會放在您的組態設定，想 tooprotect hello 密碼做為有風險的 hello 用戶端密碼。 如 toouse 用戶端識別碼和憑證，而不是用戶端識別碼和用戶端密碼 tooauthenticate hello Azure AD 應用程式的討論，請參閱下方內容。
> 
> 

## <a id="appstart"></a>擷取在啟動應用程式的 hello 密碼
現在我們需要 toocall hello 金鑰保存庫 API 的程式碼，並擷取 hello 密碼。 hello 下列程式碼可能會放入任何地方，只要您需要 toouse 之前呼叫它。 我有 hello hello Global.asax 中的應用程式開始事件中將這個程式，以便執行一次啟動並讓 hello 供 hello 應用程式密碼。

    //add these using statements
    using Microsoft.Azure.KeyVault;
    using System.Web.Configuration;

    // I put my GetToken method in a Utils class. Change for wherever you placed your method.
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

    var sec = await kv.GetSecretAsync(WebConfigurationManager.AppSettings["SecretUri"]);

    //I put a variable in a Utils class toohold hello secret for general  application use.
    Utils.EncryptSecret = sec.Value;



## <a id="portalsettings"></a>在 hello Azure 入口網站 （選擇性） 加入應用程式設定
如果您有 Azure Web 應用程式您現在可以在 hello Azure 入口網站中加入 hello hello AppSettings 的實際值。 如此一來，hello 實際值 hello web.config 中將不會但受到 hello 入口網站具有獨立的存取控制功能。 這些值將會取代為您輸入在 web.config 中的 hello 值。請確定 hello 名稱是 hello 相同。

![Azure 入口網站中顯示的應用程式設定][1]

## <a name="authenticate-with-a-certificate-instead-of-a-client-secret"></a>使用憑證 (而非用戶端密碼) 進行驗證。
另一個方式 tooauthenticate Azure AD 應用程式是使用用戶端識別碼和憑證，而非用戶端識別碼和用戶端密碼。 下列是 hello 步驟 toouse Azure Web 應用程式中的憑證：

1. 取得或建立憑證
2. 將憑證 hello 與 Azure AD 應用程式產生關聯
3. 新增程式碼 tooyour Web 應用程式 toouse hello 憑證
4. 新增憑證 tooyour Web 應用程式

**取得或建立憑證** 基於本文的目的，我們將測試憑證。 以下是幾個您可以使用開發人員命令提示字元 toocreate 中憑證的命令。 變更目錄 toowhere 您想要建立 hello 憑證檔案。  此外，開頭和結尾 hello 憑證日期 hello，使用 hello 目前日期加上 1 年。

    makecert -sv mykey.pvk -n "cn=KVWebApp" KVWebApp.cer -b 03/07/2017 -e 03/07/2018 -r
    pvk2pfx -pvk mykey.pvk -spc KVWebApp.cer -pfx KVWebApp.pfx -po test123

請記下 hello 結束日期和 hello hello.pfx 的密碼 (在此範例中： 07/31/2016年和 test123)。 您將需要在下面使用這些資訊。

如需如何建立測試憑證的詳細資訊，請參閱 [做法：自行建立測試憑證](https://msdn.microsoft.com/library/ff699202.aspx)

**與 Azure AD 應用程式產生關聯的 hello 憑證**有憑證之後，您需要 tooassociate 它與 Azure AD 應用程式。 目前，hello Azure 入口網站不支援這個工作流程。這可以透過 PowerShell 完成。 執行下列命令 tooassoicate hello 憑證與 hello Azure AD 應用程式的 hello:

    $x509 = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2
    $x509.Import("C:\data\KVWebApp.cer")
    $credValue = [System.Convert]::ToBase64String($x509.GetRawCertData())

    # If you used different dates for makecert then adjust these values
    $now = [System.DateTime]::Now
    $yearfromnow = $now.AddYears(1)

    $adapp = New-AzureRmADApplication -DisplayName "KVWebApp" -HomePage "http://kvwebapp" -IdentifierUris "http://kvwebapp" -CertValue $credValue -StartDate $now -EndDate $yearfromnow

    $sp = New-AzureRmADServicePrincipal -ApplicationId $adapp.ApplicationId

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'contosokv' -ServicePrincipalName $sp.ServicePrincipalName -PermissionsToSecrets all -ResourceGroupName 'contosorg'

    # get hello thumbprint toouse in your app settings
    $x509.Thumbprint

執行這些命令之後，您可以看到在 Azure AD 中的 hello 應用程式。 搜尋時，請選取 [我的公司擁有的應用程式] 而不是 「 應用程式我的公司會使用"hello 搜尋對話方塊。

toolearn 深入了解 Azure AD 應用程式物件和 ServicePrincipal 物件，請參閱[應用程式與服務主體物件](../active-directory/active-directory-application-objects.md)

**新增程式碼 tooyour Web 應用程式 toouse hello 憑證**現在我們將會加入程式碼 tooyour Web 應用程式 tooaccess hello 憑證，並將它用於驗證。

第一個是程式碼 tooaccess hello 憑證。

    public static class CertificateHelper
    {
        public static X509Certificate2 FindCertificateByThumbprint(string findValue)
        {
            X509Store store = new X509Store(StoreName.My, StoreLocation.CurrentUser);
            try
            {
                store.Open(OpenFlags.ReadOnly);
                X509Certificate2Collection col = store.Certificates.Find(X509FindType.FindByThumbprint,
                    findValue, false); // Don't validate certs, since hello test root isn't installed.
                if (col == null || col.Count == 0)
                    return null;
                return col[0];
            }
            finally
            {
                store.Close();
            }
        }
    }


請注意該 hello StoreLocation 而不是 LocalMachine CurrentUser。 我們提供的 'false' toohello 並發現方法，因為我們使用測試憑證。

接下來是使用 hello CertificateHelper 並建立 ClientAssertionCertificate 為驗證所需的程式碼。

    public static ClientAssertionCertificate AssertionCert { get; set; }

    public static void GetCert()
    {
        var clientAssertionCertPfx = CertificateHelper.FindCertificateByThumbprint(WebConfigurationManager.AppSettings["thumbprint"]);
        AssertionCert = new ClientAssertionCertificate(WebConfigurationManager.AppSettings["clientid"], clientAssertionCertPfx);
    }


以下是 hello 新程式碼 tooget hello 的存取權杖。 這會取代上述的 hello GetToken 方法。 為方便起見，我已將其改名。

    public static async Task<string> GetAccessToken(string authority, string resource, string scope)
    {
        var context = new AuthenticationContext(authority, TokenCache.DefaultShared);
        var result = await context.AcquireTokenAsync(resource, AssertionCert);
        return result.AccessToken;
    }

為了方便使用，我已將所有此類程式碼放入我的 Web 應用程式專案的公用程式類別。

最後一個程式碼變更 hello 處於 hello Application_Start 方法。 首先，我們需要 toocall hello GetCert() 方法 tooload hello ClientAssertionCertificate。 然後我們再變更 hello 時建立新的 KeyVaultClient 我們提供的回呼方法。 請注意這會取代 hello 我們在上面的程式碼。

    Utils.GetCert();
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetAccessToken));


**新增憑證 tooyour Web 應用程式透過 Azure 入口網站 hello**新增憑證 tooyour Web 應用程式是簡單的兩個步驟的程序。 首先，請移 toohello Azure 入口網站，並瀏覽 tooyour Web 應用程式。 在 hello 設定刀鋒視窗中的 Web 應用程式，按一下 「 自訂網域與 SSL 」 hello 項目。 Hello 上刀鋒視窗，開啟時，您將會無法 tooupload hello KVWebApp.pfx 先前建立的憑證，請確定您記得 hello hello pfx 密碼。

![在 hello Azure 入口網站中加入憑證 tooa Web 應用程式][2]

hello，您需要 toodo 的最後一個項目是 tooadd 具有 hello 名稱網站的 Web 應用程式的應用程式設定 tooyour\_負載\_憑證和值為 *。 如此可確保載入所有憑證。 如果您想 tooload 只有 hello 的憑證，您已上傳，然後您可以輸入其指紋的逗號分隔清單。

toolearn 詳細資料加入憑證 tooa Web 應用程式，請參閱[Azure 網站應用程式中使用的憑證](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)

**新增憑證 tooKey 保存庫做為密碼**而不是直接上傳您的憑證 toohello Web 應用程式服務，您可以將它儲存在金鑰保存庫做為密碼，並將它從該處部署。 這是兩個步驟程序所述 hello 下列部落格文章：[透過金鑰保存庫部署 Azure Web 應用程式憑證](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)

## <a id="next"></a>接續步驟
如需程式設計參考，請參閱 [Azure 金鑰保存庫 C# 用戶端 API 參考](https://msdn.microsoft.com/library/azure/dn903628.aspx)。

<!--Image references-->
[1]: ./media/key-vault-use-from-web-application/PortalAppSettings.png
[2]: ./media/key-vault-use-from-web-application/PortalAddCertificate.png
