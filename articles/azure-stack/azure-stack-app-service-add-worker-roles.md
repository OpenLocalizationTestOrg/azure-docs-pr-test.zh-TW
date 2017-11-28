---
title: "應用程式服務-Azure 堆疊中的背景工作角色出 aaaScale |Microsoft 文件"
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
ms.openlocfilehash: 252b4a531655e38f3a3747f8a04b16fc6303f9e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-on-azure-stack-adding-more-worker-roles"></a><span data-ttu-id="d78be-103">Azure Stack 上的 App Service：新增更多背景工作角色</span><span class="sxs-lookup"><span data-stu-id="d78be-103">App Service on Azure Stack: Adding more worker roles</span></span> 

<span data-ttu-id="d78be-104">本文件提供有關如何指示 tooscale 應用程式服務堆疊 Azure 工作者角色上的。</span><span class="sxs-lookup"><span data-stu-id="d78be-104">This document provides instructions about how tooscale App Service on Azure Stack worker roles.</span></span> <span data-ttu-id="d78be-105">它包含建立額外的背景工作角色 toosupport 應用程式的任何大小的步驟。</span><span class="sxs-lookup"><span data-stu-id="d78be-105">It contains steps for creating additional worker roles toosupport applications of any size.</span></span>

> [!NOTE]
> <span data-ttu-id="d78be-106">如果您 Azure Stack POC 環境的 RAM 未超過 96 GB，您可能很難增加額外的容量。</span><span class="sxs-lookup"><span data-stu-id="d78be-106">If your Azure Stack POC Environment does not have more than 96-GB RAM you may have difficulties adding additional capacity.</span></span>

<span data-ttu-id="d78be-107">根據預設值，Azure Stack 上的 App Service 支援免費和共用背景工作角色層。</span><span class="sxs-lookup"><span data-stu-id="d78be-107">App Service on Azure Stack, by default, supports free and shared worker tiers.</span></span> <span data-ttu-id="d78be-108">tooadd 其他背景工作層，您需要 tooadd 更多背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="d78be-108">tooadd other worker tiers, you need tooadd more worker roles.</span></span>

<span data-ttu-id="d78be-109">如果您不確定哪些部署時已安裝 Azure 堆疊上的 hello 預設應用程式服務，您可以檢閱 hello 中的其他資訊[應用程式服務在 Azure 堆疊概觀](azure-stack-app-service-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="d78be-109">If you are not sure what was deployed with hello default App Service on Azure Stack installation, you can review additional information in hello [App Service on Azure Stack overview](azure-stack-app-service-overview.md).</span></span>

<span data-ttu-id="d78be-110">有兩種方式 tooadd 額外容量 tooApp Azure 堆疊上的服務：</span><span class="sxs-lookup"><span data-stu-id="d78be-110">There are two ways tooadd additional capacity tooApp Service on Azure Stack:</span></span>
1.  <span data-ttu-id="d78be-111">[新增其他工作者直接從 hello 應用程式服務資源提供者系統管理員內](#Add-additional-workers-directly-from-within-the-App-Service-Resource-Provider-Admin)。</span><span class="sxs-lookup"><span data-stu-id="d78be-111">[Add additional workers directly from with within hello App Service Resource Provider Admin](#Add-additional-workers-directly-from-within-the-App-Service-Resource-Provider-Admin).</span></span>
2.  <span data-ttu-id="d78be-112">[手動建立其他 Vm，並將它們加入 toohello 應用程式服務資源提供者](#Create-additional-VMs-manually-and-add-them-to-the-App-Service-Resource-Provider)。</span><span class="sxs-lookup"><span data-stu-id="d78be-112">[Create additional VMs manually and add them toohello App Service Resource Provider](#Create-additional-VMs-manually-and-add-them-to-the-App-Service-Resource-Provider).</span></span>

## <a name="add-additional-workers-directly-within-hello-app-service-resource-provider-admin"></a><span data-ttu-id="d78be-113">加入額外的背景工作，直接在 hello 應用程式服務資源提供者系統管理員。</span><span class="sxs-lookup"><span data-stu-id="d78be-113">Add additional workers directly within hello App Service Resource Provider Admin.</span></span>

1.  <span data-ttu-id="d78be-114">登入 toohello 堆疊 Azure 入口網站以 hello 服務系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="d78be-114">Log in toohello Azure Stack portal as hello service administrator;</span></span>
2.  <span data-ttu-id="d78be-115">瀏覽過**資源提供者**和選取 hello**應用程式服務資源提供者系統管理員**。![Azure Stack 資源提供者][1]</span><span class="sxs-lookup"><span data-stu-id="d78be-115">Browse too**Resource Providers** and select hello **App Service Resource Provider Admin**. ![Azure Stack Resource Providers][1]</span></span>
3.  <span data-ttu-id="d78be-116">按一下 [角色]。</span><span class="sxs-lookup"><span data-stu-id="d78be-116">Click **Roles**.</span></span>  <span data-ttu-id="d78be-117">這裡您會看到所有的應用程式服務角色部署的 hello 分解。</span><span class="sxs-lookup"><span data-stu-id="d78be-117">Here you see hello breakdown of all App Service roles deployed.</span></span>
4.  <span data-ttu-id="d78be-118">按一下 hello 選項**新的角色執行個體**![新增新的角色執行個體][2]</span><span class="sxs-lookup"><span data-stu-id="d78be-118">Click hello option **New Role Instance** ![Add new role instance][2]</span></span>
5.  <span data-ttu-id="d78be-119">在 hello**新的角色執行個體**刀鋒視窗中：</span><span class="sxs-lookup"><span data-stu-id="d78be-119">In hello **New Role Instance** blade:</span></span>
    1. <span data-ttu-id="d78be-120">選擇多少其他**角色執行個體**希望 tooadd。</span><span class="sxs-lookup"><span data-stu-id="d78be-120">Choose how many additional **role instances** you would like tooadd.</span></span>  <span data-ttu-id="d78be-121">在 hello 預覽中，沒有最多 10 個。</span><span class="sxs-lookup"><span data-stu-id="d78be-121">In hello preview, there is a maximum of 10.</span></span>
    2. <span data-ttu-id="d78be-122">選取 hello**角色類型**。</span><span class="sxs-lookup"><span data-stu-id="d78be-122">Select hello **role type**.</span></span>  <span data-ttu-id="d78be-123">在此預覽中，這個選項會限制的 tooWeb 背景工作。</span><span class="sxs-lookup"><span data-stu-id="d78be-123">In this preview, this option is limited tooWeb Worker.</span></span>
    3. <span data-ttu-id="d78be-124">選取 hello**背景工作層**希望 toodeploy 這個工作者，預設的選項是小型、 中型、 大型 或共用。</span><span class="sxs-lookup"><span data-stu-id="d78be-124">Select hello **worker tier** you would like toodeploy this worker into, default choices are Small, Medium, Large, or Shared.</span></span>  <span data-ttu-id="d78be-125">如果您已建立自己的背景工作層，也可選取您的背景工作層。</span><span class="sxs-lookup"><span data-stu-id="d78be-125">If, you have created your own worker tiers, your worker tiers will also be available for selection.</span></span>
    4. <span data-ttu-id="d78be-126">按一下**確定**toodeploy hello 額外的背景工作</span><span class="sxs-lookup"><span data-stu-id="d78be-126">Click **OK** toodeploy hello additional workers</span></span>
6.  <span data-ttu-id="d78be-127">Hello 其他 Vm，請將其設定、 安裝 hello 所需的所有軟體，將它們標示為已備妥，完成此程序時，現在將加入 Azure 堆疊會在應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="d78be-127">App Service on Azure Stack will now add hello additional VMs, configure them, install all hello required software and mark them as ready when this process is complete.</span></span>  <span data-ttu-id="d78be-128">此程序大約需要 80 分鐘。</span><span class="sxs-lookup"><span data-stu-id="d78be-128">This process can take approximately 80 minutes.</span></span>
7.  <span data-ttu-id="d78be-129">您可以藉由檢視 hello 工作者在 hello 監視 hello hello 整備 hello 新背景工作的進度**角色**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d78be-129">You can monitor hello progress of hello readiness of hello new workers by viewing hello workers in hello **roles** blade.</span></span>

>[!NOTE]
>  <span data-ttu-id="d78be-130">在此預覽中，hello 整合新的角色執行個體流程有限的 tooWorker 角色並將 Vm 部署的大小只 A1。</span><span class="sxs-lookup"><span data-stu-id="d78be-130">In this preview, hello integrated New Role Instance flow is limited tooWorker Roles and deploy VMs of size A1 only.</span></span>  <span data-ttu-id="d78be-131">我們將在未來版本中擴充此功能。</span><span class="sxs-lookup"><span data-stu-id="d78be-131">We will be expanding this capability in a future release.</span></span>

## <a name="manually-adding-additional-capacity-tooapp-service-on-azure-stack"></a><span data-ttu-id="d78be-132">手動新增額外的容量 tooApp Azure 堆疊上的服務。</span><span class="sxs-lookup"><span data-stu-id="d78be-132">Manually adding additional capacity tooApp Service on Azure Stack.</span></span>

<span data-ttu-id="d78be-133">hello 下列步驟是必要的 tooadd 其他角色：</span><span class="sxs-lookup"><span data-stu-id="d78be-133">hello following steps are required tooadd additional roles:</span></span>

1. [<span data-ttu-id="d78be-134">建立新的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="d78be-134">Create a new virtual machine</span></span>](#step-1-create-a-new-vm-to-support-the-new-instance-size)
2. [<span data-ttu-id="d78be-135">Hello 虛擬機器設定</span><span class="sxs-lookup"><span data-stu-id="d78be-135">Configure hello virtual machine</span></span>](#step-2-configure-the-virtual-machine)
3. [<span data-ttu-id="d78be-136">在 hello Azure 堆疊入口網站中設定 hello web 背景工作角色</span><span class="sxs-lookup"><span data-stu-id="d78be-136">Configure hello web worker role in hello Azure Stack portal</span></span>](#step-3-configure-the-web-worker-role-in-the-azure-stack-portal)
4. [<span data-ttu-id="d78be-137">設定 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="d78be-137">Configure app service plans</span></span>](#step-4-configure-app-service-plans)

## <a name="step-1-create-a-new-vm-toosupport-hello-new-instance-size"></a><span data-ttu-id="d78be-138">步驟 1： 建立新 VM toosupport hello 新執行個體的大小</span><span class="sxs-lookup"><span data-stu-id="d78be-138">Step 1: Create a new VM toosupport hello new instance size</span></span>
<span data-ttu-id="d78be-139">建立虛擬機器中所述[本文](azure-stack-provision-vm.md)，確保 hello 下列則會選取：</span><span class="sxs-lookup"><span data-stu-id="d78be-139">Create a virtual machine as described in [this article](azure-stack-provision-vm.md), ensuring that hello following selections are made:</span></span>

* <span data-ttu-id="d78be-140">使用者名稱和密碼： 提供 hello 相同使用者名稱和您在安裝 Azure 堆疊上的應用程式服務時，您提供的密碼。</span><span class="sxs-lookup"><span data-stu-id="d78be-140">User name and password: Provide hello same user name and password you provided when you installed App Service on Azure Stack.</span></span>
* <span data-ttu-id="d78be-141">訂用帳戶： 使用 hello 預設提供者訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d78be-141">Subscription: Use hello default provider subscription.</span></span>
* <span data-ttu-id="d78be-142">資源群組：選擇 [AppService-LOCAL]。</span><span class="sxs-lookup"><span data-stu-id="d78be-142">Resource group: Choose **AppService-LOCAL**.</span></span>

> [!NOTE]
> <span data-ttu-id="d78be-143">將背景工作角色的 hello 虛擬機器儲存在 hello Azure 堆疊上的應用程式服務相同資源群組部署至。</span><span class="sxs-lookup"><span data-stu-id="d78be-143">Store hello virtual machines for worker roles in hello same resource group as App Service on Azure Stack is deployed to.</span></span> <span data-ttu-id="d78be-144">(這是適用於此版本的建議作法)。</span><span class="sxs-lookup"><span data-stu-id="d78be-144">(This is recommended for this release.)</span></span>
> 
> 

## <a name="step-2-configure-hello-virtual-machine"></a><span data-ttu-id="d78be-145">步驟 2： 設定 hello 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="d78be-145">Step 2: Configure hello Virtual Machine</span></span>
<span data-ttu-id="d78be-146">Hello 部署完成後，請 hello 下列組態會是必要的 toosupport hello web 背景工作角色：</span><span class="sxs-lookup"><span data-stu-id="d78be-146">Once hello deployment has completed, hello following configuration is required toosupport hello web worker role:</span></span>

1. <span data-ttu-id="d78be-147">瀏覽 toohello **AppService 本機**hello 入口網站和選取 hello 您在步驟 1 中建立新的機器中的資源群組。</span><span class="sxs-lookup"><span data-stu-id="d78be-147">Browse toohello **AppService-LOCAL** resource group in hello portal and select hello new machine you created in Step 1.</span></span>
2. <span data-ttu-id="d78be-148">按一下 [連線] hello VM 刀鋒視窗 toodownload hello 遠端桌面設定檔中。</span><span class="sxs-lookup"><span data-stu-id="d78be-148">Click connect in hello VM blade toodownload hello remote desktop profile.</span></span>  <span data-ttu-id="d78be-149">開啟 hello 設定檔 tooopen 遠端桌面工作階段 tooyour VM。</span><span class="sxs-lookup"><span data-stu-id="d78be-149">Open hello profile tooopen a remote desktop session tooyour VM.</span></span>
3. <span data-ttu-id="d78be-150">登入 toohello VM hello 使用者名稱和您在步驟 1 中指定的密碼。</span><span class="sxs-lookup"><span data-stu-id="d78be-150">Log in toohello VM using hello username and password you specified in Step 1.</span></span>
4. <span data-ttu-id="d78be-151">開啟 PowerShell，依序按一下 hello**啟動**按鈕並輸入 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="d78be-151">Open PowerShell by clicking hello **Start** button and typing PowerShell.</span></span> <span data-ttu-id="d78be-152">以滑鼠右鍵按一下**PowerShell.exe**，然後選取**系統管理員身分執行**tooopen PowerShell 以系統管理員模式。</span><span class="sxs-lookup"><span data-stu-id="d78be-152">Right-click **PowerShell.exe**, and select **Run as administrator** tooopen PowerShell in administrator mode.</span></span>
5. <span data-ttu-id="d78be-153">複製和貼上每個 hello 到 hello PowerShell 視窗，然後按下列命令 （一次一個） 的輸入：</span><span class="sxs-lookup"><span data-stu-id="d78be-153">Copy and paste each of hello following commands (one at a time) into hello PowerShell window, and press enter:</span></span>
   
   ```netsh advfirewall firewall set rule group="File and Printer Sharing" new enable=Yes```
   ```netsh advfirewall firewall set rule group="Windows Management Instrumentation (WMI)" new enable=yes```
   ```reg add HKLM\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion\\Policies\\system /v LocalAccountTokenFilterPolicy /t REG\_DWORD /d 1 /f```
   
6. <span data-ttu-id="d78be-154">關閉您的遠端桌面工作階段。</span><span class="sxs-lookup"><span data-stu-id="d78be-154">Close your remote desktop session.</span></span>
7. <span data-ttu-id="d78be-155">重新啟動 hello VM 從 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="d78be-155">Restart hello VM from hello portal.</span></span>

> [!NOTE]
> <span data-ttu-id="d78be-156">這些是針對 Azure Stack 上之 App Service 的最低需求。</span><span class="sxs-lookup"><span data-stu-id="d78be-156">These are minimum requirements for App Service on Azure Stack.</span></span> <span data-ttu-id="d78be-157">它們是 hello hello Azure 堆疊所包含的 Windows 2012 R2 映像的預設設定。</span><span class="sxs-lookup"><span data-stu-id="d78be-157">They are hello default settings of hello Windows 2012 R2 image included with Azure Stack.</span></span> <span data-ttu-id="d78be-158">已提供 hello 指示供日後參考，並使用不同的影像。</span><span class="sxs-lookup"><span data-stu-id="d78be-158">hello instructions have been provided for future reference, and for those using a different image.</span></span>
> 
> 

## <a name="step-3-configure-hello-worker-role-in-hello-azure-stack-portal"></a><span data-ttu-id="d78be-159">步驟 3: Hello Azure 堆疊入口網站中設定 hello 背景工作角色</span><span class="sxs-lookup"><span data-stu-id="d78be-159">Step 3: Configure hello worker role in hello Azure Stack portal</span></span>
1. <span data-ttu-id="d78be-160">在 hello 服務系統管理員身分開啟 hello 入口網站**ClientVM**。</span><span class="sxs-lookup"><span data-stu-id="d78be-160">Open hello portal as hello service administrator on **ClientVM**.</span></span>
2. <span data-ttu-id="d78be-161">瀏覽過**資源提供者** &gt; **應用程式服務資源提供者系統管理員**。![應用程式服務資源提供者管理][3]</span><span class="sxs-lookup"><span data-stu-id="d78be-161">Navigate too**Resource Providers** &gt; **App Service Resource Provider Admin**.![App Service Resource Provider Admin][3]</span></span>
3. <span data-ttu-id="d78be-162">在 hello 設定刀鋒視窗中，按一下 **角色**。![應用程式服務資源提供者角色][4]</span><span class="sxs-lookup"><span data-stu-id="d78be-162">In hello settings blade, click **Roles**.![App Service Resource Provider Roles][4]</span></span>
4. <span data-ttu-id="d78be-163">按一下 [新增角色執行個體]。</span><span class="sxs-lookup"><span data-stu-id="d78be-163">Click **Add Role Instance**.</span></span>
5. <span data-ttu-id="d78be-164">中的 hello 文字方塊**伺服器名稱**輸入 hello **IP 位址**hello 伺服器稍早 （區段 1) 中所建立。</span><span class="sxs-lookup"><span data-stu-id="d78be-164">In hello textbox for **Server Name** enter hello **IP Address** of hello server you created earlier (in Section 1).</span></span>
6. <span data-ttu-id="d78be-165">選取 hello**角色類型**希望 tooadd-控制器、 管理伺服器、 前端、 Web 背景工作、 發行者或檔案伺服器。</span><span class="sxs-lookup"><span data-stu-id="d78be-165">Select hello **Role Type** you would like tooadd - Controller, Management Server, Front End, Web Worker, Publisher, or File Server.</span></span>  <span data-ttu-id="d78be-166">在此範例中，請選取 [Web 背景工作]。</span><span class="sxs-lookup"><span data-stu-id="d78be-166">In this instance, select Web Worker.</span></span>
7. <span data-ttu-id="d78be-167">按一下 hello**層**會像 toodeploy hello 的新執行個體太 （小型、 中型、 大型或共用）。</span><span class="sxs-lookup"><span data-stu-id="d78be-167">Click hello **Tier** you would like toodeploy hello new instance too(small, medium, large, or shared).</span></span>  <span data-ttu-id="d78be-168">如果您已建立自己的背景工作層，也可選取這些背景工作層。</span><span class="sxs-lookup"><span data-stu-id="d78be-168">If you have created your own worker tiers these will also be available for selection.</span></span>
8. <span data-ttu-id="d78be-169">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="d78be-169">Click **OK.**</span></span>
9. <span data-ttu-id="d78be-170">返回 toohello**角色**檢視</span><span class="sxs-lookup"><span data-stu-id="d78be-170">Go back toohello **Roles** view</span></span>
10. <span data-ttu-id="d78be-171">按一下 hello 資料列對應 toohello 角色類型和背景工作層的組合，您指派至 VM。</span><span class="sxs-lookup"><span data-stu-id="d78be-171">Click hello row corresponding toohello Role Type and Worker Tier combination you assigned your VM to.</span></span>
11. <span data-ttu-id="d78be-172">尋找 hello 您剛才加入的伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="d78be-172">Look for hello Server Name you just added.</span></span> <span data-ttu-id="d78be-173">檢閱 hello 狀態 資料行，並等候 toomove toohello 下一個步驟，直到 hello 狀態是 「 就緒 」。</span><span class="sxs-lookup"><span data-stu-id="d78be-173">Review hello status column, and wait toomove toohello next step until hello status is "Ready."</span></span> <span data-ttu-id="d78be-174">這大約需要 80 分鐘。</span><span class="sxs-lookup"><span data-stu-id="d78be-174">This can take approximately 80 minutes.</span></span> <span data-ttu-id="d78be-175">![App Service 資源提供者角色就緒][5]</span><span class="sxs-lookup"><span data-stu-id="d78be-175">![App Service Resource Provider Role Ready][5]</span></span>

## <a name="step-4-configure-app-service-plans"></a><span data-ttu-id="d78be-176">步驟 4：設定 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="d78be-176">Step 4: Configure app service plans</span></span>

1. <span data-ttu-id="d78be-177">登入上 hello ClientVM toohello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="d78be-177">Sign in toohello portal on hello ClientVM.</span></span>
2. <span data-ttu-id="d78be-178">瀏覽過**新增** &gt; **Web 和行動裝置版**。</span><span class="sxs-lookup"><span data-stu-id="d78be-178">Navigate too**New** &gt; **Web and Mobile**.</span></span>
3. <span data-ttu-id="d78be-179">選取 hello 類型的應用程式中，您想要 toodeploy。</span><span class="sxs-lookup"><span data-stu-id="d78be-179">Select hello type of application you would like toodeploy.</span></span>
4. <span data-ttu-id="d78be-180">提供 hello hello 應用程式的資訊，然後選取**應用程式服務方案 / 位置**。</span><span class="sxs-lookup"><span data-stu-id="d78be-180">Provide hello information for hello application, and then select **AppService Plan / Location**.</span></span>
    1. <span data-ttu-id="d78be-181">按一下 [新建] 。</span><span class="sxs-lookup"><span data-stu-id="d78be-181">Click **Create New**.</span></span>
    2. <span data-ttu-id="d78be-182">建立您的計劃中，然後再選取 hello 相對應的定價層 hello 計劃。</span><span class="sxs-lookup"><span data-stu-id="d78be-182">Create your plan, selecting hello corresponding pricing tier for hello plan.</span></span>

> [!NOTE]
> <span data-ttu-id="d78be-183">您可以在此刀鋒視窗上建立多個方案。</span><span class="sxs-lookup"><span data-stu-id="d78be-183">You can create multiple plans while on this blade.</span></span> <span data-ttu-id="d78be-184">您部署，但是之前, 請確定您已選取 hello 適當的計畫。</span><span class="sxs-lookup"><span data-stu-id="d78be-184">Before you deploy, however, ensure you have selected hello appropriate plan.</span></span>
> 
> 

<span data-ttu-id="d78be-185">hello 下列預設會顯示 hello 的範例可以使用多個定價層。</span><span class="sxs-lookup"><span data-stu-id="d78be-185">hello following shows an example of hello multiple pricing tiers available by default.</span></span>  <span data-ttu-id="d78be-186">您注意到，是否有特定的背景工作層沒有可用的背景工作，對應的定價層 hello 選項 toochoose hello 就無法使用。</span><span class="sxs-lookup"><span data-stu-id="d78be-186">You notice that if there are no available workers for a particular worker tier, hello option toochoose hello corresponding pricing tier is unavailable.</span></span>![Azure Stack 上的 App Service 預設定價層][6]

<!--Image references-->
[1]: ./media/azure-stack-app-service-add-worker-roles/azure-stack-resource-providers.png
[2]: ./media/azure-stack-app-service-add-worker-roles/app-service-new-role-instance.png
[3]: ./media/azure-stack-app-service-add-worker-roles/app-service-resource-provider-admin.png
[4]: ./media/azure-stack-app-service-add-worker-roles/app-service-resource-provider-roles.png
[5]: ./media/azure-stack-app-service-add-worker-roles/app-service-resource-provider-role-ready.png
[6]: ./media/azure-stack-app-service-add-worker-roles/app-service-resource-provider-pricing-tier.png
