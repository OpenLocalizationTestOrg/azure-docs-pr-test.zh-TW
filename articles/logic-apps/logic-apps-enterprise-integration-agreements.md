---
title: "B2B 通訊-Azure 邏輯應用程式的 aaaAgreements |Microsoft 文件"
description: "建立協議，讓夥伴可以通訊 B2B 案例中，為 Azure 邏輯應用程式與 hello 企業版整合套件"
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
ms.openlocfilehash: 499edcbab1cd67fbc169e393c3cad7b81658a250
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="partner-agreements-for-b2b-communication-with-azure-logic-apps-and-enterprise-integration-pack"></a><span data-ttu-id="9beec-103">具有 Azure Logic Apps 與企業整合套件的 B2B 的合作夥伴合約</span><span class="sxs-lookup"><span data-stu-id="9beec-103">Partner agreements for B2B communication with Azure Logic Apps and Enterprise Integration Pack</span></span>

<span data-ttu-id="9beec-104">合約可讓順暢地使用業界標準通訊協定進行通訊的商務實體和 hello cornerstone 進行企業對企業 (B2B) 通訊。</span><span class="sxs-lookup"><span data-stu-id="9beec-104">Agreements let business entities communicate seamlessly using industry standard protocols and are hello cornerstone for business-to-business (B2B) communication.</span></span> <span data-ttu-id="9beec-105">啟用以 hello 企業版整合套件的 logic apps B2B 案例，協議時 B2B 交易夥伴之間的通訊排列。</span><span class="sxs-lookup"><span data-stu-id="9beec-105">When enabling B2B scenarios for logic apps with hello Enterprise Integration Pack, an agreement is a communications arrangement between B2B trading partners.</span></span> <span data-ttu-id="9beec-106">此協議根據的 hello hello 夥伴想要的通訊太建立，而且是通訊協定或傳輸特定。</span><span class="sxs-lookup"><span data-stu-id="9beec-106">This agreement is based on hello communications that hello partners want too establish and is protocol or transport-specific.</span></span>

<span data-ttu-id="9beec-107">企業整合支援下列三種通訊協定或傳輸標準：</span><span class="sxs-lookup"><span data-stu-id="9beec-107">Enterprise integration supports these protocol or transport standards:</span></span>

* [<span data-ttu-id="9beec-108">AS2</span><span class="sxs-lookup"><span data-stu-id="9beec-108">AS2</span></span>](logic-apps-enterprise-integration-as2.md)
* [<span data-ttu-id="9beec-109">X12</span><span class="sxs-lookup"><span data-stu-id="9beec-109">X12</span></span>](logic-apps-enterprise-integration-x12.md)
* [<span data-ttu-id="9beec-110">EDIFACT</span><span class="sxs-lookup"><span data-stu-id="9beec-110">EDIFACT</span></span>](logic-apps-enterprise-integration-edifact.md)

## <a name="why-use-agreements"></a><span data-ttu-id="9beec-111">為什麼要使用合約</span><span class="sxs-lookup"><span data-stu-id="9beec-111">Why use agreements</span></span>

<span data-ttu-id="9beec-112">使用合約有下列常見優點：</span><span class="sxs-lookup"><span data-stu-id="9beec-112">Here are some common benefits when using agreements:</span></span>

* <span data-ttu-id="9beec-113">可讓不同組織和企業 tooexchange 資訊中的已知的格式。</span><span class="sxs-lookup"><span data-stu-id="9beec-113">Enables different organizations and businesses tooexchange information in a well-known format.</span></span>
* <span data-ttu-id="9beec-114">進行 B2B 交易時，可以提升效率</span><span class="sxs-lookup"><span data-stu-id="9beec-114">Improves efficiency when conducting B2B transactions</span></span>
* <span data-ttu-id="9beec-115">輕鬆 toocreate，管理和使用建立企業整合應用程式時</span><span class="sxs-lookup"><span data-stu-id="9beec-115">Easy toocreate, manage, and use when creating enterprise integration apps</span></span>

## <a name="how-toocreate-agreements"></a><span data-ttu-id="9beec-116">如何 toocreate 協議</span><span class="sxs-lookup"><span data-stu-id="9beec-116">How toocreate agreements</span></span>

* [<span data-ttu-id="9beec-117">建立 AS2 合約</span><span class="sxs-lookup"><span data-stu-id="9beec-117">Create an AS2 agreement</span></span>](logic-apps-enterprise-integration-as2.md)
* [<span data-ttu-id="9beec-118">建立 X12 合約</span><span class="sxs-lookup"><span data-stu-id="9beec-118">Create an X12 agreement</span></span>](logic-apps-enterprise-integration-x12.md)
* [<span data-ttu-id="9beec-119">建立 EDIFACT 合約</span><span class="sxs-lookup"><span data-stu-id="9beec-119">Create an EDIFACT agreement</span></span>](logic-apps-enterprise-integration-edifact.md)

## <a name="how-toouse-an-agreement"></a><span data-ttu-id="9beec-120">如何 toouse 協議</span><span class="sxs-lookup"><span data-stu-id="9beec-120">How toouse an agreement</span></span>

<span data-ttu-id="9beec-121">您可以使用您建立的合約來建立具有 B2B 功能的[邏輯應用程式](logic-apps-what-are-logic-apps.md "了解邏輯應用程式")。</span><span class="sxs-lookup"><span data-stu-id="9beec-121">You can create [logic apps](logic-apps-what-are-logic-apps.md "Learn about Logic apps") with B2B capabilities by using an agreement that you created.</span></span>

## <a name="how-tooedit-an-agreement"></a><span data-ttu-id="9beec-122">如何 tooedit 協議</span><span class="sxs-lookup"><span data-stu-id="9beec-122">How tooedit an agreement</span></span>

<span data-ttu-id="9beec-123">您可以依照下列步驟來編輯任何合約：</span><span class="sxs-lookup"><span data-stu-id="9beec-123">You can edit any agreement by following these steps:</span></span>

1. <span data-ttu-id="9beec-124">選取具有您想要 tooupdate hello 協議的 hello 整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="9beec-124">Select hello integration account that has hello agreement you want tooupdate.</span></span>

2. <span data-ttu-id="9beec-125">選擇 hello**協議**磚。</span><span class="sxs-lookup"><span data-stu-id="9beec-125">Choose hello **Agreements** tile.</span></span>

3. <span data-ttu-id="9beec-126">在 hello**協議**刀鋒視窗中，選取 hello 協議。</span><span class="sxs-lookup"><span data-stu-id="9beec-126">On hello **Agreements** blade, select hello agreement.</span></span>

4. <span data-ttu-id="9beec-127">選擇 [編輯]。</span><span class="sxs-lookup"><span data-stu-id="9beec-127">Choose **Edit**.</span></span> <span data-ttu-id="9beec-128">進行變更。</span><span class="sxs-lookup"><span data-stu-id="9beec-128">Make your changes.</span></span>

5. <span data-ttu-id="9beec-129">您的變更，選擇 toosave**確定**。</span><span class="sxs-lookup"><span data-stu-id="9beec-129">toosave your changes, choose **OK**.</span></span>

## <a name="how-toodelete-an-agreement"></a><span data-ttu-id="9beec-130">如何 toodelete 協議</span><span class="sxs-lookup"><span data-stu-id="9beec-130">How toodelete an agreement</span></span>

<span data-ttu-id="9beec-131">您可以依照下列步驟來刪除任何合約：</span><span class="sxs-lookup"><span data-stu-id="9beec-131">You can delete any agreement by following these steps:</span></span>

1. <span data-ttu-id="9beec-132">選取具有您想要 toodelete hello 協議的 hello 整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="9beec-132">Select hello integration account that has hello agreement you want toodelete.</span></span>
2. <span data-ttu-id="9beec-133">選擇 hello**協議**磚。</span><span class="sxs-lookup"><span data-stu-id="9beec-133">Choose hello **Agreements** tile.</span></span>
3. <span data-ttu-id="9beec-134">在 hello**協議**刀鋒視窗中，選取 hello 協議。</span><span class="sxs-lookup"><span data-stu-id="9beec-134">On hello **Agreements** blade, select hello agreement.</span></span>
4. <span data-ttu-id="9beec-135">選擇 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="9beec-135">Choose **Delete**.</span></span>
5. <span data-ttu-id="9beec-136">確認您想 toodelete hello 選取協議。</span><span class="sxs-lookup"><span data-stu-id="9beec-136">Confirm that you want toodelete hello selected agreement.</span></span>

    <span data-ttu-id="9beec-137">hello 協議 刀鋒視窗不會再顯示 hello 刪除協議。</span><span class="sxs-lookup"><span data-stu-id="9beec-137">hello Agreements blade no longer shows hello deleted agreement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9beec-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9beec-138">Next steps</span></span>
* [<span data-ttu-id="9beec-139">建立 AS2 合約</span><span class="sxs-lookup"><span data-stu-id="9beec-139">Create an AS2 agreement</span></span>](logic-apps-enterprise-integration-as2.md)
