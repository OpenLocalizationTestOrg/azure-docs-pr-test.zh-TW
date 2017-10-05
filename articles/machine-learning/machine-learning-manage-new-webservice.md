---
title: "使用 Azure Machine Learning Web 服務入口網站 | Microsoft Docs"
description: "管理 Azure 機器學習工作區的存取權，並部署和管理 ML API Web 服務"
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: jhubbard
editor: cgronlun
ms.assetid: b62cf2ca-dd2a-4a83-bb54-469f948fb026
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: v-donglo
ms.openlocfilehash: ad1314aa4b504bd2cb3285789073d4f1de1f545d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-a-web-service-using-the-azure-machine-learning-web-services-portal"></a><span data-ttu-id="b0592-103">使用 Azure Machine Learning Web 服務入口網站管理 Web 服務</span><span class="sxs-lookup"><span data-stu-id="b0592-103">Manage a Web service using the Azure Machine Learning Web Services portal</span></span>
<span data-ttu-id="b0592-104">您可以使用 Microsoft Azure Machine Learning Web 服務入口網站，管理 Machine Learning 新式和傳統 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="b0592-104">You can manage your Machine Learning New and Classic Web services using the Microsoft Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="b0592-105">因為傳統 Web 服務和新式 Web 服務是根據不同的基礎技術，所以各有稍微不同的管理功能。</span><span class="sxs-lookup"><span data-stu-id="b0592-105">Since Classic Web services and New Web services are based on different underlying technologies, you have slightly different management capabilities for each of them.</span></span>

<span data-ttu-id="b0592-106">在 Machine Learning Web 服務入口網站中，您可以︰</span><span class="sxs-lookup"><span data-stu-id="b0592-106">In the Machine Learning Web Services portal you can:</span></span>

* <span data-ttu-id="b0592-107">監視 Web 服務的使用方式。</span><span class="sxs-lookup"><span data-stu-id="b0592-107">Monitor how the web service is being used.</span></span>
* <span data-ttu-id="b0592-108">設定描述、更新 Web 服務的金鑰 (僅限新式)、更新您的儲存體帳戶金鑰 (僅限新式)、啟用記錄，以及啟用或停用範例資料。</span><span class="sxs-lookup"><span data-stu-id="b0592-108">Configure the description, update the keys for the web service (New only), update your storage account key (New only), enable logging, and enable or disable sample data.</span></span>
* <span data-ttu-id="b0592-109">刪除 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="b0592-109">Delete the web service.</span></span>
* <span data-ttu-id="b0592-110">建立、刪除或更新計費方案 (僅限新式)。</span><span class="sxs-lookup"><span data-stu-id="b0592-110">Create, delete, or update billing plans (New only).</span></span>
* <span data-ttu-id="b0592-111">新增和刪除端點 (僅限傳統)</span><span class="sxs-lookup"><span data-stu-id="b0592-111">Add and delete endpoints (Classic only)</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="permissions-to-manage-new-resources-manager-based-web-services"></a><span data-ttu-id="b0592-112">管理以資源管理員為基礎的新 Web 服務的權限</span><span class="sxs-lookup"><span data-stu-id="b0592-112">Permissions to manage New Resources Manager based web services</span></span>

<span data-ttu-id="b0592-113">新的 Web 服務會部署為 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="b0592-113">New web services are deployed as Azure resources.</span></span> <span data-ttu-id="b0592-114">因此，您必須具備正確權限，才能部署和管理新的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="b0592-114">As such, you must have the correct permissions to deploy and manage New web services.</span></span>  <span data-ttu-id="b0592-115">若要部署或管理新的 Web 服務，您必須獲得下列角色的指派：要部署 Web 服務之訂用帳戶上的參與者或管理員角色。</span><span class="sxs-lookup"><span data-stu-id="b0592-115">To deploy or manage New web services you must be assigned a contributor or administrator role on the subscription to which the web service is deployed.</span></span> <span data-ttu-id="b0592-116">如果您邀請另一位使用者到 Machine Learning 工作區，就必須為他們指派訂用帳戶上的參與者或管理員角色，然後他們才能部署或管理 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="b0592-116">If you invite another user to a machine learning workspace, you must assign them to a contributor or administrator role on the subscription before they can deploy or manage web services.</span></span> 

<span data-ttu-id="b0592-117">如果使用者沒有正確權限來存取 Azure Machine Learning Web 服務入口網站中的資源，他們將會在嘗試部署 Web 服務時，收到下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="b0592-117">If the user does not have the correct permissions to access resources in the Azure Machine Learning Web Services portal, they will receive the following error when trying to deploy a web service:</span></span>

<span data-ttu-id="b0592-118">*Web 服務部署工作失敗。此帳戶沒有足夠權限來存取包含該工作區的 Azure 訂用帳戶。若要將 Web 服務部署到 Azure，必須邀請同一個帳戶到該工作區，並為該帳戶授予包含該工作區之 Azure 訂用帳戶的存取權。*</span><span class="sxs-lookup"><span data-stu-id="b0592-118">*Web Service deployment failed. This account does not have sufficient access to the Azure subscription that contains the Workspace. In order to deploy a Web Service to Azure, the same account must be invited to the Workspace and be given access to the Azure subscription that contains the Workspace.*</span></span>

<span data-ttu-id="b0592-119">如需建立工作區的詳細資訊，請參閱[建立和共用 Azure Machine Learning 工作區](machine-learning-create-workspace.md)。</span><span class="sxs-lookup"><span data-stu-id="b0592-119">For more information on creating a workspace, see [Create and share an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

<span data-ttu-id="b0592-120">如需設定存取權限的詳細資訊，請參閱[在 Azure 入口網站 - 公開預覽中檢視存取使用者和群組的工作分派](../active-directory/role-based-access-control-manage-assignments.md)。</span><span class="sxs-lookup"><span data-stu-id="b0592-120">For more information on setting access permissions, see [View access assignments for users and groups in the Azure portal - Public preview](../active-directory/role-based-access-control-manage-assignments.md).</span></span>


## <a name="manage-new-web-services"></a><span data-ttu-id="b0592-121">管理新式 Web 服務</span><span class="sxs-lookup"><span data-stu-id="b0592-121">Manage New Web services</span></span>
<span data-ttu-id="b0592-122">管理新式 Web 服務：</span><span class="sxs-lookup"><span data-stu-id="b0592-122">To manage your New Web services:</span></span>

1. <span data-ttu-id="b0592-123">使用您的 Microsoft Azure 帳戶登入 [Microsoft Azure Machine Learning Web 服務入口網站](https://services.azureml.net/quickstart) - 使用與 Azure 訂用帳戶相關聯的帳戶。</span><span class="sxs-lookup"><span data-stu-id="b0592-123">Sign in to the [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal using your Microsoft Azure account - use the account that's associated with the Azure subscription.</span></span>
2. <span data-ttu-id="b0592-124">在功能表上，按一下 [Web 服務] 。</span><span class="sxs-lookup"><span data-stu-id="b0592-124">On the menu, click **Web Services**.</span></span>

<span data-ttu-id="b0592-125">這會針對您的訂用帳戶顯示一份已部署的 Web 服務清單。</span><span class="sxs-lookup"><span data-stu-id="b0592-125">This displays a list of deployed Web services for your subscription.</span></span> 

<span data-ttu-id="b0592-126">若要管理 Web 服務，請按一下 [Web 服務]。</span><span class="sxs-lookup"><span data-stu-id="b0592-126">To manage a Web service, click Web Services.</span></span> <span data-ttu-id="b0592-127">您可以從 [Web 服務] 頁面上︰</span><span class="sxs-lookup"><span data-stu-id="b0592-127">From the Web Services page you can:</span></span>

* <span data-ttu-id="b0592-128">按一下 Web 服務進行管理。</span><span class="sxs-lookup"><span data-stu-id="b0592-128">Click the web service to manage it.</span></span>
* <span data-ttu-id="b0592-129">按一下 Web 服務的 [計費方案] 進行更新。</span><span class="sxs-lookup"><span data-stu-id="b0592-129">Click the Billing Plan for the web service to update it.</span></span>
* <span data-ttu-id="b0592-130">刪除 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="b0592-130">Delete a web service.</span></span>
* <span data-ttu-id="b0592-131">複製 Web 服務並將它部署到另一個區域。</span><span class="sxs-lookup"><span data-stu-id="b0592-131">Copy a web service and deploy it to another region.</span></span>

<span data-ttu-id="b0592-132">當您按一下某個 Web 服務時，Web 服務的 [快速入門] 頁面就會開啟。</span><span class="sxs-lookup"><span data-stu-id="b0592-132">When you click a web service, the web service Quickstart page opens.</span></span> <span data-ttu-id="b0592-133">Web 服務 [快速入門] 頁面有兩個功能表選項可讓您管理您的 Web 服務︰</span><span class="sxs-lookup"><span data-stu-id="b0592-133">The web service Quickstart page has two menu options that allow you to manage your web service:</span></span>

* <span data-ttu-id="b0592-134">**儀表板** -可讓您檢視 Web 服務使用量。</span><span class="sxs-lookup"><span data-stu-id="b0592-134">**DASHBOARD** - Allows you to view Web service usage.</span></span>
* <span data-ttu-id="b0592-135">**設定** -可讓您新增描述性文字、更新與 Web 服務相關聯的儲存體帳戶金鑰，以及啟用和停用範例資料。</span><span class="sxs-lookup"><span data-stu-id="b0592-135">**CONFIGURE** - Allows you to add descriptive text, update the key for the storage account associated with the Web service, and enable or disable sample data.</span></span>

### <a name="monitoring-how-the-web-service-is-being-used"></a><span data-ttu-id="b0592-136">監視 Web 服務的使用方式</span><span class="sxs-lookup"><span data-stu-id="b0592-136">Monitoring how the web service is being used</span></span>
<span data-ttu-id="b0592-137">按一下 [ **儀表板** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="b0592-137">Click the **DASHBOARD** tab.</span></span>

<span data-ttu-id="b0592-138">您可以從儀表板中檢視您的 Web 服務經過一段時間的整體使用量。</span><span class="sxs-lookup"><span data-stu-id="b0592-138">From the dashboard, you can view overall usage of your Web service over a period of time.</span></span> <span data-ttu-id="b0592-139">您可以從使用量圖表右上角的 [期間] 下拉式功能表中選取要檢視的期間。</span><span class="sxs-lookup"><span data-stu-id="b0592-139">You can select the period to view from the Period dropdown menu in the upper right of the usage charts.</span></span> <span data-ttu-id="b0592-140">儀表板會顯示下列資訊：</span><span class="sxs-lookup"><span data-stu-id="b0592-140">The dashboard shows the following information:</span></span>

* <span data-ttu-id="b0592-141">**一段時間的要求數** 顯示選取的一段時間內，要求數目的步階圖形。</span><span class="sxs-lookup"><span data-stu-id="b0592-141">**Requests Over Time** displays a step graph of the number of requests over the selected time period.</span></span> <span data-ttu-id="b0592-142">它可以協助識別您所遇到的使用量尖峰。</span><span class="sxs-lookup"><span data-stu-id="b0592-142">It can help identify if you are experiencing spikes in usage.</span></span>
* <span data-ttu-id="b0592-143">**要求-回應要求數** 顯示服務在選取的一段時間內收到的要求-回應呼叫總數，以及失敗的數目。</span><span class="sxs-lookup"><span data-stu-id="b0592-143">**Request-Response Requests** displays the total number of Request-Response calls the service has received over the selected time period and how many of them failed.</span></span>
* <span data-ttu-id="b0592-144">**平均要求-回應計算時間** 顯示執行收到的要求所需的平均時間。</span><span class="sxs-lookup"><span data-stu-id="b0592-144">**Average Request-Response Compute Time** displays an average of the time needed to execute the received requests.</span></span>
* <span data-ttu-id="b0592-145">**批次要求數** 顯示服務在選取的一段時間內收到的批次要求總數，以及失敗的數目。</span><span class="sxs-lookup"><span data-stu-id="b0592-145">**Batch Requests** displays the total number of Batch Requests the service has received over the selected time period and how many of them failed.</span></span>
* <span data-ttu-id="b0592-146">**平均作業延遲** 顯示執行收到的要求所需的平均時間。</span><span class="sxs-lookup"><span data-stu-id="b0592-146">**Average Job Latency** displays an average of the time needed to execute the received requests.</span></span>
* <span data-ttu-id="b0592-147">**錯誤數**顯示呼叫 Web 服務時所發生的錯誤彙總數目。</span><span class="sxs-lookup"><span data-stu-id="b0592-147">**Errors** displays the aggregate number of errors that have occurred on calls to the web service.</span></span>
* <span data-ttu-id="b0592-148">**服務成本** 顯示與服務相關聯的計費方案費用。</span><span class="sxs-lookup"><span data-stu-id="b0592-148">**Services Costs** displays the charges for the billing plan associated with the service.</span></span>

### <a name="configuring-the-web-service"></a><span data-ttu-id="b0592-149">設定 Web 服務</span><span class="sxs-lookup"><span data-stu-id="b0592-149">Configuring the web service</span></span>
<span data-ttu-id="b0592-150">按一下 [設定]  功能表選項。</span><span class="sxs-lookup"><span data-stu-id="b0592-150">Click the **CONFIGURE** menu option.</span></span>

<span data-ttu-id="b0592-151">您可以更新下列屬性：</span><span class="sxs-lookup"><span data-stu-id="b0592-151">You can update the following properties:</span></span>

* <span data-ttu-id="b0592-152">[描述] 可讓您輸入 Web 服務的描述。</span><span class="sxs-lookup"><span data-stu-id="b0592-152">**Description** allows you to enter a description for the Web service.</span></span>
* <span data-ttu-id="b0592-153">**標題**可讓您輸入 Web 服務的標題。</span><span class="sxs-lookup"><span data-stu-id="b0592-153">**Title** allows you to enter a title for the Web service</span></span>
* <span data-ttu-id="b0592-154">**金鑰** 可讓您交換您的主要和次要 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="b0592-154">**Keys** allows you to rotate your primary and secondary API keys.</span></span>
* <span data-ttu-id="b0592-155">**儲存體帳戶金鑰**可讓您為與 Web 服務變更相關聯的儲存體帳戶更新金鑰。</span><span class="sxs-lookup"><span data-stu-id="b0592-155">**Storage account key** allows you to update the key for the storage account associated with the Web service changes.</span></span> 
* <span data-ttu-id="b0592-156">[啟用範例資料] 可讓您提供範例資料，用來測試要求-回應服務。</span><span class="sxs-lookup"><span data-stu-id="b0592-156">**Enable Sample data** allows you to provide sample data that you can use to test the Request-Response service.</span></span> <span data-ttu-id="b0592-157">如果您是在 Machine Learning Studio 中建立 Web 服務，範例資料會取自您用來訓練模型的資料。</span><span class="sxs-lookup"><span data-stu-id="b0592-157">If you created the web service in Machine Learning Studio, the sample data is taken from the data your used to train your model.</span></span> <span data-ttu-id="b0592-158">如果您是以程式設計方式建立服務，資料會取自您提供做為 JSON 套件一部分的範例資料。</span><span class="sxs-lookup"><span data-stu-id="b0592-158">If you created the service programmatically, the data is taken from the example data you provided as part of the JSON package.</span></span>

### <a name="managing-billing-plans"></a><span data-ttu-id="b0592-159">管理計費方案</span><span class="sxs-lookup"><span data-stu-id="b0592-159">Managing billing plans</span></span>
<span data-ttu-id="b0592-160">從 Web 服務 [快速入門] 頁面按一下 [方案]  功能表選項。</span><span class="sxs-lookup"><span data-stu-id="b0592-160">Click the **Plans** menu option from the web services Quickstart page.</span></span> <span data-ttu-id="b0592-161">您也可以按一下與特定 Web 服務相關聯的方案來管理該方案。</span><span class="sxs-lookup"><span data-stu-id="b0592-161">You can also click the plan associated with specific Web service to manage that plan.</span></span>

* <span data-ttu-id="b0592-162">**新增** 可讓您建立新的方案。</span><span class="sxs-lookup"><span data-stu-id="b0592-162">**New** allows you to create a new plan.</span></span>
* <span data-ttu-id="b0592-163">**新增/移除方案執行個體** 可讓您「相應放大」現有的方案以增加容量。</span><span class="sxs-lookup"><span data-stu-id="b0592-163">**Add/Remove Plan instance** allows you to "scale out" an existing plan to add capacity.</span></span>
* <span data-ttu-id="b0592-164">**升級/降級** 可讓您「相應增加」現有的方案以增加容量。</span><span class="sxs-lookup"><span data-stu-id="b0592-164">**Upgrade/DownGrade** allows you to "scale up" an existing plan to add capacity.</span></span>
* <span data-ttu-id="b0592-165">**刪除** 可讓您刪除方案。</span><span class="sxs-lookup"><span data-stu-id="b0592-165">**Delete** allows you to delete a plan.</span></span>

<span data-ttu-id="b0592-166">按一下方案可檢視其儀表板。</span><span class="sxs-lookup"><span data-stu-id="b0592-166">Click a plan to view its dashboard.</span></span> <span data-ttu-id="b0592-167">儀表板可提供所選一段時間的快照或方案使用量。</span><span class="sxs-lookup"><span data-stu-id="b0592-167">The dashboard gives you snapshot or plan usage over a selected period of time.</span></span> <span data-ttu-id="b0592-168">若要選取時間期間來檢視，請按一下儀表板右上角的 [期間] 下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="b0592-168">To select the time period to view, click the **Period** dropdown at the upper right of dashboard.</span></span> 

<span data-ttu-id="b0592-169">方案儀表板會提供下列資訊：</span><span class="sxs-lookup"><span data-stu-id="b0592-169">The plan dashboard provides the following information:</span></span>

* <span data-ttu-id="b0592-170">**方案描述** 顯示成本相關資訊和與方案相關聯的容量。</span><span class="sxs-lookup"><span data-stu-id="b0592-170">**Plan Description** displays information about the costs and capacity associated with the plan.</span></span>
* <span data-ttu-id="b0592-171">**方案使用量** 顯示交易數目和已依方案計費的計算時數。</span><span class="sxs-lookup"><span data-stu-id="b0592-171">**Plan Usage** displays the number of transactions and compute hours that have been charged against the plan.</span></span>
* <span data-ttu-id="b0592-172">**Web 服務數**顯示使用此方案的 Web 服務數目。</span><span class="sxs-lookup"><span data-stu-id="b0592-172">**Web Services** displays the number of Web services that are using this plan.</span></span>
* <span data-ttu-id="b0592-173">**依呼叫數的前幾名 Web 服務**顯示依方案計費進行呼叫的前四個 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="b0592-173">**Top Web Service By Calls** displays the top four Web services that are making calls that are charged against the plan.</span></span>
* <span data-ttu-id="b0592-174">**依計算時數的前幾名 Web 服務**顯示依方案計費使用計算資源的前四個 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="b0592-174">**Top Web Services by Compute Hrs** displays the top four Web services that are using compute resources that are charged against the plan.</span></span>

## <a name="manage-classic-web-services"></a><span data-ttu-id="b0592-175">管理傳統 Web 服務</span><span class="sxs-lookup"><span data-stu-id="b0592-175">Manage Classic Web Services</span></span>
> [!NOTE]
> <span data-ttu-id="b0592-176">本節的程序是關於透過 Azure Machine Learning Web 服務入口網站來管理傳統 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="b0592-176">The procedures in this section are relevant to managing Classic web services through the Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="b0592-177">如需透過 Machine Learning Studio 和 Azure 傳統入口網站管理傳統 Web 服務的相關資訊，請參閱[管理 Azure Machine Learning 工作區](machine-learning-manage-workspace.md)。</span><span class="sxs-lookup"><span data-stu-id="b0592-177">For information on managing Classic Web services through the Machine Learning Studio and the Azure classic portal, see [Manage an Azure Machine Learning workspace](machine-learning-manage-workspace.md).</span></span>
> 
> 

<span data-ttu-id="b0592-178">管理傳統 Web 服務：</span><span class="sxs-lookup"><span data-stu-id="b0592-178">To manage your Classic Web services:</span></span>

1. <span data-ttu-id="b0592-179">使用您的 Microsoft Azure 帳戶登入 [Microsoft Azure Machine Learning Web 服務入口網站](https://services.azureml.net/quickstart) - 使用與 Azure 訂用帳戶相關聯的帳戶。</span><span class="sxs-lookup"><span data-stu-id="b0592-179">Sign in to the [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal using your Microsoft Azure account - use the account that's associated with the Azure subscription.</span></span>
2. <span data-ttu-id="b0592-180">在功能表上，按一下 [傳統 Web 服務]。</span><span class="sxs-lookup"><span data-stu-id="b0592-180">On the menu, click **Classic Web Services**.</span></span>

<span data-ttu-id="b0592-181">若要管理傳統 Web 服務，請按一下 [傳統 Web 服務]。</span><span class="sxs-lookup"><span data-stu-id="b0592-181">To manage a Classic Web Service, click **Classic Web Services**.</span></span> <span data-ttu-id="b0592-182">您可以從 [傳統 Web 服務] 頁面上︰</span><span class="sxs-lookup"><span data-stu-id="b0592-182">From the Classic Web Services page you can:</span></span>

* <span data-ttu-id="b0592-183">按一下 Web 服務以檢視相關聯的端點。</span><span class="sxs-lookup"><span data-stu-id="b0592-183">Click the web service to view the associated endpoints.</span></span>
* <span data-ttu-id="b0592-184">刪除 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="b0592-184">Delete a web service.</span></span>

<span data-ttu-id="b0592-185">管理傳統 Web 服務時是個別管理每個端點。</span><span class="sxs-lookup"><span data-stu-id="b0592-185">When you manage a Classic Web service, you manage each of the endpoints separately.</span></span> <span data-ttu-id="b0592-186">當您按一下 [Web 服務] 頁面中的 Web 服務時，將會開啟與服務相關聯的端點清單。</span><span class="sxs-lookup"><span data-stu-id="b0592-186">When you click a web service in the Web Services page, the list of endpoints associated with the service opens.</span></span> 

<span data-ttu-id="b0592-187">在 [傳統 Web 服務端點] 頁面上，您可以新增和刪除服務的端點。</span><span class="sxs-lookup"><span data-stu-id="b0592-187">On the Classic Web Service endpoint page, you can add and delete endpoints on the service.</span></span> <span data-ttu-id="b0592-188">如需有關新增端點的詳細資訊，請參閱 [建立端點](machine-learning-create-endpoint.md)。</span><span class="sxs-lookup"><span data-stu-id="b0592-188">For more information on adding endpoints, see [Creating Endpoints](machine-learning-create-endpoint.md).</span></span>

<span data-ttu-id="b0592-189">按一下其中一個端點，以開啟 Web 服務 [快速入門] 頁面。</span><span class="sxs-lookup"><span data-stu-id="b0592-189">Click one of the endpoints to open the web service Quickstart page.</span></span> <span data-ttu-id="b0592-190">[快速入門] 頁面有兩個功能表選項可讓您管理 Web 服務︰</span><span class="sxs-lookup"><span data-stu-id="b0592-190">On the Quickstart page, there are two menu options that allow you to manage your web service:</span></span>

* <span data-ttu-id="b0592-191">**儀表板** -可讓您檢視 Web 服務使用量。</span><span class="sxs-lookup"><span data-stu-id="b0592-191">**DASHBOARD** - Allows you to view Web service usage.</span></span>
* <span data-ttu-id="b0592-192">**設定** -可讓您新增描述性文字、開啟和關閉錯誤記錄、更新與 Web 服務相關聯的儲存體帳戶金鑰，以及啟用和停用範例資料。</span><span class="sxs-lookup"><span data-stu-id="b0592-192">**CONFIGURE** - Allows you to add descriptive text, turn error logging on and off, update the key for the storage account associated with the Web service, and enable and disable sample data.</span></span>

### <a name="monitoring-how-the-web-service-is-being-used"></a><span data-ttu-id="b0592-193">監視 Web 服務的使用方式</span><span class="sxs-lookup"><span data-stu-id="b0592-193">Monitoring how the web service is being used</span></span>
<span data-ttu-id="b0592-194">按一下 [ **儀表板** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="b0592-194">Click the **DASHBOARD** tab.</span></span>

<span data-ttu-id="b0592-195">您可以從儀表板中檢視您的 Web 服務經過一段時間的整體使用量。</span><span class="sxs-lookup"><span data-stu-id="b0592-195">From the dashboard, you can view overall usage of your Web service over a period of time.</span></span> <span data-ttu-id="b0592-196">您可以從使用量圖表右上角的 [期間] 下拉式功能表中選取要檢視的期間。</span><span class="sxs-lookup"><span data-stu-id="b0592-196">You can select the period to view from the Period dropdown menu in the upper right of the usage charts.</span></span> <span data-ttu-id="b0592-197">儀表板會顯示下列資訊：</span><span class="sxs-lookup"><span data-stu-id="b0592-197">The dashboard shows the following information:</span></span>

* <span data-ttu-id="b0592-198">**一段時間的要求數** 顯示選取的一段時間內，要求數目的步階圖形。</span><span class="sxs-lookup"><span data-stu-id="b0592-198">**Requests Over Time** displays a step graph of the number of requests over the selected time period.</span></span> <span data-ttu-id="b0592-199">它可以協助識別您所遇到的使用量尖峰。</span><span class="sxs-lookup"><span data-stu-id="b0592-199">It can help identify if you are experiencing spikes in usage.</span></span>
* <span data-ttu-id="b0592-200">**要求-回應要求數** 顯示服務在選取的一段時間內收到的要求-回應呼叫總數，以及失敗的數目。</span><span class="sxs-lookup"><span data-stu-id="b0592-200">**Request-Response Requests** displays the total number of Request-Response calls the service has received over the selected time period and how many of them failed.</span></span>
* <span data-ttu-id="b0592-201">**平均要求-回應計算時間** 顯示執行收到的要求所需的平均時間。</span><span class="sxs-lookup"><span data-stu-id="b0592-201">**Average Request-Response Compute Time** displays an average of the time needed to execute the received requests.</span></span>
* <span data-ttu-id="b0592-202">**批次要求數** 顯示服務在選取的一段時間內收到的批次要求總數，以及失敗的數目。</span><span class="sxs-lookup"><span data-stu-id="b0592-202">**Batch Requests** displays the total number of Batch Requests the service has received over the selected time period and how many of them failed.</span></span>
* <span data-ttu-id="b0592-203">**平均作業延遲** 顯示執行收到的要求所需的平均時間。</span><span class="sxs-lookup"><span data-stu-id="b0592-203">**Average Job Latency** displays an average of the time needed to execute the received requests.</span></span>
* <span data-ttu-id="b0592-204">**錯誤數**顯示呼叫 Web 服務時所發生的錯誤彙總數目。</span><span class="sxs-lookup"><span data-stu-id="b0592-204">**Errors** displays the aggregate number of errors that have occurred on calls to the web service.</span></span>
* <span data-ttu-id="b0592-205">**服務成本** 顯示與服務相關聯的計費方案費用。</span><span class="sxs-lookup"><span data-stu-id="b0592-205">**Services Costs** displays the charges for the billing plan associated with the service.</span></span>

### <a name="configuring-the-web-service"></a><span data-ttu-id="b0592-206">設定 Web 服務</span><span class="sxs-lookup"><span data-stu-id="b0592-206">Configuring the web service</span></span>
<span data-ttu-id="b0592-207">按一下 [設定]  功能表選項。</span><span class="sxs-lookup"><span data-stu-id="b0592-207">Click the **CONFIGURE** menu option.</span></span>

<span data-ttu-id="b0592-208">您可以更新下列屬性：</span><span class="sxs-lookup"><span data-stu-id="b0592-208">You can update the following properties:</span></span>

* <span data-ttu-id="b0592-209">[描述] 可讓您輸入 Web 服務的描述。</span><span class="sxs-lookup"><span data-stu-id="b0592-209">**Description** allows you to enter a description for the Web service.</span></span> <span data-ttu-id="b0592-210">[描述] 必要欄位。</span><span class="sxs-lookup"><span data-stu-id="b0592-210">Description is a required field.</span></span>
* <span data-ttu-id="b0592-211">[記錄] 可讓您啟用或停用端點上的錯誤記錄。</span><span class="sxs-lookup"><span data-stu-id="b0592-211">**Logging** allows you to enable or disable error logging on the endpoint.</span></span> <span data-ttu-id="b0592-212">如需有關記錄的詳細資訊，請參閱[為 Machine Learning Web 服務啟用記錄](machine-learning-web-services-logging.md)。</span><span class="sxs-lookup"><span data-stu-id="b0592-212">For more information on Logging, see Enable [logging for Machine Learning web services](machine-learning-web-services-logging.md).</span></span>
* <span data-ttu-id="b0592-213">[啟用範例資料] 可讓您提供範例資料，用來測試要求-回應服務。</span><span class="sxs-lookup"><span data-stu-id="b0592-213">**Enable Sample data** allows you to provide sample data that you can use to test the Request-Response service.</span></span> <span data-ttu-id="b0592-214">如果您是在 Machine Learning Studio 中建立 Web 服務，範例資料會取自您用來訓練模型的資料。</span><span class="sxs-lookup"><span data-stu-id="b0592-214">If you created the web service in Machine Learning Studio, the sample data is taken from the data your used to train your model.</span></span> <span data-ttu-id="b0592-215">如果您是以程式設計方式建立服務，資料會取自您提供做為 JSON 套件一部分的範例資料。</span><span class="sxs-lookup"><span data-stu-id="b0592-215">If you created the service programmatically, the data is taken from the example data you provided as part of the JSON package.</span></span>

## <a name="grant-or-suspend-access-to-web-services-for-users-in-the-portal"></a><span data-ttu-id="b0592-216">在入口網站中授與或暫停使用者對 Web 服務的存取</span><span class="sxs-lookup"><span data-stu-id="b0592-216">Grant or suspend access to Web services for users in the portal</span></span>
<span data-ttu-id="b0592-217">您可以使用 Azure 傳統入口網站來允許或拒絕特定使用者的存取。</span><span class="sxs-lookup"><span data-stu-id="b0592-217">Using the Azure classic portal, you can allow or deny access to specific users.</span></span>

### <a name="access-for-users-of-new-web-services"></a><span data-ttu-id="b0592-218">新式 Web 服務的使用者存取</span><span class="sxs-lookup"><span data-stu-id="b0592-218">Access for users of New Web services</span></span>
<span data-ttu-id="b0592-219">若要讓其他使用者在 Azure Machine Learning Web 服務入口網站中使用您的 Web 服務，您必須將他們新增為 Azure 訂用帳戶的共同管理員。</span><span class="sxs-lookup"><span data-stu-id="b0592-219">To enable other users to work with your Web services in the Azure Machine Learning Web Services portal, you must add them as co-adminstrators on your Azure subscription.</span></span>

<span data-ttu-id="b0592-220">使用您的 Microsoft Azure 帳戶登入 [Azure 傳統入口網站](https://manage.windowsazure.com/) - 使用與 Azure 訂用帳戶相關聯的帳戶。</span><span class="sxs-lookup"><span data-stu-id="b0592-220">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) using your Microsoft Azure account - use the account that's associated with the Azure subscription.</span></span>

1. <span data-ttu-id="b0592-221">在導覽窗格中按一下 [設定]，然後按一下 [系統管理員]。</span><span class="sxs-lookup"><span data-stu-id="b0592-221">In the navigation pane, click **Settings**, then click **Administrators**.</span></span>
2. <span data-ttu-id="b0592-222">在視窗底部按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="b0592-222">At the bottom of the window, click **Add**.</span></span> 
3. <span data-ttu-id="b0592-223">在 [新增共同管理員] 對話方塊中，輸入您想新增為共同管理員之人員的電子郵件地址，然後選取您想讓共同管理員存取的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b0592-223">In the ADD A CO-ADMINISTRATOR dialog, type the email address of the person you want to add as Co-administrator and then select the subscription that you want the Co-administrator to access.</span></span>
4. <span data-ttu-id="b0592-224">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="b0592-224">Click **Save**.</span></span>

### <a name="access-for-users-of-classic-web-services"></a><span data-ttu-id="b0592-225">傳統 Web 服務的使用者存取</span><span class="sxs-lookup"><span data-stu-id="b0592-225">Access for users of Classic Web services</span></span>
<span data-ttu-id="b0592-226">若要管理工作區：</span><span class="sxs-lookup"><span data-stu-id="b0592-226">To manage a workspace:</span></span>

<span data-ttu-id="b0592-227">使用您的 Microsoft Azure 帳戶登入 [Azure 傳統入口網站](https://manage.windowsazure.com/) - 使用與 Azure 訂用帳戶相關聯的帳戶。</span><span class="sxs-lookup"><span data-stu-id="b0592-227">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) using your Microsoft Azure account - use the account that's associated with the Azure subscription.</span></span>

1. <span data-ttu-id="b0592-228">在 Microsoft Azure 服務面板中，按一下 [機器學習] 。</span><span class="sxs-lookup"><span data-stu-id="b0592-228">In the Microsoft Azure services panel, click **MACHINE LEARNING**.</span></span>
2. <span data-ttu-id="b0592-229">按一下您想要管理的工作區。</span><span class="sxs-lookup"><span data-stu-id="b0592-229">Click the workspace you want to manage.</span></span>
3. <span data-ttu-id="b0592-230">按一下 [設定]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="b0592-230">Click the **CONFIGURE** tab.</span></span>

<span data-ttu-id="b0592-231">從 [設定] 索引標籤中，您可以按一下 [拒絕] 來擱置對 Machine Learning 工作區的存取。</span><span class="sxs-lookup"><span data-stu-id="b0592-231">From the configuration tab, you can suspend access to the Machine Learning workspace by clicking **DENY**.</span></span> <span data-ttu-id="b0592-232">使用者將不再能在 Machine Learning Studio 中開啟工作區。</span><span class="sxs-lookup"><span data-stu-id="b0592-232">Users will no longer be able to open the workspace in Machine Learning Studio.</span></span> <span data-ttu-id="b0592-233">若要還原存取，請按一下 [允許]。</span><span class="sxs-lookup"><span data-stu-id="b0592-233">To restore access, click **ALLOW**.</span></span>

<span data-ttu-id="b0592-234">特定的使用者︰</span><span class="sxs-lookup"><span data-stu-id="b0592-234">To specific users:</span></span>

<span data-ttu-id="b0592-235">若要管理可以存取 Machine Learning Studio 中工作區的其他帳戶，請按一下 [儀表板] 索引標籤中的 [登入 ML Studio]。</span><span class="sxs-lookup"><span data-stu-id="b0592-235">To manage additional accounts who have access to the workspace in Machine Learning Studio, click **Sign-in to ML Studio** in the **DASHBOARD** tab.</span></span> <span data-ttu-id="b0592-236">這會在 Machine Learning Studio 中開啟工作區。</span><span class="sxs-lookup"><span data-stu-id="b0592-236">This opens the workspace in Machine Learning Studio.</span></span> <span data-ttu-id="b0592-237">從這裡按一下 [設定] 索引標籤，然後按一下 [使用者]。</span><span class="sxs-lookup"><span data-stu-id="b0592-237">From here, click the **SETTINGS** tab and then **USERS**.</span></span> <span data-ttu-id="b0592-238">您可以按一下 [邀請使用者]，讓使用者存取工作區，或選取使用者，並按一下 [移除]。</span><span class="sxs-lookup"><span data-stu-id="b0592-238">You can click **INVITE MORE USERS** to give users access to the workspace, or select a user and click **REMOVE**.</span></span>

> [!NOTE]
> <span data-ttu-id="b0592-239">[ **登入 ML Studio** ] 連結會使用目前登入的 Microsoft 帳戶來開啟 Machine Learning Studio。</span><span class="sxs-lookup"><span data-stu-id="b0592-239">The **Sign-in to ML Studio** link opens Machine Learning Studio using the Microsoft Account you are currently signed into.</span></span> <span data-ttu-id="b0592-240">您用來登入 Azure 傳統入口網站以建立工作區的 Microsoft 帳戶，不會自動具備開啟該工作區的權限。</span><span class="sxs-lookup"><span data-stu-id="b0592-240">The Microsoft Account you used to sign in to the Azure classic portal to create a workspace does not automatically have permission to open that workspace.</span></span> <span data-ttu-id="b0592-241">若要開啟工作區，您必須使用定義為工作區擁有者的 Microsoft 帳戶登入，或者您需要收到來自擁有者的邀請，才能加入工作區。</span><span class="sxs-lookup"><span data-stu-id="b0592-241">To open a workspace, you must be signed in to the Microsoft Account that was defined as the owner of the workspace, or you need to receive an invitation from the owner to join the workspace.</span></span>
> 
> 

