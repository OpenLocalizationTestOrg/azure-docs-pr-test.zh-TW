---
title: "使用端對端金鑰輪替和稽核設定 Azure 金鑰保存庫 | Microsoft Docs"
description: "使用此操作說明可協助您使用金鑰輪替和監視金鑰保存庫記錄檔來進行設定。"
services: key-vault
documentationcenter: 
author: swgriffith
manager: mbaldwin
tags: 
ms.assetid: 9cd7e15e-23b8-41c0-a10a-06e6207ed157
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: jodehavi;stgriffi
ms.openlocfilehash: 38c342802ed687985ac6f84f5a590a1a0dcc6c6a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-azure-key-vault-with-end-to-end-key-rotation-and-auditing"></a><span data-ttu-id="ddc32-103">使用端對端金鑰輪替和稽核設定 Azure 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="ddc32-103">Set up Azure Key Vault with end-to-end key rotation and auditing</span></span>
## <a name="introduction"></a><span data-ttu-id="ddc32-104">簡介</span><span class="sxs-lookup"><span data-stu-id="ddc32-104">Introduction</span></span>
<span data-ttu-id="ddc32-105">在建立金鑰保存庫之後，您可以開始使用該保存庫來儲存金鑰和密碼。</span><span class="sxs-lookup"><span data-stu-id="ddc32-105">After creating your key vault, you will be able to start using that vault to store your keys and secrets.</span></span> <span data-ttu-id="ddc32-106">應用程式不再需要保存金鑰或密碼，而是視需要從金鑰保存庫要求取得。</span><span class="sxs-lookup"><span data-stu-id="ddc32-106">Your applications no longer need to persist your keys or secrets, but rather will request them from the key vault as needed.</span></span> <span data-ttu-id="ddc32-107">這可讓您更新金鑰和密碼，而不會影響應用程式的行為，讓您有各種可能方式來管理金鑰和密碼。</span><span class="sxs-lookup"><span data-stu-id="ddc32-107">This allows you to update keys and secrets without affecting the behavior of your application, which opens up a breadth of possibilities around your key and secret management.</span></span>

<span data-ttu-id="ddc32-108">本文逐步解說使用 Azure 金鑰保存庫來儲存密碼的範例，在此案例中就是應用程式所存取的 Azure 儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="ddc32-108">This article walks through an example of using Azure Key Vault to store a secret, in this case an Azure Storage Account key that is accessed by an application.</span></span> <span data-ttu-id="ddc32-109">文中也會示範如何實作該儲存體帳戶金鑰的排程輪替。</span><span class="sxs-lookup"><span data-stu-id="ddc32-109">It also demonstrates implementation of a scheduled rotation of that storage account key.</span></span> <span data-ttu-id="ddc32-110">最後，本文會逐步示範如何監視金鑰保存庫稽核記錄檔，並在提出未預期的要求時發出警示。</span><span class="sxs-lookup"><span data-stu-id="ddc32-110">Finally, it walks through a demonstration of how to monitor the key vault audit logs and raise alerts when unexpected requests are made.</span></span>

> [!NOTE]
> <span data-ttu-id="ddc32-111">本教學課程並不打算詳細說明金鑰保存庫的初始設定。</span><span class="sxs-lookup"><span data-stu-id="ddc32-111">This tutorial is not intended to explain in detail the initial setup of your key vault.</span></span> <span data-ttu-id="ddc32-112">如需這方面的資訊，請參閱 [開始使用 Azure 金鑰保存庫](key-vault-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="ddc32-112">For this information, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span> <span data-ttu-id="ddc32-113">如需跨平台命令列介面的指示，請參閱[使用 CLI 管理金鑰保存庫](key-vault-manage-with-cli2.md)。</span><span class="sxs-lookup"><span data-stu-id="ddc32-113">For Cross-Platform Command-Line Interface instructions, see [Manage Key Vault using CLI](key-vault-manage-with-cli2.md).</span></span>
>
>

## <a name="set-up-key-vault"></a><span data-ttu-id="ddc32-114">設定金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="ddc32-114">Set up Key Vault</span></span>
<span data-ttu-id="ddc32-115">若要讓應用程式能夠從金鑰保存庫擷取密碼，您必須先建立此密碼，並上傳至保存庫。</span><span class="sxs-lookup"><span data-stu-id="ddc32-115">To enable an application to retrieve a secret from Key Vault, you must first create the secret and upload it to your vault.</span></span> <span data-ttu-id="ddc32-116">開始 Azure PowerShell 工作階段，並使用下列命令登入您的 Azure 帳戶，即可完成此作業：</span><span class="sxs-lookup"><span data-stu-id="ddc32-116">This can be accomplished by starting an Azure PowerShell session and signing in to your Azure account with the following command:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="ddc32-117">在快顯瀏覽器視窗中，輸入您的 Azure 帳戶使用者名稱與密碼。</span><span class="sxs-lookup"><span data-stu-id="ddc32-117">In the pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="ddc32-118">PowerShell 會取得與此帳戶相關聯的所有訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ddc32-118">PowerShell will get all the subscriptions that are associated with this account.</span></span> <span data-ttu-id="ddc32-119">PowerShell 使用預設第一個訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ddc32-119">PowerShell uses the first one by default.</span></span>

<span data-ttu-id="ddc32-120">如果您有多個訂用帳戶，您可能必須指定用來建立金鑰保存庫的那一個訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ddc32-120">If you have multiple subscriptions, you might have to specify the one that was used to create your key vault.</span></span> <span data-ttu-id="ddc32-121">輸入下列命令以查看您帳戶的訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="ddc32-121">Enter the following to see the subscriptions for your account:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="ddc32-122">若要指定與所要記錄之金鑰保存庫相關聯的訂用帳戶，請輸入：</span><span class="sxs-lookup"><span data-stu-id="ddc32-122">To specify the subscription that's associated with the key vault you will be logging, enter:</span></span>

```powershell
Set-AzureRmContext -SubscriptionId <subscriptionID>
```

<span data-ttu-id="ddc32-123">因為本文會示範如何將儲存體帳戶金鑰儲存為密碼，所以您必須取得該儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="ddc32-123">Because this article demonstrates storing a storage account key as a secret, you must get that storage account key.</span></span>

```powershell
Get-AzureRmStorageAccountKey -ResourceGroupName <resourceGroupName> -Name <storageAccountName>
```

<span data-ttu-id="ddc32-124">在擷取密碼之後，在此案例中就是儲存體帳戶金鑰，您必須將其轉換為安全字串，然後使用該值在金鑰保存庫中建立密碼。</span><span class="sxs-lookup"><span data-stu-id="ddc32-124">After retrieving your secret (in this case, your storage account key), you must convert that to a secure string and then create a secret with that value in your key vault.</span></span>

```powershell
$secretvalue = ConvertTo-SecureString <storageAccountKey> -AsPlainText -Force

Set-AzureKeyVaultSecret -VaultName <vaultName> -Name <secretName> -SecretValue $secretvalue
```
<span data-ttu-id="ddc32-125">接下來，取得您建立之密碼的 URI。</span><span class="sxs-lookup"><span data-stu-id="ddc32-125">Next, get the URI for the secret you created.</span></span> <span data-ttu-id="ddc32-126">在稍後的步驟中，當您呼叫金鑰保存庫以擷取密碼時將會用到。</span><span class="sxs-lookup"><span data-stu-id="ddc32-126">This is used in a later step when you call the key vault to retrieve your secret.</span></span> <span data-ttu-id="ddc32-127">執行下列 PowerShell 命令，並記下 ID 值，也就是密碼的 URI：</span><span class="sxs-lookup"><span data-stu-id="ddc32-127">Run the following PowerShell command and make note of the ID value, which is the secret URI:</span></span>

```powershell
Get-AzureKeyVaultSecret –VaultName <vaultName>
```

## <a name="set-up-the-application"></a><span data-ttu-id="ddc32-128">設定範例應用程式</span><span class="sxs-lookup"><span data-stu-id="ddc32-128">Set up the application</span></span>
<span data-ttu-id="ddc32-129">現在您已儲存密碼，您可以使用程式碼進行擷取並加以使用。</span><span class="sxs-lookup"><span data-stu-id="ddc32-129">Now that you have a secret stored, you can use code to retrieve and use it.</span></span> <span data-ttu-id="ddc32-130">需要執行幾個步驟才能達到這個目的。</span><span class="sxs-lookup"><span data-stu-id="ddc32-130">There are a few steps required to achieve this.</span></span> <span data-ttu-id="ddc32-131">第一個也是最重要的步驟是向 Azure Active Directory 註冊應用程式，然後讓金鑰保存庫知道應用程式的資訊，以便允許來自應用程式的要求。</span><span class="sxs-lookup"><span data-stu-id="ddc32-131">The first and most important step is registering your application with Azure Active Directory and then telling Key Vault your application information so that it can allow requests from your application.</span></span>

> [!NOTE]
> <span data-ttu-id="ddc32-132">應用程式必須建立在與金鑰保存庫相同的 Azure Active Directory 租用戶上。</span><span class="sxs-lookup"><span data-stu-id="ddc32-132">Your application must be created on the same Azure Active Directory tenant as your key vault.</span></span>
>
>

<span data-ttu-id="ddc32-133">開啟 Azure Active Directory 的 [應用程式] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="ddc32-133">Open the applications tab of Azure Active Directory.</span></span>

![在 Azure Active Directory 中開啟應用程式](./media/keyvault-keyrotation/AzureAD_Header.png)

<span data-ttu-id="ddc32-135">選擇 [新增] 將應用程式新增到 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="ddc32-135">Choose **ADD** to add an application to your Azure Active Directory.</span></span>

![選擇 [新增]](./media/keyvault-keyrotation/Azure_AD_AddApp.png)

<span data-ttu-id="ddc32-137">讓應用程式類型保持使用 [Web 應用程式和/或 WEB API]，然後為應用程式提供名稱。</span><span class="sxs-lookup"><span data-stu-id="ddc32-137">Leave the application type as **WEB APPLICATION AND/OR WEB API** and give your application a name.</span></span>

![為應用程式命名](./media/keyvault-keyrotation/AzureAD_NewApp1.png)

<span data-ttu-id="ddc32-139">為應用程式提供 [登入 URL] 和 [應用程式識別碼 URI]。</span><span class="sxs-lookup"><span data-stu-id="ddc32-139">Give your application a **SIGN-ON URL** and an **APP ID URI**.</span></span> <span data-ttu-id="ddc32-140">這些可以是任何想用於此示範的值，並可在稍後視需要加以變更。</span><span class="sxs-lookup"><span data-stu-id="ddc32-140">These can be anything you want for this demo, and they can be changed later if needed.</span></span>

![提供必要的 URI](./media/keyvault-keyrotation/AzureAD_NewApp2.png)

<span data-ttu-id="ddc32-142">在應用程式新增至 Azure Active Directory 之後，您將會進入應用程式頁面。</span><span class="sxs-lookup"><span data-stu-id="ddc32-142">After the application is added to Azure Active Directory, you will be brought into the application page.</span></span> <span data-ttu-id="ddc32-143">按一下 [設定] 索引標籤，然後尋找並複製 [用戶端識別碼] 值。</span><span class="sxs-lookup"><span data-stu-id="ddc32-143">Click the **Configure** tab and then find and copy the **Client ID** value.</span></span> <span data-ttu-id="ddc32-144">記下用戶端識別碼以供後續步驟使用。</span><span class="sxs-lookup"><span data-stu-id="ddc32-144">Make note of the client ID for later steps.</span></span>

<span data-ttu-id="ddc32-145">接下來，產生金鑰，以便應用程式與 Azure Active Directory 互動。</span><span class="sxs-lookup"><span data-stu-id="ddc32-145">Next, generate a key for your application so it can interact with your Azure Active Directory.</span></span> <span data-ttu-id="ddc32-146">您可以在 [設定] 索引標籤的 [金鑰] 區段底下建立此金鑰。</span><span class="sxs-lookup"><span data-stu-id="ddc32-146">You can create this under the **Keys** section in the **Configuration** tab.</span></span> <span data-ttu-id="ddc32-147">記下從 Azure Active Directory 應用程式新產生的金鑰，以供後續步驟使用。</span><span class="sxs-lookup"><span data-stu-id="ddc32-147">Make note of the newly generated key from your Azure Active Directory application for use in a later step.</span></span>

![Azure Active Directory 應用程式金鑰](./media/keyvault-keyrotation/Azure_AD_AppKeys.png)

<span data-ttu-id="ddc32-149">在建立任何從應用程式到金鑰保存庫的呼叫之前，您必須讓金鑰保存庫知道應用程式及其權限。</span><span class="sxs-lookup"><span data-stu-id="ddc32-149">Before establishing any calls from your application into the key vault, you must tell the key vault about your application and its permissions.</span></span> <span data-ttu-id="ddc32-150">下列命令會從 Azure Active Directory 應用程式取得保存庫名稱和用戶端識別碼，並授與 **Get** 權限給應用程式的金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="ddc32-150">The following command takes the vault name and the client ID from your Azure Active Directory app and grants **Get** access to your key vault for the application.</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <clientIDfromAzureAD> -PermissionsToSecrets Get
```

<span data-ttu-id="ddc32-151">此時，您已準備好開始建置應用程式呼叫。</span><span class="sxs-lookup"><span data-stu-id="ddc32-151">At this point, you are ready to start building your application calls.</span></span> <span data-ttu-id="ddc32-152">在應用程式中，您必須先安裝所需的 NuGet 套件，以便與 Azure 金鑰保存庫和 Azure Active Directory 互動。</span><span class="sxs-lookup"><span data-stu-id="ddc32-152">In your application, you must install the NuGet packages required to interact with Azure Key Vault and Azure Active Directory.</span></span> <span data-ttu-id="ddc32-153">從 Visual Studio Package Manager Console 輸入下列命令。</span><span class="sxs-lookup"><span data-stu-id="ddc32-153">From the Visual Studio Package Manager console, enter the following commands.</span></span> <span data-ttu-id="ddc32-154">在本文撰寫的當下，Azure Active Directory 套件的最新版本是 3.10.305231913，因此請確認最新版本並據以更新。</span><span class="sxs-lookup"><span data-stu-id="ddc32-154">At the writing of this article, the current version of the Azure Active Directory package is 3.10.305231913, so you might want to confirm the latest version and update accordingly.</span></span>

```powershell
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 3.10.305231913

Install-Package Microsoft.Azure.KeyVault
```

<span data-ttu-id="ddc32-155">在應用程式程式碼中，建立類別以保有Azure Active Directory 驗證的方法。</span><span class="sxs-lookup"><span data-stu-id="ddc32-155">In your application code, create a class to hold the method for your Azure Active Directory authentication.</span></span> <span data-ttu-id="ddc32-156">在此範例中，該類別稱為 **Utils**。</span><span class="sxs-lookup"><span data-stu-id="ddc32-156">In this example, that class is called **Utils**.</span></span> <span data-ttu-id="ddc32-157">加入下列 using 陳述式：</span><span class="sxs-lookup"><span data-stu-id="ddc32-157">Add the following using statement:</span></span>

```csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="ddc32-158">接著，新增下列方法，以從 Azure Active Directory 擷取 JWT 權杖。</span><span class="sxs-lookup"><span data-stu-id="ddc32-158">Next, add the following method to retrieve the JWT token from Azure Active Directory.</span></span> <span data-ttu-id="ddc32-159">為了能夠維護，請將硬式編碼的字串值移動至 Web 或應用程式組態。</span><span class="sxs-lookup"><span data-stu-id="ddc32-159">For maintainability, you may want to move the hard-coded string values into your web or application configuration.</span></span>

```csharp
public async static Task<string> GetToken(string authority, string resource, string scope)
{
    var authContext = new AuthenticationContext(authority);

    ClientCredential clientCred = new ClientCredential("<AzureADApplicationClientID>","<AzureADApplicationClientKey>");

    AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

    if (result == null)

    throw new InvalidOperationException("Failed to obtain the JWT token");

    return result.AccessToken;
}
```

<span data-ttu-id="ddc32-160">新增必要的程式碼，以呼叫金鑰保存庫並擷取密碼值。</span><span class="sxs-lookup"><span data-stu-id="ddc32-160">Add the necessary code to call Key Vault and retrieve your secret value.</span></span> <span data-ttu-id="ddc32-161">首先，您必須加入下列 using 陳述式：</span><span class="sxs-lookup"><span data-stu-id="ddc32-161">First you must add the following using statement:</span></span>

```csharp
using Microsoft.Azure.KeyVault;
```

<span data-ttu-id="ddc32-162">新增方法呼叫來叫用金鑰保存庫，並擷取密碼。</span><span class="sxs-lookup"><span data-stu-id="ddc32-162">Add the method calls to invoke Key Vault and retrieve your secret.</span></span> <span data-ttu-id="ddc32-163">在這個方法中，您會提供您在先前步驟中儲存的密碼 URI。</span><span class="sxs-lookup"><span data-stu-id="ddc32-163">In this method, you provide the secret URI that you saved in a previous step.</span></span> <span data-ttu-id="ddc32-164">請注意來自先前建立的 **Utils** 類別的 **GetToken** 方法的使用方式。</span><span class="sxs-lookup"><span data-stu-id="ddc32-164">Note the use of the **GetToken** method from the **Utils** class created previously.</span></span>

```csharp
var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

var sec = kv.GetSecretAsync(<SecretID>).Result.Value;
```

<span data-ttu-id="ddc32-165">當您執行應用程式時，您現在應該向 Azure Active Directory 進行驗證，然後從 Azure 金鑰保存庫中擷取密碼值。</span><span class="sxs-lookup"><span data-stu-id="ddc32-165">When you run your application, you should now be authenticating to Azure Active Directory and then retrieving your secret value from Azure Key Vault.</span></span>

## <a name="key-rotation-using-azure-automation"></a><span data-ttu-id="ddc32-166">使用 Azure 自動化的金鑰輪替</span><span class="sxs-lookup"><span data-stu-id="ddc32-166">Key rotation using Azure Automation</span></span>
<span data-ttu-id="ddc32-167">針對儲存為 Azure 金鑰保存庫密碼的值，有各種選項可用來實作其輪替策略。</span><span class="sxs-lookup"><span data-stu-id="ddc32-167">There are various options for implementing a rotation strategy for values you store as Azure Key Vault secrets.</span></span> <span data-ttu-id="ddc32-168">密碼可以在進行手動程序時輪替、使用 API 呼叫以程式設計的方式輪替，或是透過自動化指令碼來輪替。</span><span class="sxs-lookup"><span data-stu-id="ddc32-168">Secrets can be rotated as part of a manual process, they may be rotated programmatically by using API calls, or they may be rotated by way of an Automation script.</span></span> <span data-ttu-id="ddc32-169">基於本文的目的，您將會使用 Azure PowerShell 並結合 Azure 自動化，以變更 Azure 儲存體帳戶存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="ddc32-169">For the purposes of this article, you will be using Azure PowerShell combined with Azure Automation to change an Azure Storage Account access key.</span></span> <span data-ttu-id="ddc32-170">然後您將使用這個新金鑰來更新金鑰保存庫密碼。</span><span class="sxs-lookup"><span data-stu-id="ddc32-170">You will then update a key vault secret with that new key.</span></span>

<span data-ttu-id="ddc32-171">若要允許 Azure 自動化在金鑰保存庫中設定密碼值，您必須取得建立 Azure 自動化執行個體時所建立、名為 'AzureRunAsConnection' 的連線的用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="ddc32-171">To allow Azure Automation to set secret values in your key vault, you must get the client ID for the connection named AzureRunAsConnection, which was created when you established your Azure Automation instance.</span></span> <span data-ttu-id="ddc32-172">從 Azure 自動化執行個體選擇 [資產]，即可尋找這個識別碼。</span><span class="sxs-lookup"><span data-stu-id="ddc32-172">You can find this ID by choosing **Assets** from your Azure Automation instance.</span></span> <span data-ttu-id="ddc32-173">在該處選擇 [連線]，然後選取 [AzureRunAsConnection] 服務主體。</span><span class="sxs-lookup"><span data-stu-id="ddc32-173">From there, you choose **Connections** and then select the **AzureRunAsConnection** service principle.</span></span> <span data-ttu-id="ddc32-174">請記下 [應用程式識別碼]。</span><span class="sxs-lookup"><span data-stu-id="ddc32-174">Take note of the **Application ID**.</span></span>

![Azure 自動化用戶端識別碼](./media/keyvault-keyrotation/Azure_Automation_ClientID.png)

<span data-ttu-id="ddc32-176">在 [資產] 中，選擇 [模組]。</span><span class="sxs-lookup"><span data-stu-id="ddc32-176">In **Assets**, choose **Modules**.</span></span> <span data-ttu-id="ddc32-177">在 [模組] 中選取 [資源庫]，然後搜尋並 [匯入] 下列每個模組的更新版本：</span><span class="sxs-lookup"><span data-stu-id="ddc32-177">From **Modules**, select **Gallery**, and then search for and **Import** updated versions of each of the following modules:</span></span>

    Azure
    Azure.Storage
    AzureRM.Profile
    AzureRM.KeyVault
    AzureRM.Automation
    AzureRM.Storage


> [!NOTE]
> <span data-ttu-id="ddc32-178">在撰寫本文的當時，就下列指令碼而言，需要更新的只有先前所述的模組。</span><span class="sxs-lookup"><span data-stu-id="ddc32-178">At the writing of this article, only the previously noted modules needed to be updated for the following script.</span></span> <span data-ttu-id="ddc32-179">如果您發現自動化作業失敗，請確認您已匯入所有必要的模組及其相依項目。</span><span class="sxs-lookup"><span data-stu-id="ddc32-179">If you find that your automation job is failing, confirm that you have imported all necessary modules and their dependencies.</span></span>
>
>

<span data-ttu-id="ddc32-180">擷取 Azure 自動化連線的應用程式識別碼之後，您必須讓金鑰保存庫知道，此應用程式有權更新保存庫中的密碼。</span><span class="sxs-lookup"><span data-stu-id="ddc32-180">After you have retrieved the application ID for your Azure Automation connection, you must tell your key vault that this application has access to update secrets in your vault.</span></span> <span data-ttu-id="ddc32-181">這可以使用下列 PowerShell 命令來完成：</span><span class="sxs-lookup"><span data-stu-id="ddc32-181">This can be accomplished with the following PowerShell command:</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <applicationIDfromAzureAutomation> -PermissionsToSecrets Set
```

<span data-ttu-id="ddc32-182">接下來，選取 Azure 自動化執行個體底下的 [Runbook] 資源，然後選取 [新增 Runbook]。</span><span class="sxs-lookup"><span data-stu-id="ddc32-182">Next, select **Runbooks** under your Azure Automation instance, and then select **Add a Runbook**.</span></span> <span data-ttu-id="ddc32-183">選取 [快速建立] 。</span><span class="sxs-lookup"><span data-stu-id="ddc32-183">Select **Quick Create**.</span></span> <span data-ttu-id="ddc32-184">為 Runbook 命名，然後選取 [PowerShell] 做為 Runbook 類型。</span><span class="sxs-lookup"><span data-stu-id="ddc32-184">Name your runbook and select **PowerShell** as the runbook type.</span></span> <span data-ttu-id="ddc32-185">您可選擇新增說明。</span><span class="sxs-lookup"><span data-stu-id="ddc32-185">You have the option to add a description.</span></span> <span data-ttu-id="ddc32-186">最後，按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="ddc32-186">Finally, click **Create**.</span></span>

![建立 Runbook](./media/keyvault-keyrotation/Create_Runbook.png)

<span data-ttu-id="ddc32-188">在新的 Runbook 的編輯器窗格中，貼上下列 PowerShell 指令碼：</span><span class="sxs-lookup"><span data-stu-id="ddc32-188">Paste the following PowerShell script in the editor pane for your new runbook:</span></span>

```powershell
$connectionName = "AzureRunAsConnection"
try
{
    # Get the connection "AzureRunAsConnection "
    $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

    "Logging in to Azure..."
    Add-AzureRmAccount `
        -ServicePrincipal `
        -TenantId $servicePrincipalConnection.TenantId `
        -ApplicationId $servicePrincipalConnection.ApplicationId `
        -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
    "Login complete."
}
catch {
    if (!$servicePrincipalConnection)
    {
        $ErrorMessage = "Connection $connectionName not found."
        throw $ErrorMessage
    } else{
        Write-Error -Message $_.Exception
        throw $_.Exception
    }
}

#Optionally you may set the following as parameters
$StorageAccountName = <storageAccountName>
$RGName = <storageAccountResourceGroupName>
$VaultName = <keyVaultName>
$SecretName = <keyVaultSecretName>

#Key name. For example key1 or key2 for the storage account
New-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName -KeyName "key2" -Verbose
$SAKeys = Get-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName

$secretvalue = ConvertTo-SecureString $SAKeys[1].Value -AsPlainText -Force

$secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secretvalue
```

<span data-ttu-id="ddc32-189">在編輯器窗格中，選擇 [測試窗格] 來測試指令碼。</span><span class="sxs-lookup"><span data-stu-id="ddc32-189">From the editor pane, choose **Test pane** to test your script.</span></span> <span data-ttu-id="ddc32-190">一旦指令碼在執行時不會發生錯誤，您可以選取 [發佈] 選項，然後回到 Runbook 的組態窗格套用 Runbook 的排程。</span><span class="sxs-lookup"><span data-stu-id="ddc32-190">Once the script is running without error, you can select **Publish**, and then you can apply a schedule for the runbook back in the runbook configuration pane.</span></span>

## <a name="key-vault-auditing-pipeline"></a><span data-ttu-id="ddc32-191">金鑰保存庫稽核管線</span><span class="sxs-lookup"><span data-stu-id="ddc32-191">Key Vault auditing pipeline</span></span>
<span data-ttu-id="ddc32-192">當您設定金鑰保存庫時，您可以開啟稽核功能，以收集對金鑰保存庫提出的存取要求的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="ddc32-192">When you set up a key vault, you can turn on auditing to collect logs on access requests made to the key vault.</span></span> <span data-ttu-id="ddc32-193">這些記錄檔會儲存在指定的 Azure 儲存體帳戶中，以供提取、監視和分析。</span><span class="sxs-lookup"><span data-stu-id="ddc32-193">These logs are stored in a designated Azure Storage account and can be pulled out, monitored, and analyzed.</span></span> <span data-ttu-id="ddc32-194">下列案例使用 Azure Functions、Azure Logic Apps 和金鑰保存庫稽核記錄檔來建立管線，以在與 Web 應用程式的應用程式識別碼相符的應用程式擷取保存庫中的密碼時傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="ddc32-194">The following scenario uses Azure functions, Azure logic apps, and key vault audit logs to create a pipeline to send an email when an app that does match the app ID of the web app retrieves secrets from the vault.</span></span>

<span data-ttu-id="ddc32-195">首先，您必須在金鑰保存庫上啟用記錄功能。</span><span class="sxs-lookup"><span data-stu-id="ddc32-195">First, you must enable logging on your key vault.</span></span> <span data-ttu-id="ddc32-196">這可以透過下列 PowerShell 命令來完成 (在 [key-vault-logging](key-vault-logging.md) 可以看到完整的詳細資料)：</span><span class="sxs-lookup"><span data-stu-id="ddc32-196">This can be done via the following PowerShell commands (full details can be seen at [key-vault-logging](key-vault-logging.md)):</span></span>

```powershell
$sa = New-AzureRmStorageAccount -ResourceGroupName <resourceGroupName> -Name <storageAccountName> -Type Standard\_LRS -Location 'East US'
$kv = Get-AzureRmKeyVault -VaultName '<vaultName>'
Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent
```

<span data-ttu-id="ddc32-197">啟用此功能後，就會開始將稽核記錄檔收集到指定的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ddc32-197">After this is enabled, audit logs start collecting into the designated storage account.</span></span> <span data-ttu-id="ddc32-198">這些記錄檔包含有關金鑰保存庫存取方式、時間和存取者的事件。</span><span class="sxs-lookup"><span data-stu-id="ddc32-198">These logs contain events about how and when your key vaults are accessed, and by whom.</span></span>

> [!NOTE]
> <span data-ttu-id="ddc32-199">在金鑰保存庫作業 10 分鐘後，您就可以存取記錄資訊。</span><span class="sxs-lookup"><span data-stu-id="ddc32-199">You can access your logging information 10 minutes after the key vault operation.</span></span> <span data-ttu-id="ddc32-200">但通常不用這麼久。</span><span class="sxs-lookup"><span data-stu-id="ddc32-200">It will usually be quicker than this.</span></span>
>
>

<span data-ttu-id="ddc32-201">下一步是 [建立 Azure 服務匯流排佇列](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md)。</span><span class="sxs-lookup"><span data-stu-id="ddc32-201">The next step is to [create an Azure Service Bus queue](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span> <span data-ttu-id="ddc32-202">這是金鑰保存庫稽核記錄檔的推送位置。</span><span class="sxs-lookup"><span data-stu-id="ddc32-202">This is where key vault audit logs are pushed.</span></span> <span data-ttu-id="ddc32-203">當稽核記錄檔訊息位於佇列時，邏輯應用程式可加以挑選並採取行動。</span><span class="sxs-lookup"><span data-stu-id="ddc32-203">When the audit log messages are in the queue, the logic app picks them up and acts on them.</span></span> <span data-ttu-id="ddc32-204">使用下列步驟建立服務匯流排︰</span><span class="sxs-lookup"><span data-stu-id="ddc32-204">Create a service bus with the following steps:</span></span>

1. <span data-ttu-id="ddc32-205">建立服務匯流排命名空間 (如果您已經有一個想要用於此作業的命名空間，請跳至步驟 2)。</span><span class="sxs-lookup"><span data-stu-id="ddc32-205">Create a Service Bus namespace (if you already have one that you want to use for this, skip to Step 2).</span></span>
2. <span data-ttu-id="ddc32-206">在 Azure 入口網站中瀏覽至服務匯流排，然後選取要在其中建立佇列的命名空間。</span><span class="sxs-lookup"><span data-stu-id="ddc32-206">Browse to the service bus in the Azure portal and select the namespace you want to create the queue in.</span></span>
3. <span data-ttu-id="ddc32-207">選取 [新增]，然後選擇 [服務匯流排] -> [佇列]，並輸入必要詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ddc32-207">Select **New** and choose **Service Bus > Queue** and enter the required details.</span></span>
4. <span data-ttu-id="ddc32-208">選擇命名空間，然後按一下 [連接資訊]，以選取服務匯流排連接資訊。</span><span class="sxs-lookup"><span data-stu-id="ddc32-208">Select the Service Bus connection information by choosing the namespace and clicking **Connection Information**.</span></span> <span data-ttu-id="ddc32-209">下一個區段需要此資訊。</span><span class="sxs-lookup"><span data-stu-id="ddc32-209">You will need this information for the next section.</span></span>

<span data-ttu-id="ddc32-210">接下來，[建立 Azure 函式](../azure-functions/functions-create-first-azure-function.md) 以輪詢儲存體帳戶中的金鑰保存庫記錄，並挑選新的事件。</span><span class="sxs-lookup"><span data-stu-id="ddc32-210">Next, [create an Azure function](../azure-functions/functions-create-first-azure-function.md) to poll key vault logs within the storage account and pick up new events.</span></span> <span data-ttu-id="ddc32-211">這是會依排程觸發的函式。</span><span class="sxs-lookup"><span data-stu-id="ddc32-211">This will be a function that is triggered on a schedule.</span></span>

<span data-ttu-id="ddc32-212">若要建立 Azure 函式，請在 Azure 入口網站中選擇 [新增] -> [函式應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ddc32-212">To create an Azure function, choose **New > Function App** in the Azure portal.</span></span> <span data-ttu-id="ddc32-213">在建立期間，您可以使用現有的主控方案，或建立新的方案。</span><span class="sxs-lookup"><span data-stu-id="ddc32-213">During creation, you can use an existing hosting plan or create a new one.</span></span> <span data-ttu-id="ddc32-214">您也可以選擇動態主控。</span><span class="sxs-lookup"><span data-stu-id="ddc32-214">You could also opt for dynamic hosting.</span></span> <span data-ttu-id="ddc32-215">如需函式主控選項的詳細資訊，請參閱[如何調整 Azure Functions](../azure-functions/functions-scale.md)。</span><span class="sxs-lookup"><span data-stu-id="ddc32-215">More details on Function hosting options can be found at [How to scale Azure Functions](../azure-functions/functions-scale.md).</span></span>

<span data-ttu-id="ddc32-216">建立 Azure 函式後，請瀏覽到該函式並選擇計時器函式和 C\#。</span><span class="sxs-lookup"><span data-stu-id="ddc32-216">When the Azure function is created, navigate to it and choose a timer function and C\#.</span></span> <span data-ttu-id="ddc32-217">然後按一下 [建立此函式]。</span><span class="sxs-lookup"><span data-stu-id="ddc32-217">Then click **Create this function**.</span></span>

![Azure Functions 啟動刀鋒視窗](./media/keyvault-keyrotation/Azure_Functions_Start.png)

<span data-ttu-id="ddc32-219">在 [開發] 索引標籤上，以下列內容取代 run.csx 程式碼︰</span><span class="sxs-lookup"><span data-stu-id="ddc32-219">On the **Develop** tab, replace the run.csx code with the following:</span></span>

```csharp
#r "Newtonsoft.Json"

using System;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Blob;
using Microsoft.ServiceBus.Messaging;
using System.Text;

public static void Run(TimerInfo myTimer, TextReader inputBlob, TextWriter outputBlob, TraceWriter log)
{
    log.Info("Starting");

    CloudStorageAccount sourceStorageAccount = new CloudStorageAccount(new StorageCredentials("<STORAGE_ACCOUNT_NAME>", "<STORAGE_ACCOUNT_KEY>"), true);

    CloudBlobClient sourceCloudBlobClient = sourceStorageAccount.CreateCloudBlobClient();

    var connectionString = "<SERVICE_BUS_CONNECTION_STRING>";
    var queueName = "<SERVICE_BUS_QUEUE_NAME>";

    var sbClient = QueueClient.CreateFromConnectionString(connectionString, queueName);

    DateTime dtPrev = DateTime.UtcNow;
    if(inputBlob != null)
    {
        var txt = inputBlob.ReadToEnd();

        if(!string.IsNullOrEmpty(txt))
        {
            dtPrev = DateTime.Parse(txt);
            log.Verbose($"SyncPoint: {dtPrev.ToString("O")}");
        }
        else
        {
            dtPrev = DateTime.UtcNow;
            log.Verbose($"Sync point file didnt have a date. Setting to now.");
        }
    }

    var now = DateTime.UtcNow;

    string blobPrefix = "insights-logs-auditevent/resourceId=/SUBSCRIPTIONS/<SUBSCRIPTION_ID>/RESOURCEGROUPS/<RESOURCE_GROUP_NAME>/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/<KEY_VAULT_NAME>/y=" + now.Year +"/m="+now.Month.ToString("D2")+"/d="+ (now.Day).ToString("D2")+"/h="+(now.Hour).ToString("D2")+"/m=00/";

    log.Info($"Scanning:  {blobPrefix}");

    IEnumerable<IListBlobItem> blobs = sourceCloudBlobClient.ListBlobs(blobPrefix, true);

    log.Info($"found {blobs.Count()} blobs");

    foreach(var item in blobs)
    {
        if (item is CloudBlockBlob)
        {
            CloudBlockBlob blockBlob = (CloudBlockBlob)item;

            log.Info($"Syncing: {item.Uri}");

            string sharedAccessUri = GetContainerSasUri(blockBlob);

            CloudBlockBlob sourceBlob = new CloudBlockBlob(new Uri(sharedAccessUri));

            string text;
            using (var memoryStream = new MemoryStream())
            {
                sourceBlob.DownloadToStream(memoryStream);
                text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
            }

            dynamic dynJson = JsonConvert.DeserializeObject(text);

            //required to order by time as they may not be in the file
            var results = ((IEnumerable<dynamic>) dynJson.records).OrderBy(p => p.time);

            foreach (var jsonItem in results)
            {
                DateTime dt = Convert.ToDateTime(jsonItem.time);

                if(dt>dtPrev){
                    log.Info($"{jsonItem.ToString()}");

                    var payloadStream = new MemoryStream(Encoding.UTF8.GetBytes(jsonItem.ToString()));
                    //When sending to ServiceBus, use the payloadStream and set keeporiginal to true
                    var message = new BrokeredMessage(payloadStream, true);
                    sbClient.Send(message);
                    dtPrev = dt;
                }
            }
        }
    }
    outputBlob.Write(dtPrev.ToString("o"));
}

static string GetContainerSasUri(CloudBlockBlob blob)
{
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();

    sasConstraints.SharedAccessStartTime = DateTime.UtcNow.AddMinutes(-5);
    sasConstraints.SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.Read;

    //Generate the shared access signature on the container, setting the constraints directly on the signature.
    string sasBlobToken = blob.GetSharedAccessSignature(sasConstraints);

    //Return the URI string for the container, including the SAS token.
    return blob.Uri + sasBlobToken;
}
```


> [!NOTE]
> <span data-ttu-id="ddc32-220">請務必取代上述程式碼中的變數，以指向「金鑰保存庫」記錄的寫入儲存體帳戶、稍早建立的服務匯流排，以及指向金鑰保存庫儲存體記錄的特定路徑。</span><span class="sxs-lookup"><span data-stu-id="ddc32-220">Make sure to replace the variables in the preceding code to point to your storage account where the key vault logs are written, the service bus you created earlier, and the specific path to the key vault storage logs.</span></span>
>
>

<span data-ttu-id="ddc32-221">此函式會挑選金鑰保存庫記錄所寫入到的儲存體帳戶中最新的記錄檔、取得來自該檔案的最新事件，並推送到服務匯流排佇列。</span><span class="sxs-lookup"><span data-stu-id="ddc32-221">The function picks up the latest log file from the storage account where the key vault logs are written, grabs the latest events from that file, and pushes them to a Service Bus queue.</span></span> <span data-ttu-id="ddc32-222">由於單一檔案可以有多個事件，所以您應該建立函式也會查看的 sync.txt 檔案，以判斷所挑選的最後一個事件的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="ddc32-222">Since a single file could have multiple events, you should create a sync.txt file that the function also looks at to determine the time stamp of the last event that was picked up.</span></span> <span data-ttu-id="ddc32-223">這可確保您不會多次推送相同的事件。</span><span class="sxs-lookup"><span data-stu-id="ddc32-223">This ensures that you don't push the same event multiple times.</span></span> <span data-ttu-id="ddc32-224">這個 sync.txt 檔案包含最後發生之事件的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="ddc32-224">This sync.txt file contains a timestamp for the last encountered event.</span></span> <span data-ttu-id="ddc32-225">記錄檔在載入時，必須根據時間戳記加以排序，以確保記錄檔會以正確順序排序。</span><span class="sxs-lookup"><span data-stu-id="ddc32-225">The logs, when loaded, have to be sorted based on the timestamp to ensure they are ordered correctly.</span></span>

<span data-ttu-id="ddc32-226">在這個函式中，我們會參考 Azure Functions 中數個必非立即可用的額外程式庫。</span><span class="sxs-lookup"><span data-stu-id="ddc32-226">For this function, we reference a couple of additional libraries that are not available out of the box in Azure Functions.</span></span> <span data-ttu-id="ddc32-227">若要加入這些程式庫，我們需要 Azure Functions 才能使用 NuGet 提取它們。</span><span class="sxs-lookup"><span data-stu-id="ddc32-227">To include these, we need Azure Functions to pull them using NuGet.</span></span> <span data-ttu-id="ddc32-228">選擇 [檢視檔案] 選項。</span><span class="sxs-lookup"><span data-stu-id="ddc32-228">Choose the **View Files** option.</span></span>

![檢視檔案選項](./media/keyvault-keyrotation/Azure_Functions_ViewFiles.png)

<span data-ttu-id="ddc32-230">然後使用下列內容新增名為 project.json 的檔案︰</span><span class="sxs-lookup"><span data-stu-id="ddc32-230">And add a file called project.json with following content:</span></span>

```json
    {
      "frameworks": {
        "net46":{
          "dependencies": {
                "WindowsAzure.Storage": "7.0.0",
                "WindowsAzure.ServiceBus":"3.2.2"
          }
        }
       }
    }
```
<span data-ttu-id="ddc32-231">在 [儲存] 時，Azure Functions 會下載所需的二進位檔。</span><span class="sxs-lookup"><span data-stu-id="ddc32-231">Upon **Save**, Azure Functions will download the required binaries.</span></span>

<span data-ttu-id="ddc32-232">切換至 [整合]  索引標籤，然後為計時器參數提供有意義的名稱以在函式內使用。</span><span class="sxs-lookup"><span data-stu-id="ddc32-232">Switch to the **Integrate** tab and give the timer parameter a meaningful name to use within the function.</span></span> <span data-ttu-id="ddc32-233">前面的程式碼預期計時器名稱為 myTimer。</span><span class="sxs-lookup"><span data-stu-id="ddc32-233">In the preceding code, it expects the timer to be called *myTimer*.</span></span> <span data-ttu-id="ddc32-234">依下列方式為計時器指定 [CRON 運算式](../app-service-web/web-sites-create-web-jobs.md#CreateScheduledCRON)︰0 \* \* \* \* \*，這會讓函式每分鐘執行一次。</span><span class="sxs-lookup"><span data-stu-id="ddc32-234">Specify a [CRON expression](../app-service-web/web-sites-create-web-jobs.md#CreateScheduledCRON) as follows: 0 \* \* \* \* \* for the timer that will cause the function to run once a minute.</span></span>

<span data-ttu-id="ddc32-235">在同一個 [整合] 索引標籤上，新增 [Azure Blob 儲存體] 類型的輸入。</span><span class="sxs-lookup"><span data-stu-id="ddc32-235">On the same **Integrate** tab, add an input of the type **Azure Blob Storage**.</span></span> <span data-ttu-id="ddc32-236">這會指向包含函式所查看之最後一個事件的時間戳記的 sync.txt 檔案。</span><span class="sxs-lookup"><span data-stu-id="ddc32-236">This will point to the sync.txt file that contains the timestamp of the last event looked at by the function.</span></span> <span data-ttu-id="ddc32-237">這會在函式中依參數名稱提供。</span><span class="sxs-lookup"><span data-stu-id="ddc32-237">This will be available within the function by the parameter name.</span></span> <span data-ttu-id="ddc32-238">在前面的程式碼中，Azure Blob 儲存體輸入預期參數名稱為 inputBlob。</span><span class="sxs-lookup"><span data-stu-id="ddc32-238">In the preceding code, the Azure Blob Storage input expects the parameter name to be *inputBlob*.</span></span> <span data-ttu-id="ddc32-239">選擇 sync.txt 檔案所位於的儲存體帳戶 (可能是相同或不同的儲存體帳戶)。</span><span class="sxs-lookup"><span data-stu-id="ddc32-239">Choose the storage account where the sync.txt file will reside (it could be the same or a different storage account).</span></span> <span data-ttu-id="ddc32-240">在 [路徑] 欄位中，以 {container-name}/path/to/sync.txt 格式提供檔案所在位置的路徑。</span><span class="sxs-lookup"><span data-stu-id="ddc32-240">In the path field, provide the path where the file lives in the format {container-name}/path/to/sync.txt.</span></span>

<span data-ttu-id="ddc32-241">新增類型為 [Azure Blob 儲存體] 輸出的輸出。</span><span class="sxs-lookup"><span data-stu-id="ddc32-241">Add an output of the type *Azure Blob Storage* output.</span></span> <span data-ttu-id="ddc32-242">這會指向您剛才在輸入中定義的 sync.txt 檔案。</span><span class="sxs-lookup"><span data-stu-id="ddc32-242">This will point to the sync.txt file you defined in the input.</span></span> <span data-ttu-id="ddc32-243">這可供函式用來寫入所查看的最後一個事件的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="ddc32-243">This is used by the function to write the timestamp of the last event looked at.</span></span> <span data-ttu-id="ddc32-244">前面的程式碼預期此參數名稱為 outputBlob。</span><span class="sxs-lookup"><span data-stu-id="ddc32-244">The preceding code expects this parameter to be called *outputBlob*.</span></span>

<span data-ttu-id="ddc32-245">此時，函式已準備就緒。</span><span class="sxs-lookup"><span data-stu-id="ddc32-245">At this point, the function is ready.</span></span> <span data-ttu-id="ddc32-246">請務必切換回 [開發] 索引標籤並儲存程式碼。</span><span class="sxs-lookup"><span data-stu-id="ddc32-246">Make sure to switch back to the **Develop** tab and save the code.</span></span> <span data-ttu-id="ddc32-247">檢查 [輸出] 視窗中是否有任何編譯錯誤，並據以更正。</span><span class="sxs-lookup"><span data-stu-id="ddc32-247">Check the output window for any compilation errors and correct them accordingly.</span></span> <span data-ttu-id="ddc32-248">如果程式碼進行編譯，則程式碼現在應該會每隔一分鐘檢查金鑰保存庫的記錄檔，並將任何新事件推送到已定義的服務匯流排佇列。</span><span class="sxs-lookup"><span data-stu-id="ddc32-248">If the code compiles, then the code should now be checking the key vault logs every minute and pushing any new events onto the defined Service Bus queue.</span></span> <span data-ttu-id="ddc32-249">您應該會在每次觸發函式時看到記錄資訊寫入到 [記錄檔] 視窗。</span><span class="sxs-lookup"><span data-stu-id="ddc32-249">You should see logging information write out to the log window every time the function is triggered.</span></span>

### <a name="azure-logic-app"></a><span data-ttu-id="ddc32-250">Azure 邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="ddc32-250">Azure logic app</span></span>
<span data-ttu-id="ddc32-251">接下來，您必須建立 Azure 邏輯應用程式，以挑選函式推送至服務匯流排佇列的事件、剖析內容，以及根據符合的條件傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="ddc32-251">Next you must create an Azure logic app that picks up the events that the function is pushing to the Service Bus queue, parses the content, and sends an email based on a condition being matched.</span></span>

<span data-ttu-id="ddc32-252">移至 [新增] -> [邏輯應用程式] 以[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="ddc32-252">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) by going to **New > Logic App**.</span></span>

<span data-ttu-id="ddc32-253">建立邏輯應用程式後，請瀏覽到該應用程式，然後選擇 [編輯] 。</span><span class="sxs-lookup"><span data-stu-id="ddc32-253">Once the logic app is created, navigate to it and choose **edit**.</span></span> <span data-ttu-id="ddc32-254">在邏輯應用程式編輯器中，選擇 [服務匯流排佇列] 並輸入服務匯流排認證，以將其連接至佇列。</span><span class="sxs-lookup"><span data-stu-id="ddc32-254">Within the logic app editor, choose **Service Bus Queue** and enter your Service Bus credentials to connect it to the queue.</span></span>

![Azure 邏輯應用程式服務匯流排](./media/keyvault-keyrotation/Azure_LogicApp_ServiceBus.png)

<span data-ttu-id="ddc32-256">接下來選擇 [新增條件]。</span><span class="sxs-lookup"><span data-stu-id="ddc32-256">Next choose **Add a condition**.</span></span> <span data-ttu-id="ddc32-257">在條件中，切換到進階編輯器並輸入下列程式碼，並以 Web 應用程式的實際 APP_ID 取代 APP_ID：</span><span class="sxs-lookup"><span data-stu-id="ddc32-257">In the condition, switch to the advanced editor and enter the following code, replacing APP_ID with the actual APP_ID of your web app:</span></span>

```
@equals('<APP_ID>', json(decodeBase64(triggerBody()['ContentData']))['identity']['claim']['appid'])
```

<span data-ttu-id="ddc32-258">如果來自連入事件 (亦即服務匯流排訊息的內文) 的 *appid* 不是應用程式的 *appid*，這個運算式基本上會傳回 **false**。</span><span class="sxs-lookup"><span data-stu-id="ddc32-258">This expression essentially returns **false** if the *appid* from the incoming event (which is the body of the Service Bus message) is not the *appid* of the app.</span></span>

<span data-ttu-id="ddc32-259">現在，在 [若為否，則不執行任何動作]  選項底下建立動作。</span><span class="sxs-lookup"><span data-stu-id="ddc32-259">Now, create an action under **If no, do nothing**.</span></span>

![Azure 邏輯應用程式選擇動作](./media/keyvault-keyrotation/Azure_LogicApp_Condition.png)

<span data-ttu-id="ddc32-261">針對動作選擇 [Office 365 - 傳送電子郵件] 。</span><span class="sxs-lookup"><span data-stu-id="ddc32-261">For the action, choose **Office 365 - send email**.</span></span> <span data-ttu-id="ddc32-262">填寫欄位，以建立定義的條件傳回 **false** 時要傳送的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="ddc32-262">Fill out the fields to create an email to send when the defined condition returns **false**.</span></span> <span data-ttu-id="ddc32-263">如果您沒有 Office 365，您可以查看能夠達到相同結果的替代方案。</span><span class="sxs-lookup"><span data-stu-id="ddc32-263">If you do not have Office 365, you could look at alternatives to achieve the same results.</span></span>

<span data-ttu-id="ddc32-264">此時，您已擁有端對端管線，它會每分鐘尋找是否有新的金鑰保存庫稽核記錄檔一次。</span><span class="sxs-lookup"><span data-stu-id="ddc32-264">At this point, you have an end to end pipeline that looks for new key vault audit logs once a minute.</span></span> <span data-ttu-id="ddc32-265">它會將找到的新記錄檔推送至服務匯流排佇列。</span><span class="sxs-lookup"><span data-stu-id="ddc32-265">It pushes new logs it finds to a service bus queue.</span></span> <span data-ttu-id="ddc32-266">新訊息放入佇列時就會觸發邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="ddc32-266">The logic app is triggered when a new message lands in the queue.</span></span> <span data-ttu-id="ddc32-267">如果事件中的 *appid* 不符合呼叫端應用程式的應用程式識別碼，則會傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="ddc32-267">If the *appid* within the event does not match the app ID of the calling application, it sends an email.</span></span>
