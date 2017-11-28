---
title: "aaaManage Machine Learning 工作區 |Microsoft 文件"
description: "管理存取 tooAzure 機器學習服務工作區，並將部署和管理 ML API web 服務"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: daf3d413-7a77-4beb-9a7a-6b4bdf717719
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: garye
ms.openlocfilehash: 7bd378d82aa46f4340ca974c7dc5a612c089cdca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-machine-learning-workspace"></a><span data-ttu-id="75450-103">管理 Azure Machine Learning 工作區</span><span class="sxs-lookup"><span data-stu-id="75450-103">Manage an Azure Machine Learning workspace</span></span>

> [!NOTE]
> <span data-ttu-id="75450-104">如需管理 hello 機器學習 Web 服務入口網站中的 Web 服務的資訊，請參閱[管理 Web 服務使用 hello Azure 機器學習 Web 服務網站](machine-learning-manage-new-webservice.md)。</span><span class="sxs-lookup"><span data-stu-id="75450-104">For information on managing Web services in hello Machine Learning Web Services portal, see [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span>
> 
> 

<span data-ttu-id="75450-105">您可以管理任一 hello Azure 入口網站中的機器學習服務工作區，或 hello Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="75450-105">You can manage Machine Learning workspaces in either hello Azure portal or hello Azure classic portal.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="use-hello-azure-portal"></a><span data-ttu-id="75450-106">使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="75450-106">Use hello Azure portal</span></span>

<span data-ttu-id="75450-107">toomanage hello Azure 入口網站中的工作區：</span><span class="sxs-lookup"><span data-stu-id="75450-107">toomanage a workspace in hello Azure portal:</span></span>

1. <span data-ttu-id="75450-108">登入 toohello [Azure 入口網站](https://portal.azure.com/)使用的 Azure 訂用帳戶系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="75450-108">Sign in toohello [Azure portal](https://portal.azure.com/) using an Azure subscription administrator account.</span></span>
2. <span data-ttu-id="75450-109">在 hello 頁面頂端的 hello hello 搜尋方塊中輸入 「 機器學習服務工作區 」，然後選取**機器學習工作區**。</span><span class="sxs-lookup"><span data-stu-id="75450-109">In hello search box at hello top of hello page, enter "machine learning workspaces" and then select **Machine Learning Workspaces**.</span></span>
3. <span data-ttu-id="75450-110">按一下您想要 toomanage hello 工作區。</span><span class="sxs-lookup"><span data-stu-id="75450-110">Click hello workspace you want toomanage.</span></span>

<span data-ttu-id="75450-111">此外 toohello 標準資源管理資訊和可用的選項，您可以：</span><span class="sxs-lookup"><span data-stu-id="75450-111">In addition toohello standard resource management information and options available, you can:</span></span>

- <span data-ttu-id="75450-112">檢視**屬性**-此頁面會顯示 hello 工作區和資源資訊，而且您可以變更訂閱 hello 與此工作區會連接到資源群組。</span><span class="sxs-lookup"><span data-stu-id="75450-112">View **Properties** - This page displays hello workspace and resource information, and you can change hello subscription and resource group that this workspace is connected with.</span></span>
- <span data-ttu-id="75450-113">**重新同步處理儲存體金鑰**-hello 工作區會維護金鑰 toohello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="75450-113">**Resync Storage Keys** - hello workspace maintains keys toohello storage account.</span></span> <span data-ttu-id="75450-114">如果 hello 儲存體帳戶變更索引鍵，則您可以按一下**重新同步處理金鑰**toosynchronize hello hello 工作區金鑰。</span><span class="sxs-lookup"><span data-stu-id="75450-114">If hello storage account changes keys, then you can click **Resync keys** toosynchronize hello keys with hello workspace.</span></span>

<span data-ttu-id="75450-115">此工作區中，與相關聯的 toomanage hello web 服務使用 hello 機器學習 Web 服務入口網站。</span><span class="sxs-lookup"><span data-stu-id="75450-115">toomanage hello web services associated with this workspace, use hello Machine Learning Web Services portal.</span></span> <span data-ttu-id="75450-116">請參閱[管理 Web 服務使用 hello Azure 機器學習 Web 服務網站](machine-learning-manage-new-webservice.md)如需完整資訊。</span><span class="sxs-lookup"><span data-stu-id="75450-116">See [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md) for complete information.</span></span>

> [!NOTE]
> <span data-ttu-id="75450-117">toodeploy 或管理您的參與者必須被指派新的 web 服務或部署 hello 訂用帳戶 toowhich hello web 服務上的系統管理員角色。</span><span class="sxs-lookup"><span data-stu-id="75450-117">toodeploy or manage New web services you must be assigned a contributor or administrator role on hello subscription toowhich hello web service is deployed.</span></span> <span data-ttu-id="75450-118">您可以邀請其他使用者 tooa 機器學習服務工作區，您必須指派它們 tooa 參與者或系統管理員角色，hello 訂用帳戶才能部署或管理 web 服務。</span><span class="sxs-lookup"><span data-stu-id="75450-118">If you invite another user tooa machine learning workspace, you must assign them tooa contributor or administrator role on hello subscription before they can deploy or manage web services.</span></span> 
> 
><span data-ttu-id="75450-119">如需設定存取權限的詳細資訊，請參閱[hello Azure 入口網站-公開預覽中的使用者及群組的檢視存取工作分派](../active-directory/role-based-access-control-manage-assignments.md)。</span><span class="sxs-lookup"><span data-stu-id="75450-119">For more information on setting access permissions, see [View access assignments for users and groups in hello Azure portal - Public preview](../active-directory/role-based-access-control-manage-assignments.md).</span></span>

## <a name="use-hello-azure-classic-portal"></a><span data-ttu-id="75450-120">使用 hello Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="75450-120">Use hello Azure classic portal</span></span>

<span data-ttu-id="75450-121">您可以使用 hello Azure 傳統入口網站，管理您的機器學習服務工作區，以：</span><span class="sxs-lookup"><span data-stu-id="75450-121">Using hello Azure classic portal, you can manage your Machine Learning workspaces to:</span></span>

* <span data-ttu-id="75450-122">監視 [hello] 工作區中的使用方式</span><span class="sxs-lookup"><span data-stu-id="75450-122">Monitor how hello workspace is being used</span></span>
* <span data-ttu-id="75450-123">設定 [hello] 工作區 tooallow 或拒絕存取</span><span class="sxs-lookup"><span data-stu-id="75450-123">Configure hello workspace tooallow or deny access</span></span>
* <span data-ttu-id="75450-124">管理在 hello 工作區中建立的 Web 服務</span><span class="sxs-lookup"><span data-stu-id="75450-124">Manage Web services created in hello workspace</span></span>
* <span data-ttu-id="75450-125">刪除 hello 工作區</span><span class="sxs-lookup"><span data-stu-id="75450-125">Delete hello workspace</span></span>

<span data-ttu-id="75450-126">此外，hello 儀表板索引標籤會提供您工作區的使用方式的概觀，以及您的工作區資訊的快速概覽。</span><span class="sxs-lookup"><span data-stu-id="75450-126">In addition, hello dashboard tab provides an overview of your workspace usage and a quick glance of your workspace information.</span></span>  

> [!TIP]
> <span data-ttu-id="75450-127">在 hello，Azure Machine Learning Studio 中**WEB 服務**索引標籤上，您可以加入、 更新或刪除的機器學習 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="75450-127">In Azure Machine Learning Studio, on hello **WEB SERVICES** tab, you can add, update, or delete a Machine Learning Web service.</span></span>
> 
> 

<span data-ttu-id="75450-128">toomanage hello Azure 傳統入口網站中的工作區：</span><span class="sxs-lookup"><span data-stu-id="75450-128">toomanage a workspace in hello Azure classic portal:</span></span>

1. <span data-ttu-id="75450-129">登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com/)使用 Microsoft Azure 帳戶-請使用 hello 與 hello Azure 訂用帳戶相關聯的帳戶。</span><span class="sxs-lookup"><span data-stu-id="75450-129">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) using your Microsoft Azure account - use hello account that's associated with hello Azure subscription.</span></span>
2. <span data-ttu-id="75450-130">在 hello Microsoft Azure 服務面板中，按一下  **MACHINE LEARNING**。</span><span class="sxs-lookup"><span data-stu-id="75450-130">In hello Microsoft Azure services panel, click **MACHINE LEARNING**.</span></span>
3. <span data-ttu-id="75450-131">按一下您想要 toomanage hello 工作區。</span><span class="sxs-lookup"><span data-stu-id="75450-131">Click hello workspace you want toomanage.</span></span>

<span data-ttu-id="75450-132">hello 工作區頁面有三個索引標籤：</span><span class="sxs-lookup"><span data-stu-id="75450-132">hello workspace page has three tabs:</span></span>

* <span data-ttu-id="75450-133">**儀表板**-可讓您 tooview 工作區的使用方式和資訊</span><span class="sxs-lookup"><span data-stu-id="75450-133">**DASHBOARD** - Allows you tooview workspace usage and information</span></span>
* <span data-ttu-id="75450-134">**設定**-可讓您工作區中存取 toohello toomanage</span><span class="sxs-lookup"><span data-stu-id="75450-134">**CONFIGURE** - Allows you toomanage access toohello workspace</span></span>
* <span data-ttu-id="75450-135">**WEB 服務**-可讓您 toomanage 從此工作區已發佈的 Web 服務</span><span class="sxs-lookup"><span data-stu-id="75450-135">**WEB SERVICES** - Allows you toomanage Web services that have been published from this workspace</span></span>

### <a name="toomonitor-how-hello-workspace-is-being-used"></a><span data-ttu-id="75450-136">toomonitor hello 工作區中的使用方式</span><span class="sxs-lookup"><span data-stu-id="75450-136">toomonitor how hello workspace is being used</span></span>
<span data-ttu-id="75450-137">按一下 hello**儀表板** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="75450-137">Click hello **DASHBOARD** tab.</span></span>

<span data-ttu-id="75450-138">從 hello 儀表板，您可以檢視工作區的整體使用狀況，並取得工作區資訊的快速概覽。</span><span class="sxs-lookup"><span data-stu-id="75450-138">From hello dashboard, you can view overall usage of your workspace and get a quick glance of workspace information.</span></span>

* <span data-ttu-id="75450-139">hello**計算**圖表可顯示 hello hello 工作區正在使用的計算資源。</span><span class="sxs-lookup"><span data-stu-id="75450-139">hello **COMPUTE** chart shows hello compute resources being used by hello workspace.</span></span> <span data-ttu-id="75450-140">您可以變更 hello 檢視 toodisplay 相對或絕對值，而且您可以變更 hello hello 圖表中顯示的時間範圍內。</span><span class="sxs-lookup"><span data-stu-id="75450-140">You can change hello view toodisplay relative or absolute values, and you can change hello timeframe displayed in hello chart.</span></span>
* <span data-ttu-id="75450-141">**使用量概觀**顯示 hello 工作區正在使用的 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="75450-141">**Usage overview** displays Azure storage being used by hello workspace.</span></span>
* <span data-ttu-id="75450-142">**快速概覽** 提供工作區資訊和實用連結的摘要。</span><span class="sxs-lookup"><span data-stu-id="75450-142">**Quick glance** provides a summary of workspace information and useful links.</span></span>

> [!NOTE]
> <span data-ttu-id="75450-143">hello**登入 tooML Studio**連結會開啟 Machine Learning Studio 使用 hello 目前登入的 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="75450-143">hello **Sign-in tooML Studio** link opens Machine Learning Studio using hello Microsoft Account you are currently signed into.</span></span> <span data-ttu-id="75450-144">hello toosign 用於 toohello Azure 傳統入口網站 toocreate 工作區的 Microsoft 帳戶不會自動具備權限 tooopen 該工作區。</span><span class="sxs-lookup"><span data-stu-id="75450-144">hello Microsoft Account you used toosign in toohello Azure classic portal toocreate a workspace does not automatically have permission tooopen that workspace.</span></span> <span data-ttu-id="75450-145">tooopen 工作區中，您必須登入 toohello 已定義為 hello hello 工作區中，擁有者的 Microsoft 帳戶或您需要 tooreceive 從 hello 擁有者 toojoin hello 工作區的邀請。</span><span class="sxs-lookup"><span data-stu-id="75450-145">tooopen a workspace, you must be signed in toohello Microsoft Account that was defined as hello owner of hello workspace, or you need tooreceive an invitation from hello owner toojoin hello workspace.</span></span>
> 
> 

### <a name="toogrant-or-suspend-access-for-users"></a><span data-ttu-id="75450-146">toogrant 或暫止使用者的存取權</span><span class="sxs-lookup"><span data-stu-id="75450-146">toogrant or suspend access for users</span></span>
<span data-ttu-id="75450-147">按一下 hello**設定** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="75450-147">Click hello **CONFIGURE** tab.</span></span>

<span data-ttu-id="75450-148">您可以從 hello 設定 索引標籤：</span><span class="sxs-lookup"><span data-stu-id="75450-148">From hello configuration tab you can:</span></span>

* <span data-ttu-id="75450-149">暫停存取 toohello Machine Learning 工作區，按一下 [拒絕]。</span><span class="sxs-lookup"><span data-stu-id="75450-149">Suspend access toohello Machine Learning workspace by clicking DENY.</span></span> <span data-ttu-id="75450-150">使用者將不再能夠 tooopen Machine Learning Studio 中的 hello 工作區。</span><span class="sxs-lookup"><span data-stu-id="75450-150">Users will no longer be able tooopen hello workspace in Machine Learning Studio.</span></span> <span data-ttu-id="75450-151">toorestore 存取，請按一下 [允許]。</span><span class="sxs-lookup"><span data-stu-id="75450-151">toorestore access, click ALLOW.</span></span>

<span data-ttu-id="75450-152">toomanage 其他帳戶擁有存取 toohello 工作區，在機器學習 Studio 中，按一下**登入 tooML Studio**在 hello**儀表板** 索引標籤 (請參閱 hello 前面附註有關**Sign-in tooML Studio**)。</span><span class="sxs-lookup"><span data-stu-id="75450-152">toomanage additional accounts who have access toohello workspace in Machine Learning Studio, click **Sign-in tooML Studio** in hello **DASHBOARD** tab (see hello preceeding note regarding **Sign-in tooML Studio**).</span></span> <span data-ttu-id="75450-153">這會開啟 Machine Learning Studio hello 工作區。</span><span class="sxs-lookup"><span data-stu-id="75450-153">This opens hello workspace in Machine Learning Studio.</span></span> <span data-ttu-id="75450-154">從這裡按一下 hello**設定** 索引標籤，然後**使用者**。</span><span class="sxs-lookup"><span data-stu-id="75450-154">From here, click hello **SETTINGS** tab and then **USERS**.</span></span> <span data-ttu-id="75450-155">您可以按一下**更邀請使用者**toogive 使用者存取 toohello 工作區中，或選取的使用者，然後按一下**移除**。</span><span class="sxs-lookup"><span data-stu-id="75450-155">You can click **INVITE MORE USERS** toogive users access toohello workspace, or select a user and click **REMOVE**.</span></span>

### <a name="toomanage-web-services-in-this-workspace"></a><span data-ttu-id="75450-156">此工作區中的 toomanage web 服務</span><span class="sxs-lookup"><span data-stu-id="75450-156">toomanage web services in this workspace</span></span>
<span data-ttu-id="75450-157">按一下 hello **WEB 服務** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="75450-157">Click hello **WEB SERVICES** tab.</span></span>

<span data-ttu-id="75450-158">這會顯示從此工作區發佈的 Web 服務的清單。</span><span class="sxs-lookup"><span data-stu-id="75450-158">This displays a list of web services published from this workspace.</span></span>
<span data-ttu-id="75450-159">toomanage web 服務，按一下 hello 清單 tooopen hello Web 服務頁面中的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="75450-159">toomanage a web service, click hello name in hello list tooopen hello Web service page.</span></span>

<span data-ttu-id="75450-160">Web 服務可能會有一個或多個定義的端點。</span><span class="sxs-lookup"><span data-stu-id="75450-160">A Web service may have one or more endpoints defined.</span></span>

* <span data-ttu-id="75450-161">您可以新增 toohello"Default"端點中定義多個端點。</span><span class="sxs-lookup"><span data-stu-id="75450-161">You can define more endpoints in addition toohello "Default" endpoint.</span></span> <span data-ttu-id="75450-162">tooadd hello 端點，請按一下**管理端點**底部 hello hello 儀表板 tooopen hello Azure 機器學習 Web 服務入口網站。</span><span class="sxs-lookup"><span data-stu-id="75450-162">tooadd hello endpoint, click **Manage Endpoints** at hello bottom of hello dashboard tooopen hello Azure Machine Learning Web Services portal.</span></span>
* <span data-ttu-id="75450-163">toodelete 端點 （您無法刪除 hello"Default"端點），按一下 [hello] 核取方塊，在 hello 開頭 hello 端點的資料列，然後按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="75450-163">toodelete an endpoint (you cannot delete hello "Default" endpoint), click hello check box at hello beginning of hello endpoint row, and click **DELETE**.</span></span> <span data-ttu-id="75450-164">這會移除 hello 端點從 hello Web 服務。</span><span class="sxs-lookup"><span data-stu-id="75450-164">This removes hello endpoint from hello Web service.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="75450-165">如果刪除 hello 端點時，應用程式正在使用 hello web 服務端點，hello 應用程式會在下一次嘗試 tooaccess hello 服務時收到錯誤 hello。</span><span class="sxs-lookup"><span data-stu-id="75450-165">If an application is using hello web service endpoint when hello endpoint is deleted, hello application will receive an error hello next time it tries tooaccess hello service.</span></span>
  > 
  > 

<span data-ttu-id="75450-166">按一下 Web 服務端點 tooopen hello 名稱它。</span><span class="sxs-lookup"><span data-stu-id="75450-166">Click hello name of a Web service endpoint tooopen it.</span></span> 

<span data-ttu-id="75450-167">從 hello 儀表板，您可以檢視您的 Web 服務的整體使用狀況經過一段時間。</span><span class="sxs-lookup"><span data-stu-id="75450-167">From hello dashboard, you can view overall usage of your Web service over a period of time.</span></span> <span data-ttu-id="75450-168">您可以選取 hello 期間 tooview 從 hello 週期 下拉式功能表中的 hello 使用量圖表的 hello 右上方。</span><span class="sxs-lookup"><span data-stu-id="75450-168">You can select hello period tooview from hello Period dropdown menu in hello upper right of hello usage charts.</span></span> <span data-ttu-id="75450-169">hello 儀表板會顯示下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="75450-169">hello dashboard shows hello following information:</span></span>

* <span data-ttu-id="75450-170">**要求一段時間**會顯示選取的時間週期的 hello 步驟圖形 hello 要求數目。</span><span class="sxs-lookup"><span data-stu-id="75450-170">**Requests Over Time** displays a step graph of hello number of requests over hello selected time period.</span></span> <span data-ttu-id="75450-171">它可以協助識別您所遇到的使用量尖峰。</span><span class="sxs-lookup"><span data-stu-id="75450-171">It can help identify if you are experiencing spikes in usage.</span></span>
* <span data-ttu-id="75450-172">**要求-回應要求**顯示 hello 的 hello 服務已收到 hello 選的時段和多少個失敗的要求-回應呼叫次數總計。</span><span class="sxs-lookup"><span data-stu-id="75450-172">**Request-Response Requests** displays hello total number of Request-Response calls hello service has received over hello selected time period and how many of them failed.</span></span>
* <span data-ttu-id="75450-173">**平均要求回應計算時間**顯示 hello 時間的平均值的所需 tooexecute hello 收到要求。</span><span class="sxs-lookup"><span data-stu-id="75450-173">**Average Request-Response Compute Time** displays an average of hello time needed tooexecute hello received requests.</span></span>
* <span data-ttu-id="75450-174">**批次要求**顯示 hello 總數批次要求 hello 服務已收到透過選取的時間週期的 hello，且其中多少失敗。</span><span class="sxs-lookup"><span data-stu-id="75450-174">**Batch Requests** displays hello total number of Batch Requests hello service has received over hello selected time period and how many of them failed.</span></span>
* <span data-ttu-id="75450-175">**平均工作延遲**顯示 hello 時間的平均值的所需 tooexecute hello 收到要求。</span><span class="sxs-lookup"><span data-stu-id="75450-175">**Average Job Latency** displays an average of hello time needed tooexecute hello received requests.</span></span>
* <span data-ttu-id="75450-176">**錯誤**呼叫 toohello web 服務上顯示 hello 彙總數目所發生的錯誤。</span><span class="sxs-lookup"><span data-stu-id="75450-176">**Errors** displays hello aggregate number of errors that have occurred on calls toohello web service.</span></span>
* <span data-ttu-id="75450-177">**服務成本**顯示 hello 費用 hello 與 hello 服務相關聯的計費方案。</span><span class="sxs-lookup"><span data-stu-id="75450-177">**Services Costs** displays hello charges for hello billing plan associated with hello service.</span></span>

<span data-ttu-id="75450-178">從 hello 設定 頁面，您可以更新下列屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="75450-178">From hello Configure page, you can update hello following properties:</span></span>

* <span data-ttu-id="75450-179">**描述**可讓您 tooenter hello Web 服務的描述。</span><span class="sxs-lookup"><span data-stu-id="75450-179">**Description** allows you tooenter a description for hello Web service.</span></span> <span data-ttu-id="75450-180">[描述] 必要欄位。</span><span class="sxs-lookup"><span data-stu-id="75450-180">Description is a required field.</span></span>
* <span data-ttu-id="75450-181">**記錄**可讓您登入 hello 端點 tooenable 或停用錯誤。</span><span class="sxs-lookup"><span data-stu-id="75450-181">**Logging** allows you tooenable or disable error logging on hello endpoint.</span></span> <span data-ttu-id="75450-182">如需有關記錄的詳細資訊，請參閱[為 Machine Learning Web 服務啟用記錄](machine-learning-web-services-logging.md)。</span><span class="sxs-lookup"><span data-stu-id="75450-182">For more information on Logging, see Enable [logging for Machine Learning web services](machine-learning-web-services-logging.md).</span></span>
* <span data-ttu-id="75450-183">**啟用範例資料**tooprovide 範例資料，您可以使用 tootest hello 要求-回應服務可讓您。</span><span class="sxs-lookup"><span data-stu-id="75450-183">**Enable Sample data** allows you tooprovide sample data that you can use tootest hello Request-Response service.</span></span> <span data-ttu-id="75450-184">如果您在 Machine Learning Studio 中建立 hello web 服務，hello 範例資料取自 hello 資料您使用的 tootrain 您的模型。</span><span class="sxs-lookup"><span data-stu-id="75450-184">If you created hello web service in Machine Learning Studio, hello sample data is taken from hello data your used tootrain your model.</span></span> <span data-ttu-id="75450-185">如果您以程式設計方式建立 hello 服務，hello 資料取自 hello 範例資料，您提供為 hello JSON 封裝的一部分。</span><span class="sxs-lookup"><span data-stu-id="75450-185">If you created hello service programmatically, hello data is taken from hello example data you provided as part of hello JSON package.</span></span>

