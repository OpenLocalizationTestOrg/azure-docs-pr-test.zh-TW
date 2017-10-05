---
title: "使用 Azure Machine Learning Web 服務參數 | Microsoft Docs"
description: "如何使用 Azure Machine Learning Web 服務參數來修改模型在 Web 服務受到存取時的行為。"
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: c49187db-b976-4731-89d6-11a0bf653db1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/12/2017
ms.author: raymondl;garye
ms.openlocfilehash: 482726c1dae5385964e08b720e529817d5907537
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-machine-learning-web-service-parameters"></a><span data-ttu-id="cd818-103">使用 Azure Machine Learning Web 服務參數</span><span class="sxs-lookup"><span data-stu-id="cd818-103">Use Azure Machine Learning Web Service Parameters</span></span>
<span data-ttu-id="cd818-104">藉由發行包含可設定參數模組的試驗，來建立 Azure Machine Learning Web 服務。</span><span class="sxs-lookup"><span data-stu-id="cd818-104">An Azure Machine Learning web service is created by publishing an experiment that contains modules with configurable parameters.</span></span> <span data-ttu-id="cd818-105">在某些情況下，您可能想要在執行 Web 服務時之際，變更模組的行為。</span><span class="sxs-lookup"><span data-stu-id="cd818-105">In some cases, you may want to change the module behavior while the web service is running.</span></span> <span data-ttu-id="cd818-106">「Web 服務參數」可讓您執行這項工作。</span><span class="sxs-lookup"><span data-stu-id="cd818-106">*Web Service Parameters* allow you to do this task.</span></span> 

<span data-ttu-id="cd818-107">常見的範例是設定[匯入資料][reader]模組，讓已發佈之 Web 服務的使用者可以在存取 Web 服務時，指定不同的資料來源。</span><span class="sxs-lookup"><span data-stu-id="cd818-107">A common example is setting up the [Import Data][reader] module so that the user of the published web service can specify a different data source when the web service is accessed.</span></span> <span data-ttu-id="cd818-108">或者，設定[匯出資料][writer]模組，以便能夠指定不同的目的地。</span><span class="sxs-lookup"><span data-stu-id="cd818-108">Or configuring the [Export Data][writer] module so that a different destination can be specified.</span></span> <span data-ttu-id="cd818-109">部分其他範例包括變更[特徵雜湊][feature-hashing]模組的位元數，或變更[以篩選器為基礎的特徵選取][filter-based-feature-selection]模組的所需特徵數。</span><span class="sxs-lookup"><span data-stu-id="cd818-109">Some other examples include changing the number of bits for the [Feature Hashing][feature-hashing] module or the number of desired features for the [Filter-Based Feature Selection][filter-based-feature-selection] module.</span></span> 

<span data-ttu-id="cd818-110">您可以設定 Web 服務參數，並使其與實驗中的一個或多個模組參數產生關聯，而且您可以指定它們是必要還是選用參數。</span><span class="sxs-lookup"><span data-stu-id="cd818-110">You can set Web Service Parameters and associate them with one or more module parameters in your experiment, and you can specify whether they are required or optional.</span></span> <span data-ttu-id="cd818-111">然後 Web 服務的使用者就可以在呼叫 Web 服務時，提供這些參數的值。</span><span class="sxs-lookup"><span data-stu-id="cd818-111">The user of the web service can then provide values for these parameters when they call the web service.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="how-to-set-and-use-web-service-parameters"></a><span data-ttu-id="cd818-112">如何設定及使用 Web 服務參數</span><span class="sxs-lookup"><span data-stu-id="cd818-112">How to set and use Web Service Parameters</span></span>
<span data-ttu-id="cd818-113">您可以按一下模組參數旁邊的圖示，然後選取 [設為 Web 服務參數] 來定義 Web 服務參數。</span><span class="sxs-lookup"><span data-stu-id="cd818-113">You define a Web Service Parameter by clicking the icon next to the parameter for a module and selecting "Set as web service parameter".</span></span> <span data-ttu-id="cd818-114">這會建立新的 Web 服務參數並將它連線至該模組參數。</span><span class="sxs-lookup"><span data-stu-id="cd818-114">This creates a new Web Service Parameter and connects it to that module parameter.</span></span> <span data-ttu-id="cd818-115">然後，在 Web 服務受到存取時，使用者可以指定 Web 服務參數的值，該值就會套用至模組參數。</span><span class="sxs-lookup"><span data-stu-id="cd818-115">Then, when the web service is accessed, the user can specify a value for the Web Service Parameter and it is applied to the module parameter.</span></span>

<span data-ttu-id="cd818-116">在您定義 Web 服務參數之後，該參數就可以供試驗中任何其他的模組參數使用。</span><span class="sxs-lookup"><span data-stu-id="cd818-116">Once you define a Web Service Parameter, it's available to any other module parameter in the experiment.</span></span> <span data-ttu-id="cd818-117">如果您定義和某個模組參數相關聯的 Web 服務參數，那麼只要參數預期具有相同類型的值，您就可以將該 Web 服務參數用於任何其他模組。</span><span class="sxs-lookup"><span data-stu-id="cd818-117">If you define a Web Service Parameter associated with a parameter for one module, you can use that same Web Service Parameter for any other module, as long as the parameter expects the same type of value.</span></span> <span data-ttu-id="cd818-118">例如，如果 Web 服務參數是數值，那麼該參數就只能用於預期值為數值的模組參數。</span><span class="sxs-lookup"><span data-stu-id="cd818-118">For example, if the Web Service Parameter is a numeric value, then it can only be used for module parameters that expect a numeric value.</span></span> <span data-ttu-id="cd818-119">當使用者設定 Web 服務參數的值時，該值將會套用至所有相關聯的模組參數。</span><span class="sxs-lookup"><span data-stu-id="cd818-119">When the user sets a value for the Web Service Parameter, it will be applied to all associated module parameters.</span></span>

<span data-ttu-id="cd818-120">您可以決定是否要為 Web 服務參數提供預設值。</span><span class="sxs-lookup"><span data-stu-id="cd818-120">You can decide whether to provide a default value for the Web Service Parameter.</span></span> <span data-ttu-id="cd818-121">如果您提供預設值，Web 服務的使用者就可以選擇是否使用該參數。</span><span class="sxs-lookup"><span data-stu-id="cd818-121">If you do, then the parameter is optional for the user of the web service.</span></span> <span data-ttu-id="cd818-122">如果您沒有提供預設值，使用者就需要在存取 Web 服務時輸入值。</span><span class="sxs-lookup"><span data-stu-id="cd818-122">If you don't provide a default value, then the user is required to enter a value when the web service is accessed.</span></span>

<span data-ttu-id="cd818-123">Web 服務的 API 文件會包含 Web 服務使用者在存取 Web 服務時，如何以程式設計方式指定 Web 服務參數的資訊。</span><span class="sxs-lookup"><span data-stu-id="cd818-123">The API documentation for the web service includes information for the web service user on how to specify the Web Service Parameter programmatically when accessing the web service.</span></span>

> [!NOTE]
> <span data-ttu-id="cd818-124">傳統 Web 服務的 API 文件是透過 Machine Learning Studio 中 Web 服務 [儀表板] 的 [API 說明頁面] 連結提供。</span><span class="sxs-lookup"><span data-stu-id="cd818-124">The API documentation for a classic web service is provided through the **API help page** link in the web service **DASHBOARD** in Machine Learning Studio.</span></span> <span data-ttu-id="cd818-125">新的 Web 服務的 API 文件則是透過 [Azure Machine Learning Web Services](https://services.azureml.net/Quickstart) 入口網站中 Web 服務的 [取用] 和 [Swagger API] 頁面提供。</span><span class="sxs-lookup"><span data-stu-id="cd818-125">The API documentation for a new web service is provided through the [Azure Machine Learning Web Services](https://services.azureml.net/Quickstart) portal on the **Consume** and **Swagger API** pages for your web service.</span></span>
> 
> 

## <a name="example"></a><span data-ttu-id="cd818-126">範例</span><span class="sxs-lookup"><span data-stu-id="cd818-126">Example</span></span>
<span data-ttu-id="cd818-127">舉例來說，假設我們有一個[匯出資料][writer]模組實驗，該模組會傳送資訊給 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="cd818-127">As an example, let's assume we have an experiment with an [Export Data][writer] module that sends information to Azure blob storage.</span></span> <span data-ttu-id="cd818-128">我們將會定義名為 Blob path 的 Web 服務參數，以在服務被存取時允許 Web 服務使用者將路徑變更至 Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="cd818-128">We'll define a Web Service Parameter named "Blob path" that allows the web service user to change the path to the blob storage when the service is accessed.</span></span>

1. <span data-ttu-id="cd818-129">在 Machine Learning Studio 中，按一下 [[匯出資料][writer]] 模組來選取它。</span><span class="sxs-lookup"><span data-stu-id="cd818-129">In Machine Learning Studio, click the [Export Data][writer] module to select it.</span></span> <span data-ttu-id="cd818-130">其屬性會顯示在試驗畫布右邊的 [屬性] 窗格中。</span><span class="sxs-lookup"><span data-stu-id="cd818-130">Its properties are shown in the Properties pane to the right of the experiment canvas.</span></span>
2. <span data-ttu-id="cd818-131">指定儲存體類型：</span><span class="sxs-lookup"><span data-stu-id="cd818-131">Specify the storage type:</span></span>
   
   * <span data-ttu-id="cd818-132">在 **[請指定資料目的地]**底下，選取 [Azure Blob 儲存體]。</span><span class="sxs-lookup"><span data-stu-id="cd818-132">Under **Please specify data destination**, select "Azure Blob Storage".</span></span>
   * <span data-ttu-id="cd818-133">在 **[請指定驗證類型]**底下，選取 [帳戶]。</span><span class="sxs-lookup"><span data-stu-id="cd818-133">Under **Please specify authentication type**, select "Account".</span></span>
   * <span data-ttu-id="cd818-134">輸入 Azure Blob 儲存體的帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="cd818-134">Enter the account information for the Azure blob storage.</span></span> 
     <p /><span data-ttu-id="cd818-135">
3. 按一下 **[以容器參數為開頭的 Blob 路徑]** 右邊的圖示。</span><span class="sxs-lookup"><span data-stu-id="cd818-135">
3. Click the icon to the right of the **Path to blob beginning with container parameter**.</span></span> <span data-ttu-id="cd818-136">它看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="cd818-136">It looks like this:</span></span>
   
   ![Web 服務參數圖示][icon]
   
   <span data-ttu-id="cd818-138">選取 [設為 Web 服務參數]。</span><span class="sxs-lookup"><span data-stu-id="cd818-138">Select "Set as web service parameter".</span></span>
   
   <span data-ttu-id="cd818-139">就會在 **[屬性] 窗格底部的 [Web 服務參數]** 底下新增一個名為 [以容器為開頭的 Blob 路徑] 項目。</span><span class="sxs-lookup"><span data-stu-id="cd818-139">An entry is added under **Web Service Parameters** at the bottom of the Properties pane with the name "Path to blob beginning with container".</span></span> <span data-ttu-id="cd818-140">這就是現在與此[匯出資料][writer]模組參數關聯的「Web 服務參數」。</span><span class="sxs-lookup"><span data-stu-id="cd818-140">This is the Web Service Parameter that is now associated with this [Export Data][writer] module parameter.</span></span>
4. <span data-ttu-id="cd818-141">若要重新命名 Web 服務參數，請按一下名稱，輸入 Blob path，然後按 **Enter** 鍵。</span><span class="sxs-lookup"><span data-stu-id="cd818-141">To rename the Web Service Parameter, click the name, enter "Blob path", and press the **Enter** key.</span></span> 
5. <span data-ttu-id="cd818-142">若要為 Web 服務參數提供預設值，請按一下名稱右邊的圖示，選取 [提供預設值]，輸入值 (例如 container1/output1.csv)，然後按 **Enter** 鍵。</span><span class="sxs-lookup"><span data-stu-id="cd818-142">To provide a default value for the Web Service Parameter, click the icon to the right of the name, select "Provide default value", enter a value (for example, "container1/output1.csv"), and press the **Enter** key.</span></span>
   
   ![Web 服務參數][parameter]
6. <span data-ttu-id="cd818-144">按一下 **[執行]**。</span><span class="sxs-lookup"><span data-stu-id="cd818-144">Click **Run**.</span></span> 
7. <span data-ttu-id="cd818-145">按一下 [部署 Web 服務]，然後選取 [部署 Web 服務 [傳統]] 或 [部署 Web 服務 [新]] 可部署 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="cd818-145">Click **Deploy Web Service** and select **Deploy Web Service [Classic]** or **Deploy Web Service [New]** to deploy the web service.</span></span>

> [!NOTE] 
> <span data-ttu-id="cd818-146">若要部署新的 Web 服務，您必須在要部署 Web 服務的訂用帳戶中具備足夠的權限。</span><span class="sxs-lookup"><span data-stu-id="cd818-146">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="cd818-147">如需詳細資訊，請參閱[使用 Azure Machine Learning Web 服務入口網站管理 Web 服務](machine-learning-manage-new-webservice.md)。</span><span class="sxs-lookup"><span data-stu-id="cd818-147">For more information see, [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="cd818-148">Web 服務的使用者現在即可在存取 Web 服務時，為[匯出資料][writer]模組指定新的目的地。</span><span class="sxs-lookup"><span data-stu-id="cd818-148">The user of the web service can now specify a new destination for the [Export Data][writer] module when accessing the web service.</span></span>

## <a name="more-information"></a><span data-ttu-id="cd818-149">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="cd818-149">More information</span></span>
<span data-ttu-id="cd818-150">如需更詳細的範例，請參閱 [Machine Learning Blog](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx) 中的 [Web 服務參數](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx)項目。</span><span class="sxs-lookup"><span data-stu-id="cd818-150">For a more detailed example, see the [Web Service Parameters](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx) entry in the [Machine Learning Blog](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx).</span></span>

<span data-ttu-id="cd818-151">有關存取 Machine Learning Web 服務的詳細資訊，請參閱[如何使用 Azure Machine Learning Web 服務](machine-learning-consume-web-services.md)。</span><span class="sxs-lookup"><span data-stu-id="cd818-151">For more information on accessing a Machine Learning web service, see [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

<!-- Images -->
[icon]: ./media/machine-learning-web-service-parameters/icon.png
[parameter]: ./media/machine-learning-web-service-parameters/parameter.png


<!-- Module References -->
[feature-hashing]: https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[reader]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[writer]: https://msdn.microsoft.com/library/azure/7a391181-b6a7-4ad4-b82d-e419c0d6522c/

