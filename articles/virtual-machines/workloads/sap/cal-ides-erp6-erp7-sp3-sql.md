---
title: "在 Azure 上部署適用於 SAP ERP 6.0 的 SAP IDES EHP7 SP3 | Microsoft Docs"
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
ms.openlocfilehash: 91eed294077ff72d0760018b10c98f32db88f3be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-sap-ides-ehp7-sp3-for-sap-erp-60-on-azure"></a><span data-ttu-id="76498-103">在 Azure 上部署適用於 SAP ERP 6.0 的 SAP IDES EHP7 SP3</span><span class="sxs-lookup"><span data-stu-id="76498-103">Deploy SAP IDES EHP7 SP3 for SAP ERP 6.0 on Azure</span></span>
<span data-ttu-id="76498-104">本文說明如何透過 SAP Cloud Appliance Library (SAP CAL) 3.0 在 Azure 上部署與 SQL Server 和 Windows 作業系統搭配執行的 SAP IDES 系統。</span><span class="sxs-lookup"><span data-stu-id="76498-104">This article describes how to deploy an SAP IDES system running with SQL Server and the Windows operating system on Azure via the SAP Cloud Appliance Library (SAP CAL) 3.0.</span></span> <span data-ttu-id="76498-105">螢幕擷取畫面會顯示逐步程序。</span><span class="sxs-lookup"><span data-stu-id="76498-105">The screenshots show the step-by-step process.</span></span> <span data-ttu-id="76498-106">若要部署不同的解決方案，請遵循相同的步驟。</span><span class="sxs-lookup"><span data-stu-id="76498-106">To deploy a different solution, follow the same steps.</span></span>

<span data-ttu-id="76498-107">若要開始使用 SAP CAL，請前往 [SAP Cloud Appliance Library](https://cal.sap.com/) 網站。</span><span class="sxs-lookup"><span data-stu-id="76498-107">To start with the SAP CAL, go to the [SAP Cloud Appliance Library](https://cal.sap.com/) website.</span></span> <span data-ttu-id="76498-108">SAP 也有關於全新 [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience) 的部落格。</span><span class="sxs-lookup"><span data-stu-id="76498-108">SAP also has a blog about the new [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span></span> 

> [!NOTE]
<span data-ttu-id="76498-109">自 2017 年 5 月 29 日起，除了較不建議使用的傳統部署模型外，您還可以使用 Azure Resource Manager 部署模型來部署 SAP CAL。</span><span class="sxs-lookup"><span data-stu-id="76498-109">As of May 29, 2017, you can use the Azure Resource Manager deployment model in addition to the less-preferred classic deployment model to deploy the SAP CAL.</span></span> <span data-ttu-id="76498-110">我們建議您使用新的 Resource Manager 部署模型，而不要使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="76498-110">We recommend that you use the new Resource Manager deployment model and disregard the classic deployment model.</span></span>

<span data-ttu-id="76498-111">如果您已建立使用傳統模型的 SAP CAL 帳戶，則必須建立其他 SAP CAL 帳戶。</span><span class="sxs-lookup"><span data-stu-id="76498-111">If you already created an SAP CAL account that uses the classic model, *you need to create another SAP CAL account*.</span></span> <span data-ttu-id="76498-112">您必須使用 Resource Manager 模型，以獨佔方式將此帳戶部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="76498-112">This account needs to exclusively deploy into Azure by using the Resource Manager model.</span></span>

<span data-ttu-id="76498-113">在登入 SAP CAL 之後，第一個頁面通常會帶您進入 [解決方案] 頁面。</span><span class="sxs-lookup"><span data-stu-id="76498-113">After you sign in to the SAP CAL, the first page usually leads you to the **Solutions** page.</span></span> <span data-ttu-id="76498-114">SAP CAL 上所提供的解決方案會不斷增加，所以您可能必須捲動很久才能找到您要的解決方案。</span><span class="sxs-lookup"><span data-stu-id="76498-114">The solutions offered on the SAP CAL are steadily increasing, so you might need to scroll quite a bit to find the solution you want.</span></span> <span data-ttu-id="76498-115">反白顯示的 Azure 專用 Windows 型 SAP IDE 解決方案會示範部署程序：</span><span class="sxs-lookup"><span data-stu-id="76498-115">The highlighted Windows-based SAP IDES solution that is available exclusively on Azure demonstrates the deployment process:</span></span>

![SAP CAL 解決方案](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic1.jpg)

### <a name="create-an-account-in-the-sap-cal"></a><span data-ttu-id="76498-117">在 SAP CAL 中建立帳戶</span><span class="sxs-lookup"><span data-stu-id="76498-117">Create an account in the SAP CAL</span></span>
1. <span data-ttu-id="76498-118">若要第一次進行 SAP CAL 登入，請使用您的 SAP S-User 或其他已向 SAP 註冊的使用者。</span><span class="sxs-lookup"><span data-stu-id="76498-118">To sign in to the SAP CAL for the first time, use your SAP S-User or other user registered with SAP.</span></span> <span data-ttu-id="76498-119">然後定義 SAP CAL 帳戶，以供 SAP CAL 用來在 Azure 上部署應用裝置。</span><span class="sxs-lookup"><span data-stu-id="76498-119">Then define an SAP CAL account that is used by the SAP CAL to deploy appliances on Azure.</span></span> <span data-ttu-id="76498-120">在帳戶定義中，您需要：</span><span class="sxs-lookup"><span data-stu-id="76498-120">In the account definition, you need to:</span></span>

    <span data-ttu-id="76498-121">a.</span><span class="sxs-lookup"><span data-stu-id="76498-121">a.</span></span> <span data-ttu-id="76498-122">選取 Azure 上的部署模型 (Resource Manager 或傳統)。</span><span class="sxs-lookup"><span data-stu-id="76498-122">Select the deployment model on Azure (Resource Manager or classic).</span></span>

    <span data-ttu-id="76498-123">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="76498-123">b.</span></span> <span data-ttu-id="76498-124">輸入您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="76498-124">Enter your Azure subscription.</span></span> <span data-ttu-id="76498-125">一個 SAP CAL 帳戶只能指派給一個訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="76498-125">An SAP CAL account can be assigned to one subscription only.</span></span> <span data-ttu-id="76498-126">如果您需要多個訂用帳戶，則必須另外建立 SAP CAL 帳戶。</span><span class="sxs-lookup"><span data-stu-id="76498-126">If you need more than one subscription, you need to create another SAP CAL account.</span></span>
    
    <span data-ttu-id="76498-127">c.</span><span class="sxs-lookup"><span data-stu-id="76498-127">c.</span></span> <span data-ttu-id="76498-128">賦予 SAP CAL 部署到 Azure 訂用帳戶的權限。</span><span class="sxs-lookup"><span data-stu-id="76498-128">Give the SAP CAL permission to deploy into your Azure subscription.</span></span>

    > [!NOTE]
    <span data-ttu-id="76498-129">接下來的步驟會示範如何針對 Resource Manager 部署建立 SAP CAL 帳戶。</span><span class="sxs-lookup"><span data-stu-id="76498-129">The next steps show how to create an SAP CAL account for Resource Manager deployments.</span></span> <span data-ttu-id="76498-130">如果您已有連結至傳統部署模型的 SAP CAL 帳戶，則您「必須」遵循下列步驟來建立新的 SAP CAL 帳戶。</span><span class="sxs-lookup"><span data-stu-id="76498-130">If you already have an SAP CAL account that is linked to the classic deployment model, you *need* to follow these steps to create a new SAP CAL account.</span></span> <span data-ttu-id="76498-131">新的 SAP CAL 帳戶必須以 Resource Manager 模式部署。</span><span class="sxs-lookup"><span data-stu-id="76498-131">The new SAP CAL account needs to deploy in the Resource Manager model.</span></span>

2. <span data-ttu-id="76498-132">若要建立新的 SAP CAL 帳戶，[帳戶] 頁面會顯示兩個適用於 Azure 的選項：</span><span class="sxs-lookup"><span data-stu-id="76498-132">To create a new SAP CAL account, the **Accounts** page shows two choices for Azure:</span></span> 

    <span data-ttu-id="76498-133">a.</span><span class="sxs-lookup"><span data-stu-id="76498-133">a.</span></span> <span data-ttu-id="76498-134">**Microsoft Azure (傳統)** 是傳統部署模型，目前不再建議使用。</span><span class="sxs-lookup"><span data-stu-id="76498-134">**Microsoft Azure (classic)** is the classic deployment model and is no longer preferred.</span></span>

    <span data-ttu-id="76498-135">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="76498-135">b.</span></span> <span data-ttu-id="76498-136">**Microsoft Azure** 是新的 Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="76498-136">**Microsoft Azure** is the new Resource Manager deployment model.</span></span>

    ![SAP CAL 帳戶](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic-2a.PNG)

    <span data-ttu-id="76498-138">若要在 Resource Manager 模型中部署，請選取 [Microsoft Azure]。</span><span class="sxs-lookup"><span data-stu-id="76498-138">To deploy in the Resource Manager model, select **Microsoft Azure**.</span></span>

    ![SAP CAL 帳戶](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic3c.PNG)

3. <span data-ttu-id="76498-140">輸入可在 Azure 入口網站上找到的 Azure **訂用帳戶識別碼**。</span><span class="sxs-lookup"><span data-stu-id="76498-140">Enter the Azure **Subscription ID** that can be found on the Azure portal.</span></span> 

    ![SAP CAL 訂用帳戶識別碼](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic3c.PNG)

4. <span data-ttu-id="76498-142">若要授權 SAP CAL 部署到您所定義的 Azure 訂用帳戶，請按一下 [授權]。</span><span class="sxs-lookup"><span data-stu-id="76498-142">To authorize the SAP CAL to deploy into the Azure subscription you defined, click **Authorize**.</span></span> <span data-ttu-id="76498-143">瀏覽器索引標籤中會出現下列頁面：</span><span class="sxs-lookup"><span data-stu-id="76498-143">The following page appears in the browser tab:</span></span>

    ![Internet Explorer 雲端服務登入](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic4c.PNG)

5. <span data-ttu-id="76498-145">如果頁面中列出多個使用者，請選擇連結至成為您所選 Azure 訂用帳戶共同管理員的 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="76498-145">If more than one user is listed, choose the Microsoft account that is linked to be the coadministrator of the Azure subscription you selected.</span></span> <span data-ttu-id="76498-146">瀏覽器索引標籤中會出現下列頁面：</span><span class="sxs-lookup"><span data-stu-id="76498-146">The following page appears in the browser tab:</span></span>

    ![Internet Explorer 雲端服務確認](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic5a.PNG)

6. <span data-ttu-id="76498-148">按一下 [接受]。</span><span class="sxs-lookup"><span data-stu-id="76498-148">Click **Accept**.</span></span> <span data-ttu-id="76498-149">如果授權成功，SAP CAL 帳戶定義便會再次顯示。</span><span class="sxs-lookup"><span data-stu-id="76498-149">If the authorization is successful, the SAP CAL account definition displays again.</span></span> <span data-ttu-id="76498-150">片刻之後便會出現訊息來確認授權程序已成功。</span><span class="sxs-lookup"><span data-stu-id="76498-150">After a short time, a message confirms that the authorization process was successful.</span></span>

7. <span data-ttu-id="76498-151">若要將新建立的 SAP CAL 帳戶指派給您的使用者，請在右邊的文字方塊中輸入您的 [使用者識別碼]，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="76498-151">To assign the newly created SAP CAL account to your user, enter your **User ID** in the text box on the right and click **Add**.</span></span> 

    ![帳戶與使用者的關聯](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic8a.PNG)

8. <span data-ttu-id="76498-153">若要讓您的帳戶與您用來登入 SAP CAL 的使用者產生關聯，請按一下 [檢閱]。</span><span class="sxs-lookup"><span data-stu-id="76498-153">To associate your account with the user that you use to sign in to the SAP CAL, click **Review**.</span></span> 

9. <span data-ttu-id="76498-154">若要在使用者與新建立的 SAP CAL 帳戶之間建立關聯，請按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="76498-154">To create the association between your user and the newly created SAP CAL account, click **Create**.</span></span>

    ![使用者與帳戶的關聯](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic9b.PNG)

<span data-ttu-id="76498-156">您已成功建立可執行下列作業的 SAP CAL 帳戶：</span><span class="sxs-lookup"><span data-stu-id="76498-156">You successfully created an SAP CAL account that is able to:</span></span>

- <span data-ttu-id="76498-157">使用 Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="76498-157">Use the Resource Manager deployment model.</span></span>
- <span data-ttu-id="76498-158">將 SAP 系統部署到您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="76498-158">Deploy SAP systems into your Azure subscription.</span></span>

> [!NOTE]
<span data-ttu-id="76498-159">您可能需要先註冊 SAP CAL 訂用帳戶，才可以部署以 Windows 和 SQL Server 為基礎的 SAP IDES 解決方案。</span><span class="sxs-lookup"><span data-stu-id="76498-159">Before you can deploy the SAP IDES solution based on Windows and SQL Server, you might need to sign up for an SAP CAL subscription.</span></span> <span data-ttu-id="76498-160">否則在概觀頁面上，解決方案可能會顯示為 [已鎖定]。</span><span class="sxs-lookup"><span data-stu-id="76498-160">Otherwise, the solution might show up as **Locked** on the overview page.</span></span>

### <a name="deploy-a-solution"></a><span data-ttu-id="76498-161">部署解決方案</span><span class="sxs-lookup"><span data-stu-id="76498-161">Deploy a solution</span></span>
1. <span data-ttu-id="76498-162">在設定 SAP CAL 帳戶之後，請選取 [Windows 和 SQL Server 上的 SAP IDES 解決方案] 解決方案。</span><span class="sxs-lookup"><span data-stu-id="76498-162">After you set up an SAP CAL account, select **The SAP IDES solution on Windows and SQL Server** solution.</span></span> <span data-ttu-id="76498-163">按一下 [建立執行個體]，並確認使用條款和條件。</span><span class="sxs-lookup"><span data-stu-id="76498-163">Click **Create Instance**, and confirm the usage and terms conditions.</span></span> 

2. <span data-ttu-id="76498-164">在 [基本模式: 建立執行個體] 頁面上，您必須：</span><span class="sxs-lookup"><span data-stu-id="76498-164">On the **Basic Mode: Create Instance** page, you need to:</span></span>

    <span data-ttu-id="76498-165">a.</span><span class="sxs-lookup"><span data-stu-id="76498-165">a.</span></span> <span data-ttu-id="76498-166">輸入執行個體**名稱**。</span><span class="sxs-lookup"><span data-stu-id="76498-166">Enter an instance **Name**.</span></span>

    <span data-ttu-id="76498-167">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="76498-167">b.</span></span> <span data-ttu-id="76498-168">選取 Azure **區域**。</span><span class="sxs-lookup"><span data-stu-id="76498-168">Select an Azure **Region**.</span></span> <span data-ttu-id="76498-169">您可能需要 SAP CAL 訂用帳戶才能取得所提供的多個 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="76498-169">You might need an SAP CAL subscription to get multiple Azure regions offered.</span></span>

    <span data-ttu-id="76498-170">c.</span><span class="sxs-lookup"><span data-stu-id="76498-170">c.</span></span>  <span data-ttu-id="76498-171">輸入解決方案的主要**密碼**，如下所示：</span><span class="sxs-lookup"><span data-stu-id="76498-171">Enter the master **Password** for the solution, as shown:</span></span>

    ![SAP CAL 基本模式：建立執行個體](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic10a.png)

3. <span data-ttu-id="76498-173">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="76498-173">Click **Create**.</span></span> <span data-ttu-id="76498-174">在一段時間之後，視解決方案的大小和複雜性 (SAP CAL 會提供預估) 而定，狀態將會顯示為作用中並可供使用：</span><span class="sxs-lookup"><span data-stu-id="76498-174">After some time, depending on the size and complexity of the solution (the SAP CAL provides an estimate), the status is shown as active and ready for use:</span></span> 

    ![SAP CAL 執行個體](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic12a.png)

4. <span data-ttu-id="76498-176">若要尋找 SAP CAL 所建立的資源群組及其所有物件，請移至 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="76498-176">To find the resource group and all its objects that were created by the SAP CAL, go to the Azure portal.</span></span> <span data-ttu-id="76498-177">您會發現以 SAP CAL 中所提供的相同執行個體名稱開頭的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="76498-177">The virtual machine can be found starting with the same instance name that was given in the SAP CAL.</span></span>

    ![資源群組物件](./media/cal-ides-erp6-ehp7-sp3-sql/ides_resource_group.PNG)

5. <span data-ttu-id="76498-179">在 SAP CAL 入口網站中，移至已部署的執行個體，然後按一下 [連線]。</span><span class="sxs-lookup"><span data-stu-id="76498-179">On the SAP CAL portal, go to the deployed instances and click **Connect**.</span></span> <span data-ttu-id="76498-180">下列快顯視窗隨即出現：</span><span class="sxs-lookup"><span data-stu-id="76498-180">The following pop-up window appears:</span></span> 

    ![連線到執行個體](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic14a.PNG)

6. <span data-ttu-id="76498-182">請先按一下 [開始使用指南]，之後您才能使用其中一個選項來連線至已部署的系統。</span><span class="sxs-lookup"><span data-stu-id="76498-182">Before you can use one of the options to connect to the deployed systems, click **Getting Started Guide**.</span></span> <span data-ttu-id="76498-183">文件會指出每個連線方法的使用者。</span><span class="sxs-lookup"><span data-stu-id="76498-183">The documentation names the users for each of the connectivity methods.</span></span> <span data-ttu-id="76498-184">這些使用者的密碼會設定為您在部署程序開始時所定義的主要密碼。</span><span class="sxs-lookup"><span data-stu-id="76498-184">The passwords for those users are set to the master password you defined at the beginning of the deployment process.</span></span> <span data-ttu-id="76498-185">文件中會另外列出多名功能使用者及其密碼，以供您用來登入已部署的系統。</span><span class="sxs-lookup"><span data-stu-id="76498-185">In the documentation, other more functional users are listed with their passwords, which you can use to sign in to the deployed system.</span></span>

    ![SAP 歡迎使用文件](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic15.jpg)

<span data-ttu-id="76498-187">在幾個小時內，狀況良好的 SAP IDES 系統便會部署在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="76498-187">Within a few hours, a healthy SAP IDES system is deployed in Azure.</span></span>

<span data-ttu-id="76498-188">如果您已購買 SAP CAL 訂用帳戶，SAP 便可完全支援透過 SAP CAL 在 Azure 上進行部署。</span><span class="sxs-lookup"><span data-stu-id="76498-188">If you bought an SAP CAL subscription, SAP fully supports deployments through the SAP CAL on Azure.</span></span> <span data-ttu-id="76498-189">支援佇列是 BC-VCM-CAL。</span><span class="sxs-lookup"><span data-stu-id="76498-189">The support queue is BC-VCM-CAL.</span></span>

