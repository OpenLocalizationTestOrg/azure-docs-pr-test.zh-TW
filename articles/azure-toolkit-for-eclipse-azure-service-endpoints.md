---
title: "aaaAzure 服務端點"
description: "描述在 hello Azure Toolkit for Eclipse 中的 hello Azure 服務端點設定。"
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
ms.openlocfilehash: 357aa56409a894719077f2c8f302575c8ebb6883
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-endpoints"></a><span data-ttu-id="26b16-103">Azure 服務端點</span><span class="sxs-lookup"><span data-stu-id="26b16-103">Azure Service Endpoints</span></span>
<span data-ttu-id="26b16-104">Azure 服務端點會判斷您的應用程式是否已部署的 tooand hello 全域 Azure 平台所管理，Azure 由 21Vianet in China 或私人 Azure 平台運作。</span><span class="sxs-lookup"><span data-stu-id="26b16-104">Azure service endpoints determine whether your application is deployed tooand managed by hello global Azure platform, Azure operated by 21Vianet in China, or a private Azure platform.</span></span> <span data-ttu-id="26b16-105">hello**服務端點**對話方塊可讓您的服務端點想 toouse toospecify。</span><span class="sxs-lookup"><span data-stu-id="26b16-105">hello **Service Endpoints** dialog allows you toospecify which service endpoints you want toouse.</span></span> <span data-ttu-id="26b16-106">tooopen hello**服務端點**對話方塊中的，在 Eclipse 中，按一下**視窗**，按一下 **喜好設定**，依序展開**Azure**，然後按一下**服務端點**。</span><span class="sxs-lookup"><span data-stu-id="26b16-106">tooopen hello **Service Endpoints** dialog, within Eclipse, click **Window**, click **Preferences**, expand **Azure**, and then click **Service Endpoints**.</span></span> <span data-ttu-id="26b16-107">設定 hello**作用中設定**欄位會決定目前的工作區中的哪一種 Azure 服務端點會用於 hello Azure 專案。</span><span class="sxs-lookup"><span data-stu-id="26b16-107">Setting hello **Active Set** field determines which Azure service endpoints will be used for hello Azure projects in your current workspace.</span></span>

<span data-ttu-id="26b16-108">hello 下列範例示範 hello**服務端點**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="26b16-108">hello following shows hello **Service Endpoints** dialog.</span></span>

![][ic719493]

## <a name="tooset-hello-service-endpoints"></a><span data-ttu-id="26b16-109">tooset hello 服務端點</span><span class="sxs-lookup"><span data-stu-id="26b16-109">tooset hello service endpoints</span></span>
<span data-ttu-id="26b16-110">在 hello**服務端點**對話方塊中，下列動作的 hello 的其中一個執行：</span><span class="sxs-lookup"><span data-stu-id="26b16-110">In hello **Service Endpoints** dialog, take one of hello following actions:</span></span>

* <span data-ttu-id="26b16-111">如果您想 toouse hello 全域 Azure 平台，從 hello**作用中設定**下拉式清單中選取**windowsazure.com**按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="26b16-111">If you want toouse hello global Azure platform, from hello **Active Set** dropdown list, select **windowsazure.com** and click **OK**.</span></span>

* <span data-ttu-id="26b16-112">如果您想的 toouse Azure 由 21Vianet in China 從 hello 運作**作用中設定**下拉式清單中選取**windowsazure.cn （中國）**按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="26b16-112">If you want toouse Azure operated by 21Vianet in China, from hello **Active Set** dropdown list, select **windowsazure.cn (China)** and click **OK**.</span></span>

* <span data-ttu-id="26b16-113">如果您想 toouse 私人 Azure 平台：</span><span class="sxs-lookup"><span data-stu-id="26b16-113">If you want toouse a private Azure platform:</span></span>

  1. <span data-ttu-id="26b16-114">按一下 [ **編輯**]。</span><span class="sxs-lookup"><span data-stu-id="26b16-114">Click **Edit**.</span></span>

  2. <span data-ttu-id="26b16-115">會開啟一個對話方塊，通知您該 hello**服務端點**會關閉對話方塊，並將開啟 hello 喜好設定設定檔。</span><span class="sxs-lookup"><span data-stu-id="26b16-115">A dialog box opens, informing you that hello **Service Endpoints** dialog will be closed, and hello preference sets file will be opened.</span></span> <span data-ttu-id="26b16-116">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="26b16-116">Click **OK**.</span></span>

  3. <span data-ttu-id="26b16-117">在 hello preferencesets.xml 檔案中，建立新`preferenceset`項目。</span><span class="sxs-lookup"><span data-stu-id="26b16-117">In hello preferencesets.xml file, create a new `preferenceset` element.</span></span> <span data-ttu-id="26b16-118">這個新的項目，對於建立`name`， `blob`， `management`，`portalURL`和`publishsettings`屬性，然後新增其對應 tooyour 私人 Azure 平台的值。</span><span class="sxs-lookup"><span data-stu-id="26b16-118">For this new element, create `name`, `blob`, `management`, `portalURL` and `publishsettings` attributes, and add values for them that correspond tooyour private Azure platform.</span></span> <span data-ttu-id="26b16-119">您可以使用 hello 值提供給現有的 hello`preferenceset`做為範本的項目。</span><span class="sxs-lookup"><span data-stu-id="26b16-119">You can use hello values provided for hello existing `preferenceset` elements as templates.</span></span> <span data-ttu-id="26b16-120">**請注意**: hello 值為 hello`blob`屬性必須包含"blob"hello URL 中的 hello 文字。</span><span class="sxs-lookup"><span data-stu-id="26b16-120">**Note**: hello value used for hello `blob` attribute must contain hello text "blob" in hello URL.</span></span>

  4. <span data-ttu-id="26b16-121">儲存並關閉 preferencesets.xml。</span><span class="sxs-lookup"><span data-stu-id="26b16-121">Save and close preferencesets.xml.</span></span>

  5. <span data-ttu-id="26b16-122">重新開啟 hello**服務端點**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="26b16-122">Reopen hello **Service Endpoints** dialog.</span></span>

  6. <span data-ttu-id="26b16-123">從 hello**作用中設定**下拉式清單中，選取 hello 作用中設定您建立，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="26b16-123">From hello **Active Set** dropdown list, select hello active set that you created and click **OK**.</span></span>

  7. <span data-ttu-id="26b16-124">一旦您已建立私人 Azure 平台`preferenceset`項目，您可以按一下 hello 變更 hello 指派值 tooit**編輯**按鈕在 hello**服務端點**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="26b16-124">Once you've created your private Azure platform `preferenceset` element, you can change hello values assigned tooit by clicking hello **Edit** button in hello **Services Endpoint** dialog.</span></span> <span data-ttu-id="26b16-125">如有需要，也可以建立多個私人 Azure 平台 `preferenceset` 元素。</span><span class="sxs-lookup"><span data-stu-id="26b16-125">You can also create multiple private Azure platform `preferenceset` elements, if you desire.</span></span>

## <a name="see-also"></a><span data-ttu-id="26b16-126">另請參閱</span><span class="sxs-lookup"><span data-stu-id="26b16-126">See Also</span></span>
<span data-ttu-id="26b16-127">[適用於 Eclipse 的 Azure 工具組][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="26b16-127">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="26b16-128">[安裝 Azure Toolkit for Eclipse hello][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="26b16-128">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="26b16-129">[在 Eclipse 中為 Azure 建立 Hello World 應用程式][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="26b16-129">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="26b16-130">如需有關使用 Azure 與 Java 的詳細資訊，請參閱 hello [Azure Java 開發人員中心][Azure Java Developer Center]。</span><span class="sxs-lookup"><span data-stu-id="26b16-130">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719493]: ./media/azure-toolkit-for-eclipse-azure-service-endpoints/ic719493.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268600.aspx -->
