---
title: "aaaRegister Azure 堆疊 |Microsoft 文件"
description: "使用您的 Azure 訂用帳戶註冊 Azure Stack。"
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: erikje
ms.openlocfilehash: 3a3c8e82bec3e1e26ecfe591ecc27b2b91f6f91e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="register-azure-stack-with-your-azure-subscription"></a><span data-ttu-id="ac514-103">使用您的 Azure 訂用帳戶註冊 Azure Stack</span><span class="sxs-lookup"><span data-stu-id="ac514-103">Register Azure Stack with your Azure Subscription</span></span>

<span data-ttu-id="ac514-104">Azure Active Directory 部署，您可以向 Azure 堆疊從 Azure 和商務資料回報 tooMicrosoft tooset Azure toodownload marketplace 項目。</span><span class="sxs-lookup"><span data-stu-id="ac514-104">For Azure Active Directory deployments, you can register Azure Stack with Azure toodownload marketplace items from Azure and tooset up commerce data reporting back tooMicrosoft.</span></span> 

> [!NOTE]
><span data-ttu-id="ac514-105">建議註冊，因為它可讓您 tootest 重要 Azure 堆疊功能，例如 marketplace 新聞訂閱和使用方式報表。</span><span class="sxs-lookup"><span data-stu-id="ac514-105">Registration is recommended because it enables you tootest important Azure Stack functionality, like marketplace syndication and usage reporting.</span></span> <span data-ttu-id="ac514-106">註冊 Azure 堆疊之後，用法就是報告的 tooAzure 商務。</span><span class="sxs-lookup"><span data-stu-id="ac514-106">After you register Azure Stack, usage is reported tooAzure commerce.</span></span> <span data-ttu-id="ac514-107">您可以查看您用於註冊 hello 訂用帳戶底下。</span><span class="sxs-lookup"><span data-stu-id="ac514-107">You can see it under hello subscription you used for registration.</span></span> <span data-ttu-id="ac514-108">Azure Stack 開發套件使用者將不需針對回報的任何使用方式支付費用。</span><span class="sxs-lookup"><span data-stu-id="ac514-108">Azure Stack Development Kit users will not be charged for any usage they report.</span></span>
>


## <a name="get-azure-subscription"></a><span data-ttu-id="ac514-109">取得 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ac514-109">Get Azure subscription</span></span>

<span data-ttu-id="ac514-110">使用 Azure 註冊 Azure Stack 之前，您必須：</span><span class="sxs-lookup"><span data-stu-id="ac514-110">Before registering Azure Stack with Azure, you must have:</span></span>

- <span data-ttu-id="ac514-111">hello Azure 訂用帳戶的訂用帳戶 ID。</span><span class="sxs-lookup"><span data-stu-id="ac514-111">hello subscription ID for an Azure subscription.</span></span> <span data-ttu-id="ac514-112">tooget hello ID，登入 tooAzure，按一下**更多服務** > **訂閱**，按一下您想要 toouse，hello 訂用帳戶，並在**Essentials**您可以尋找 hello**訂用帳戶 ID**。</span><span class="sxs-lookup"><span data-stu-id="ac514-112">tooget hello ID, sign in tooAzure, click **More services** > **Subscriptions**, click hello subscription you want toouse, and under **Essentials** you can find hello **Subscription ID**.</span></span> <span data-ttu-id="ac514-113">目前不支援中國、德國，和美國政府雲端訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ac514-113">China, Germany, and US government cloud subscriptions are not currently supported.</span></span>
- <span data-ttu-id="ac514-114">hello 使用者名稱和密碼是 hello 訂用帳戶擁有者的帳戶 （MSA/2FA 帳戶支援）</span><span class="sxs-lookup"><span data-stu-id="ac514-114">hello username and password for an account that is an owner for hello subscription (MSA/2FA accounts are supported)</span></span>
- <span data-ttu-id="ac514-115">hello hello Azure 訂用帳戶的 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="ac514-115">hello Azure Active Directory for hello Azure subscription.</span></span> <span data-ttu-id="ac514-116">將滑鼠游標停留在您的顯示圖片在 hello 右上角的 hello Azure 入口網站，您可以在 Azure 中找到此目錄。</span><span class="sxs-lookup"><span data-stu-id="ac514-116">You can find this directory in Azure by hovering over your avatar at hello top right corner of hello Azure portal.</span></span> 
- <span data-ttu-id="ac514-117">已註冊的 hello Azure 堆疊資源提供者 (請參閱 hello**註冊的 Azure 堆疊資源提供者**下面章節以取得詳細資料)</span><span class="sxs-lookup"><span data-stu-id="ac514-117">Registered hello Azure Stack resource provider (see hello **Register Azure Stack Resource Provider** section below for details)</span></span>

<span data-ttu-id="ac514-118">如果您沒有符合這些需求的 Azure 訂用帳戶，則可以[在這裡建立免費的 Azure 帳戶](https://azure.microsoft.com/en-us/free/?b=17.06)。</span><span class="sxs-lookup"><span data-stu-id="ac514-118">If you don’t have an Azure subscription that meets these requirements, you can [create a free Azure account here](https://azure.microsoft.com/en-us/free/?b=17.06).</span></span> <span data-ttu-id="ac514-119">註冊 Azure Stack 不會對您的 Azure 訂用帳戶收取任何費用。</span><span class="sxs-lookup"><span data-stu-id="ac514-119">Registering Azure Stack incurs no cost on your Azure subscription.</span></span>



## <a name="register-azure-stack-resource-provider-in-azure"></a><span data-ttu-id="ac514-120">在 Azure 中註冊 Azure Stack 資源提供者</span><span class="sxs-lookup"><span data-stu-id="ac514-120">Register Azure Stack resource provider in Azure</span></span>
> [!NOTE] 
> <span data-ttu-id="ac514-121">此步驟只需要 toobe 完成一次在 Azure 堆疊環境中。</span><span class="sxs-lookup"><span data-stu-id="ac514-121">This step only needs toobe completed once in an Azure Stack environment.</span></span>
>

1. <span data-ttu-id="ac514-122">以系統管理員身分啟動 PowerShell ISE。</span><span class="sxs-lookup"><span data-stu-id="ac514-122">Start Powershell ISE as an administrator.</span></span>
2. <span data-ttu-id="ac514-123">登入 Azure 帳戶擁有者之 hello toohello Azure 訂用帳戶-EnvironmentName 參數設定得 「 AzureCloud"。</span><span class="sxs-lookup"><span data-stu-id="ac514-123">Log in toohello Azure account that is an owner of hello Azure subscription with -EnvironmentName parameter set too"AzureCloud".</span></span>
3. <span data-ttu-id="ac514-124">註冊 hello Azure 資源提供者 」 Microsoft.AzureStack"。</span><span class="sxs-lookup"><span data-stu-id="ac514-124">Register hello Azure resource provider "Microsoft.AzureStack".</span></span>

<span data-ttu-id="ac514-125">範例：</span><span class="sxs-lookup"><span data-stu-id="ac514-125">Example:</span></span> 
```Powershell
Login-AzureRmAccount -EnvironmentName "AzureCloud"
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.AzureStack -Force
```


## <a name="register-azure-stack-with-azure"></a><span data-ttu-id="ac514-126">向 Azure 註冊 Azure Stack</span><span class="sxs-lookup"><span data-stu-id="ac514-126">Register Azure Stack with Azure</span></span>

> [!NOTE]
><span data-ttu-id="ac514-127">所有的這些步驟必須完成 hello 主機電腦上。</span><span class="sxs-lookup"><span data-stu-id="ac514-127">All these steps must be completed on hello host computer.</span></span>
>

1. <span data-ttu-id="ac514-128">[安裝適用於 Azure Stack 的 PowerShell](azure-stack-powershell-install.md)。</span><span class="sxs-lookup"><span data-stu-id="ac514-128">[Install PowerShell for Azure Stack](azure-stack-powershell-install.md).</span></span> 
2. <span data-ttu-id="ac514-129">複製 hello [RegisterWithAzure.ps1 指令碼](https://go.microsoft.com/fwlink/?linkid=842959)tooa 資料夾 （例如 C:\Temp)。</span><span class="sxs-lookup"><span data-stu-id="ac514-129">Copy hello [RegisterWithAzure.ps1 script](https://go.microsoft.com/fwlink/?linkid=842959) tooa folder (such as C:\Temp).</span></span>
3. <span data-ttu-id="ac514-130">以系統管理員身分啟動 PowerShell ISE。</span><span class="sxs-lookup"><span data-stu-id="ac514-130">Start PowerShell ISE as an administrator.</span></span>    
4. <span data-ttu-id="ac514-131">執行 hello RegisterWithAzure.ps1 指令碼，取代下列預留位置 hello:</span><span class="sxs-lookup"><span data-stu-id="ac514-131">Run hello RegisterWithAzure.ps1 script, replacing hello following placeholders:</span></span>
    - <span data-ttu-id="ac514-132">*YourAccountName* hello hello Azure 訂用帳戶擁有者</span><span class="sxs-lookup"><span data-stu-id="ac514-132">*YourAccountName* is hello owner of hello Azure subscription</span></span>
    - <span data-ttu-id="ac514-133">*YourID*是您想要 toouse tooregister Azure 堆疊的 hello Azure 訂用帳戶 ID</span><span class="sxs-lookup"><span data-stu-id="ac514-133">*YourID* is hello Azure subscription ID that you want toouse tooregister Azure Stack</span></span>
    - <span data-ttu-id="ac514-134">*YourDirectory* hello 您 Azure 訂用帳戶所屬的 Azure Active Directory 租用戶名稱。</span><span class="sxs-lookup"><span data-stu-id="ac514-134">*YourDirectory* is hello name of your Azure Active Directory tenant that your Azure subscription is a part of.</span></span>

    ```powershell
    RegisterWithAzure.ps1 -azureSubscriptionId YourID -azureDirectoryTenantName YourDirectory -azureAccountId YourAccountName
    ```
    
    <span data-ttu-id="ac514-135">例如：</span><span class="sxs-lookup"><span data-stu-id="ac514-135">For example:</span></span>
    
    ```powershell
    C:\temp\RegisterWithAzure.ps1 -azureSubscriptionId "5e0ae55d-0b7a-47a3-afbc-8b372650abd3" `
    -azureDirectoryTenantName "contoso.onmicrosoft.com" `
    -azureAccountId serviceadmin@contoso.onmicrosoft.com
    ```
    
5. <span data-ttu-id="ac514-136">在 hello 兩個提示出現時，按 Enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="ac514-136">At hello two prompts, press Enter.</span></span>
6. <span data-ttu-id="ac514-137">在 hello 登入快顯視窗中，輸入您 Azure 訂用帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="ac514-137">In hello pop-up login window, enter your Azure subscription credentials.</span></span>

## <a name="verify-hello-registration"></a><span data-ttu-id="ac514-138">確認 hello 註冊</span><span class="sxs-lookup"><span data-stu-id="ac514-138">Verify hello registration</span></span>

1. <span data-ttu-id="ac514-139">登入 toohello 管理員入口網站 (https://adminportal.local.azurestack.external)。</span><span class="sxs-lookup"><span data-stu-id="ac514-139">Sign in toohello administrator portal (https://adminportal.local.azurestack.external).</span></span>
2. <span data-ttu-id="ac514-140">按一下 [更多服務]  >  [市集管理]  >  [從 Azure 新增]。</span><span class="sxs-lookup"><span data-stu-id="ac514-140">Click **More Services** > **Marketplace Management** > **Add from Azure**.</span></span>
3. <span data-ttu-id="ac514-141">如果您看到 Azure 提供的項目清單 (例如 WordPress)，則表示啟用已成功。</span><span class="sxs-lookup"><span data-stu-id="ac514-141">If you see a list of items available from Azure (such as WordPress), your activation was successful.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ac514-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ac514-142">Next steps</span></span>

[<span data-ttu-id="ac514-143">連接 tooAzure 堆疊</span><span class="sxs-lookup"><span data-stu-id="ac514-143">Connect tooAzure Stack</span></span>](azure-stack-connect-azure-stack.md)

