---
title: "在 Machine Learning 中建立 Web 服務端點 | Microsoft Docs"
description: "在 Azure Machine Learning 中建立 Web 服務端點"
services: machine-learning
documentationcenter: 
author: hiteshmadan
manager: padou
editor: cgronlun
ms.assetid: 4657fc1b-5228-4950-a29e-bc709259f728
ms.service: machine-learning
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 10/04/2016
ms.author: himad
ms.openlocfilehash: 9f83ffc9cf7dbe37c1ce9980fd7f5b9133fe78f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="creating-endpoints"></a><span data-ttu-id="28c7f-103">建立端點</span><span class="sxs-lookup"><span data-stu-id="28c7f-103">Creating Endpoints</span></span>
> [!NOTE]
>  <span data-ttu-id="28c7f-104">此主題描述適用於**傳統** Machine Learning Web 服務的技巧。</span><span class="sxs-lookup"><span data-stu-id="28c7f-104">This topic describes techniques applicable to a **Classic** Machine Learning Web service.</span></span>
> 
> 

<span data-ttu-id="28c7f-105">當您建立會進而銷售給客戶的 Web 服務時，必須為每位客戶提供仍連結至建立 Web 服務之實驗的定型模型。</span><span class="sxs-lookup"><span data-stu-id="28c7f-105">When you create Web services that you sell forward to your customers, you need to provide trained models to each customer that are still linked to the experiment from which the Web service was created.</span></span> <span data-ttu-id="28c7f-106">此外，實驗的任何更新都應可以選擇性地套用到整個端點，而不會覆寫自訂項目。</span><span class="sxs-lookup"><span data-stu-id="28c7f-106">In addition, any updates to the experiment should be applied selectively to an endpoint without overwriting the customizations.</span></span>

<span data-ttu-id="28c7f-107">為了達到這個目的，Azure Machine Learning 允許您為已部署的 Web 服務建立多個端點。</span><span class="sxs-lookup"><span data-stu-id="28c7f-107">To accomplish this, Azure Machine Learning allows you to create multiple endpoints for a deployed Web service.</span></span> <span data-ttu-id="28c7f-108">Web 服務的每個端點都是個別定址、節流以及管理。</span><span class="sxs-lookup"><span data-stu-id="28c7f-108">Each endpoint in the Web service is independently addressed, throttled, and managed.</span></span> <span data-ttu-id="28c7f-109">每個端點是一個唯一 URL 和授權金鑰，您可散發給您的客戶。</span><span class="sxs-lookup"><span data-stu-id="28c7f-109">Each endpoint is a unique URL and authorization key that you can distribute to your customers.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="adding-endpoints-to-a-web-service"></a><span data-ttu-id="28c7f-110">將端點新增至 Web 服務</span><span class="sxs-lookup"><span data-stu-id="28c7f-110">Adding endpoints to a Web service</span></span>
<span data-ttu-id="28c7f-111">有三種方式可在 Web 服務中新增端點。</span><span class="sxs-lookup"><span data-stu-id="28c7f-111">There are three ways to add an endpoint to a Web service.</span></span>

* <span data-ttu-id="28c7f-112">以程式設計方式</span><span class="sxs-lookup"><span data-stu-id="28c7f-112">Programmatically</span></span>
* <span data-ttu-id="28c7f-113">透過 Azure Machine Learning Web 服務入口網站</span><span class="sxs-lookup"><span data-stu-id="28c7f-113">Through the Azure Machine Learning Web Services portal</span></span>
* <span data-ttu-id="28c7f-114">透過 Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="28c7f-114">Though the Azure classic portal</span></span>

<span data-ttu-id="28c7f-115">建立端點之後，您就可以透過同步 API、批次 API 以及 Excel 工作表來取用該端點。</span><span class="sxs-lookup"><span data-stu-id="28c7f-115">Once the endpoint is created, you can consume it through synchronous APIs, batch APIs, and excel worksheets.</span></span> <span data-ttu-id="28c7f-116">除了透過此 UI 新增端點之外，您也可以使用端點管理 API，以程式設計方式加入端點。</span><span class="sxs-lookup"><span data-stu-id="28c7f-116">In addition to adding endpoints through this UI, you can also use the Endpoint Management APIs to programmatically add endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="28c7f-117">如果您已在 Web 服務中新增額外的端點，就無法刪除預設端點。</span><span class="sxs-lookup"><span data-stu-id="28c7f-117">If you have added additional endpoints to the Web service, you cannot delete the default endpoint.</span></span>
> 
> 

## <a name="adding-an-endpoint-programmatically"></a><span data-ttu-id="28c7f-118">以程式設計方式新增端點</span><span class="sxs-lookup"><span data-stu-id="28c7f-118">Adding an endpoint programmatically</span></span>
<span data-ttu-id="28c7f-119">您可以使用 [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) 範例程式碼，以程式設計方式將端點新增至您的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="28c7f-119">You can add an endpoint to your Web service programmatically using the [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.</span></span>

## <a name="adding-an-endpoint-using-the-azure-machine-learning-web-services-portal"></a><span data-ttu-id="28c7f-120">使用 Azure Machine Learning Web 服務入口網站新增端點</span><span class="sxs-lookup"><span data-stu-id="28c7f-120">Adding an endpoint using the Azure Machine Learning Web Services portal</span></span>
1. <span data-ttu-id="28c7f-121">在 Machine Learning Studio 中，按一下左側的 [Web 服務]。</span><span class="sxs-lookup"><span data-stu-id="28c7f-121">In Machine Learning Studio, on the left navigation column, click Web Services.</span></span>
2. <span data-ttu-id="28c7f-122">在 Web 服務儀表板底部，按一下 [管理端點]。</span><span class="sxs-lookup"><span data-stu-id="28c7f-122">At the bottom of the Web service dashboard, click **Manage endpoints**.</span></span> <span data-ttu-id="28c7f-123">Azure Machine Learning Web 服務 入口網站會開啟 Web 服務的端點頁面。</span><span class="sxs-lookup"><span data-stu-id="28c7f-123">The Azure Machine Learning Web Services portal opens to the endpoints page for the Web service.</span></span>
3. <span data-ttu-id="28c7f-124">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="28c7f-124">Click **New**.</span></span>
4. <span data-ttu-id="28c7f-125">輸入新端點的名稱和描述。</span><span class="sxs-lookup"><span data-stu-id="28c7f-125">Type a name and description for the new endpoint.</span></span> <span data-ttu-id="28c7f-126">端點名稱長度不可超過 24 個字元，而且必須由小寫字母或數字組成。</span><span class="sxs-lookup"><span data-stu-id="28c7f-126">Endpoint names must be 24 character or less in length, and must be made up of lower-case alphabets or numbers.</span></span> <span data-ttu-id="28c7f-127">選取記錄層級，以及是否啟用範例資料。</span><span class="sxs-lookup"><span data-stu-id="28c7f-127">Select the logging level and whether sample data is enabled.</span></span> <span data-ttu-id="28c7f-128">如需有關記錄的詳細資訊，請參閱[為 Machine Learning Web 服務啟用記錄](machine-learning-web-services-logging.md)。</span><span class="sxs-lookup"><span data-stu-id="28c7f-128">For more information on logging, see [Enable logging for Machine Learning Web services](machine-learning-web-services-logging.md).</span></span>

## <a name="adding-an-endpoint-using-the-azure-classic-portal"></a><span data-ttu-id="28c7f-129">使用 Azure 傳統入口網站新增端點</span><span class="sxs-lookup"><span data-stu-id="28c7f-129">Adding an endpoint using the Azure classic portal</span></span>
1. <span data-ttu-id="28c7f-130">登入 [Azure 傳統入口網站](http://manage.windowsazure.com)，按一下左欄中的 [Machine Learning]。</span><span class="sxs-lookup"><span data-stu-id="28c7f-130">Sign in to the [Azure classic portal](http://manage.windowsazure.com), click **Machine Learning** in the left column.</span></span> <span data-ttu-id="28c7f-131">按一下包含您感興趣之 Web 服務的工作區。</span><span class="sxs-lookup"><span data-stu-id="28c7f-131">Click the workspace which contains the Web service in which you are interested.</span></span>
   
    ![瀏覽到工作區](./media/machine-learning-create-endpoint/figure-1.png)
2. <span data-ttu-id="28c7f-133">按一下 [Web 服務] 。</span><span class="sxs-lookup"><span data-stu-id="28c7f-133">Click **Web Services**.</span></span>
   
    ![瀏覽到 Web 服務](./media/machine-learning-create-endpoint/figure-2.png)
3. <span data-ttu-id="28c7f-135">按一下您感興趣的 Web 服務，以查看可用端點的清單。</span><span class="sxs-lookup"><span data-stu-id="28c7f-135">Click the Web service you're interested in to see the list of available endpoints.</span></span>
   
    ![瀏覽到端點](./media/machine-learning-create-endpoint/figure-3.png)
4. <span data-ttu-id="28c7f-137">按一下頁面底部的 [新增端點] 。</span><span class="sxs-lookup"><span data-stu-id="28c7f-137">At the bottom of the page, click **Add Endpoint**.</span></span> <span data-ttu-id="28c7f-138">輸入名稱和描述，確定此 Web 服務中沒有名稱相同的其他端點。</span><span class="sxs-lookup"><span data-stu-id="28c7f-138">Type a name and description, ensure there are no other endpoints with the same name in this Web service.</span></span> <span data-ttu-id="28c7f-139">除非您有特殊需求，否則請保留節流層級的預設值。</span><span class="sxs-lookup"><span data-stu-id="28c7f-139">Leave the throttle level with its default value unless you have special requirements.</span></span> <span data-ttu-id="28c7f-140">若要深入了解節流，請參閱[調整 API 端點](machine-learning-scaling-webservice.md)。</span><span class="sxs-lookup"><span data-stu-id="28c7f-140">To learn more about throttling, see [Scaling API Endpoints](machine-learning-scaling-webservice.md).</span></span>
   
    ![建立端點](./media/machine-learning-create-endpoint/figure-4.png)

## <a name="next-steps"></a><span data-ttu-id="28c7f-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="28c7f-142">Next Steps</span></span>
<span data-ttu-id="28c7f-143">[如何使用 Azure Machine Learning Web 服務](machine-learning-consume-web-services.md)。</span><span class="sxs-lookup"><span data-stu-id="28c7f-143">[How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

