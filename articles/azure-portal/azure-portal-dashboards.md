---
title: "建立和共用 Azure 入口網站儀表板 | Microsoft Docs"
description: "本文說明如何在 Azure 入口網站建立和編輯儀表板。"
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
ms.openlocfilehash: 5429e68723448ff5db6ef0ed8da1b927e97e6dd9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-share-dashboards-in-the-azure-portal"></a><span data-ttu-id="23c8f-103">在 Azure 入口網站中建立和共用儀表板</span><span class="sxs-lookup"><span data-stu-id="23c8f-103">Create and share dashboards in the Azure portal</span></span>
<span data-ttu-id="23c8f-104">您可以建立多個儀表板，並與可存取您 Azure 訂用帳戶的其他人共用。</span><span class="sxs-lookup"><span data-stu-id="23c8f-104">You can create multiple dashboards and share them with others who have access to your Azure subscriptions.</span></span>  <span data-ttu-id="23c8f-105">本文說明建立/編輯、發佈和管理儀表板存取權的基本概念。</span><span class="sxs-lookup"><span data-stu-id="23c8f-105">This article goes through the basics of creating, editing, publishing, and managing access to dashboards.</span></span>

## <a name="create-a-dashboard"></a><span data-ttu-id="23c8f-106">建立儀表板</span><span class="sxs-lookup"><span data-stu-id="23c8f-106">Create a dashboard</span></span>
<span data-ttu-id="23c8f-107">若要建立儀表板，請選取目前的儀表板名稱旁的 [新增儀表板]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="23c8f-107">To create a dashboard, select the **New dashboard** button next to the current dashboard's name.</span></span>  

![建立儀表板](./media/azure-portal-dashboards/new-dashboard.png)

<span data-ttu-id="23c8f-109">這個動作會建立全新的空白私人儀表板並讓您進入自訂模式，供您為儀表板命名並新增或重新排列圖格。</span><span class="sxs-lookup"><span data-stu-id="23c8f-109">This action creates a new, empty, private dashboard and puts you into customization mode where you can name your dashboard and add or rearrange tiles.</span></span>  <span data-ttu-id="23c8f-110">處於此模式時，可摺疊的圖格庫會接管左側導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="23c8f-110">When in this mode, the collapsible tile gallery takes over the left navigation menu.</span></span>  <span data-ttu-id="23c8f-111">圖格庫可讓您以各種方式尋找 Azure 資源的圖格︰您可以依[資源群組](../azure-resource-manager/resource-group-overview.md#resource-groups)、資源類型、[標籤](../azure-resource-manager/resource-group-using-tags.md)進行瀏覽，或依名稱搜尋資源。</span><span class="sxs-lookup"><span data-stu-id="23c8f-111">The tile gallery lets you find tiles for your Azure resources in various ways: you can browse by [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups), by resource type, by [tag](../azure-resource-manager/resource-group-using-tags.md), or by searching for your resource by name.</span></span>  

![自訂儀表板](./media/azure-portal-dashboards/customize-dashboard.png)

<span data-ttu-id="23c8f-113">拖放圖格到儀表板介面上想要的位置來加以新增。</span><span class="sxs-lookup"><span data-stu-id="23c8f-113">Add tiles by dragging and dropping them onto the dashboard surface wherever you want.</span></span>

<span data-ttu-id="23c8f-114">未與特定資源相關聯的圖格有新的類別，其名稱為**一般**。</span><span class="sxs-lookup"><span data-stu-id="23c8f-114">There's a new category called **General** for tiles that are not associated with a particular resource.</span></span>  <span data-ttu-id="23c8f-115">在此範例中，我們釘選 [Markdown] 圖格。</span><span class="sxs-lookup"><span data-stu-id="23c8f-115">In this example, we pin the Markdown tile.</span></span>  <span data-ttu-id="23c8f-116">您可以使用此圖格將自訂內容新增至儀表板。</span><span class="sxs-lookup"><span data-stu-id="23c8f-116">You use this tile to add custom content to your dashboard.</span></span>  <span data-ttu-id="23c8f-117">圖格支援純文字、[Markdown 語法](https://daringfireball.net/projects/markdown/syntax)和一組有限的 HTML </span><span class="sxs-lookup"><span data-stu-id="23c8f-117">The tile supports plain text, [Markdown syntax](https://daringfireball.net/projects/markdown/syntax), and a limited set of HTML.</span></span>  <span data-ttu-id="23c8f-118">(基於安全考量，您無法執行插入 `<script>` 標籤或使用可能會干擾入口網站的特定 CSS 樣式元素等動作)。</span><span class="sxs-lookup"><span data-stu-id="23c8f-118">(For safety, you can't do things like inject `<script>` tags or use certain styling element of CSS that might interfere with the portal.)</span></span> 

![新增 Markdown](./media/azure-portal-dashboards/add-markdown.png)

## <a name="edit-a-dashboard"></a><span data-ttu-id="23c8f-120">編輯儀表板</span><span class="sxs-lookup"><span data-stu-id="23c8f-120">Edit a dashboard</span></span>
<span data-ttu-id="23c8f-121">建立儀表板之後，您可以從圖格庫或以圖格表示的刀鋒視窗釘選圖格。</span><span class="sxs-lookup"><span data-stu-id="23c8f-121">After creating your dashboard, you can pin tiles from the tile gallery or the tile representation of blades.</span></span> <span data-ttu-id="23c8f-122">釘選資源群組表示方法。</span><span class="sxs-lookup"><span data-stu-id="23c8f-122">Let's pin the representation of our resource group.</span></span> <span data-ttu-id="23c8f-123">您可以在瀏覽項目時釘選，或從資源群組刀鋒視窗釘選。</span><span class="sxs-lookup"><span data-stu-id="23c8f-123">You can either pin when browsing the item, or from the resource group blade.</span></span> <span data-ttu-id="23c8f-124">這兩種方法都會釘選以圖格表示的資源群組。</span><span class="sxs-lookup"><span data-stu-id="23c8f-124">Both approaches result in pinning the tile representation of the resource group.</span></span>

![釘選到儀表板](./media/azure-portal-dashboards/pin-to-dashboard.png)

<span data-ttu-id="23c8f-126">釘選項目之後，它就會出現在儀表板上。</span><span class="sxs-lookup"><span data-stu-id="23c8f-126">After pinning the item, it appears on your dashboard.</span></span>

![檢視儀表板](./media/azure-portal-dashboards/view-dashboard.png)

<span data-ttu-id="23c8f-128">現在我們已將 Markdown 圖格和資源群組釘選到儀表板，接下來，我們可以將圖格調整大小並重新排列為適合的版面配置。</span><span class="sxs-lookup"><span data-stu-id="23c8f-128">Now that we have a Markdown tile and a resource group pinned to the dashboard, we can resize and rearrange the tiles into a suitable layout.</span></span>

<span data-ttu-id="23c8f-129">藉由將滑鼠游標停留在 "..." 並加以選取或是對圖格按一下滑鼠右鍵，您就可以看到該圖格的所有關聯式命令。</span><span class="sxs-lookup"><span data-stu-id="23c8f-129">By hovering and selecting "…" or right-clicking on a tile you can see all the contextual commands for that tile.</span></span> <span data-ttu-id="23c8f-130">預設會有兩個項目：</span><span class="sxs-lookup"><span data-stu-id="23c8f-130">By default, there are two items:</span></span>

1. <span data-ttu-id="23c8f-131">**從儀表板取消釘選** – 從儀表板移除圖格</span><span class="sxs-lookup"><span data-stu-id="23c8f-131">**Unpin from dashboard** – removes the tile from the dashboard</span></span>
2. <span data-ttu-id="23c8f-132">**自訂** – 進入自訂模式</span><span class="sxs-lookup"><span data-stu-id="23c8f-132">**Customize** – enters customize mode</span></span>

![自訂圖格](./media/azure-portal-dashboards/customize-tile.png)

<span data-ttu-id="23c8f-134">藉由選取自訂，您可以將圖格調整大小並重新排列。</span><span class="sxs-lookup"><span data-stu-id="23c8f-134">By selecting customize, you can resize and reorder tiles.</span></span> <span data-ttu-id="23c8f-135">若要為圖格調整大小，請從關聯式功能表選取新的大小，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="23c8f-135">To resize a tile, select the new size from the contextual menu, as shown in the following image.</span></span>

![對圖格調整大小](./media/azure-portal-dashboards/resize-tile.png)

<span data-ttu-id="23c8f-137">或者，如果圖格支援任何大小，您可以將右下角拖曳到所需大小。</span><span class="sxs-lookup"><span data-stu-id="23c8f-137">Or, if the tile supports any size, you can drag the bottom right-hand corner to the desired size.</span></span>

![對圖格調整大小](./media/azure-portal-dashboards/resize-corner.png)

<span data-ttu-id="23c8f-139">將圖格調整大小之後，檢視儀表板。</span><span class="sxs-lookup"><span data-stu-id="23c8f-139">After resizing tiles, view the dashboard.</span></span>

![檢視圖格](./media/azure-portal-dashboards/view-tile.png)

<span data-ttu-id="23c8f-141">在儀表板完成自訂後，只需選取 [完成自訂] 來結束自訂模式，或按一下滑鼠右鍵並從關聯式功能表選取 [完成自訂]。</span><span class="sxs-lookup"><span data-stu-id="23c8f-141">Once you are finished customizing a dashboard, simply select the **Done customizing** to exit customize mode or right-click and select **Done customizing** from the context menu.</span></span>

## <a name="publish-a-dashboard-and-manage-access-control"></a><span data-ttu-id="23c8f-142">發佈儀表板和管理存取控制</span><span class="sxs-lookup"><span data-stu-id="23c8f-142">Publish a dashboard and manage access control</span></span>
<span data-ttu-id="23c8f-143">當您建立儀表板時，它預設是私人用途，這表示只有您會看得到。</span><span class="sxs-lookup"><span data-stu-id="23c8f-143">When you create a dashboard, it is private by default, which means you are the only person who can see it.</span></span>  <span data-ttu-id="23c8f-144">若要讓其他人也能看見，請使用與其他儀表板命令一同出現的 [共用]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="23c8f-144">To make it visible to others, use the **Share** button that appears alongside the other dashboard commands.</span></span>

![共用儀表板](./media/azure-portal-dashboards/share-dashboard.png)

<span data-ttu-id="23c8f-146">系統會要求您選擇可將儀表板發佈至的訂用帳戶和資源群組。</span><span class="sxs-lookup"><span data-stu-id="23c8f-146">You are asked to choose a subscription and resource group for your dashboard to be published to.</span></span> <span data-ttu-id="23c8f-147">為了將儀表板完美整合到生態系統，我們已將共用儀表板實作為 Azure 資源 (因此，您無法透過輸入電子郵件地址來共用)。</span><span class="sxs-lookup"><span data-stu-id="23c8f-147">To seamlessly integrate dashboards into the ecosystem, we've implemented shared dashboards as Azure resources (so you can't share by typing an email address).</span></span>  <span data-ttu-id="23c8f-148">入口網站中大多數圖格所顯示資訊的存取權是由 [Azure 角色型存取控制](../active-directory/role-based-access-control-configure.md)所控管。</span><span class="sxs-lookup"><span data-stu-id="23c8f-148">Access to the information displayed by most of the tiles in the portal are governed by [Azure Role Based Access Control](../active-directory/role-based-access-control-configure.md).</span></span> <span data-ttu-id="23c8f-149">從存取控制觀點來看，共用儀表板與虛擬機器或儲存體帳戶並無不同。</span><span class="sxs-lookup"><span data-stu-id="23c8f-149">From an access control perspective, shared dashboards are no different from a virtual machine or a storage account.</span></span>  

<span data-ttu-id="23c8f-150">假設您有 Azure 訂用帳戶，而且已為小組成員指派訂用帳戶的**擁有者**、**參與者**或**讀取者**角色。</span><span class="sxs-lookup"><span data-stu-id="23c8f-150">Let's say you have an Azure subscription and members of your team have been assigned the roles of **owner**, **contributor**, or **reader** of the subscription.</span></span>  <span data-ttu-id="23c8f-151">身為擁有者或參與者的使用者能夠列出、檢視、建立、修改或刪除該訂用帳戶內的儀表板。</span><span class="sxs-lookup"><span data-stu-id="23c8f-151">Users who are owners or contributors are able to list, view, create, modify, or delete dashboards within that subscription.</span></span>  <span data-ttu-id="23c8f-152">身為讀取者的使用者能夠列出和檢視儀表板，但無法進行修改或刪除。</span><span class="sxs-lookup"><span data-stu-id="23c8f-152">Users who are readers are able to list and view dashboards, but cannot modify or delete them.</span></span>  <span data-ttu-id="23c8f-153">具有讀取者存取權的使用者能夠對共用的儀表板進行本機編輯，但無法將這些變更發佈回伺服器。</span><span class="sxs-lookup"><span data-stu-id="23c8f-153">Users with reader access are able to make local edits to a shared dashboard, but are not able to publish those changes back to the server.</span></span>  <span data-ttu-id="23c8f-154">不過，他們可以製作儀表板的私人複本供自己使用。</span><span class="sxs-lookup"><span data-stu-id="23c8f-154">However, they can make a private copy of the dashboard for their own use.</span></span>  <span data-ttu-id="23c8f-155">一如往常，儀表板上的個別圖格會根據其對應的資源，強制執行自己的存取控制規則。</span><span class="sxs-lookup"><span data-stu-id="23c8f-155">As always, individual tiles on the dashboard enforce their own access control rules based on the resources they correspond to.</span></span>  

<span data-ttu-id="23c8f-156">為了方便起見，入口網站的發佈體驗會引導您朝向將儀表板放在稱為 **儀表板**的資源群組中的模式。</span><span class="sxs-lookup"><span data-stu-id="23c8f-156">For convenience, the portal's publishing experience guides you towards a pattern where you place dashboards in a resource group called **dashboards**.</span></span>  

![發佈儀表板](./media/azure-portal-dashboards/publish-dashboard.png)

<span data-ttu-id="23c8f-158">您也可以選擇將儀表板發佈到特定資源群組。</span><span class="sxs-lookup"><span data-stu-id="23c8f-158">You can also choose to publish a dashboard to a particular resource group.</span></span>  <span data-ttu-id="23c8f-159">該儀表板的存取控制與資源群組的存取控制相符。</span><span class="sxs-lookup"><span data-stu-id="23c8f-159">The access control for that dashboard matches the access control for the resource group.</span></span>  <span data-ttu-id="23c8f-160">可以管理該資源群組中資源的使用者也可以存取儀表板。</span><span class="sxs-lookup"><span data-stu-id="23c8f-160">Users that can manage the resources in that resource group also have access to the dashboards.</span></span>

![將儀表板發佈至資源群組](./media/azure-portal-dashboards/publish-to-resource-group.png)

<span data-ttu-id="23c8f-162">儀表板發佈之後，[共用 + 存取控制]  窗格便會重新整理，並顯示所發佈儀表板的相關資訊，包括用以管理儀表板使用者存取權的連結。</span><span class="sxs-lookup"><span data-stu-id="23c8f-162">After your dashboard is published, the **Sharing + access** control pane will refresh and show you information about the published dashboard, including a link to manage user access to the dashboard.</span></span>  <span data-ttu-id="23c8f-163">此連結會啟動用來管理任何 Azure 資源存取權的標準角色型存取控制刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="23c8f-163">This link launches the standard Role Based Access Control blade used to manage access for any Azure resource.</span></span>  <span data-ttu-id="23c8f-164">您隨時都可以透過選取 [共用] 來回到此檢視。</span><span class="sxs-lookup"><span data-stu-id="23c8f-164">You can always get back to this view by selecting **Share**.</span></span>

![管理存取控制](./media/azure-portal-dashboards/manage-access.png)

## <a name="next-steps"></a><span data-ttu-id="23c8f-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="23c8f-166">Next steps</span></span>
* <span data-ttu-id="23c8f-167">若要管理資源，請參閱 [透過入口網站管理 Azure 資源](../azure-resource-manager/resource-group-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="23c8f-167">To manage resources, see [Manage Azure resources through portal](../azure-resource-manager/resource-group-portal.md).</span></span>
* <span data-ttu-id="23c8f-168">若要部署資源，請參閱 [使用 Resource Manager 範本與 Azure 入口網站來部署資源](../azure-resource-manager/resource-group-template-deploy-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="23c8f-168">To deploy resources, see [Deploy resources with Resource Manager templates and Azure portal](../azure-resource-manager/resource-group-template-deploy-portal.md).</span></span>

