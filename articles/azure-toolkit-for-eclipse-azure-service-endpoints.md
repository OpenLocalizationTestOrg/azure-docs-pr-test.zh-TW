---
title: "Azure 服務端點"
description: "說明適用於 Eclipse 的 Azure 工具組中 Azure 服務端點的設定。"
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9c6125ec-7278-461e-b69c-ed56e844f742
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 6059c292c2687f1bf3d9be04c03aaaaf6adde945
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-service-endpoints"></a><span data-ttu-id="602dd-103">Azure 服務端點</span><span class="sxs-lookup"><span data-stu-id="602dd-103">Azure Service Endpoints</span></span>
<span data-ttu-id="602dd-104">Azure 服務端點會判斷您的應用程式是否已部署至全域 Azure 平台並由該平台管理，Azure 由位於中國的 21Vianet 或私人 Azure 平台運作。</span><span class="sxs-lookup"><span data-stu-id="602dd-104">Azure service endpoints determine whether your application is deployed to and managed by the global Azure platform, Azure operated by 21Vianet in China, or a private Azure platform.</span></span> <span data-ttu-id="602dd-105">[ **服務端點** ] 對話方塊可讓您指定要使用的服務端點。</span><span class="sxs-lookup"><span data-stu-id="602dd-105">The **Service Endpoints** dialog allows you to specify which service endpoints you want to use.</span></span> <span data-ttu-id="602dd-106">若要在 Eclipse 中開啟 [服務端點] 對話方塊，請依序按一下 [視窗]、[喜好設定]，展開 [Azure]，然後按一下 [服務端點]。</span><span class="sxs-lookup"><span data-stu-id="602dd-106">To open the **Service Endpoints** dialog, within Eclipse, click **Window**, click **Preferences**, expand **Azure**, and then click **Service Endpoints**.</span></span> <span data-ttu-id="602dd-107">設定 [ **作用中設定** ] 欄位，可決定您目前工作區中的 Azure 專案將使用的 Azure 服務端點。</span><span class="sxs-lookup"><span data-stu-id="602dd-107">Setting the **Active Set** field determines which Azure service endpoints will be used for the Azure projects in your current workspace.</span></span>

<span data-ttu-id="602dd-108">[ **服務端點** ] 對話方塊如下顯示。</span><span class="sxs-lookup"><span data-stu-id="602dd-108">The following shows the **Service Endpoints** dialog.</span></span>

![][ic719493]

## <a name="to-set-the-service-endpoints"></a><span data-ttu-id="602dd-109">設定服務端點</span><span class="sxs-lookup"><span data-stu-id="602dd-109">To set the service endpoints</span></span>
<span data-ttu-id="602dd-110">在 [ **服務端點** ] 對話方塊中，執行下列其中一個動作：</span><span class="sxs-lookup"><span data-stu-id="602dd-110">In the **Service Endpoints** dialog, take one of the following actions:</span></span>

* <span data-ttu-id="602dd-111">如果想使用全域 Azure 平台，請從 [作用中設定] 下拉式清單中，選取 [windowsazure.com]，並按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="602dd-111">If you want to use the global Azure platform, from the **Active Set** dropdown list, select **windowsazure.com** and click **OK**.</span></span>

* <span data-ttu-id="602dd-112">如果想使用由位於中國的 21Vianet 所運作的 Azure，請從 [作用中設定] 下拉式清單中，選取 [windowsazure.cn (中國)]，並按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="602dd-112">If you want to use Azure operated by 21Vianet in China, from the **Active Set** dropdown list, select **windowsazure.cn (China)** and click **OK**.</span></span>

* <span data-ttu-id="602dd-113">如果想使用私人 Azure 平台：</span><span class="sxs-lookup"><span data-stu-id="602dd-113">If you want to use a private Azure platform:</span></span>

  1. <span data-ttu-id="602dd-114">按一下 [ **編輯**]。</span><span class="sxs-lookup"><span data-stu-id="602dd-114">Click **Edit**.</span></span>

  2. <span data-ttu-id="602dd-115">隨即會開啟一個對話方塊，告知您 [ **服務端點** ] 對話方塊將關閉，喜好設定檔案將開啟。</span><span class="sxs-lookup"><span data-stu-id="602dd-115">A dialog box opens, informing you that the **Service Endpoints** dialog will be closed, and the preference sets file will be opened.</span></span> <span data-ttu-id="602dd-116">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="602dd-116">Click **OK**.</span></span>

  3. <span data-ttu-id="602dd-117">在 preferencesets.xml 檔案中，建立新的 `preferenceset` 元素。</span><span class="sxs-lookup"><span data-stu-id="602dd-117">In the preferencesets.xml file, create a new `preferenceset` element.</span></span> <span data-ttu-id="602dd-118">針對此新元素，建立 `name`、`blob`、`management`、`portalURL` 和 `publishsettings` 屬性，再為其新增對應至私人 Azure 平台的值。</span><span class="sxs-lookup"><span data-stu-id="602dd-118">For this new element, create `name`, `blob`, `management`, `portalURL` and `publishsettings` attributes, and add values for them that correspond to your private Azure platform.</span></span> <span data-ttu-id="602dd-119">您可使用為現有 `preferenceset` 元素所提供的值作為範本。</span><span class="sxs-lookup"><span data-stu-id="602dd-119">You can use the values provided for the existing `preferenceset` elements as templates.</span></span> <span data-ttu-id="602dd-120">**注意**：用於 `blob` 屬性的值必須在 URL 中包含 "blob" 文字。</span><span class="sxs-lookup"><span data-stu-id="602dd-120">**Note**: The value used for the `blob` attribute must contain the text "blob" in the URL.</span></span>

  4. <span data-ttu-id="602dd-121">儲存並關閉 preferencesets.xml。</span><span class="sxs-lookup"><span data-stu-id="602dd-121">Save and close preferencesets.xml.</span></span>

  5. <span data-ttu-id="602dd-122">重新開啟 [ **服務端點** ] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="602dd-122">Reopen the **Service Endpoints** dialog.</span></span>

  6. <span data-ttu-id="602dd-123">從 [作用中設定] 下拉式清單中，選取您建立的作用中設定，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="602dd-123">From the **Active Set** dropdown list, select the active set that you created and click **OK**.</span></span>

  7. <span data-ttu-id="602dd-124">建立私人 Azure 平台 `preferenceset` 元素後，您可以按一下 [服務端點] 對話方塊中的 [編輯] 按鈕，變更指派給該元素的值。</span><span class="sxs-lookup"><span data-stu-id="602dd-124">Once you've created your private Azure platform `preferenceset` element, you can change the values assigned to it by clicking the **Edit** button in the **Services Endpoint** dialog.</span></span> <span data-ttu-id="602dd-125">如有需要，也可以建立多個私人 Azure 平台 `preferenceset` 元素。</span><span class="sxs-lookup"><span data-stu-id="602dd-125">You can also create multiple private Azure platform `preferenceset` elements, if you desire.</span></span>

## <a name="see-also"></a><span data-ttu-id="602dd-126">另請參閱</span><span class="sxs-lookup"><span data-stu-id="602dd-126">See Also</span></span>
<span data-ttu-id="602dd-127">[適用於 Eclipse 的 Azure 工具組][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="602dd-127">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="602dd-128">[安裝適用於 Eclipse 的 Azure 工具組][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="602dd-128">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="602dd-129">[在 Eclipse 中為 Azure 建立 Hello World 應用程式][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="602dd-129">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="602dd-130">如需有關如何搭配使用 Azure 與 Java 的詳細資訊，請參閱 [Azure Java 開發人員中心][Azure Java Developer Center]。</span><span class="sxs-lookup"><span data-stu-id="602dd-130">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719493]: ./media/azure-toolkit-for-eclipse-azure-service-endpoints/ic719493.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268600.aspx -->
