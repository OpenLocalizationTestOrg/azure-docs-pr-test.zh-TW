---
title: "企業對企業 (B2B) 訊息-Azure 邏輯應用程式的 aaaCreate 夥伴 |Microsoft 文件"
description: "了解如何 tooadd 夥伴 tooyour 整合帳戶 hello 企業版整合套件與 Logic Apps"
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
ms.openlocfilehash: 8dc70a8f441fcf228ed178029dcdbac940d794b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-update-partners-in-business-to-business-agreements-in-your-workflow"></a><span data-ttu-id="0435d-103">新增或更新工作流程中企業對企業協議中的夥伴</span><span class="sxs-lookup"><span data-stu-id="0435d-103">Add or update partners in business-to-business agreements in your workflow</span></span>

<span data-ttu-id="0435d-104">合作夥伴是參與企業對企業 (B2B) 交易及在彼此之間交換訊息的實體。</span><span class="sxs-lookup"><span data-stu-id="0435d-104">Partners are entities that participate in business-to-business (B2B) transactions and exchange messages between each other.</span></span> <span data-ttu-id="0435d-105">在您可以建立這些交易中代表您與其他組織的合作夥伴之前，你們雙方必須先共用可識別及驗證彼此所傳送訊息的資訊。</span><span class="sxs-lookup"><span data-stu-id="0435d-105">Before you can create partners that represent you and another organization in these transactions, you must both share information that identifies and validates messages sent by each other.</span></span> <span data-ttu-id="0435d-106">在討論這些詳細資料，並已準備好 toostart 商務關係之後，您可以建立在您整合帳戶 toorepresent 夥伴雙方。</span><span class="sxs-lookup"><span data-stu-id="0435d-106">After you discuss these details and are ready toostart your business relationship, you can create partners in your integration account toorepresent you both.</span></span>

## <a name="what-roles-do-partners-have-in-your-integration-account"></a><span data-ttu-id="0435d-107">合作夥伴在您的整合帳戶中扮演什麼角色？</span><span class="sxs-lookup"><span data-stu-id="0435d-107">What roles do partners have in your integration account?</span></span>

<span data-ttu-id="0435d-108">有關夥伴之間交換的 hello 訊息 toodefine 詳細資料，您會建立這些夥伴之間的協議。</span><span class="sxs-lookup"><span data-stu-id="0435d-108">toodefine details about hello messages exchanged between partners, you create agreements between those partners.</span></span> <span data-ttu-id="0435d-109">不過，您可以建立協議之前，您必須新增至少兩個夥伴 tooyour 整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="0435d-109">However, before you can create an agreement, you must have added at least two partners tooyour integration account.</span></span> <span data-ttu-id="0435d-110">您的組織必須為 hello hello 協議**主控合作夥伴**。</span><span class="sxs-lookup"><span data-stu-id="0435d-110">Your organization must be part of hello agreement as hello **host partner**.</span></span> <span data-ttu-id="0435d-111">hello 另一個夥伴，或**來賓夥伴**代表 hello 與您的組織交換訊息的組織。</span><span class="sxs-lookup"><span data-stu-id="0435d-111">hello other partner, or **guest partner** represents hello organization that exchanges messages with your organization.</span></span> <span data-ttu-id="0435d-112">hello 來賓夥伴可以是另一家公司或甚至您組織中的部門。</span><span class="sxs-lookup"><span data-stu-id="0435d-112">hello guest partner can be another company, or even a department in your own organization.</span></span>

<span data-ttu-id="0435d-113">在您新增這些合作夥伴之後，您可以建立合約。</span><span class="sxs-lookup"><span data-stu-id="0435d-113">After you add these partners, you can create an agreement.</span></span>

<span data-ttu-id="0435d-114">接收和傳送設定會導向從 hello 觀點來看的 hello Hosted 夥伴。</span><span class="sxs-lookup"><span data-stu-id="0435d-114">Receive and Send settings are oriented from hello point of view of hello Hosted Partner.</span></span> <span data-ttu-id="0435d-115">例如，hello 接收協議中的設定判斷 hello 主控夥伴接收從來賓夥伴傳送訊息的方式。</span><span class="sxs-lookup"><span data-stu-id="0435d-115">For example, hello receive settings in an agreement determine how hello hosted partner receives messages sent from a guest partner.</span></span> <span data-ttu-id="0435d-116">同樣地，hello hello 協議上的傳送設定會指出 hello 主控夥伴傳送訊息 toohello 來賓夥伴的方式。</span><span class="sxs-lookup"><span data-stu-id="0435d-116">Likewise, hello send settings on hello agreement indicate how hello hosted partner sends messages toohello guest partner.</span></span>

## <a name="how-toocreate-a-partner"></a><span data-ttu-id="0435d-117">如何 toocreate 合作夥伴嗎？</span><span class="sxs-lookup"><span data-stu-id="0435d-117">How toocreate a partner?</span></span>

1. <span data-ttu-id="0435d-118">在 hello Azure 入口網站，選取 **瀏覽**。</span><span class="sxs-lookup"><span data-stu-id="0435d-118">In hello Azure portal, select **Browse**.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. <span data-ttu-id="0435d-119">在 hello 篩選搜尋方塊中，輸入**整合**，然後選取**整合帳戶**hello 結果 清單中。</span><span class="sxs-lookup"><span data-stu-id="0435d-119">In hello filter search box, enter **integration**, then select **Integration Accounts** in hello results list.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. <span data-ttu-id="0435d-120">選取您想 tooadd 合作夥伴之間的 hello 整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="0435d-120">Select hello integration account where you want tooadd your partners.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. <span data-ttu-id="0435d-121">選取 hello**夥伴**磚。</span><span class="sxs-lookup"><span data-stu-id="0435d-121">Select hello **Partners** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-1.png)

5. <span data-ttu-id="0435d-122">在 hello 夥伴刀鋒視窗中，選擇 **新增**。</span><span class="sxs-lookup"><span data-stu-id="0435d-122">In hello Partners blade, choose **Add**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-2.png)

6. <span data-ttu-id="0435d-123">輸入合作夥伴的名稱，然後選取 [辨識符號]。</span><span class="sxs-lookup"><span data-stu-id="0435d-123">Enter a name for your partner, then select a **Qualifier**.</span></span> <span data-ttu-id="0435d-124">最後，請輸入**值**toohelp 識別進入您的應用程式的文件。</span><span class="sxs-lookup"><span data-stu-id="0435d-124">Finally, enter a **Value** toohelp identify documents that come into your apps.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-3.png)

7. <span data-ttu-id="0435d-125">您的夥伴建立程序中，選取 hello toosee hello 進度*鈴鐺*通知圖示。</span><span class="sxs-lookup"><span data-stu-id="0435d-125">toosee hello progress for your partner creation process, select hello *bell* notification icon.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-4.png)

8. <span data-ttu-id="0435d-126">加入新合作夥伴之間成功的 tooconfirm，選取 hello**夥伴**磚。</span><span class="sxs-lookup"><span data-stu-id="0435d-126">tooconfirm that your new partners were successfully added, select hello **Partners** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-5.png)

    <span data-ttu-id="0435d-127">選取 hello 夥伴磚之後，您也會看到新增的夥伴 hello 夥伴刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="0435d-127">After you select hello Partners tile, you'll also see  newly added partners in hello Partners blade.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-6.png)

## <a name="how-tooedit-existing-partners-in-your-integration-account"></a><span data-ttu-id="0435d-128">如何 tooedit 現有整合帳戶中的合作夥伴</span><span class="sxs-lookup"><span data-stu-id="0435d-128">How tooedit existing partners in your integration account</span></span>

1. <span data-ttu-id="0435d-129">選取 hello**夥伴**磚。</span><span class="sxs-lookup"><span data-stu-id="0435d-129">Select hello **Partners** tile.</span></span>
2. <span data-ttu-id="0435d-130">Hello 夥伴刀鋒視窗開啟後，請選取您想要 tooedit hello 夥伴。</span><span class="sxs-lookup"><span data-stu-id="0435d-130">After hello Partners blade opens, select hello partner you want tooedit.</span></span>
3. <span data-ttu-id="0435d-131">在 hello**更新夥伴**磚上，進行變更。</span><span class="sxs-lookup"><span data-stu-id="0435d-131">On hello **Update Partner** tile, make your changes.</span></span>
4. <span data-ttu-id="0435d-132">瀏覽完畢之後，請選擇**儲存**，或您的變更，選取 toocancel**捨棄**。</span><span class="sxs-lookup"><span data-stu-id="0435d-132">After you're done, choose **Save**, or toocancel your changes, select **Discard**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/edit-1.png)

## <a name="how-toodelete-a-partner"></a><span data-ttu-id="0435d-133">如何 toodelete 合作夥伴</span><span class="sxs-lookup"><span data-stu-id="0435d-133">How toodelete a partner</span></span>

1. <span data-ttu-id="0435d-134">選取 hello**夥伴**磚。</span><span class="sxs-lookup"><span data-stu-id="0435d-134">Select hello **Partners** tile.</span></span>
2. <span data-ttu-id="0435d-135">Hello 夥伴刀鋒視窗開啟後，請選取您想 toodelete hello 夥伴。</span><span class="sxs-lookup"><span data-stu-id="0435d-135">After hello Partner blade opens, select hello partner that you want toodelete.</span></span>
3. <span data-ttu-id="0435d-136">選擇 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="0435d-136">Choose **Delete**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/delete-1.png)

## <a name="next-steps"></a><span data-ttu-id="0435d-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0435d-137">Next steps</span></span>
* [<span data-ttu-id="0435d-138">深入了解合約</span><span class="sxs-lookup"><span data-stu-id="0435d-138">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "了解企業整合合約")  

