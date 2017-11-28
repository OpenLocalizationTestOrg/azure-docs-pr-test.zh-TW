---
title: "aaaUse hello Azure 機器學習 Web 服務入口網站 |Microsoft 文件"
description: "管理存取 tooAzure 機器學習服務工作區，並將部署和管理 ML API web 服務"
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
ms.openlocfilehash: 04b49027fc0ab227382b320310088bb66aafacc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-web-service-using-hello-azure-machine-learning-web-services-portal"></a><span data-ttu-id="58fa5-103">管理 Web 服務使用 hello Azure 機器學習 Web 服務入口網站</span><span class="sxs-lookup"><span data-stu-id="58fa5-103">Manage a Web service using hello Azure Machine Learning Web Services portal</span></span>
<span data-ttu-id="58fa5-104">您可以管理您使用 hello Microsoft Azure 機器學習 Web 服務入口網站的機器學習新的和傳統的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="58fa5-104">You can manage your Machine Learning New and Classic Web services using hello Microsoft Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="58fa5-105">因為傳統 Web 服務和新式 Web 服務是根據不同的基礎技術，所以各有稍微不同的管理功能。</span><span class="sxs-lookup"><span data-stu-id="58fa5-105">Since Classic Web services and New Web services are based on different underlying technologies, you have slightly different management capabilities for each of them.</span></span>

<span data-ttu-id="58fa5-106">在 hello 機器學習 Web 服務入口網站中，您可以：</span><span class="sxs-lookup"><span data-stu-id="58fa5-106">In hello Machine Learning Web Services portal you can:</span></span>

* <span data-ttu-id="58fa5-107">監視 hello web 服務的使用方式。</span><span class="sxs-lookup"><span data-stu-id="58fa5-107">Monitor how hello web service is being used.</span></span>
* <span data-ttu-id="58fa5-108">設定 hello 描述，請更新 hello 金鑰 hello web 服務 （僅新）、 更新金鑰 （新增只），啟用記錄，您儲存體帳戶和啟用或停用的範例資料。</span><span class="sxs-lookup"><span data-stu-id="58fa5-108">Configure hello description, update hello keys for hello web service (New only), update your storage account key (New only), enable logging, and enable or disable sample data.</span></span>
* <span data-ttu-id="58fa5-109">刪除 hello web 服務。</span><span class="sxs-lookup"><span data-stu-id="58fa5-109">Delete hello web service.</span></span>
* <span data-ttu-id="58fa5-110">建立、刪除或更新計費方案 (僅限新式)。</span><span class="sxs-lookup"><span data-stu-id="58fa5-110">Create, delete, or update billing plans (New only).</span></span>
* <span data-ttu-id="58fa5-111">新增和刪除端點 (僅限傳統)</span><span class="sxs-lookup"><span data-stu-id="58fa5-111">Add and delete endpoints (Classic only)</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="permissions-toomanage-new-resources-manager-based-web-services"></a><span data-ttu-id="58fa5-112">新的資源管理員的權限 toomanage 為基礎的 web 服務</span><span class="sxs-lookup"><span data-stu-id="58fa5-112">Permissions toomanage New Resources Manager based web services</span></span>

<span data-ttu-id="58fa5-113">新的 Web 服務會部署為 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="58fa5-113">New web services are deployed as Azure resources.</span></span> <span data-ttu-id="58fa5-114">因此，您必須擁有 hello 正確的權限 toodeploy 和管理新的 web 服務。</span><span class="sxs-lookup"><span data-stu-id="58fa5-114">As such, you must have hello correct permissions toodeploy and manage New web services.</span></span>  <span data-ttu-id="58fa5-115">toodeploy 或管理您的參與者必須被指派新的 web 服務或部署 hello 訂用帳戶 toowhich hello web 服務上的系統管理員角色。</span><span class="sxs-lookup"><span data-stu-id="58fa5-115">toodeploy or manage New web services you must be assigned a contributor or administrator role on hello subscription toowhich hello web service is deployed.</span></span> <span data-ttu-id="58fa5-116">您可以邀請其他使用者 tooa 機器學習服務工作區，您必須指派它們 tooa 參與者或系統管理員角色，hello 訂用帳戶才能部署或管理 web 服務。</span><span class="sxs-lookup"><span data-stu-id="58fa5-116">If you invite another user tooa machine learning workspace, you must assign them tooa contributor or administrator role on hello subscription before they can deploy or manage web services.</span></span> 

<span data-ttu-id="58fa5-117">若 hello 使用者沒有正確權限 tooaccess 資源 hello Azure 機器學習 Web 服務入口網站中的 hello，就會收到下列錯誤，當嘗試 toodeploy web 服務的 hello:</span><span class="sxs-lookup"><span data-stu-id="58fa5-117">If hello user does not have hello correct permissions tooaccess resources in hello Azure Machine Learning Web Services portal, they will receive hello following error when trying toodeploy a web service:</span></span>

<span data-ttu-id="58fa5-118">*Web 服務部署工作失敗。此帳戶沒有足夠的存取 toohello 包含 hello 工作區的 Azure 訂用帳戶。順序 toodeploy Web 服務 tooAzure，hello 相同的帳戶必須是受邀 toohello 工作區，並可指定的存取 toohello Azure 訂用帳戶包含 hello 工作區。*</span><span class="sxs-lookup"><span data-stu-id="58fa5-118">*Web Service deployment failed. This account does not have sufficient access toohello Azure subscription that contains hello Workspace. In order toodeploy a Web Service tooAzure, hello same account must be invited toohello Workspace and be given access toohello Azure subscription that contains hello Workspace.*</span></span>

<span data-ttu-id="58fa5-119">如需建立工作區的詳細資訊，請參閱[建立和共用 Azure Machine Learning 工作區](machine-learning-create-workspace.md)。</span><span class="sxs-lookup"><span data-stu-id="58fa5-119">For more information on creating a workspace, see [Create and share an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

<span data-ttu-id="58fa5-120">如需設定存取權限的詳細資訊，請參閱[hello Azure 入口網站-公開預覽中的使用者及群組的檢視存取工作分派](../active-directory/role-based-access-control-manage-assignments.md)。</span><span class="sxs-lookup"><span data-stu-id="58fa5-120">For more information on setting access permissions, see [View access assignments for users and groups in hello Azure portal - Public preview](../active-directory/role-based-access-control-manage-assignments.md).</span></span>


## <a name="manage-new-web-services"></a><span data-ttu-id="58fa5-121">管理新式 Web 服務</span><span class="sxs-lookup"><span data-stu-id="58fa5-121">Manage New Web services</span></span>
<span data-ttu-id="58fa5-122">toomanage 至新的 Web 服務：</span><span class="sxs-lookup"><span data-stu-id="58fa5-122">toomanage your New Web services:</span></span>

1. <span data-ttu-id="58fa5-123">登入 toohello [Microsoft Azure 機器學習 Web 服務](https://services.azureml.net/quickstart)入口網站使用您的 Microsoft Azure 帳戶-使用 hello 帳戶相關聯 hello Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="58fa5-123">Sign in toohello [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal using your Microsoft Azure account - use hello account that's associated with hello Azure subscription.</span></span>
2. <span data-ttu-id="58fa5-124">在 [hello] 功能表上按一下**Web 服務**。</span><span class="sxs-lookup"><span data-stu-id="58fa5-124">On hello menu, click **Web Services**.</span></span>

<span data-ttu-id="58fa5-125">這會針對您的訂用帳戶顯示一份已部署的 Web 服務清單。</span><span class="sxs-lookup"><span data-stu-id="58fa5-125">This displays a list of deployed Web services for your subscription.</span></span> 

<span data-ttu-id="58fa5-126">toomanage Web 服務，按一下 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="58fa5-126">toomanage a Web service, click Web Services.</span></span> <span data-ttu-id="58fa5-127">您可以從 hello Web 服務 頁面上：</span><span class="sxs-lookup"><span data-stu-id="58fa5-127">From hello Web Services page you can:</span></span>

* <span data-ttu-id="58fa5-128">按一下 hello web 服務 toomanage 它。</span><span class="sxs-lookup"><span data-stu-id="58fa5-128">Click hello web service toomanage it.</span></span>
* <span data-ttu-id="58fa5-129">按一下 hello 計費計劃的 hello web 服務 tooupdate 它。</span><span class="sxs-lookup"><span data-stu-id="58fa5-129">Click hello Billing Plan for hello web service tooupdate it.</span></span>
* <span data-ttu-id="58fa5-130">刪除 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="58fa5-130">Delete a web service.</span></span>
* <span data-ttu-id="58fa5-131">複製 web 服務，並將它部署 tooanother 區域。</span><span class="sxs-lookup"><span data-stu-id="58fa5-131">Copy a web service and deploy it tooanother region.</span></span>

<span data-ttu-id="58fa5-132">當您按一下 web 服務時，hello web 服務快速入門 頁面隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="58fa5-132">When you click a web service, hello web service Quickstart page opens.</span></span> <span data-ttu-id="58fa5-133">hello web 服務快速入門頁面有兩個功能表選項，可讓您 toomanage web 服務：</span><span class="sxs-lookup"><span data-stu-id="58fa5-133">hello web service Quickstart page has two menu options that allow you toomanage your web service:</span></span>

* <span data-ttu-id="58fa5-134">**儀表板**-可讓您 tooview Web 服務使用。</span><span class="sxs-lookup"><span data-stu-id="58fa5-134">**DASHBOARD** - Allows you tooview Web service usage.</span></span>
* <span data-ttu-id="58fa5-135">**設定**-允許您 tooadd 描述性文字，更新 hello 機碼 hello 儲存體帳戶與相關聯的 hello Web 服務和啟用或停用的範例資料。</span><span class="sxs-lookup"><span data-stu-id="58fa5-135">**CONFIGURE** - Allows you tooadd descriptive text, update hello key for hello storage account associated with hello Web service, and enable or disable sample data.</span></span>

### <a name="monitoring-how-hello-web-service-is-being-used"></a><span data-ttu-id="58fa5-136">監視 hello web 服務的使用方式</span><span class="sxs-lookup"><span data-stu-id="58fa5-136">Monitoring how hello web service is being used</span></span>
<span data-ttu-id="58fa5-137">按一下 hello**儀表板** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="58fa5-137">Click hello **DASHBOARD** tab.</span></span>

<span data-ttu-id="58fa5-138">從 hello 儀表板，您可以檢視您的 Web 服務的整體使用狀況經過一段時間。</span><span class="sxs-lookup"><span data-stu-id="58fa5-138">From hello dashboard, you can view overall usage of your Web service over a period of time.</span></span> <span data-ttu-id="58fa5-139">您可以選取 hello 期間 tooview 從 hello 週期 下拉式功能表中的 hello 使用量圖表的 hello 右上方。</span><span class="sxs-lookup"><span data-stu-id="58fa5-139">You can select hello period tooview from hello Period dropdown menu in hello upper right of hello usage charts.</span></span> <span data-ttu-id="58fa5-140">hello 儀表板會顯示下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="58fa5-140">hello dashboard shows hello following information:</span></span>

* <span data-ttu-id="58fa5-141">**要求一段時間**會顯示選取的時間週期的 hello 步驟圖形 hello 要求數目。</span><span class="sxs-lookup"><span data-stu-id="58fa5-141">**Requests Over Time** displays a step graph of hello number of requests over hello selected time period.</span></span> <span data-ttu-id="58fa5-142">它可以協助識別您所遇到的使用量尖峰。</span><span class="sxs-lookup"><span data-stu-id="58fa5-142">It can help identify if you are experiencing spikes in usage.</span></span>
* <span data-ttu-id="58fa5-143">**要求-回應要求**顯示 hello 的 hello 服務已收到 hello 選的時段和多少個失敗的要求-回應呼叫次數總計。</span><span class="sxs-lookup"><span data-stu-id="58fa5-143">**Request-Response Requests** displays hello total number of Request-Response calls hello service has received over hello selected time period and how many of them failed.</span></span>
* <span data-ttu-id="58fa5-144">**平均要求回應計算時間**顯示 hello 時間的平均值的所需 tooexecute hello 收到要求。</span><span class="sxs-lookup"><span data-stu-id="58fa5-144">**Average Request-Response Compute Time** displays an average of hello time needed tooexecute hello received requests.</span></span>
* <span data-ttu-id="58fa5-145">**批次要求**顯示 hello 總數批次要求 hello 服務已收到透過選取的時間週期的 hello，且其中多少失敗。</span><span class="sxs-lookup"><span data-stu-id="58fa5-145">**Batch Requests** displays hello total number of Batch Requests hello service has received over hello selected time period and how many of them failed.</span></span>
* <span data-ttu-id="58fa5-146">**平均工作延遲**顯示 hello 時間的平均值的所需 tooexecute hello 收到要求。</span><span class="sxs-lookup"><span data-stu-id="58fa5-146">**Average Job Latency** displays an average of hello time needed tooexecute hello received requests.</span></span>
* <span data-ttu-id="58fa5-147">**錯誤**呼叫 toohello web 服務上顯示 hello 彙總數目所發生的錯誤。</span><span class="sxs-lookup"><span data-stu-id="58fa5-147">**Errors** displays hello aggregate number of errors that have occurred on calls toohello web service.</span></span>
* <span data-ttu-id="58fa5-148">**服務成本**顯示 hello 費用 hello 與 hello 服務相關聯的計費方案。</span><span class="sxs-lookup"><span data-stu-id="58fa5-148">**Services Costs** displays hello charges for hello billing plan associated with hello service.</span></span>

### <a name="configuring-hello-web-service"></a><span data-ttu-id="58fa5-149">設定 hello web 服務</span><span class="sxs-lookup"><span data-stu-id="58fa5-149">Configuring hello web service</span></span>
<span data-ttu-id="58fa5-150">按一下 hello**設定**功能表選項。</span><span class="sxs-lookup"><span data-stu-id="58fa5-150">Click hello **CONFIGURE** menu option.</span></span>

<span data-ttu-id="58fa5-151">您可以更新下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="58fa5-151">You can update hello following properties:</span></span>

* <span data-ttu-id="58fa5-152">**描述**可讓您 tooenter hello Web 服務的描述。</span><span class="sxs-lookup"><span data-stu-id="58fa5-152">**Description** allows you tooenter a description for hello Web service.</span></span>
* <span data-ttu-id="58fa5-153">**標題**可讓您 tooenter hello Web 服務的標題</span><span class="sxs-lookup"><span data-stu-id="58fa5-153">**Title** allows you tooenter a title for hello Web service</span></span>
* <span data-ttu-id="58fa5-154">**索引鍵**可讓您 toorotate 您主要和次要的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="58fa5-154">**Keys** allows you toorotate your primary and secondary API keys.</span></span>
* <span data-ttu-id="58fa5-155">**儲存體帳戶金鑰**可讓您 tooupdate hello hello hello Web 服務的變更與相關聯的儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="58fa5-155">**Storage account key** allows you tooupdate hello key for hello storage account associated with hello Web service changes.</span></span> 
* <span data-ttu-id="58fa5-156">**啟用範例資料**tooprovide 範例資料，您可以使用 tootest hello 要求-回應服務可讓您。</span><span class="sxs-lookup"><span data-stu-id="58fa5-156">**Enable Sample data** allows you tooprovide sample data that you can use tootest hello Request-Response service.</span></span> <span data-ttu-id="58fa5-157">如果您在 Machine Learning Studio 中建立 hello web 服務，hello 範例資料取自 hello 資料您使用的 tootrain 您的模型。</span><span class="sxs-lookup"><span data-stu-id="58fa5-157">If you created hello web service in Machine Learning Studio, hello sample data is taken from hello data your used tootrain your model.</span></span> <span data-ttu-id="58fa5-158">如果您以程式設計方式建立 hello 服務，hello 資料取自 hello 範例資料，您提供為 hello JSON 封裝的一部分。</span><span class="sxs-lookup"><span data-stu-id="58fa5-158">If you created hello service programmatically, hello data is taken from hello example data you provided as part of hello JSON package.</span></span>

### <a name="managing-billing-plans"></a><span data-ttu-id="58fa5-159">管理計費方案</span><span class="sxs-lookup"><span data-stu-id="58fa5-159">Managing billing plans</span></span>
<span data-ttu-id="58fa5-160">按一下 hello**計劃**從 hello web 服務快速入門 頁面上的功能表選項。</span><span class="sxs-lookup"><span data-stu-id="58fa5-160">Click hello **Plans** menu option from hello web services Quickstart page.</span></span> <span data-ttu-id="58fa5-161">您也可以按一下特定的 Web 服務 toomanage 計劃相關聯的 hello 計劃。</span><span class="sxs-lookup"><span data-stu-id="58fa5-161">You can also click hello plan associated with specific Web service toomanage that plan.</span></span>

* <span data-ttu-id="58fa5-162">**新**可讓您 toocreate 新計劃。</span><span class="sxs-lookup"><span data-stu-id="58fa5-162">**New** allows you toocreate a new plan.</span></span>
* <span data-ttu-id="58fa5-163">**新增/移除計劃的執行個體**可讓您太 「 向外延展 」 的現有的計劃 tooadd 容量。</span><span class="sxs-lookup"><span data-stu-id="58fa5-163">**Add/Remove Plan instance** allows you too"scale out" an existing plan tooadd capacity.</span></span>
* <span data-ttu-id="58fa5-164">**升級/降級**可讓您太 「 向上延展 」 的現有的計劃 tooadd 容量。</span><span class="sxs-lookup"><span data-stu-id="58fa5-164">**Upgrade/DownGrade** allows you too"scale up" an existing plan tooadd capacity.</span></span>
* <span data-ttu-id="58fa5-165">**刪除**可讓您 toodelete 計劃。</span><span class="sxs-lookup"><span data-stu-id="58fa5-165">**Delete** allows you toodelete a plan.</span></span>

<span data-ttu-id="58fa5-166">按一下計劃 tooview 其儀表板。</span><span class="sxs-lookup"><span data-stu-id="58fa5-166">Click a plan tooview its dashboard.</span></span> <span data-ttu-id="58fa5-167">hello 儀表板可讓您使用快照式或計劃在選取的一段時間。</span><span class="sxs-lookup"><span data-stu-id="58fa5-167">hello dashboard gives you snapshot or plan usage over a selected period of time.</span></span> <span data-ttu-id="58fa5-168">tooselect hello 時間週期 tooview 中，按一下 hello**期間**在儀表板的 hello 右上方的下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="58fa5-168">tooselect hello time period tooview, click hello **Period** dropdown at hello upper right of dashboard.</span></span> 

<span data-ttu-id="58fa5-169">hello 方案儀表板提供下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="58fa5-169">hello plan dashboard provides hello following information:</span></span>

* <span data-ttu-id="58fa5-170">**計劃描述**顯示 hello 成本和 hello 計劃相關聯的容量資訊。</span><span class="sxs-lookup"><span data-stu-id="58fa5-170">**Plan Description** displays information about hello costs and capacity associated with hello plan.</span></span>
* <span data-ttu-id="58fa5-171">**規劃使用**顯示 hello 的交易和已付費 hello 計劃的計算時數的數字。</span><span class="sxs-lookup"><span data-stu-id="58fa5-171">**Plan Usage** displays hello number of transactions and compute hours that have been charged against hello plan.</span></span>
* <span data-ttu-id="58fa5-172">**Web 服務**顯示使用此計劃的 Web 服務的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="58fa5-172">**Web Services** displays hello number of Web services that are using this plan.</span></span>
* <span data-ttu-id="58fa5-173">**排名最前面的 Web 服務所呼叫**顯示 hello 前四個 Web 服務，都需支付 hello 計劃的呼叫。</span><span class="sxs-lookup"><span data-stu-id="58fa5-173">**Top Web Service By Calls** displays hello top four Web services that are making calls that are charged against hello plan.</span></span>
* <span data-ttu-id="58fa5-174">**Web 服務前所計算的小時**顯示 hello 前四個 Web 服務使用 hello 計劃需支付的運算資源。</span><span class="sxs-lookup"><span data-stu-id="58fa5-174">**Top Web Services by Compute Hrs** displays hello top four Web services that are using compute resources that are charged against hello plan.</span></span>

## <a name="manage-classic-web-services"></a><span data-ttu-id="58fa5-175">管理傳統 Web 服務</span><span class="sxs-lookup"><span data-stu-id="58fa5-175">Manage Classic Web Services</span></span>
> [!NOTE]
> <span data-ttu-id="58fa5-176">本節中的 hello 程序是透過 hello Azure 機器學習 Web 服務入口網站的相關 toomanaging 傳統 web 服務。</span><span class="sxs-lookup"><span data-stu-id="58fa5-176">hello procedures in this section are relevant toomanaging Classic web services through hello Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="58fa5-177">如需管理傳統 Web 服務透過 hello Machine Learning Studio 和 hello Azure 傳統入口網站，請參閱[管理 Azure Machine Learning 工作區](machine-learning-manage-workspace.md)。</span><span class="sxs-lookup"><span data-stu-id="58fa5-177">For information on managing Classic Web services through hello Machine Learning Studio and hello Azure classic portal, see [Manage an Azure Machine Learning workspace](machine-learning-manage-workspace.md).</span></span>
> 
> 

<span data-ttu-id="58fa5-178">toomanage 傳統 Web 服務：</span><span class="sxs-lookup"><span data-stu-id="58fa5-178">toomanage your Classic Web services:</span></span>

1. <span data-ttu-id="58fa5-179">登入 toohello [Microsoft Azure 機器學習 Web 服務](https://services.azureml.net/quickstart)入口網站使用您的 Microsoft Azure 帳戶-使用 hello 帳戶相關聯 hello Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="58fa5-179">Sign in toohello [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/quickstart) portal using your Microsoft Azure account - use hello account that's associated with hello Azure subscription.</span></span>
2. <span data-ttu-id="58fa5-180">在 [hello] 功能表上按一下**傳統 Web 服務**。</span><span class="sxs-lookup"><span data-stu-id="58fa5-180">On hello menu, click **Classic Web Services**.</span></span>

<span data-ttu-id="58fa5-181">toomanage 傳統的 Web 服務，按一下**傳統 Web 服務**。</span><span class="sxs-lookup"><span data-stu-id="58fa5-181">toomanage a Classic Web Service, click **Classic Web Services**.</span></span> <span data-ttu-id="58fa5-182">您可以從 hello 傳統 Web 服務 頁面上：</span><span class="sxs-lookup"><span data-stu-id="58fa5-182">From hello Classic Web Services page you can:</span></span>

* <span data-ttu-id="58fa5-183">按一下 hello web 服務 tooview 相關聯的 hello 端點。</span><span class="sxs-lookup"><span data-stu-id="58fa5-183">Click hello web service tooview hello associated endpoints.</span></span>
* <span data-ttu-id="58fa5-184">刪除 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="58fa5-184">Delete a web service.</span></span>

<span data-ttu-id="58fa5-185">當您管理的傳統 Web 服務時，您每個 hello 端點分開管理。</span><span class="sxs-lookup"><span data-stu-id="58fa5-185">When you manage a Classic Web service, you manage each of hello endpoints separately.</span></span> <span data-ttu-id="58fa5-186">當您按一下 hello Web 服務 頁面中的 web 服務時，會開啟 hello 與 hello 服務相關聯的端點清單。</span><span class="sxs-lookup"><span data-stu-id="58fa5-186">When you click a web service in hello Web Services page, hello list of endpoints associated with hello service opens.</span></span> 

<span data-ttu-id="58fa5-187">在 hello 傳統 Web 服務端點 頁面上，您可以加入及刪除 hello 服務上的端點。</span><span class="sxs-lookup"><span data-stu-id="58fa5-187">On hello Classic Web Service endpoint page, you can add and delete endpoints on hello service.</span></span> <span data-ttu-id="58fa5-188">如需有關新增端點的詳細資訊，請參閱 [建立端點](machine-learning-create-endpoint.md)。</span><span class="sxs-lookup"><span data-stu-id="58fa5-188">For more information on adding endpoints, see [Creating Endpoints](machine-learning-create-endpoint.md).</span></span>

<span data-ttu-id="58fa5-189">按一下其中一個 hello 端點 tooopen hello web 服務快速入門頁面。</span><span class="sxs-lookup"><span data-stu-id="58fa5-189">Click one of hello endpoints tooopen hello web service Quickstart page.</span></span> <span data-ttu-id="58fa5-190">在 hello 快速入門 頁面上，有兩個功能表選項，可讓您 toomanage web 服務：</span><span class="sxs-lookup"><span data-stu-id="58fa5-190">On hello Quickstart page, there are two menu options that allow you toomanage your web service:</span></span>

* <span data-ttu-id="58fa5-191">**儀表板**-可讓您 tooview Web 服務使用。</span><span class="sxs-lookup"><span data-stu-id="58fa5-191">**DASHBOARD** - Allows you tooview Web service usage.</span></span>
* <span data-ttu-id="58fa5-192">**設定**-tooadd 描述性文字，可讓您開啟錯誤記錄開啟或關閉更新 hello 機 hello 儲存體帳戶與相關聯的 hello Web 服務，以及啟用和停用的範例資料。</span><span class="sxs-lookup"><span data-stu-id="58fa5-192">**CONFIGURE** - Allows you tooadd descriptive text, turn error logging on and off, update hello key for hello storage account associated with hello Web service, and enable and disable sample data.</span></span>

### <a name="monitoring-how-hello-web-service-is-being-used"></a><span data-ttu-id="58fa5-193">監視 hello web 服務的使用方式</span><span class="sxs-lookup"><span data-stu-id="58fa5-193">Monitoring how hello web service is being used</span></span>
<span data-ttu-id="58fa5-194">按一下 hello**儀表板** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="58fa5-194">Click hello **DASHBOARD** tab.</span></span>

<span data-ttu-id="58fa5-195">從 hello 儀表板，您可以檢視您的 Web 服務的整體使用狀況經過一段時間。</span><span class="sxs-lookup"><span data-stu-id="58fa5-195">From hello dashboard, you can view overall usage of your Web service over a period of time.</span></span> <span data-ttu-id="58fa5-196">您可以選取 hello 期間 tooview 從 hello 週期 下拉式功能表中的 hello 使用量圖表的 hello 右上方。</span><span class="sxs-lookup"><span data-stu-id="58fa5-196">You can select hello period tooview from hello Period dropdown menu in hello upper right of hello usage charts.</span></span> <span data-ttu-id="58fa5-197">hello 儀表板會顯示下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="58fa5-197">hello dashboard shows hello following information:</span></span>

* <span data-ttu-id="58fa5-198">**要求一段時間**會顯示選取的時間週期的 hello 步驟圖形 hello 要求數目。</span><span class="sxs-lookup"><span data-stu-id="58fa5-198">**Requests Over Time** displays a step graph of hello number of requests over hello selected time period.</span></span> <span data-ttu-id="58fa5-199">它可以協助識別您所遇到的使用量尖峰。</span><span class="sxs-lookup"><span data-stu-id="58fa5-199">It can help identify if you are experiencing spikes in usage.</span></span>
* <span data-ttu-id="58fa5-200">**要求-回應要求**顯示 hello 的 hello 服務已收到 hello 選的時段和多少個失敗的要求-回應呼叫次數總計。</span><span class="sxs-lookup"><span data-stu-id="58fa5-200">**Request-Response Requests** displays hello total number of Request-Response calls hello service has received over hello selected time period and how many of them failed.</span></span>
* <span data-ttu-id="58fa5-201">**平均要求回應計算時間**顯示 hello 時間的平均值的所需 tooexecute hello 收到要求。</span><span class="sxs-lookup"><span data-stu-id="58fa5-201">**Average Request-Response Compute Time** displays an average of hello time needed tooexecute hello received requests.</span></span>
* <span data-ttu-id="58fa5-202">**批次要求**顯示 hello 總數批次要求 hello 服務已收到透過選取的時間週期的 hello，且其中多少失敗。</span><span class="sxs-lookup"><span data-stu-id="58fa5-202">**Batch Requests** displays hello total number of Batch Requests hello service has received over hello selected time period and how many of them failed.</span></span>
* <span data-ttu-id="58fa5-203">**平均工作延遲**顯示 hello 時間的平均值的所需 tooexecute hello 收到要求。</span><span class="sxs-lookup"><span data-stu-id="58fa5-203">**Average Job Latency** displays an average of hello time needed tooexecute hello received requests.</span></span>
* <span data-ttu-id="58fa5-204">**錯誤**呼叫 toohello web 服務上顯示 hello 彙總數目所發生的錯誤。</span><span class="sxs-lookup"><span data-stu-id="58fa5-204">**Errors** displays hello aggregate number of errors that have occurred on calls toohello web service.</span></span>
* <span data-ttu-id="58fa5-205">**服務成本**顯示 hello 費用 hello 與 hello 服務相關聯的計費方案。</span><span class="sxs-lookup"><span data-stu-id="58fa5-205">**Services Costs** displays hello charges for hello billing plan associated with hello service.</span></span>

### <a name="configuring-hello-web-service"></a><span data-ttu-id="58fa5-206">設定 hello web 服務</span><span class="sxs-lookup"><span data-stu-id="58fa5-206">Configuring hello web service</span></span>
<span data-ttu-id="58fa5-207">按一下 hello**設定**功能表選項。</span><span class="sxs-lookup"><span data-stu-id="58fa5-207">Click hello **CONFIGURE** menu option.</span></span>

<span data-ttu-id="58fa5-208">您可以更新下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="58fa5-208">You can update hello following properties:</span></span>

* <span data-ttu-id="58fa5-209">**描述**可讓您 tooenter hello Web 服務的描述。</span><span class="sxs-lookup"><span data-stu-id="58fa5-209">**Description** allows you tooenter a description for hello Web service.</span></span> <span data-ttu-id="58fa5-210">[描述] 必要欄位。</span><span class="sxs-lookup"><span data-stu-id="58fa5-210">Description is a required field.</span></span>
* <span data-ttu-id="58fa5-211">**記錄**可讓您登入 hello 端點 tooenable 或停用錯誤。</span><span class="sxs-lookup"><span data-stu-id="58fa5-211">**Logging** allows you tooenable or disable error logging on hello endpoint.</span></span> <span data-ttu-id="58fa5-212">如需有關記錄的詳細資訊，請參閱[為 Machine Learning Web 服務啟用記錄](machine-learning-web-services-logging.md)。</span><span class="sxs-lookup"><span data-stu-id="58fa5-212">For more information on Logging, see Enable [logging for Machine Learning web services](machine-learning-web-services-logging.md).</span></span>
* <span data-ttu-id="58fa5-213">**啟用範例資料**tooprovide 範例資料，您可以使用 tootest hello 要求-回應服務可讓您。</span><span class="sxs-lookup"><span data-stu-id="58fa5-213">**Enable Sample data** allows you tooprovide sample data that you can use tootest hello Request-Response service.</span></span> <span data-ttu-id="58fa5-214">如果您在 Machine Learning Studio 中建立 hello web 服務，hello 範例資料取自 hello 資料您使用的 tootrain 您的模型。</span><span class="sxs-lookup"><span data-stu-id="58fa5-214">If you created hello web service in Machine Learning Studio, hello sample data is taken from hello data your used tootrain your model.</span></span> <span data-ttu-id="58fa5-215">如果您以程式設計方式建立 hello 服務，hello 資料取自 hello 範例資料，您提供為 hello JSON 封裝的一部分。</span><span class="sxs-lookup"><span data-stu-id="58fa5-215">If you created hello service programmatically, hello data is taken from hello example data you provided as part of hello JSON package.</span></span>

## <a name="grant-or-suspend-access-tooweb-services-for-users-in-hello-portal"></a><span data-ttu-id="58fa5-216">授予或暫止 hello 入口網站中的使用者的存取 tooWeb 服務</span><span class="sxs-lookup"><span data-stu-id="58fa5-216">Grant or suspend access tooWeb services for users in hello portal</span></span>
<span data-ttu-id="58fa5-217">您可以使用 hello Azure 傳統入口網站，允許或拒絕存取 toospecific 使用者。</span><span class="sxs-lookup"><span data-stu-id="58fa5-217">Using hello Azure classic portal, you can allow or deny access toospecific users.</span></span>

### <a name="access-for-users-of-new-web-services"></a><span data-ttu-id="58fa5-218">新式 Web 服務的使用者存取</span><span class="sxs-lookup"><span data-stu-id="58fa5-218">Access for users of New Web services</span></span>
<span data-ttu-id="58fa5-219">tooenable hello Azure 機器學習 Web 服務入口網站中的 Web 服務與其他使用者 toowork，就必須加入為共同管理員 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="58fa5-219">tooenable other users toowork with your Web services in hello Azure Machine Learning Web Services portal, you must add them as co-adminstrators on your Azure subscription.</span></span>

<span data-ttu-id="58fa5-220">登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com/)使用 Microsoft Azure 帳戶-請使用 hello 與 hello Azure 訂用帳戶相關聯的帳戶。</span><span class="sxs-lookup"><span data-stu-id="58fa5-220">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) using your Microsoft Azure account - use hello account that's associated with hello Azure subscription.</span></span>

1. <span data-ttu-id="58fa5-221">Hello 瀏覽窗格中，按一下**設定**，然後按一下 **管理員**。</span><span class="sxs-lookup"><span data-stu-id="58fa5-221">In hello navigation pane, click **Settings**, then click **Administrators**.</span></span>
2. <span data-ttu-id="58fa5-222">在 hello hello 視窗底部，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="58fa5-222">At hello bottom of hello window, click **Add**.</span></span> 
3. <span data-ttu-id="58fa5-223">在 hello 新增的共同管理員 對話方塊中，輸入您要 tooadd 做為共同管理員及您想 hello 共同管理員 tooaccess 然後選取 hello 訂閱 hello 人員 hello 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="58fa5-223">In hello ADD A CO-ADMINISTRATOR dialog, type hello email address of hello person you want tooadd as Co-administrator and then select hello subscription that you want hello Co-administrator tooaccess.</span></span>
4. <span data-ttu-id="58fa5-224">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="58fa5-224">Click **Save**.</span></span>

### <a name="access-for-users-of-classic-web-services"></a><span data-ttu-id="58fa5-225">傳統 Web 服務的使用者存取</span><span class="sxs-lookup"><span data-stu-id="58fa5-225">Access for users of Classic Web services</span></span>
<span data-ttu-id="58fa5-226">toomanage 工作區：</span><span class="sxs-lookup"><span data-stu-id="58fa5-226">toomanage a workspace:</span></span>

<span data-ttu-id="58fa5-227">登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com/)使用 Microsoft Azure 帳戶-請使用 hello 與 hello Azure 訂用帳戶相關聯的帳戶。</span><span class="sxs-lookup"><span data-stu-id="58fa5-227">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) using your Microsoft Azure account - use hello account that's associated with hello Azure subscription.</span></span>

1. <span data-ttu-id="58fa5-228">在 hello Microsoft Azure 服務面板中，按一下  **MACHINE LEARNING**。</span><span class="sxs-lookup"><span data-stu-id="58fa5-228">In hello Microsoft Azure services panel, click **MACHINE LEARNING**.</span></span>
2. <span data-ttu-id="58fa5-229">按一下您想要 toomanage hello 工作區。</span><span class="sxs-lookup"><span data-stu-id="58fa5-229">Click hello workspace you want toomanage.</span></span>
3. <span data-ttu-id="58fa5-230">按一下 hello**設定** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="58fa5-230">Click hello **CONFIGURE** tab.</span></span>

<span data-ttu-id="58fa5-231">Hello 組態 索引標籤，您可以暫停存取 toohello Machine Learning 工作區依序按一下**拒絕**。</span><span class="sxs-lookup"><span data-stu-id="58fa5-231">From hello configuration tab, you can suspend access toohello Machine Learning workspace by clicking **DENY**.</span></span> <span data-ttu-id="58fa5-232">使用者將不再能夠 tooopen Machine Learning Studio 中的 hello 工作區。</span><span class="sxs-lookup"><span data-stu-id="58fa5-232">Users will no longer be able tooopen hello workspace in Machine Learning Studio.</span></span> <span data-ttu-id="58fa5-233">toorestore 存取按一下**允許**。</span><span class="sxs-lookup"><span data-stu-id="58fa5-233">toorestore access, click **ALLOW**.</span></span>

<span data-ttu-id="58fa5-234">toospecific 使用者：</span><span class="sxs-lookup"><span data-stu-id="58fa5-234">toospecific users:</span></span>

<span data-ttu-id="58fa5-235">toomanage 其他帳戶擁有存取 toohello 工作區，在機器學習 Studio 中，按一下**登入 tooML Studio**在 hello**儀表板** 索引標籤。這會開啟 Machine Learning Studio hello 工作區。</span><span class="sxs-lookup"><span data-stu-id="58fa5-235">toomanage additional accounts who have access toohello workspace in Machine Learning Studio, click **Sign-in tooML Studio** in hello **DASHBOARD** tab. This opens hello workspace in Machine Learning Studio.</span></span> <span data-ttu-id="58fa5-236">從這裡按一下 hello**設定** 索引標籤，然後**使用者**。</span><span class="sxs-lookup"><span data-stu-id="58fa5-236">From here, click hello **SETTINGS** tab and then **USERS**.</span></span> <span data-ttu-id="58fa5-237">您可以按一下**更邀請使用者**toogive 使用者存取 toohello 工作區中，或選取的使用者，然後按一下**移除**。</span><span class="sxs-lookup"><span data-stu-id="58fa5-237">You can click **INVITE MORE USERS** toogive users access toohello workspace, or select a user and click **REMOVE**.</span></span>

> [!NOTE]
> <span data-ttu-id="58fa5-238">hello**登入 tooML Studio**連結會開啟 Machine Learning Studio 使用 hello 目前登入的 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="58fa5-238">hello **Sign-in tooML Studio** link opens Machine Learning Studio using hello Microsoft Account you are currently signed into.</span></span> <span data-ttu-id="58fa5-239">hello toosign 用於 toohello Azure 傳統入口網站 toocreate 工作區的 Microsoft 帳戶不會自動具備權限 tooopen 該工作區。</span><span class="sxs-lookup"><span data-stu-id="58fa5-239">hello Microsoft Account you used toosign in toohello Azure classic portal toocreate a workspace does not automatically have permission tooopen that workspace.</span></span> <span data-ttu-id="58fa5-240">tooopen 工作區中，您必須登入 toohello 已定義為 hello hello 工作區中，擁有者的 Microsoft 帳戶或您需要 tooreceive 從 hello 擁有者 toojoin hello 工作區的邀請。</span><span class="sxs-lookup"><span data-stu-id="58fa5-240">tooopen a workspace, you must be signed in toohello Microsoft Account that was defined as hello owner of hello workspace, or you need tooreceive an invitation from hello owner toojoin hello workspace.</span></span>
> 
> 

