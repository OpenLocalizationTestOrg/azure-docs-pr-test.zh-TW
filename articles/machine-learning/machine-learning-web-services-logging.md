---
title: "Machine Learning web 服務的 aaaLogging |Microsoft 文件"
description: "深入了解如何 tooenable 記錄機器學習 web 服務。 記錄提供 toohelp 疑難排解 hello 應用程式開發介面的其他資訊。"
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
ms.openlocfilehash: ed23933d52d2151af658af2307d7df8743071f65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-logging-for-machine-learning-web-services"></a><span data-ttu-id="43437-104">為 Machine Learning Web 服務啟用記錄</span><span class="sxs-lookup"><span data-stu-id="43437-104">Enable logging for Machine Learning web services</span></span>
<span data-ttu-id="43437-105">本文件提供記錄功能的機器學習 web 服務的 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="43437-105">This document provides information on hello logging capability of Machine Learning web services.</span></span> <span data-ttu-id="43437-106">記錄提供只錯誤號碼和訊息，可以幫助您疑難排解您呼叫 toohello 機器學習 Api 之外的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="43437-106">Logging provides additional information, beyond just an error number and a message, that can help you troubleshoot your calls toohello Machine Learning APIs.</span></span>  

## <a name="how-tooenable-logging-for-a-web-service"></a><span data-ttu-id="43437-107">如何 tooenable 記錄 Web 服務</span><span class="sxs-lookup"><span data-stu-id="43437-107">How tooenable logging for a Web service</span></span>

<span data-ttu-id="43437-108">啟用記錄從 hello [Azure 機器學習 Web 服務](https://services.azureml.net)入口網站。</span><span class="sxs-lookup"><span data-stu-id="43437-108">You enable logging from hello [Azure Machine Learning Web Services](https://services.azureml.net) portal.</span></span> 

1. <span data-ttu-id="43437-109">登入 toohello Azure 機器學習 Web 服務的入口網站位於[https://services.azureml.net](https://services.azureml.net)。</span><span class="sxs-lookup"><span data-stu-id="43437-109">Sign in toohello Azure Machine Learning Web Services portal at [https://services.azureml.net](https://services.azureml.net).</span></span> <span data-ttu-id="43437-110">傳統 web 服務，您也可以取得 toohello 入口網站按一下**新的 Web 服務體驗**hello Machine Learning Studio 中的機器學習 Web 服務頁面上。</span><span class="sxs-lookup"><span data-stu-id="43437-110">For a Classic web service, you can also get toohello portal by clicking **New Web Services Experience** on hello Machine Learning Web Services page in Machine Learning Studio.</span></span>

   ![新的 Web 服務體驗連結](media/machine-learning-web-services-logging/new-web-services-experience-link.png)

2. <span data-ttu-id="43437-112">Hello 頂端功能表列上，按一下**Web 服務**新的 web 服務，或按一下**傳統 Web 服務**的傳統 web 服務。</span><span class="sxs-lookup"><span data-stu-id="43437-112">On hello top menu bar, click **Web Services** for a New web service, or click **Classic Web Services** for a Classic web service.</span></span>

   ![選取新的或傳統 Web 服務](media/machine-learning-web-services-logging/select-web-service.png)

3. <span data-ttu-id="43437-114">新的 web 服務，按一下 hello web 服務名稱。</span><span class="sxs-lookup"><span data-stu-id="43437-114">For a New web service, click hello web service name.</span></span> <span data-ttu-id="43437-115">傳統 web 服務中，按一下 hello web 服務名稱，然後在 hello 下一步 頁面上按一下 hello 適當的端點。</span><span class="sxs-lookup"><span data-stu-id="43437-115">For a Classic web service, click hello web service name and then on hello next page click hello appropriate endpoint.</span></span>

4. <span data-ttu-id="43437-116">Hello 頂端功能表列上，按一下**設定**。</span><span class="sxs-lookup"><span data-stu-id="43437-116">On hello top menu bar, click **Configure**.</span></span>

5. <span data-ttu-id="43437-117">設定 hello **Enable Logging**太選項*錯誤*（toolog 唯一錯誤） 或*所有*（適用於完整記錄）。</span><span class="sxs-lookup"><span data-stu-id="43437-117">Set hello **Enable Logging** option too*Error* (toolog only errors) or *All* (for full logging).</span></span>

   ![選取記錄等級](media/machine-learning-web-services-logging/enable-logging.png)

6. <span data-ttu-id="43437-119">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="43437-119">Click **Save**.</span></span>

7. <span data-ttu-id="43437-120">傳統 web 服務，建立 hello **ml 診斷**容器。</span><span class="sxs-lookup"><span data-stu-id="43437-120">For Classic web services, create hello **ml-diagnostics** container.</span></span>

   <span data-ttu-id="43437-121">所有的 web 服務記錄檔會保留在 blob 容器，名為**ml 診斷**hello 與 hello web 服務相關聯的儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="43437-121">All web service logs are kept in a blob container named **ml-diagnostics** in hello storage account associated with hello web service.</span></span> <span data-ttu-id="43437-122">為新的 web 服務，此容器會建立 hello 存取 hello web 服務的第一次。</span><span class="sxs-lookup"><span data-stu-id="43437-122">For New web services, this container is created hello first time you access hello web service.</span></span> <span data-ttu-id="43437-123">傳統 web 服務，則需要 toocreate hello 容器不存在。</span><span class="sxs-lookup"><span data-stu-id="43437-123">For Classic web services, you need toocreate hello container if it doesn't already exist.</span></span> 

   1. <span data-ttu-id="43437-124">在 hello [Azure 入口網站](https://portal.azure.com)，移至 toohello hello web 服務相關聯的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="43437-124">In hello [Azure portal](https://portal.azure.com), go toohello storage account associated with hello web service.</span></span>

   2. <span data-ttu-id="43437-125">在 [Blob 服務] 下，按一下 [容器]。</span><span class="sxs-lookup"><span data-stu-id="43437-125">Under **Blob Service**, click **Containers**.</span></span>

   3. <span data-ttu-id="43437-126">如果 hello 容器**ml 診斷**不存在，請按一下**+ 容器**，授與 hello 容器 hello 名稱"ml-diagnostics"，然後選取 hello**存取類型**為"Blob"。</span><span class="sxs-lookup"><span data-stu-id="43437-126">If hello container **ml-diagnostics** doesn't exist, click **+Container**, give hello container hello name "ml-diagnostics", and select hello **Access type** as "Blob".</span></span> <span data-ttu-id="43437-127">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="43437-127">Click **OK**.</span></span>

      ![選取記錄等級](media/machine-learning-web-services-logging/create-ml-diagnostics-container.png)

> [!TIP]
>
> <span data-ttu-id="43437-129">傳統 web 服務，hello Machine Learning Studio 中的 Web 服務儀表板也會有交換器 tooenable 記錄。</span><span class="sxs-lookup"><span data-stu-id="43437-129">For a Classic web service, hello Web Services Dashboard in Machine Learning Studio also has a switch tooenable logging.</span></span> <span data-ttu-id="43437-130">不過，記錄現在透過 hello Web Services 入口網站管理，因為您會需要 tooenable 記錄透過 hello 入口網站中這篇文章所述。</span><span class="sxs-lookup"><span data-stu-id="43437-130">However, because logging is now managed through hello Web Services portal, you need tooenable logging through hello portal as described in this article.</span></span> <span data-ttu-id="43437-131">如果您已啟用登入 Studio，然後在 hello 服務入口網站，停用記錄，然後再次啟用。</span><span class="sxs-lookup"><span data-stu-id="43437-131">If you already enabled logging in Studio, then in hello Web Services Portal, disable logging and enable it again.</span></span>


## <a name="hello-effects-of-enabling-logging"></a><span data-ttu-id="43437-132">啟用記錄功能的 hello 效果</span><span class="sxs-lookup"><span data-stu-id="43437-132">hello effects of enabling logging</span></span>
<span data-ttu-id="43437-133">啟用記錄時，會將 hello 診斷和 hello web 服務端點中的錯誤記錄在 hello **ml 診斷**與 hello 使用者的工作區連結 hello Azure 儲存體帳戶中的 blob 容器。</span><span class="sxs-lookup"><span data-stu-id="43437-133">When logging is enabled, hello diagnostics and errors from hello web service endpoint are logged in hello **ml-diagnostics** blob container in hello Azure Storage Account linked with hello user’s workspace.</span></span> <span data-ttu-id="43437-134">此容器保留與這個儲存體帳戶相關聯的所有 hello 工作區的所有 hello web 服務端點的所有 hello 診斷資訊。</span><span class="sxs-lookup"><span data-stu-id="43437-134">This container holds all hello diagnostics information for all hello web service endpoints for all hello workspaces associated with this storage account.</span></span>

<span data-ttu-id="43437-135">使用任何 hello 數個工具可用 tooexplore Azure 儲存體帳戶即可檢視 hello 記錄。</span><span class="sxs-lookup"><span data-stu-id="43437-135">hello logs can be viewed using any of hello several tools available tooexplore an Azure Storage Account.</span></span> <span data-ttu-id="43437-136">最簡單的 hello 可能是 hello Azure 入口網站中的 toonavigate toohello 儲存體帳戶中，按一下**容器**，然後按一下hello 容器**ml 診斷**。</span><span class="sxs-lookup"><span data-stu-id="43437-136">hello easiest may be toonavigate toohello storage account in hello Azure portal, click **Containers**, and then click hello container **ml-diagnostics**.</span></span>  

## <a name="log-blob-detail-information"></a><span data-ttu-id="43437-137">記錄檔 blob 詳細資訊</span><span class="sxs-lookup"><span data-stu-id="43437-137">Log blob detail information</span></span>
<span data-ttu-id="43437-138">Hello 容器中的每個 blob 會保存 hello 的診斷資訊，正好有一個 hello 下列動作：</span><span class="sxs-lookup"><span data-stu-id="43437-138">Each blob in hello container holds hello diagnostics information for exactly one of hello following actions:</span></span>

* <span data-ttu-id="43437-139">執行 hello 批次執行方法</span><span class="sxs-lookup"><span data-stu-id="43437-139">An execution of hello Batch-Execution method</span></span>  
* <span data-ttu-id="43437-140">執行要求-回應 hello 方法</span><span class="sxs-lookup"><span data-stu-id="43437-140">An execution of hello Request-Response method</span></span>  
* <span data-ttu-id="43437-141">要求-回應容器的初始化</span><span class="sxs-lookup"><span data-stu-id="43437-141">Initialization of a Request-Response container</span></span>

<span data-ttu-id="43437-142">hello 的每個 blob 的名稱具有下列形式的 hello 的前置詞：</span><span class="sxs-lookup"><span data-stu-id="43437-142">hello name of each blob has a prefix of hello following form:</span></span> 


`{Workspace Id}-{Web service Id}-{Endpoint Id}/{Log type}`


<span data-ttu-id="43437-143">其中_記錄類型_是 hello 下列值之一：</span><span class="sxs-lookup"><span data-stu-id="43437-143">Where _Log type_ is one of hello following values:</span></span>  

* <span data-ttu-id="43437-144">批次</span><span class="sxs-lookup"><span data-stu-id="43437-144">batch</span></span>  
* <span data-ttu-id="43437-145">分數/要求</span><span class="sxs-lookup"><span data-stu-id="43437-145">score/requests</span></span>  
* <span data-ttu-id="43437-146">分數/初始</span><span class="sxs-lookup"><span data-stu-id="43437-146">score/init</span></span>  

