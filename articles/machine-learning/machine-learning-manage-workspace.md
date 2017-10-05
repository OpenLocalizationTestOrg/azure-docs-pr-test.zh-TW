---
title: "管理 Machine Learning 工作區 | Microsoft Docs"
description: "管理 Azure 機器學習工作區的存取權，並部署和管理 ML API Web 服務"
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
ms.openlocfilehash: 94800f51baf83311c33490cada5f991ff2101da9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-an-azure-machine-learning-workspace"></a><span data-ttu-id="4aca5-103">管理 Azure Machine Learning 工作區</span><span class="sxs-lookup"><span data-stu-id="4aca5-103">Manage an Azure Machine Learning workspace</span></span>

> [!NOTE]
> <span data-ttu-id="4aca5-104">如需在 Machine Learning Web 服務入口網站中管理 Web 服務的相關資訊，請參閱[使用 Azure Machine Learning Web 服務入口網站管理 Web 服務](machine-learning-manage-new-webservice.md)。</span><span class="sxs-lookup"><span data-stu-id="4aca5-104">For information on managing Web services in the Machine Learning Web Services portal, see [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span>
> 
> 

<span data-ttu-id="4aca5-105">您可以在 Azure 入口網站或 Azure 傳統入口網站中管理 Machine Learning 工作區。</span><span class="sxs-lookup"><span data-stu-id="4aca5-105">You can manage Machine Learning workspaces in either the Azure portal or the Azure classic portal.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="use-the-azure-portal"></a><span data-ttu-id="4aca5-106">使用 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="4aca5-106">Use the Azure portal</span></span>

<span data-ttu-id="4aca5-107">若要在 Azure 入口網站中管理工作區︰</span><span class="sxs-lookup"><span data-stu-id="4aca5-107">To manage a workspace in the Azure portal:</span></span>

1. <span data-ttu-id="4aca5-108">使用 Azure 訂用帳戶系統管理員帳戶登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="4aca5-108">Sign in to the [Azure portal](https://portal.azure.com/) using an Azure subscription administrator account.</span></span>
2. <span data-ttu-id="4aca5-109">在頁面頂端的搜尋方塊中輸入「Machine Learning 工作區」，然後選取 [Machine Learning 工作區]。</span><span class="sxs-lookup"><span data-stu-id="4aca5-109">In the search box at the top of the page, enter "machine learning workspaces" and then select **Machine Learning Workspaces**.</span></span>
3. <span data-ttu-id="4aca5-110">按一下您想要管理的工作區。</span><span class="sxs-lookup"><span data-stu-id="4aca5-110">Click the workspace you want to manage.</span></span>

<span data-ttu-id="4aca5-111">除了標準的資源管理資訊和可用的選項，您還可以︰</span><span class="sxs-lookup"><span data-stu-id="4aca5-111">In addition to the standard resource management information and options available, you can:</span></span>

- <span data-ttu-id="4aca5-112">檢視**屬性** - 此頁面會顯示工作區和資源的資訊，而且您可以變更這個工作區所連線的訂用帳戶和資源群組。</span><span class="sxs-lookup"><span data-stu-id="4aca5-112">View **Properties** - This page displays the workspace and resource information, and you can change the subscription and resource group that this workspace is connected with.</span></span>
- <span data-ttu-id="4aca5-113">**重新同步儲存體金鑰** - 工作區會保有儲存體帳戶的金鑰。</span><span class="sxs-lookup"><span data-stu-id="4aca5-113">**Resync Storage Keys** - The workspace maintains keys to the storage account.</span></span> <span data-ttu-id="4aca5-114">如果儲存體帳戶變更了金鑰，則您可以按一下 [重新同步金鑰] 來與工作區同步處理金鑰。</span><span class="sxs-lookup"><span data-stu-id="4aca5-114">If the storage account changes keys, then you can click **Resync keys** to synchronize the keys with the workspace.</span></span>

<span data-ttu-id="4aca5-115">若要管理與此工作區相關聯的 Web 服務，請使用 Machine Learning Web 服務入口網站。</span><span class="sxs-lookup"><span data-stu-id="4aca5-115">To manage the web services associated with this workspace, use the Machine Learning Web Services portal.</span></span> <span data-ttu-id="4aca5-116">如需詳細資訊，請參閱[使用 Azure Machine Learning Web 服務入口網站管理 Web 服務](machine-learning-manage-new-webservice.md)。</span><span class="sxs-lookup"><span data-stu-id="4aca5-116">See [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md) for complete information.</span></span>

> [!NOTE]
> <span data-ttu-id="4aca5-117">若要部署或管理新的 Web 服務，您必須獲得下列角色的指派：要部署 Web 服務之訂用帳戶上的參與者或系統管理員角色。</span><span class="sxs-lookup"><span data-stu-id="4aca5-117">To deploy or manage New web services you must be assigned a contributor or administrator role on the subscription to which the web service is deployed.</span></span> <span data-ttu-id="4aca5-118">如果您邀請另一位使用者到 Machine Learning 工作區，就必須為他們指派訂用帳戶上的參與者或系統管理員角色，然後他們才能部署或管理 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="4aca5-118">If you invite another user to a machine learning workspace, you must assign them to a contributor or administrator role on the subscription before they can deploy or manage web services.</span></span> 
> 
><span data-ttu-id="4aca5-119">如需有關設定存取權限的詳細資訊，請參閱[在 Azure 入口網站 (公開預覽) 中檢視使用者和群組的存取權指派](../active-directory/role-based-access-control-manage-assignments.md)。</span><span class="sxs-lookup"><span data-stu-id="4aca5-119">For more information on setting access permissions, see [View access assignments for users and groups in the Azure portal - Public preview](../active-directory/role-based-access-control-manage-assignments.md).</span></span>

## <a name="use-the-azure-classic-portal"></a><span data-ttu-id="4aca5-120">使用 Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="4aca5-120">Use the Azure classic portal</span></span>

<span data-ttu-id="4aca5-121">您可以使用 Azure 傳統入口網站來管理您的機器學習服務工作區，以便：</span><span class="sxs-lookup"><span data-stu-id="4aca5-121">Using the Azure classic portal, you can manage your Machine Learning workspaces to:</span></span>

* <span data-ttu-id="4aca5-122">監視工作區的使用方式</span><span class="sxs-lookup"><span data-stu-id="4aca5-122">Monitor how the workspace is being used</span></span>
* <span data-ttu-id="4aca5-123">設定工作區以允許或拒絕存取</span><span class="sxs-lookup"><span data-stu-id="4aca5-123">Configure the workspace to allow or deny access</span></span>
* <span data-ttu-id="4aca5-124">管理工作區中建立的 Web 服務</span><span class="sxs-lookup"><span data-stu-id="4aca5-124">Manage Web services created in the workspace</span></span>
* <span data-ttu-id="4aca5-125">刪除工作區</span><span class="sxs-lookup"><span data-stu-id="4aca5-125">Delete the workspace</span></span>

<span data-ttu-id="4aca5-126">此外，儀表板索引標籤會提供工作區使用方式的概觀和工作區資訊的快速概覽。</span><span class="sxs-lookup"><span data-stu-id="4aca5-126">In addition, the dashboard tab provides an overview of your workspace usage and a quick glance of your workspace information.</span></span>  

> [!TIP]
> <span data-ttu-id="4aca5-127">在 Azure Machine Learning Studio 中，您可以在 [Web 服務] 索引標籤上新增、更新或刪除 Machine Learning Web 服務。</span><span class="sxs-lookup"><span data-stu-id="4aca5-127">In Azure Machine Learning Studio, on the **WEB SERVICES** tab, you can add, update, or delete a Machine Learning Web service.</span></span>
> 
> 

<span data-ttu-id="4aca5-128">若要在 Azure 傳統入口網站中管理工作區︰</span><span class="sxs-lookup"><span data-stu-id="4aca5-128">To manage a workspace in the Azure classic portal:</span></span>

1. <span data-ttu-id="4aca5-129">使用您的 Microsoft Azure 帳戶登入 [Azure 傳統入口網站](https://manage.windowsazure.com/) - 使用與 Azure 訂用帳戶相關聯的帳戶。</span><span class="sxs-lookup"><span data-stu-id="4aca5-129">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) using your Microsoft Azure account - use the account that's associated with the Azure subscription.</span></span>
2. <span data-ttu-id="4aca5-130">在 Microsoft Azure 服務面板中，按一下 [機器學習] 。</span><span class="sxs-lookup"><span data-stu-id="4aca5-130">In the Microsoft Azure services panel, click **MACHINE LEARNING**.</span></span>
3. <span data-ttu-id="4aca5-131">按一下您想要管理的工作區。</span><span class="sxs-lookup"><span data-stu-id="4aca5-131">Click the workspace you want to manage.</span></span>

<span data-ttu-id="4aca5-132">工作區頁面有三個索引標籤：</span><span class="sxs-lookup"><span data-stu-id="4aca5-132">The workspace page has three tabs:</span></span>

* <span data-ttu-id="4aca5-133">**儀表板** - 可讓您檢視工作區使用方式和資訊</span><span class="sxs-lookup"><span data-stu-id="4aca5-133">**DASHBOARD** - Allows you to view workspace usage and information</span></span>
* <span data-ttu-id="4aca5-134">**設定** - 可讓您管理對工作區的存取</span><span class="sxs-lookup"><span data-stu-id="4aca5-134">**CONFIGURE** - Allows you to manage access to the workspace</span></span>
* <span data-ttu-id="4aca5-135">**Web 服務** - 可讓您管理從此工作區發佈的 Web 服務</span><span class="sxs-lookup"><span data-stu-id="4aca5-135">**WEB SERVICES** - Allows you to manage Web services that have been published from this workspace</span></span>

### <a name="to-monitor-how-the-workspace-is-being-used"></a><span data-ttu-id="4aca5-136">監視工作區的使用方式</span><span class="sxs-lookup"><span data-stu-id="4aca5-136">To monitor how the workspace is being used</span></span>
<span data-ttu-id="4aca5-137">按一下 [ **儀表板** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="4aca5-137">Click the **DASHBOARD** tab.</span></span>

<span data-ttu-id="4aca5-138">從儀表板，您可以檢視工作區的整體使用量，並取得工作區資訊的快速概覽。</span><span class="sxs-lookup"><span data-stu-id="4aca5-138">From the dashboard, you can view overall usage of your workspace and get a quick glance of workspace information.</span></span>

* <span data-ttu-id="4aca5-139">**計算** 圖表會顯示工作區正在使用的計算資源。</span><span class="sxs-lookup"><span data-stu-id="4aca5-139">The **COMPUTE** chart shows the compute resources being used by the workspace.</span></span> <span data-ttu-id="4aca5-140">您可以變更檢視來顯示相對或絕對值，並且可以變更圖表中顯示的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="4aca5-140">You can change the view to display relative or absolute values, and you can change the timeframe displayed in the chart.</span></span>
* <span data-ttu-id="4aca5-141">**使用量概觀** 顯示工作區正在使用的 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="4aca5-141">**Usage overview** displays Azure storage being used by the workspace.</span></span>
* <span data-ttu-id="4aca5-142">**快速概覽** 提供工作區資訊和實用連結的摘要。</span><span class="sxs-lookup"><span data-stu-id="4aca5-142">**Quick glance** provides a summary of workspace information and useful links.</span></span>

> [!NOTE]
> <span data-ttu-id="4aca5-143">[ **登入 ML Studio** ] 連結會使用目前登入的 Microsoft 帳戶來開啟 Machine Learning Studio。</span><span class="sxs-lookup"><span data-stu-id="4aca5-143">The **Sign-in to ML Studio** link opens Machine Learning Studio using the Microsoft Account you are currently signed into.</span></span> <span data-ttu-id="4aca5-144">您用來登入 Azure 傳統入口網站以建立工作區的 Microsoft 帳戶，不會自動具備開啟該工作區的權限。</span><span class="sxs-lookup"><span data-stu-id="4aca5-144">The Microsoft Account you used to sign in to the Azure classic portal to create a workspace does not automatically have permission to open that workspace.</span></span> <span data-ttu-id="4aca5-145">若要開啟工作區，您必須使用定義為工作區擁有者的 Microsoft 帳戶登入，或者您需要收到來自擁有者的邀請，才能加入工作區。</span><span class="sxs-lookup"><span data-stu-id="4aca5-145">To open a workspace, you must be signed in to the Microsoft Account that was defined as the owner of the workspace, or you need to receive an invitation from the owner to join the workspace.</span></span>
> 
> 

### <a name="to-grant-or-suspend-access-for-users"></a><span data-ttu-id="4aca5-146">授與或暫停使用者的存取權</span><span class="sxs-lookup"><span data-stu-id="4aca5-146">To grant or suspend access for users</span></span>
<span data-ttu-id="4aca5-147">按一下 [設定]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="4aca5-147">Click the **CONFIGURE** tab.</span></span>

<span data-ttu-id="4aca5-148">您可以從設定索引標籤：</span><span class="sxs-lookup"><span data-stu-id="4aca5-148">From the configuration tab you can:</span></span>

* <span data-ttu-id="4aca5-149">按一下 [拒絕] 來擱置對機器學習服務工作區的存取。</span><span class="sxs-lookup"><span data-stu-id="4aca5-149">Suspend access to the Machine Learning workspace by clicking DENY.</span></span> <span data-ttu-id="4aca5-150">使用者將不再能在 Machine Learning Studio 中開啟工作區。</span><span class="sxs-lookup"><span data-stu-id="4aca5-150">Users will no longer be able to open the workspace in Machine Learning Studio.</span></span> <span data-ttu-id="4aca5-151">若要還原存取，請按一下 [允許]。</span><span class="sxs-lookup"><span data-stu-id="4aca5-151">To restore access, click ALLOW.</span></span>

<span data-ttu-id="4aca5-152">若要管理可以存取 Machine Learning Studio 中工作區的其他帳戶，請按一下 [儀表板] 索引標籤中的 [登入 ML Studio]\(請參閱上述有關**登入 ML Studio** 的附註)。</span><span class="sxs-lookup"><span data-stu-id="4aca5-152">To manage additional accounts who have access to the workspace in Machine Learning Studio, click **Sign-in to ML Studio** in the **DASHBOARD** tab (see the preceeding note regarding **Sign-in to ML Studio**).</span></span> <span data-ttu-id="4aca5-153">這會在 Machine Learning Studio 中開啟工作區。</span><span class="sxs-lookup"><span data-stu-id="4aca5-153">This opens the workspace in Machine Learning Studio.</span></span> <span data-ttu-id="4aca5-154">從這裡按一下 [設定] 索引標籤，然後按一下 [使用者]。</span><span class="sxs-lookup"><span data-stu-id="4aca5-154">From here, click the **SETTINGS** tab and then **USERS**.</span></span> <span data-ttu-id="4aca5-155">您可以按一下 [邀請使用者]，讓使用者存取工作區，或選取使用者，並按一下 [移除]。</span><span class="sxs-lookup"><span data-stu-id="4aca5-155">You can click **INVITE MORE USERS** to give users access to the workspace, or select a user and click **REMOVE**.</span></span>

### <a name="to-manage-web-services-in-this-workspace"></a><span data-ttu-id="4aca5-156">管理此工作區中的 Web 服務</span><span class="sxs-lookup"><span data-stu-id="4aca5-156">To manage web services in this workspace</span></span>
<span data-ttu-id="4aca5-157">按一下 [ **Web 服務** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="4aca5-157">Click the **WEB SERVICES** tab.</span></span>

<span data-ttu-id="4aca5-158">這會顯示從此工作區發佈的 Web 服務的清單。</span><span class="sxs-lookup"><span data-stu-id="4aca5-158">This displays a list of web services published from this workspace.</span></span>
<span data-ttu-id="4aca5-159">若要管理 Web 服務，請按一下清單中的名稱以開啟 Web 服務頁面。</span><span class="sxs-lookup"><span data-stu-id="4aca5-159">To manage a web service, click the name in the list to open the Web service page.</span></span>

<span data-ttu-id="4aca5-160">Web 服務可能會有一個或多個定義的端點。</span><span class="sxs-lookup"><span data-stu-id="4aca5-160">A Web service may have one or more endpoints defined.</span></span>

* <span data-ttu-id="4aca5-161">除了「預設」端點以外，您可以定義更多端點。</span><span class="sxs-lookup"><span data-stu-id="4aca5-161">You can define more endpoints in addition to the "Default" endpoint.</span></span> <span data-ttu-id="4aca5-162">若要新增端點，請按一下儀表板底部的 [管理端點]，開啟 Azure Machine Learning Web 服務入口網站。</span><span class="sxs-lookup"><span data-stu-id="4aca5-162">To add the endpoint, click **Manage Endpoints** at the bottom of the dashboard to open the Azure Machine Learning Web Services portal.</span></span>
* <span data-ttu-id="4aca5-163">若要刪除端點 (您無法刪除「預設」端點)，請按一下端點列開頭的核取方塊，然後按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="4aca5-163">To delete an endpoint (you cannot delete the "Default" endpoint), click the check box at the beginning of the endpoint row, and click **DELETE**.</span></span> <span data-ttu-id="4aca5-164">這會從 Web 服務移除端點。</span><span class="sxs-lookup"><span data-stu-id="4aca5-164">This removes the endpoint from the Web service.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="4aca5-165">如果刪除端點時應用程式使用 Web 服務端點，應用程式會在下一次嘗試存取服務時收到錯誤。</span><span class="sxs-lookup"><span data-stu-id="4aca5-165">If an application is using the web service endpoint when the endpoint is deleted, the application will receive an error the next time it tries to access the service.</span></span>
  > 
  > 

<span data-ttu-id="4aca5-166">按一下 Web 服務端點的名稱以開啟它。</span><span class="sxs-lookup"><span data-stu-id="4aca5-166">Click the name of a Web service endpoint to open it.</span></span> 

<span data-ttu-id="4aca5-167">您可以從儀表板中檢視您的 Web 服務經過一段時間的整體使用量。</span><span class="sxs-lookup"><span data-stu-id="4aca5-167">From the dashboard, you can view overall usage of your Web service over a period of time.</span></span> <span data-ttu-id="4aca5-168">您可以從使用量圖表右上角的 [期間] 下拉式功能表中選取要檢視的期間。</span><span class="sxs-lookup"><span data-stu-id="4aca5-168">You can select the period to view from the Period dropdown menu in the upper right of the usage charts.</span></span> <span data-ttu-id="4aca5-169">儀表板會顯示下列資訊：</span><span class="sxs-lookup"><span data-stu-id="4aca5-169">The dashboard shows the following information:</span></span>

* <span data-ttu-id="4aca5-170">**一段時間的要求數** 顯示選取的一段時間內，要求數目的步階圖形。</span><span class="sxs-lookup"><span data-stu-id="4aca5-170">**Requests Over Time** displays a step graph of the number of requests over the selected time period.</span></span> <span data-ttu-id="4aca5-171">它可以協助識別您所遇到的使用量尖峰。</span><span class="sxs-lookup"><span data-stu-id="4aca5-171">It can help identify if you are experiencing spikes in usage.</span></span>
* <span data-ttu-id="4aca5-172">**要求-回應要求數** 顯示服務在選取的一段時間內收到的要求-回應呼叫總數，以及失敗的數目。</span><span class="sxs-lookup"><span data-stu-id="4aca5-172">**Request-Response Requests** displays the total number of Request-Response calls the service has received over the selected time period and how many of them failed.</span></span>
* <span data-ttu-id="4aca5-173">**平均要求-回應計算時間** 顯示執行收到的要求所需的平均時間。</span><span class="sxs-lookup"><span data-stu-id="4aca5-173">**Average Request-Response Compute Time** displays an average of the time needed to execute the received requests.</span></span>
* <span data-ttu-id="4aca5-174">**批次要求數** 顯示服務在選取的一段時間內收到的批次要求總數，以及失敗的數目。</span><span class="sxs-lookup"><span data-stu-id="4aca5-174">**Batch Requests** displays the total number of Batch Requests the service has received over the selected time period and how many of them failed.</span></span>
* <span data-ttu-id="4aca5-175">**平均作業延遲** 顯示執行收到的要求所需的平均時間。</span><span class="sxs-lookup"><span data-stu-id="4aca5-175">**Average Job Latency** displays an average of the time needed to execute the received requests.</span></span>
* <span data-ttu-id="4aca5-176">**錯誤數**顯示呼叫 Web 服務時所發生的錯誤彙總數目。</span><span class="sxs-lookup"><span data-stu-id="4aca5-176">**Errors** displays the aggregate number of errors that have occurred on calls to the web service.</span></span>
* <span data-ttu-id="4aca5-177">**服務成本** 顯示與服務相關聯的計費方案費用。</span><span class="sxs-lookup"><span data-stu-id="4aca5-177">**Services Costs** displays the charges for the billing plan associated with the service.</span></span>

<span data-ttu-id="4aca5-178">您可以從 [設定] 頁面更新下列屬性：</span><span class="sxs-lookup"><span data-stu-id="4aca5-178">From the Configure page, you can update the following properties:</span></span>

* <span data-ttu-id="4aca5-179">[描述] 可讓您輸入 Web 服務的描述。</span><span class="sxs-lookup"><span data-stu-id="4aca5-179">**Description** allows you to enter a description for the Web service.</span></span> <span data-ttu-id="4aca5-180">[描述] 必要欄位。</span><span class="sxs-lookup"><span data-stu-id="4aca5-180">Description is a required field.</span></span>
* <span data-ttu-id="4aca5-181">[記錄] 可讓您啟用或停用端點上的錯誤記錄。</span><span class="sxs-lookup"><span data-stu-id="4aca5-181">**Logging** allows you to enable or disable error logging on the endpoint.</span></span> <span data-ttu-id="4aca5-182">如需有關記錄的詳細資訊，請參閱[為 Machine Learning Web 服務啟用記錄](machine-learning-web-services-logging.md)。</span><span class="sxs-lookup"><span data-stu-id="4aca5-182">For more information on Logging, see Enable [logging for Machine Learning web services](machine-learning-web-services-logging.md).</span></span>
* <span data-ttu-id="4aca5-183">[啟用範例資料] 可讓您提供範例資料，用來測試要求-回應服務。</span><span class="sxs-lookup"><span data-stu-id="4aca5-183">**Enable Sample data** allows you to provide sample data that you can use to test the Request-Response service.</span></span> <span data-ttu-id="4aca5-184">如果您是在 Machine Learning Studio 中建立 Web 服務，範例資料會取自您用來訓練模型的資料。</span><span class="sxs-lookup"><span data-stu-id="4aca5-184">If you created the web service in Machine Learning Studio, the sample data is taken from the data your used to train your model.</span></span> <span data-ttu-id="4aca5-185">如果您是以程式設計方式建立服務，資料會取自您提供做為 JSON 套件一部分的範例資料。</span><span class="sxs-lookup"><span data-stu-id="4aca5-185">If you created the service programmatically, the data is taken from the example data you provided as part of the JSON package.</span></span>

