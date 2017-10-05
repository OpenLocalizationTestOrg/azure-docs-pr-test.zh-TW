---
title: "在應用程式服務中相應放大背景工作角色 - Azure Stack | Microsoft Docs"
description: "調整 Azure Stack 應用程式服務的詳細指導方針"
services: azure-stack
documentationcenter: 
author: kathm
manager: slinehan
editor: anwestg
ms.assetid: 3cbe87bd-8ae2-47dc-a367-51e67ed4b3c0
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/6/2017
ms.author: kathm
ms.openlocfilehash: f844658c6ad2529fd385476be63095bdae7c88e5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="app-service-on-azure-stack-adding-more-worker-roles"></a><span data-ttu-id="173c1-103">Azure Stack 上的 App Service：新增更多背景工作角色</span><span class="sxs-lookup"><span data-stu-id="173c1-103">App Service on Azure Stack: Adding more worker roles</span></span> 

<span data-ttu-id="173c1-104">此文件提供如何調整 Azure Stack 上之 App Service 背景工作角色的相關指示。</span><span class="sxs-lookup"><span data-stu-id="173c1-104">This document provides instructions about how to scale App Service on Azure Stack worker roles.</span></span> <span data-ttu-id="173c1-105">其中包含建立額外的背景工作角色以支援任何規模之應用程式的步驟。</span><span class="sxs-lookup"><span data-stu-id="173c1-105">It contains steps for creating additional worker roles to support applications of any size.</span></span>

> [!NOTE]
> <span data-ttu-id="173c1-106">如果您 Azure Stack POC 環境的 RAM 未超過 96 GB，您可能很難增加額外的容量。</span><span class="sxs-lookup"><span data-stu-id="173c1-106">If your Azure Stack POC Environment does not have more than 96-GB RAM you may have difficulties adding additional capacity.</span></span>

<span data-ttu-id="173c1-107">根據預設值，Azure Stack 上的 App Service 支援免費和共用背景工作角色層。</span><span class="sxs-lookup"><span data-stu-id="173c1-107">App Service on Azure Stack, by default, supports free and shared worker tiers.</span></span> <span data-ttu-id="173c1-108">若要新增其他背景工作角色層，您需要新增更多背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="173c1-108">To add other worker tiers, you need to add more worker roles.</span></span>

<span data-ttu-id="173c1-109">如果您不確定已透過 Azure Stack 安裝上的預設 App Service 部署了哪個背景工作層，您可以在 [Azure Stack 上的 App Service 概觀](azure-stack-app-service-overview.md)中檢閱其他資訊。</span><span class="sxs-lookup"><span data-stu-id="173c1-109">If you are not sure what was deployed with the default App Service on Azure Stack installation, you can review additional information in the [App Service on Azure Stack overview](azure-stack-app-service-overview.md).</span></span>

<span data-ttu-id="173c1-110">有兩種方式可將額外的容量新增至 Azure Stack 上的 App Service：</span><span class="sxs-lookup"><span data-stu-id="173c1-110">There are two ways to add additional capacity to App Service on Azure Stack:</span></span>
1.  <span data-ttu-id="173c1-111">[直接從 App Service 資源提供者系統管理內新增其他背景工作角色](#Add-additional-workers-directly-from-within-the-App-Service-Resource-Provider-Admin)。</span><span class="sxs-lookup"><span data-stu-id="173c1-111">[Add additional workers directly from with within the App Service Resource Provider Admin](#Add-additional-workers-directly-from-within-the-App-Service-Resource-Provider-Admin).</span></span>
2.  <span data-ttu-id="173c1-112">[手動建立其他的 VM，並將它們新增到 App Service 資源提供者](#Create-additional-VMs-manually-and-add-them-to-the-App-Service-Resource-Provider)。</span><span class="sxs-lookup"><span data-stu-id="173c1-112">[Create additional VMs manually and add them to the App Service Resource Provider](#Create-additional-VMs-manually-and-add-them-to-the-App-Service-Resource-Provider).</span></span>

## <a name="add-additional-workers-directly-within-the-app-service-resource-provider-admin"></a><span data-ttu-id="173c1-113">直接在 App Service 資源提供者系統管理內新增其他背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="173c1-113">Add additional workers directly within the App Service Resource Provider Admin.</span></span>

1.  <span data-ttu-id="173c1-114">以服務管理員身分登入 Azure Stack 入口網站。</span><span class="sxs-lookup"><span data-stu-id="173c1-114">Log in to the Azure Stack portal as the service administrator;</span></span>
2.  <span data-ttu-id="173c1-115">瀏覽至 [資源提供者]，然後選取 [App Service 資源提供者管理]。</span><span class="sxs-lookup"><span data-stu-id="173c1-115">Browse to **Resource Providers** and select the **App Service Resource Provider Admin**.</span></span> <span data-ttu-id="173c1-116">![Azure Stack 資源提供者][1]</span><span class="sxs-lookup"><span data-stu-id="173c1-116">![Azure Stack Resource Providers][1]</span></span>
3.  <span data-ttu-id="173c1-117">按一下 [角色]。</span><span class="sxs-lookup"><span data-stu-id="173c1-117">Click **Roles**.</span></span>  <span data-ttu-id="173c1-118">您可以在這裡看到所有已部署之 App Service 角色的明細。</span><span class="sxs-lookup"><span data-stu-id="173c1-118">Here you see the breakdown of all App Service roles deployed.</span></span>
4.  <span data-ttu-id="173c1-119">按一下 [新的角色執行個體] 選項 ![新增角色執行個體][2]</span><span class="sxs-lookup"><span data-stu-id="173c1-119">Click the option **New Role Instance** ![Add new role instance][2]</span></span>
5.  <span data-ttu-id="173c1-120">在 [新的角色執行個體] 刀鋒視窗中：</span><span class="sxs-lookup"><span data-stu-id="173c1-120">In the **New Role Instance** blade:</span></span>
    1. <span data-ttu-id="173c1-121">選擇您想要新增多少個額外的**角色執行個體**。</span><span class="sxs-lookup"><span data-stu-id="173c1-121">Choose how many additional **role instances** you would like to add.</span></span>  <span data-ttu-id="173c1-122">在此預覽中，上限是 10 個。</span><span class="sxs-lookup"><span data-stu-id="173c1-122">In the preview, there is a maximum of 10.</span></span>
    2. <span data-ttu-id="173c1-123">選取**角色類型**。</span><span class="sxs-lookup"><span data-stu-id="173c1-123">Select the **role type**.</span></span>  <span data-ttu-id="173c1-124">在此預覽中，已將此選項限制為 [Web 背景工作]。</span><span class="sxs-lookup"><span data-stu-id="173c1-124">In this preview, this option is limited to Web Worker.</span></span>
    3. <span data-ttu-id="173c1-125">選取您想要部署這個背景工作的**背景工作層**，預設選項為 [小型]、[中型]、[大型] 或 [共用]。</span><span class="sxs-lookup"><span data-stu-id="173c1-125">Select the **worker tier** you would like to deploy this worker into, default choices are Small, Medium, Large, or Shared.</span></span>  <span data-ttu-id="173c1-126">如果您已建立自己的背景工作層，也可選取您的背景工作層。</span><span class="sxs-lookup"><span data-stu-id="173c1-126">If, you have created your own worker tiers, your worker tiers will also be available for selection.</span></span>
    4. <span data-ttu-id="173c1-127">按一下 [確定] 以部署額外的背景工作</span><span class="sxs-lookup"><span data-stu-id="173c1-127">Click **OK** to deploy the additional workers</span></span>
6.  <span data-ttu-id="173c1-128">Azure Stack 上的 App Service 現在將會新增額外的 VM、設定它們、安裝所有必要的軟體，並在完成此程序時將它們標示為就緒。</span><span class="sxs-lookup"><span data-stu-id="173c1-128">App Service on Azure Stack will now add the additional VMs, configure them, install all the required software and mark them as ready when this process is complete.</span></span>  <span data-ttu-id="173c1-129">此程序大約需要 80 分鐘。</span><span class="sxs-lookup"><span data-stu-id="173c1-129">This process can take approximately 80 minutes.</span></span>
7.  <span data-ttu-id="173c1-130">您可以檢視 [角色] 刀鋒視窗中的背景工作，來監視整備新背景工作的進度。</span><span class="sxs-lookup"><span data-stu-id="173c1-130">You can monitor the progress of the readiness of the new workers by viewing the workers in the **roles** blade.</span></span>

>[!NOTE]
>  <span data-ttu-id="173c1-131">在此預覽中，已將整合的 [新的角色執行個體] 流程限制為 [背景工作角色]，而且只會部署 A1 大小的 VM。</span><span class="sxs-lookup"><span data-stu-id="173c1-131">In this preview, the integrated New Role Instance flow is limited to Worker Roles and deploy VMs of size A1 only.</span></span>  <span data-ttu-id="173c1-132">我們將在未來版本中擴充此功能。</span><span class="sxs-lookup"><span data-stu-id="173c1-132">We will be expanding this capability in a future release.</span></span>

## <a name="manually-adding-additional-capacity-to-app-service-on-azure-stack"></a><span data-ttu-id="173c1-133">手動將額外的容量新增到 Azure Stack 上的 App Service。</span><span class="sxs-lookup"><span data-stu-id="173c1-133">Manually adding additional capacity to App Service on Azure Stack.</span></span>

<span data-ttu-id="173c1-134">以下為新增額外角色所需的步驟：</span><span class="sxs-lookup"><span data-stu-id="173c1-134">The following steps are required to add additional roles:</span></span>

1. [<span data-ttu-id="173c1-135">建立新的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="173c1-135">Create a new virtual machine</span></span>](#step-1-create-a-new-vm-to-support-the-new-instance-size)
2. [<span data-ttu-id="173c1-136">設定虛擬機器</span><span class="sxs-lookup"><span data-stu-id="173c1-136">Configure the virtual machine</span></span>](#step-2-configure-the-virtual-machine)
3. [<span data-ttu-id="173c1-137">在 Azure Stack 入口網站中設定 Web 背景工作角色</span><span class="sxs-lookup"><span data-stu-id="173c1-137">Configure the web worker role in the Azure Stack portal</span></span>](#step-3-configure-the-web-worker-role-in-the-azure-stack-portal)
4. [<span data-ttu-id="173c1-138">設定 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="173c1-138">Configure app service plans</span></span>](#step-4-configure-app-service-plans)

## <a name="step-1-create-a-new-vm-to-support-the-new-instance-size"></a><span data-ttu-id="173c1-139">步驟 1：建立新的 VM 以支援新的執行個體大小</span><span class="sxs-lookup"><span data-stu-id="173c1-139">Step 1: Create a new VM to support the new instance size</span></span>
<span data-ttu-id="173c1-140">如[此文章](azure-stack-provision-vm.md)中所述的方式建立虛擬機器，確保會進行下列選擇：</span><span class="sxs-lookup"><span data-stu-id="173c1-140">Create a virtual machine as described in [this article](azure-stack-provision-vm.md), ensuring that the following selections are made:</span></span>

* <span data-ttu-id="173c1-141">使用者名稱和密碼：提供您在安裝 Azure Stack 上的 App Service 時所提供的相同使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="173c1-141">User name and password: Provide the same user name and password you provided when you installed App Service on Azure Stack.</span></span>
* <span data-ttu-id="173c1-142">訂用帳戶：使用預設的提供者訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="173c1-142">Subscription: Use the default provider subscription.</span></span>
* <span data-ttu-id="173c1-143">資源群組：選擇 [AppService-LOCAL]。</span><span class="sxs-lookup"><span data-stu-id="173c1-143">Resource group: Choose **AppService-LOCAL**.</span></span>

> [!NOTE]
> <span data-ttu-id="173c1-144">將適用於背景工作角色的虛擬機器儲存在與要部署 Azure Stack 上之 App Service 相同的資源群組中</span><span class="sxs-lookup"><span data-stu-id="173c1-144">Store the virtual machines for worker roles in the same resource group as App Service on Azure Stack is deployed to.</span></span> <span data-ttu-id="173c1-145">(這是適用於此版本的建議作法)。</span><span class="sxs-lookup"><span data-stu-id="173c1-145">(This is recommended for this release.)</span></span>
> 
> 

## <a name="step-2-configure-the-virtual-machine"></a><span data-ttu-id="173c1-146">步驟 2：設定虛擬機器</span><span class="sxs-lookup"><span data-stu-id="173c1-146">Step 2: Configure the Virtual Machine</span></span>
<span data-ttu-id="173c1-147">一旦完成部署，必須進行下列設定，才能支援 Web 背景工作角色：</span><span class="sxs-lookup"><span data-stu-id="173c1-147">Once the deployment has completed, the following configuration is required to support the web worker role:</span></span>

1. <span data-ttu-id="173c1-148">瀏覽至入口網站中的 [AppService-LOCAL] 資源群組，並選取您在步驟 1 中建立新的機器。</span><span class="sxs-lookup"><span data-stu-id="173c1-148">Browse to the **AppService-LOCAL** resource group in the portal and select the new machine you created in Step 1.</span></span>
2. <span data-ttu-id="173c1-149">按一下 VM 刀鋒視窗中的 [連線]，以下載遠端桌面設定檔。</span><span class="sxs-lookup"><span data-stu-id="173c1-149">Click connect in the VM blade to download the remote desktop profile.</span></span>  <span data-ttu-id="173c1-150">開啟設定檔，以便開啟您 VM 的遠端桌面工作階段。</span><span class="sxs-lookup"><span data-stu-id="173c1-150">Open the profile to open a remote desktop session to your VM.</span></span>
3. <span data-ttu-id="173c1-151">使用您在步驟 1 中指定的使用者名稱和密碼來登入 VM。</span><span class="sxs-lookup"><span data-stu-id="173c1-151">Log in to the VM using the username and password you specified in Step 1.</span></span>
4. <span data-ttu-id="173c1-152">依序按一下 [開始] 按鈕並輸入 PowerShell 來開啟 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="173c1-152">Open PowerShell by clicking the **Start** button and typing PowerShell.</span></span> <span data-ttu-id="173c1-153">以滑鼠右鍵按一下 [PowerShell.exe]，然後選取 [以系統管理員身分執行]，在系統管理員模式中開啟 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="173c1-153">Right-click **PowerShell.exe**, and select **Run as administrator** to open PowerShell in administrator mode.</span></span>
5. <span data-ttu-id="173c1-154">複製下列每個命令 (一次一個) 並貼至 PowerShell 視窗，然後按 Enter：</span><span class="sxs-lookup"><span data-stu-id="173c1-154">Copy and paste each of the following commands (one at a time) into the PowerShell window, and press enter:</span></span>
   
   ```netsh advfirewall firewall set rule group="File and Printer Sharing" new enable=Yes```
   ```netsh advfirewall firewall set rule group="Windows Management Instrumentation (WMI)" new enable=yes```
   ```reg add HKLM\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion\\Policies\\system /v LocalAccountTokenFilterPolicy /t REG\_DWORD /d 1 /f```
   
6. <span data-ttu-id="173c1-155">關閉您的遠端桌面工作階段。</span><span class="sxs-lookup"><span data-stu-id="173c1-155">Close your remote desktop session.</span></span>
7. <span data-ttu-id="173c1-156">從入口網站重新啟動 VM。</span><span class="sxs-lookup"><span data-stu-id="173c1-156">Restart the VM from the portal.</span></span>

> [!NOTE]
> <span data-ttu-id="173c1-157">這些是針對 Azure Stack 上之 App Service 的最低需求。</span><span class="sxs-lookup"><span data-stu-id="173c1-157">These are minimum requirements for App Service on Azure Stack.</span></span> <span data-ttu-id="173c1-158">它們是 Azure Stack 所含之 Windows 2012 R2 映像的預設設定。</span><span class="sxs-lookup"><span data-stu-id="173c1-158">They are the default settings of the Windows 2012 R2 image included with Azure Stack.</span></span> <span data-ttu-id="173c1-159">這些指示已提供來供日後參考，也可供使用不同映像的那些情況使用。</span><span class="sxs-lookup"><span data-stu-id="173c1-159">The instructions have been provided for future reference, and for those using a different image.</span></span>
> 
> 

## <a name="step-3-configure-the-worker-role-in-the-azure-stack-portal"></a><span data-ttu-id="173c1-160">步驟 3：在 Azure Stack 入口網站中設定背景工作角色</span><span class="sxs-lookup"><span data-stu-id="173c1-160">Step 3: Configure the worker role in the Azure Stack portal</span></span>
1. <span data-ttu-id="173c1-161">在 **ClientVM** 中，以服務管理員身分開啟入口網站。</span><span class="sxs-lookup"><span data-stu-id="173c1-161">Open the portal as the service administrator on **ClientVM**.</span></span>
2. <span data-ttu-id="173c1-162">瀏覽至 [資源提供者] &gt; [App Service 資源提供者系統管理]。![App Service 資源提供者系統管理][3]</span><span class="sxs-lookup"><span data-stu-id="173c1-162">Navigate to **Resource Providers** &gt; **App Service Resource Provider Admin**.![App Service Resource Provider Admin][3]</span></span>
3. <span data-ttu-id="173c1-163">在 [設定] 刀鋒視窗中，按一下 [角色]。![App Service 資源提供者角色][4]</span><span class="sxs-lookup"><span data-stu-id="173c1-163">In the settings blade, click **Roles**.![App Service Resource Provider Roles][4]</span></span>
4. <span data-ttu-id="173c1-164">按一下 [新增角色執行個體]。</span><span class="sxs-lookup"><span data-stu-id="173c1-164">Click **Add Role Instance**.</span></span>
5. <span data-ttu-id="173c1-165">在 [伺服器名稱] 文字方塊中，輸入您稍早建立 (在區段 1 中) 之伺服器的 **IP 位址**。</span><span class="sxs-lookup"><span data-stu-id="173c1-165">In the textbox for **Server Name** enter the **IP Address** of the server you created earlier (in Section 1).</span></span>
6. <span data-ttu-id="173c1-166">選取您想要新增的**角色類型**：控制器、管理伺服器、前端、Web 背景工作、發行者或檔案伺服器。</span><span class="sxs-lookup"><span data-stu-id="173c1-166">Select the **Role Type** you would like to add - Controller, Management Server, Front End, Web Worker, Publisher, or File Server.</span></span>  <span data-ttu-id="173c1-167">在此範例中，請選取 [Web 背景工作]。</span><span class="sxs-lookup"><span data-stu-id="173c1-167">In this instance, select Web Worker.</span></span>
7. <span data-ttu-id="173c1-168">按一下您想要部署新執行個體的 [階層] \(小型、中型、大型或共用)。</span><span class="sxs-lookup"><span data-stu-id="173c1-168">Click the **Tier** you would like to deploy the new instance to (small, medium, large, or shared).</span></span>  <span data-ttu-id="173c1-169">如果您已建立自己的背景工作層，也可選取這些背景工作層。</span><span class="sxs-lookup"><span data-stu-id="173c1-169">If you have created your own worker tiers these will also be available for selection.</span></span>
8. <span data-ttu-id="173c1-170">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="173c1-170">Click **OK.**</span></span>
9. <span data-ttu-id="173c1-171">返回 [角色] 檢視</span><span class="sxs-lookup"><span data-stu-id="173c1-171">Go back to the **Roles** view</span></span>
10. <span data-ttu-id="173c1-172">按一下對應至您已指派 VM 之 [角色類型] 與 [背景工作層] 組合的資料列。</span><span class="sxs-lookup"><span data-stu-id="173c1-172">Click the row corresponding to the Role Type and Worker Tier combination you assigned your VM to.</span></span>
11. <span data-ttu-id="173c1-173">尋找您剛新增的伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="173c1-173">Look for the Server Name you just added.</span></span> <span data-ttu-id="173c1-174">檢閱 [狀態] 欄，並在狀態成為「就緒」之後移至下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="173c1-174">Review the status column, and wait to move to the next step until the status is "Ready."</span></span> <span data-ttu-id="173c1-175">這大約需要 80 分鐘。</span><span class="sxs-lookup"><span data-stu-id="173c1-175">This can take approximately 80 minutes.</span></span> <span data-ttu-id="173c1-176">![App Service 資源提供者角色就緒][5]</span><span class="sxs-lookup"><span data-stu-id="173c1-176">![App Service Resource Provider Role Ready][5]</span></span>

## <a name="step-4-configure-app-service-plans"></a><span data-ttu-id="173c1-177">步驟 4：設定 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="173c1-177">Step 4: Configure app service plans</span></span>

1. <span data-ttu-id="173c1-178">登入 ClientVM 上的入口網站。</span><span class="sxs-lookup"><span data-stu-id="173c1-178">Sign in to the portal on the ClientVM.</span></span>
2. <span data-ttu-id="173c1-179">瀏覽至 [新增] &gt; [Web 與行動裝置]。</span><span class="sxs-lookup"><span data-stu-id="173c1-179">Navigate to **New** &gt; **Web and Mobile**.</span></span>
3. <span data-ttu-id="173c1-180">選取您想要部署的應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="173c1-180">Select the type of application you would like to deploy.</span></span>
4. <span data-ttu-id="173c1-181">提供應用程式的資訊，然後選取 [AppService 方案 / 位置]。</span><span class="sxs-lookup"><span data-stu-id="173c1-181">Provide the information for the application, and then select **AppService Plan / Location**.</span></span>
    1. <span data-ttu-id="173c1-182">按一下 [新建] 。</span><span class="sxs-lookup"><span data-stu-id="173c1-182">Click **Create New**.</span></span>
    2. <span data-ttu-id="173c1-183">建立您的方案，選取方案的對應定價層。</span><span class="sxs-lookup"><span data-stu-id="173c1-183">Create your plan, selecting the corresponding pricing tier for the plan.</span></span>

> [!NOTE]
> <span data-ttu-id="173c1-184">您可以在此刀鋒視窗上建立多個方案。</span><span class="sxs-lookup"><span data-stu-id="173c1-184">You can create multiple plans while on this blade.</span></span> <span data-ttu-id="173c1-185">不過，在部署之前，請確定您已選取適當的方案。</span><span class="sxs-lookup"><span data-stu-id="173c1-185">Before you deploy, however, ensure you have selected the appropriate plan.</span></span>
> 
> 

<span data-ttu-id="173c1-186">以下顯示的是預設可用的多個定價層範例。</span><span class="sxs-lookup"><span data-stu-id="173c1-186">The following shows an example of the multiple pricing tiers available by default.</span></span>  <span data-ttu-id="173c1-187">您會注意到，如果特定的背景工作層沒有可用的背景工作，就無法使用選擇對應定價層的選項。</span><span class="sxs-lookup"><span data-stu-id="173c1-187">You notice that if there are no available workers for a particular worker tier, the option to choose the corresponding pricing tier is unavailable.</span></span>![Azure Stack 上的 App Service 預設定價層][6]

<!--Image references-->
[1]: ./media/azure-stack-app-service-add-worker-roles/azure-stack-resource-providers.png
[2]: ./media/azure-stack-app-service-add-worker-roles/app-service-new-role-instance.png
[3]: ./media/azure-stack-app-service-add-worker-roles/app-service-resource-provider-admin.png
[4]: ./media/azure-stack-app-service-add-worker-roles/app-service-resource-provider-roles.png
[5]: ./media/azure-stack-app-service-add-worker-roles/app-service-resource-provider-role-ready.png
[6]: ./media/azure-stack-app-service-add-worker-roles/app-service-resource-provider-pricing-tier.png
