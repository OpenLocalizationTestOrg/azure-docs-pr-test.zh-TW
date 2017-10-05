---
title: "註冊 Azure Stack | Microsoft Docs"
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
ms.openlocfilehash: f71ec571fee8e59ea9061cd619914b81a5bf701a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="register-azure-stack-with-your-azure-subscription"></a><span data-ttu-id="34527-103">使用您的 Azure 訂用帳戶註冊 Azure Stack</span><span class="sxs-lookup"><span data-stu-id="34527-103">Register Azure Stack with your Azure Subscription</span></span>

<span data-ttu-id="34527-104">針對 Azure Active Directory 部署，您可以使用 Azure 註冊 Azure Stack，以便從 Azure 下載市集項目，以及設定回報給 Microsoft 的商務資料。</span><span class="sxs-lookup"><span data-stu-id="34527-104">For Azure Active Directory deployments, you can register Azure Stack with Azure to download marketplace items from Azure and to set up commerce data reporting back to Microsoft.</span></span> 

> [!NOTE]
><span data-ttu-id="34527-105">我們建議您註冊，因為它可讓您測試重要的 Azure Stack 功能，例如市集摘要整合和使用方式報告。</span><span class="sxs-lookup"><span data-stu-id="34527-105">Registration is recommended because it enables you to test important Azure Stack functionality, like marketplace syndication and usage reporting.</span></span> <span data-ttu-id="34527-106">註冊 Azure Stack 之後，使用方式會回報給 Azure 商務。</span><span class="sxs-lookup"><span data-stu-id="34527-106">After you register Azure Stack, usage is reported to Azure commerce.</span></span> <span data-ttu-id="34527-107">您可以在註冊時所使用的訂用帳戶下看到這項資訊。</span><span class="sxs-lookup"><span data-stu-id="34527-107">You can see it under the subscription you used for registration.</span></span> <span data-ttu-id="34527-108">Azure Stack 開發套件使用者將不需針對回報的任何使用方式支付費用。</span><span class="sxs-lookup"><span data-stu-id="34527-108">Azure Stack Development Kit users will not be charged for any usage they report.</span></span>
>


## <a name="get-azure-subscription"></a><span data-ttu-id="34527-109">取得 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="34527-109">Get Azure subscription</span></span>

<span data-ttu-id="34527-110">使用 Azure 註冊 Azure Stack 之前，您必須：</span><span class="sxs-lookup"><span data-stu-id="34527-110">Before registering Azure Stack with Azure, you must have:</span></span>

- <span data-ttu-id="34527-111">Azure 訂用帳戶的訂用帳戶 ID。</span><span class="sxs-lookup"><span data-stu-id="34527-111">The subscription ID for an Azure subscription.</span></span> <span data-ttu-id="34527-112">若要取得 ID，請登入 Azure 並按一下 [更多服務]  >  [訂用帳戶]，然後按一下您要使用的訂用帳戶，便可以在 [基本資訊] 下找到 [訂用帳戶 ID]。</span><span class="sxs-lookup"><span data-stu-id="34527-112">To get the ID, sign in to Azure, click **More services** > **Subscriptions**, click the subscription you want to use, and under **Essentials** you can find the **Subscription ID**.</span></span> <span data-ttu-id="34527-113">目前不支援中國、德國，和美國政府雲端訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="34527-113">China, Germany, and US government cloud subscriptions are not currently supported.</span></span>
- <span data-ttu-id="34527-114">訂用帳戶擁有者的帳戶使用者名稱和密碼 (支援 MSA/2FA 帳戶)</span><span class="sxs-lookup"><span data-stu-id="34527-114">The username and password for an account that is an owner for the subscription (MSA/2FA accounts are supported)</span></span>
- <span data-ttu-id="34527-115">Azure 訂用帳戶的 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="34527-115">The Azure Active Directory for the Azure subscription.</span></span> <span data-ttu-id="34527-116">您可以將游標暫留在 Azure 入口網站右上角的顯示圖片，即可在 Azure 中找到此目錄。</span><span class="sxs-lookup"><span data-stu-id="34527-116">You can find this directory in Azure by hovering over your avatar at the top right corner of the Azure portal.</span></span> 
- <span data-ttu-id="34527-117">註冊 Azure Stack 資源提供者 (請參閱下方的**註冊 Azure Stack 資源提供者**區段以取得詳細資料)</span><span class="sxs-lookup"><span data-stu-id="34527-117">Registered the Azure Stack resource provider (see the **Register Azure Stack Resource Provider** section below for details)</span></span>

<span data-ttu-id="34527-118">如果您沒有符合這些需求的 Azure 訂用帳戶，則可以[在這裡建立免費的 Azure 帳戶](https://azure.microsoft.com/en-us/free/?b=17.06)。</span><span class="sxs-lookup"><span data-stu-id="34527-118">If you don’t have an Azure subscription that meets these requirements, you can [create a free Azure account here](https://azure.microsoft.com/en-us/free/?b=17.06).</span></span> <span data-ttu-id="34527-119">註冊 Azure Stack 不會對您的 Azure 訂用帳戶收取任何費用。</span><span class="sxs-lookup"><span data-stu-id="34527-119">Registering Azure Stack incurs no cost on your Azure subscription.</span></span>



## <a name="register-azure-stack-resource-provider-in-azure"></a><span data-ttu-id="34527-120">在 Azure 中註冊 Azure Stack 資源提供者</span><span class="sxs-lookup"><span data-stu-id="34527-120">Register Azure Stack resource provider in Azure</span></span>
> [!NOTE] 
> <span data-ttu-id="34527-121">此步驟僅需在 Azure Stack 環境中完成一次。</span><span class="sxs-lookup"><span data-stu-id="34527-121">This step only needs to be completed once in an Azure Stack environment.</span></span>
>

1. <span data-ttu-id="34527-122">以系統管理員身分啟動 PowerShell ISE。</span><span class="sxs-lookup"><span data-stu-id="34527-122">Start Powershell ISE as an administrator.</span></span>
2. <span data-ttu-id="34527-123">透過將 -EnvironmentName 參數設定為「AzureCloud」以登入至 Azure 訂用帳戶擁有者的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="34527-123">Log in to the Azure account that is an owner of the Azure subscription with -EnvironmentName parameter set to "AzureCloud".</span></span>
3. <span data-ttu-id="34527-124">註冊 Azure 資源提供者「Microsoft.AzureStack」。</span><span class="sxs-lookup"><span data-stu-id="34527-124">Register the Azure resource provider "Microsoft.AzureStack".</span></span>

<span data-ttu-id="34527-125">範例：</span><span class="sxs-lookup"><span data-stu-id="34527-125">Example:</span></span> 
```Powershell
Login-AzureRmAccount -EnvironmentName "AzureCloud"
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.AzureStack -Force
```


## <a name="register-azure-stack-with-azure"></a><span data-ttu-id="34527-126">向 Azure 註冊 Azure Stack</span><span class="sxs-lookup"><span data-stu-id="34527-126">Register Azure Stack with Azure</span></span>

> [!NOTE]
><span data-ttu-id="34527-127">這些所有步驟必須在主機電腦上完成。</span><span class="sxs-lookup"><span data-stu-id="34527-127">All these steps must be completed on the host computer.</span></span>
>

1. <span data-ttu-id="34527-128">[安裝 Azure Stack 適用的 PowerShell](azure-stack-powershell-install.md)。</span><span class="sxs-lookup"><span data-stu-id="34527-128">[Install PowerShell for Azure Stack](azure-stack-powershell-install.md).</span></span> 
2. <span data-ttu-id="34527-129">將 [RegisterWithAzure.ps1 指令碼](https://go.microsoft.com/fwlink/?linkid=842959)複製至資料夾 (例如 C:\Temp)。</span><span class="sxs-lookup"><span data-stu-id="34527-129">Copy the [RegisterWithAzure.ps1 script](https://go.microsoft.com/fwlink/?linkid=842959) to a folder (such as C:\Temp).</span></span>
3. <span data-ttu-id="34527-130">以系統管理員身分啟動 PowerShell ISE。</span><span class="sxs-lookup"><span data-stu-id="34527-130">Start PowerShell ISE as an administrator.</span></span>    
4. <span data-ttu-id="34527-131">執行 RegisterWithAzure.ps1 指令碼以取代下列預留位置：</span><span class="sxs-lookup"><span data-stu-id="34527-131">Run the RegisterWithAzure.ps1 script, replacing the following placeholders:</span></span>
    - <span data-ttu-id="34527-132">YourAccountName 是 Azure 訂用帳戶的擁有者</span><span class="sxs-lookup"><span data-stu-id="34527-132">*YourAccountName* is the owner of the Azure subscription</span></span>
    - <span data-ttu-id="34527-133">YourID 是您要用來註冊 Azure Stack 的 Azure 訂用帳戶 ID</span><span class="sxs-lookup"><span data-stu-id="34527-133">*YourID* is the Azure subscription ID that you want to use to register Azure Stack</span></span>
    - <span data-ttu-id="34527-134">YourDirectory 是您 Azure 訂用帳戶所屬 Azure Active Directory 租用戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="34527-134">*YourDirectory* is the name of your Azure Active Directory tenant that your Azure subscription is a part of.</span></span>

    ```powershell
    RegisterWithAzure.ps1 -azureSubscriptionId YourID -azureDirectoryTenantName YourDirectory -azureAccountId YourAccountName
    ```
    
    <span data-ttu-id="34527-135">例如：</span><span class="sxs-lookup"><span data-stu-id="34527-135">For example:</span></span>
    
    ```powershell
    C:\temp\RegisterWithAzure.ps1 -azureSubscriptionId "5e0ae55d-0b7a-47a3-afbc-8b372650abd3" `
    -azureDirectoryTenantName "contoso.onmicrosoft.com" `
    -azureAccountId serviceadmin@contoso.onmicrosoft.com
    ```
    
5. <span data-ttu-id="34527-136">出現兩個提示時，按 Enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="34527-136">At the two prompts, press Enter.</span></span>
6. <span data-ttu-id="34527-137">在彈出的登入視窗中，輸入您的 Azure 訂用帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="34527-137">In the pop-up login window, enter your Azure subscription credentials.</span></span>

## <a name="verify-the-registration"></a><span data-ttu-id="34527-138">確認註冊</span><span class="sxs-lookup"><span data-stu-id="34527-138">Verify the registration</span></span>

1. <span data-ttu-id="34527-139">登入系統管理員入口網站 (https://adminportal.local.azurestack.external)。</span><span class="sxs-lookup"><span data-stu-id="34527-139">Sign in to the administrator portal (https://adminportal.local.azurestack.external).</span></span>
2. <span data-ttu-id="34527-140">按一下 [更多服務]  >  [市集管理]  >  [從 Azure 新增]。</span><span class="sxs-lookup"><span data-stu-id="34527-140">Click **More Services** > **Marketplace Management** > **Add from Azure**.</span></span>
3. <span data-ttu-id="34527-141">如果您看到 Azure 提供的項目清單 (例如 WordPress)，則表示啟用已成功。</span><span class="sxs-lookup"><span data-stu-id="34527-141">If you see a list of items available from Azure (such as WordPress), your activation was successful.</span></span>

## <a name="next-steps"></a><span data-ttu-id="34527-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="34527-142">Next steps</span></span>

[<span data-ttu-id="34527-143">連接至 Azure Stack</span><span class="sxs-lookup"><span data-stu-id="34527-143">Connect to Azure Stack</span></span>](azure-stack-connect-azure-stack.md)

