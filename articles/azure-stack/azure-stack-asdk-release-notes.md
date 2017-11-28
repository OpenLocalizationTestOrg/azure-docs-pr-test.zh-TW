---
title: "aaaMicrosoft Azure 堆疊開發套件版本資訊 |Microsoft 文件"
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
ms.openlocfilehash: c1644f224933a63e1f0265b6ef4113789900cf12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stack-development-kit-release-notes"></a><span data-ttu-id="08ebd-102">Azure Stack 開發套件版本資訊</span><span class="sxs-lookup"><span data-stu-id="08ebd-102">Azure Stack Development Kit release notes</span></span>
<span data-ttu-id="08ebd-103">這些版本資訊提供新功能和已知問題的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="08ebd-103">These release notes provide information on new features and known issues.</span></span>

## <a name="release-build-201706271"></a><span data-ttu-id="08ebd-104">版本組建 20170627.1</span><span class="sxs-lookup"><span data-stu-id="08ebd-104">Release Build 20170627.1</span></span>
<span data-ttu-id="08ebd-105">開頭為 hello [20170627.1](azure-stack-updates.md#determine-the-current-version)版本中，Azure 堆疊概念證明已重新命名的 tooAzure 堆疊開發套件。</span><span class="sxs-lookup"><span data-stu-id="08ebd-105">Starting with hello [20170627.1](azure-stack-updates.md#determine-the-current-version) release, Azure Stack Proof of Concept has been renamed tooAzure Stack Development Kit.</span></span>  <span data-ttu-id="08ebd-106">就像 hello Azure 堆疊 POC，Azure 堆疊開發套件是 toobe 開發和評估環境使用 tooexplore Azure 堆疊功能，並提供開發平台的 Azure 堆疊。</span><span class="sxs-lookup"><span data-stu-id="08ebd-106">Like hello Azure Stack POC, Azure Stack Development Kit is intended toobe a development and evaluation environment used tooexplore Azure Stack features, and provide a development platform for Azure Stack.</span></span>

### <a name="whats-new"></a><span data-ttu-id="08ebd-107">新功能</span><span class="sxs-lookup"><span data-stu-id="08ebd-107">What's new</span></span>
- <span data-ttu-id="08ebd-108">您現在可以使用命令列的 CLI 2.0 toomanage Azure 堆疊資源受歡迎的作業系統上。</span><span class="sxs-lookup"><span data-stu-id="08ebd-108">You can now use CLI 2.0 toomanage Azure Stack resources from a commandline on popular operating systems.</span></span>
- <span data-ttu-id="08ebd-109">DSV2 虛擬機器大小支援 Azure 和 Azure Stack 之間的範本可攜性。</span><span class="sxs-lookup"><span data-stu-id="08ebd-109">DSV2 virtual machine sizes enable template portability between Azure and Azure Stack.</span></span>
- <span data-ttu-id="08ebd-110">雲端操作員可以預覽 hello 容量管理刀鋒視窗中的 hello 容量管理經驗。</span><span class="sxs-lookup"><span data-stu-id="08ebd-110">Cloud operators can preview hello capacity management experience within hello capacity management blade.</span></span>
- <span data-ttu-id="08ebd-111">您現在可以從您的虛擬機器使用 hello Azure 診斷擴充功能 toogather 診斷資料。</span><span class="sxs-lookup"><span data-stu-id="08ebd-111">You can now use hello Azure Diagnostics extension toogather diagnostic data from your virtual machines.</span></span>  <span data-ttu-id="08ebd-112">在分析工作負載效能及調查問題時，收集此資料會非常有用。</span><span class="sxs-lookup"><span data-stu-id="08ebd-112">Capturing this data is useful when analyzing workload performance and for investigating issues.</span></span>
- <span data-ttu-id="08ebd-113">新的[部署體驗](azure-stack-run-powershell-script.md)取代了先前已編寫指令碼的部署步驟。</span><span class="sxs-lookup"><span data-stu-id="08ebd-113">A new [deployment experience](azure-stack-run-powershell-script.md) replaces previous scripted steps for deployment.</span></span>  <span data-ttu-id="08ebd-114">hello 新的部署經驗提供通用的圖形化介面，透過 hello 整個部署生命週期。</span><span class="sxs-lookup"><span data-stu-id="08ebd-114">hello new deployment experience provides a common graphical interface through hello entire deployment lifecycle.</span></span>
- <span data-ttu-id="08ebd-115">現在部署期間支援 Microsoft 帳戶 (MSA)。</span><span class="sxs-lookup"><span data-stu-id="08ebd-115">Microsoft Accounts (MSA) are now supported during deployment.</span></span>
- <span data-ttu-id="08ebd-116">現在部署期間也支援 Multi-Factor Authentication (MFA)。</span><span class="sxs-lookup"><span data-stu-id="08ebd-116">Multi-Factor Authentication (MFA) is now supported during deployment.</span></span>  <span data-ttu-id="08ebd-117">之前在部署期間必須停用 MFA。</span><span class="sxs-lookup"><span data-stu-id="08ebd-117">Previously, MFA must be disabled during deployment.</span></span>

### <a name="known-issues"></a><span data-ttu-id="08ebd-118">已知問題</span><span class="sxs-lookup"><span data-stu-id="08ebd-118">Known issues</span></span>
#### <a name="deployment"></a><span data-ttu-id="08ebd-119">部署</span><span class="sxs-lookup"><span data-stu-id="08ebd-119">Deployment</span></span>
* <span data-ttu-id="08ebd-120">您可能會注意到部署時使用的時間比舊版長。</span><span class="sxs-lookup"><span data-stu-id="08ebd-120">You may notice deployment taking longer than previous releases.</span></span> 
* <span data-ttu-id="08ebd-121">Get AzureStackLogs 會產生診斷記錄檔，不過，不會記錄進度 toohello 主控台。</span><span class="sxs-lookup"><span data-stu-id="08ebd-121">Get-AzureStackLogs generates diagnostic logs, however, does not log progress toohello console.</span></span>
* <span data-ttu-id="08ebd-122">您必須使用 hello 新[部署經驗](azure-stack-run-powershell-script.md)toodeploy Azure 堆疊或部署可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="08ebd-122">You must use hello new [deployment experience](azure-stack-run-powershell-script.md) toodeploy Azure Stack, or deployment may fail.</span></span>

#### <a name="portal"></a><span data-ttu-id="08ebd-123">入口網站</span><span class="sxs-lookup"><span data-stu-id="08ebd-123">Portal</span></span>
* <span data-ttu-id="08ebd-124">您可能會看見 hello 入口網站中的空白儀表板。</span><span class="sxs-lookup"><span data-stu-id="08ebd-124">You may see a blank dashboard in hello portal.</span></span>  <span data-ttu-id="08ebd-125">您可以在 hello 右上方的 hello 入口網站中，選取 hello 齒輪，然後選取 [還原預設設定] 來復原 hello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="08ebd-125">You can recover hello dashboard by selecting hello gear in hello upper right of hello portal, and selecting "Restore default settings".</span></span>
* <span data-ttu-id="08ebd-126">租用戶可以 toobrowse hello 完整 marketplace 沒有訂用帳戶，而且將會看到像計劃和優惠的系統管理項目。</span><span class="sxs-lookup"><span data-stu-id="08ebd-126">Tenants are able toobrowse hello full marketplace without a subscription, and will see administrative items like plans and offers.</span></span>  <span data-ttu-id="08ebd-127">這些項目包含非功能性 tootenants。</span><span class="sxs-lookup"><span data-stu-id="08ebd-127">These items are non-functional tootenants.</span></span>
* <span data-ttu-id="08ebd-128">在選取基礎結構角色執行個體時，您會看到顯示參考錯誤的錯誤。</span><span class="sxs-lookup"><span data-stu-id="08ebd-128">When selecting an infrastructure role instance,  you see an error showing a reference error.</span></span> <span data-ttu-id="08ebd-129">使用 hello 瀏覽器的重新整理功能 toorefresh hello 管理入口網站。</span><span class="sxs-lookup"><span data-stu-id="08ebd-129">Use hello browser’s refresh functionality toorefresh hello Admin Portal.</span></span>
* <span data-ttu-id="08ebd-130">hello 「 移動 」 按鈕已停用 hello 資源群組 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="08ebd-130">hello "move" button is disabled on hello Resource Group blade.</span></span>  <span data-ttu-id="08ebd-131">這是預期的行為，因為目前不支援在訂用帳戶之間移動資源群組。</span><span class="sxs-lookup"><span data-stu-id="08ebd-131">This is expected behavior, because moving resource groups between subscriptions is not currently supported.</span></span>
* <span data-ttu-id="08ebd-132">您將會收到和已完成下載之聯合市集項目有關的重複通知。</span><span class="sxs-lookup"><span data-stu-id="08ebd-132">You will receive repeated notifications for syndicated marketplace items that have completed downloading.</span></span>
* <span data-ttu-id="08ebd-133">您不能 tooview 權限 tooyour 使用 hello Azure 堆疊入口網站的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="08ebd-133">You are not able tooview permissions tooyour subscription using hello Azure Stack portals.</span></span>  <span data-ttu-id="08ebd-134">解決方法是，可以使用 Powershell 確認權限。</span><span class="sxs-lookup"><span data-stu-id="08ebd-134">As a work-around, you can verify permissions using Powershell.</span></span>
* <span data-ttu-id="08ebd-135">您必須新增`-TenantID`做為從 hello 入口網站的自動化指令碼匯出已完成的部署時的旗標。</span><span class="sxs-lookup"><span data-stu-id="08ebd-135">You must add `-TenantID` as a flag when exporting a completed deployment as an automation script from hello portal.</span></span>

#### <a name="services"></a><span data-ttu-id="08ebd-136">服務</span><span class="sxs-lookup"><span data-stu-id="08ebd-136">Services</span></span>
* <span data-ttu-id="08ebd-137">金鑰保存庫服務必須建立從 hello 租用戶入口網站或租用戶 API。</span><span class="sxs-lookup"><span data-stu-id="08ebd-137">Key Vault services must be created from hello tenant portal or tenant API.</span></span>  <span data-ttu-id="08ebd-138">如果您以系統管理員身分登入，請確定 toouse hello 租用戶入口網站 toocreate 新的金鑰保存庫保存庫、 機密資料，並且索引鍵。</span><span class="sxs-lookup"><span data-stu-id="08ebd-138">If you are logged in as an administrator, make sure toouse hello tenant portal toocreate new Key Vault vaults, secrets, and keys.</span></span>
* <span data-ttu-id="08ebd-139">雖然可以透過範本建立虛擬機器擴展集，但是沒有可用於建立它們的市集體驗。</span><span class="sxs-lookup"><span data-stu-id="08ebd-139">There is no marketplace experience for creating virtual machine scale sets, though they can be created via template.</span></span>
* <span data-ttu-id="08ebd-140">您無法將負載平衡器與 hello 入口網站透過後端 」 網路。</span><span class="sxs-lookup"><span data-stu-id="08ebd-140">You cannot associate a load balancer with a backend network via hello portal.</span></span>  <span data-ttu-id="08ebd-141">此工作可以透過 PowerShell 或透過範本來完成。</span><span class="sxs-lookup"><span data-stu-id="08ebd-141">This task can be completed with PowerShell or with a template.</span></span>
* <span data-ttu-id="08ebd-142">VM 可用性設定組只能設定一個容錯網域和一個更新網域。</span><span class="sxs-lookup"><span data-stu-id="08ebd-142">VM Availability sets can only be configured with a fault domain of one and an update domain of one.</span></span>  
* <span data-ttu-id="08ebd-143">租用戶必須有現有的儲存體帳戶，才能建立新的 Azure Function。</span><span class="sxs-lookup"><span data-stu-id="08ebd-143">A tenant must have an existing storage account before creating a new Azure Function.</span></span>
* <span data-ttu-id="08ebd-144">VM 可能會失敗並報告 「 無法繫結引數 tooparameter 'VM 網路介面卡' 因為它是 null。 」</span><span class="sxs-lookup"><span data-stu-id="08ebd-144">VM may fail and report "Cannot bind argument tooparameter 'VM Network Adapter' because it is null."</span></span>  <span data-ttu-id="08ebd-145">重新部署的 hello 虛擬機器就會成功。</span><span class="sxs-lookup"><span data-stu-id="08ebd-145">Redeployment of hello virtual machine succeeds.</span></span>  
* <span data-ttu-id="08ebd-146">刪除租用戶訂用帳戶會導致產生孤立的資源。</span><span class="sxs-lookup"><span data-stu-id="08ebd-146">Deleting tenant subscriptions results in orphaned resources.</span></span>  <span data-ttu-id="08ebd-147">因應措施是，先刪除租用戶資源或整個資源群組，然後再刪除租用戶訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="08ebd-147">As a workaround, first delete tenant resources or entire resource group, and then delete tenant subscriptions.</span></span> 
* <span data-ttu-id="08ebd-148">建立網路負載平衡器時，您必須建立 NAT 規則，或當您嘗試 tooadd NAT 規則建立 hello 負載平衡器後，您會收到錯誤。</span><span class="sxs-lookup"><span data-stu-id="08ebd-148">You must create a NAT rule when creating a network load balancer, or you will receive an error when you attempt tooadd a NAT rule after hello load balancer is created.</span></span>
* <span data-ttu-id="08ebd-149">租用戶可以建立大於配額允許大小的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="08ebd-149">Tenants can create virtual machines larger than quota allows.</span></span>  <span data-ttu-id="08ebd-150">此行為是因為未強制套用計算配額。</span><span class="sxs-lookup"><span data-stu-id="08ebd-150">This behavior is because compute quotas are not enforced.</span></span>
* <span data-ttu-id="08ebd-151">租用戶不指定的 hello 選項 toocreate 具有地理備援儲存體的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="08ebd-151">Tenants are given hello option toocreate a virtual machine with geo-redundant storage.</span></span>  <span data-ttu-id="08ebd-152">此組態導致虛擬機器建立 toofail。</span><span class="sxs-lookup"><span data-stu-id="08ebd-152">This configuration causes virtual machine creation toofail.</span></span>
* <span data-ttu-id="08ebd-153">它可能會佔用 tooan 小時之前租用戶可以在新的 SQL 或 MySQL SKU 中建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="08ebd-153">It can take up tooan hour before tenants can create databases in a new SQL or MySQL SKU.</span></span> 
* <span data-ttu-id="08ebd-154">建立直接在 SQL 和 MySQL 主控伺服器不會執行 hello 資源提供者上的項目不支援，以及可能會導致不相符的狀態。</span><span class="sxs-lookup"><span data-stu-id="08ebd-154">Creation of items directly on SQL and MySQL hosting servers that are not performed by hello resource provider is not supported and may result in mismatched state.</span></span>
* <span data-ttu-id="08ebd-155">AzureRM PowerShell 1.2.10 需要額外的設定步驟：</span><span class="sxs-lookup"><span data-stu-id="08ebd-155">AzureRM PowerShell 1.2.10 requires extra configuration steps:</span></span>
    * <span data-ttu-id="08ebd-156">請在執行 Azure AD 部署的 Add-AzureRMEnvironment 之後執行此作業。</span><span class="sxs-lookup"><span data-stu-id="08ebd-156">Run this after running Add-AzureRMEnvironment for Azure AD deployments.</span></span>  <span data-ttu-id="08ebd-157">提供使用 hello 輸出 hello 名稱] 和 [GraphAudience 值`Add-AzureRMEnvironment`。</span><span class="sxs-lookup"><span data-stu-id="08ebd-157">Provide hello Name and GraphAudience values using hello output from `Add-AzureRMEnvironment`.</span></span>
      
      ```PowerShell
      Set-AzureRmEnvironment -Name <Environment Name> -GraphAudience <Graph Endpoint URL>
      ```
    * <span data-ttu-id="08ebd-158">請在執行 AD FS 部署的 Add-AzureRMEnvironment 之後執行此作業。</span><span class="sxs-lookup"><span data-stu-id="08ebd-158">Run this after running Add-AzureRMEnvironment for AD FS deployments.</span></span>  <span data-ttu-id="08ebd-159">提供使用的 hello 輸出 hello 名稱] 和 [GraphAudience 值`Add-AzureRMEnvironment`。</span><span class="sxs-lookup"><span data-stu-id="08ebd-159">Provide hello Name and GraphAudience values using hello output of `Add-AzureRMEnvironment`.</span></span>
      
      ```PowerShell
      Set-AzureRmEnvironment <Environment Name> -GraphAudience <Graph Endpoint URL> -EnableAdfsAuthentication:$true
      ```
    
    <span data-ttu-id="08ebd-160">例如，hello 下列可用於 Azure AD 環境：</span><span class="sxs-lookup"><span data-stu-id="08ebd-160">As an example, hello following is used for an Azure AD environment:</span></span>

    ```PowerShell
      Set-AzureRmEnvironment AzureStack -GraphAudience https://graph.local.azurestack.external/
    ```

#### <a name="fabric"></a><span data-ttu-id="08ebd-161">網狀架構</span><span class="sxs-lookup"><span data-stu-id="08ebd-161">Fabric</span></span>
* <span data-ttu-id="08ebd-162">hello 計算資源提供者顯示未知的狀態。</span><span class="sxs-lookup"><span data-stu-id="08ebd-162">hello compute resource provider displays an unknown state.</span></span>
* <span data-ttu-id="08ebd-163">hello 必要節點資訊的延展單位中未顯示 hello BMC IP 位址 （& s） 模型。</span><span class="sxs-lookup"><span data-stu-id="08ebd-163">hello BMC IP address & model are not shown in hello essential information of a Scale Unit Node.</span></span>  <span data-ttu-id="08ebd-164">這是 Azure Stack 開發套件中的預期行為。</span><span class="sxs-lookup"><span data-stu-id="08ebd-164">This behavior is expected in Azure Stack development kit.</span></span>
* <span data-ttu-id="08ebd-165">不應該使用 hello 計算控制器基礎結構角色 （AzS XRP01 執行個體） 上的重新啟動動作。</span><span class="sxs-lookup"><span data-stu-id="08ebd-165">hello restart action on Compute controller infrastructure role (AzS-XRP01 instance) should not be used.</span></span>
* <span data-ttu-id="08ebd-166">hello 備份刀鋒視窗中不應使用的基礎結構。</span><span class="sxs-lookup"><span data-stu-id="08ebd-166">hello Infrastructure backup blade should not be used.</span></span>
