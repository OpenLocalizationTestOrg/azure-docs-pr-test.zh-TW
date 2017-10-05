---
title: "使用雲端總管管理 Azure 資源 | Microsoft Docs"
description: "了解如何在 Visual Studio 內使用 [雲端總管] 瀏覽和管理 Azure 資源。"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 6347dc53-f497-49d5-b29b-e8b9f0e939d7
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/25/2017
ms.author: kraigb
ms.openlocfilehash: 6e6d8d559f0251b71bfa6d529ead82a246cb3235
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="manage-the-resources-associated-with-your-azure-accounts-in-visual-studio-cloud-explorer"></a><span data-ttu-id="a1949-103">在 Visual Studio Cloud Explorer 中管理與 Azure 帳戶關聯的資源</span><span class="sxs-lookup"><span data-stu-id="a1949-103">Manage the resources associated with your Azure accounts in Visual Studio Cloud Explorer</span></span>
<span data-ttu-id="a1949-104">Cloud Explorer 可讓您從 Visual Studio 內檢視您的 Azure 資源和資源群組、檢查其屬性，以及執行重要的開發人員診斷動作。</span><span class="sxs-lookup"><span data-stu-id="a1949-104">Cloud Explorer enables you to view your Azure resources and resource groups, inspect their properties, and perform key developer diagnostics actions from within Visual Studio.</span></span> 

<span data-ttu-id="a1949-105">與 [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)相同，Cloud Explorer 也是建立在 Azure Resource Manager 堆疊的基礎上。</span><span class="sxs-lookup"><span data-stu-id="a1949-105">Like the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), Cloud Explorer is built on the Azure Resource Manager stack.</span></span> <span data-ttu-id="a1949-106">因此，Cloud Explorer 了解 Azure 資源群組之類的資源，以及邏輯應用程式和 API 應用程式之類的 Azure 服務，並且支援[角色型存取控制](active-directory/role-based-access-control-configure.md) (RBAC)。</span><span class="sxs-lookup"><span data-stu-id="a1949-106">Therefore, Cloud Explorer understands resources such as Azure resource groups and Azure services such as Logic apps and API apps, and it supports [role-based access control](active-directory/role-based-access-control-configure.md) (RBAC).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a1949-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="a1949-107">Prerequisites</span></span>
- <span data-ttu-id="a1949-108">已選取「Azure 工作負載」的 [Visual Studio 2017](https://www.visualstudio.com/downloads/)，或是具備 [Microsoft Azure SDK for .NET 2.9](https://www.microsoft.com/en-us/download/details.aspx?id=51657) 的舊版 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="a1949-108">[Visual Studio 2017](https://www.visualstudio.com/downloads/) with the **Azure workload** selected, or an earlier version of Visual Studio with the [Microsoft Azure SDK for .NET 2.9](https://www.microsoft.com/en-us/download/details.aspx?id=51657).</span></span>
- <span data-ttu-id="a1949-109">Microsoft Azure 帳戶 - 如果您沒有帳戶，您可以[申請免費試用](http://go.microsoft.com/fwlink/?LinkId=623901)，或是[啟用您的 Visual Studio 訂閱者權益](http://go.microsoft.com/fwlink/?LinkId=623901)。</span><span class="sxs-lookup"><span data-stu-id="a1949-109">Microsoft Azure account - If you don't have an account, you can [sign up for a free trial](http://go.microsoft.com/fwlink/?LinkId=623901) or [activate your Visual Studio subscriber benefits](http://go.microsoft.com/fwlink/?LinkId=623901).</span></span>

> [!NOTE]
> <span data-ttu-id="a1949-110">若要檢視 Cloud Explorer，請在功能表列上，選取 [檢視] > [Cloud Explorer]。</span><span class="sxs-lookup"><span data-stu-id="a1949-110">To view Cloud Explorer, select **View** > **Cloud Explorer** on the menu bar.</span></span>   
> 
> 

## <a name="add-an-azure-account-to-cloud-explorer"></a><span data-ttu-id="a1949-111">將 Azure 帳戶新增到 Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="a1949-111">Add an Azure account to Cloud Explorer</span></span>
<span data-ttu-id="a1949-112">若要檢視與 Azure 帳戶關聯的資源，您必須先將帳戶新增到 Cloud Explorer。</span><span class="sxs-lookup"><span data-stu-id="a1949-112">To view the resources associated with an Azure account, you must first add the account to Cloud Explorer.</span></span> 

1. <span data-ttu-id="a1949-113">在 [Cloud Explorer] 中，選取 [Azure 帳戶設定]。</span><span class="sxs-lookup"><span data-stu-id="a1949-113">In **Cloud Explorer**, select **Azure account settings**.</span></span>

    ![Cloud Explorer 的 [Azure 帳戶設定] 圖示](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. <span data-ttu-id="a1949-115">選取 [新增帳戶]。</span><span class="sxs-lookup"><span data-stu-id="a1949-115">Select **Add new account**.</span></span> 

    ![Cloud Explorer 的 [新增帳戶] 連結](media/vs-azure-tools-resources-managing-with-cloud-explorer/add-account-link.png)

1. <span data-ttu-id="a1949-117">登入您想要瀏覽資源的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a1949-117">Log in to the Azure account whose resources you want to browse.</span></span> 

1. <span data-ttu-id="a1949-118">登入 Azure 帳戶之後，系統就會顯示與該帳戶關聯的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="a1949-118">Once logged in to an Azure account, the subscriptions associated with that account display.</span></span> <span data-ttu-id="a1949-119">選取您想要瀏覽之帳戶訂用帳戶的核取方塊，然後選取 [套用]。</span><span class="sxs-lookup"><span data-stu-id="a1949-119">Select the check boxes for the account subscriptions you want to browse and then select **Apply**.</span></span> 
 
    ![Cloud Explorer：選取要顯示的 Azure 帳戶](media/vs-azure-tools-resources-managing-with-cloud-explorer/select-subscriptions.png)

1. <span data-ttu-id="a1949-121">選取您想要瀏覽資源的訂用帳戶之後，Cloud Explorer 中就會顯示這些訂用帳戶和資源。</span><span class="sxs-lookup"><span data-stu-id="a1949-121">After selecting the subscriptions whose resources you want to browse, those subscriptions and resources display in the Cloud Explorer.</span></span>

    ![Cloud Explorer 的 Azure 帳戶資源清單](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-listed.png)

## <a name="remove-an-azure-account-from-cloud-explorer"></a><span data-ttu-id="a1949-123">從 Cloud Explorer 中移除 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="a1949-123">Remove an Azure account from Cloud Explorer</span></span> 

1. <span data-ttu-id="a1949-124">在 [Cloud Explorer] 中，選取 [Azure 帳戶設定]。</span><span class="sxs-lookup"><span data-stu-id="a1949-124">In **Cloud Explorer**, select **Azure account settings**.</span></span>

    ![Cloud Explorer 的 [Azure 帳戶設定] 圖示](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. <span data-ttu-id="a1949-126">在您想要移除的帳戶旁邊，選取 [移除]。</span><span class="sxs-lookup"><span data-stu-id="a1949-126">Next to the account you want to remove, select **Remove**.</span></span>

    ![Cloud Explorer 的 [Azure 帳戶設定] 圖示](media/vs-azure-tools-resources-managing-with-cloud-explorer/remove-account.png)

## <a name="view-resource-types-or-resource-groups"></a><span data-ttu-id="a1949-128">檢視資源類型或資源群組</span><span class="sxs-lookup"><span data-stu-id="a1949-128">View resource types or resource groups</span></span>
<span data-ttu-id="a1949-129">若要檢視您的 Azure 資源，您可以選擇 [資源類型] 或 [資源群組] 檢視。</span><span class="sxs-lookup"><span data-stu-id="a1949-129">To view your Azure resources, you can choose either **Resource Types** or **Resource Groups** view.</span></span>

1. <span data-ttu-id="a1949-130">在 [Cloud Explorer] 中，選取資源檢視下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="a1949-130">In **Cloud Explorer**, select the resource view dropdown.</span></span>

    ![可供選取所需資源檢視的 Cloud Explorer 下拉式清單](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-view-dropdown.png)

1. <span data-ttu-id="a1949-132">從操作功能表中，選取所需的檢視：</span><span class="sxs-lookup"><span data-stu-id="a1949-132">From the context menu, select the desired view:</span></span> 

    - <span data-ttu-id="a1949-133">[資源類型] 檢視 - 在 [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)上使用的一般檢視，此檢視會依資源的類型 (例如 Web 應用程式、儲存體帳戶及虛擬機器) 分類來顯示 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="a1949-133">**Resource Types** view - The common view used on the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), shows your Azure resources categorized by their type, such as web apps, storage accounts, and virtual machines.</span></span> 
    - <span data-ttu-id="a1949-134">[資源群組] 檢視 - 將 Azure 資源依關聯的 Azure 資源群組進行分類。</span><span class="sxs-lookup"><span data-stu-id="a1949-134">**Resource Groups** view - Categorizes Azure resources by the Azure resource group with which they're associated.</span></span> <span data-ttu-id="a1949-135">資源群組是通常由特定應用程式使用的 Azure 資源組合。</span><span class="sxs-lookup"><span data-stu-id="a1949-135">A resource group is a bundle of Azure resources, typically used by a specific application.</span></span> <span data-ttu-id="a1949-136">若要深入了解 Azure 資源群組，請參閱 [Azure Resource Manager 概觀](./azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="a1949-136">To learn more about Azure resource groups, see [Azure Resource Manager Overview](./azure-resource-manager/resource-group-overview.md).</span></span>

    <span data-ttu-id="a1949-137">下圖顯示這兩種資源檢視的比較：</span><span class="sxs-lookup"><span data-stu-id="a1949-137">The following image shows a comparison of the two resource views:</span></span>

    ![Cloud Explorer 資源檢視比較](media/vs-azure-tools-resources-managing-with-cloud-explorer/resource-views-comparison.png)

## <a name="view-and-navigate-resources-in-cloud-explorer"></a><span data-ttu-id="a1949-139">在 Cloud Explorer 中檢視和瀏覽資源</span><span class="sxs-lookup"><span data-stu-id="a1949-139">View and navigate resources in Cloud Explorer</span></span>
<span data-ttu-id="a1949-140">若要在 Cloud Explorer 中瀏覽至 Azure 資源並檢視其資訊，請展開項目的類型或關聯的資源群組，然後選取資源。</span><span class="sxs-lookup"><span data-stu-id="a1949-140">To navigate to an Azure resource and view its information in Cloud Explorer, expand the item's type or associated resource group and then select the resource.</span></span> <span data-ttu-id="a1949-141">當您選取資源時，Cloud Explorer 底部的 [動作] 和 [屬性] 這兩個索引標籤中會顯示資訊。</span><span class="sxs-lookup"><span data-stu-id="a1949-141">When you select a resource, information appears in the two tabs - **Actions** and **Properties** - at the bottom of Cloud Explorer.</span></span> 

- <span data-ttu-id="a1949-142">[動作] 索引標籤 - 列出您可以在 Cloud Explorer 中針對所選資源採取的動作。</span><span class="sxs-lookup"><span data-stu-id="a1949-142">**Actions** tab - Lists the actions you can take in Cloud Explorer for the selected resource.</span></span> <span data-ttu-id="a1949-143">您也可以在資源上按一下滑鼠右鍵來檢視其操作功能表，以檢視這些選項。</span><span class="sxs-lookup"><span data-stu-id="a1949-143">You can also view these options by right-clicking the resource to view its context menu.</span></span>

- <span data-ttu-id="a1949-144">[屬性]  索引標籤 - 顯示資源的屬性，例如其類型、地區設定及關聯的資源群組。</span><span class="sxs-lookup"><span data-stu-id="a1949-144">**Properties** tab - Shows the properties of the resource, such as its type, locale, and resource group with which it is associated.</span></span>

<span data-ttu-id="a1949-145">下圖顯示您在 App Service 的各個索引標籤上所看到畫面的範例比較：</span><span class="sxs-lookup"><span data-stu-id="a1949-145">The following image shows an example comparison of what you see on each tab for an App Service:</span></span>

![](./media/vs-azure-tools-resources-managing-with-cloud-explorer/actions-and-properties.png)

<span data-ttu-id="a1949-146">每個資源都有 [在入口網站中開啟] 這個動作。</span><span class="sxs-lookup"><span data-stu-id="a1949-146">Every resource has the action **Open in portal**.</span></span> <span data-ttu-id="a1949-147">當您選擇此動作時，[雲端總管] 會在 [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)中顯示選取的資源。</span><span class="sxs-lookup"><span data-stu-id="a1949-147">When you choose this action, Cloud Explorer displays the selected resource in the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span> <span data-ttu-id="a1949-148">[在入口網站中開啟] 功能可方便您瀏覽至位於深層巢狀結構中的資源。</span><span class="sxs-lookup"><span data-stu-id="a1949-148">The **Open in portal** feature is handy for navigating to deeply nested resources.</span></span>

<span data-ttu-id="a1949-149">根據 Azure 資源而定，也可能出現其他動作和屬性值。</span><span class="sxs-lookup"><span data-stu-id="a1949-149">Additional actions and property values may also appear based on the Azure resource.</span></span> <span data-ttu-id="a1949-150">例如，除了 [在入口網站中開啟]，Web 應用程式和邏輯應用程式也有 [在瀏覽器中開啟] 和 [附加偵錯工具] 動作。</span><span class="sxs-lookup"><span data-stu-id="a1949-150">For example, web apps and logic apps also have the actions **Open in browser** and **Attach debugger** in addition to **Open in portal**.</span></span> <span data-ttu-id="a1949-151">當您選擇儲存體帳戶 blob、佇列或資料表時，將會出現開啟編輯器的動作。</span><span class="sxs-lookup"><span data-stu-id="a1949-151">Actions to open editors appear when you choose a storage account blob, queue, or table.</span></span> <span data-ttu-id="a1949-152">Azure 應用程式具有 **URL** 和 **狀態**屬性，而儲存體資源具有索引鍵和連接字串屬性。</span><span class="sxs-lookup"><span data-stu-id="a1949-152">Azure apps have **URL** and **Status** properties, while storage resources have key and connection string properties.</span></span>

## <a name="find-resources-in-cloud-explorer"></a><span data-ttu-id="a1949-153">在 Cloud Explorer 中尋找資源</span><span class="sxs-lookup"><span data-stu-id="a1949-153">Find resources in Cloud Explorer</span></span>
<span data-ttu-id="a1949-154">若要在 Azure 帳戶訂用帳戶中尋找具有特定名稱的資源，請在 Cloud Explorer 的 [搜尋] 方塊中輸入名稱。</span><span class="sxs-lookup"><span data-stu-id="a1949-154">To locate resources with a specific name in your Azure account subscriptions, enter the name in the **Search** box in Cloud Explorer.</span></span>

![在 [雲端總管] 中尋找資源](./media/vs-azure-tools-resources-managing-with-cloud-explorer/search-for-resources.png)

<span data-ttu-id="a1949-156">當您在 [搜尋] 方塊中輸入字元時，只有符合這些字元的資源才會出現在資源樹狀目錄中。</span><span class="sxs-lookup"><span data-stu-id="a1949-156">As you enter characters in the **Search** box, only resources that match those characters appear in the resource tree.</span></span>
