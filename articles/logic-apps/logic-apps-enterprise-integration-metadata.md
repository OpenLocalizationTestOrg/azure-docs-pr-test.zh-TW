---
title: "aaaManage 整合帳戶成品中繼資料-Azure 邏輯應用程式 |Microsoft 文件"
description: "從 Azure Logic Apps 的整合帳戶新增或擷取構件中繼資料"
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 11/21/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 8de71bffa9f9975d5409716b2208fa6c3a9545d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-artifact-metadata-in-integration-accounts-for-logic-apps"></a><span data-ttu-id="ddbb4-103">在 Logic Apps 的整合帳戶中管理構件中繼資料</span><span class="sxs-lookup"><span data-stu-id="ddbb4-103">Manage artifact metadata in integration accounts for logic apps</span></span>

<span data-ttu-id="ddbb4-104">您可以在整合帳戶中定義構件的自訂中繼資料，並在邏輯應用程式的執行階段期間擷取該中繼資料。</span><span class="sxs-lookup"><span data-stu-id="ddbb4-104">You can define custom metadata for artifacts in integration accounts and retrieve that metadata during runtime for your logic app.</span></span> <span data-ttu-id="ddbb4-105">例如，您可以指定構件的中繼資料，例如，合作夥伴、合約、結構描述及對應，這些全都會使用索引鍵值組來儲存中繼資料。</span><span class="sxs-lookup"><span data-stu-id="ddbb4-105">For example, you can specify metadata for artifacts like partners, agreements, schemas, and maps - all store metadata using key-value pairs.</span></span> <span data-ttu-id="ddbb4-106">目前，成品無法建立中繼資料透過 UI，但您可以使用 REST Api toocreate 中繼資料。</span><span class="sxs-lookup"><span data-stu-id="ddbb4-106">Currently, artifacts can't create metadata through UI, but you can use REST APIs toocreate metadata.</span></span> <span data-ttu-id="ddbb4-107">tooadd 中繼資料，當您建立或選取 hello Azure 入口網站中的夥伴、 協議或結構描述選擇**編輯 json**。</span><span class="sxs-lookup"><span data-stu-id="ddbb4-107">tooadd metadata when you create or select a partner, agreement, or schema in hello Azure portal, choose **Edit as JSON**.</span></span> <span data-ttu-id="ddbb4-108">tooretrieve 成品的中繼資料邏輯應用程式中，您可以使用 hello 整合帳戶成品查閱功能。</span><span class="sxs-lookup"><span data-stu-id="ddbb4-108">tooretrieve artifact metadata in logic apps, you can use hello Integration Account Artifact Lookup feature.</span></span>

## <a name="add-metadata-tooartifacts-in-integration-accounts"></a><span data-ttu-id="ddbb4-109">在整合帳戶中加入中繼資料 tooartifacts</span><span class="sxs-lookup"><span data-stu-id="ddbb4-109">Add metadata tooartifacts in integration accounts</span></span>

1. <span data-ttu-id="ddbb4-110">建立[整合帳戶](logic-apps-enterprise-integration-create-integration-account.md)。</span><span class="sxs-lookup"><span data-stu-id="ddbb4-110">Create an [integration account](logic-apps-enterprise-integration-create-integration-account.md).</span></span>

2. <span data-ttu-id="ddbb4-111">新增成品 tooyour 整合帳戶，例如、[夥伴](logic-apps-enterprise-integration-partners.md#how-to-create-a-partner)，[協議](logic-apps-enterprise-integration-agreements.md#how-to-create-agreements)，或[結構描述](logic-apps-enterprise-integration-schemas.md)。</span><span class="sxs-lookup"><span data-stu-id="ddbb4-111">Add an artifact tooyour integration account, for example, a [partner](logic-apps-enterprise-integration-partners.md#how-to-create-a-partner), [agreement](logic-apps-enterprise-integration-agreements.md#how-to-create-agreements), or [schema](logic-apps-enterprise-integration-schemas.md).</span></span>

3.  <span data-ttu-id="ddbb4-112">選取 hello 成品，選擇 **編輯 json**，並輸入中繼資料的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ddbb4-112">Select hello artifact, choose **Edit as JSON**, and enter metadata details.</span></span>

    ![輸入中繼資料](media/logic-apps-enterprise-integration-metadata/image1.png)

## <a name="retrieve-metadata-from-artifacts-for-logic-apps"></a><span data-ttu-id="ddbb4-114">從邏輯應用程式的構件擷取中繼資料</span><span class="sxs-lookup"><span data-stu-id="ddbb4-114">Retrieve metadata from artifacts for logic apps</span></span>

1. <span data-ttu-id="ddbb4-115">建立[邏輯應用程式](logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="ddbb4-115">Create a [logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="ddbb4-116">建立[連結從邏輯應用程式 tooyour 整合帳戶](logic-apps-enterprise-integration-create-integration-account.md#link-an-integration-account-to-a-logic-app)。</span><span class="sxs-lookup"><span data-stu-id="ddbb4-116">Create a [link from your logic app tooyour integration account](logic-apps-enterprise-integration-create-integration-account.md#link-an-integration-account-to-a-logic-app).</span></span> 

3. <span data-ttu-id="ddbb4-117">在邏輯應用程式的設計工具，加入 觸發程序類似*要求*或*HTTP* tooyour 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="ddbb4-117">In Logic App Designer, add a trigger like *Request* or *HTTP* tooyour logic app.</span></span>

4.  <span data-ttu-id="ddbb4-118">選擇 [下一步] > [新增動作]。</span><span class="sxs-lookup"><span data-stu-id="ddbb4-118">Choose **Next Step** > **Add an action**.</span></span> <span data-ttu-id="ddbb4-119">搜尋「整合」，如此一來，您就能尋找然後選取 [整合帳戶 - 整合帳戶構件查閱]。</span><span class="sxs-lookup"><span data-stu-id="ddbb4-119">Search for *integration* so you can find and then select **Integration Account - Integration Account Artifact Lookup**.</span></span>

    ![選取整合帳戶構件查閱](media/logic-apps-enterprise-integration-metadata/image2.png)

5. <span data-ttu-id="ddbb4-121">選取 hello**成品類型**，並提供 hello**成品名稱**。</span><span class="sxs-lookup"><span data-stu-id="ddbb4-121">Select hello **Artifact Type**, and provide hello **Artifact Name**.</span></span>

    ![選取構件類型並指定構件名稱](media/logic-apps-enterprise-integration-metadata/image3.png)

## <a name="example-retrieve-partner-metadata"></a><span data-ttu-id="ddbb4-123">範例：擷取合作夥伴中繼資料</span><span class="sxs-lookup"><span data-stu-id="ddbb4-123">Example: Retrieve partner metadata</span></span>

<span data-ttu-id="ddbb4-124">合作夥伴中繼資料含有這些 `routingUrl` 詳細資料：</span><span class="sxs-lookup"><span data-stu-id="ddbb4-124">Partner metadata has these `routingUrl` details:</span></span>

![尋找合作夥伴 "routingURL" 中繼資料](media/logic-apps-enterprise-integration-metadata/image6.png)

1. <span data-ttu-id="ddbb4-126">在您的邏輯應用程式中，新增觸發程序、適用於您合作夥伴的 [整合帳戶 - 整合帳戶構件查閱] 動作，以及 **HTTP**。</span><span class="sxs-lookup"><span data-stu-id="ddbb4-126">In your logic app, add your trigger, an **Integration Account - Integration Account Artifact Lookup** action for your partner, and an **HTTP**.</span></span>

    ![加入觸發程序、 成品查閱 」 和 「 HTTP 」 tooyour 邏輯應用程式](media/logic-apps-enterprise-integration-metadata/image4.png)

2. <span data-ttu-id="ddbb4-128">tooretrieve hello URI，請移 tooCode 檢視應用程式邏輯。</span><span class="sxs-lookup"><span data-stu-id="ddbb4-128">tooretrieve hello URI, go tooCode View for your logic app.</span></span> <span data-ttu-id="ddbb4-129">您的邏輯應用程式定義應該看起來像這個範例：</span><span class="sxs-lookup"><span data-stu-id="ddbb4-129">Your logic app definition should look like this example:</span></span>

    ![搜尋查閱](media/logic-apps-enterprise-integration-metadata/image5.png)


## <a name="next-steps"></a><span data-ttu-id="ddbb4-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ddbb4-131">Next steps</span></span>
* [<span data-ttu-id="ddbb4-132">深入了解合約</span><span class="sxs-lookup"><span data-stu-id="ddbb4-132">Learn more about agreements</span></span>](logic-apps-enterprise-integration-agreements.md "了解企業整合合約")  
