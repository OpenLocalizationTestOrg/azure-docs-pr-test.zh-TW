---
title: "應用程式服務環境的 aaaCustom 設定"
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
ms.openlocfilehash: 3d140688c88b389e71bfdd465c418339cccab3a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="custom-configuration-settings-for-app-service-environments"></a><span data-ttu-id="f0f5c-103">App Service 環境的自訂組態設定</span><span class="sxs-lookup"><span data-stu-id="f0f5c-103">Custom configuration settings for App Service Environments</span></span>
## <a name="overview"></a><span data-ttu-id="f0f5c-104">概觀</span><span class="sxs-lookup"><span data-stu-id="f0f5c-104">Overview</span></span>
<span data-ttu-id="f0f5c-105">由於應用程式服務環境隔離的 tooa 單一客戶，有一些組態設定可以套用專門 tooApp 服務環境。</span><span class="sxs-lookup"><span data-stu-id="f0f5c-105">Because App Service Environments are isolated tooa single customer, there are certain configuration settings that can be applied exclusively tooApp Service Environments.</span></span> <span data-ttu-id="f0f5c-106">此文件編號 hello 各種可用的應用程式服務環境的特定自訂。</span><span class="sxs-lookup"><span data-stu-id="f0f5c-106">This article documents hello various specific customizations that are available for App Service Environments.</span></span>

<span data-ttu-id="f0f5c-107">如果您沒有 App Service 環境，請參閱[如何 tooCreate App Service 環境](app-service-web-how-to-create-an-app-service-environment.md)。</span><span class="sxs-lookup"><span data-stu-id="f0f5c-107">If you do not have an App Service Environment, see [How tooCreate an App Service Environment](app-service-web-how-to-create-an-app-service-environment.md).</span></span>

<span data-ttu-id="f0f5c-108">您可以將 App Service 環境的自訂內容儲存利用陣列中的 hello 新**clusterSettings**屬性。</span><span class="sxs-lookup"><span data-stu-id="f0f5c-108">You can store App Service Environment customizations by using an array in hello new **clusterSettings** attribute.</span></span> <span data-ttu-id="f0f5c-109">這個屬性的 hello 的 hello 「 屬性 」 目錄中找到*hostingEnvironments* Azure 資源管理員實體。</span><span class="sxs-lookup"><span data-stu-id="f0f5c-109">This attribute is found in hello "Properties" dictionary of hello *hostingEnvironments* Azure Resource Manager entity.</span></span>

<span data-ttu-id="f0f5c-110">hello 下列縮寫的資源管理員範本程式碼片段示範 hello **clusterSettings**屬性：</span><span class="sxs-lookup"><span data-stu-id="f0f5c-110">hello following abbreviated Resource Manager template snippet shows hello **clusterSettings** attribute:</span></span>

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

<span data-ttu-id="f0f5c-111">hello **clusterSettings**屬性可以包含在資源管理員範本 tooupdate hello App Service 環境。</span><span class="sxs-lookup"><span data-stu-id="f0f5c-111">hello **clusterSettings** attribute can be included in a Resource Manager template tooupdate hello App Service Environment.</span></span>

## <a name="use-azure-resource-explorer-tooupdate-an-app-service-environment"></a><span data-ttu-id="f0f5c-112">使用 Azure 資源總管 tooupdate App Service 環境</span><span class="sxs-lookup"><span data-stu-id="f0f5c-112">Use Azure Resource Explorer tooupdate an App Service Environment</span></span>
<span data-ttu-id="f0f5c-113">或者，您可以藉由更新 App Service 環境的 hello [Azure 資源總管](https://resources.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="f0f5c-113">Alternatively, you can update hello App Service Environment by using [Azure Resource Explorer](https://resources.azure.com).</span></span>  

1. <span data-ttu-id="f0f5c-114">在資源總管中，請移至 App Service 環境的 hello toohello 節點 (**訂閱** > **resourceGroups** > **提供者** > **Microsoft.Web** > **hostingEnvironments**)。</span><span class="sxs-lookup"><span data-stu-id="f0f5c-114">In Resource Explorer, go toohello node for hello App Service Environment (**subscriptions** > **resourceGroups** > **providers** > **Microsoft.Web** > **hostingEnvironments**).</span></span> <span data-ttu-id="f0f5c-115">然後按一下 hello 想 tooupdate 特定 App Service 環境。</span><span class="sxs-lookup"><span data-stu-id="f0f5c-115">Then click hello specific App Service Environment that you want tooupdate.</span></span>
2. <span data-ttu-id="f0f5c-116">Hello 右窗格中，按一下 **讀/寫**hello 上方工具列 tooallow 互動式編輯在 資源總管 中。</span><span class="sxs-lookup"><span data-stu-id="f0f5c-116">In hello right pane, click **Read/Write** in hello upper toolbar tooallow interactive editing in Resource Explorer.</span></span>  
3. <span data-ttu-id="f0f5c-117">按一下藍色 hello**編輯**按鈕 toomake hello 資源管理員範本可編輯。</span><span class="sxs-lookup"><span data-stu-id="f0f5c-117">Click hello blue **Edit** button toomake hello Resource Manager template editable.</span></span>
4. <span data-ttu-id="f0f5c-118">捲動 toohello hello 右窗格的底部。</span><span class="sxs-lookup"><span data-stu-id="f0f5c-118">Scroll toohello bottom of hello right pane.</span></span> <span data-ttu-id="f0f5c-119">hello **clusterSettings**屬性位於 hello 最底部，您可以在其中輸入或更新其值。</span><span class="sxs-lookup"><span data-stu-id="f0f5c-119">hello **clusterSettings** attribute is at hello very bottom, where you can enter or update its value.</span></span>
5. <span data-ttu-id="f0f5c-120">您想在 hello 的組態值的類型 （或複製和貼上） hello 陣列**clusterSettings**屬性。</span><span class="sxs-lookup"><span data-stu-id="f0f5c-120">Type (or copy and paste) hello array of configuration values you want in hello **clusterSettings** attribute.</span></span>  
6. <span data-ttu-id="f0f5c-121">按一下綠色的 hello**放**按鈕，在 hello 右窗格 toocommit hello 變更 toohello App Service 環境的 hello 頂端找到。</span><span class="sxs-lookup"><span data-stu-id="f0f5c-121">Click hello green **PUT** button that's located at hello top of hello right pane toocommit hello change toohello App Service Environment.</span></span>

<span data-ttu-id="f0f5c-122">不過您送出 hello 變更時，所花大約 30 分鐘乘以前端 hello App Service 環境的 hello 變更 tootake 作用中的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="f0f5c-122">However you submit hello change, it takes roughly 30 minutes multiplied by hello number of front ends in hello App Service Environment for hello change tootake effect.</span></span>
<span data-ttu-id="f0f5c-123">例如，如果 App Service 環境有四個前端，它會使用 hello 組態更新 toofinish 約兩小時後。</span><span class="sxs-lookup"><span data-stu-id="f0f5c-123">For example, if an App Service Environment has four front ends, it will take roughly two hours for hello configuration update toofinish.</span></span> <span data-ttu-id="f0f5c-124">雖然 hello 組態變更正在推出，沒有其他的縮放作業或組態變更作業可能需要 hello App Service 環境中的位置。</span><span class="sxs-lookup"><span data-stu-id="f0f5c-124">While hello configuration change is being rolled out, no other scaling operations or configuration change operations can take place in hello App Service Environment.</span></span>

## <a name="disable-tls-10"></a><span data-ttu-id="f0f5c-125">停用 TLS 1.0</span><span class="sxs-lookup"><span data-stu-id="f0f5c-125">Disable TLS 1.0</span></span>
<span data-ttu-id="f0f5c-126">來自客戶的週期性問題，特別是在處理的 PCI 合規性客戶稽核，是如何 tooexplicitly 停用 TLS 1.0 的自己的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f0f5c-126">A recurring question from customers, especially customers who are dealing with PCI compliance audits, is how tooexplicitly disable TLS 1.0 for their apps.</span></span>

<span data-ttu-id="f0f5c-127">您可以停用 TLS 1.0 透過 hello 下列**clusterSettings**項目：</span><span class="sxs-lookup"><span data-stu-id="f0f5c-127">TLS 1.0 can be disabled through hello following **clusterSettings** entry:</span></span>

        "clusterSettings": [
            {
                "name": "DisableTls1.0",
                "value": "1"
            }
        ],

## <a name="change-tls-cipher-suite-order"></a><span data-ttu-id="f0f5c-128">變更 TLS 加密套件順序</span><span class="sxs-lookup"><span data-stu-id="f0f5c-128">Change TLS cipher suite order</span></span>
<span data-ttu-id="f0f5c-129">來自客戶的另一個問題就是它們可以修改其伺服器所交涉的加密方式 hello 清單，並且這可藉由修改 hello **clusterSettings**如下所示。</span><span class="sxs-lookup"><span data-stu-id="f0f5c-129">Another question from customers is if they can modify hello list of ciphers negotiated by their server and this can be achieved by modifying hello **clusterSettings** as shown below.</span></span> <span data-ttu-id="f0f5c-130">可以從擷取可用的加密套件 hello 清單[MSDN 本文](https://msdn.microsoft.com/library/windows/desktop/aa374757\(v=vs.85\).aspx)。</span><span class="sxs-lookup"><span data-stu-id="f0f5c-130">hello list of cipher suites available can be retrieved from [this MSDN article](https://msdn.microsoft.com/library/windows/desktop/aa374757\(v=vs.85\).aspx).</span></span>

        "clusterSettings": [
            {
                "name": "FrontEndSSLCipherSuiteOrder",
                "value": "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384_P256,TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA_P256"
            }
        ],

> [!WARNING]
> <span data-ttu-id="f0f5c-131">安全通道不了解的 hello 加密套件設定不正確的值，如果所有 TLS 通訊 tooyour 伺服器可能會都停止運作。</span><span class="sxs-lookup"><span data-stu-id="f0f5c-131">If incorrect values are set for hello cipher suite that SChannel cannot understand, all TLS communication tooyour server might stop functioning.</span></span> <span data-ttu-id="f0f5c-132">在此情況下，您將需要 tooremove hello *FrontEndSSLCipherSuiteOrder*項目從**clusterSettings**並送出 hello 更新資源管理員範本 toorevert 後 toohello 預設加密套件設定。</span><span class="sxs-lookup"><span data-stu-id="f0f5c-132">In such a case, you will need tooremove hello *FrontEndSSLCipherSuiteOrder* entry from **clusterSettings** and submit hello updated Resource Manager template toorevert back toohello default cipher suite settings.</span></span>  <span data-ttu-id="f0f5c-133">請謹慎使用這項功能。</span><span class="sxs-lookup"><span data-stu-id="f0f5c-133">Please use this functionality with caution.</span></span>
> 
> 

## <a name="get-started"></a><span data-ttu-id="f0f5c-134">開始使用</span><span class="sxs-lookup"><span data-stu-id="f0f5c-134">Get started</span></span>
<span data-ttu-id="f0f5c-135">hello Azure 快速入門資源管理員範本站台包含具有 hello 基底定義的範本[建立 App Service 環境](https://azure.microsoft.com/documentation/templates/201-web-app-ase-create/)。</span><span class="sxs-lookup"><span data-stu-id="f0f5c-135">hello Azure Quickstart Resource Manager template site includes a template with hello base definition for [creating an App Service Environment](https://azure.microsoft.com/documentation/templates/201-web-app-ase-create/).</span></span>

<!-- LINKS -->

<!-- IMAGES -->
