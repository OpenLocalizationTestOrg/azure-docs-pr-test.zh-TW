---
title: "aaaCreate 和共用 Azure 入口網站的儀表板 |Microsoft 文件"
description: "本文說明如何 toocreate 和編輯的儀表板 hello Azure 入口網站。"
services: azure-portal
documentationcenter: 
author: sewatson
manager: timlt
editor: tysonn
ms.assetid: ff422f36-47d2-409b-8a19-02e24b03ffe7
ms.service: multiple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 09/06/2016
ms.author: sewatson
ms.openlocfilehash: 0facd10fe3284d7ad9a9e29791e5af5b5b95c97f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-share-dashboards-in-hello-azure-portal"></a><span data-ttu-id="d73da-103">建立並共用 hello Azure 入口網站的儀表板</span><span class="sxs-lookup"><span data-stu-id="d73da-103">Create and share dashboards in hello Azure portal</span></span>
<span data-ttu-id="d73da-104">您可以建立多個儀表板並分享與其他人存取 tooyour Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d73da-104">You can create multiple dashboards and share them with others who have access tooyour Azure subscriptions.</span></span>  <span data-ttu-id="d73da-105">這篇文章探討 hello 的建立、 編輯、 發行及管理存取 toodashboards 的基本概念。</span><span class="sxs-lookup"><span data-stu-id="d73da-105">This article goes through hello basics of creating, editing, publishing, and managing access toodashboards.</span></span>

## <a name="create-a-dashboard"></a><span data-ttu-id="d73da-106">建立儀表板</span><span class="sxs-lookup"><span data-stu-id="d73da-106">Create a dashboard</span></span>
<span data-ttu-id="d73da-107">toocreate 儀表板中，選取 hello**新儀表板**按鈕下一步 toohello 目前儀表板的名稱。</span><span class="sxs-lookup"><span data-stu-id="d73da-107">toocreate a dashboard, select hello **New dashboard** button next toohello current dashboard's name.</span></span>  

![建立儀表板](./media/azure-portal-dashboards/new-dashboard.png)

<span data-ttu-id="d73da-109">這個動作會建立全新的空白私人儀表板並讓您進入自訂模式，供您為儀表板命名並新增或重新排列圖格。</span><span class="sxs-lookup"><span data-stu-id="d73da-109">This action creates a new, empty, private dashboard and puts you into customization mode where you can name your dashboard and add or rearrange tiles.</span></span>  <span data-ttu-id="d73da-110">在此模式下，hello 可摺疊會並排組件庫會使用透過 hello 左的導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="d73da-110">When in this mode, hello collapsible tile gallery takes over hello left navigation menu.</span></span>  <span data-ttu-id="d73da-111">hello 並排組件庫可讓您尋找磚為您的 Azure 資源不同的方式： 您可以瀏覽[資源群組](../azure-resource-manager/resource-group-overview.md#resource-groups)、 藉由資源類型，由[標記](../azure-resource-manager/resource-group-using-tags.md)，或依名稱搜尋您的資源。</span><span class="sxs-lookup"><span data-stu-id="d73da-111">hello tile gallery lets you find tiles for your Azure resources in various ways: you can browse by [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups), by resource type, by [tag](../azure-resource-manager/resource-group-using-tags.md), or by searching for your resource by name.</span></span>  

![自訂儀表板](./media/azure-portal-dashboards/customize-dashboard.png)

<span data-ttu-id="d73da-113">將磚加入拖曳和卸除它們拖曳至 hello 儀表板介面想要的位置。</span><span class="sxs-lookup"><span data-stu-id="d73da-113">Add tiles by dragging and dropping them onto hello dashboard surface wherever you want.</span></span>

<span data-ttu-id="d73da-114">未與特定資源相關聯的圖格有新的類別，其名稱為**一般**。</span><span class="sxs-lookup"><span data-stu-id="d73da-114">There's a new category called **General** for tiles that are not associated with a particular resource.</span></span>  <span data-ttu-id="d73da-115">在此範例中，我們 hello Markdown 圖格釘選。</span><span class="sxs-lookup"><span data-stu-id="d73da-115">In this example, we pin hello Markdown tile.</span></span>  <span data-ttu-id="d73da-116">您使用此磚 tooadd 自訂內容 tooyour 儀表板。</span><span class="sxs-lookup"><span data-stu-id="d73da-116">You use this tile tooadd custom content tooyour dashboard.</span></span>  <span data-ttu-id="d73da-117">hello 磚支援純文字[Markdown 語法](https://daringfireball.net/projects/markdown/syntax)，和一組有限的 HTML。</span><span class="sxs-lookup"><span data-stu-id="d73da-117">hello tile supports plain text, [Markdown syntax](https://daringfireball.net/projects/markdown/syntax), and a limited set of HTML.</span></span>  <span data-ttu-id="d73da-118">(基於安全考量，您無法執行一些作業，例如插入`<script>`標記，或使用特定的樣式項目，可能會干擾 hello 入口網站的 CSS。)</span><span class="sxs-lookup"><span data-stu-id="d73da-118">(For safety, you can't do things like inject `<script>` tags or use certain styling element of CSS that might interfere with hello portal.)</span></span> 

![新增 Markdown](./media/azure-portal-dashboards/add-markdown.png)

## <a name="edit-a-dashboard"></a><span data-ttu-id="d73da-120">編輯儀表板</span><span class="sxs-lookup"><span data-stu-id="d73da-120">Edit a dashboard</span></span>
<span data-ttu-id="d73da-121">建立儀表板之後, 您可以釘選圖格來自 hello 並排組件庫或 hello 磚表示刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d73da-121">After creating your dashboard, you can pin tiles from hello tile gallery or hello tile representation of blades.</span></span> <span data-ttu-id="d73da-122">讓我們釘選 hello 表示我們的資源群組。</span><span class="sxs-lookup"><span data-stu-id="d73da-122">Let's pin hello representation of our resource group.</span></span> <span data-ttu-id="d73da-123">您也可以是固定項目，或從 hello 資源群組 刀鋒視窗，瀏覽 hello 時。</span><span class="sxs-lookup"><span data-stu-id="d73da-123">You can either pin when browsing hello item, or from hello resource group blade.</span></span> <span data-ttu-id="d73da-124">釘選磚表示法 hello hello 資源群組導致這兩種方法。</span><span class="sxs-lookup"><span data-stu-id="d73da-124">Both approaches result in pinning hello tile representation of hello resource group.</span></span>

![Pin toodashboard](./media/azure-portal-dashboards/pin-to-dashboard.png)

<span data-ttu-id="d73da-126">Hello 項目釘選，它就會出現在儀表板上。</span><span class="sxs-lookup"><span data-stu-id="d73da-126">After pinning hello item, it appears on your dashboard.</span></span>

![檢視儀表板](./media/azure-portal-dashboards/view-dashboard.png)

<span data-ttu-id="d73da-128">現在，我們已經 Markdown 磚和資源群組已釘選的 toohello 儀表板，我們可以調整大小及重新排列 hello 磚磚至適合的配置。</span><span class="sxs-lookup"><span data-stu-id="d73da-128">Now that we have a Markdown tile and a resource group pinned toohello dashboard, we can resize and rearrange hello tiles into a suitable layout.</span></span>

<span data-ttu-id="d73da-129">暫留並選取"..."或磚上按一下滑鼠右鍵，您可以看到該磚的 hello 內容命令。</span><span class="sxs-lookup"><span data-stu-id="d73da-129">By hovering and selecting "…" or right-clicking on a tile you can see all hello contextual commands for that tile.</span></span> <span data-ttu-id="d73da-130">預設會有兩個項目：</span><span class="sxs-lookup"><span data-stu-id="d73da-130">By default, there are two items:</span></span>

1. <span data-ttu-id="d73da-131">**從儀表板取消釘選**– 移除 hello hello 儀表板圖格</span><span class="sxs-lookup"><span data-stu-id="d73da-131">**Unpin from dashboard** – removes hello tile from hello dashboard</span></span>
2. <span data-ttu-id="d73da-132">**自訂** – 進入自訂模式</span><span class="sxs-lookup"><span data-stu-id="d73da-132">**Customize** – enters customize mode</span></span>

![自訂圖格](./media/azure-portal-dashboards/customize-tile.png)

<span data-ttu-id="d73da-134">藉由選取自訂，您可以將圖格調整大小並重新排列。</span><span class="sxs-lookup"><span data-stu-id="d73da-134">By selecting customize, you can resize and reorder tiles.</span></span> <span data-ttu-id="d73da-135">hello 下列影像所示，tooresize 磚中，選取 hello hello 內容功能表上，從新的大小。</span><span class="sxs-lookup"><span data-stu-id="d73da-135">tooresize a tile, select hello new size from hello contextual menu, as shown in hello following image.</span></span>

![對圖格調整大小](./media/azure-portal-dashboards/resize-tile.png)

<span data-ttu-id="d73da-137">或者，如果 hello 磚支援任何大小，您可以拖曳 hello 底端右下角 toohello 預期大小。</span><span class="sxs-lookup"><span data-stu-id="d73da-137">Or, if hello tile supports any size, you can drag hello bottom right-hand corner toohello desired size.</span></span>

![對圖格調整大小](./media/azure-portal-dashboards/resize-corner.png)

<span data-ttu-id="d73da-139">之後調整磚的大小，檢視 hello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="d73da-139">After resizing tiles, view hello dashboard.</span></span>

![檢視圖格](./media/azure-portal-dashboards/view-tile.png)

<span data-ttu-id="d73da-141">一旦您完成自訂儀表板時，只需選取 hello**完成自訂**tooexit 自訂模式或以滑鼠右鍵按一下並選取**完成自訂**hello 操作功能表中。</span><span class="sxs-lookup"><span data-stu-id="d73da-141">Once you are finished customizing a dashboard, simply select hello **Done customizing** tooexit customize mode or right-click and select **Done customizing** from hello context menu.</span></span>

## <a name="publish-a-dashboard-and-manage-access-control"></a><span data-ttu-id="d73da-142">發佈儀表板和管理存取控制</span><span class="sxs-lookup"><span data-stu-id="d73da-142">Publish a dashboard and manage access control</span></span>
<span data-ttu-id="d73da-143">當您建立儀表板時，它是私用根據預設，這表示您可以看到它 hello 唯一人員項目。</span><span class="sxs-lookup"><span data-stu-id="d73da-143">When you create a dashboard, it is private by default, which means you are hello only person who can see it.</span></span>  <span data-ttu-id="d73da-144">toomake 它可見 tooothers，使用 hello**共用**顯示在旁邊的按鈕 hello 其他儀表板的命令。</span><span class="sxs-lookup"><span data-stu-id="d73da-144">toomake it visible tooothers, use hello **Share** button that appears alongside hello other dashboard commands.</span></span>

![共用儀表板](./media/azure-portal-dashboards/share-dashboard.png)

<span data-ttu-id="d73da-146">系統會要求您發行至的訂用帳戶和資源群組的儀表板 toobe toochoose。</span><span class="sxs-lookup"><span data-stu-id="d73da-146">You are asked toochoose a subscription and resource group for your dashboard toobe published to.</span></span> <span data-ttu-id="d73da-147">tooseamlessly 整合 hello 生態系統中的儀表板，我們已共用的儀表板實作做為 Azure 資源 （如此您就無法共用輸入電子郵件地址）。</span><span class="sxs-lookup"><span data-stu-id="d73da-147">tooseamlessly integrate dashboards into hello ecosystem, we've implemented shared dashboards as Azure resources (so you can't share by typing an email address).</span></span>  <span data-ttu-id="d73da-148">大部分的 hello 入口網站中的 hello 磚所顯示的存取 toohello 資訊都受到[Azure Role Based Access Control](../active-directory/role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="d73da-148">Access toohello information displayed by most of hello tiles in hello portal are governed by [Azure Role Based Access Control](../active-directory/role-based-access-control-configure.md).</span></span> <span data-ttu-id="d73da-149">從存取控制觀點來看，共用儀表板與虛擬機器或儲存體帳戶並無不同。</span><span class="sxs-lookup"><span data-stu-id="d73da-149">From an access control perspective, shared dashboards are no different from a virtual machine or a storage account.</span></span>  

<span data-ttu-id="d73da-150">讓我們假設您有 Azure 訂用帳戶和您的小組成員已指派給 hello 角色**擁有者**，**參與者**，或**讀取器**hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d73da-150">Let's say you have an Azure subscription and members of your team have been assigned hello roles of **owner**, **contributor**, or **reader** of hello subscription.</span></span>  <span data-ttu-id="d73da-151">使用者是擁有者或參與者都可以 toolist，檢視、 建立、 修改或刪除該訂用帳戶內的儀表板。</span><span class="sxs-lookup"><span data-stu-id="d73da-151">Users who are owners or contributors are able toolist, view, create, modify, or delete dashboards within that subscription.</span></span>  <span data-ttu-id="d73da-152">讀取器的使用者都能 toolist 和檢視儀表板，但無法修改或刪除它們。</span><span class="sxs-lookup"><span data-stu-id="d73da-152">Users who are readers are able toolist and view dashboards, but cannot modify or delete them.</span></span>  <span data-ttu-id="d73da-153">讀取器存取的使用者可以 toomake 本機編輯 tooa 共用儀表板，但您不能 toopublish 這些變更後 toohello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d73da-153">Users with reader access are able toomake local edits tooa shared dashboard, but are not able toopublish those changes back toohello server.</span></span>  <span data-ttu-id="d73da-154">不過，它們可讓 hello 儀表板供自己使用的私用複本。</span><span class="sxs-lookup"><span data-stu-id="d73da-154">However, they can make a private copy of hello dashboard for their own use.</span></span>  <span data-ttu-id="d73da-155">一如往常，個別的圖格 hello 儀表板上強制執行自己根據它們對應於 hello 資源的存取控制規則。</span><span class="sxs-lookup"><span data-stu-id="d73da-155">As always, individual tiles on hello dashboard enforce their own access control rules based on hello resources they correspond to.</span></span>  

<span data-ttu-id="d73da-156">為了方便起見，hello 入口網站的發行您朝向您放置儀表板資源群組中的模式稱為體驗指南**儀表板**。</span><span class="sxs-lookup"><span data-stu-id="d73da-156">For convenience, hello portal's publishing experience guides you towards a pattern where you place dashboards in a resource group called **dashboards**.</span></span>  

![發佈儀表板](./media/azure-portal-dashboards/publish-dashboard.png)

<span data-ttu-id="d73da-158">您也可以選擇 toopublish 儀表板 tooa 特定資源群組。</span><span class="sxs-lookup"><span data-stu-id="d73da-158">You can also choose toopublish a dashboard tooa particular resource group.</span></span>  <span data-ttu-id="d73da-159">hello 該儀表板的存取控制會比對 hello hello 資源群組的存取控制。</span><span class="sxs-lookup"><span data-stu-id="d73da-159">hello access control for that dashboard matches hello access control for hello resource group.</span></span>  <span data-ttu-id="d73da-160">使用者可以管理該資源群組中的 hello 資源也會有存取 toohello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="d73da-160">Users that can manage hello resources in that resource group also have access toohello dashboards.</span></span>

![發行儀表板 tooresource 群組](./media/azure-portal-dashboards/publish-to-resource-group.png)

<span data-ttu-id="d73da-162">發行您的儀表板之後，hello**共用 + 存取**控制項窗格將會重新整理並顯示 hello 發行儀表板，包括連結 toomanage 使用者存取 toohello 儀表板的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="d73da-162">After your dashboard is published, hello **Sharing + access** control pane will refresh and show you information about hello published dashboard, including a link toomanage user access toohello dashboard.</span></span>  <span data-ttu-id="d73da-163">此連結會啟動 hello 標準 Role Based Access Control 刀鋒視窗中使用 toomanage 對於任何 Azure 資源存取。</span><span class="sxs-lookup"><span data-stu-id="d73da-163">This link launches hello standard Role Based Access Control blade used toomanage access for any Azure resource.</span></span>  <span data-ttu-id="d73da-164">您可以一律會回到 toothis 檢視選取**共用**。</span><span class="sxs-lookup"><span data-stu-id="d73da-164">You can always get back toothis view by selecting **Share**.</span></span>

![管理存取控制](./media/azure-portal-dashboards/manage-access.png)

## <a name="next-steps"></a><span data-ttu-id="d73da-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d73da-166">Next steps</span></span>
* <span data-ttu-id="d73da-167">toomanage 資源，請參閱[透過入口網站管理 Azure 資源](../azure-resource-manager/resource-group-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="d73da-167">toomanage resources, see [Manage Azure resources through portal](../azure-resource-manager/resource-group-portal.md).</span></span>
* <span data-ttu-id="d73da-168">toodeploy 資源，請參閱[部署具有資源管理員範本和 Azure 入口網站資源](../azure-resource-manager/resource-group-template-deploy-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="d73da-168">toodeploy resources, see [Deploy resources with Resource Manager templates and Azure portal](../azure-resource-manager/resource-group-template-deploy-portal.md).</span></span>

