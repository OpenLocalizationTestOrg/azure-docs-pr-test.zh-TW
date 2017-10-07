---
title: "aaaCreate、 連結、 刪除或移動 Azure 邏輯應用程式中整合帳戶 |Microsoft 文件"
description: "如何整合 toocreate 帳戶，並將其連結 tooyour 邏輯應用程式"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: d3ad9e99-a9ee-477b-81bf-0881e11e632f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: LADocs; mandia
ms.openlocfilehash: fda6c91723b3e3624ee176df112ba8b6c9800273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-an-integration-account"></a><span data-ttu-id="26c7e-103">什麼是整合帳戶？</span><span class="sxs-lookup"><span data-stu-id="26c7e-103">What is an integration account?</span></span>

<span data-ttu-id="26c7e-104">整合帳戶可讓企業整合應用程式 toomanage 成品，包括結構描述、 對應、 憑證、 夥伴和協議。</span><span class="sxs-lookup"><span data-stu-id="26c7e-104">An integration account allows enterprise integration apps toomanage artifacts, including schemas, maps, certificates, partners and agreements.</span></span> <span data-ttu-id="26c7e-105">您所建立的任何整合應用程式使用整合帳戶 tooaccess 這些結構描述、 對應、 憑證等等。</span><span class="sxs-lookup"><span data-stu-id="26c7e-105">Any integration app you create uses an integration account tooaccess these schemas, maps, certificates, and so on.</span></span>

## <a name="create-an-integration-account"></a><span data-ttu-id="26c7e-106">建立整合帳戶</span><span class="sxs-lookup"><span data-stu-id="26c7e-106">Create an integration account</span></span>

1.  <span data-ttu-id="26c7e-107">登入 toohello [Azure 入口網站](http://portal.azure.com "Azure 入口網站")。</span><span class="sxs-lookup"><span data-stu-id="26c7e-107">Sign in toohello [Azure portal](http://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="26c7e-108">從 hello 左窗格中，選取**更多服務**。</span><span class="sxs-lookup"><span data-stu-id="26c7e-108">From hello left menu, select **More services**.</span></span>

    ![選取 [更多服務]。](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="26c7e-110">在 hello 搜尋方塊中，輸入 「 整合 」 篩選條件。</span><span class="sxs-lookup"><span data-stu-id="26c7e-110">In hello search box, type "integration" for your filter.</span></span> <span data-ttu-id="26c7e-111">在 hello 結果清單中，選取 **整合帳戶**。</span><span class="sxs-lookup"><span data-stu-id="26c7e-111">In hello results list, select **Integration Accounts**.</span></span>

    ![依據 [整合] 篩選，選取 [整合帳戶]](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. <span data-ttu-id="26c7e-113">在 hello hello 頁面頂端，選擇**新增**。</span><span class="sxs-lookup"><span data-stu-id="26c7e-113">At hello top of hello page, choose **Add**.</span></span>

    ![選擇 [新增]](./media/logic-apps-enterprise-integration-accounts/account-3.png)

4. <span data-ttu-id="26c7e-115">命名您的整合帳戶和選取 hello 想 toouse 的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="26c7e-115">Name your integration account and select hello Azure subscription that you want toouse.</span></span> <span data-ttu-id="26c7e-116">您可以建立新的 [資源群組]，或選取現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="26c7e-116">You can either create a new **Resource group** or select an existing resource group.</span></span> <span data-ttu-id="26c7e-117">然後選取 [位置] 以便裝載整合帳戶和 [定價層]。</span><span class="sxs-lookup"><span data-stu-id="26c7e-117">Then select a **Location** for hosting your integration account and a **Pricing Tier**.</span></span> 

    <span data-ttu-id="26c7e-118">準備就緒時，請選擇 [建立]。</span><span class="sxs-lookup"><span data-stu-id="26c7e-118">When you're ready, choose **Create**.</span></span>

    ![提供整合帳戶的詳細資料](./media/logic-apps-enterprise-integration-accounts/account-4.png)

    <span data-ttu-id="26c7e-120">Azure 會佈建您的整合帳戶在選取的 hello 的位置，應該在 1 分鐘內完成。</span><span class="sxs-lookup"><span data-stu-id="26c7e-120">Azure provisions your integration account  in hello selected location, which should complete within 1 minute.</span></span>

5. <span data-ttu-id="26c7e-121">重新整理 hello 頁面。</span><span class="sxs-lookup"><span data-stu-id="26c7e-121">Refresh hello page.</span></span> <span data-ttu-id="26c7e-122">您會看到已列出新的整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="26c7e-122">You see your new integration account listed.</span></span>

    ![您的新整合帳戶隨即出現](./media/logic-apps-enterprise-integration-accounts/account-5.png) 

<span data-ttu-id="26c7e-124">接下來，hello 整合帳戶，您建立的 tooyour 邏輯應用程式連結。</span><span class="sxs-lookup"><span data-stu-id="26c7e-124">Next, link hello integration account that you created tooyour logic app.</span></span> 

## <a name="link-an-integration-account-tooa-logic-app"></a><span data-ttu-id="26c7e-125">連結整合帳戶 tooa 邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="26c7e-125">Link an integration account tooa logic app</span></span>

<span data-ttu-id="26c7e-126">toogive toomaps、 結構描述、 合約和其他成品，整合帳戶，連結 hello 整合帳戶 tooyour 邏輯應用程式中的，存取您的 logic apps。</span><span class="sxs-lookup"><span data-stu-id="26c7e-126">toogive your logic apps access toomaps, schemas, agreements, and other artifacts in your integration account, link hello integration account tooyour logic app.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="26c7e-127">必要條件</span><span class="sxs-lookup"><span data-stu-id="26c7e-127">Prerequisites</span></span>

* <span data-ttu-id="26c7e-128">整合帳戶</span><span class="sxs-lookup"><span data-stu-id="26c7e-128">An integration account</span></span>
* <span data-ttu-id="26c7e-129">邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="26c7e-129">A logic app</span></span>

> [!NOTE] 
> <span data-ttu-id="26c7e-130">請確定應用程式整合帳戶和邏輯位於 hello*相同的 Azure 位置*開始之前。</span><span class="sxs-lookup"><span data-stu-id="26c7e-130">Make sure your integration account and logic app are in hello *same Azure location* before you begin.</span></span>


1. <span data-ttu-id="26c7e-131">在 hello Azure 入口網站，選取應用程式邏輯，並檢查邏輯應用程式的位置。</span><span class="sxs-lookup"><span data-stu-id="26c7e-131">In hello Azure portal, select your logic app, and check your logic app's location.</span></span>

    ![選取邏輯應用程式，檢查位置](./media/logic-apps-enterprise-integration-accounts/linkaccount-1.png)

2. <span data-ttu-id="26c7e-133">在 [設定] 之下，選取 [整合帳戶]。</span><span class="sxs-lookup"><span data-stu-id="26c7e-133">Under **Settings**, select **Integration Account**.</span></span>

    ![選取 [整合帳戶]](./media/logic-apps-enterprise-integration-accounts/linkaccount-2.png)

3. <span data-ttu-id="26c7e-135">從 hello**選取整合帳戶**清單，選取 hello 整合帳戶想 toolink tooyour 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="26c7e-135">From hello **Select an Integration account** list, select hello integration account you want toolink tooyour logic app.</span></span> <span data-ttu-id="26c7e-136">toofinish 連結中，選擇**儲存**。</span><span class="sxs-lookup"><span data-stu-id="26c7e-136">toofinish linking, choose **Save**.</span></span>

    ![選取您的整合帳戶](./media/logic-apps-enterprise-integration-accounts/linkaccount-3.png)

    <span data-ttu-id="26c7e-138">您會得到通知帳戶是連結的 tooyour 邏輯應用程式，且整合帳戶中的所有成品都都可以立即可用 tooyour 邏輯應用程式顯示您的整合。</span><span class="sxs-lookup"><span data-stu-id="26c7e-138">You get a notification that shows your integration account is linked tooyour logic app,  and that all artifacts in your integration account are now available tooyour logic app.</span></span>

    ![邏輯應用程式連結 tooyour 整合帳戶](./media/logic-apps-enterprise-integration-accounts/linkaccount-5.png)

<span data-ttu-id="26c7e-140">現在已整合帳戶連結的 tooyour 邏輯應用程式，您可以使用邏輯應用程式中的 hello B2B 連接器。</span><span class="sxs-lookup"><span data-stu-id="26c7e-140">Now that your integration account is linked tooyour logic app, you can use hello B2B connectors in your logic apps.</span></span> <span data-ttu-id="26c7e-141">部分常見的 B2B 連接器包括 XML 驗證和一般檔案編碼/解碼。</span><span class="sxs-lookup"><span data-stu-id="26c7e-141">Some common B2B connectors include XML validation and flat file encode/decode.</span></span>  

## <a name="delete-your-integration-account"></a><span data-ttu-id="26c7e-142">刪除您的整合帳戶</span><span class="sxs-lookup"><span data-stu-id="26c7e-142">Delete your integration account</span></span>

1. <span data-ttu-id="26c7e-143">選取 [更多服務]。</span><span class="sxs-lookup"><span data-stu-id="26c7e-143">Select **More services**.</span></span>

    ![選取 [更多服務]。](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="26c7e-145">在 hello 搜尋方塊中，輸入 「 整合 」 篩選條件。</span><span class="sxs-lookup"><span data-stu-id="26c7e-145">In hello search box, type "integration" for your filter.</span></span> <span data-ttu-id="26c7e-146">在 hello 結果清單中，選取 **整合帳戶**。</span><span class="sxs-lookup"><span data-stu-id="26c7e-146">In hello results list, select **Integration Accounts**.</span></span>

    ![依據 [整合] 篩選，選取 [整合帳戶]](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. <span data-ttu-id="26c7e-148">選取您想 toodelete hello 整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="26c7e-148">Select hello integration account that you want toodelete.</span></span>

    ![選取整合帳戶 toodelete](./media/logic-apps-enterprise-integration-accounts/account-5.png)

4. <span data-ttu-id="26c7e-150">在 hello 功能表上選擇 **刪除**。</span><span class="sxs-lookup"><span data-stu-id="26c7e-150">On hello menu, choose **Delete**.</span></span>

    ![選擇 [刪除]](./media/logic-apps-enterprise-integration-accounts/delete.png)

5. <span data-ttu-id="26c7e-152">確認您的選擇 toodelete hello 整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="26c7e-152">Confirm your choice toodelete hello integration account.</span></span>

## <a name="move-your-integration-account"></a><span data-ttu-id="26c7e-153">移動您的整合帳戶</span><span class="sxs-lookup"><span data-stu-id="26c7e-153">Move your integration account</span></span>

<span data-ttu-id="26c7e-154">toomove 整合帳戶 tooanother Azure 的訂用帳戶或資源群組，請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="26c7e-154">toomove an integration account tooanother Azure subscription or resource group, follow these steps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="26c7e-155">在您移動整合帳戶之後，您必須更新所有指令碼 toouse hello 新的資源 Id。</span><span class="sxs-lookup"><span data-stu-id="26c7e-155">You must update all scripts toouse hello new resource IDs after you move an integration account.</span></span>

1. <span data-ttu-id="26c7e-156">選取 [更多服務]。</span><span class="sxs-lookup"><span data-stu-id="26c7e-156">Select **More services**.</span></span>

    ![選取 [更多服務]。](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="26c7e-158">在 hello 搜尋方塊中，輸入 「 整合 」 篩選條件。</span><span class="sxs-lookup"><span data-stu-id="26c7e-158">In hello search box, type "integration" for your filter.</span></span> <span data-ttu-id="26c7e-159">在 hello 結果清單中，選取 **整合帳戶**。</span><span class="sxs-lookup"><span data-stu-id="26c7e-159">In hello results list, select **Integration Accounts**.</span></span>

    ![依據 [整合] 篩選，選取 [整合帳戶]](./media/logic-apps-enterprise-integration-accounts/account-2.png)

3. <span data-ttu-id="26c7e-161">選取您想 toomove hello 整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="26c7e-161">Select hello integration account that you want toomove.</span></span> <span data-ttu-id="26c7e-162">在 [設定] 之下選擇 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="26c7e-162">Under **Settings**, choose **Properties**.</span></span>

    ![選取整合帳戶 toomove。](./media/logic-apps-enterprise-integration-accounts/move.png)

5. <span data-ttu-id="26c7e-165">變更 hello 資源群組或與整合帳戶相關聯的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="26c7e-165">Change hello resource group or Azure subscription that's associated with your integration account.</span></span>

    ![選擇 [變更資源群組] 或 [變更訂用帳戶]](./media/logic-apps-enterprise-integration-accounts/move-2.png)

## <a name="next-steps"></a><span data-ttu-id="26c7e-167">後續步驟</span><span class="sxs-lookup"><span data-stu-id="26c7e-167">Next Steps</span></span>
* [<span data-ttu-id="26c7e-168">深入了解合約</span><span class="sxs-lookup"><span data-stu-id="26c7e-168">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "了解企業整合合約")  

