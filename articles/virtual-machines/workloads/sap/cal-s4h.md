---
title: "SAP S/4HANA 或 Azure VM 上的 BW/4HANA aaaDeploy |Microsoft 文件"
description: "在 Azure VM 上部署 SAP S/4HANA 或 BW/4HANA"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 44bbd2b6-a376-4b5c-b824-e76917117fa9
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 09/15/2016
ms.author: hermannd
ms.openlocfilehash: 7e57f7daa7667b7c7dbcb86f6892a54e4295b74c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-sap-s4hana-or-bw4hana-on-azure"></a><span data-ttu-id="a11d6-103">在 Azure 上部署 SAP S/4HANA 或 BW/4HANA</span><span class="sxs-lookup"><span data-stu-id="a11d6-103">Deploy SAP S/4HANA or BW/4HANA on Azure</span></span>
<span data-ttu-id="a11d6-104">本文說明如何使用 toodeploy 在 Azure 上的 S/4HANA hello SAP 雲端應用裝置程式庫 (SAP CAL) 3.0。</span><span class="sxs-lookup"><span data-stu-id="a11d6-104">This article describes how toodeploy S/4HANA on Azure by using hello SAP Cloud Appliance Library (SAP CAL) 3.0.</span></span> <span data-ttu-id="a11d6-105">toodeploy 其他 SAP HANA 為基礎的解決方案，例如 BW/4HANA，遵循 hello 相同的步驟。</span><span class="sxs-lookup"><span data-stu-id="a11d6-105">toodeploy other SAP HANA-based solutions, such as BW/4HANA, follow hello same steps.</span></span>

> [!NOTE]
<span data-ttu-id="a11d6-106">如需 hello SAP CAL 的詳細資訊，請移至 toohello [SAP 雲端應用裝置程式庫](https://cal.sap.com/)網站。</span><span class="sxs-lookup"><span data-stu-id="a11d6-106">For more information about hello SAP CAL, go toohello [SAP Cloud Appliance Library](https://cal.sap.com/) website.</span></span> <span data-ttu-id="a11d6-107">SAP 也有關於 hello 部落格[SAP 雲端應用裝置程式庫 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience)。</span><span class="sxs-lookup"><span data-stu-id="a11d6-107">SAP also has a blog about hello [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span></span>

> [!NOTE]
<span data-ttu-id="a11d6-108">2017 年 29，您可以使用 hello Azure Resource Manager 部署模型，因為除了 toohello 較偏好傳統部署模型 toodeploy hello SAP CAL。</span><span class="sxs-lookup"><span data-stu-id="a11d6-108">As of May 29, 2017, you can use hello Azure Resource Manager deployment model in addition toohello less-preferred classic deployment model toodeploy hello SAP CAL.</span></span> <span data-ttu-id="a11d6-109">我們建議您使用 hello 新的資源管理員部署模型，並忽略 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="a11d6-109">We recommend that you use hello new Resource Manager deployment model and disregard hello classic deployment model.</span></span>

## <a name="step-by-step-process-toodeploy-hello-solution"></a><span data-ttu-id="a11d6-110">逐步程序 toodeploy hello 解決方案</span><span class="sxs-lookup"><span data-stu-id="a11d6-110">Step-by-step process toodeploy hello solution</span></span>

<span data-ttu-id="a11d6-111">hello 下列螢幕擷取畫面的順序顯示如何使用 toodeploy 在 Azure 上的 S/4HANA hello SAP CAL。</span><span class="sxs-lookup"><span data-stu-id="a11d6-111">hello following sequence of screenshots shows you how toodeploy S/4HANA on Azure by using hello SAP CAL.</span></span> <span data-ttu-id="a11d6-112">hello 程序的運作 hello 其他解決方案，例如 BW/4HANA 相同的方式。</span><span class="sxs-lookup"><span data-stu-id="a11d6-112">hello process works hello same way for other solutions, such as BW/4HANA.</span></span>

<span data-ttu-id="a11d6-113">hello**解決方案**頁面會顯示某些 hello SAP CAL HANA 為基礎的解決方案可在 Azure 上。</span><span class="sxs-lookup"><span data-stu-id="a11d6-113">hello **Solutions** page shows some of hello SAP CAL HANA-based solutions available on Azure.</span></span> <span data-ttu-id="a11d6-114">**SAP S/4HANA 1610 FPS01，Fully-Activated 應用裝置**位於 hello 中間的資料列：</span><span class="sxs-lookup"><span data-stu-id="a11d6-114">**SAP S/4HANA 1610 FPS01, Fully-Activated Appliance** is in hello middle row:</span></span>

![SAP CAL 解決方案](./media/cal-s4h/s4h-pic-1c.png)

### <a name="create-an-account-in-hello-sap-cal"></a><span data-ttu-id="a11d6-116">Hello SAP CAL 中建立帳戶</span><span class="sxs-lookup"><span data-stu-id="a11d6-116">Create an account in hello SAP CAL</span></span>
1. <span data-ttu-id="a11d6-117">中的 hello toohello SAP CAL toosign 第一次，使用 SAP S-使用者或其他使用者註冊與 SAP。</span><span class="sxs-lookup"><span data-stu-id="a11d6-117">toosign in toohello SAP CAL for hello first time, use your SAP S-User or other user registered with SAP.</span></span> <span data-ttu-id="a11d6-118">然後定義 hello Azure 上 SAP CAL toodeploy 應用裝置由 SAP CAL 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a11d6-118">Then define an SAP CAL account that is used by hello SAP CAL toodeploy appliances on Azure.</span></span> <span data-ttu-id="a11d6-119">在 hello 帳戶定義中，您需要：</span><span class="sxs-lookup"><span data-stu-id="a11d6-119">In hello account definition, you need to:</span></span>

    <span data-ttu-id="a11d6-120">a.</span><span class="sxs-lookup"><span data-stu-id="a11d6-120">a.</span></span> <span data-ttu-id="a11d6-121">選取 hello Azure （「 資源管理員 」 或 「 傳統 」） 上的部署模型。</span><span class="sxs-lookup"><span data-stu-id="a11d6-121">Select hello deployment model on Azure (Resource Manager or classic).</span></span>

    <span data-ttu-id="a11d6-122">b.</span><span class="sxs-lookup"><span data-stu-id="a11d6-122">b.</span></span> <span data-ttu-id="a11d6-123">輸入您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="a11d6-123">Enter your Azure subscription.</span></span> <span data-ttu-id="a11d6-124">SAP CAL 帳戶可以指派只有 tooone 訂閱。</span><span class="sxs-lookup"><span data-stu-id="a11d6-124">An SAP CAL account can be assigned tooone subscription only.</span></span> <span data-ttu-id="a11d6-125">如果您需要多個訂用帳戶，您需要 toocreate SAP CAL 的其他帳戶。</span><span class="sxs-lookup"><span data-stu-id="a11d6-125">If you need more than one subscription, you need toocreate another SAP CAL account.</span></span>

    <span data-ttu-id="a11d6-126">c.</span><span class="sxs-lookup"><span data-stu-id="a11d6-126">c.</span></span> <span data-ttu-id="a11d6-127">提供 hello SAP CAL 權限 toodeploy 到您的 Azure 訂閱。</span><span class="sxs-lookup"><span data-stu-id="a11d6-127">Give hello SAP CAL permission toodeploy into your Azure subscription.</span></span>

    > [!NOTE]
    <span data-ttu-id="a11d6-128">hello 接下來的步驟顯示如何 toocreate SAP CAL 帳戶資源管理員部署。</span><span class="sxs-lookup"><span data-stu-id="a11d6-128">hello next steps show how toocreate an SAP CAL account for Resource Manager deployments.</span></span> <span data-ttu-id="a11d6-129">如果您已經有 SAP CAL 帳戶是連結的 toohello 傳統部署模型，您*需要*toofollow 這些步驟 toocreate 新 SAP CAL 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a11d6-129">If you already have an SAP CAL account that is linked toohello classic deployment model, you *need* toofollow these steps toocreate a new SAP CAL account.</span></span> <span data-ttu-id="a11d6-130">hello 新 SAP CAL 帳戶需要 toodeploy hello 資源管理員模型中。</span><span class="sxs-lookup"><span data-stu-id="a11d6-130">hello new SAP CAL account needs toodeploy in hello Resource Manager model.</span></span>

2. <span data-ttu-id="a11d6-131">建立新的 SAP CAL 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a11d6-131">Create a new SAP CAL account.</span></span> <span data-ttu-id="a11d6-132">hello**帳戶**頁面會顯示 Azure 三個選項：</span><span class="sxs-lookup"><span data-stu-id="a11d6-132">hello **Accounts** page shows three choices for Azure:</span></span> 

    <span data-ttu-id="a11d6-133">a.</span><span class="sxs-lookup"><span data-stu-id="a11d6-133">a.</span></span> <span data-ttu-id="a11d6-134">**Microsoft Azure （傳統）** hello 傳統部署模型，而不會再慣用。</span><span class="sxs-lookup"><span data-stu-id="a11d6-134">**Microsoft Azure (classic)** is hello classic deployment model and is no longer preferred.</span></span>

    <span data-ttu-id="a11d6-135">b.</span><span class="sxs-lookup"><span data-stu-id="a11d6-135">b.</span></span> <span data-ttu-id="a11d6-136">**Microsoft Azure**是 hello 新的資源管理員部署模型。</span><span class="sxs-lookup"><span data-stu-id="a11d6-136">**Microsoft Azure** is hello new Resource Manager deployment model.</span></span>

    <span data-ttu-id="a11d6-137">c.</span><span class="sxs-lookup"><span data-stu-id="a11d6-137">c.</span></span> <span data-ttu-id="a11d6-138">**Windows Azure 由 21Vianet 運作**是中國使用 hello 傳統部署模型中的選項。</span><span class="sxs-lookup"><span data-stu-id="a11d6-138">**Windows Azure operated by 21Vianet** is an option in China that uses hello classic deployment model.</span></span>

    <span data-ttu-id="a11d6-139">toodeploy 在 hello 資源管理員模型中，選取**Microsoft Azure**。</span><span class="sxs-lookup"><span data-stu-id="a11d6-139">toodeploy in hello Resource Manager model, select **Microsoft Azure**.</span></span>

    ![SAP CAL 帳戶詳細資料](./media/cal-s4h/s4h-pic-2a.png)

3. <span data-ttu-id="a11d6-141">輸入 hello Azure**訂用帳戶 ID**可以在 hello Azure 入口網站上找到的。</span><span class="sxs-lookup"><span data-stu-id="a11d6-141">Enter hello Azure **Subscription ID** that can be found on hello Azure portal.</span></span>

   ![SAP CAL 帳戶](./media/cal-s4h/s4h-pic3c.png)

4. <span data-ttu-id="a11d6-143">定義 tooauthorize hello SAP CAL toodeploy 到 hello Azure 訂用帳戶中，按一下**授權**。</span><span class="sxs-lookup"><span data-stu-id="a11d6-143">tooauthorize hello SAP CAL toodeploy into hello Azure subscription you defined, click **Authorize**.</span></span> <span data-ttu-id="a11d6-144">hello 遵循頁面上會出現在 hello 瀏覽器索引標籤：</span><span class="sxs-lookup"><span data-stu-id="a11d6-144">hello following page appears in hello browser tab:</span></span>

   ![Internet Explorer 雲端服務登入](./media/cal-s4h/s4h-pic4c.png)

5. <span data-ttu-id="a11d6-146">如果列出多個使用者，請選擇屬於 hello 您選取的 Azure 訂用帳戶的連結的 toobe hello coadministrator hello Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a11d6-146">If more than one user is listed, choose hello Microsoft account that is linked toobe hello coadministrator of hello Azure subscription you selected.</span></span> <span data-ttu-id="a11d6-147">hello 遵循頁面上會出現在 hello 瀏覽器索引標籤：</span><span class="sxs-lookup"><span data-stu-id="a11d6-147">hello following page appears in hello browser tab:</span></span>

   ![Internet Explorer 雲端服務確認](./media/cal-s4h/s4h-pic5a.png)

6. <span data-ttu-id="a11d6-149">按一下 [接受]。</span><span class="sxs-lookup"><span data-stu-id="a11d6-149">Click **Accept**.</span></span> <span data-ttu-id="a11d6-150">Hello 授權是否成功，會再次顯示 hello SAP CAL 帳戶定義。</span><span class="sxs-lookup"><span data-stu-id="a11d6-150">If hello authorization is successful, hello SAP CAL account definition displays again.</span></span> <span data-ttu-id="a11d6-151">在一段時間之後, 會出現確認訊息 hello 授權程序成功。</span><span class="sxs-lookup"><span data-stu-id="a11d6-151">After a short time, a message confirms that hello authorization process was successful.</span></span>

7. <span data-ttu-id="a11d6-152">tooassign hello 新建立的 SAP CAL 帳戶 tooyour 使用者中，輸入您**使用者識別碼**在 hello hello 右邊的文字方塊中，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="a11d6-152">tooassign hello newly created SAP CAL account tooyour user, enter your **User ID** in hello text box on hello right and click **Add**.</span></span>

   ![帳戶 toouser 關聯](./media/cal-s4h/s4h-pic8a.png)

8. <span data-ttu-id="a11d6-154">tooassociate toohello SAP CAL 用於 toosign 您帳戶的 hello 使用者按一下**檢閱**。</span><span class="sxs-lookup"><span data-stu-id="a11d6-154">tooassociate your account with hello user that you use toosign in toohello SAP CAL, click **Review**.</span></span> 
 
9. <span data-ttu-id="a11d6-155">toocreate hello 關聯使用者與 hello 新建立的 SAP CAL 帳戶，請按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="a11d6-155">toocreate hello association between your user and hello newly created SAP CAL account, click **Create**.</span></span>

   ![使用者 tooSAP CAL 帳戶關聯](./media/cal-s4h/s4h-pic9b.png)

<span data-ttu-id="a11d6-157">您已成功建立可執行下列作業的 SAP CAL 帳戶：</span><span class="sxs-lookup"><span data-stu-id="a11d6-157">You successfully created an SAP CAL account that is able to:</span></span>

- <span data-ttu-id="a11d6-158">使用 hello Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="a11d6-158">Use hello Resource Manager deployment model.</span></span>
- <span data-ttu-id="a11d6-159">將 SAP 系統部署到您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="a11d6-159">Deploy SAP systems into your Azure subscription.</span></span>

<span data-ttu-id="a11d6-160">現在您可以開始 toodeploy S/4HANA 到您在 Azure 中的使用者訂閱。</span><span class="sxs-lookup"><span data-stu-id="a11d6-160">Now you can start toodeploy S/4HANA into your user subscription in Azure.</span></span>

> [!NOTE]
<span data-ttu-id="a11d6-161">在繼續之前，請先確定您是否有適用於 Azure H 系列 VM 的 Azure 核心配額。</span><span class="sxs-lookup"><span data-stu-id="a11d6-161">Before you continue, determine whether you have Azure core quotas for Azure H-Series VMs.</span></span> <span data-ttu-id="a11d6-162">在 hello 的時刻，hello SAP CAL 使用的 Azure Vm H 數列 toodeploy 某些 hello SAP HANA 為基礎的解決方案。</span><span class="sxs-lookup"><span data-stu-id="a11d6-162">At hello moment, hello SAP CAL uses H-Series VMs of Azure toodeploy some of hello SAP HANA-based solutions.</span></span> <span data-ttu-id="a11d6-163">您的 Azure 訂用帳戶可能沒有 H 系列的核心配額。</span><span class="sxs-lookup"><span data-stu-id="a11d6-163">Your Azure subscription might not have any H-Series core quotas for H-Series.</span></span> <span data-ttu-id="a11d6-164">如果是這樣，您可能需要 toocontact Azure 支援 tooget H 系列的最少 16 個核心的配額。</span><span class="sxs-lookup"><span data-stu-id="a11d6-164">If so, you might need toocontact Azure support tooget a quota of at least 16 H-Series cores.</span></span>

> [!NOTE]
<span data-ttu-id="a11d6-165">當您部署在 Azure 中 SAP CAL hello 的解決方案時，您可能會發現，您可以選擇只有一個 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="a11d6-165">When you deploy a solution on Azure in hello SAP CAL, you might find that you can choose only one Azure region.</span></span> <span data-ttu-id="a11d6-166">其中一個 hello SAP CAL 所建議 toodeploy 成 hello 以外的 Azure 區域，，您需要 toopurchase 從 SAP CAL 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="a11d6-166">toodeploy into Azure regions other than hello one suggested by hello SAP CAL, you need toopurchase a CAL subscription from SAP.</span></span> <span data-ttu-id="a11d6-167">您也可能需要 tooopen SAP toohave 訊息您 CAL 帳戶啟用 toodeliver 成 hello 一開始建議的項目以外的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="a11d6-167">You also might need tooopen a message with SAP toohave your CAL account enabled toodeliver into Azure regions other than hello ones initially suggested.</span></span>

### <a name="deploy-a-solution"></a><span data-ttu-id="a11d6-168">部署解決方案</span><span class="sxs-lookup"><span data-stu-id="a11d6-168">Deploy a solution</span></span>

<span data-ttu-id="a11d6-169">讓我們來部署解決方案從 hello**解決方案**hello SAP CAL 的頁面。</span><span class="sxs-lookup"><span data-stu-id="a11d6-169">Let's deploy a solution from hello **Solutions** page of hello SAP CAL.</span></span> <span data-ttu-id="a11d6-170">hello SAP CAL 有兩個序列 toodeploy:</span><span class="sxs-lookup"><span data-stu-id="a11d6-170">hello SAP CAL has two sequences toodeploy:</span></span>

- <span data-ttu-id="a11d6-171">都使用一個頁面 toodefine hello 系統 toobe 部署的基本順序</span><span class="sxs-lookup"><span data-stu-id="a11d6-171">A basic sequence that uses one page toodefine hello system toobe deployed</span></span>
- <span data-ttu-id="a11d6-172">進階順序則會有某些 VM 大小可供您選擇</span><span class="sxs-lookup"><span data-stu-id="a11d6-172">An advanced sequence that gives you certain choices on VM sizes</span></span> 

<span data-ttu-id="a11d6-173">我們將示範 hello 基本路徑 toodeployment。</span><span class="sxs-lookup"><span data-stu-id="a11d6-173">We demonstrate hello basic path toodeployment here.</span></span>

1. <span data-ttu-id="a11d6-174">在 hello**帳戶詳細資料**頁面上，您需要：</span><span class="sxs-lookup"><span data-stu-id="a11d6-174">On hello **Account Details** page, you need to:</span></span>

    <span data-ttu-id="a11d6-175">a.</span><span class="sxs-lookup"><span data-stu-id="a11d6-175">a.</span></span> <span data-ttu-id="a11d6-176">選取 SAP CAL 帳戶 </span><span class="sxs-lookup"><span data-stu-id="a11d6-176">Select an SAP CAL account.</span></span> <span data-ttu-id="a11d6-177">（使用 hello Resource Manager 部署模型與相關聯的 toodeploy 帳戶）。</span><span class="sxs-lookup"><span data-stu-id="a11d6-177">(Use an account that is associated toodeploy with hello Resource Manager deployment model.)</span></span>

    <span data-ttu-id="a11d6-178">b.</span><span class="sxs-lookup"><span data-stu-id="a11d6-178">b.</span></span> <span data-ttu-id="a11d6-179">輸入執行個體**名稱**。</span><span class="sxs-lookup"><span data-stu-id="a11d6-179">Enter an instance **Name**.</span></span>

    <span data-ttu-id="a11d6-180">c.</span><span class="sxs-lookup"><span data-stu-id="a11d6-180">c.</span></span> <span data-ttu-id="a11d6-181">選取 Azure **區域**。</span><span class="sxs-lookup"><span data-stu-id="a11d6-181">Select an Azure **Region**.</span></span> <span data-ttu-id="a11d6-182">hello SAP CAL 會建議一個區域。</span><span class="sxs-lookup"><span data-stu-id="a11d6-182">hello SAP CAL suggests a region.</span></span> <span data-ttu-id="a11d6-183">如果您需要另一個 Azure 區域，而且您不需要在 SAP CAL 訂用帳戶，您需要與 SAP tooorder CAL 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="a11d6-183">If you need another Azure region and you don't have an SAP CAL subscription, you need tooorder a CAL subscription with SAP.</span></span>

    <span data-ttu-id="a11d6-184">d.</span><span class="sxs-lookup"><span data-stu-id="a11d6-184">d.</span></span> <span data-ttu-id="a11d6-185">輸入主要**密碼**8 或 9 個字元的 hello 解決方案。</span><span class="sxs-lookup"><span data-stu-id="a11d6-185">Enter a master **Password** for hello solution of eight or nine characters.</span></span> <span data-ttu-id="a11d6-186">hello hello 不同元件的系統管理員，使用 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="a11d6-186">hello password is used for hello administrators of hello different components.</span></span>

   ![SAP CAL 基本模式：建立執行個體](./media/cal-s4h/s4h-pic10a.png)

2. <span data-ttu-id="a11d6-188">按一下**建立**，在出現的 hello 訊息方塊中按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="a11d6-188">Click **Create**, and in hello message box that appears, click **OK**.</span></span>

   ![SAP CAL 支援的 VM 大小](./media/cal-s4h/s4h-pic10b.png)

3. <span data-ttu-id="a11d6-190">在 hello**私密金鑰**對話方塊中，按一下**存放區**toostore hello 私密金鑰 hello SAP CAL。</span><span class="sxs-lookup"><span data-stu-id="a11d6-190">In hello **Private Key** dialog box, click **Store** toostore hello private key in hello SAP CAL.</span></span> <span data-ttu-id="a11d6-191">按一下 toouse hello 私用金鑰的密碼保護**下載**。</span><span class="sxs-lookup"><span data-stu-id="a11d6-191">toouse password protection for hello private key, click **Download**.</span></span> 

   ![SAP CAL 私密金鑰](./media/cal-s4h/s4h-pic10c.png)

4. <span data-ttu-id="a11d6-193">讀取 hello SAP CAL**警告**訊息，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="a11d6-193">Read hello SAP CAL **Warning** message, and click **OK**.</span></span>

   ![SAP CAL 警告](./media/cal-s4h/s4h-pic10d.png)

    <span data-ttu-id="a11d6-195">現在 hello 部署就會發生。</span><span class="sxs-lookup"><span data-stu-id="a11d6-195">Now hello deployment takes place.</span></span> <span data-ttu-id="a11d6-196">一段時間後 hello 大小和複雜度 hello 方案 (hello SAP CAL 提供的估計值)，根據 hello 顯示狀態為作用中且可供使用。</span><span class="sxs-lookup"><span data-stu-id="a11d6-196">After some time, depending on hello size and complexity of hello solution (hello SAP CAL provides an estimate), hello status is shown as active and ready for use.</span></span>

5. <span data-ttu-id="a11d6-197">toofind hello 虛擬機器，以收集 hello 一個資源群組中其他相關聯的資源，請移 toohello Azure 入口網站：</span><span class="sxs-lookup"><span data-stu-id="a11d6-197">toofind hello virtual machines collected with hello other associated resources in one resource group, go toohello Azure portal:</span></span> 

   ![Hello 新入口網站中部署的 SAP CAL 物件](./media/cal-s4h/sapcaldeplyment_portalview.png)

6. <span data-ttu-id="a11d6-199">在 hello SAP CAL 入口網站，hello 狀態會顯示為**Active**。</span><span class="sxs-lookup"><span data-stu-id="a11d6-199">On hello SAP CAL portal, hello status appears as **Active**.</span></span> <span data-ttu-id="a11d6-200">tooconnect toohello 方案中，按一下 **連接**。</span><span class="sxs-lookup"><span data-stu-id="a11d6-200">tooconnect toohello solution, click **Connect**.</span></span> <span data-ttu-id="a11d6-201">不同的選項 tooconnect toohello 不同元件部署這個方案中。</span><span class="sxs-lookup"><span data-stu-id="a11d6-201">Different options tooconnect toohello different components are deployed within this solution.</span></span>

   ![SAP CAL 執行個體](./media/cal-s4h/active_solution.png)

7. <span data-ttu-id="a11d6-203">您可以使用其中一個 hello 選項 tooconnect toohello 部署系統之前，請按一下**入門指南**。</span><span class="sxs-lookup"><span data-stu-id="a11d6-203">Before you can use one of hello options tooconnect toohello deployed systems, click **Getting Started Guide**.</span></span> 

   ![連接 toohello 執行個體](./media/cal-s4h/connect_to_solution.png)

    <span data-ttu-id="a11d6-205">hello 文件名稱 hello 使用者針對每個 hello 連線方法。</span><span class="sxs-lookup"><span data-stu-id="a11d6-205">hello documentation names hello users for each of hello connectivity methods.</span></span> <span data-ttu-id="a11d6-206">hello 密碼，這些使用者會在 hello 開頭 hello 部署程序設定 toohello 您定義的主要密碼。</span><span class="sxs-lookup"><span data-stu-id="a11d6-206">hello passwords for those users are set toohello master password you defined at hello beginning of hello deployment process.</span></span> <span data-ttu-id="a11d6-207">在 hello 文件，其他多運作的使用者會列出與他們的密碼，您可以使用在 toohello toosign 部署系統。</span><span class="sxs-lookup"><span data-stu-id="a11d6-207">In hello documentation, other more functional users are listed with their passwords, which you can use toosign in toohello deployed system.</span></span> 

    <span data-ttu-id="a11d6-208">例如，如果您使用 hello 已預先安裝 SAP GUI hello Windows 遠端桌面的電腦上，hello S/4 系統看起來可能像這樣：</span><span class="sxs-lookup"><span data-stu-id="a11d6-208">For example, if you use hello SAP GUI that's preinstalled on hello Windows Remote Desktop machine, hello S/4 system might look like this:</span></span>

   ![在 hello SM50 預先安裝 SAP GUI](./media/cal-s4h/gui_sm50.png)

    <span data-ttu-id="a11d6-210">或者，如果您使用 hello DBACockpit，hello 執行個體可能會看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="a11d6-210">Or if you use hello DBACockpit, hello instance might look like this:</span></span>

   ![在 hello DBACockpit SAP GUI SM50](./media/cal-s4h/dbacockpit.png)

<span data-ttu-id="a11d6-212">在幾個小時內，狀況良好的 SAP S/4 應用裝置便會部署在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="a11d6-212">Within a few hours, a healthy SAP S/4 appliance is deployed in Azure.</span></span>

<span data-ttu-id="a11d6-213">如果您購買的 SAP CAL 訂用帳戶時，SAP 完全支援透過 hello SAP CAL 部署在 Azure 上。</span><span class="sxs-lookup"><span data-stu-id="a11d6-213">If you bought an SAP CAL subscription, SAP fully supports deployments through hello SAP CAL on Azure.</span></span> <span data-ttu-id="a11d6-214">hello 支援佇列是 BC-VCM-CAL。</span><span class="sxs-lookup"><span data-stu-id="a11d6-214">hello support queue is BC-VCM-CAL.</span></span>






