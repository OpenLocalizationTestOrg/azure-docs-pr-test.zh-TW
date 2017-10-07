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
# <a name="use-azure-key-vault-from-a-web-application"></a><span data-ttu-id="24abb-103">從 Web 應用程式使用 Azure 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="24abb-103">Use Azure Key Vault from a Web Application</span></span>
## <a name="introduction"></a><span data-ttu-id="24abb-104">簡介</span><span class="sxs-lookup"><span data-stu-id="24abb-104">Introduction</span></span>
<span data-ttu-id="24abb-105">使用此教學課程 toohelp 您學習如何 toouse Azure 金鑰保存庫在 Azure 中的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="24abb-105">Use this tutorial toohelp you learn how toouse Azure Key Vault from a web application in Azure.</span></span> <span data-ttu-id="24abb-106">它會引導您完成存取 Azure 金鑰保存庫中的密碼，使其可以用於 web 應用程式中的 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="24abb-106">It walks you through hello process of accessing a secret from an Azure Key Vault so that it can be used in your web application.</span></span>

<span data-ttu-id="24abb-107">**估計時間 toocomplete:** 15 分鐘</span><span class="sxs-lookup"><span data-stu-id="24abb-107">**Estimated time toocomplete:** 15 minutes</span></span>

<span data-ttu-id="24abb-108">如需 Azure 金鑰保存庫的概觀資訊，請參閱 [什麼是 Azure 金鑰保存庫？](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="24abb-108">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24abb-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="24abb-109">Prerequisites</span></span>
<span data-ttu-id="24abb-110">toocomplete 本教學課程中，您必須擁有下列 hello:</span><span class="sxs-lookup"><span data-stu-id="24abb-110">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="24abb-111">在 Azure 金鑰保存庫 URI tooa 密碼</span><span class="sxs-lookup"><span data-stu-id="24abb-111">A URI tooa secret in an Azure Key Vault</span></span>
* <span data-ttu-id="24abb-112">用戶端識別碼和用戶端秘密 web 應用程式向 Azure Active Directory 具有存取 tooyour 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="24abb-112">A Client ID and a Client Secret for a web application registered with Azure Active Directory that has access tooyour Key Vault</span></span>
* <span data-ttu-id="24abb-113">Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="24abb-113">A web application.</span></span> <span data-ttu-id="24abb-114">我們將說明 ASP.NET MVC 應用程式部署在 Azure Web 應用程式中的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="24abb-114">We will be showing hello steps for an ASP.NET MVC application deployed in Azure as a Web App.</span></span>

> [!NOTE]
> <span data-ttu-id="24abb-115">您已完成 hello 步驟中所列務必[開始使用 Azure 金鑰保存庫](key-vault-get-started.md)本教學課程中，讓您擁有 hello URI tooa 密碼和 hello 用戶端識別碼和用戶端密碼是 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="24abb-115">It is essential that you have completed hello steps listed in [Get Started with Azure Key Vault](key-vault-get-started.md) for this tutorial so that you have hello URI tooa secret and hello Client ID and Client Secret for a web application.</span></span>
> 
> 

<span data-ttu-id="24abb-116">將用來存取 hello 金鑰保存庫的 hello web 應用程式為 hello 其中一個 Azure Active Directory 中註冊且已被授與存取 tooyour 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="24abb-116">hello web application that will be accessing hello Key Vault is hello one that is registered in Azure Active Directory and has been given access tooyour Key Vault.</span></span> <span data-ttu-id="24abb-117">如果這不是 hello 案例，請返回 tooRegister hello 快速入門教學課程中的應用程式，並重複 hello 步驟所列。</span><span class="sxs-lookup"><span data-stu-id="24abb-117">If this is not hello case, go back tooRegister an Application in hello Get Started tutorial and repeat hello steps listed.</span></span>

<span data-ttu-id="24abb-118">本教學課程是針對 web 程式開發人員了解 hello 基本概念，在 Azure 上建立 web 應用程式的設計。</span><span class="sxs-lookup"><span data-stu-id="24abb-118">This tutorial is designed for web developers that understand hello basics of creating web applications on Azure.</span></span> <span data-ttu-id="24abb-119">如需有關 Azure Web Apps 的詳細資訊，請參閱 [Web Apps 概觀](../app-service-web/app-service-web-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="24abb-119">For more information about Azure Web Apps, see [Web Apps overview](../app-service-web/app-service-web-overview.md).</span></span>

## <span data-ttu-id="24abb-120"><a id="packages"></a>新增 Nuget 封裝</span><span class="sxs-lookup"><span data-stu-id="24abb-120"><a id="packages"></a>Add Nuget Packages</span></span>
<span data-ttu-id="24abb-121">有兩個 web 應用程式需要 toohave 安裝的封裝。</span><span class="sxs-lookup"><span data-stu-id="24abb-121">There are two packages that your web application needs toohave installed.</span></span>

* <span data-ttu-id="24abb-122">Active Directory 驗證程式庫 - 包含與 Azure Active Directory 互動及管理使用者身分識別的方法</span><span class="sxs-lookup"><span data-stu-id="24abb-122">Active Directory Authentication Library - contains methods for interacting with Azure Active Directory and managing user identity</span></span>
* <span data-ttu-id="24abb-123">Azure 金鑰保存庫資源庫 - 包含與 Azure 金鑰保存庫互動的方法</span><span class="sxs-lookup"><span data-stu-id="24abb-123">Azure Key Vault Library - contains methods for interacting with Azure Key Vault</span></span>

<span data-ttu-id="24abb-124">這兩個這些封裝可以使用安裝 hello Package Manager Console 使用 hello Install-package 命令。</span><span class="sxs-lookup"><span data-stu-id="24abb-124">Both of these packages can be installed using hello Package Manager Console using hello Install-Package command.</span></span>

    // this is currently hello latest stable version of ADAL
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

    Install-Package Microsoft.Azure.KeyVault


## <span data-ttu-id="24abb-125"><a id="webconfig"></a>修改 Web.Config</span><span class="sxs-lookup"><span data-stu-id="24abb-125"><a id="webconfig"></a>Modify Web.Config</span></span>
<span data-ttu-id="24abb-126">有三個應用程式設定需要 toobe 加入的 toohello web.config 檔案，如下所示。</span><span class="sxs-lookup"><span data-stu-id="24abb-126">There are three application settings that need toobe added toohello web.config file as follows.</span></span>

    <!-- ClientId and ClientSecret refer toohello web application registration with Azure Active Directory -->
    <add key="ClientId" value="clientid" />
    <add key="ClientSecret" value="clientsecret" />

    <!-- SecretUri is hello URI for hello secret in Azure Key Vault -->
    <add key="SecretUri" value="secreturi" />


<span data-ttu-id="24abb-127">如果您不會 toohost 您應用程式當做 Azure Web 應用程式，您應該加入 hello 實際 ClientId、 用戶端密碼和密碼 URI 值 toohello web.config。因為我們將會獲得一層額外的安全性 hello Azure 入口網站中加入 hello 實際值，否則保留這些空值。</span><span class="sxs-lookup"><span data-stu-id="24abb-127">If you are not going toohost your application as an Azure Web App, then you should add hello actual ClientId, Client Secret, and Secret URI values toohello web.config. Otherwise leave these dummy values because we will be adding hello actual values in hello Azure Portal for an additional level of security.</span></span>

## <span data-ttu-id="24abb-128"><a id="gettoken"></a>加入方法 tooGet 存取權杖</span><span class="sxs-lookup"><span data-stu-id="24abb-128"><a id="gettoken"></a>Add Method tooGet an Access Token</span></span>
<span data-ttu-id="24abb-129">在訂單 toouse hello 金鑰保存庫 API 中，您需要存取權杖。</span><span class="sxs-lookup"><span data-stu-id="24abb-129">In order toouse hello Key Vault API you need an access token.</span></span> <span data-ttu-id="24abb-130">金鑰保存庫用戶端 hello 處理呼叫 toohello 金鑰保存庫 API，但需要 toosupply 取得 hello 存取語彙基元函式使用。</span><span class="sxs-lookup"><span data-stu-id="24abb-130">hello Key Vault Client handles calls toohello Key Vault API but you need toosupply it with a function that gets hello access token.</span></span>  

<span data-ttu-id="24abb-131">以下是 hello 程式碼 tooget 從 Azure Active Directory 存取權杖。</span><span class="sxs-lookup"><span data-stu-id="24abb-131">Following is hello code tooget an access token from Azure Active Directory.</span></span> <span data-ttu-id="24abb-132">此程式碼可以放置在應用程式的任何位置。</span><span class="sxs-lookup"><span data-stu-id="24abb-132">This code can go anywhere in your application.</span></span> <span data-ttu-id="24abb-133">我喜歡 tooadd 公用程式或 EncryptionHelper 類別。</span><span class="sxs-lookup"><span data-stu-id="24abb-133">I like tooadd a Utils or EncryptionHelper class.</span></span>  

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
> <span data-ttu-id="24abb-134">使用用戶端識別碼和用戶端密碼是最簡單方式 tooauthenticate hello Azure AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="24abb-134">Using a Client ID and Client Secret is hello easiest way tooauthenticate an Azure AD application.</span></span> <span data-ttu-id="24abb-135">此外，如果在 Web 應用程式中使用該密碼，您將能夠區分職責，並充分掌控您的金鑰管理。</span><span class="sxs-lookup"><span data-stu-id="24abb-135">And using it in your web application allows for a separation of duties and more control over your key management.</span></span> <span data-ttu-id="24abb-136">但是，它會依賴置於您的組態設定其中部分可能會放在您的組態設定，想 tooprotect hello 密碼做為有風險的 hello 用戶端密碼。</span><span class="sxs-lookup"><span data-stu-id="24abb-136">But it does rely on putting hello Client Secret in your configuration settings which for some can be as risky as putting hello secret that you want tooprotect in your configuration settings.</span></span> <span data-ttu-id="24abb-137">如 toouse 用戶端識別碼和憑證，而不是用戶端識別碼和用戶端密碼 tooauthenticate hello Azure AD 應用程式的討論，請參閱下方內容。</span><span class="sxs-lookup"><span data-stu-id="24abb-137">See below for a discussion on how toouse a Client ID and Certificate instead of Client ID and Client Secret tooauthenticate hello Azure AD application.</span></span>
> 
> 

## <span data-ttu-id="24abb-138"><a id="appstart"></a>擷取在啟動應用程式的 hello 密碼</span><span class="sxs-lookup"><span data-stu-id="24abb-138"><a id="appstart"></a>Retrieve hello secret on Application Start</span></span>
<span data-ttu-id="24abb-139">現在我們需要 toocall hello 金鑰保存庫 API 的程式碼，並擷取 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="24abb-139">Now we need code toocall hello Key Vault API and retrieve hello secret.</span></span> <span data-ttu-id="24abb-140">hello 下列程式碼可能會放入任何地方，只要您需要 toouse 之前呼叫它。</span><span class="sxs-lookup"><span data-stu-id="24abb-140">hello following code can be put anywhere as long as it is called before you need toouse it.</span></span> <span data-ttu-id="24abb-141">我有 hello hello Global.asax 中的應用程式開始事件中將這個程式，以便執行一次啟動並讓 hello 供 hello 應用程式密碼。</span><span class="sxs-lookup"><span data-stu-id="24abb-141">I have put this code in hello Application Start event in hello Global.asax so that it runs once on start and makes hello secret available for hello application.</span></span>

    //add these using statements
    using Microsoft.Azure.KeyVault;
    using System.Web.Configuration;

    // I put my GetToken method in a Utils class. Change for wherever you placed your method.
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

    var sec = await kv.GetSecretAsync(WebConfigurationManager.AppSettings["SecretUri"]);

    //I put a variable in a Utils class toohold hello secret for general  application use.
    Utils.EncryptSecret = sec.Value;



## <span data-ttu-id="24abb-142"><a id="portalsettings"></a>在 hello Azure 入口網站 （選擇性） 加入應用程式設定</span><span class="sxs-lookup"><span data-stu-id="24abb-142"><a id="portalsettings"></a>Add App Settings in hello Azure Portal (optional)</span></span>
<span data-ttu-id="24abb-143">如果您有 Azure Web 應用程式您現在可以在 hello Azure 入口網站中加入 hello hello AppSettings 的實際值。</span><span class="sxs-lookup"><span data-stu-id="24abb-143">If you have an Azure Web App you can now add hello actual values for hello AppSettings in hello Azure Portal.</span></span> <span data-ttu-id="24abb-144">如此一來，hello 實際值 hello web.config 中將不會但受到 hello 入口網站具有獨立的存取控制功能。</span><span class="sxs-lookup"><span data-stu-id="24abb-144">By doing this, hello actual values will not be in hello web.config but protected via hello Portal where you have separate access control capabilities.</span></span> <span data-ttu-id="24abb-145">這些值將會取代為您輸入在 web.config 中的 hello 值。請確定 hello 名稱是 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="24abb-145">These values will be substituted for hello values that you entered in your web.config. Make sure that hello names are hello same.</span></span>

![Azure 入口網站中顯示的應用程式設定][1]

## <a name="authenticate-with-a-certificate-instead-of-a-client-secret"></a><span data-ttu-id="24abb-147">使用憑證 (而非用戶端密碼) 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="24abb-147">Authenticate with a Certificate instead of a Client Secret</span></span>
<span data-ttu-id="24abb-148">另一個方式 tooauthenticate Azure AD 應用程式是使用用戶端識別碼和憑證，而非用戶端識別碼和用戶端密碼。</span><span class="sxs-lookup"><span data-stu-id="24abb-148">Another way tooauthenticate an Azure AD application is by using a Client ID and a Certificate instead of a Client ID and Client Secret.</span></span> <span data-ttu-id="24abb-149">下列是 hello 步驟 toouse Azure Web 應用程式中的憑證：</span><span class="sxs-lookup"><span data-stu-id="24abb-149">Following are hello steps toouse a Certificate in an Azure Web App:</span></span>

1. <span data-ttu-id="24abb-150">取得或建立憑證</span><span class="sxs-lookup"><span data-stu-id="24abb-150">Get or Create a Certificate</span></span>
2. <span data-ttu-id="24abb-151">將憑證 hello 與 Azure AD 應用程式產生關聯</span><span class="sxs-lookup"><span data-stu-id="24abb-151">Associate hello Certificate with an Azure AD application</span></span>
3. <span data-ttu-id="24abb-152">新增程式碼 tooyour Web 應用程式 toouse hello 憑證</span><span class="sxs-lookup"><span data-stu-id="24abb-152">Add code tooyour Web App toouse hello Certificate</span></span>
4. <span data-ttu-id="24abb-153">新增憑證 tooyour Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="24abb-153">Add a Certificate tooyour Web App</span></span>

<span data-ttu-id="24abb-154">**取得或建立憑證** 基於本文的目的，我們將測試憑證。</span><span class="sxs-lookup"><span data-stu-id="24abb-154">**Get or Create a Certificate** For our purposes we will make a test certificate.</span></span> <span data-ttu-id="24abb-155">以下是幾個您可以使用開發人員命令提示字元 toocreate 中憑證的命令。</span><span class="sxs-lookup"><span data-stu-id="24abb-155">Here are a couple of commands that you can use in a Developer Command Prompt toocreate a certificate.</span></span> <span data-ttu-id="24abb-156">變更目錄 toowhere 您想要建立 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="24abb-156">Change directory toowhere you want hello cert files created.</span></span>  <span data-ttu-id="24abb-157">此外，開頭和結尾 hello 憑證日期 hello，使用 hello 目前日期加上 1 年。</span><span class="sxs-lookup"><span data-stu-id="24abb-157">Also, for hello beginning and ending date of hello certificate, use hello current date plus 1 year.</span></span>

    makecert -sv mykey.pvk -n "cn=KVWebApp" KVWebApp.cer -b 03/07/2017 -e 03/07/2018 -r
    pvk2pfx -pvk mykey.pvk -spc KVWebApp.cer -pfx KVWebApp.pfx -po test123

<span data-ttu-id="24abb-158">請記下 hello 結束日期和 hello hello.pfx 的密碼 (在此範例中： 07/31/2016年和 test123)。</span><span class="sxs-lookup"><span data-stu-id="24abb-158">Make note of hello end date and hello password for hello .pfx (in this example: 07/31/2016 and test123).</span></span> <span data-ttu-id="24abb-159">您將需要在下面使用這些資訊。</span><span class="sxs-lookup"><span data-stu-id="24abb-159">You will need them below.</span></span>

<span data-ttu-id="24abb-160">如需如何建立測試憑證的詳細資訊，請參閱 [做法：自行建立測試憑證](https://msdn.microsoft.com/library/ff699202.aspx)</span><span class="sxs-lookup"><span data-stu-id="24abb-160">For more information on creating a test certificate, see [How to: Create Your Own Test Certificate](https://msdn.microsoft.com/library/ff699202.aspx)</span></span>

<span data-ttu-id="24abb-161">**與 Azure AD 應用程式產生關聯的 hello 憑證**有憑證之後，您需要 tooassociate 它與 Azure AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="24abb-161">**Associate hello Certificate with an Azure AD application** Now that you have a certificate, you need tooassociate it with an Azure AD application.</span></span> <span data-ttu-id="24abb-162">目前，hello Azure 入口網站不支援這個工作流程。這可以透過 PowerShell 完成。</span><span class="sxs-lookup"><span data-stu-id="24abb-162">Presently, hello Azure Portal does not support this workflow; this can be completed through PowerShell.</span></span> <span data-ttu-id="24abb-163">執行下列命令 tooassoicate hello 憑證與 hello Azure AD 應用程式的 hello:</span><span class="sxs-lookup"><span data-stu-id="24abb-163">Run hello following commands tooassoicate hello certificate with hello Azure AD application:</span></span>

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

<span data-ttu-id="24abb-164">執行這些命令之後，您可以看到在 Azure AD 中的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="24abb-164">After you have run these commands, you can see hello application in Azure AD.</span></span> <span data-ttu-id="24abb-165">搜尋時，請選取 [我的公司擁有的應用程式] 而不是 「 應用程式我的公司會使用"hello 搜尋對話方塊。</span><span class="sxs-lookup"><span data-stu-id="24abb-165">When searching, ensure you select "Applications my company owns" instead of "Applications my company uses" in hello search dialog.</span></span>

<span data-ttu-id="24abb-166">toolearn 深入了解 Azure AD 應用程式物件和 ServicePrincipal 物件，請參閱[應用程式與服務主體物件](../active-directory/active-directory-application-objects.md)</span><span class="sxs-lookup"><span data-stu-id="24abb-166">toolearn more about Azure AD Application Objects and ServicePrincipal Objects, see [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md)</span></span>

<span data-ttu-id="24abb-167">**新增程式碼 tooyour Web 應用程式 toouse hello 憑證**現在我們將會加入程式碼 tooyour Web 應用程式 tooaccess hello 憑證，並將它用於驗證。</span><span class="sxs-lookup"><span data-stu-id="24abb-167">**Add code tooyour Web App toouse hello Certificate** Now we will add code tooyour Web App tooaccess hello cert and use it for authentication.</span></span>

<span data-ttu-id="24abb-168">第一個是程式碼 tooaccess hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="24abb-168">First there is code tooaccess hello cert.</span></span>

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


<span data-ttu-id="24abb-169">請注意該 hello StoreLocation 而不是 LocalMachine CurrentUser。</span><span class="sxs-lookup"><span data-stu-id="24abb-169">Note that hello StoreLocation is CurrentUser instead of LocalMachine.</span></span> <span data-ttu-id="24abb-170">我們提供的 'false' toohello 並發現方法，因為我們使用測試憑證。</span><span class="sxs-lookup"><span data-stu-id="24abb-170">And that we are supplying 'false' toohello Find method because we are using a test cert.</span></span>

<span data-ttu-id="24abb-171">接下來是使用 hello CertificateHelper 並建立 ClientAssertionCertificate 為驗證所需的程式碼。</span><span class="sxs-lookup"><span data-stu-id="24abb-171">Next is code that uses hello CertificateHelper and creates a ClientAssertionCertificate which is needed for authentication.</span></span>

    public static ClientAssertionCertificate AssertionCert { get; set; }

    public static void GetCert()
    {
        var clientAssertionCertPfx = CertificateHelper.FindCertificateByThumbprint(WebConfigurationManager.AppSettings["thumbprint"]);
        AssertionCert = new ClientAssertionCertificate(WebConfigurationManager.AppSettings["clientid"], clientAssertionCertPfx);
    }


<span data-ttu-id="24abb-172">以下是 hello 新程式碼 tooget hello 的存取權杖。</span><span class="sxs-lookup"><span data-stu-id="24abb-172">Here is hello new code tooget hello access token.</span></span> <span data-ttu-id="24abb-173">這會取代上述的 hello GetToken 方法。</span><span class="sxs-lookup"><span data-stu-id="24abb-173">This replaces hello GetToken method above.</span></span> <span data-ttu-id="24abb-174">為方便起見，我已將其改名。</span><span class="sxs-lookup"><span data-stu-id="24abb-174">I have given it a different name for convenience.</span></span>

    public static async Task<string> GetAccessToken(string authority, string resource, string scope)
    {
        var context = new AuthenticationContext(authority, TokenCache.DefaultShared);
        var result = await context.AcquireTokenAsync(resource, AssertionCert);
        return result.AccessToken;
    }

<span data-ttu-id="24abb-175">為了方便使用，我已將所有此類程式碼放入我的 Web 應用程式專案的公用程式類別。</span><span class="sxs-lookup"><span data-stu-id="24abb-175">I have put all of this code into my Web App project's Utils class for ease of use.</span></span>

<span data-ttu-id="24abb-176">最後一個程式碼變更 hello 處於 hello Application_Start 方法。</span><span class="sxs-lookup"><span data-stu-id="24abb-176">hello last code change is in hello Application_Start method.</span></span> <span data-ttu-id="24abb-177">首先，我們需要 toocall hello GetCert() 方法 tooload hello ClientAssertionCertificate。</span><span class="sxs-lookup"><span data-stu-id="24abb-177">First we need toocall hello GetCert() method tooload hello ClientAssertionCertificate.</span></span> <span data-ttu-id="24abb-178">然後我們再變更 hello 時建立新的 KeyVaultClient 我們提供的回呼方法。</span><span class="sxs-lookup"><span data-stu-id="24abb-178">And then we change hello callback method that we supply when creating a new KeyVaultClient.</span></span> <span data-ttu-id="24abb-179">請注意這會取代 hello 我們在上面的程式碼。</span><span class="sxs-lookup"><span data-stu-id="24abb-179">Note that this replaces hello code that we had above.</span></span>

    Utils.GetCert();
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetAccessToken));


<span data-ttu-id="24abb-180">**新增憑證 tooyour Web 應用程式透過 Azure 入口網站 hello**新增憑證 tooyour Web 應用程式是簡單的兩個步驟的程序。</span><span class="sxs-lookup"><span data-stu-id="24abb-180">**Add a Certificate tooyour Web App through hello Azure Portal** Adding a Certificate tooyour Web App is a simple two-step process.</span></span> <span data-ttu-id="24abb-181">首先，請移 toohello Azure 入口網站，並瀏覽 tooyour Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="24abb-181">First, go toohello Azure Portal and navigate tooyour Web App.</span></span> <span data-ttu-id="24abb-182">在 hello 設定刀鋒視窗中的 Web 應用程式，按一下 「 自訂網域與 SSL 」 hello 項目。</span><span class="sxs-lookup"><span data-stu-id="24abb-182">On hello Settings blade for your Web App, click on hello entry for "Custom domains and SSL".</span></span> <span data-ttu-id="24abb-183">Hello 上刀鋒視窗，開啟時，您將會無法 tooupload hello KVWebApp.pfx 先前建立的憑證，請確定您記得 hello hello pfx 密碼。</span><span class="sxs-lookup"><span data-stu-id="24abb-183">On hello blade that opens you will be able tooupload hello Certificate that you created above, KVWebApp.pfx, make sure that you remember hello password for hello pfx.</span></span>

![在 hello Azure 入口網站中加入憑證 tooa Web 應用程式][2]

<span data-ttu-id="24abb-185">hello，您需要 toodo 的最後一個項目是 tooadd 具有 hello 名稱網站的 Web 應用程式的應用程式設定 tooyour\_負載\_憑證和值為 *。</span><span class="sxs-lookup"><span data-stu-id="24abb-185">hello last thing that you need toodo is tooadd an Application Setting tooyour Web App that has hello name WEBSITE\_LOAD\_CERTIFICATES and a value of *.</span></span> <span data-ttu-id="24abb-186">如此可確保載入所有憑證。</span><span class="sxs-lookup"><span data-stu-id="24abb-186">This will ensure that all Certificates are loaded.</span></span> <span data-ttu-id="24abb-187">如果您想 tooload 只有 hello 的憑證，您已上傳，然後您可以輸入其指紋的逗號分隔清單。</span><span class="sxs-lookup"><span data-stu-id="24abb-187">If you wanted tooload only hello Certificates that you have uploaded, then you can enter a comma-separated list of their thumbprints.</span></span>

<span data-ttu-id="24abb-188">toolearn 詳細資料加入憑證 tooa Web 應用程式，請參閱[Azure 網站應用程式中使用的憑證](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)</span><span class="sxs-lookup"><span data-stu-id="24abb-188">toolearn more about adding a Certificate tooa Web App, see [Using Certificates in Azure Websites Applications](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)</span></span>

<span data-ttu-id="24abb-189">**新增憑證 tooKey 保存庫做為密碼**而不是直接上傳您的憑證 toohello Web 應用程式服務，您可以將它儲存在金鑰保存庫做為密碼，並將它從該處部署。</span><span class="sxs-lookup"><span data-stu-id="24abb-189">**Add a Certificate tooKey Vault as a secret** Instead of uploading your certificate toohello Web App service directly, you can store it in Key Vault as a secret and deploy it from there.</span></span> <span data-ttu-id="24abb-190">這是兩個步驟程序所述 hello 下列部落格文章：[透過金鑰保存庫部署 Azure Web 應用程式憑證](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)</span><span class="sxs-lookup"><span data-stu-id="24abb-190">This is a two-step process that is outlined in hello following blog post, [Deploying Azure Web App Certificate through Key Vault](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)</span></span>

## <span data-ttu-id="24abb-191"><a id="next"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="24abb-191"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="24abb-192">如需程式設計參考，請參閱 [Azure 金鑰保存庫 C# 用戶端 API 參考](https://msdn.microsoft.com/library/azure/dn903628.aspx)。</span><span class="sxs-lookup"><span data-stu-id="24abb-192">For programming references, see [Azure Key Vault C# Client API Reference](https://msdn.microsoft.com/library/azure/dn903628.aspx).</span></span>

<!--Image references-->
[1]: ./media/key-vault-use-from-web-application/PortalAppSettings.png
[2]: ./media/key-vault-use-from-web-application/PortalAddCertificate.png
