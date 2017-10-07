---
title: "aaaDeploy SAP 的 Azure 上的 SAP ERP 6.0 IDE EHP7 SP3 |Microsoft 文件"
description: "在 Azure 上部署適用於 SAP ERP 6.0 的 SAP IDES EHP7 SP3"
services: virtual-machines-windows
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 626c1523-1026-478f-bd8a-22c83b869231
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 09/16/2016
ms.author: hermannd
ms.openlocfilehash: 26d88c7b48a91d35602464c4f89ca7a30502c4b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-sap-ides-ehp7-sp3-for-sap-erp-60-on-azure"></a><span data-ttu-id="3d3b5-103">在 Azure 上部署適用於 SAP ERP 6.0 的 SAP IDES EHP7 SP3</span><span class="sxs-lookup"><span data-stu-id="3d3b5-103">Deploy SAP IDES EHP7 SP3 for SAP ERP 6.0 on Azure</span></span>
<span data-ttu-id="3d3b5-104">本文說明如何 toodeploy SAP 與 SQL Server 和 Windows 作業系統 hello Azure 上執行 hello SAP 雲端應用裝置程式庫 (SAP CAL) 3.0 透過 IDE 系統。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-104">This article describes how toodeploy an SAP IDES system running with SQL Server and hello Windows operating system on Azure via hello SAP Cloud Appliance Library (SAP CAL) 3.0.</span></span> <span data-ttu-id="3d3b5-105">hello 螢幕擷取畫面顯示 hello 逐步程序。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-105">hello screenshots show hello step-by-step process.</span></span> <span data-ttu-id="3d3b5-106">toodeploy 不同的解決方案，請遵循 hello 相同的步驟。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-106">toodeploy a different solution, follow hello same steps.</span></span>

<span data-ttu-id="3d3b5-107">以 hello SAP CAL，請移 toohello toostart [SAP 雲端應用裝置程式庫](https://cal.sap.com/)網站。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-107">toostart with hello SAP CAL, go toohello [SAP Cloud Appliance Library](https://cal.sap.com/) website.</span></span> <span data-ttu-id="3d3b5-108">SAP 也有關於 hello 部落格新[SAP 雲端應用裝置程式庫 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience)。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-108">SAP also has a blog about hello new [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span></span> 

> [!NOTE]
<span data-ttu-id="3d3b5-109">2017 年 29，您可以使用 hello Azure Resource Manager 部署模型，因為除了 toohello 較偏好傳統部署模型 toodeploy hello SAP CAL。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-109">As of May 29, 2017, you can use hello Azure Resource Manager deployment model in addition toohello less-preferred classic deployment model toodeploy hello SAP CAL.</span></span> <span data-ttu-id="3d3b5-110">我們建議您使用 hello 新的資源管理員部署模型，並忽略 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-110">We recommend that you use hello new Resource Manager deployment model and disregard hello classic deployment model.</span></span>

<span data-ttu-id="3d3b5-111">如果您已經建立的 SAP CAL 帳戶使用 hello 傳統模式，*其他 SAP CAL 帳戶需要 toocreate*。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-111">If you already created an SAP CAL account that uses hello classic model, *you need toocreate another SAP CAL account*.</span></span> <span data-ttu-id="3d3b5-112">此帳戶需要 tooexclusively 使用 hello 資源管理員的模型部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-112">This account needs tooexclusively deploy into Azure by using hello Resource Manager model.</span></span>

<span data-ttu-id="3d3b5-113">您登入 toohello SAP CAL 之後，第一頁的 hello 通常會引導您 toohello**解決方案**頁面。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-113">After you sign in toohello SAP CAL, hello first page usually leads you toohello **Solutions** page.</span></span> <span data-ttu-id="3d3b5-114">hello hello SAP CAL 所提供的方案會持續穩定增加，因此您可能需要 tooscroll 稍微 toofind hello 您想的方案。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-114">hello solutions offered on hello SAP CAL are steadily increasing, so you might need tooscroll quite a bit toofind hello solution you want.</span></span> <span data-ttu-id="3d3b5-115">可在 Azure 的 hello 反白顯示 windows SAP IDE 解決方案示範 hello 部署程序：</span><span class="sxs-lookup"><span data-stu-id="3d3b5-115">hello highlighted Windows-based SAP IDES solution that is available exclusively on Azure demonstrates hello deployment process:</span></span>

![SAP CAL 解決方案](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic1.jpg)

### <a name="create-an-account-in-hello-sap-cal"></a><span data-ttu-id="3d3b5-117">Hello SAP CAL 中建立帳戶</span><span class="sxs-lookup"><span data-stu-id="3d3b5-117">Create an account in hello SAP CAL</span></span>
1. <span data-ttu-id="3d3b5-118">中的 hello toohello SAP CAL toosign 第一次，使用 SAP S-使用者或其他使用者註冊與 SAP。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-118">toosign in toohello SAP CAL for hello first time, use your SAP S-User or other user registered with SAP.</span></span> <span data-ttu-id="3d3b5-119">然後定義 hello Azure 上 SAP CAL toodeploy 應用裝置由 SAP CAL 帳戶。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-119">Then define an SAP CAL account that is used by hello SAP CAL toodeploy appliances on Azure.</span></span> <span data-ttu-id="3d3b5-120">在 hello 帳戶定義中，您需要：</span><span class="sxs-lookup"><span data-stu-id="3d3b5-120">In hello account definition, you need to:</span></span>

    <span data-ttu-id="3d3b5-121">a.</span><span class="sxs-lookup"><span data-stu-id="3d3b5-121">a.</span></span> <span data-ttu-id="3d3b5-122">選取 hello Azure （「 資源管理員 」 或 「 傳統 」） 上的部署模型。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-122">Select hello deployment model on Azure (Resource Manager or classic).</span></span>

    <span data-ttu-id="3d3b5-123">b.</span><span class="sxs-lookup"><span data-stu-id="3d3b5-123">b.</span></span> <span data-ttu-id="3d3b5-124">輸入您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-124">Enter your Azure subscription.</span></span> <span data-ttu-id="3d3b5-125">SAP CAL 帳戶可以指派只有 tooone 訂閱。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-125">An SAP CAL account can be assigned tooone subscription only.</span></span> <span data-ttu-id="3d3b5-126">如果您需要多個訂用帳戶，您需要 toocreate SAP CAL 的其他帳戶。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-126">If you need more than one subscription, you need toocreate another SAP CAL account.</span></span>
    
    <span data-ttu-id="3d3b5-127">c.</span><span class="sxs-lookup"><span data-stu-id="3d3b5-127">c.</span></span> <span data-ttu-id="3d3b5-128">提供 hello SAP CAL 權限 toodeploy 到您的 Azure 訂閱。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-128">Give hello SAP CAL permission toodeploy into your Azure subscription.</span></span>

    > [!NOTE]
    <span data-ttu-id="3d3b5-129">hello 接下來的步驟顯示如何 toocreate SAP CAL 帳戶資源管理員部署。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-129">hello next steps show how toocreate an SAP CAL account for Resource Manager deployments.</span></span> <span data-ttu-id="3d3b5-130">如果您已經有 SAP CAL 帳戶是連結的 toohello 傳統部署模型，您*需要*toofollow 這些步驟 toocreate 新 SAP CAL 帳戶。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-130">If you already have an SAP CAL account that is linked toohello classic deployment model, you *need* toofollow these steps toocreate a new SAP CAL account.</span></span> <span data-ttu-id="3d3b5-131">hello 新 SAP CAL 帳戶需要 toodeploy hello 資源管理員模型中。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-131">hello new SAP CAL account needs toodeploy in hello Resource Manager model.</span></span>

2. <span data-ttu-id="3d3b5-132">新的 SAP CAL toocreate 帳戶，hello**帳戶**頁面會顯示 Azure 兩個選擇：</span><span class="sxs-lookup"><span data-stu-id="3d3b5-132">toocreate a new SAP CAL account, hello **Accounts** page shows two choices for Azure:</span></span> 

    <span data-ttu-id="3d3b5-133">a.</span><span class="sxs-lookup"><span data-stu-id="3d3b5-133">a.</span></span> <span data-ttu-id="3d3b5-134">**Microsoft Azure （傳統）** hello 傳統部署模型，而不會再慣用。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-134">**Microsoft Azure (classic)** is hello classic deployment model and is no longer preferred.</span></span>

    <span data-ttu-id="3d3b5-135">b.</span><span class="sxs-lookup"><span data-stu-id="3d3b5-135">b.</span></span> <span data-ttu-id="3d3b5-136">**Microsoft Azure**是 hello 新的資源管理員部署模型。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-136">**Microsoft Azure** is hello new Resource Manager deployment model.</span></span>

    ![SAP CAL 帳戶](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic-2a.PNG)

    <span data-ttu-id="3d3b5-138">toodeploy 在 hello 資源管理員模型中，選取**Microsoft Azure**。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-138">toodeploy in hello Resource Manager model, select **Microsoft Azure**.</span></span>

    ![SAP CAL 帳戶](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic3c.PNG)

3. <span data-ttu-id="3d3b5-140">輸入 hello Azure**訂用帳戶 ID**可以在 hello Azure 入口網站上找到的。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-140">Enter hello Azure **Subscription ID** that can be found on hello Azure portal.</span></span> 

    ![SAP CAL 訂用帳戶識別碼](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic3c.PNG)

4. <span data-ttu-id="3d3b5-142">定義 tooauthorize hello SAP CAL toodeploy 到 hello Azure 訂用帳戶中，按一下**授權**。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-142">tooauthorize hello SAP CAL toodeploy into hello Azure subscription you defined, click **Authorize**.</span></span> <span data-ttu-id="3d3b5-143">hello 遵循頁面上會出現在 hello 瀏覽器索引標籤：</span><span class="sxs-lookup"><span data-stu-id="3d3b5-143">hello following page appears in hello browser tab:</span></span>

    ![Internet Explorer 雲端服務登入](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic4c.PNG)

5. <span data-ttu-id="3d3b5-145">如果列出多個使用者，請選擇屬於 hello 您選取的 Azure 訂用帳戶的連結的 toobe hello coadministrator hello Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-145">If more than one user is listed, choose hello Microsoft account that is linked toobe hello coadministrator of hello Azure subscription you selected.</span></span> <span data-ttu-id="3d3b5-146">hello 遵循頁面上會出現在 hello 瀏覽器索引標籤：</span><span class="sxs-lookup"><span data-stu-id="3d3b5-146">hello following page appears in hello browser tab:</span></span>

    ![Internet Explorer 雲端服務確認](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic5a.PNG)

6. <span data-ttu-id="3d3b5-148">按一下 [接受]。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-148">Click **Accept**.</span></span> <span data-ttu-id="3d3b5-149">Hello 授權是否成功，會再次顯示 hello SAP CAL 帳戶定義。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-149">If hello authorization is successful, hello SAP CAL account definition displays again.</span></span> <span data-ttu-id="3d3b5-150">在一段時間之後, 會出現確認訊息 hello 授權程序成功。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-150">After a short time, a message confirms that hello authorization process was successful.</span></span>

7. <span data-ttu-id="3d3b5-151">tooassign hello 新建立的 SAP CAL 帳戶 tooyour 使用者中，輸入您**使用者識別碼**在 hello hello 右邊的文字方塊中，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-151">tooassign hello newly created SAP CAL account tooyour user, enter your **User ID** in hello text box on hello right and click **Add**.</span></span> 

    ![帳戶 toouser 關聯](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic8a.PNG)

8. <span data-ttu-id="3d3b5-153">tooassociate toohello SAP CAL 用於 toosign 您帳戶的 hello 使用者按一下**檢閱**。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-153">tooassociate your account with hello user that you use toosign in toohello SAP CAL, click **Review**.</span></span> 

9. <span data-ttu-id="3d3b5-154">toocreate hello 關聯使用者與 hello 新建立的 SAP CAL 帳戶，請按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-154">toocreate hello association between your user and hello newly created SAP CAL account, click **Create**.</span></span>

    ![使用者 tooaccount 關聯](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic9b.PNG)

<span data-ttu-id="3d3b5-156">您已成功建立可執行下列作業的 SAP CAL 帳戶：</span><span class="sxs-lookup"><span data-stu-id="3d3b5-156">You successfully created an SAP CAL account that is able to:</span></span>

- <span data-ttu-id="3d3b5-157">使用 hello Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-157">Use hello Resource Manager deployment model.</span></span>
- <span data-ttu-id="3d3b5-158">將 SAP 系統部署到您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-158">Deploy SAP systems into your Azure subscription.</span></span>

> [!NOTE]
<span data-ttu-id="3d3b5-159">您可以部署 Windows 和 SQL Server 為基礎的 hello SAP IDE 解決方案之前，您可能需要 toosign SAP CAL 訂用帳戶註冊。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-159">Before you can deploy hello SAP IDES solution based on Windows and SQL Server, you might need toosign up for an SAP CAL subscription.</span></span> <span data-ttu-id="3d3b5-160">否則，hello 方案可能會顯示為**鎖定**hello 概觀 頁面上。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-160">Otherwise, hello solution might show up as **Locked** on hello overview page.</span></span>

### <a name="deploy-a-solution"></a><span data-ttu-id="3d3b5-161">部署解決方案</span><span class="sxs-lookup"><span data-stu-id="3d3b5-161">Deploy a solution</span></span>
1. <span data-ttu-id="3d3b5-162">您將 SAP CAL 帳戶設定之後，請選取**hello Windows 和 SQL Server 上的 SAP IDE 解決方案**方案。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-162">After you set up an SAP CAL account, select **hello SAP IDES solution on Windows and SQL Server** solution.</span></span> <span data-ttu-id="3d3b5-163">按一下**建立執行個體**，並確認 hello 使用量和詞彙的條件。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-163">Click **Create Instance**, and confirm hello usage and terms conditions.</span></span> 

2. <span data-ttu-id="3d3b5-164">在 hello**基本模式： 建立執行個體**頁面上，您需要：</span><span class="sxs-lookup"><span data-stu-id="3d3b5-164">On hello **Basic Mode: Create Instance** page, you need to:</span></span>

    <span data-ttu-id="3d3b5-165">a.</span><span class="sxs-lookup"><span data-stu-id="3d3b5-165">a.</span></span> <span data-ttu-id="3d3b5-166">輸入執行個體**名稱**。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-166">Enter an instance **Name**.</span></span>

    <span data-ttu-id="3d3b5-167">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-167">b.</span></span> <span data-ttu-id="3d3b5-168">選取 Azure **區域**。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-168">Select an Azure **Region**.</span></span> <span data-ttu-id="3d3b5-169">您可能需要多個 Azure 區域提供 SAP CAL 訂用帳戶 tooget。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-169">You might need an SAP CAL subscription tooget multiple Azure regions offered.</span></span>

    <span data-ttu-id="3d3b5-170">c.</span><span class="sxs-lookup"><span data-stu-id="3d3b5-170">c.</span></span>  <span data-ttu-id="3d3b5-171">輸入 hello master**密碼**hello 方案，如所示：</span><span class="sxs-lookup"><span data-stu-id="3d3b5-171">Enter hello master **Password** for hello solution, as shown:</span></span>

    ![SAP CAL 基本模式：建立執行個體](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic10a.png)

3. <span data-ttu-id="3d3b5-173">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-173">Click **Create**.</span></span> <span data-ttu-id="3d3b5-174">一段時間後 hello 大小和複雜度 hello 方案 (hello SAP CAL 提供的估計值)，根據 hello 狀態會顯示為作用中且可供使用：</span><span class="sxs-lookup"><span data-stu-id="3d3b5-174">After some time, depending on hello size and complexity of hello solution (hello SAP CAL provides an estimate), hello status is shown as active and ready for use:</span></span> 

    ![SAP CAL 執行個體](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic12a.png)

4. <span data-ttu-id="3d3b5-176">toofind hello 資源群組及其所建立的所有物件 hello SAP CAL 資訊，請 toohello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-176">toofind hello resource group and all its objects that were created by hello SAP CAL, go toohello Azure portal.</span></span> <span data-ttu-id="3d3b5-177">開頭為相同執行個體名稱指定在 hello SAP CAL hello 可以找到 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-177">hello virtual machine can be found starting with hello same instance name that was given in hello SAP CAL.</span></span>

    ![資源群組物件](./media/cal-ides-erp6-ehp7-sp3-sql/ides_resource_group.PNG)

5. <span data-ttu-id="3d3b5-179">在 hello SAP CAL 入口網站中，移 toohello 部署執行個體，然後按一下**連接**。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-179">On hello SAP CAL portal, go toohello deployed instances and click **Connect**.</span></span> <span data-ttu-id="3d3b5-180">此時會出現下列快顯視窗中的 hello:</span><span class="sxs-lookup"><span data-stu-id="3d3b5-180">hello following pop-up window appears:</span></span> 

    ![連接 toohello 執行個體](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic14a.PNG)

6. <span data-ttu-id="3d3b5-182">您可以使用其中一個 hello 選項 tooconnect toohello 部署系統之前，請按一下**入門指南**。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-182">Before you can use one of hello options tooconnect toohello deployed systems, click **Getting Started Guide**.</span></span> <span data-ttu-id="3d3b5-183">hello 文件名稱 hello 使用者針對每個 hello 連線方法。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-183">hello documentation names hello users for each of hello connectivity methods.</span></span> <span data-ttu-id="3d3b5-184">hello 密碼，這些使用者會在 hello 開頭 hello 部署程序設定 toohello 您定義的主要密碼。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-184">hello passwords for those users are set toohello master password you defined at hello beginning of hello deployment process.</span></span> <span data-ttu-id="3d3b5-185">在 hello 文件，其他多運作的使用者會列出與他們的密碼，您可以使用在 toohello toosign 部署系統。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-185">In hello documentation, other more functional users are listed with their passwords, which you can use toosign in toohello deployed system.</span></span>

    ![SAP 歡迎使用文件](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic15.jpg)

<span data-ttu-id="3d3b5-187">在幾個小時內，狀況良好的 SAP IDES 系統便會部署在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-187">Within a few hours, a healthy SAP IDES system is deployed in Azure.</span></span>

<span data-ttu-id="3d3b5-188">如果您購買的 SAP CAL 訂用帳戶時，SAP 完全支援透過 hello SAP CAL 部署在 Azure 上。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-188">If you bought an SAP CAL subscription, SAP fully supports deployments through hello SAP CAL on Azure.</span></span> <span data-ttu-id="3d3b5-189">hello 支援佇列是 BC-VCM-CAL。</span><span class="sxs-lookup"><span data-stu-id="3d3b5-189">hello support queue is BC-VCM-CAL.</span></span>

