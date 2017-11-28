---
title: "在機器學習中的 aaaCreating Web 服務端點 |Microsoft 文件"
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
ms.openlocfilehash: 10a2bc586c6fe35e28d8bf0293854c578827c453
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="creating-endpoints"></a><span data-ttu-id="da506-103">建立端點</span><span class="sxs-lookup"><span data-stu-id="da506-103">Creating Endpoints</span></span>
> [!NOTE]
>  <span data-ttu-id="da506-104">本主題說明的技巧適用 tooa**傳統**機器學習 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="da506-104">This topic describes techniques applicable tooa **Classic** Machine Learning Web service.</span></span>
> 
> 

<span data-ttu-id="da506-105">當您建立銷售轉寄 tooyour 客戶的 Web 服務時，您必須是哪些 hello Web 服務建立的連結仍 toohello 實驗 tooprovide 定型的模型 tooeach 客戶。</span><span class="sxs-lookup"><span data-stu-id="da506-105">When you create Web services that you sell forward tooyour customers, you need tooprovide trained models tooeach customer that are still linked toohello experiment from which hello Web service was created.</span></span> <span data-ttu-id="da506-106">此外，任何更新 toohello 實驗應該套用選擇性 tooan 端點而不覆寫 hello 自訂項目。</span><span class="sxs-lookup"><span data-stu-id="da506-106">In addition, any updates toohello experiment should be applied selectively tooan endpoint without overwriting hello customizations.</span></span>

<span data-ttu-id="da506-107">tooaccomplish，Azure 機器學習可讓您 toocreate 多個已部署的 Web 服務的端點。</span><span class="sxs-lookup"><span data-stu-id="da506-107">tooaccomplish this, Azure Machine Learning allows you toocreate multiple endpoints for a deployed Web service.</span></span> <span data-ttu-id="da506-108">Hello Web 服務中的每個端點獨立定址，節流處理，並管理。</span><span class="sxs-lookup"><span data-stu-id="da506-108">Each endpoint in hello Web service is independently addressed, throttled, and managed.</span></span> <span data-ttu-id="da506-109">每個端點都是唯一的 URL 和授權的索引鍵，您可以將發佈 tooyour 客戶。</span><span class="sxs-lookup"><span data-stu-id="da506-109">Each endpoint is a unique URL and authorization key that you can distribute tooyour customers.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="adding-endpoints-tooa-web-service"></a><span data-ttu-id="da506-110">加入端點 tooa Web 服務</span><span class="sxs-lookup"><span data-stu-id="da506-110">Adding endpoints tooa Web service</span></span>
<span data-ttu-id="da506-111">有三種方式 tooadd 端點 tooa Web 服務。</span><span class="sxs-lookup"><span data-stu-id="da506-111">There are three ways tooadd an endpoint tooa Web service.</span></span>

* <span data-ttu-id="da506-112">以程式設計方式</span><span class="sxs-lookup"><span data-stu-id="da506-112">Programmatically</span></span>
* <span data-ttu-id="da506-113">透過 hello Azure 機器學習 Web 服務入口網站</span><span class="sxs-lookup"><span data-stu-id="da506-113">Through hello Azure Machine Learning Web Services portal</span></span>
* <span data-ttu-id="da506-114">雖然 hello Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="da506-114">Though hello Azure classic portal</span></span>

<span data-ttu-id="da506-115">Hello 端點建立之後，您可以使用它，透過同步應用程式開發介面，批次應用程式開發介面，和 excel 工作表。</span><span class="sxs-lookup"><span data-stu-id="da506-115">Once hello endpoint is created, you can consume it through synchronous APIs, batch APIs, and excel worksheets.</span></span> <span data-ttu-id="da506-116">除了透過此 UI tooadding 端點，您也可以使用 hello 端點管理 Api tooprogrammatically 加入端點。</span><span class="sxs-lookup"><span data-stu-id="da506-116">In addition tooadding endpoints through this UI, you can also use hello Endpoint Management APIs tooprogrammatically add endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="da506-117">如果您已經加入其他端點 toohello Web 服務，您無法刪除 hello 預設端點。</span><span class="sxs-lookup"><span data-stu-id="da506-117">If you have added additional endpoints toohello Web service, you cannot delete hello default endpoint.</span></span>
> 
> 

## <a name="adding-an-endpoint-programmatically"></a><span data-ttu-id="da506-118">以程式設計方式新增端點</span><span class="sxs-lookup"><span data-stu-id="da506-118">Adding an endpoint programmatically</span></span>
<span data-ttu-id="da506-119">您可以加入端點 tooyour Web 服務以程式設計方式使用 hello [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs)範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="da506-119">You can add an endpoint tooyour Web service programmatically using hello [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.</span></span>

## <a name="adding-an-endpoint-using-hello-azure-machine-learning-web-services-portal"></a><span data-ttu-id="da506-120">加入使用 hello Azure 機器學習 Web 服務入口網站的端點</span><span class="sxs-lookup"><span data-stu-id="da506-120">Adding an endpoint using hello Azure Machine Learning Web Services portal</span></span>
1. <span data-ttu-id="da506-121">在機器學習 Studio 中，在 hello 左側瀏覽資料行中，按一下 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="da506-121">In Machine Learning Studio, on hello left navigation column, click Web Services.</span></span>
2. <span data-ttu-id="da506-122">在 hello hello Web 服務儀表板底部，按一下 **管理端點**。</span><span class="sxs-lookup"><span data-stu-id="da506-122">At hello bottom of hello Web service dashboard, click **Manage endpoints**.</span></span> <span data-ttu-id="da506-123">hello Azure 機器學習 Web 服務入口網站開啟 toohello hello Web 服務端點 頁面。</span><span class="sxs-lookup"><span data-stu-id="da506-123">hello Azure Machine Learning Web Services portal opens toohello endpoints page for hello Web service.</span></span>
3. <span data-ttu-id="da506-124">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="da506-124">Click **New**.</span></span>
4. <span data-ttu-id="da506-125">輸入的名稱和描述 hello 新端點。</span><span class="sxs-lookup"><span data-stu-id="da506-125">Type a name and description for hello new endpoint.</span></span> <span data-ttu-id="da506-126">端點名稱長度不可超過 24 個字元，而且必須由小寫字母或數字組成。</span><span class="sxs-lookup"><span data-stu-id="da506-126">Endpoint names must be 24 character or less in length, and must be made up of lower-case alphabets or numbers.</span></span> <span data-ttu-id="da506-127">選取 hello 記錄層級，以及是否啟用範例資料。</span><span class="sxs-lookup"><span data-stu-id="da506-127">Select hello logging level and whether sample data is enabled.</span></span> <span data-ttu-id="da506-128">如需有關記錄的詳細資訊，請參閱[為 Machine Learning Web 服務啟用記錄](machine-learning-web-services-logging.md)。</span><span class="sxs-lookup"><span data-stu-id="da506-128">For more information on logging, see [Enable logging for Machine Learning Web services](machine-learning-web-services-logging.md).</span></span>

## <a name="adding-an-endpoint-using-hello-azure-classic-portal"></a><span data-ttu-id="da506-129">加入使用 hello Azure 傳統入口網站的端點</span><span class="sxs-lookup"><span data-stu-id="da506-129">Adding an endpoint using hello Azure classic portal</span></span>
1. <span data-ttu-id="da506-130">登入 toohello [Azure 傳統入口網站](http://manage.windowsazure.com)，按一下  **Machine Learning** hello 左側資料行中。</span><span class="sxs-lookup"><span data-stu-id="da506-130">Sign in toohello [Azure classic portal](http://manage.windowsazure.com), click **Machine Learning** in hello left column.</span></span> <span data-ttu-id="da506-131">按一下 hello 工作區，其中包含您感興趣的 hello Web 服務。</span><span class="sxs-lookup"><span data-stu-id="da506-131">Click hello workspace which contains hello Web service in which you are interested.</span></span>
   
    ![瀏覽 tooworkspace](./media/machine-learning-create-endpoint/figure-1.png)
2. <span data-ttu-id="da506-133">按一下 [Web 服務] 。</span><span class="sxs-lookup"><span data-stu-id="da506-133">Click **Web Services**.</span></span>
   
    ![瀏覽 tooWeb 服務](./media/machine-learning-create-endpoint/figure-2.png)
3. <span data-ttu-id="da506-135">按一下您想要在 toosee hello 可用的端點清單中的 hello Web 服務。</span><span class="sxs-lookup"><span data-stu-id="da506-135">Click hello Web service you're interested in toosee hello list of available endpoints.</span></span>
   
    ![瀏覽 tooendpoint](./media/machine-learning-create-endpoint/figure-3.png)
4. <span data-ttu-id="da506-137">在 hello hello 頁面底部，按一下**加入端點**。</span><span class="sxs-lookup"><span data-stu-id="da506-137">At hello bottom of hello page, click **Add Endpoint**.</span></span> <span data-ttu-id="da506-138">輸入名稱和描述，請確定沒有其他端點與此 Web 服務中名稱相同的 hello。</span><span class="sxs-lookup"><span data-stu-id="da506-138">Type a name and description, ensure there are no other endpoints with hello same name in this Web service.</span></span> <span data-ttu-id="da506-139">保留 hello 節流層級以預設值，除非您有特殊需求。</span><span class="sxs-lookup"><span data-stu-id="da506-139">Leave hello throttle level with its default value unless you have special requirements.</span></span> <span data-ttu-id="da506-140">toolearn 深入了解節流，請參閱[調整應用程式開發介面端點](machine-learning-scaling-webservice.md)。</span><span class="sxs-lookup"><span data-stu-id="da506-140">toolearn more about throttling, see [Scaling API Endpoints](machine-learning-scaling-webservice.md).</span></span>
   
    ![建立端點](./media/machine-learning-create-endpoint/figure-4.png)

## <a name="next-steps"></a><span data-ttu-id="da506-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="da506-142">Next Steps</span></span>
<span data-ttu-id="da506-143">[如何在 Azure 機器學習 Web 服務 tooconsume](machine-learning-consume-web-services.md)。</span><span class="sxs-lookup"><span data-stu-id="da506-143">[How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

