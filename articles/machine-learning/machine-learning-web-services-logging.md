---
title: "Machine Learning Web 服務的記錄 | Microsoft Docs"
description: "了解如何為 Machine Learning Web 服務啟用記錄。 記錄提供可協助疑難排解 API 的其他資訊。"
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: c54d41e1-0300-46ef-bbfc-d6f7dca85086
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/15/2017
ms.author: raymondl;garye
ms.openlocfilehash: 7d0b2db01427430d6b0a317cdfefc265dd4b06e2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="enable-logging-for-machine-learning-web-services"></a><span data-ttu-id="01b67-104">為 Machine Learning Web 服務啟用記錄</span><span class="sxs-lookup"><span data-stu-id="01b67-104">Enable logging for Machine Learning web services</span></span>
<span data-ttu-id="01b67-105">本文件提供 Machine Learning Web 服務記錄功能的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="01b67-105">This document provides information on the logging capability of Machine Learning web services.</span></span> <span data-ttu-id="01b67-106">記錄會提供其他資訊，而不只是錯誤碼和訊息而已，可協助您針對 Machine Learning API 的呼叫進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="01b67-106">Logging provides additional information, beyond just an error number and a message, that can help you troubleshoot your calls to the Machine Learning APIs.</span></span>  

## <a name="how-to-enable-logging-for-a-web-service"></a><span data-ttu-id="01b67-107">如何為 Web 服務啟用記錄</span><span class="sxs-lookup"><span data-stu-id="01b67-107">How to enable logging for a Web service</span></span>

<span data-ttu-id="01b67-108">從 [Azure Machine Learning Web 服務](https://services.azureml.net)入口網站啟用記錄。</span><span class="sxs-lookup"><span data-stu-id="01b67-108">You enable logging from the [Azure Machine Learning Web Services](https://services.azureml.net) portal.</span></span> 

1. <span data-ttu-id="01b67-109">登入 Azure Machine Learning Web 服務入口網站 [https://services.azureml.net](https://services.azureml.net)。</span><span class="sxs-lookup"><span data-stu-id="01b67-109">Sign in to the Azure Machine Learning Web Services portal at [https://services.azureml.net](https://services.azureml.net).</span></span> <span data-ttu-id="01b67-110">對於傳統 Web 服務，您也可以在 Machine Learning Studio 中的 Machine Learning Web 服務頁面上按一下 [新的 Web 服務體驗]，以進入入口網站。</span><span class="sxs-lookup"><span data-stu-id="01b67-110">For a Classic web service, you can also get to the portal by clicking **New Web Services Experience** on the Machine Learning Web Services page in Machine Learning Studio.</span></span>

   ![新的 Web 服務體驗連結](media/machine-learning-web-services-logging/new-web-services-experience-link.png)

2. <span data-ttu-id="01b67-112">在頂端的功能表列上，按一下 [Web 服務] 以取得新的 Web 服務，或按一下 [傳統 Web 服務] 以取得傳統 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="01b67-112">On the top menu bar, click **Web Services** for a New web service, or click **Classic Web Services** for a Classic web service.</span></span>

   ![選取新的或傳統 Web 服務](media/machine-learning-web-services-logging/select-web-service.png)

3. <span data-ttu-id="01b67-114">對於新的 Web 服務，按一下 Web 服務名稱。</span><span class="sxs-lookup"><span data-stu-id="01b67-114">For a New web service, click the web service name.</span></span> <span data-ttu-id="01b67-115">對於傳統 Web 服務，按一下 Web 服務名稱，然後在下一個頁面中按一下適當的端點。</span><span class="sxs-lookup"><span data-stu-id="01b67-115">For a Classic web service, click the web service name and then on the next page click the appropriate endpoint.</span></span>

4. <span data-ttu-id="01b67-116">按一下頂端功能表列上的 [設定]。</span><span class="sxs-lookup"><span data-stu-id="01b67-116">On the top menu bar, click **Configure**.</span></span>

5. <span data-ttu-id="01b67-117">將 **[啟用記錄]** 選項設定為 *[錯誤]* \(僅記錄錯誤) 或 *[所有]* \(適用於完整記錄)。</span><span class="sxs-lookup"><span data-stu-id="01b67-117">Set the **Enable Logging** option to *Error* (to log only errors) or *All* (for full logging).</span></span>

   ![選取記錄等級](media/machine-learning-web-services-logging/enable-logging.png)

6. <span data-ttu-id="01b67-119">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="01b67-119">Click **Save**.</span></span>

7. <span data-ttu-id="01b67-120">對於傳統 Web 服務，請建立 **ml-診斷**容器。</span><span class="sxs-lookup"><span data-stu-id="01b67-120">For Classic web services, create the **ml-diagnostics** container.</span></span>

   <span data-ttu-id="01b67-121">所有的 Web 服務記錄會保存在與 Web 服務相關聯的儲存體帳戶中名為 **ml-診斷**的 blob 容器中。</span><span class="sxs-lookup"><span data-stu-id="01b67-121">All web service logs are kept in a blob container named **ml-diagnostics** in the storage account associated with the web service.</span></span> <span data-ttu-id="01b67-122">對於新的 Web 服務，此容器會在您第一次存取 Web 服務時建立。</span><span class="sxs-lookup"><span data-stu-id="01b67-122">For New web services, this container is created the first time you access the web service.</span></span> <span data-ttu-id="01b67-123">對於傳統 Web 服務，如果容器不存在，則您需要建立容器。</span><span class="sxs-lookup"><span data-stu-id="01b67-123">For Classic web services, you need to create the container if it doesn't already exist.</span></span> 

   1. <span data-ttu-id="01b67-124">在 [Azure 入口網站](https://portal.azure.com)中，移至與 Web 服務相關聯的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="01b67-124">In the [Azure portal](https://portal.azure.com), go to the storage account associated with the web service.</span></span>

   2. <span data-ttu-id="01b67-125">在 [Blob 服務] 下，按一下 [容器]。</span><span class="sxs-lookup"><span data-stu-id="01b67-125">Under **Blob Service**, click **Containers**.</span></span>

   3. <span data-ttu-id="01b67-126">如果容器 **ml-診斷**不存在，按一下 [+ 容器]，將容器命名為「ml-診斷」，[存取型別] 選取「Blob」。</span><span class="sxs-lookup"><span data-stu-id="01b67-126">If the container **ml-diagnostics** doesn't exist, click **+Container**, give the container the name "ml-diagnostics", and select the **Access type** as "Blob".</span></span> <span data-ttu-id="01b67-127">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="01b67-127">Click **OK**.</span></span>

      ![選取記錄等級](media/machine-learning-web-services-logging/create-ml-diagnostics-container.png)

> [!TIP]
>
> <span data-ttu-id="01b67-129">對於傳統 Web 服務，Machine Learning Studio 中的 Web 服務儀表板也有啟用記錄的參數。</span><span class="sxs-lookup"><span data-stu-id="01b67-129">For a Classic web service, the Web Services Dashboard in Machine Learning Studio also has a switch to enable logging.</span></span> <span data-ttu-id="01b67-130">不過，由於記錄現在是透過 Web 服務入口網站所管理，您需要透過入口網站來啟用記錄，如本文所述。</span><span class="sxs-lookup"><span data-stu-id="01b67-130">However, because logging is now managed through the Web Services portal, you need to enable logging through the portal as described in this article.</span></span> <span data-ttu-id="01b67-131">如果您已在 Studio 中啟用記錄，請在 Web 服務入口網站中停用記錄，然後再次啟用。</span><span class="sxs-lookup"><span data-stu-id="01b67-131">If you already enabled logging in Studio, then in the Web Services Portal, disable logging and enable it again.</span></span>


## <a name="the-effects-of-enabling-logging"></a><span data-ttu-id="01b67-132">啟用記錄的效果</span><span class="sxs-lookup"><span data-stu-id="01b67-132">The effects of enabling logging</span></span>
<span data-ttu-id="01b67-133">記錄啟用時，診斷和錯誤都會從 Web 服務端點記錄到與使用者工作區連結的 Azure 儲存體帳戶之 **ml-診斷** blob 容器中。</span><span class="sxs-lookup"><span data-stu-id="01b67-133">When logging is enabled, the diagnostics and errors from the web service endpoint are logged in the **ml-diagnostics** blob container in the Azure Storage Account linked with the user’s workspace.</span></span> <span data-ttu-id="01b67-134">這個容器針對所有與此儲存體帳戶相關聯的工作區，存放所有 Web 服務端點的診斷資訊。</span><span class="sxs-lookup"><span data-stu-id="01b67-134">This container holds all the diagnostics information for all the web service endpoints for all the workspaces associated with this storage account.</span></span>

<span data-ttu-id="01b67-135">記錄可使用任何可用於探索 Azure 儲存體帳戶的多種工具來檢視。</span><span class="sxs-lookup"><span data-stu-id="01b67-135">The logs can be viewed using any of the several tools available to explore an Azure Storage Account.</span></span> <span data-ttu-id="01b67-136">最簡單的方法就是瀏覽至 Azure 入口網站中的儲存體帳戶，按一下 [容器]，然後按一下 [ml-診斷] 容器。</span><span class="sxs-lookup"><span data-stu-id="01b67-136">The easiest may be to navigate to the storage account in the Azure portal, click **Containers**, and then click the container **ml-diagnostics**.</span></span>  

## <a name="log-blob-detail-information"></a><span data-ttu-id="01b67-137">記錄檔 blob 詳細資訊</span><span class="sxs-lookup"><span data-stu-id="01b67-137">Log blob detail information</span></span>
<span data-ttu-id="01b67-138">在容器中的每個 blob，只會存放下列其中一項動作的診斷資訊：</span><span class="sxs-lookup"><span data-stu-id="01b67-138">Each blob in the container holds the diagnostics information for exactly one of the following actions:</span></span>

* <span data-ttu-id="01b67-139">批次執行方法的執行</span><span class="sxs-lookup"><span data-stu-id="01b67-139">An execution of the Batch-Execution method</span></span>  
* <span data-ttu-id="01b67-140">要求-回應方法的執行</span><span class="sxs-lookup"><span data-stu-id="01b67-140">An execution of the Request-Response method</span></span>  
* <span data-ttu-id="01b67-141">要求-回應容器的初始化</span><span class="sxs-lookup"><span data-stu-id="01b67-141">Initialization of a Request-Response container</span></span>

<span data-ttu-id="01b67-142">每個 blob 的名稱具有下列形式的前置詞︰</span><span class="sxs-lookup"><span data-stu-id="01b67-142">The name of each blob has a prefix of the following form:</span></span> 


`{Workspace Id}-{Web service Id}-{Endpoint Id}/{Log type}`


<span data-ttu-id="01b67-143">其中的_記錄型別_是下列其中一個值：</span><span class="sxs-lookup"><span data-stu-id="01b67-143">Where _Log type_ is one of the following values:</span></span>  

* <span data-ttu-id="01b67-144">批次</span><span class="sxs-lookup"><span data-stu-id="01b67-144">batch</span></span>  
* <span data-ttu-id="01b67-145">分數/要求</span><span class="sxs-lookup"><span data-stu-id="01b67-145">score/requests</span></span>  
* <span data-ttu-id="01b67-146">分數/初始</span><span class="sxs-lookup"><span data-stu-id="01b67-146">score/init</span></span>  

