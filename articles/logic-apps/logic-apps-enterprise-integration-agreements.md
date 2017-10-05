---
title: "B2B 通訊的合約 - Azure Logic Apps | Microsoft Docs"
description: "建立合約，讓合作夥伴可以針對 Azure Logic Apps 與企業整合套件在 B2B 案例中溝通"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 447ffb8e-3e91-4403-872b-2f496495899d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2016
ms.author: LADocs
ms.openlocfilehash: 7ce0860272901f3b4e4cf3d63f7361d539f64741
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="partner-agreements-for-b2b-communication-with-azure-logic-apps-and-enterprise-integration-pack"></a><span data-ttu-id="b4162-103">具有 Azure Logic Apps 與企業整合套件的 B2B 的合作夥伴合約</span><span class="sxs-lookup"><span data-stu-id="b4162-103">Partner agreements for B2B communication with Azure Logic Apps and Enterprise Integration Pack</span></span>

<span data-ttu-id="b4162-104">合約可讓企業實體使用業界標準通訊協定順利地進行溝通，而且是企業對企業 (B2B) 通訊的基石。</span><span class="sxs-lookup"><span data-stu-id="b4162-104">Agreements let business entities communicate seamlessly using industry standard protocols and are the cornerstone for business-to-business (B2B) communication.</span></span> <span data-ttu-id="b4162-105">使用企業整合套件針對邏輯應用程式啟用 B2B 案例時，合約是 B2B 交易合作夥伴之間的通訊協議。</span><span class="sxs-lookup"><span data-stu-id="b4162-105">When enabling B2B scenarios for logic apps with the Enterprise Integration Pack, an agreement is a communications arrangement between B2B trading partners.</span></span> <span data-ttu-id="b4162-106">此合約是以合作夥伴想要達成的通訊為基礎，而且是通訊協定或傳輸特定的。</span><span class="sxs-lookup"><span data-stu-id="b4162-106">This agreement is based on the communications that the partners want to establish and is protocol or transport-specific.</span></span>

<span data-ttu-id="b4162-107">企業整合支援下列三種通訊協定或傳輸標準：</span><span class="sxs-lookup"><span data-stu-id="b4162-107">Enterprise integration supports these protocol or transport standards:</span></span>

* [<span data-ttu-id="b4162-108">AS2</span><span class="sxs-lookup"><span data-stu-id="b4162-108">AS2</span></span>](logic-apps-enterprise-integration-as2.md)
* [<span data-ttu-id="b4162-109">X12</span><span class="sxs-lookup"><span data-stu-id="b4162-109">X12</span></span>](logic-apps-enterprise-integration-x12.md)
* [<span data-ttu-id="b4162-110">EDIFACT</span><span class="sxs-lookup"><span data-stu-id="b4162-110">EDIFACT</span></span>](logic-apps-enterprise-integration-edifact.md)

## <a name="why-use-agreements"></a><span data-ttu-id="b4162-111">為什麼要使用合約</span><span class="sxs-lookup"><span data-stu-id="b4162-111">Why use agreements</span></span>

<span data-ttu-id="b4162-112">使用合約有下列常見優點：</span><span class="sxs-lookup"><span data-stu-id="b4162-112">Here are some common benefits when using agreements:</span></span>

* <span data-ttu-id="b4162-113">可讓不同的組織和企業能夠利用已知格式來交換資訊。</span><span class="sxs-lookup"><span data-stu-id="b4162-113">Enables different organizations and businesses to exchange information in a well-known format.</span></span>
* <span data-ttu-id="b4162-114">進行 B2B 交易時，可以提升效率</span><span class="sxs-lookup"><span data-stu-id="b4162-114">Improves efficiency when conducting B2B transactions</span></span>
* <span data-ttu-id="b4162-115">在建立企業整合應用程式時輕鬆地建立、管理及使用它們</span><span class="sxs-lookup"><span data-stu-id="b4162-115">Easy to create, manage, and use when creating enterprise integration apps</span></span>

## <a name="how-to-create-agreements"></a><span data-ttu-id="b4162-116">如何建立合約</span><span class="sxs-lookup"><span data-stu-id="b4162-116">How to create agreements</span></span>

* [<span data-ttu-id="b4162-117">建立 AS2 合約</span><span class="sxs-lookup"><span data-stu-id="b4162-117">Create an AS2 agreement</span></span>](logic-apps-enterprise-integration-as2.md)
* [<span data-ttu-id="b4162-118">建立 X12 合約</span><span class="sxs-lookup"><span data-stu-id="b4162-118">Create an X12 agreement</span></span>](logic-apps-enterprise-integration-x12.md)
* [<span data-ttu-id="b4162-119">建立 EDIFACT 合約</span><span class="sxs-lookup"><span data-stu-id="b4162-119">Create an EDIFACT agreement</span></span>](logic-apps-enterprise-integration-edifact.md)

## <a name="how-to-use-an-agreement"></a><span data-ttu-id="b4162-120">如何使用合約</span><span class="sxs-lookup"><span data-stu-id="b4162-120">How to use an agreement</span></span>

<span data-ttu-id="b4162-121">您可以使用您建立的合約來建立具有 B2B 功能的[邏輯應用程式](logic-apps-what-are-logic-apps.md "了解邏輯應用程式")。</span><span class="sxs-lookup"><span data-stu-id="b4162-121">You can create [logic apps](logic-apps-what-are-logic-apps.md "Learn about Logic apps") with B2B capabilities by using an agreement that you created.</span></span>

## <a name="how-to-edit-an-agreement"></a><span data-ttu-id="b4162-122">如何編輯合約</span><span class="sxs-lookup"><span data-stu-id="b4162-122">How to edit an agreement</span></span>

<span data-ttu-id="b4162-123">您可以依照下列步驟來編輯任何合約：</span><span class="sxs-lookup"><span data-stu-id="b4162-123">You can edit any agreement by following these steps:</span></span>

1. <span data-ttu-id="b4162-124">選取包含您要更新之合約的整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="b4162-124">Select the integration account that has the agreement you want to update.</span></span>

2. <span data-ttu-id="b4162-125">選擇 [合約] 圖格。</span><span class="sxs-lookup"><span data-stu-id="b4162-125">Choose the **Agreements** tile.</span></span>

3. <span data-ttu-id="b4162-126">在 [合約] 刀鋒視窗上，選取合約。</span><span class="sxs-lookup"><span data-stu-id="b4162-126">On the **Agreements** blade, select the agreement.</span></span>

4. <span data-ttu-id="b4162-127">選擇 [編輯]。</span><span class="sxs-lookup"><span data-stu-id="b4162-127">Choose **Edit**.</span></span> <span data-ttu-id="b4162-128">進行變更。</span><span class="sxs-lookup"><span data-stu-id="b4162-128">Make your changes.</span></span>

5. <span data-ttu-id="b4162-129">若要儲存變更，請選擇 [確定]。</span><span class="sxs-lookup"><span data-stu-id="b4162-129">To save your changes, choose **OK**.</span></span>

## <a name="how-to-delete-an-agreement"></a><span data-ttu-id="b4162-130">如何刪除合約</span><span class="sxs-lookup"><span data-stu-id="b4162-130">How to delete an agreement</span></span>

<span data-ttu-id="b4162-131">您可以依照下列步驟來刪除任何合約：</span><span class="sxs-lookup"><span data-stu-id="b4162-131">You can delete any agreement by following these steps:</span></span>

1. <span data-ttu-id="b4162-132">選取包含您要刪除之合約的整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="b4162-132">Select the integration account that has the agreement you want to delete.</span></span>
2. <span data-ttu-id="b4162-133">選擇 [合約] 圖格。</span><span class="sxs-lookup"><span data-stu-id="b4162-133">Choose the **Agreements** tile.</span></span>
3. <span data-ttu-id="b4162-134">在 [合約] 刀鋒視窗上，選取合約。</span><span class="sxs-lookup"><span data-stu-id="b4162-134">On the **Agreements** blade, select the agreement.</span></span>
4. <span data-ttu-id="b4162-135">選擇 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="b4162-135">Choose **Delete**.</span></span>
5. <span data-ttu-id="b4162-136">確認您要刪除選取的合約。</span><span class="sxs-lookup"><span data-stu-id="b4162-136">Confirm that you want to delete the selected agreement.</span></span>

    <span data-ttu-id="b4162-137">[合約] 刀鋒視窗不會再顯示已刪除的合約。</span><span class="sxs-lookup"><span data-stu-id="b4162-137">The Agreements blade no longer shows the deleted agreement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4162-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b4162-138">Next steps</span></span>
* [<span data-ttu-id="b4162-139">建立 AS2 合約</span><span class="sxs-lookup"><span data-stu-id="b4162-139">Create an AS2 agreement</span></span>](logic-apps-enterprise-integration-as2.md)
