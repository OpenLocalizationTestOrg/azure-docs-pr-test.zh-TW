---
title: "Microsoft Azure Stack 開發套件版本資訊 | Microsoft Docs"
description: 
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: a7e61ea4-be2f-4e55-9beb-7a079f348e05
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: helaw
ms.openlocfilehash: 2cf11155dbd524260329f8b271ce4d9b19095b6a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-stack-development-kit-release-notes"></a><span data-ttu-id="1e22f-102">Azure Stack 開發套件版本資訊</span><span class="sxs-lookup"><span data-stu-id="1e22f-102">Azure Stack Development Kit release notes</span></span>
<span data-ttu-id="1e22f-103">這些版本資訊提供新功能和已知問題的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="1e22f-103">These release notes provide information on new features and known issues.</span></span>

## <a name="release-build-201706271"></a><span data-ttu-id="1e22f-104">版本組建 20170627.1</span><span class="sxs-lookup"><span data-stu-id="1e22f-104">Release Build 20170627.1</span></span>
<span data-ttu-id="1e22f-105">從 [20170627.1](azure-stack-updates.md#determine-the-current-version) 版本開始，Azure Stack 概念證明已重新命名為 Azure Stack 開發套件。</span><span class="sxs-lookup"><span data-stu-id="1e22f-105">Starting with the [20170627.1](azure-stack-updates.md#determine-the-current-version) release, Azure Stack Proof of Concept has been renamed to Azure Stack Development Kit.</span></span>  <span data-ttu-id="1e22f-106">與 Azure Stack POC 一樣，Azure Stack 開發套件也是作為開發和評估環境，用於探索 Azure Stack 功能，並提供 Azure Stack 的開發平台。</span><span class="sxs-lookup"><span data-stu-id="1e22f-106">Like the Azure Stack POC, Azure Stack Development Kit is intended to be a development and evaluation environment used to explore Azure Stack features, and provide a development platform for Azure Stack.</span></span>

### <a name="whats-new"></a><span data-ttu-id="1e22f-107">新功能</span><span class="sxs-lookup"><span data-stu-id="1e22f-107">What's new</span></span>
- <span data-ttu-id="1e22f-108">您現在可以使用 CLI 2.0，從熱門作業系統中的命令列管理 Azure Stack 資源。</span><span class="sxs-lookup"><span data-stu-id="1e22f-108">You can now use CLI 2.0 to manage Azure Stack resources from a commandline on popular operating systems.</span></span>
- <span data-ttu-id="1e22f-109">DSV2 虛擬機器大小支援 Azure 和 Azure Stack 之間的範本可攜性。</span><span class="sxs-lookup"><span data-stu-id="1e22f-109">DSV2 virtual machine sizes enable template portability between Azure and Azure Stack.</span></span>
- <span data-ttu-id="1e22f-110">雲端操作員可以在容量管理刀鋒視窗中預覽容量管理體驗。</span><span class="sxs-lookup"><span data-stu-id="1e22f-110">Cloud operators can preview the capacity management experience within the capacity management blade.</span></span>
- <span data-ttu-id="1e22f-111">您現在可以使用「Azure 診斷」擴充功能從虛擬機器收集診斷資料。</span><span class="sxs-lookup"><span data-stu-id="1e22f-111">You can now use the Azure Diagnostics extension to gather diagnostic data from your virtual machines.</span></span>  <span data-ttu-id="1e22f-112">在分析工作負載效能及調查問題時，收集此資料會非常有用。</span><span class="sxs-lookup"><span data-stu-id="1e22f-112">Capturing this data is useful when analyzing workload performance and for investigating issues.</span></span>
- <span data-ttu-id="1e22f-113">新的[部署體驗](azure-stack-run-powershell-script.md)取代了先前已編寫指令碼的部署步驟。</span><span class="sxs-lookup"><span data-stu-id="1e22f-113">A new [deployment experience](azure-stack-run-powershell-script.md) replaces previous scripted steps for deployment.</span></span>  <span data-ttu-id="1e22f-114">新的部署體驗會在整個部署生命週期中提供通用的圖形化介面。</span><span class="sxs-lookup"><span data-stu-id="1e22f-114">The new deployment experience provides a common graphical interface through the entire deployment lifecycle.</span></span>
- <span data-ttu-id="1e22f-115">現在部署期間支援 Microsoft 帳戶 (MSA)。</span><span class="sxs-lookup"><span data-stu-id="1e22f-115">Microsoft Accounts (MSA) are now supported during deployment.</span></span>
- <span data-ttu-id="1e22f-116">現在部署期間也支援 Multi-Factor Authentication (MFA)。</span><span class="sxs-lookup"><span data-stu-id="1e22f-116">Multi-Factor Authentication (MFA) is now supported during deployment.</span></span>  <span data-ttu-id="1e22f-117">之前在部署期間必須停用 MFA。</span><span class="sxs-lookup"><span data-stu-id="1e22f-117">Previously, MFA must be disabled during deployment.</span></span>

### <a name="known-issues"></a><span data-ttu-id="1e22f-118">已知問題</span><span class="sxs-lookup"><span data-stu-id="1e22f-118">Known issues</span></span>
#### <a name="deployment"></a><span data-ttu-id="1e22f-119">部署</span><span class="sxs-lookup"><span data-stu-id="1e22f-119">Deployment</span></span>
* <span data-ttu-id="1e22f-120">您可能會注意到部署時使用的時間比舊版長。</span><span class="sxs-lookup"><span data-stu-id="1e22f-120">You may notice deployment taking longer than previous releases.</span></span> 
* <span data-ttu-id="1e22f-121">Get-AzureStackLogs 可產生診斷記錄檔，但是不會將進度記錄至主控台。</span><span class="sxs-lookup"><span data-stu-id="1e22f-121">Get-AzureStackLogs generates diagnostic logs, however, does not log progress to the console.</span></span>
* <span data-ttu-id="1e22f-122">您必須使用新的[部署體驗](azure-stack-run-powershell-script.md)部署 Azure Stack，否則部署可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="1e22f-122">You must use the new [deployment experience](azure-stack-run-powershell-script.md) to deploy Azure Stack, or deployment may fail.</span></span>

#### <a name="portal"></a><span data-ttu-id="1e22f-123">入口網站</span><span class="sxs-lookup"><span data-stu-id="1e22f-123">Portal</span></span>
* <span data-ttu-id="1e22f-124">您可能會在入口網站中看到空白的儀表板。</span><span class="sxs-lookup"><span data-stu-id="1e22f-124">You may see a blank dashboard in the portal.</span></span>  <span data-ttu-id="1e22f-125">您可以選取位於入口網站右上角的齒輪，然後選取 [還原預設設定]，以還原儀表板。</span><span class="sxs-lookup"><span data-stu-id="1e22f-125">You can recover the dashboard by selecting the gear in the upper right of the portal, and selecting "Restore default settings".</span></span>
* <span data-ttu-id="1e22f-126">租用戶不需要訂用帳戶就能瀏覽完整的市集，而且將會看到如方案和供應項目的管理項目。</span><span class="sxs-lookup"><span data-stu-id="1e22f-126">Tenants are able to browse the full marketplace without a subscription, and will see administrative items like plans and offers.</span></span>  <span data-ttu-id="1e22f-127">對租用戶而言，這些項目都是非功能性項目。</span><span class="sxs-lookup"><span data-stu-id="1e22f-127">These items are non-functional to tenants.</span></span>
* <span data-ttu-id="1e22f-128">在選取基礎結構角色執行個體時，您會看到顯示參考錯誤的錯誤。</span><span class="sxs-lookup"><span data-stu-id="1e22f-128">When selecting an infrastructure role instance,  you see an error showing a reference error.</span></span> <span data-ttu-id="1e22f-129">請使用瀏覽器的重新整理功能重新整理管理入口網站。</span><span class="sxs-lookup"><span data-stu-id="1e22f-129">Use the browser’s refresh functionality to refresh the Admin Portal.</span></span>
* <span data-ttu-id="1e22f-130">[資源群組] 刀鋒視窗上的 [移動] 按鈕已經停用。</span><span class="sxs-lookup"><span data-stu-id="1e22f-130">The "move" button is disabled on the Resource Group blade.</span></span>  <span data-ttu-id="1e22f-131">這是預期的行為，因為目前不支援在訂用帳戶之間移動資源群組。</span><span class="sxs-lookup"><span data-stu-id="1e22f-131">This is expected behavior, because moving resource groups between subscriptions is not currently supported.</span></span>
* <span data-ttu-id="1e22f-132">您將會收到和已完成下載之聯合市集項目有關的重複通知。</span><span class="sxs-lookup"><span data-stu-id="1e22f-132">You will receive repeated notifications for syndicated marketplace items that have completed downloading.</span></span>
* <span data-ttu-id="1e22f-133">您無法使用 Azure Stack 入口網站檢視訂用帳戶的權限。</span><span class="sxs-lookup"><span data-stu-id="1e22f-133">You are not able to view permissions to your subscription using the Azure Stack portals.</span></span>  <span data-ttu-id="1e22f-134">解決方法是，可以使用 Powershell 確認權限。</span><span class="sxs-lookup"><span data-stu-id="1e22f-134">As a work-around, you can verify permissions using Powershell.</span></span>
* <span data-ttu-id="1e22f-135">從入口網站將完整的部署匯出為自動指令碼時，必須將 `-TenantID` 新增為旗標。</span><span class="sxs-lookup"><span data-stu-id="1e22f-135">You must add `-TenantID` as a flag when exporting a completed deployment as an automation script from the portal.</span></span>

#### <a name="services"></a><span data-ttu-id="1e22f-136">服務</span><span class="sxs-lookup"><span data-stu-id="1e22f-136">Services</span></span>
* <span data-ttu-id="1e22f-137">必須從租用戶入口網站或租用戶 API 建立 Key Vault 服務。</span><span class="sxs-lookup"><span data-stu-id="1e22f-137">Key Vault services must be created from the tenant portal or tenant API.</span></span>  <span data-ttu-id="1e22f-138">如果是以系統管理員身分登入，請務必使用租用戶入口網站建立新的 Key Vault 保存庫、密碼和金鑰。</span><span class="sxs-lookup"><span data-stu-id="1e22f-138">If you are logged in as an administrator, make sure to use the tenant portal to create new Key Vault vaults, secrets, and keys.</span></span>
* <span data-ttu-id="1e22f-139">雖然可以透過範本建立虛擬機器擴展集，但是沒有可用於建立它們的市集體驗。</span><span class="sxs-lookup"><span data-stu-id="1e22f-139">There is no marketplace experience for creating virtual machine scale sets, though they can be created via template.</span></span>
* <span data-ttu-id="1e22f-140">您無法透過入口網站將負載平衡器與後端網路建立關聯。</span><span class="sxs-lookup"><span data-stu-id="1e22f-140">You cannot associate a load balancer with a backend network via the portal.</span></span>  <span data-ttu-id="1e22f-141">此工作可以透過 PowerShell 或透過範本來完成。</span><span class="sxs-lookup"><span data-stu-id="1e22f-141">This task can be completed with PowerShell or with a template.</span></span>
* <span data-ttu-id="1e22f-142">VM 可用性設定組只能設定一個容錯網域和一個更新網域。</span><span class="sxs-lookup"><span data-stu-id="1e22f-142">VM Availability sets can only be configured with a fault domain of one and an update domain of one.</span></span>  
* <span data-ttu-id="1e22f-143">租用戶必須有現有的儲存體帳戶，才能建立新的 Azure Function。</span><span class="sxs-lookup"><span data-stu-id="1e22f-143">A tenant must have an existing storage account before creating a new Azure Function.</span></span>
* <span data-ttu-id="1e22f-144">VM 可能會失敗並報告「無法將引數繫結到 'VM Network Adapter' 參數，因為它是 Null。」</span><span class="sxs-lookup"><span data-stu-id="1e22f-144">VM may fail and report "Cannot bind argument to parameter 'VM Network Adapter' because it is null."</span></span>  <span data-ttu-id="1e22f-145">虛擬機器重新部署成功。</span><span class="sxs-lookup"><span data-stu-id="1e22f-145">Redeployment of the virtual machine succeeds.</span></span>  
* <span data-ttu-id="1e22f-146">刪除租用戶訂用帳戶會導致產生孤立的資源。</span><span class="sxs-lookup"><span data-stu-id="1e22f-146">Deleting tenant subscriptions results in orphaned resources.</span></span>  <span data-ttu-id="1e22f-147">因應措施是，先刪除租用戶資源或整個資源群組，然後再刪除租用戶訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1e22f-147">As a workaround, first delete tenant resources or entire resource group, and then delete tenant subscriptions.</span></span> 
* <span data-ttu-id="1e22f-148">建立網路負載平衡器時，必須建立 NAT 規則，否則在建立負載平衡器之後嘗試新增 NAT 規則時，會收到錯誤。</span><span class="sxs-lookup"><span data-stu-id="1e22f-148">You must create a NAT rule when creating a network load balancer, or you will receive an error when you attempt to add a NAT rule after the load balancer is created.</span></span>
* <span data-ttu-id="1e22f-149">租用戶可以建立大於配額允許大小的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="1e22f-149">Tenants can create virtual machines larger than quota allows.</span></span>  <span data-ttu-id="1e22f-150">此行為是因為未強制套用計算配額。</span><span class="sxs-lookup"><span data-stu-id="1e22f-150">This behavior is because compute quotas are not enforced.</span></span>
* <span data-ttu-id="1e22f-151">系統會提供選項，供租用戶建立具備異地備援儲存體的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="1e22f-151">Tenants are given the option to create a virtual machine with geo-redundant storage.</span></span>  <span data-ttu-id="1e22f-152">此設定會導致虛擬機器建立失敗。</span><span class="sxs-lookup"><span data-stu-id="1e22f-152">This configuration causes virtual machine creation to fail.</span></span>
* <span data-ttu-id="1e22f-153">這最多可能需要一個小時，然後租用戶才能在新的 SQL 或 MySQL SKU 中建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="1e22f-153">It can take up to an hour before tenants can create databases in a new SQL or MySQL SKU.</span></span> 
* <span data-ttu-id="1e22f-154">不支援在不是由資源提供者執行的 SQL 和 MySQL 主控伺服器中直接建立項目，且可能會導致不相符的狀態。</span><span class="sxs-lookup"><span data-stu-id="1e22f-154">Creation of items directly on SQL and MySQL hosting servers that are not performed by the resource provider is not supported and may result in mismatched state.</span></span>
* <span data-ttu-id="1e22f-155">AzureRM PowerShell 1.2.10 需要額外的設定步驟：</span><span class="sxs-lookup"><span data-stu-id="1e22f-155">AzureRM PowerShell 1.2.10 requires extra configuration steps:</span></span>
    * <span data-ttu-id="1e22f-156">請在執行 Azure AD 部署的 Add-AzureRMEnvironment 之後執行此作業。</span><span class="sxs-lookup"><span data-stu-id="1e22f-156">Run this after running Add-AzureRMEnvironment for Azure AD deployments.</span></span>  <span data-ttu-id="1e22f-157">使用 `Add-AzureRMEnvironment` 的輸出提供 Name 和 GraphAudience 值。</span><span class="sxs-lookup"><span data-stu-id="1e22f-157">Provide the Name and GraphAudience values using the output from `Add-AzureRMEnvironment`.</span></span>
      
      ```PowerShell
      Set-AzureRmEnvironment -Name <Environment Name> -GraphAudience <Graph Endpoint URL>
      ```
    * <span data-ttu-id="1e22f-158">請在執行 AD FS 部署的 Add-AzureRMEnvironment 之後執行此作業。</span><span class="sxs-lookup"><span data-stu-id="1e22f-158">Run this after running Add-AzureRMEnvironment for AD FS deployments.</span></span>  <span data-ttu-id="1e22f-159">使用 `Add-AzureRMEnvironment` 的輸出提供 Name 和 GraphAudience 值。</span><span class="sxs-lookup"><span data-stu-id="1e22f-159">Provide the Name and GraphAudience values using the output of `Add-AzureRMEnvironment`.</span></span>
      
      ```PowerShell
      Set-AzureRmEnvironment <Environment Name> -GraphAudience <Graph Endpoint URL> -EnableAdfsAuthentication:$true
      ```
    
    <span data-ttu-id="1e22f-160">例如，以下項目用於 Azure AD 環境：</span><span class="sxs-lookup"><span data-stu-id="1e22f-160">As an example, the following is used for an Azure AD environment:</span></span>

    ```PowerShell
      Set-AzureRmEnvironment AzureStack -GraphAudience https://graph.local.azurestack.external/
    ```

#### <a name="fabric"></a><span data-ttu-id="1e22f-161">網狀架構</span><span class="sxs-lookup"><span data-stu-id="1e22f-161">Fabric</span></span>
* <span data-ttu-id="1e22f-162">計算資源提供者會顯示未知的狀態。</span><span class="sxs-lookup"><span data-stu-id="1e22f-162">The compute resource provider displays an unknown state.</span></span>
* <span data-ttu-id="1e22f-163">縮放單位節點的基本資訊中不會顯示 BMC IP 位址和模型。</span><span class="sxs-lookup"><span data-stu-id="1e22f-163">The BMC IP address & model are not shown in the essential information of a Scale Unit Node.</span></span>  <span data-ttu-id="1e22f-164">這是 Azure Stack 開發套件中的預期行為。</span><span class="sxs-lookup"><span data-stu-id="1e22f-164">This behavior is expected in Azure Stack development kit.</span></span>
* <span data-ttu-id="1e22f-165">不應該使用計算控制器基礎結構角色 (AzS-XRP01 執行個體) 上的重新啟動動作。</span><span class="sxs-lookup"><span data-stu-id="1e22f-165">The restart action on Compute controller infrastructure role (AzS-XRP01 instance) should not be used.</span></span>
* <span data-ttu-id="1e22f-166">不應該使用基礎結構備份刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="1e22f-166">The Infrastructure backup blade should not be used.</span></span>
