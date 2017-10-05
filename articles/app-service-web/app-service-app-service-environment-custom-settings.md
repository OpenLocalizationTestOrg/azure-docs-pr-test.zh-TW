---
title: "App Service 環境的自訂設定"
description: "App Service 環境的自訂組態設定"
services: app-service
documentationcenter: 
author: stefsch
manager: nirma
editor: 
ms.assetid: 1d1d85f3-6cc6-4d57-ae1a-5b37c642d812
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2016
ms.author: stefsch
ms.openlocfilehash: 687475fae0c90713c15e8abbb92b71059eae81c0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="custom-configuration-settings-for-app-service-environments"></a><span data-ttu-id="7fb4d-103">App Service 環境的自訂組態設定</span><span class="sxs-lookup"><span data-stu-id="7fb4d-103">Custom configuration settings for App Service Environments</span></span>
## <a name="overview"></a><span data-ttu-id="7fb4d-104">Overview</span><span class="sxs-lookup"><span data-stu-id="7fb4d-104">Overview</span></span>
<span data-ttu-id="7fb4d-105">因為 App Service 環境對單一客戶是隔離的，所以有某些專門套用到 App Service 環境的組態設定。</span><span class="sxs-lookup"><span data-stu-id="7fb4d-105">Because App Service Environments are isolated to a single customer, there are certain configuration settings that can be applied exclusively to App Service Environments.</span></span> <span data-ttu-id="7fb4d-106">本文記錄各種可供 App Service 環境使用的特定自訂。</span><span class="sxs-lookup"><span data-stu-id="7fb4d-106">This article documents the various specific customizations that are available for App Service Environments.</span></span>

<span data-ttu-id="7fb4d-107">如果您沒有 App Service 環境，請參閱 [如何建立 App Service 環境](app-service-web-how-to-create-an-app-service-environment.md)。</span><span class="sxs-lookup"><span data-stu-id="7fb4d-107">If you do not have an App Service Environment, see [How to Create an App Service Environment](app-service-web-how-to-create-an-app-service-environment.md).</span></span>

<span data-ttu-id="7fb4d-108">您可以使用新 **clusterSettings** 屬性的陣列儲存 App Service 環境自訂。</span><span class="sxs-lookup"><span data-stu-id="7fb4d-108">You can store App Service Environment customizations by using an array in the new **clusterSettings** attribute.</span></span> <span data-ttu-id="7fb4d-109">這個屬性是在 *hostingEnvironments* Azure Resource Manager 實體的「屬性」字典中找到的。</span><span class="sxs-lookup"><span data-stu-id="7fb4d-109">This attribute is found in the "Properties" dictionary of the *hostingEnvironments* Azure Resource Manager entity.</span></span>

<span data-ttu-id="7fb4d-110">下列縮寫的 Resource Manager 範本程式碼片段顯示 **clusterSettings** 屬性︰</span><span class="sxs-lookup"><span data-stu-id="7fb4d-110">The following abbreviated Resource Manager template snippet shows the **clusterSettings** attribute:</span></span>

    "resources": [
    {
       "apiVersion": "2015-08-01",
       "type": "Microsoft.Web/hostingEnvironments",
       "name": ...,
       "location": ...,
       "properties": {
          "clusterSettings": [
             {
                 "name": "nameOfCustomSetting",
                 "value": "valueOfCustomSetting"
             }
          ],
          "workerPools": [ ...],
          etc...
       }
    }

<span data-ttu-id="7fb4d-111">**clusterSettings** 屬性可以包含在 Resource Manager 範本中，以更新 App Service 環境。</span><span class="sxs-lookup"><span data-stu-id="7fb4d-111">The **clusterSettings** attribute can be included in a Resource Manager template to update the App Service Environment.</span></span>

## <a name="use-azure-resource-explorer-to-update-an-app-service-environment"></a><span data-ttu-id="7fb4d-112">使用 Azure 資源總管更新 App Service 環境</span><span class="sxs-lookup"><span data-stu-id="7fb4d-112">Use Azure Resource Explorer to update an App Service Environment</span></span>
<span data-ttu-id="7fb4d-113">或者，您可以使用 [Azure 資源總管](https://resources.azure.com)更新 App Service 環境。</span><span class="sxs-lookup"><span data-stu-id="7fb4d-113">Alternatively, you can update the App Service Environment by using [Azure Resource Explorer](https://resources.azure.com).</span></span>  

1. <span data-ttu-id="7fb4d-114">在 [資源總管] 中，移至 App Service 環境的節點 ([訂用帳戶] > [resourceGroups] > [提供者] > [Microsoft.Web] > [hostingEnvironments])。</span><span class="sxs-lookup"><span data-stu-id="7fb4d-114">In Resource Explorer, go to the node for the App Service Environment (**subscriptions** > **resourceGroups** > **providers** > **Microsoft.Web** > **hostingEnvironments**).</span></span> <span data-ttu-id="7fb4d-115">接著，按一下您想要更新的特定 App Service 環境。</span><span class="sxs-lookup"><span data-stu-id="7fb4d-115">Then click the specific App Service Environment that you want to update.</span></span>
2. <span data-ttu-id="7fb4d-116">按一下右窗格上方工具列中的 [讀取/寫入]  ，允許在資源總管中進行互動式編輯。</span><span class="sxs-lookup"><span data-stu-id="7fb4d-116">In the right pane, click **Read/Write** in the upper toolbar to allow interactive editing in Resource Explorer.</span></span>  
3. <span data-ttu-id="7fb4d-117">按一下藍色的 [編輯]  按鈕，開放編輯 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="7fb4d-117">Click the blue **Edit** button to make the Resource Manager template editable.</span></span>
4. <span data-ttu-id="7fb4d-118">向下捲動到右窗格底部。</span><span class="sxs-lookup"><span data-stu-id="7fb4d-118">Scroll to the bottom of the right pane.</span></span> <span data-ttu-id="7fb4d-119">**clusterSettings** 屬性位在最底部，您可以在此輸入或更新其值。</span><span class="sxs-lookup"><span data-stu-id="7fb4d-119">The **clusterSettings** attribute is at the very bottom, where you can enter or update its value.</span></span>
5. <span data-ttu-id="7fb4d-120">輸入 (或複製並貼上) 您希望 **clusterSettings** 屬性出現的組態值陣列。</span><span class="sxs-lookup"><span data-stu-id="7fb4d-120">Type (or copy and paste) the array of configuration values you want in the **clusterSettings** attribute.</span></span>  
6. <span data-ttu-id="7fb4d-121">按一下右窗格上方的綠色 [PUT]  按鈕，確認 App Service 環境的變更。</span><span class="sxs-lookup"><span data-stu-id="7fb4d-121">Click the green **PUT** button that's located at the top of the right pane to commit the change to the App Service Environment.</span></span>

<span data-ttu-id="7fb4d-122">不過，送出變更後，約需 30 分鐘乘以 App Service 環境中前端數量的時間，變更才會生效。</span><span class="sxs-lookup"><span data-stu-id="7fb4d-122">However you submit the change, it takes roughly 30 minutes multiplied by the number of front ends in the App Service Environment for the change to take effect.</span></span>
<span data-ttu-id="7fb4d-123">例如，如果 App Service 環境有四個前端，大約需要兩個小時才能完成組態更新。</span><span class="sxs-lookup"><span data-stu-id="7fb4d-123">For example, if an App Service Environment has four front ends, it will take roughly two hours for the configuration update to finish.</span></span> <span data-ttu-id="7fb4d-124">實行組態變更時，App Service 環境上就不會進行其他調整作業或組態變更作業。</span><span class="sxs-lookup"><span data-stu-id="7fb4d-124">While the configuration change is being rolled out, no other scaling operations or configuration change operations can take place in the App Service Environment.</span></span>

## <a name="disable-tls-10"></a><span data-ttu-id="7fb4d-125">停用 TLS 1.0</span><span class="sxs-lookup"><span data-stu-id="7fb4d-125">Disable TLS 1.0</span></span>
<span data-ttu-id="7fb4d-126">客戶的常見問題是，尤其是處理 PCI 規範稽核的客戶，如何明確停用其應用程式的 TLS 1.0。</span><span class="sxs-lookup"><span data-stu-id="7fb4d-126">A recurring question from customers, especially customers who are dealing with PCI compliance audits, is how to explicitly disable TLS 1.0 for their apps.</span></span>

<span data-ttu-id="7fb4d-127">透過下列 **clusterSettings** 項目可以停用 TLS 1.0︰</span><span class="sxs-lookup"><span data-stu-id="7fb4d-127">TLS 1.0 can be disabled through the following **clusterSettings** entry:</span></span>

        "clusterSettings": [
            {
                "name": "DisableTls1.0",
                "value": "1"
            }
        ],

## <a name="change-tls-cipher-suite-order"></a><span data-ttu-id="7fb4d-128">變更 TLS 加密套件順序</span><span class="sxs-lookup"><span data-stu-id="7fb4d-128">Change TLS cipher suite order</span></span>
<span data-ttu-id="7fb4d-129">來自客戶的另一個問題是，他們是否可以修改由其伺服器交涉的加密的清單，而這可透過修改 **clusterSettings** 來達成，如下所示。</span><span class="sxs-lookup"><span data-stu-id="7fb4d-129">Another question from customers is if they can modify the list of ciphers negotiated by their server and this can be achieved by modifying the **clusterSettings** as shown below.</span></span> <span data-ttu-id="7fb4d-130">您可以從[此 MSDN 文章](https://msdn.microsoft.com/library/windows/desktop/aa374757\(v=vs.85\).aspx)擷取可用加密套件的清單。</span><span class="sxs-lookup"><span data-stu-id="7fb4d-130">The list of cipher suites available can be retrieved from [this MSDN article](https://msdn.microsoft.com/library/windows/desktop/aa374757\(v=vs.85\).aspx).</span></span>

        "clusterSettings": [
            {
                "name": "FrontEndSSLCipherSuiteOrder",
                "value": "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384_P256,TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA_P256"
            }
        ],

> [!WARNING]
> <span data-ttu-id="7fb4d-131">如果對安全通道無法了解的加密套件設定了不正確的值，對您的伺服器的所有 TLS 通訊可能會停止運作。</span><span class="sxs-lookup"><span data-stu-id="7fb4d-131">If incorrect values are set for the cipher suite that SChannel cannot understand, all TLS communication to your server might stop functioning.</span></span> <span data-ttu-id="7fb4d-132">在這種情況下，您必須從 **clusterSettings** 移除 FrontEndSSLCipherSuiteOrder 項目，並提交更新的 Resource Manager 範本以還原回預設的加密套件設定。</span><span class="sxs-lookup"><span data-stu-id="7fb4d-132">In such a case, you will need to remove the *FrontEndSSLCipherSuiteOrder* entry from **clusterSettings** and submit the updated Resource Manager template to revert back to the default cipher suite settings.</span></span>  <span data-ttu-id="7fb4d-133">請謹慎使用這項功能。</span><span class="sxs-lookup"><span data-stu-id="7fb4d-133">Please use this functionality with caution.</span></span>
> 
> 

## <a name="get-started"></a><span data-ttu-id="7fb4d-134">開始使用</span><span class="sxs-lookup"><span data-stu-id="7fb4d-134">Get started</span></span>
<span data-ttu-id="7fb4d-135">Azure 快速入門 Resource Manager 範本網站包含具有 [建立 App Service 環境](https://azure.microsoft.com/documentation/templates/201-web-app-ase-create/)基本定義的範本。</span><span class="sxs-lookup"><span data-stu-id="7fb4d-135">The Azure Quickstart Resource Manager template site includes a template with the base definition for [creating an App Service Environment](https://azure.microsoft.com/documentation/templates/201-web-app-ase-create/).</span></span>

<!-- LINKS -->

<!-- IMAGES -->
