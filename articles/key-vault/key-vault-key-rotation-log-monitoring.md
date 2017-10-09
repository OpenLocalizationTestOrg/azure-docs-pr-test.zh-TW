---
title: "端對端金鑰輪替和稽核與 Azure 金鑰保存庫註冊 aaaSet |Microsoft 文件"
description: "使用此方式 tootoohelp 利用金鑰輪替與監視的金鑰保存庫記錄檔取得設定。"
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
ms.openlocfilehash: e0c393873077e3b91adc9fa7f39128bc1b6abe26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-azure-key-vault-with-end-to-end-key-rotation-and-auditing"></a><span data-ttu-id="30c49-103">使用端對端金鑰輪替和稽核設定 Azure 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="30c49-103">Set up Azure Key Vault with end-to-end key rotation and auditing</span></span>
## <a name="introduction"></a><span data-ttu-id="30c49-104">簡介</span><span class="sxs-lookup"><span data-stu-id="30c49-104">Introduction</span></span>
<span data-ttu-id="30c49-105">建立金鑰保存庫之後, 您就會使用該保存庫 toostore，您的金鑰和秘密可以 toostart。</span><span class="sxs-lookup"><span data-stu-id="30c49-105">After creating your key vault, you will be able toostart using that vault toostore your keys and secrets.</span></span> <span data-ttu-id="30c49-106">您的應用程式不需要再 toopersist 您的金鑰或密碼，但而是會視需要要求它們 hello 金鑰保存庫中。</span><span class="sxs-lookup"><span data-stu-id="30c49-106">Your applications no longer need toopersist your keys or secrets, but rather will request them from hello key vault as needed.</span></span> <span data-ttu-id="30c49-107">這可讓您 tooupdate 金鑰和密碼而不會影響 hello 應用程式的行為，開啟您的金鑰和秘密管理周圍的可能值範圍。</span><span class="sxs-lookup"><span data-stu-id="30c49-107">This allows you tooupdate keys and secrets without affecting hello behavior of your application, which opens up a breadth of possibilities around your key and secret management.</span></span>

<span data-ttu-id="30c49-108">本文逐步解說示範如何使用 Azure 金鑰保存庫 toostore 密碼，在此情況下存取應用程式的 Azure 儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="30c49-108">This article walks through an example of using Azure Key Vault toostore a secret, in this case an Azure Storage Account key that is accessed by an application.</span></span> <span data-ttu-id="30c49-109">文中也會示範如何實作該儲存體帳戶金鑰的排程輪替。</span><span class="sxs-lookup"><span data-stu-id="30c49-109">It also demonstrates implementation of a scheduled rotation of that storage account key.</span></span> <span data-ttu-id="30c49-110">最後，它逐步解說示範如何 toomonitor hello 金鑰保存庫稽核記錄檔，以及進行非預期的要求時發出警示。</span><span class="sxs-lookup"><span data-stu-id="30c49-110">Finally, it walks through a demonstration of how toomonitor hello key vault audit logs and raise alerts when unexpected requests are made.</span></span>

> [!NOTE]
> <span data-ttu-id="30c49-111">本教學課程不預期的 tooexplain 詳細 hello 初始設定金鑰保存庫中。</span><span class="sxs-lookup"><span data-stu-id="30c49-111">This tutorial is not intended tooexplain in detail hello initial setup of your key vault.</span></span> <span data-ttu-id="30c49-112">如需這方面的資訊，請參閱 [開始使用 Azure 金鑰保存庫](key-vault-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="30c49-112">For this information, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span> <span data-ttu-id="30c49-113">如需跨平台命令列介面的指示，請參閱[使用 CLI 管理金鑰保存庫](key-vault-manage-with-cli2.md)。</span><span class="sxs-lookup"><span data-stu-id="30c49-113">For Cross-Platform Command-Line Interface instructions, see [Manage Key Vault using CLI](key-vault-manage-with-cli2.md).</span></span>
>
>

## <a name="set-up-key-vault"></a><span data-ttu-id="30c49-114">設定金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="30c49-114">Set up Key Vault</span></span>
<span data-ttu-id="30c49-115">tooenable 應用程式 tooretrieve 密碼從金鑰保存庫，您必須先建立 hello 密碼並將它上傳 tooyour 保存庫。</span><span class="sxs-lookup"><span data-stu-id="30c49-115">tooenable an application tooretrieve a secret from Key Vault, you must first create hello secret and upload it tooyour vault.</span></span> <span data-ttu-id="30c49-116">這可藉由啟動 Azure PowerShell 工作階段然後登入 tooyour Azure 帳戶以 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="30c49-116">This can be accomplished by starting an Azure PowerShell session and signing in tooyour Azure account with hello following command:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="30c49-117">在 [hello] 快顯瀏覽器視窗中，輸入您的 Azure 帳戶使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="30c49-117">In hello pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="30c49-118">PowerShell 會取得與此帳戶相關聯的所有 hello 訂閱。</span><span class="sxs-lookup"><span data-stu-id="30c49-118">PowerShell will get all hello subscriptions that are associated with this account.</span></span> <span data-ttu-id="30c49-119">PowerShell 會使用 hello 預設第一個。</span><span class="sxs-lookup"><span data-stu-id="30c49-119">PowerShell uses hello first one by default.</span></span>

<span data-ttu-id="30c49-120">如果您有多個訂閱，您可能必須 toospecify hello 分別為使用的 toocreate 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="30c49-120">If you have multiple subscriptions, you might have toospecify hello one that was used toocreate your key vault.</span></span> <span data-ttu-id="30c49-121">輸入下列帳戶 toosee hello 訂閱 hello:</span><span class="sxs-lookup"><span data-stu-id="30c49-121">Enter hello following toosee hello subscriptions for your account:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="30c49-122">輸入 toospecify hello 訂用帳戶與 hello 金鑰保存庫，您將記錄、 相關聯：</span><span class="sxs-lookup"><span data-stu-id="30c49-122">toospecify hello subscription that's associated with hello key vault you will be logging, enter:</span></span>

```powershell
Set-AzureRmContext -SubscriptionId <subscriptionID>
```

<span data-ttu-id="30c49-123">因為本文會示範如何將儲存體帳戶金鑰儲存為密碼，所以您必須取得該儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="30c49-123">Because this article demonstrates storing a storage account key as a secret, you must get that storage account key.</span></span>

```powershell
Get-AzureRmStorageAccountKey -ResourceGroupName <resourceGroupName> -Name <storageAccountName>
```

<span data-ttu-id="30c49-124">擷取後您的密碼 （在此情況下，儲存體帳戶金鑰），您必須轉換該 tooa 安全字串，然後建立該密碼金鑰保存庫中。</span><span class="sxs-lookup"><span data-stu-id="30c49-124">After retrieving your secret (in this case, your storage account key), you must convert that tooa secure string and then create a secret with that value in your key vault.</span></span>

```powershell
$secretvalue = ConvertTo-SecureString <storageAccountKey> -AsPlainText -Force

Set-AzureKeyVaultSecret -VaultName <vaultName> -Name <secretName> -SecretValue $secretvalue
```
<span data-ttu-id="30c49-125">接下來，您所建立的 hello 密碼取得 hello URI。</span><span class="sxs-lookup"><span data-stu-id="30c49-125">Next, get hello URI for hello secret you created.</span></span> <span data-ttu-id="30c49-126">這用在稍後步驟中，當您呼叫 hello 金鑰保存庫 tooretrieve 您的密碼。</span><span class="sxs-lookup"><span data-stu-id="30c49-126">This is used in a later step when you call hello key vault tooretrieve your secret.</span></span> <span data-ttu-id="30c49-127">執行下列 PowerShell 命令的 hello，並記下 hello ID 值為 hello 密碼 URI:</span><span class="sxs-lookup"><span data-stu-id="30c49-127">Run hello following PowerShell command and make note of hello ID value, which is hello secret URI:</span></span>

```powershell
Get-AzureKeyVaultSecret –VaultName <vaultName>
```

## <a name="set-up-hello-application"></a><span data-ttu-id="30c49-128">設定 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="30c49-128">Set up hello application</span></span>
<span data-ttu-id="30c49-129">既然您已儲存的密碼，您可以使用程式碼 tooretrieve，並使用它。</span><span class="sxs-lookup"><span data-stu-id="30c49-129">Now that you have a secret stored, you can use code tooretrieve and use it.</span></span> <span data-ttu-id="30c49-130">有幾個步驟需要的 tooachieve 這。</span><span class="sxs-lookup"><span data-stu-id="30c49-130">There are a few steps required tooachieve this.</span></span> <span data-ttu-id="30c49-131">hello 第一個且最重要步驟是向 Azure Active Directory 中註冊您的應用程式，然後告訴金鑰保存庫的應用程式資訊，使它可以讓您的應用程式的要求。</span><span class="sxs-lookup"><span data-stu-id="30c49-131">hello first and most important step is registering your application with Azure Active Directory and then telling Key Vault your application information so that it can allow requests from your application.</span></span>

> [!NOTE]
> <span data-ttu-id="30c49-132">您的應用程式必須在建立 hello 相同金鑰保存庫以 Azure Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="30c49-132">Your application must be created on hello same Azure Active Directory tenant as your key vault.</span></span>
>
>

<span data-ttu-id="30c49-133">開啟 Azure Active Directory hello 應用程式 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="30c49-133">Open hello applications tab of Azure Active Directory.</span></span>

![在 Azure Active Directory 中開啟應用程式](./media/keyvault-keyrotation/AzureAD_Header.png)

<span data-ttu-id="30c49-135">選擇**新增**tooadd 應用程式 tooyour Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="30c49-135">Choose **ADD** tooadd an application tooyour Azure Active Directory.</span></span>

![選擇 [新增]](./media/keyvault-keyrotation/Azure_AD_AddApp.png)

<span data-ttu-id="30c49-137">保留 hello 應用程式類型為**WEB 應用程式和/或 WEB API**並提供您的應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="30c49-137">Leave hello application type as **WEB APPLICATION AND/OR WEB API** and give your application a name.</span></span>

![名稱 hello 應用程式](./media/keyvault-keyrotation/AzureAD_NewApp1.png)

<span data-ttu-id="30c49-139">為應用程式提供 [登入 URL] 和 [應用程式識別碼 URI]。</span><span class="sxs-lookup"><span data-stu-id="30c49-139">Give your application a **SIGN-ON URL** and an **APP ID URI**.</span></span> <span data-ttu-id="30c49-140">這些可以是任何想用於此示範的值，並可在稍後視需要加以變更。</span><span class="sxs-lookup"><span data-stu-id="30c49-140">These can be anything you want for this demo, and they can be changed later if needed.</span></span>

![提供必要的 URI](./media/keyvault-keyrotation/AzureAD_NewApp2.png)

<span data-ttu-id="30c49-142">Hello 應用程式會加入 tooAzure Active Directory 之後，您將帶入 hello 應用程式頁面。</span><span class="sxs-lookup"><span data-stu-id="30c49-142">After hello application is added tooAzure Active Directory, you will be brought into hello application page.</span></span> <span data-ttu-id="30c49-143">按一下 hello**設定**索引標籤，然後尋找並複製 hello**用戶端識別碼**值。</span><span class="sxs-lookup"><span data-stu-id="30c49-143">Click hello **Configure** tab and then find and copy hello **Client ID** value.</span></span> <span data-ttu-id="30c49-144">記下稍後步驟中的 hello 用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="30c49-144">Make note of hello client ID for later steps.</span></span>

<span data-ttu-id="30c49-145">接下來，產生金鑰，以便應用程式與 Azure Active Directory 互動。</span><span class="sxs-lookup"><span data-stu-id="30c49-145">Next, generate a key for your application so it can interact with your Azure Active Directory.</span></span> <span data-ttu-id="30c49-146">您可以在 hello 下建立這個**金鑰**> 一節中 hello**組態** 索引標籤。記下稍後步驟中使用的新產生的 hello 金鑰從 Azure Active Directory 應用程式。</span><span class="sxs-lookup"><span data-stu-id="30c49-146">You can create this under hello **Keys** section in hello **Configuration** tab. Make note of hello newly generated key from your Azure Active Directory application for use in a later step.</span></span>

![Azure Active Directory 應用程式金鑰](./media/keyvault-keyrotation/Azure_AD_AppKeys.png)

<span data-ttu-id="30c49-148">建立應用程式分成 hello 金鑰保存庫中的任何呼叫之前, 您必須告訴 hello 金鑰保存庫有關您的應用程式和其權限。</span><span class="sxs-lookup"><span data-stu-id="30c49-148">Before establishing any calls from your application into hello key vault, you must tell hello key vault about your application and its permissions.</span></span> <span data-ttu-id="30c49-149">hello 下列命令會使用 hello 保存庫名稱和 hello 用戶端識別碼，從您的 Azure Active Directory 應用程式和授與**取得**hello 應用程式的存取 tooyour 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="30c49-149">hello following command takes hello vault name and hello client ID from your Azure Active Directory app and grants **Get** access tooyour key vault for hello application.</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <clientIDfromAzureAD> -PermissionsToSecrets Get
```

<span data-ttu-id="30c49-150">此時，您就準備好 toostart 建置您的應用程式呼叫。</span><span class="sxs-lookup"><span data-stu-id="30c49-150">At this point, you are ready toostart building your application calls.</span></span> <span data-ttu-id="30c49-151">在您的應用程式中，您必須安裝 hello NuGet 套件需要的 toointeract 使用 Azure 金鑰保存庫與 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="30c49-151">In your application, you must install hello NuGet packages required toointeract with Azure Key Vault and Azure Active Directory.</span></span> <span data-ttu-id="30c49-152">Hello Visual Studio 封裝管理員主控台中，輸入下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="30c49-152">From hello Visual Studio Package Manager console, enter hello following commands.</span></span> <span data-ttu-id="30c49-153">Hello 撰寫這篇文章，hello 目前 hello Azure Active Directory 封裝會版 3.10.305231913，因此您可能會想 tooconfirm hello 最新版本，並據此更新。</span><span class="sxs-lookup"><span data-stu-id="30c49-153">At hello writing of this article, hello current version of hello Azure Active Directory package is 3.10.305231913, so you might want tooconfirm hello latest version and update accordingly.</span></span>

```powershell
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 3.10.305231913

Install-Package Microsoft.Azure.KeyVault
```

<span data-ttu-id="30c49-154">在您的應用程式程式碼建立類別 toohold hello 方法的 Azure Active Directory 驗證。</span><span class="sxs-lookup"><span data-stu-id="30c49-154">In your application code, create a class toohold hello method for your Azure Active Directory authentication.</span></span> <span data-ttu-id="30c49-155">在此範例中，該類別稱為 **Utils**。</span><span class="sxs-lookup"><span data-stu-id="30c49-155">In this example, that class is called **Utils**.</span></span> <span data-ttu-id="30c49-156">新增 hello 下列 using 陳述式：</span><span class="sxs-lookup"><span data-stu-id="30c49-156">Add hello following using statement:</span></span>

```csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="30c49-157">接下來，新增 Azure Active Directory 中的下列方法 tooretrieve hello JWT 權杖中的 hello。</span><span class="sxs-lookup"><span data-stu-id="30c49-157">Next, add hello following method tooretrieve hello JWT token from Azure Active Directory.</span></span> <span data-ttu-id="30c49-158">為方便維護，您可能想 toomove hello 硬式編碼的字串值至 web 或應用程式組態中。</span><span class="sxs-lookup"><span data-stu-id="30c49-158">For maintainability, you may want toomove hello hard-coded string values into your web or application configuration.</span></span>

```csharp
public async static Task<string> GetToken(string authority, string resource, string scope)
{
    var authContext = new AuthenticationContext(authority);

    ClientCredential clientCred = new ClientCredential("<AzureADApplicationClientID>","<AzureADApplicationClientKey>");

    AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

    if (result == null)

    throw new InvalidOperationException("Failed tooobtain hello JWT token");

    return result.AccessToken;
}
```

<span data-ttu-id="30c49-159">新增 hello 必要的程式碼 toocall 金鑰保存庫，和擷取您的密碼值。</span><span class="sxs-lookup"><span data-stu-id="30c49-159">Add hello necessary code toocall Key Vault and retrieve your secret value.</span></span> <span data-ttu-id="30c49-160">您必須在第一次加入 hello 下列 using 陳述式：</span><span class="sxs-lookup"><span data-stu-id="30c49-160">First you must add hello following using statement:</span></span>

```csharp
using Microsoft.Azure.KeyVault;
```

<span data-ttu-id="30c49-161">新增 hello 方法呼叫 tooinvoke 金鑰保存庫，和擷取您的密碼。</span><span class="sxs-lookup"><span data-stu-id="30c49-161">Add hello method calls tooinvoke Key Vault and retrieve your secret.</span></span> <span data-ttu-id="30c49-162">在此方法中，您可以提供 hello 機密您在上一個步驟中儲存的 URI。</span><span class="sxs-lookup"><span data-stu-id="30c49-162">In this method, you provide hello secret URI that you saved in a previous step.</span></span> <span data-ttu-id="30c49-163">請記下的 hello hello 使用**GetToken**方法從 hello **Utils**先前建立的類別。</span><span class="sxs-lookup"><span data-stu-id="30c49-163">Note hello use of hello **GetToken** method from hello **Utils** class created previously.</span></span>

```csharp
var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

var sec = kv.GetSecretAsync(<SecretID>).Result.Value;
```

<span data-ttu-id="30c49-164">當您執行您的應用程式時，您應該立即驗證 tooAzure Active Directory，然後從 Azure 金鑰保存庫擷取您的密碼值。</span><span class="sxs-lookup"><span data-stu-id="30c49-164">When you run your application, you should now be authenticating tooAzure Active Directory and then retrieving your secret value from Azure Key Vault.</span></span>

## <a name="key-rotation-using-azure-automation"></a><span data-ttu-id="30c49-165">使用 Azure 自動化的金鑰輪替</span><span class="sxs-lookup"><span data-stu-id="30c49-165">Key rotation using Azure Automation</span></span>
<span data-ttu-id="30c49-166">針對儲存為 Azure 金鑰保存庫密碼的值，有各種選項可用來實作其輪替策略。</span><span class="sxs-lookup"><span data-stu-id="30c49-166">There are various options for implementing a rotation strategy for values you store as Azure Key Vault secrets.</span></span> <span data-ttu-id="30c49-167">密碼可以在進行手動程序時輪替、使用 API 呼叫以程式設計的方式輪替，或是透過自動化指令碼來輪替。</span><span class="sxs-lookup"><span data-stu-id="30c49-167">Secrets can be rotated as part of a manual process, they may be rotated programmatically by using API calls, or they may be rotated by way of an Automation script.</span></span> <span data-ttu-id="30c49-168">基於 hello 這篇文章，您將無法使用 Azure PowerShell 結合 Azure 自動化 toochange 的 Azure 儲存體帳戶存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="30c49-168">For hello purposes of this article, you will be using Azure PowerShell combined with Azure Automation toochange an Azure Storage Account access key.</span></span> <span data-ttu-id="30c49-169">然後您將使用這個新金鑰來更新金鑰保存庫密碼。</span><span class="sxs-lookup"><span data-stu-id="30c49-169">You will then update a key vault secret with that new key.</span></span>

<span data-ttu-id="30c49-170">tooallow Azure 自動化 tooset 祕密值在金鑰保存庫中的，您必須取得名為 AzureRunAsConnection，建立您的 Azure 自動化執行個體時所建立的 hello 連接 hello 用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="30c49-170">tooallow Azure Automation tooset secret values in your key vault, you must get hello client ID for hello connection named AzureRunAsConnection, which was created when you established your Azure Automation instance.</span></span> <span data-ttu-id="30c49-171">從 Azure 自動化執行個體選擇 [資產]，即可尋找這個識別碼。</span><span class="sxs-lookup"><span data-stu-id="30c49-171">You can find this ID by choosing **Assets** from your Azure Automation instance.</span></span> <span data-ttu-id="30c49-172">在您選擇從該處，**連線**]，然後選取 [hello **AzureRunAsConnection**服務主體。</span><span class="sxs-lookup"><span data-stu-id="30c49-172">From there, you choose **Connections** and then select hello **AzureRunAsConnection** service principle.</span></span> <span data-ttu-id="30c49-173">記下 hello**應用程式識別碼**。</span><span class="sxs-lookup"><span data-stu-id="30c49-173">Take note of hello **Application ID**.</span></span>

![Azure 自動化用戶端識別碼](./media/keyvault-keyrotation/Azure_Automation_ClientID.png)

<span data-ttu-id="30c49-175">在 [資產] 中，選擇 [模組]。</span><span class="sxs-lookup"><span data-stu-id="30c49-175">In **Assets**, choose **Modules**.</span></span> <span data-ttu-id="30c49-176">從**模組**，選取**圖庫**，然後搜尋和**匯入**更新版本的每個 hello 下列模組：</span><span class="sxs-lookup"><span data-stu-id="30c49-176">From **Modules**, select **Gallery**, and then search for and **Import** updated versions of each of hello following modules:</span></span>

    Azure
    Azure.Storage
    AzureRM.Profile
    AzureRM.KeyVault
    AzureRM.Automation
    AzureRM.Storage


> [!NOTE]
> <span data-ttu-id="30c49-177">Hello 撰寫這篇文章時，只有 hello 前面所述的模組所需 toobe 更新 hello 下列指令碼。</span><span class="sxs-lookup"><span data-stu-id="30c49-177">At hello writing of this article, only hello previously noted modules needed toobe updated for hello following script.</span></span> <span data-ttu-id="30c49-178">如果您發現自動化作業失敗，請確認您已匯入所有必要的模組及其相依項目。</span><span class="sxs-lookup"><span data-stu-id="30c49-178">If you find that your automation job is failing, confirm that you have imported all necessary modules and their dependencies.</span></span>
>
>

<span data-ttu-id="30c49-179">Hello 應用程式識別碼擷取您的 Azure 自動化連線之後，您必須告訴您金鑰保存庫這個應用程式已存取 tooupdate 機密資料，您的保存庫中。</span><span class="sxs-lookup"><span data-stu-id="30c49-179">After you have retrieved hello application ID for your Azure Automation connection, you must tell your key vault that this application has access tooupdate secrets in your vault.</span></span> <span data-ttu-id="30c49-180">可以使用下列 PowerShell 命令的 hello 完成這個動作：</span><span class="sxs-lookup"><span data-stu-id="30c49-180">This can be accomplished with hello following PowerShell command:</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <applicationIDfromAzureAutomation> -PermissionsToSecrets Set
```

<span data-ttu-id="30c49-181">接下來，選取 Azure 自動化執行個體底下的 [Runbook] 資源，然後選取 [新增 Runbook]。</span><span class="sxs-lookup"><span data-stu-id="30c49-181">Next, select **Runbooks** under your Azure Automation instance, and then select **Add a Runbook**.</span></span> <span data-ttu-id="30c49-182">選取 [快速建立] 。</span><span class="sxs-lookup"><span data-stu-id="30c49-182">Select **Quick Create**.</span></span> <span data-ttu-id="30c49-183">命名您的 runbook，並選取**PowerShell** hello runbook 類型。</span><span class="sxs-lookup"><span data-stu-id="30c49-183">Name your runbook and select **PowerShell** as hello runbook type.</span></span> <span data-ttu-id="30c49-184">您有 hello 選項 tooadd 描述。</span><span class="sxs-lookup"><span data-stu-id="30c49-184">You have hello option tooadd a description.</span></span> <span data-ttu-id="30c49-185">最後，按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="30c49-185">Finally, click **Create**.</span></span>

![建立 Runbook](./media/keyvault-keyrotation/Create_Runbook.png)

<span data-ttu-id="30c49-187">貼上下列 PowerShell 指令碼，在新的 runbook 的 hello 編輯器窗格中的 hello:</span><span class="sxs-lookup"><span data-stu-id="30c49-187">Paste hello following PowerShell script in hello editor pane for your new runbook:</span></span>

```powershell
$connectionName = "AzureRunAsConnection"
try
{
    # Get hello connection "AzureRunAsConnection "
    $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

    "Logging in tooAzure..."
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

#Optionally you may set hello following as parameters
$StorageAccountName = <storageAccountName>
$RGName = <storageAccountResourceGroupName>
$VaultName = <keyVaultName>
$SecretName = <keyVaultSecretName>

#Key name. For example key1 or key2 for hello storage account
New-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName -KeyName "key2" -Verbose
$SAKeys = Get-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName

$secretvalue = ConvertTo-SecureString $SAKeys[1].Value -AsPlainText -Force

$secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secretvalue
```

<span data-ttu-id="30c49-188">從 hello 編輯器窗格中，選擇 **測試窗格**tootest 指令碼。</span><span class="sxs-lookup"><span data-stu-id="30c49-188">From hello editor pane, choose **Test pane** tootest your script.</span></span> <span data-ttu-id="30c49-189">一旦 hello 指令碼執行時並沒有錯誤，您可以選取**發行**，然後您可以套用回在 hello runbook 設定 窗格中的 hello runbook 的排程。</span><span class="sxs-lookup"><span data-stu-id="30c49-189">Once hello script is running without error, you can select **Publish**, and then you can apply a schedule for hello runbook back in hello runbook configuration pane.</span></span>

## <a name="key-vault-auditing-pipeline"></a><span data-ttu-id="30c49-190">金鑰保存庫稽核管線</span><span class="sxs-lookup"><span data-stu-id="30c49-190">Key Vault auditing pipeline</span></span>
<span data-ttu-id="30c49-191">當您設定金鑰保存庫時，您可以開啟稽核功能 toocollect 提出 toohello 金鑰保存庫的存取要求的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="30c49-191">When you set up a key vault, you can turn on auditing toocollect logs on access requests made toohello key vault.</span></span> <span data-ttu-id="30c49-192">這些記錄檔會儲存在指定的 Azure 儲存體帳戶中，以供提取、監視和分析。</span><span class="sxs-lookup"><span data-stu-id="30c49-192">These logs are stored in a designated Azure Storage account and can be pulled out, monitored, and analyzed.</span></span> <span data-ttu-id="30c49-193">hello 下列案例使用 Azure 函式、 Azure 邏輯應用程式和金鑰保存庫的稽核記錄檔 toocreate 管線 toosend 電子郵件時的應用程式，並符合 hello hello web 應用程式的應用程式識別碼 hello 保存庫中擷取機密資料。</span><span class="sxs-lookup"><span data-stu-id="30c49-193">hello following scenario uses Azure functions, Azure logic apps, and key vault audit logs toocreate a pipeline toosend an email when an app that does match hello app ID of hello web app retrieves secrets from hello vault.</span></span>

<span data-ttu-id="30c49-194">首先，您必須在金鑰保存庫上啟用記錄功能。</span><span class="sxs-lookup"><span data-stu-id="30c49-194">First, you must enable logging on your key vault.</span></span> <span data-ttu-id="30c49-195">這可透過下列 PowerShell 命令的 hello (完整詳細資料，可以看到在[金鑰保存庫記錄](key-vault-logging.md)):</span><span class="sxs-lookup"><span data-stu-id="30c49-195">This can be done via hello following PowerShell commands (full details can be seen at [key-vault-logging](key-vault-logging.md)):</span></span>

```powershell
$sa = New-AzureRmStorageAccount -ResourceGroupName <resourceGroupName> -Name <storageAccountName> -Type Standard\_LRS -Location 'East US'
$kv = Get-AzureRmKeyVault -VaultName '<vaultName>'
Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent
```

<span data-ttu-id="30c49-196">啟用此選項之後，稽核記錄，到指定的儲存體帳戶的 hello 收集的開始。</span><span class="sxs-lookup"><span data-stu-id="30c49-196">After this is enabled, audit logs start collecting into hello designated storage account.</span></span> <span data-ttu-id="30c49-197">這些記錄檔包含有關金鑰保存庫存取方式、時間和存取者的事件。</span><span class="sxs-lookup"><span data-stu-id="30c49-197">These logs contain events about how and when your key vaults are accessed, and by whom.</span></span>

> [!NOTE]
> <span data-ttu-id="30c49-198">您可以存取您的記錄資訊 hello 金鑰保存庫作業後 10 分鐘。</span><span class="sxs-lookup"><span data-stu-id="30c49-198">You can access your logging information 10 minutes after hello key vault operation.</span></span> <span data-ttu-id="30c49-199">但通常不用這麼久。</span><span class="sxs-lookup"><span data-stu-id="30c49-199">It will usually be quicker than this.</span></span>
>
>

<span data-ttu-id="30c49-200">hello 下一個步驟太[建立 Azure 服務匯流排佇列](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md)。</span><span class="sxs-lookup"><span data-stu-id="30c49-200">hello next step is too[create an Azure Service Bus queue](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span> <span data-ttu-id="30c49-201">這是金鑰保存庫稽核記錄檔的推送位置。</span><span class="sxs-lookup"><span data-stu-id="30c49-201">This is where key vault audit logs are pushed.</span></span> <span data-ttu-id="30c49-202">Hello 佇列中 hello 稽核記錄檔訊息時，hello 邏輯應用程式會拾取它們，並充當他們。</span><span class="sxs-lookup"><span data-stu-id="30c49-202">When hello audit log messages are in hello queue, hello logic app picks them up and acts on them.</span></span> <span data-ttu-id="30c49-203">建立服務匯流排與 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="30c49-203">Create a service bus with hello following steps:</span></span>

1. <span data-ttu-id="30c49-204">建立服務匯流排命名空間 (如果您已有您想要這麼做，toouse 略過 tooStep 2)。</span><span class="sxs-lookup"><span data-stu-id="30c49-204">Create a Service Bus namespace (if you already have one that you want toouse for this, skip tooStep 2).</span></span>
2. <span data-ttu-id="30c49-205">瀏覽 toohello hello Azure 入口網站和選取 hello 命名空間中要 toocreate hello 佇列中的服務匯流排。</span><span class="sxs-lookup"><span data-stu-id="30c49-205">Browse toohello service bus in hello Azure portal and select hello namespace you want toocreate hello queue in.</span></span>
3. <span data-ttu-id="30c49-206">選取**新增**選擇**Service Bus > 佇列**並輸入所需的 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="30c49-206">Select **New** and choose **Service Bus > Queue** and enter hello required details.</span></span>
4. <span data-ttu-id="30c49-207">選擇 hello 命名空間，並按一下選取 hello 服務匯流排連接資訊**連接資訊**。</span><span class="sxs-lookup"><span data-stu-id="30c49-207">Select hello Service Bus connection information by choosing hello namespace and clicking **Connection Information**.</span></span> <span data-ttu-id="30c49-208">您將需要這項資訊 hello 下一節。</span><span class="sxs-lookup"><span data-stu-id="30c49-208">You will need this information for hello next section.</span></span>

<span data-ttu-id="30c49-209">下一步[建立 Azure 的函式](../azure-functions/functions-create-first-azure-function.md)toopoll 金鑰保存庫的記錄檔內 hello 儲存體帳戶，並挑選新的事件。</span><span class="sxs-lookup"><span data-stu-id="30c49-209">Next, [create an Azure function](../azure-functions/functions-create-first-azure-function.md) toopoll key vault logs within hello storage account and pick up new events.</span></span> <span data-ttu-id="30c49-210">這是會依排程觸發的函式。</span><span class="sxs-lookup"><span data-stu-id="30c49-210">This will be a function that is triggered on a schedule.</span></span>

<span data-ttu-id="30c49-211">toocreate Azure 的函式，選擇**新增 > 函式應用程式**hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="30c49-211">toocreate an Azure function, choose **New > Function App** in hello Azure portal.</span></span> <span data-ttu-id="30c49-212">在建立期間，您可以使用現有的主控方案，或建立新的方案。</span><span class="sxs-lookup"><span data-stu-id="30c49-212">During creation, you can use an existing hosting plan or create a new one.</span></span> <span data-ttu-id="30c49-213">您也可以選擇動態主控。</span><span class="sxs-lookup"><span data-stu-id="30c49-213">You could also opt for dynamic hosting.</span></span> <span data-ttu-id="30c49-214">需函式裝載選項的詳細資訊，請參閱[如何 tooscale Azure 函式](../azure-functions/functions-scale.md)。</span><span class="sxs-lookup"><span data-stu-id="30c49-214">More details on Function hosting options can be found at [How tooscale Azure Functions](../azure-functions/functions-scale.md).</span></span>

<span data-ttu-id="30c49-215">建立 hello Azure 函式時，瀏覽 tooit，並選擇計時器，函式和 C\#。</span><span class="sxs-lookup"><span data-stu-id="30c49-215">When hello Azure function is created, navigate tooit and choose a timer function and C\#.</span></span> <span data-ttu-id="30c49-216">然後按一下 [建立此函式]。</span><span class="sxs-lookup"><span data-stu-id="30c49-216">Then click **Create this function**.</span></span>

![Azure Functions 啟動刀鋒視窗](./media/keyvault-keyrotation/Azure_Functions_Start.png)

<span data-ttu-id="30c49-218">在 hello**開發**索引標籤上，hello run.csx 程式碼取代 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="30c49-218">On hello **Develop** tab, replace hello run.csx code with hello following:</span></span>

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
            log.Verbose($"Sync point file didnt have a date. Setting toonow.");
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

            //required tooorder by time as they may not be in hello file
            var results = ((IEnumerable<dynamic>) dynJson.records).OrderBy(p => p.time);

            foreach (var jsonItem in results)
            {
                DateTime dt = Convert.ToDateTime(jsonItem.time);

                if(dt>dtPrev){
                    log.Info($"{jsonItem.ToString()}");

                    var payloadStream = new MemoryStream(Encoding.UTF8.GetBytes(jsonItem.ToString()));
                    //When sending tooServiceBus, use hello payloadStream and set keeporiginal tootrue
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

    //Generate hello shared access signature on hello container, setting hello constraints directly on hello signature.
    string sasBlobToken = blob.GetSharedAccessSignature(sasConstraints);

    //Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```


> [!NOTE]
> <span data-ttu-id="30c49-219">請確定 tooreplace hello 變數在上述程式碼 toopoint tooyour 儲存體帳戶寫入記錄檔-金鑰保存庫 hello hello hello 您稍早建立的服務匯流排和 hello 特定路徑 toohello 金鑰保存庫儲存體記錄。</span><span class="sxs-lookup"><span data-stu-id="30c49-219">Make sure tooreplace hello variables in hello preceding code toopoint tooyour storage account where hello key vault logs are written, hello service bus you created earlier, and hello specific path toohello key vault storage logs.</span></span>
>
>

<span data-ttu-id="30c49-220">hello 函式挑選 hello 最新記錄檔從 hello 儲存體帳戶 hello 金鑰保存庫的記錄檔可寫入，該檔案中，從 grabs hello 最新事件，並將它們推送 tooa 服務匯流排佇列。</span><span class="sxs-lookup"><span data-stu-id="30c49-220">hello function picks up hello latest log file from hello storage account where hello key vault logs are written, grabs hello latest events from that file, and pushes them tooa Service Bus queue.</span></span> <span data-ttu-id="30c49-221">由於單一檔案可以擁有多個事件，您應該建立 hello 函式也會查看已收取 hello 最後一個事件 toodetermine hello 時間戳記 sync.txt 檔案。</span><span class="sxs-lookup"><span data-stu-id="30c49-221">Since a single file could have multiple events, you should create a sync.txt file that hello function also looks at toodetermine hello time stamp of hello last event that was picked up.</span></span> <span data-ttu-id="30c49-222">這可確保您不推送 hello 多次相同的事件。</span><span class="sxs-lookup"><span data-stu-id="30c49-222">This ensures that you don't push hello same event multiple times.</span></span> <span data-ttu-id="30c49-223">這個 sync.txt 檔案包含 hello 最後發生之事件的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="30c49-223">This sync.txt file contains a timestamp for hello last encountered event.</span></span> <span data-ttu-id="30c49-224">hello 記錄檔，載入時，已排序的 toobe 根據 hello 時間戳記 tooensure 正確排序。</span><span class="sxs-lookup"><span data-stu-id="30c49-224">hello logs, when loaded, have toobe sorted based on hello timestamp tooensure they are ordered correctly.</span></span>

<span data-ttu-id="30c49-225">這個函式中，我們會參考數個立即可用 hello Azure 函式中所沒有的額外程式庫。</span><span class="sxs-lookup"><span data-stu-id="30c49-225">For this function, we reference a couple of additional libraries that are not available out of hello box in Azure Functions.</span></span> <span data-ttu-id="30c49-226">tooinclude，我們需要 Azure 函式 toopull 它們使用 NuGet。</span><span class="sxs-lookup"><span data-stu-id="30c49-226">tooinclude these, we need Azure Functions toopull them using NuGet.</span></span> <span data-ttu-id="30c49-227">選擇 hello**檢視檔案**選項。</span><span class="sxs-lookup"><span data-stu-id="30c49-227">Choose hello **View Files** option.</span></span>

![檢視檔案選項](./media/keyvault-keyrotation/Azure_Functions_ViewFiles.png)

<span data-ttu-id="30c49-229">然後使用下列內容新增名為 project.json 的檔案︰</span><span class="sxs-lookup"><span data-stu-id="30c49-229">And add a file called project.json with following content:</span></span>

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
<span data-ttu-id="30c49-230">根據**儲存**，Azure 函式會下載所需的 hello 二進位檔。</span><span class="sxs-lookup"><span data-stu-id="30c49-230">Upon **Save**, Azure Functions will download hello required binaries.</span></span>

<span data-ttu-id="30c49-231">切換 toohello**整合**索引標籤，然後在 hello 函式有意義的名稱 toouse 命名 hello 計時器的參數。</span><span class="sxs-lookup"><span data-stu-id="30c49-231">Switch toohello **Integrate** tab and give hello timer parameter a meaningful name toouse within hello function.</span></span> <span data-ttu-id="30c49-232">在上述程式碼的 hello，它會預期呼叫 hello 計時器 toobe *myTimer*。</span><span class="sxs-lookup"><span data-stu-id="30c49-232">In hello preceding code, it expects hello timer toobe called *myTimer*.</span></span> <span data-ttu-id="30c49-233">指定[CRON 運算式](../app-service-web/web-sites-create-web-jobs.md#CreateScheduledCRON)，如下所示： 0 \* \* \* \* \*的 hello 計時器會導致 hello 函式 toorun 一分鐘一次。</span><span class="sxs-lookup"><span data-stu-id="30c49-233">Specify a [CRON expression](../app-service-web/web-sites-create-web-jobs.md#CreateScheduledCRON) as follows: 0 \* \* \* \* \* for hello timer that will cause hello function toorun once a minute.</span></span>

<span data-ttu-id="30c49-234">在 hello 相同**整合**索引標籤上，新增 hello 類型的輸入**Azure Blob 儲存體**。</span><span class="sxs-lookup"><span data-stu-id="30c49-234">On hello same **Integrate** tab, add an input of hello type **Azure Blob Storage**.</span></span> <span data-ttu-id="30c49-235">這將會為 toohello sync.txt 檔案，其中包含 hello hello 看 hello 函式的最後一個事件時間戳記。</span><span class="sxs-lookup"><span data-stu-id="30c49-235">This will point toohello sync.txt file that contains hello timestamp of hello last event looked at by hello function.</span></span> <span data-ttu-id="30c49-236">這將可依 hello 參數名稱的 hello 函式內。</span><span class="sxs-lookup"><span data-stu-id="30c49-236">This will be available within hello function by hello parameter name.</span></span> <span data-ttu-id="30c49-237">在上述程式碼的 hello，hello Azure Blob 儲存體輸入預期 hello 參數名稱 toobe *inputBlob*。</span><span class="sxs-lookup"><span data-stu-id="30c49-237">In hello preceding code, hello Azure Blob Storage input expects hello parameter name toobe *inputBlob*.</span></span> <span data-ttu-id="30c49-238">選擇 hello hello sync.txt 檔案所在的儲存體帳戶 （它可能是 hello 相同或不同的儲存體帳戶）。</span><span class="sxs-lookup"><span data-stu-id="30c49-238">Choose hello storage account where hello sync.txt file will reside (it could be hello same or a different storage account).</span></span> <span data-ttu-id="30c49-239">在 [hello 路徑] 欄位中提供 hello 路徑 hello 檔案所在 hello 格式 {container-name}/path/to/sync.txt。</span><span class="sxs-lookup"><span data-stu-id="30c49-239">In hello path field, provide hello path where hello file lives in hello format {container-name}/path/to/sync.txt.</span></span>

<span data-ttu-id="30c49-240">將輸出 hello 型別的*Azure Blob 儲存體*輸出。</span><span class="sxs-lookup"><span data-stu-id="30c49-240">Add an output of hello type *Azure Blob Storage* output.</span></span> <span data-ttu-id="30c49-241">這將會為您所定義 hello 輸入 toohello sync.txt 檔案。</span><span class="sxs-lookup"><span data-stu-id="30c49-241">This will point toohello sync.txt file you defined in hello input.</span></span> <span data-ttu-id="30c49-242">這會使用 hello 函式 toowrite hello 的時間戳記 hello 探討的最後一個事件。</span><span class="sxs-lookup"><span data-stu-id="30c49-242">This is used by hello function toowrite hello timestamp of hello last event looked at.</span></span> <span data-ttu-id="30c49-243">hello 上述程式碼需要呼叫此參數 toobe *outputBlob*。</span><span class="sxs-lookup"><span data-stu-id="30c49-243">hello preceding code expects this parameter toobe called *outputBlob*.</span></span>

<span data-ttu-id="30c49-244">此時，hello 函式已準備。</span><span class="sxs-lookup"><span data-stu-id="30c49-244">At this point, hello function is ready.</span></span> <span data-ttu-id="30c49-245">請確定 tooswitch 後 toohello**開發**索引標籤，然後儲存 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="30c49-245">Make sure tooswitch back toohello **Develop** tab and save hello code.</span></span> <span data-ttu-id="30c49-246">請檢查有任何編譯錯誤 hello 輸出 視窗，並據此進行更正。</span><span class="sxs-lookup"><span data-stu-id="30c49-246">Check hello output window for any compilation errors and correct them accordingly.</span></span> <span data-ttu-id="30c49-247">如果 hello 程式碼會編譯，hello 程式碼應該現在會檢查 hello 金鑰保存庫記錄每隔一分鐘，然後推送到 hello 的任何新事件定義服務匯流排佇列。</span><span class="sxs-lookup"><span data-stu-id="30c49-247">If hello code compiles, then hello code should now be checking hello key vault logs every minute and pushing any new events onto hello defined Service Bus queue.</span></span> <span data-ttu-id="30c49-248">您應該會看到每次觸發 hello 函式會寫出 toohello 記錄視窗的記錄資訊。</span><span class="sxs-lookup"><span data-stu-id="30c49-248">You should see logging information write out toohello log window every time hello function is triggered.</span></span>

### <a name="azure-logic-app"></a><span data-ttu-id="30c49-249">Azure 邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="30c49-249">Azure logic app</span></span>
<span data-ttu-id="30c49-250">接下來，您必須建立 Azure 邏輯應用程式收取 hello 事件 hello 函式在推入 toohello Service Bus 佇列、 剖析 hello 內容，並傳送電子郵件根據條件的比對。</span><span class="sxs-lookup"><span data-stu-id="30c49-250">Next you must create an Azure logic app that picks up hello events that hello function is pushing toohello Service Bus queue, parses hello content, and sends an email based on a condition being matched.</span></span>

<span data-ttu-id="30c49-251">[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)太移**新增 > 邏輯應用程式**。</span><span class="sxs-lookup"><span data-stu-id="30c49-251">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) by going too**New > Logic App**.</span></span>

<span data-ttu-id="30c49-252">Hello 邏輯應用程式建立之後，瀏覽 tooit 並選擇**編輯**。</span><span class="sxs-lookup"><span data-stu-id="30c49-252">Once hello logic app is created, navigate tooit and choose **edit**.</span></span> <span data-ttu-id="30c49-253">在 [hello 邏輯應用程式編輯器] 中，選擇**服務匯流排佇列**並輸入您的服務匯流排認證 tooconnect 它 toohello 佇列。</span><span class="sxs-lookup"><span data-stu-id="30c49-253">Within hello logic app editor, choose **Service Bus Queue** and enter your Service Bus credentials tooconnect it toohello queue.</span></span>

![Azure 邏輯應用程式服務匯流排](./media/keyvault-keyrotation/Azure_LogicApp_ServiceBus.png)

<span data-ttu-id="30c49-255">接下來選擇 [新增條件]。</span><span class="sxs-lookup"><span data-stu-id="30c49-255">Next choose **Add a condition**.</span></span> <span data-ttu-id="30c49-256">在 hello 條件切換 toohello 進階編輯器，並輸入下列程式碼，取代 hello APP_ID hello 實際 APP_ID web 應用程式：</span><span class="sxs-lookup"><span data-stu-id="30c49-256">In hello condition, switch toohello advanced editor and enter hello following code, replacing APP_ID with hello actual APP_ID of your web app:</span></span>

```
@equals('<APP_ID>', json(decodeBase64(triggerBody()['ContentData']))['identity']['claim']['appid'])
```

<span data-ttu-id="30c49-257">這個運算式基本上會傳回**false**如果 hello *appid* hello 從內送事件 （這是 hello hello Service Bus 訊息本文） 不是 hello *appid*的 hello應用程式。</span><span class="sxs-lookup"><span data-stu-id="30c49-257">This expression essentially returns **false** if hello *appid* from hello incoming event (which is hello body of hello Service Bus message) is not hello *appid* of hello app.</span></span>

<span data-ttu-id="30c49-258">現在，在 [若為否，則不執行任何動作]  選項底下建立動作。</span><span class="sxs-lookup"><span data-stu-id="30c49-258">Now, create an action under **If no, do nothing**.</span></span>

![Azure 邏輯應用程式選擇動作](./media/keyvault-keyrotation/Azure_LogicApp_Condition.png)

<span data-ttu-id="30c49-260">Hello 動作選擇**Office 365-傳送電子郵件**。</span><span class="sxs-lookup"><span data-stu-id="30c49-260">For hello action, choose **Office 365 - send email**.</span></span> <span data-ttu-id="30c49-261">填寫 hello 欄位 toocreate 電子郵件 toosend hello 定義條件傳回**false**。</span><span class="sxs-lookup"><span data-stu-id="30c49-261">Fill out hello fields toocreate an email toosend when hello defined condition returns **false**.</span></span> <span data-ttu-id="30c49-262">如果您沒有 Office 365，您無法查看替代項目 tooachieve hello 相同的結果。</span><span class="sxs-lookup"><span data-stu-id="30c49-262">If you do not have Office 365, you could look at alternatives tooachieve hello same results.</span></span>

<span data-ttu-id="30c49-263">此時，您必須尋找一分鐘一次新的金鑰保存庫稽核記錄檔結束 tooend 管線。</span><span class="sxs-lookup"><span data-stu-id="30c49-263">At this point, you have an end tooend pipeline that looks for new key vault audit logs once a minute.</span></span> <span data-ttu-id="30c49-264">推入新的記錄檔找到 tooa 服務匯流排佇列。</span><span class="sxs-lookup"><span data-stu-id="30c49-264">It pushes new logs it finds tooa service bus queue.</span></span> <span data-ttu-id="30c49-265">新訊息放置於 hello 佇列時，會觸發 hello 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="30c49-265">hello logic app is triggered when a new message lands in hello queue.</span></span> <span data-ttu-id="30c49-266">如果 hello *appid*內 hello 事件不符合 hello 應用程式識別碼 hello 呼叫應用程式時，會傳送一封電子郵件。</span><span class="sxs-lookup"><span data-stu-id="30c49-266">If hello *appid* within hello event does not match hello app ID of hello calling application, it sends an email.</span></span>
