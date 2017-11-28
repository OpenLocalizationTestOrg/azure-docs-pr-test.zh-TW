---
title: "建立企業對企業 (B2B) 訊息的夥伴 - Azure Logic Apps | Microsoft Docs"
description: "了解如何新增夥伴至您的整合帳戶，以搭配企業整合套件與 Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: b179325c-a511-4c1b-9796-f7484b4f6873
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 950cb449b53f400f0f0f860caf5415bbb5212269
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="add-or-update-partners-in-business-to-business-agreements-in-your-workflow"></a><span data-ttu-id="f1d31-103">新增或更新工作流程中企業對企業協議中的夥伴</span><span class="sxs-lookup"><span data-stu-id="f1d31-103">Add or update partners in business-to-business agreements in your workflow</span></span>

<span data-ttu-id="f1d31-104">合作夥伴是參與企業對企業 (B2B) 交易及在彼此之間交換訊息的實體。</span><span class="sxs-lookup"><span data-stu-id="f1d31-104">Partners are entities that participate in business-to-business (B2B) transactions and exchange messages between each other.</span></span> <span data-ttu-id="f1d31-105">在您可以建立這些交易中代表您與其他組織的合作夥伴之前，你們雙方必須先共用可識別及驗證彼此所傳送訊息的資訊。</span><span class="sxs-lookup"><span data-stu-id="f1d31-105">Before you can create partners that represent you and another organization in these transactions, you must both share information that identifies and validates messages sent by each other.</span></span> <span data-ttu-id="f1d31-106">在您討論這些詳細資料並準備開始您的商業關係之後，您可以在您的整合帳戶中建立代表你們雙方的合作夥伴。</span><span class="sxs-lookup"><span data-stu-id="f1d31-106">After you discuss these details and are ready to start your business relationship, you can create partners in your integration account to represent you both.</span></span>

## <a name="what-roles-do-partners-have-in-your-integration-account"></a><span data-ttu-id="f1d31-107">合作夥伴在您的整合帳戶中扮演什麼角色？</span><span class="sxs-lookup"><span data-stu-id="f1d31-107">What roles do partners have in your integration account?</span></span>

<span data-ttu-id="f1d31-108">為定義在合作夥伴之間交換之訊息的相關詳細資料，您必須在那些合作夥伴之間建立合約。</span><span class="sxs-lookup"><span data-stu-id="f1d31-108">To define details about the messages exchanged between partners, you create agreements between those partners.</span></span> <span data-ttu-id="f1d31-109">然而，在您可以建立合約之前，至少需要在整合帳戶中新增兩個以上的合作夥伴。</span><span class="sxs-lookup"><span data-stu-id="f1d31-109">However, before you can create an agreement, you must have added at least two partners to your integration account.</span></span> <span data-ttu-id="f1d31-110">您的組織必須是與**主機合作夥伴**相關之合約的一部分。</span><span class="sxs-lookup"><span data-stu-id="f1d31-110">Your organization must be part of the agreement as the **host partner**.</span></span> <span data-ttu-id="f1d31-111">另一個合作夥伴 (或稱為**來賓合作夥伴**) 代表與您的組織交換訊息的組織。</span><span class="sxs-lookup"><span data-stu-id="f1d31-111">The other partner, or **guest partner** represents the organization that exchanges messages with your organization.</span></span> <span data-ttu-id="f1d31-112">來賓合作夥伴可以是另一家公司，或甚至是您自己組織中的部門。</span><span class="sxs-lookup"><span data-stu-id="f1d31-112">The guest partner can be another company, or even a department in your own organization.</span></span>

<span data-ttu-id="f1d31-113">在您新增這些合作夥伴之後，您可以建立合約。</span><span class="sxs-lookup"><span data-stu-id="f1d31-113">After you add these partners, you can create an agreement.</span></span>

<span data-ttu-id="f1d31-114">接收和傳送設定是主控夥伴觀點導向的。</span><span class="sxs-lookup"><span data-stu-id="f1d31-114">Receive and Send settings are oriented from the point of view of the Hosted Partner.</span></span> <span data-ttu-id="f1d31-115">例如，合約中的接收設定會決定主控夥伴如何接收來賓夥伴所傳送的訊息。</span><span class="sxs-lookup"><span data-stu-id="f1d31-115">For example, the receive settings in an agreement determine how the hosted partner receives messages sent from a guest partner.</span></span> <span data-ttu-id="f1d31-116">同樣地，合約中的傳送設定會指出主控夥伴如何將訊息傳送給來賓夥伴。</span><span class="sxs-lookup"><span data-stu-id="f1d31-116">Likewise, the send settings on the agreement indicate how the hosted partner sends messages to the guest partner.</span></span>

## <a name="how-to-create-a-partner"></a><span data-ttu-id="f1d31-117">如何建立夥伴？</span><span class="sxs-lookup"><span data-stu-id="f1d31-117">How to create a partner?</span></span>

1. <span data-ttu-id="f1d31-118">在 Azure 入口網站中，選取 [瀏覽]。</span><span class="sxs-lookup"><span data-stu-id="f1d31-118">In the Azure portal, select **Browse**.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. <span data-ttu-id="f1d31-119">在篩選搜尋方塊中輸入**整合**，然後選取結果清單中的 [整合帳戶]。</span><span class="sxs-lookup"><span data-stu-id="f1d31-119">In the filter search box, enter **integration**, then select **Integration Accounts** in the results list.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. <span data-ttu-id="f1d31-120">選取要將合作夥伴新增到其中的整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="f1d31-120">Select the integration account where you want to add your partners.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. <span data-ttu-id="f1d31-121">選取 [夥伴]  圖格。</span><span class="sxs-lookup"><span data-stu-id="f1d31-121">Select the **Partners** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-1.png)

5. <span data-ttu-id="f1d31-122">在 [合作夥伴] 刀鋒視窗中，選擇 [新增]。</span><span class="sxs-lookup"><span data-stu-id="f1d31-122">In the Partners blade, choose **Add**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-2.png)

6. <span data-ttu-id="f1d31-123">輸入合作夥伴的名稱，然後選取 [辨識符號]。</span><span class="sxs-lookup"><span data-stu-id="f1d31-123">Enter a name for your partner, then select a **Qualifier**.</span></span> <span data-ttu-id="f1d31-124">最後，輸入 [值] 以協助識別傳送到您應用程式的文件。</span><span class="sxs-lookup"><span data-stu-id="f1d31-124">Finally, enter a **Value** to help identify documents that come into your apps.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-3.png)

7. <span data-ttu-id="f1d31-125">若要查看合作夥伴建立程序，請選取 [鈴鐺] 通知圖示。</span><span class="sxs-lookup"><span data-stu-id="f1d31-125">To see the progress for your partner creation process, select the *bell* notification icon.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-4.png)

8. <span data-ttu-id="f1d31-126">若要確認是否已順利新增您的新合作夥伴，請選取 [合作夥伴] 圖格。</span><span class="sxs-lookup"><span data-stu-id="f1d31-126">To confirm that your new partners were successfully added, select the **Partners** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-5.png)

    <span data-ttu-id="f1d31-127">選取 [合作夥伴] 圖格之後，您也會看見新加入的合作夥伴顯示於 [合作夥伴] 刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="f1d31-127">After you select the Partners tile, you'll also see  newly added partners in the Partners blade.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-6.png)

## <a name="how-to-edit-existing-partners-in-your-integration-account"></a><span data-ttu-id="f1d31-128">如何編輯您整合帳戶中的現有合作夥伴</span><span class="sxs-lookup"><span data-stu-id="f1d31-128">How to edit existing partners in your integration account</span></span>

1. <span data-ttu-id="f1d31-129">選取 [合作夥伴] 圖格。</span><span class="sxs-lookup"><span data-stu-id="f1d31-129">Select the **Partners** tile.</span></span>
2. <span data-ttu-id="f1d31-130">[合作夥伴] 刀鋒視窗開啟之後，請選取您要編輯的合作夥伴。</span><span class="sxs-lookup"><span data-stu-id="f1d31-130">After the Partners blade opens, select the partner you want to edit.</span></span>
3. <span data-ttu-id="f1d31-131">在 [更新合作夥伴] 圖格上，進行您所需的變更。</span><span class="sxs-lookup"><span data-stu-id="f1d31-131">On the **Update Partner** tile, make your changes.</span></span>
4. <span data-ttu-id="f1d31-132">完成之後，請選擇 [儲存]；若要取消您的變更，請選取 [捨棄]。</span><span class="sxs-lookup"><span data-stu-id="f1d31-132">After you're done, choose **Save**, or to cancel your changes, select **Discard**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/edit-1.png)

## <a name="how-to-delete-a-partner"></a><span data-ttu-id="f1d31-133">如何刪除夥伴</span><span class="sxs-lookup"><span data-stu-id="f1d31-133">How to delete a partner</span></span>

1. <span data-ttu-id="f1d31-134">選取 [夥伴]  圖格。</span><span class="sxs-lookup"><span data-stu-id="f1d31-134">Select the **Partners** tile.</span></span>
2. <span data-ttu-id="f1d31-135">[合作夥伴] 刀鋒視窗開啟之後，請選取您要刪除的合作夥伴。</span><span class="sxs-lookup"><span data-stu-id="f1d31-135">After the Partner blade opens, select the partner that you want to delete.</span></span>
3. <span data-ttu-id="f1d31-136">選擇 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="f1d31-136">Choose **Delete**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/delete-1.png)

## <a name="next-steps"></a><span data-ttu-id="f1d31-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f1d31-137">Next steps</span></span>
* [<span data-ttu-id="f1d31-138">深入了解合約</span><span class="sxs-lookup"><span data-stu-id="f1d31-138">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "了解企業整合合約")  

