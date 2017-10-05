---
title: "從 Web 應用程式使用 Azure 金鑰保存庫 | Microsoft Docs"
description: "使用本教學課程來幫助您了解如何從 Web 應用程式使用 Azure 金鑰保存庫。"
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
ms.openlocfilehash: d095bcfe37baefa90cf79bb48bff3f703ce1dad7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-key-vault-from-a-web-application"></a><span data-ttu-id="093af-103">從 Web 應用程式使用 Azure 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="093af-103">Use Azure Key Vault from a Web Application</span></span>
## <a name="introduction"></a><span data-ttu-id="093af-104">簡介</span><span class="sxs-lookup"><span data-stu-id="093af-104">Introduction</span></span>
<span data-ttu-id="093af-105">使用此教學課程來幫助您了解如何從 Azure 中的 Web 應用程式使用 Azure 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="093af-105">Use this tutorial to help you learn how to use Azure Key Vault from a web application in Azure.</span></span> <span data-ttu-id="093af-106">它會引導您完成從 Azure 金鑰保存庫存取密碼的程序，以便在 Web 應用程式中使用該密碼。</span><span class="sxs-lookup"><span data-stu-id="093af-106">It walks you through the process of accessing a secret from an Azure Key Vault so that it can be used in your web application.</span></span>

<span data-ttu-id="093af-107">**預估完成時間：** 15 分鐘。</span><span class="sxs-lookup"><span data-stu-id="093af-107">**Estimated time to complete:** 15 minutes</span></span>

<span data-ttu-id="093af-108">如需 Azure 金鑰保存庫的概觀資訊，請參閱 [什麼是 Azure 金鑰保存庫？](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="093af-108">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="093af-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="093af-109">Prerequisites</span></span>
<span data-ttu-id="093af-110">若要完成本教學課程，您必須具備下列項目：</span><span class="sxs-lookup"><span data-stu-id="093af-110">To complete this tutorial, you must have the following:</span></span>

* <span data-ttu-id="093af-111">Azure 金鑰保存庫中密碼的 URI</span><span class="sxs-lookup"><span data-stu-id="093af-111">A URI to a secret in an Azure Key Vault</span></span>
* <span data-ttu-id="093af-112">已在 Azure Active Directory 註冊，且有權存取您金鑰保存庫之 Web 應用程式的用戶端識別碼和用戶端密碼</span><span class="sxs-lookup"><span data-stu-id="093af-112">A Client ID and a Client Secret for a web application registered with Azure Active Directory that has access to your Key Vault</span></span>
* <span data-ttu-id="093af-113">Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="093af-113">A web application.</span></span> <span data-ttu-id="093af-114">我們將會說明 ASP.NET MVC 應用程式在 Azure 中做為 Web 應用程式部署的步驟。</span><span class="sxs-lookup"><span data-stu-id="093af-114">We will be showing the steps for an ASP.NET MVC application deployed in Azure as a Web App.</span></span>

> [!NOTE]
> <span data-ttu-id="093af-115">在本教學課程中，完成在 [開始使用 Azure 金鑰保存庫](key-vault-get-started.md) 中所列步驟是很重要的，這樣您才會有 Web 應用程式的密碼 URI 和用戶端識別碼和用戶端密碼。</span><span class="sxs-lookup"><span data-stu-id="093af-115">It is essential that you have completed the steps listed in [Get Started with Azure Key Vault](key-vault-get-started.md) for this tutorial so that you have the URI to a secret and the Client ID and Client Secret for a web application.</span></span>
> 
> 

<span data-ttu-id="093af-116">已在 Azure Active Directory 註冊、且已獲權存取金鑰保存庫的 Web 應用程式將會被用來存取金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="093af-116">The web application that will be accessing the Key Vault is the one that is registered in Azure Active Directory and has been given access to your Key Vault.</span></span> <span data-ttu-id="093af-117">如果情況不是這樣，請回到開始使用教學課程中的註冊應用程式，並重複列出的步驟。</span><span class="sxs-lookup"><span data-stu-id="093af-117">If this is not the case, go back to Register an Application in the Get Started tutorial and repeat the steps listed.</span></span>

<span data-ttu-id="093af-118">本教學課程是針對 Web 開發人員所設計，這些開發人員必須了解在 Azure 上建立 Web 應用程式的基本概念。</span><span class="sxs-lookup"><span data-stu-id="093af-118">This tutorial is designed for web developers that understand the basics of creating web applications on Azure.</span></span> <span data-ttu-id="093af-119">如需有關 Azure Web Apps 的詳細資訊，請參閱 [Web Apps 概觀](../app-service-web/app-service-web-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="093af-119">For more information about Azure Web Apps, see [Web Apps overview](../app-service-web/app-service-web-overview.md).</span></span>

## <span data-ttu-id="093af-120"><a id="packages"></a>新增 Nuget 封裝</span><span class="sxs-lookup"><span data-stu-id="093af-120"><a id="packages"></a>Add Nuget Packages</span></span>
<span data-ttu-id="093af-121">有二個 Web 應用程式必須已安裝的封裝。</span><span class="sxs-lookup"><span data-stu-id="093af-121">There are two packages that your web application needs to have installed.</span></span>

* <span data-ttu-id="093af-122">Active Directory 驗證程式庫 - 包含與 Azure Active Directory 互動及管理使用者身分識別的方法</span><span class="sxs-lookup"><span data-stu-id="093af-122">Active Directory Authentication Library - contains methods for interacting with Azure Active Directory and managing user identity</span></span>
* <span data-ttu-id="093af-123">Azure 金鑰保存庫資源庫 - 包含與 Azure 金鑰保存庫互動的方法</span><span class="sxs-lookup"><span data-stu-id="093af-123">Azure Key Vault Library - contains methods for interacting with Azure Key Vault</span></span>

<span data-ttu-id="093af-124">您可以使用 Package Manager Console 的 Install-Package 命令安裝這二個封裝。</span><span class="sxs-lookup"><span data-stu-id="093af-124">Both of these packages can be installed using the Package Manager Console using the Install-Package command.</span></span>

    // this is currently the latest stable version of ADAL
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

    Install-Package Microsoft.Azure.KeyVault


## <span data-ttu-id="093af-125"><a id="webconfig"></a>修改 Web.Config</span><span class="sxs-lookup"><span data-stu-id="093af-125"><a id="webconfig"></a>Modify Web.Config</span></span>
<span data-ttu-id="093af-126">有三個必須加入至 web.config 檔案的應用程式設定，如下所示。</span><span class="sxs-lookup"><span data-stu-id="093af-126">There are three application settings that need to be added to the web.config file as follows.</span></span>

    <!-- ClientId and ClientSecret refer to the web application registration with Azure Active Directory -->
    <add key="ClientId" value="clientid" />
    <add key="ClientSecret" value="clientsecret" />

    <!-- SecretUri is the URI for the secret in Azure Key Vault -->
    <add key="SecretUri" value="secreturi" />


<span data-ttu-id="093af-127">如果您不打算將您的應用程式做為 Azure Web 應用程式裝載，則您應該將實際的 ClientId、用戶端密碼和密碼 URI 值加入 web.config。</span><span class="sxs-lookup"><span data-stu-id="093af-127">If you are not going to host your application as an Azure Web App, then you should add the actual ClientId, Client Secret, and Secret URI values to the web.config.</span></span> <span data-ttu-id="093af-128">因為我們將在 Azure 入口網站中新增實際值以取得額外的安全性層級，不然，您可以保留這些虛擬值。</span><span class="sxs-lookup"><span data-stu-id="093af-128">Otherwise leave these dummy values because we will be adding the actual values in the Azure Portal for an additional level of security.</span></span>

## <span data-ttu-id="093af-129"><a id="gettoken"></a>新增方法以取得存取權杖</span><span class="sxs-lookup"><span data-stu-id="093af-129"><a id="gettoken"></a>Add Method to Get an Access Token</span></span>
<span data-ttu-id="093af-130">為了能夠使用金鑰保存庫 API，您需要存取權杖。</span><span class="sxs-lookup"><span data-stu-id="093af-130">In order to use the Key Vault API you need an access token.</span></span> <span data-ttu-id="093af-131">金鑰保存庫用戶端會處理金鑰保存庫 API 的呼叫，但是您必須提供具有取得存取權杖的函式。</span><span class="sxs-lookup"><span data-stu-id="093af-131">The Key Vault Client handles calls to the Key Vault API but you need to supply it with a function that gets the access token.</span></span>  

<span data-ttu-id="093af-132">以下是從 Azure Active Directory 取得存取權杖的程式碼。</span><span class="sxs-lookup"><span data-stu-id="093af-132">Following is the code to get an access token from Azure Active Directory.</span></span> <span data-ttu-id="093af-133">此程式碼可以放置在應用程式的任何位置。</span><span class="sxs-lookup"><span data-stu-id="093af-133">This code can go anywhere in your application.</span></span> <span data-ttu-id="093af-134">我想要新增 Utils 或 EncryptionHelper 類別。</span><span class="sxs-lookup"><span data-stu-id="093af-134">I like to add a Utils or EncryptionHelper class.</span></span>  

    //add these using statements
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using System.Threading.Tasks;
    using System.Web.Configuration;

    //this is an optional property to hold the secret after it is retrieved
    public static string EncryptSecret { get; set; }

    //the method that will be provided to the KeyVaultClient
    public static async Task<string> GetToken(string authority, string resource, string scope)
    {
        var authContext = new AuthenticationContext(authority);
        ClientCredential clientCred = new ClientCredential(WebConfigurationManager.AppSettings["ClientId"],
                    WebConfigurationManager.AppSettings["ClientSecret"]);
        AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

        if (result == null)
            throw new InvalidOperationException("Failed to obtain the JWT token");

        return result.AccessToken;
    }

> [!NOTE]
> <span data-ttu-id="093af-135">使用用戶端識別碼和用戶端密碼來驗證 Azure AD 應用程式是最簡單的方法。</span><span class="sxs-lookup"><span data-stu-id="093af-135">Using a Client ID and Client Secret is the easiest way to authenticate an Azure AD application.</span></span> <span data-ttu-id="093af-136">此外，如果在 Web 應用程式中使用該密碼，您將能夠區分職責，並充分掌控您的金鑰管理。</span><span class="sxs-lookup"><span data-stu-id="093af-136">And using it in your web application allows for a separation of duties and more control over your key management.</span></span> <span data-ttu-id="093af-137">但是，要這樣做就必須將用戶端密碼保存在組態設定中。在某種程度上，這樣的做法與將您要保護的密碼保存在組態設定中的方法相較而言，兩者的風險是一樣的。</span><span class="sxs-lookup"><span data-stu-id="093af-137">But it does rely on putting the Client Secret in your configuration settings which for some can be as risky as putting the secret that you want to protect in your configuration settings.</span></span> <span data-ttu-id="093af-138">如需關於如何使用用戶端識別碼與憑證 (而非用戶端識別碼與用戶端密碼) 來驗證 Azure AD 應用程式的討論，請參閱以下內容。</span><span class="sxs-lookup"><span data-stu-id="093af-138">See below for a discussion on how to use a Client ID and Certificate instead of Client ID and Client Secret to authenticate the Azure AD application.</span></span>
> 
> 

## <span data-ttu-id="093af-139"><a id="appstart"></a>在應用程式啟動時擷取密碼</span><span class="sxs-lookup"><span data-stu-id="093af-139"><a id="appstart"></a>Retrieve the secret on Application Start</span></span>
<span data-ttu-id="093af-140">現在我們需要呼叫金鑰保存庫 API，並擷取密碼的程式碼。</span><span class="sxs-lookup"><span data-stu-id="093af-140">Now we need code to call the Key Vault API and retrieve the secret.</span></span> <span data-ttu-id="093af-141">下列程式碼可以放置在任何位置，只要在您需要使用它之前呼叫即可。</span><span class="sxs-lookup"><span data-stu-id="093af-141">The following code can be put anywhere as long as it is called before you need to use it.</span></span> <span data-ttu-id="093af-142">我已將程式碼放入 Global.asax 的應用程式啟動事件中，因此它在啟動時會執行一次，並讓密碼可在應用程式中使用。</span><span class="sxs-lookup"><span data-stu-id="093af-142">I have put this code in the Application Start event in the Global.asax so that it runs once on start and makes the secret available for the application.</span></span>

    //add these using statements
    using Microsoft.Azure.KeyVault;
    using System.Web.Configuration;

    // I put my GetToken method in a Utils class. Change for wherever you placed your method.
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

    var sec = await kv.GetSecretAsync(WebConfigurationManager.AppSettings["SecretUri"]);

    //I put a variable in a Utils class to hold the secret for general  application use.
    Utils.EncryptSecret = sec.Value;



## <span data-ttu-id="093af-143"><a id="portalsettings"></a>(選擇性) 在 Azure 入口網站中新增應用程式設定</span><span class="sxs-lookup"><span data-stu-id="093af-143"><a id="portalsettings"></a>Add App Settings in the Azure Portal (optional)</span></span>
<span data-ttu-id="093af-144">如果您已有 Azure Web Apps，您現在可以在 Azure 入口網站中為 AppSettings 新增實際值。</span><span class="sxs-lookup"><span data-stu-id="093af-144">If you have an Azure Web App you can now add the actual values for the AppSettings in the Azure Portal.</span></span> <span data-ttu-id="093af-145">如此一來，實際值將不會存在於 web.config 中，但會透過您有個別存取控制功能的入口網站受到保護。</span><span class="sxs-lookup"><span data-stu-id="093af-145">By doing this, the actual values will not be in the web.config but protected via the Portal where you have separate access control capabilities.</span></span> <span data-ttu-id="093af-146">這些值會被您在 web.config 中輸入的值取代。</span><span class="sxs-lookup"><span data-stu-id="093af-146">These values will be substituted for the values that you entered in your web.config.</span></span> <span data-ttu-id="093af-147">請確定名稱都相同。</span><span class="sxs-lookup"><span data-stu-id="093af-147">Make sure that the names are the same.</span></span>

![Azure 入口網站中顯示的應用程式設定][1]

## <a name="authenticate-with-a-certificate-instead-of-a-client-secret"></a><span data-ttu-id="093af-149">使用憑證 (而非用戶端密碼) 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="093af-149">Authenticate with a Certificate instead of a Client Secret</span></span>
<span data-ttu-id="093af-150">若要驗證 Azure AD 應用程式，另一種方式是使用用戶端識別碼和憑證 (而非用戶端識別碼和用戶端密碼)。</span><span class="sxs-lookup"><span data-stu-id="093af-150">Another way to authenticate an Azure AD application is by using a Client ID and a Certificate instead of a Client ID and Client Secret.</span></span> <span data-ttu-id="093af-151">以下是在 Azure Web 應用程式中使用憑證的步驟：</span><span class="sxs-lookup"><span data-stu-id="093af-151">Following are the steps to use a Certificate in an Azure Web App:</span></span>

1. <span data-ttu-id="093af-152">取得或建立憑證</span><span class="sxs-lookup"><span data-stu-id="093af-152">Get or Create a Certificate</span></span>
2. <span data-ttu-id="093af-153">將憑證與 Azure AD 應用程式產生關聯</span><span class="sxs-lookup"><span data-stu-id="093af-153">Associate the Certificate with an Azure AD application</span></span>
3. <span data-ttu-id="093af-154">將程式碼加入 Web 應用程式以使用憑證</span><span class="sxs-lookup"><span data-stu-id="093af-154">Add code to your Web App to use the Certificate</span></span>
4. <span data-ttu-id="093af-155">將憑證加入 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="093af-155">Add a Certificate to your Web App</span></span>

<span data-ttu-id="093af-156">**取得或建立憑證** 基於本文的目的，我們將測試憑證。</span><span class="sxs-lookup"><span data-stu-id="093af-156">**Get or Create a Certificate** For our purposes we will make a test certificate.</span></span> <span data-ttu-id="093af-157">以下幾個命令可讓您在開發人員命令提示字元中用來建立憑證。</span><span class="sxs-lookup"><span data-stu-id="093af-157">Here are a couple of commands that you can use in a Developer Command Prompt to create a certificate.</span></span> <span data-ttu-id="093af-158">變更您要建立憑證檔案的目錄位置。</span><span class="sxs-lookup"><span data-stu-id="093af-158">Change directory to where you want the cert files created.</span></span>  <span data-ttu-id="093af-159">此外，對於憑證的開始和結束日期，使用目前日期加上 1 年。</span><span class="sxs-lookup"><span data-stu-id="093af-159">Also, for the beginning and ending date of the certificate, use the current date plus 1 year.</span></span>

    makecert -sv mykey.pvk -n "cn=KVWebApp" KVWebApp.cer -b 03/07/2017 -e 03/07/2018 -r
    pvk2pfx -pvk mykey.pvk -spc KVWebApp.cer -pfx KVWebApp.pfx -po test123

<span data-ttu-id="093af-160">記下 .pfx 的結束日期和密碼 (在此範例中為：07/31/2016 和 test123)。</span><span class="sxs-lookup"><span data-stu-id="093af-160">Make note of the end date and the password for the .pfx (in this example: 07/31/2016 and test123).</span></span> <span data-ttu-id="093af-161">您將需要在下面使用這些資訊。</span><span class="sxs-lookup"><span data-stu-id="093af-161">You will need them below.</span></span>

<span data-ttu-id="093af-162">如需如何建立測試憑證的詳細資訊，請參閱 [做法：自行建立測試憑證](https://msdn.microsoft.com/library/ff699202.aspx)</span><span class="sxs-lookup"><span data-stu-id="093af-162">For more information on creating a test certificate, see [How to: Create Your Own Test Certificate](https://msdn.microsoft.com/library/ff699202.aspx)</span></span>

<span data-ttu-id="093af-163">**將憑證與 Azure AD 應用程式產生關聯** 有了憑證之後，您需要將其與 Azure AD 應用程式產生關聯。</span><span class="sxs-lookup"><span data-stu-id="093af-163">**Associate the Certificate with an Azure AD application** Now that you have a certificate, you need to associate it with an Azure AD application.</span></span> <span data-ttu-id="093af-164">目前「Azure 入口網站」並不支援此工作流程；您可以透過 PowerShell 來完成此工作流程。</span><span class="sxs-lookup"><span data-stu-id="093af-164">Presently, the Azure Portal does not support this workflow; this can be completed through PowerShell.</span></span> <span data-ttu-id="093af-165">請執行下列命令將憑證與 Azure AD 應用程式建立關聯：</span><span class="sxs-lookup"><span data-stu-id="093af-165">Run the following commands to assoicate the certificate with the Azure AD application:</span></span>

    $x509 = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2
    $x509.Import("C:\data\KVWebApp.cer")
    $credValue = [System.Convert]::ToBase64String($x509.GetRawCertData())

    # If you used different dates for makecert then adjust these values
    $now = [System.DateTime]::Now
    $yearfromnow = $now.AddYears(1)

    $adapp = New-AzureRmADApplication -DisplayName "KVWebApp" -HomePage "http://kvwebapp" -IdentifierUris "http://kvwebapp" -CertValue $credValue -StartDate $now -EndDate $yearfromnow

    $sp = New-AzureRmADServicePrincipal -ApplicationId $adapp.ApplicationId

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'contosokv' -ServicePrincipalName $sp.ServicePrincipalName -PermissionsToSecrets all -ResourceGroupName 'contosorg'

    # get the thumbprint to use in your app settings
    $x509.Thumbprint

<span data-ttu-id="093af-166">執行這些命令之後，您就可以在 Azure AD 中看到應用程式。</span><span class="sxs-lookup"><span data-stu-id="093af-166">After you have run these commands, you can see the application in Azure AD.</span></span> <span data-ttu-id="093af-167">搜尋時，在搜尋對話方塊中，請務必選取 [我公司所擁有的應用程式]，而不是 [我公司所使用的應用程式]。</span><span class="sxs-lookup"><span data-stu-id="093af-167">When searching, ensure you select "Applications my company owns" instead of "Applications my company uses" in the search dialog.</span></span>

<span data-ttu-id="093af-168">若要深入了解 Azure AD 應用程式物件和 ServicePrincipal 物件，請參閱[應用程式物件和服務主體物件](../active-directory/active-directory-application-objects.md)</span><span class="sxs-lookup"><span data-stu-id="093af-168">To learn more about Azure AD Application Objects and ServicePrincipal Objects, see [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md)</span></span>

<span data-ttu-id="093af-169">**將程式碼加入 Web 應用程式以使用憑證** 現在我們將程式碼加入您的 Web 應用程式，以存取憑證並使用其進行驗證。</span><span class="sxs-lookup"><span data-stu-id="093af-169">**Add code to your Web App to use the Certificate** Now we will add code to your Web App to access the cert and use it for authentication.</span></span>

<span data-ttu-id="093af-170">首先，使用程式碼存取憑證。</span><span class="sxs-lookup"><span data-stu-id="093af-170">First there is code to access the cert.</span></span>

    public static class CertificateHelper
    {
        public static X509Certificate2 FindCertificateByThumbprint(string findValue)
        {
            X509Store store = new X509Store(StoreName.My, StoreLocation.CurrentUser);
            try
            {
                store.Open(OpenFlags.ReadOnly);
                X509Certificate2Collection col = store.Certificates.Find(X509FindType.FindByThumbprint,
                    findValue, false); // Don't validate certs, since the test root isn't installed.
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


<span data-ttu-id="093af-171">請注意，StoreLocation 是 CurrentUser，而不是 LocalMachine。</span><span class="sxs-lookup"><span data-stu-id="093af-171">Note that the StoreLocation is CurrentUser instead of LocalMachine.</span></span> <span data-ttu-id="093af-172">另外，由於我們使用測試憑證，因此我們必須提供 "false" 憑證給 Find 方法。</span><span class="sxs-lookup"><span data-stu-id="093af-172">And that we are supplying 'false' to the Find method because we are using a test cert.</span></span>

<span data-ttu-id="093af-173">接著是使用 CertificateHelper 並建立驗證所需之 ClientAssertionCertificate 的程式碼。</span><span class="sxs-lookup"><span data-stu-id="093af-173">Next is code that uses the CertificateHelper and creates a ClientAssertionCertificate which is needed for authentication.</span></span>

    public static ClientAssertionCertificate AssertionCert { get; set; }

    public static void GetCert()
    {
        var clientAssertionCertPfx = CertificateHelper.FindCertificateByThumbprint(WebConfigurationManager.AppSettings["thumbprint"]);
        AssertionCert = new ClientAssertionCertificate(WebConfigurationManager.AppSettings["clientid"], clientAssertionCertPfx);
    }


<span data-ttu-id="093af-174">以下是取得存取 Token 的新程式碼。</span><span class="sxs-lookup"><span data-stu-id="093af-174">Here is the new code to get the access token.</span></span> <span data-ttu-id="093af-175">此程式碼將會取代上述的 GetToken 方法。</span><span class="sxs-lookup"><span data-stu-id="093af-175">This replaces the GetToken method above.</span></span> <span data-ttu-id="093af-176">為方便起見，我已將其改名。</span><span class="sxs-lookup"><span data-stu-id="093af-176">I have given it a different name for convenience.</span></span>

    public static async Task<string> GetAccessToken(string authority, string resource, string scope)
    {
        var context = new AuthenticationContext(authority, TokenCache.DefaultShared);
        var result = await context.AcquireTokenAsync(resource, AssertionCert);
        return result.AccessToken;
    }

<span data-ttu-id="093af-177">為了方便使用，我已將所有此類程式碼放入我的 Web 應用程式專案的公用程式類別。</span><span class="sxs-lookup"><span data-stu-id="093af-177">I have put all of this code into my Web App project's Utils class for ease of use.</span></span>

<span data-ttu-id="093af-178">最後的程式碼變更位在 Application_Start 方法中。</span><span class="sxs-lookup"><span data-stu-id="093af-178">The last code change is in the Application_Start method.</span></span> <span data-ttu-id="093af-179">首先，我們需要呼叫 GetCert() 方法以載入 ClientAssertionCertificate。</span><span class="sxs-lookup"><span data-stu-id="093af-179">First we need to call the GetCert() method to load the ClientAssertionCertificate.</span></span> <span data-ttu-id="093af-180">接著，在建立新的 KeyVaultClient 時，變更我們所提供的回呼方法。</span><span class="sxs-lookup"><span data-stu-id="093af-180">And then we change the callback method that we supply when creating a new KeyVaultClient.</span></span> <span data-ttu-id="093af-181">請注意，這會取代我們上面的程式碼。</span><span class="sxs-lookup"><span data-stu-id="093af-181">Note that this replaces the code that we had above.</span></span>

    Utils.GetCert();
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetAccessToken));


<span data-ttu-id="093af-182">**透過 Azure 入口網站將憑證加入 Web 應用程式** 將憑證加入您的 Web 應用程式的程序相當簡單，只需兩個步驟。</span><span class="sxs-lookup"><span data-stu-id="093af-182">**Add a Certificate to your Web App through the Azure Portal** Adding a Certificate to your Web App is a simple two-step process.</span></span> <span data-ttu-id="093af-183">首先，請移至 Azure 入口網站並瀏覽至您的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="093af-183">First, go to the Azure Portal and navigate to your Web App.</span></span> <span data-ttu-id="093af-184">在 Web 應用程式的 [設定] 刀鋒視窗中，按一下 [自訂網域及 SSL] 的項目。</span><span class="sxs-lookup"><span data-stu-id="093af-184">On the Settings blade for your Web App, click on the entry for "Custom domains and SSL".</span></span> <span data-ttu-id="093af-185">在開啟的刀鋒視窗中，您將能夠上傳先前建立的憑證 KVWebApp.pfx，並請確定您記得 pfx 的密碼。</span><span class="sxs-lookup"><span data-stu-id="093af-185">On the blade that opens you will be able to upload the Certificate that you created above, KVWebApp.pfx, make sure that you remember the password for the pfx.</span></span>

![在 Azure 入口網站中將憑證加入 Web 應用程式][2]

<span data-ttu-id="093af-187">您需要做的最後一件事，就是將應用程式設定新增至名為WEBSITE\_LOAD\_CERTIFICATES 與值為 * 的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="093af-187">The last thing that you need to do is to add an Application Setting to your Web App that has the name WEBSITE\_LOAD\_CERTIFICATES and a value of *.</span></span> <span data-ttu-id="093af-188">如此可確保載入所有憑證。</span><span class="sxs-lookup"><span data-stu-id="093af-188">This will ensure that all Certificates are loaded.</span></span> <span data-ttu-id="093af-189">如果您只想載入已上傳的憑證，則可輸入其憑證指紋的逗號分隔清單。</span><span class="sxs-lookup"><span data-stu-id="093af-189">If you wanted to load only the Certificates that you have uploaded, then you can enter a comma-separated list of their thumbprints.</span></span>

<span data-ttu-id="093af-190">若要深入了解將憑證加入 Web 應用程式的程序，請參閱 [在 Azure 網站應用程式中使用憑證](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)</span><span class="sxs-lookup"><span data-stu-id="093af-190">To learn more about adding a Certificate to a Web App, see [Using Certificates in Azure Websites Applications](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)</span></span>

<span data-ttu-id="093af-191">**將憑證加入至金鑰保存庫以做為密碼** (而非直接上傳您的憑證至 Web 應用程式服務)，您可以將其儲存在金鑰保存庫以做為密碼，並從此處加以部署。</span><span class="sxs-lookup"><span data-stu-id="093af-191">**Add a Certificate to Key Vault as a secret** Instead of uploading your certificate to the Web App service directly, you can store it in Key Vault as a secret and deploy it from there.</span></span> <span data-ttu-id="093af-192">這是兩個步驟的程序，以下的部落格文章有大概的描述： [透過金鑰保存庫部署 Azure Web 應用程式憑證](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)</span><span class="sxs-lookup"><span data-stu-id="093af-192">This is a two-step process that is outlined in the following blog post, [Deploying Azure Web App Certificate through Key Vault](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)</span></span>

## <span data-ttu-id="093af-193"><a id="next"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="093af-193"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="093af-194">如需程式設計參考，請參閱 [Azure 金鑰保存庫 C# 用戶端 API 參考](https://msdn.microsoft.com/library/azure/dn903628.aspx)。</span><span class="sxs-lookup"><span data-stu-id="093af-194">For programming references, see [Azure Key Vault C# Client API Reference](https://msdn.microsoft.com/library/azure/dn903628.aspx).</span></span>

<!--Image references-->
[1]: ./media/key-vault-use-from-web-application/PortalAppSettings.png
[2]: ./media/key-vault-use-from-web-application/PortalAddCertificate.png
