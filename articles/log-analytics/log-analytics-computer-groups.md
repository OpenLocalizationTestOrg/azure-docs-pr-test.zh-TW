---
title: "aaaComputer 群組中記錄分析記錄搜尋 |Microsoft 文件"
description: "記錄分析中的電腦群組可讓您 tooscope 記錄搜尋 tooa 特定一組電腦。  本文說明 hello toocreate 電腦群組，以及這些記錄檔中搜尋 toouse 如何，您可以使用不同的方法。"
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: a28b9e8a-6761-4ead-aa61-c8451ca90125
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: bwren
ms.openlocfilehash: 7dafea9829e541f5582a1d855fafb82aa4d94430
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="computer-groups-in-log-analytics-log-searches"></a><span data-ttu-id="d2205-104">Log Analytics 記錄檔搜尋中的電腦群組</span><span class="sxs-lookup"><span data-stu-id="d2205-104">Computer groups in Log Analytics log searches</span></span>

>[!NOTE]
> <span data-ttu-id="d2205-105">本文說明 hello 使用使用 hello 目前記錄 Anayltics 查詢語言的電腦群組。</span><span class="sxs-lookup"><span data-stu-id="d2205-105">This article describes hello use of Computer Groups using hello current Log Anayltics query language.</span></span>    <span data-ttu-id="d2205-106">如果您的工作區已升級的 toohello[新的記錄分析查詢語言](log-analytics-log-search-upgrade.md)，則電腦群組的運作方式不同。</span><span class="sxs-lookup"><span data-stu-id="d2205-106">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then Computer Groups work differently.</span></span>  <span data-ttu-id="d2205-107">附註 hello 新的查詢語言提供在本文中與 hello 不同的語法和行為。</span><span class="sxs-lookup"><span data-stu-id="d2205-107">Notes are provided in this article with hello different syntax and behavior for hello new query language.</span></span>  


<span data-ttu-id="d2205-108">記錄分析中的電腦群組可讓您 tooscope[記錄搜尋](log-analytics-log-searches.md)tooa 特定一組電腦。</span><span class="sxs-lookup"><span data-stu-id="d2205-108">Computer groups in Log Analytics allow you tooscope [log searches](log-analytics-log-searches.md) tooa particular set of computers.</span></span>  <span data-ttu-id="d2205-109">使用您所定義的查詢，或從不同來源匯入群組，將電腦填入每個群組中。</span><span class="sxs-lookup"><span data-stu-id="d2205-109">Each group is populated with computers either using a query that you define or by importing groups from different sources.</span></span>  <span data-ttu-id="d2205-110">Hello 群組包含在記錄搜尋，hello 結果會是有限的 toorecords 符合 hello 群組中的 hello 電腦。</span><span class="sxs-lookup"><span data-stu-id="d2205-110">When hello group is included in a log search, hello results are limited toorecords that match hello computers in hello group.</span></span>

## <a name="creating-a-computer-group"></a><span data-ttu-id="d2205-111">建立電腦群組</span><span class="sxs-lookup"><span data-stu-id="d2205-111">Creating a computer group</span></span>
<span data-ttu-id="d2205-112">您可以建立電腦群組中使用任何 hello 方法 hello 下表中的記錄分析。</span><span class="sxs-lookup"><span data-stu-id="d2205-112">You can create a computer group in Log Analytics using any of hello methods in hello following table.</span></span>  <span data-ttu-id="d2205-113">Hello 的以下各節提供每個方法的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="d2205-113">Details on each method are provided in hello sections below.</span></span> 

| <span data-ttu-id="d2205-114">方法</span><span class="sxs-lookup"><span data-stu-id="d2205-114">Method</span></span> | <span data-ttu-id="d2205-115">說明</span><span class="sxs-lookup"><span data-stu-id="d2205-115">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="d2205-116">記錄搜尋</span><span class="sxs-lookup"><span data-stu-id="d2205-116">Log search</span></span> |<span data-ttu-id="d2205-117">建立會傳回一份電腦的記錄搜尋，並將 hello 結果儲存為電腦群組。</span><span class="sxs-lookup"><span data-stu-id="d2205-117">Create a log search that returns a list of computers and save hello results as a computer group.</span></span> |
| <span data-ttu-id="d2205-118">記錄檔搜尋 API</span><span class="sxs-lookup"><span data-stu-id="d2205-118">Log Search API</span></span> |<span data-ttu-id="d2205-119">使用 hello Log Search API tooprogrammatically 建立 hello 結果的記錄搜尋為基礎的電腦群組。</span><span class="sxs-lookup"><span data-stu-id="d2205-119">Use hello Log Search API tooprogrammatically create a computer group based on hello results of a log search.</span></span> |
| <span data-ttu-id="d2205-120">Active Directory</span><span class="sxs-lookup"><span data-stu-id="d2205-120">Active Directory</span></span> |<span data-ttu-id="d2205-121">自動掃描 hello 是 Active Directory 網域的成員，且記錄分析中建立群組，針對每個安全性群組的任何代理程式電腦群組成員資格。</span><span class="sxs-lookup"><span data-stu-id="d2205-121">Automatically scan hello group membership of any agent computers that are members of an Active Directory domain and create a group in Log Analytics for each security group.</span></span> |
| <span data-ttu-id="d2205-122">WSUS</span><span class="sxs-lookup"><span data-stu-id="d2205-122">WSUS</span></span> |<span data-ttu-id="d2205-123">自動掃描 WSUS 伺服器或用戶端來找出目標群組，並為每個群組在 Log Analytics 中建立一個群組。</span><span class="sxs-lookup"><span data-stu-id="d2205-123">Automatically scan WSUS servers or clients for targeting groups and create a group in Log Analytics for each.</span></span> |

### <a name="log-search"></a><span data-ttu-id="d2205-124">記錄搜尋</span><span class="sxs-lookup"><span data-stu-id="d2205-124">Log search</span></span>
<span data-ttu-id="d2205-125">所建立的記錄搜尋的電腦群組包含所有您定義的搜尋查詢所傳回的 hello 電腦。</span><span class="sxs-lookup"><span data-stu-id="d2205-125">Computer groups created from a Log Search contain all of hello computers returned by a search query that you define.</span></span>  <span data-ttu-id="d2205-126">此查詢會執行每次使用，因此任何 hello 群組建立以來的變更會反映 hello 電腦群組。</span><span class="sxs-lookup"><span data-stu-id="d2205-126">This query is run every time hello computer group is used so that any changes since hello group was created is reflected.</span></span>

<span data-ttu-id="d2205-127">使用記錄搜尋中的下列程序 toocreate 電腦群組的 hello。</span><span class="sxs-lookup"><span data-stu-id="d2205-127">Use hello following procedure toocreate a computer group from a log search.</span></span>

1. <span data-ttu-id="d2205-128">[建立記錄檔搜尋](log-analytics-log-searches.md)來傳回電腦清單。</span><span class="sxs-lookup"><span data-stu-id="d2205-128">[Create a log search](log-analytics-log-searches.md) that returns a list of computers.</span></span>  <span data-ttu-id="d2205-129">hello 搜尋必須傳回一組不同的電腦使用類似**相異電腦**或**measure count （) 電腦**hello 查詢中。</span><span class="sxs-lookup"><span data-stu-id="d2205-129">hello search must return a distinct set of computers by using something like **Distinct Computer** or **measure count() by Computer** in hello query.</span></span>  
2. <span data-ttu-id="d2205-130">按一下 hello**儲存**在 hello 囉 」 畫面最上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="d2205-130">Click hello **Save** button at hello top of hello screen.</span></span>
3. <span data-ttu-id="d2205-131">選取**是**太**將此查詢儲存為電腦群組**。</span><span class="sxs-lookup"><span data-stu-id="d2205-131">Select **Yes** too**Save this query as a computer group**.</span></span>
4. <span data-ttu-id="d2205-132">在中輸入**名稱**和**類別**hello 群組。</span><span class="sxs-lookup"><span data-stu-id="d2205-132">Type in a **Name** and a **Category** for hello group.</span></span>  <span data-ttu-id="d2205-133">如果以搜尋可 hello 相同名稱和類別目錄已經存在，則會被提示的 toooverwrite 它。</span><span class="sxs-lookup"><span data-stu-id="d2205-133">If a search with hello same name and category already exists, then you are be prompted toooverwrite it.</span></span>  <span data-ttu-id="d2205-134">您可以有多個不同分類名稱相同的 hello 與搜尋。</span><span class="sxs-lookup"><span data-stu-id="d2205-134">You can have multiple searches with hello same name in different categories.</span></span> 

<span data-ttu-id="d2205-135">以下是您可以儲存為電腦群組的搜尋範例。</span><span class="sxs-lookup"><span data-stu-id="d2205-135">Following are example searches that you can save as a computer group.</span></span>

    Computer="Computer1" OR Computer="Computer2" | distinct Computer 
    Computer=*srv* | measure count() by Computer

>[!NOTE]
> <span data-ttu-id="d2205-136">如果您的工作區已升級的 toohello[新的記錄分析查詢語言](log-analytics-log-search-upgrade.md)則 hello 下列變更會提出的 toohello 程序 toocreate 新電腦群組。</span><span class="sxs-lookup"><span data-stu-id="d2205-136">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md) then hello following changes are made toohello procedure toocreate a new computer group.</span></span>
>  
> - <span data-ttu-id="d2205-137">hello 電腦群組必須包含查詢 toocreate `distinct Computer`。</span><span class="sxs-lookup"><span data-stu-id="d2205-137">hello query toocreate a computer group must include `distinct Computer`.</span></span>  <span data-ttu-id="d2205-138">以下是查詢 toocreate 電腦群組的範例。</span><span class="sxs-lookup"><span data-stu-id="d2205-138">Following is an example of a query toocreate a computer group.</span></span><br>`Heartbeat | where Computer contains "srv" `
> - <span data-ttu-id="d2205-139">當您建立新的電腦群組時，您必須新增 toohello 名稱中指定的別名。</span><span class="sxs-lookup"><span data-stu-id="d2205-139">When you create a new computer group, you must specify an alias in addition toohello name.</span></span>  <span data-ttu-id="d2205-140">當使用在查詢中的 hello 電腦群組，如下所述，您可以使用 hello 別名。</span><span class="sxs-lookup"><span data-stu-id="d2205-140">You use hello alias when using hello computer group in a query as described below.</span></span>  

### <a name="log-search-api"></a><span data-ttu-id="d2205-141">記錄檔搜尋 API</span><span class="sxs-lookup"><span data-stu-id="d2205-141">Log search API</span></span>
<span data-ttu-id="d2205-142">電腦群組以 hello 記錄搜尋 API 是建立 hello 相同為使用記錄搜尋所建立的搜尋。</span><span class="sxs-lookup"><span data-stu-id="d2205-142">Computer groups created with hello Log Search API are hello same as searches created with a Log Search.</span></span>

<span data-ttu-id="d2205-143">如需建立使用 hello Log Search API 的電腦群組的詳細資訊，請參閱[記錄分析記錄檔中的電腦群組搜尋 REST API](log-analytics-log-search-api.md#computer-groups)。</span><span class="sxs-lookup"><span data-stu-id="d2205-143">For details on creating a computer group using hello Log Search API see [Computer Groups in Log Analytics log search REST API](log-analytics-log-search-api.md#computer-groups).</span></span>

### <a name="active-directory"></a><span data-ttu-id="d2205-144">Active Directory</span><span class="sxs-lookup"><span data-stu-id="d2205-144">Active Directory</span></span>
<span data-ttu-id="d2205-145">當您設定記錄分析 tooimport Active Directory 群組成員資格時，它會分析 hello hello OMS 代理程式的任何已加入網域電腦群組成員資格。</span><span class="sxs-lookup"><span data-stu-id="d2205-145">When you configure Log Analytics tooimport Active Directory group memberships, it analyzes hello group membership of any domain joined computers with hello OMS agent.</span></span>  <span data-ttu-id="d2205-146">電腦群組中建立記錄分析的每個安全性群組，在 Active Directory 中，並每一部電腦會加入對應 toohello 安全性群組的成員才 toohello 電腦群組。</span><span class="sxs-lookup"><span data-stu-id="d2205-146">A computer group is created in Log Analytics for each security group in Active Directory, and each computer is added toohello computer groups corresponding toohello security groups they are members of.</span></span>  <span data-ttu-id="d2205-147">此成員資格持續地每 4 小時更新一次。</span><span class="sxs-lookup"><span data-stu-id="d2205-147">This membership is continuously updated every 4 hours.</span></span>  

<span data-ttu-id="d2205-148">設定記錄分析 tooimport Active Directory 安全性群組從 hello**電腦群組**記錄分析中的功能表**設定**。</span><span class="sxs-lookup"><span data-stu-id="d2205-148">You configure Log Analytics tooimport Active Directory security groups from hello **Computer Groups** menu in Log Analytics **Settings**.</span></span>  <span data-ttu-id="d2205-149">選取 [自動化]，然後選取 [從電腦匯入 Active Directory 群組成員資格]。</span><span class="sxs-lookup"><span data-stu-id="d2205-149">Select **Automation** and then **Import Active Directory group memberships from computers**.</span></span>  <span data-ttu-id="d2205-150">不需要進一步的組態。</span><span class="sxs-lookup"><span data-stu-id="d2205-150">There is no further configuration required.</span></span>

![來自 Active Directory 的電腦群組](media/log-analytics-computer-groups/configure-activedirectory.png)

<span data-ttu-id="d2205-152">當群組已經匯入時，hello 功能表清單 hello 與群組成員資格的電腦數目偵測到與 hello 匯入的群組數目。</span><span class="sxs-lookup"><span data-stu-id="d2205-152">When groups have been imported, hello menu lists hello number of computers with group membership detected and hello number of groups imported.</span></span>  <span data-ttu-id="d2205-153">您可以按一下這些連結 tooreturn hello 任一**ComputerGroup**這項資訊的記錄。</span><span class="sxs-lookup"><span data-stu-id="d2205-153">You can click on either of these links tooreturn hello **ComputerGroup** records with this information.</span></span>

### <a name="windows-server-update-service"></a><span data-ttu-id="d2205-154">Windows Server Update Service</span><span class="sxs-lookup"><span data-stu-id="d2205-154">Windows Server Update Service</span></span>
<span data-ttu-id="d2205-155">當您設定記錄分析 tooimport WSUS 群組成員資格，它會分析 hello 目標 hello OMS 代理程式的任何電腦群組成員資格。</span><span class="sxs-lookup"><span data-stu-id="d2205-155">When you configure Log Analytics tooimport WSUS group memberships, it analyzes hello targeting group membership of any computers with hello OMS agent.</span></span>  <span data-ttu-id="d2205-156">如果您使用用戶端為目標，是連接的 tooOMS 且為任何 WSUS 目標群組一部分的任何電腦有其群組成員資格匯入 tooLog 分析。</span><span class="sxs-lookup"><span data-stu-id="d2205-156">If you are using client-side targeting, any computer that is connected tooOMS and is part of any WSUS targeting groups has its group membership imported tooLog Analytics.</span></span> <span data-ttu-id="d2205-157">如果您使用伺服器端為目標，hello OMS 代理程式應該安裝在 hello WSUS 伺服器 hello 群組成員資格資訊 toobe 匯入 tooOMS。</span><span class="sxs-lookup"><span data-stu-id="d2205-157">If you are using server-side targeting, hello OMS agent should be installed on hello WSUS server in order for hello group membership information toobe imported tooOMS.</span></span>  <span data-ttu-id="d2205-158">此成員資格持續地每 4 小時更新一次。</span><span class="sxs-lookup"><span data-stu-id="d2205-158">This membership is continuously updated every 4 hours.</span></span> 

<span data-ttu-id="d2205-159">設定記錄分析 tooimport Active Directory 安全性群組從 hello**電腦群組**記錄分析中的功能表**設定**。</span><span class="sxs-lookup"><span data-stu-id="d2205-159">You configure Log Analytics tooimport Active Directory security groups from hello **Computer Groups** menu in Log Analytics **Settings**.</span></span>  <span data-ttu-id="d2205-160">選取 [Active Directory]，然後選取 [從電腦匯入 Active Directory 群組成員資格]。</span><span class="sxs-lookup"><span data-stu-id="d2205-160">Select **Active Directory** and then **Import Active Directory group memberships from computers**.</span></span>  <span data-ttu-id="d2205-161">不需要進一步的組態。</span><span class="sxs-lookup"><span data-stu-id="d2205-161">There is no further configuration required.</span></span>

![來自 Active Directory 的電腦群組](media/log-analytics-computer-groups/configure-wsus.png)

<span data-ttu-id="d2205-163">當群組已經匯入時，hello 功能表清單 hello 與群組成員資格的電腦數目偵測到與 hello 匯入的群組數目。</span><span class="sxs-lookup"><span data-stu-id="d2205-163">When groups have been imported, hello menu lists hello number of computers with group membership detected and hello number of groups imported.</span></span>  <span data-ttu-id="d2205-164">您可以按一下這些連結 tooreturn hello 任一**ComputerGroup**這項資訊的記錄。</span><span class="sxs-lookup"><span data-stu-id="d2205-164">You can click on either of these links tooreturn hello **ComputerGroup** records with this information.</span></span>

## <a name="managing-computer-groups"></a><span data-ttu-id="d2205-165">管理電腦群組</span><span class="sxs-lookup"><span data-stu-id="d2205-165">Managing computer groups</span></span>
<span data-ttu-id="d2205-166">您可以檢視電腦群組所建立的記錄搜尋，或從 hello hello Log Search API**電腦群組**記錄分析中的功能表**設定**。</span><span class="sxs-lookup"><span data-stu-id="d2205-166">You can view computer groups that were created from a log search or hello Log Search API from hello **Computer Groups** menu in Log Analytics **Settings**.</span></span>  <span data-ttu-id="d2205-167">按一下 hello **x**在 hello**移除**資料行 toodelete hello 電腦群組。</span><span class="sxs-lookup"><span data-stu-id="d2205-167">Click hello **x** in hello **Remove** column toodelete hello computer group.</span></span>  <span data-ttu-id="d2205-168">按一下 hello**檢視成員**傳回其成員的群組 toorun hello 群組記錄搜尋圖示。</span><span class="sxs-lookup"><span data-stu-id="d2205-168">Click hello **View members** icon for a group toorun hello group's log search that returns its members.</span></span> 

![已儲存的電腦群組](media/log-analytics-computer-groups/configure-saved.png)

<span data-ttu-id="d2205-170">toomodify hello 群組中，建立新群組以 hello 相同**類別**和**名稱**toooverwrite hello 原始群組。</span><span class="sxs-lookup"><span data-stu-id="d2205-170">toomodify hello group, create a new group with hello same **Category** and **Name** toooverwrite hello original group.</span></span>

## <a name="using-a-computer-group-in-a-log-search"></a><span data-ttu-id="d2205-171">在記錄檔搜尋中使用電腦群組</span><span class="sxs-lookup"><span data-stu-id="d2205-171">Using a computer group in a log search</span></span>
<span data-ttu-id="d2205-172">您使用下列語法 toorefer tooa 電腦群組在記錄搜尋中的 hello。</span><span class="sxs-lookup"><span data-stu-id="d2205-172">You use hello following syntax toorefer tooa computer group in a log search.</span></span>  <span data-ttu-id="d2205-173">指定 hello**類別**是選擇性的而且只需要有電腦群組以不同的類別目錄中名稱相同的 hello。</span><span class="sxs-lookup"><span data-stu-id="d2205-173">Specifying hello **Category** is optional and only required if you have computer groups with hello same name in different categories.</span></span> 

    $ComputerGroups[Category: Name]

<span data-ttu-id="d2205-174">執行搜尋時，會先解析 hello hello 在搜尋中包含的任何電腦群組的成員。</span><span class="sxs-lookup"><span data-stu-id="d2205-174">When a search is run, hello members of any computer groups included in hello search are first resolved.</span></span>  <span data-ttu-id="d2205-175">Hello 群組根據 記錄搜尋，如果該搜尋是之前執行 hello 最上層的記錄搜尋執行 tooreturn hello hello 群組成員。</span><span class="sxs-lookup"><span data-stu-id="d2205-175">If hello group is based on a log search, then that search is run tooreturn hello members of hello group before performing hello top-level log search.</span></span>

<span data-ttu-id="d2205-176">電腦群組通常會使用 hello **IN**子句在 hello 記錄搜尋中如 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="d2205-176">Computer groups are typically used with hello **IN** clause in hello log search as in hello following example:</span></span>

    Type=UpdateSummary Computer IN $ComputerGroups[My Computer Group]

>[!NOTE]
> <span data-ttu-id="d2205-177">如果您的工作區已升級的 toohello[新的記錄分析查詢語言](log-analytics-log-search-upgrade.md)，然後在查詢中使用電腦群組將其別名做為函式，如 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="d2205-177">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you use a Computer group in a query by treating its alias as a function as in hello following example:</span></span>
> 
>  `UpdateSummary | where Computer IN (MyComputerGroup)`

## <a name="computer-group-records"></a><span data-ttu-id="d2205-178">電腦群組記錄</span><span class="sxs-lookup"><span data-stu-id="d2205-178">Computer group records</span></span>
<span data-ttu-id="d2205-179">從 Active Directory 或 WSUS 建立每個電腦群組成員資格的 hello OMS 儲存機制中建立的記錄。</span><span class="sxs-lookup"><span data-stu-id="d2205-179">A record is created in hello OMS repository for each computer group membership created from Active Directory or WSUS.</span></span>  <span data-ttu-id="d2205-180">這些記錄都有一種**ComputerGroup**和 hello 下表中都有 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="d2205-180">These records have a type of **ComputerGroup** and have hello properties in hello following table.</span></span>  <span data-ttu-id="d2205-181">如果電腦群組是根據記錄檔搜尋，則不會建立記錄。</span><span class="sxs-lookup"><span data-stu-id="d2205-181">Records are not created for computer groups based on log searches.</span></span>

| <span data-ttu-id="d2205-182">屬性</span><span class="sxs-lookup"><span data-stu-id="d2205-182">Property</span></span> | <span data-ttu-id="d2205-183">說明</span><span class="sxs-lookup"><span data-stu-id="d2205-183">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="d2205-184">類型</span><span class="sxs-lookup"><span data-stu-id="d2205-184">Type</span></span> |<span data-ttu-id="d2205-185">*ComputerGroup*</span><span class="sxs-lookup"><span data-stu-id="d2205-185">*ComputerGroup*</span></span> |
| <span data-ttu-id="d2205-186">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="d2205-186">SourceSystem</span></span> |<span data-ttu-id="d2205-187">*SourceSystem*</span><span class="sxs-lookup"><span data-stu-id="d2205-187">*SourceSystem*</span></span> |
| <span data-ttu-id="d2205-188">電腦</span><span class="sxs-lookup"><span data-stu-id="d2205-188">Computer</span></span> |<span data-ttu-id="d2205-189">Hello 成員電腦的名稱。</span><span class="sxs-lookup"><span data-stu-id="d2205-189">Name of hello member computer.</span></span> |
| <span data-ttu-id="d2205-190">群組</span><span class="sxs-lookup"><span data-stu-id="d2205-190">Group</span></span> |<span data-ttu-id="d2205-191">Hello 群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="d2205-191">Name of hello group.</span></span> |
| <span data-ttu-id="d2205-192">GroupFullName</span><span class="sxs-lookup"><span data-stu-id="d2205-192">GroupFullName</span></span> |<span data-ttu-id="d2205-193">完整路徑 toohello 群組包括 hello 來源與來源名稱。</span><span class="sxs-lookup"><span data-stu-id="d2205-193">Full path toohello group including hello source and source name.</span></span> |
| <span data-ttu-id="d2205-194">GroupSource</span><span class="sxs-lookup"><span data-stu-id="d2205-194">GroupSource</span></span> |<span data-ttu-id="d2205-195">群組的收集來源。</span><span class="sxs-lookup"><span data-stu-id="d2205-195">Source that group was collected from.</span></span> <br><br><span data-ttu-id="d2205-196">ActiveDirectory</span><span class="sxs-lookup"><span data-stu-id="d2205-196">ActiveDirectory</span></span><br><span data-ttu-id="d2205-197">WSUS</span><span class="sxs-lookup"><span data-stu-id="d2205-197">WSUS</span></span><br><span data-ttu-id="d2205-198">WSUSClientTargeting</span><span class="sxs-lookup"><span data-stu-id="d2205-198">WSUSClientTargeting</span></span> |
| <span data-ttu-id="d2205-199">GroupSourceName</span><span class="sxs-lookup"><span data-stu-id="d2205-199">GroupSourceName</span></span> |<span data-ttu-id="d2205-200">從收集 hello 來源 hello 群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="d2205-200">Name of hello source that hello group was collected from.</span></span>  <span data-ttu-id="d2205-201">針對 Active Directory，這是 hello 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="d2205-201">For Active Directory, this is hello domain name.</span></span> |
| <span data-ttu-id="d2205-202">ManagementGroupName</span><span class="sxs-lookup"><span data-stu-id="d2205-202">ManagementGroupName</span></span> |<span data-ttu-id="d2205-203">SCOM 代理程式 hello 管理群組名稱。</span><span class="sxs-lookup"><span data-stu-id="d2205-203">Name of hello management group for SCOM agents.</span></span>  <span data-ttu-id="d2205-204">若為其他代理程式，此為 AOI-\<工作區 ID\></span><span class="sxs-lookup"><span data-stu-id="d2205-204">For other agents, this is AOI-\<workspace ID\></span></span> |
| <span data-ttu-id="d2205-205">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="d2205-205">TimeGenerated</span></span> |<span data-ttu-id="d2205-206">建立或更新的日期和時間的 hello 電腦群組。</span><span class="sxs-lookup"><span data-stu-id="d2205-206">Date and time hello computer group was created or updated.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d2205-207">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d2205-207">Next steps</span></span>
* <span data-ttu-id="d2205-208">深入了解[記錄搜尋](log-analytics-log-searches.md)tooanalyze hello 資料收集的資料來源和解決方案。</span><span class="sxs-lookup"><span data-stu-id="d2205-208">Learn about [log searches](log-analytics-log-searches.md) tooanalyze hello data collected from data sources and solutions.</span></span>  

