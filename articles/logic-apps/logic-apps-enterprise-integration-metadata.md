---
title: "管理整合帳戶構件中繼資料 - Azure Logic Apps | Microsoft Docs"
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
ms.openlocfilehash: 28bb8296ddd820ec5aa9793dc0928b4b1e67bf6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-artifact-metadata-in-integration-accounts-for-logic-apps"></a><span data-ttu-id="9c663-103">在 Logic Apps 的整合帳戶中管理構件中繼資料</span><span class="sxs-lookup"><span data-stu-id="9c663-103">Manage artifact metadata in integration accounts for logic apps</span></span>

<span data-ttu-id="9c663-104">您可以在整合帳戶中定義構件的自訂中繼資料，並在邏輯應用程式的執行階段期間擷取該中繼資料。</span><span class="sxs-lookup"><span data-stu-id="9c663-104">You can define custom metadata for artifacts in integration accounts and retrieve that metadata during runtime for your logic app.</span></span> <span data-ttu-id="9c663-105">例如，您可以指定構件的中繼資料，例如，合作夥伴、合約、結構描述及對應，這些全都會使用索引鍵值組來儲存中繼資料。</span><span class="sxs-lookup"><span data-stu-id="9c663-105">For example, you can specify metadata for artifacts like partners, agreements, schemas, and maps - all store metadata using key-value pairs.</span></span> <span data-ttu-id="9c663-106">構件目前無法透過 UI 來建立中繼資料，但您可以使用 REST API 來建立中繼資料。</span><span class="sxs-lookup"><span data-stu-id="9c663-106">Currently, artifacts can't create metadata through UI, but you can use REST APIs to create metadata.</span></span> <span data-ttu-id="9c663-107">若要在您於 Azure 入口網站中建立或選取合作夥伴、合約或結構描述時新增中繼資料，可選擇 [編輯為 JSON]。</span><span class="sxs-lookup"><span data-stu-id="9c663-107">To add metadata when you create or select a partner, agreement, or schema in the Azure portal, choose **Edit as JSON**.</span></span> <span data-ttu-id="9c663-108">若要擷取邏輯應用程式中的構件中繼資料，您可以使用整合帳戶構件查閱功能。</span><span class="sxs-lookup"><span data-stu-id="9c663-108">To retrieve artifact metadata in logic apps, you can use the Integration Account Artifact Lookup feature.</span></span>

## <a name="add-metadata-to-artifacts-in-integration-accounts"></a><span data-ttu-id="9c663-109">將中繼資料新增至整合帳戶中的構件</span><span class="sxs-lookup"><span data-stu-id="9c663-109">Add metadata to artifacts in integration accounts</span></span>

1. <span data-ttu-id="9c663-110">建立[整合帳戶](logic-apps-enterprise-integration-create-integration-account.md)。</span><span class="sxs-lookup"><span data-stu-id="9c663-110">Create an [integration account](logic-apps-enterprise-integration-create-integration-account.md).</span></span>

2. <span data-ttu-id="9c663-111">將構件新增至您的整合帳戶，例如，[合作夥伴](logic-apps-enterprise-integration-partners.md#how-to-create-a-partner)、[合約](logic-apps-enterprise-integration-agreements.md#how-to-create-agreements)或[結構描述](logic-apps-enterprise-integration-schemas.md)。</span><span class="sxs-lookup"><span data-stu-id="9c663-111">Add an artifact to your integration account, for example, a [partner](logic-apps-enterprise-integration-partners.md#how-to-create-a-partner), [agreement](logic-apps-enterprise-integration-agreements.md#how-to-create-agreements), or [schema](logic-apps-enterprise-integration-schemas.md).</span></span>

3.  <span data-ttu-id="9c663-112">選取構件、選擇 [編輯為 JSON]，然後輸入中繼資料詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="9c663-112">Select the artifact, choose **Edit as JSON**, and enter metadata details.</span></span>

    ![輸入中繼資料](media/logic-apps-enterprise-integration-metadata/image1.png)

## <a name="retrieve-metadata-from-artifacts-for-logic-apps"></a><span data-ttu-id="9c663-114">從邏輯應用程式的構件擷取中繼資料</span><span class="sxs-lookup"><span data-stu-id="9c663-114">Retrieve metadata from artifacts for logic apps</span></span>

1. <span data-ttu-id="9c663-115">建立[邏輯應用程式](logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="9c663-115">Create a [logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="9c663-116">建立[從邏輯應用程式到您整合帳戶的連結](logic-apps-enterprise-integration-create-integration-account.md#link-an-integration-account-to-a-logic-app)。</span><span class="sxs-lookup"><span data-stu-id="9c663-116">Create a [link from your logic app to your integration account](logic-apps-enterprise-integration-create-integration-account.md#link-an-integration-account-to-a-logic-app).</span></span> 

3. <span data-ttu-id="9c663-117">在邏輯應用程式設計工具中，將要求 或 HTTP 之類的觸發程序新增至邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="9c663-117">In Logic App Designer, add a trigger like *Request* or *HTTP* to your logic app.</span></span>

4.  <span data-ttu-id="9c663-118">選擇 [下一步] > [新增動作]。</span><span class="sxs-lookup"><span data-stu-id="9c663-118">Choose **Next Step** > **Add an action**.</span></span> <span data-ttu-id="9c663-119">搜尋「整合」，如此一來，您就能尋找然後選取 [整合帳戶 - 整合帳戶構件查閱]。</span><span class="sxs-lookup"><span data-stu-id="9c663-119">Search for *integration* so you can find and then select **Integration Account - Integration Account Artifact Lookup**.</span></span>

    ![選取整合帳戶構件查閱](media/logic-apps-enterprise-integration-metadata/image2.png)

5. <span data-ttu-id="9c663-121">選取 [構件類型]，並提供 [構件名稱]。</span><span class="sxs-lookup"><span data-stu-id="9c663-121">Select the **Artifact Type**, and provide the **Artifact Name**.</span></span>

    ![選取構件類型並指定構件名稱](media/logic-apps-enterprise-integration-metadata/image3.png)

## <a name="example-retrieve-partner-metadata"></a><span data-ttu-id="9c663-123">範例：擷取合作夥伴中繼資料</span><span class="sxs-lookup"><span data-stu-id="9c663-123">Example: Retrieve partner metadata</span></span>

<span data-ttu-id="9c663-124">合作夥伴中繼資料含有這些 `routingUrl` 詳細資料：</span><span class="sxs-lookup"><span data-stu-id="9c663-124">Partner metadata has these `routingUrl` details:</span></span>

![尋找合作夥伴 "routingURL" 中繼資料](media/logic-apps-enterprise-integration-metadata/image6.png)

1. <span data-ttu-id="9c663-126">在您的邏輯應用程式中，新增觸發程序、適用於您合作夥伴的 [整合帳戶 - 整合帳戶構件查閱] 動作，以及 **HTTP**。</span><span class="sxs-lookup"><span data-stu-id="9c663-126">In your logic app, add your trigger, an **Integration Account - Integration Account Artifact Lookup** action for your partner, and an **HTTP**.</span></span>

    ![將觸發程序、構件查閱及 "HTTP" 新增至您的邏輯應用程式](media/logic-apps-enterprise-integration-metadata/image4.png)

2. <span data-ttu-id="9c663-128">若要擷取 URI，請移至邏輯應用程式的 [程式碼檢視]。</span><span class="sxs-lookup"><span data-stu-id="9c663-128">To retrieve the URI, go to Code View for your logic app.</span></span> <span data-ttu-id="9c663-129">您的邏輯應用程式定義應該看起來像這個範例：</span><span class="sxs-lookup"><span data-stu-id="9c663-129">Your logic app definition should look like this example:</span></span>

    ![搜尋查閱](media/logic-apps-enterprise-integration-metadata/image5.png)


## <a name="next-steps"></a><span data-ttu-id="9c663-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9c663-131">Next steps</span></span>
* [<span data-ttu-id="9c663-132">深入了解合約</span><span class="sxs-lookup"><span data-stu-id="9c663-132">Learn more about agreements</span></span>](logic-apps-enterprise-integration-agreements.md "了解企業整合合約")  
