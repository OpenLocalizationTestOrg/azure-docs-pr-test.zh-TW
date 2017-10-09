---
title: "aaaManaging Azure 資源的 Cloud Explorer |Microsoft 文件"
description: "深入了解如何 toouse Cloud Explorer toobrowse 及管理 Visual Studio 中的 Azure 資源。"
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
ms.openlocfilehash: 8a81660074d5d04be063df9e25076b7a97586514
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-resources-associated-with-your-azure-accounts-in-visual-studio-cloud-explorer"></a><span data-ttu-id="f4121-103">管理與您在 Visual Studio Cloud Explorer 中的 Azure 帳戶相關聯的 hello 資源</span><span class="sxs-lookup"><span data-stu-id="f4121-103">Manage hello resources associated with your Azure accounts in Visual Studio Cloud Explorer</span></span>
<span data-ttu-id="f4121-104">Cloud Explorer 可讓您 tooview 您的 Azure 資源，資源群組，請檢查其屬性，並執行從 Visual Studio 中的索引鍵的開發人員診斷動作。</span><span class="sxs-lookup"><span data-stu-id="f4121-104">Cloud Explorer enables you tooview your Azure resources and resource groups, inspect their properties, and perform key developer diagnostics actions from within Visual Studio.</span></span> 

<span data-ttu-id="f4121-105">像 hello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)，Cloud Explorer 建置在 hello Azure Resource Manager 堆疊。</span><span class="sxs-lookup"><span data-stu-id="f4121-105">Like hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), Cloud Explorer is built on hello Azure Resource Manager stack.</span></span> <span data-ttu-id="f4121-106">因此，Cloud Explorer 了解 Azure 資源群組之類的資源，以及邏輯應用程式和 API 應用程式之類的 Azure 服務，並且支援[角色型存取控制](active-directory/role-based-access-control-configure.md) (RBAC)。</span><span class="sxs-lookup"><span data-stu-id="f4121-106">Therefore, Cloud Explorer understands resources such as Azure resource groups and Azure services such as Logic apps and API apps, and it supports [role-based access control](active-directory/role-based-access-control-configure.md) (RBAC).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f4121-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="f4121-107">Prerequisites</span></span>
- <span data-ttu-id="f4121-108">[Visual Studio 2017](https://www.visualstudio.com/downloads/)以 hello **Azure 的工作負載**選取，或更早版本的 Visual Studio 以 hello [Microsoft Azure SDK for.NET 2.9](https://www.microsoft.com/en-us/download/details.aspx?id=51657)。</span><span class="sxs-lookup"><span data-stu-id="f4121-108">[Visual Studio 2017](https://www.visualstudio.com/downloads/) with hello **Azure workload** selected, or an earlier version of Visual Studio with hello [Microsoft Azure SDK for .NET 2.9](https://www.microsoft.com/en-us/download/details.aspx?id=51657).</span></span>
- <span data-ttu-id="f4121-109">Microsoft Azure 帳戶 - 如果您沒有帳戶，您可以[申請免費試用](http://go.microsoft.com/fwlink/?LinkId=623901)，或是[啟用您的 Visual Studio 訂閱者權益](http://go.microsoft.com/fwlink/?LinkId=623901)。</span><span class="sxs-lookup"><span data-stu-id="f4121-109">Microsoft Azure account - If you don't have an account, you can [sign up for a free trial](http://go.microsoft.com/fwlink/?LinkId=623901) or [activate your Visual Studio subscriber benefits](http://go.microsoft.com/fwlink/?LinkId=623901).</span></span>

> [!NOTE]
> <span data-ttu-id="f4121-110">tooview Cloud Explorer 中，選取**檢視** > **Cloud Explorer** hello 功能表列上。</span><span class="sxs-lookup"><span data-stu-id="f4121-110">tooview Cloud Explorer, select **View** > **Cloud Explorer** on hello menu bar.</span></span>   
> 
> 

## <a name="add-an-azure-account-toocloud-explorer"></a><span data-ttu-id="f4121-111">新增 Azure 帳戶 tooCloud 總管</span><span class="sxs-lookup"><span data-stu-id="f4121-111">Add an Azure account tooCloud Explorer</span></span>
<span data-ttu-id="f4121-112">與 Azure 帳戶相關聯的 tooview hello 資源，您必須先新增 hello 帳戶 tooCloud 總管。</span><span class="sxs-lookup"><span data-stu-id="f4121-112">tooview hello resources associated with an Azure account, you must first add hello account tooCloud Explorer.</span></span> 

1. <span data-ttu-id="f4121-113">在 [Cloud Explorer] 中，選取 [Azure 帳戶設定]。</span><span class="sxs-lookup"><span data-stu-id="f4121-113">In **Cloud Explorer**, select **Azure account settings**.</span></span>

    ![Cloud Explorer 的 [Azure 帳戶設定] 圖示](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. <span data-ttu-id="f4121-115">選取 [新增帳戶]。</span><span class="sxs-lookup"><span data-stu-id="f4121-115">Select **Add new account**.</span></span> 

    ![Cloud Explorer 的 [新增帳戶] 連結](media/vs-azure-tools-resources-managing-with-cloud-explorer/add-account-link.png)

1. <span data-ttu-id="f4121-117">登入您想要將其資源的 Azure 帳戶 toohello toobrowse。</span><span class="sxs-lookup"><span data-stu-id="f4121-117">Log in toohello Azure account whose resources you want toobrowse.</span></span> 

1. <span data-ttu-id="f4121-118">登入 tooan Azure 帳戶之後，便會顯示 hello 與該帳戶相關聯的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f4121-118">Once logged in tooan Azure account, hello subscriptions associated with that account display.</span></span> <span data-ttu-id="f4121-119">選取 hello hello 帳戶訂閱您想 toobrowse，然後選取核取方塊**套用**。</span><span class="sxs-lookup"><span data-stu-id="f4121-119">Select hello check boxes for hello account subscriptions you want toobrowse and then select **Apply**.</span></span> 
 
    ![選取 Azure 訂用帳戶 toodisplay cloud Explorer:](media/vs-azure-tools-resources-managing-with-cloud-explorer/select-subscriptions.png)

1. <span data-ttu-id="f4121-121">選取您想要將其資源的 hello 訂閱之後 toobrowse 這些訂用帳戶或資源顯示 hello Cloud Explorer 中。</span><span class="sxs-lookup"><span data-stu-id="f4121-121">After selecting hello subscriptions whose resources you want toobrowse, those subscriptions and resources display in hello Cloud Explorer.</span></span>

    ![Cloud Explorer 的 Azure 帳戶資源清單](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-listed.png)

## <a name="remove-an-azure-account-from-cloud-explorer"></a><span data-ttu-id="f4121-123">從 Cloud Explorer 中移除 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="f4121-123">Remove an Azure account from Cloud Explorer</span></span> 

1. <span data-ttu-id="f4121-124">在 [Cloud Explorer] 中，選取 [Azure 帳戶設定]。</span><span class="sxs-lookup"><span data-stu-id="f4121-124">In **Cloud Explorer**, select **Azure account settings**.</span></span>

    ![Cloud Explorer 的 [Azure 帳戶設定] 圖示](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. <span data-ttu-id="f4121-126">選取您想要讓 tooremove 的下一個 toohello 帳戶**移除**。</span><span class="sxs-lookup"><span data-stu-id="f4121-126">Next toohello account you want tooremove, select **Remove**.</span></span>

    ![Cloud Explorer 的 [Azure 帳戶設定] 圖示](media/vs-azure-tools-resources-managing-with-cloud-explorer/remove-account.png)

## <a name="view-resource-types-or-resource-groups"></a><span data-ttu-id="f4121-128">檢視資源類型或資源群組</span><span class="sxs-lookup"><span data-stu-id="f4121-128">View resource types or resource groups</span></span>
<span data-ttu-id="f4121-129">tooview 您的 Azure 資源，您可以任選**資源類型**或**資源群組**檢視。</span><span class="sxs-lookup"><span data-stu-id="f4121-129">tooview your Azure resources, you can choose either **Resource Types** or **Resource Groups** view.</span></span>

1. <span data-ttu-id="f4121-130">在**Cloud Explorer**，選取 hello 資源檢視下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="f4121-130">In **Cloud Explorer**, select hello resource view dropdown.</span></span>

    ![Cloud Explorer 下拉式清單 tooselect hello 所需的資源檢視](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-view-dropdown.png)

1. <span data-ttu-id="f4121-132">Hello 內容功能表中選取所需的 hello 檢視：</span><span class="sxs-lookup"><span data-stu-id="f4121-132">From hello context menu, select hello desired view:</span></span> 

    - <span data-ttu-id="f4121-133">**資源類型**檢視-hello hello 上使用的一般檢視[Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)，顯示您分類依其類型，例如 web 應用程式、 儲存體帳戶和虛擬機器的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="f4121-133">**Resource Types** view - hello common view used on hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), shows your Azure resources categorized by their type, such as web apps, storage accounts, and virtual machines.</span></span> 
    - <span data-ttu-id="f4121-134">**資源群組**檢視-hello 與它們相關聯的 Azure 資源群組來分類的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="f4121-134">**Resource Groups** view - Categorizes Azure resources by hello Azure resource group with which they're associated.</span></span> <span data-ttu-id="f4121-135">資源群組是通常由特定應用程式使用的 Azure 資源組合。</span><span class="sxs-lookup"><span data-stu-id="f4121-135">A resource group is a bundle of Azure resources, typically used by a specific application.</span></span> <span data-ttu-id="f4121-136">toolearn 進一步了解 Azure 資源群組，請參閱[Azure 資源管理員概觀](./azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="f4121-136">toolearn more about Azure resource groups, see [Azure Resource Manager Overview](./azure-resource-manager/resource-group-overview.md).</span></span>

    <span data-ttu-id="f4121-137">hello 下列影像顯示 hello 比較兩個資源檢視：</span><span class="sxs-lookup"><span data-stu-id="f4121-137">hello following image shows a comparison of hello two resource views:</span></span>

    ![Cloud Explorer 資源檢視比較](media/vs-azure-tools-resources-managing-with-cloud-explorer/resource-views-comparison.png)

## <a name="view-and-navigate-resources-in-cloud-explorer"></a><span data-ttu-id="f4121-139">在 Cloud Explorer 中檢視和瀏覽資源</span><span class="sxs-lookup"><span data-stu-id="f4121-139">View and navigate resources in Cloud Explorer</span></span>
<span data-ttu-id="f4121-140">toonavigate tooan Azure 資源和檢視其資訊在 Cloud Explorer 中，展開 hello 項目的型別或相關聯的資源群組，然後選取 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="f4121-140">toonavigate tooan Azure resource and view its information in Cloud Explorer, expand hello item's type or associated resource group and then select hello resource.</span></span> <span data-ttu-id="f4121-141">當您選取的資源時，資訊會出現在 hello 兩個索引標籤後-**動作**和**屬性**-在 hello Cloud Explorer 底部。</span><span class="sxs-lookup"><span data-stu-id="f4121-141">When you select a resource, information appears in hello two tabs - **Actions** and **Properties** - at hello bottom of Cloud Explorer.</span></span> 

- <span data-ttu-id="f4121-142">**動作**索引標籤-清單 hello 之動作可以在 Cloud Explorer 中的 hello 選取資源。</span><span class="sxs-lookup"><span data-stu-id="f4121-142">**Actions** tab - Lists hello actions you can take in Cloud Explorer for hello selected resource.</span></span> <span data-ttu-id="f4121-143">您也可以檢視這些選項以滑鼠右鍵按一下 hello 資源 tooview 其操作功能表。</span><span class="sxs-lookup"><span data-stu-id="f4121-143">You can also view these options by right-clicking hello resource tooview its context menu.</span></span>

- <span data-ttu-id="f4121-144">**屬性**索引標籤-顯示 hello 屬性 hello 資源，例如其與相關聯的型別、 地區設定和資源群組。</span><span class="sxs-lookup"><span data-stu-id="f4121-144">**Properties** tab - Shows hello properties of hello resource, such as its type, locale, and resource group with which it is associated.</span></span>

<span data-ttu-id="f4121-145">hello 下列影像顯示的範例中比較您看到每個索引標籤上的應用程式服務：</span><span class="sxs-lookup"><span data-stu-id="f4121-145">hello following image shows an example comparison of what you see on each tab for an App Service:</span></span>

![](./media/vs-azure-tools-resources-managing-with-cloud-explorer/actions-and-properties.png)

<span data-ttu-id="f4121-146">每個資源都有 hello 動作**在入口網站中開啟**。</span><span class="sxs-lookup"><span data-stu-id="f4121-146">Every resource has hello action **Open in portal**.</span></span> <span data-ttu-id="f4121-147">當您選擇此動作時，Cloud Explorer 會顯示 hello 的 hello 選取資源[Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="f4121-147">When you choose this action, Cloud Explorer displays hello selected resource in hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span> <span data-ttu-id="f4121-148">hello**在入口網站中開啟**功能是很方便用來瀏覽 toodeeply 巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="f4121-148">hello **Open in portal** feature is handy for navigating toodeeply nested resources.</span></span>

<span data-ttu-id="f4121-149">其他動作和屬性值可能也會顯示根據 hello Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="f4121-149">Additional actions and property values may also appear based on hello Azure resource.</span></span> <span data-ttu-id="f4121-150">例如，web 應用程式和邏輯應用程式也有 hello 動作**瀏覽器中開啟**和**附加偵錯工具**此外太**在入口網站中開啟**。</span><span class="sxs-lookup"><span data-stu-id="f4121-150">For example, web apps and logic apps also have hello actions **Open in browser** and **Attach debugger** in addition too**Open in portal**.</span></span> <span data-ttu-id="f4121-151">當您選擇儲存體帳戶 blob、 佇列或資料表時，會出現動作 tooopen 編輯器。</span><span class="sxs-lookup"><span data-stu-id="f4121-151">Actions tooopen editors appear when you choose a storage account blob, queue, or table.</span></span> <span data-ttu-id="f4121-152">Azure 應用程式具有 **URL** 和 **狀態**屬性，而儲存體資源具有索引鍵和連接字串屬性。</span><span class="sxs-lookup"><span data-stu-id="f4121-152">Azure apps have **URL** and **Status** properties, while storage resources have key and connection string properties.</span></span>

## <a name="find-resources-in-cloud-explorer"></a><span data-ttu-id="f4121-153">在 Cloud Explorer 中尋找資源</span><span class="sxs-lookup"><span data-stu-id="f4121-153">Find resources in Cloud Explorer</span></span>
<span data-ttu-id="f4121-154">具有特定名稱在您的 Azure 帳戶的訂閱，toolocate 資源輸入 hello 名稱在 hello**搜尋**方塊在 Cloud Explorer 中。</span><span class="sxs-lookup"><span data-stu-id="f4121-154">toolocate resources with a specific name in your Azure account subscriptions, enter hello name in hello **Search** box in Cloud Explorer.</span></span>

![在 [雲端總管] 中尋找資源](./media/vs-azure-tools-resources-managing-with-cloud-explorer/search-for-resources.png)

<span data-ttu-id="f4121-156">當您輸入的字元在 hello**搜尋**hello 資源樹狀目錄中會出現的方塊中，比對這些字元的資源。</span><span class="sxs-lookup"><span data-stu-id="f4121-156">As you enter characters in hello **Search** box, only resources that match those characters appear in hello resource tree.</span></span>
