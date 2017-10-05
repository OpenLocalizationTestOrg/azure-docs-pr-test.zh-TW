---
title: " 管理在 Azure 中執行的處理伺服器 (Resource Manager) | Microsoft Doc"
description: "使文章說明如何在 Azure 中設定容錯回復處理伺服器 (Resource Manager)。"
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 2b9b31abd5d11d02935a74e47d26be9803cdc920
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-a-process-server-running-in-azure-resource-manager"></a><span data-ttu-id="4f2ab-103">管理在 Azure 中執行的處理伺服器 (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="4f2ab-103">Manage a process server running in Azure (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4f2ab-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4f2ab-104">Resource Manager</span></span>](./site-recovery-vmware-setup-azure-ps-resource-manager.md)
> * [<span data-ttu-id="4f2ab-105">傳統</span><span class="sxs-lookup"><span data-stu-id="4f2ab-105">Classic </span></span>](./site-recovery-vmware-setup-azure-ps-classic.md)

<span data-ttu-id="4f2ab-106">在容錯回復期間，如果 Azure 虛擬網路和您的內部部署網路之間發生高延遲，則建議在 Azure 中部署處理伺服器。</span><span class="sxs-lookup"><span data-stu-id="4f2ab-106">During failback, it is recommended to deploy process server in Azure if there is high latency between the Azure Virtual Network and your on-premises network.</span></span> <span data-ttu-id="4f2ab-107">此文章說明如何設定、配置及管理在 Azure 中執行的處理伺服器。</span><span class="sxs-lookup"><span data-stu-id="4f2ab-107">This article describes how you can set up, configure, and manage the process servers running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="4f2ab-108">若要在容錯回復期間使用 **Resource Manager** 做為虛擬機器部署模型，可以參考此文章。</span><span class="sxs-lookup"><span data-stu-id="4f2ab-108">This article is to be used if you used **Resource Manager** as the deployment model for the virtual machines during failover.</span></span> <span data-ttu-id="4f2ab-109">如果您使用「傳統」部署模型，請依照[如何設定及配置容錯回復處理序伺服器 (傳統)](./site-recovery-vmware-setup-azure-ps-classic.md) 中的步驟執行</span><span class="sxs-lookup"><span data-stu-id="4f2ab-109">If you used **Classic** as the deployment model, follow the steps in [How to set up & configure a Failback process server (Classic)](./site-recovery-vmware-setup-azure-ps-classic.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4f2ab-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="4f2ab-110">Prerequisites</span></span>

[!INCLUDE [site-recovery-vmware-process-server-prerequ](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a><span data-ttu-id="4f2ab-111">在 Azure 上部署處理伺服器</span><span class="sxs-lookup"><span data-stu-id="4f2ab-111">Deploy a process server on Azure</span></span>
1. <span data-ttu-id="4f2ab-112">在 保存庫 > 位於 管理 標題下方的 Site Recovery 基礎結構 > 位於 適用於 VMware 與實體機器 標題下方 組態伺服器 中，選取組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="4f2ab-112">In the Vault > **Site Recovery Infrastructure** (under the "Manage" heading) > **Configuration Servers** (under "For VMware and Physical Machines" heading), select the configuration server.</span></span>
2. <span data-ttu-id="4f2ab-113">在開啟的組態伺服器詳細資料頁面中按一下 [+ 處理伺服器]</span><span class="sxs-lookup"><span data-stu-id="4f2ab-113">In the Configuration Server details page that opens click "+ Process server"</span></span>

  ![新增處理伺服器資源庫](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps.png)

3.  <span data-ttu-id="4f2ab-115">在 [新增處理伺服器] 頁面上，選取下列值</span><span class="sxs-lookup"><span data-stu-id="4f2ab-115">On the **Add process server** page, select the following values</span></span>

  ![新增處理伺服器資源庫項目](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-1.png)
|<span data-ttu-id="4f2ab-117">**欄位名稱**</span><span class="sxs-lookup"><span data-stu-id="4f2ab-117">**Field Name**</span></span>|<span data-ttu-id="4f2ab-118">**值**</span><span class="sxs-lookup"><span data-stu-id="4f2ab-118">**Value**</span></span>|
|-|-|
|<span data-ttu-id="4f2ab-119">選擇您要部署處理伺服器的位置</span><span class="sxs-lookup"><span data-stu-id="4f2ab-119">Choose where you want to deploy your process server</span></span>|<span data-ttu-id="4f2ab-120">選取 [在 Azure 中部署容錯回復處理伺服器] 值</span><span class="sxs-lookup"><span data-stu-id="4f2ab-120">Select the value **Deploy a failback process server in Azure**</span></span> |
|<span data-ttu-id="4f2ab-121">訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="4f2ab-121">Subscription</span></span>|<span data-ttu-id="4f2ab-122">選取容錯回復虛擬機器的 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="4f2ab-122">Select the Azure Subscription where you failed over the virtual machines</span></span>|
|<span data-ttu-id="4f2ab-123">資源群組</span><span class="sxs-lookup"><span data-stu-id="4f2ab-123">Resource Group</span></span>|<span data-ttu-id="4f2ab-124">您可以建立要部署此處理伺服器的資源群組，或選擇要在其中部署處理伺服器的現有資源群組</span><span class="sxs-lookup"><span data-stu-id="4f2ab-124">You can create a Resource Group to deploy this process server or choose to deploy the process server in an existing Resource Group</span></span>|
|<span data-ttu-id="4f2ab-125">位置</span><span class="sxs-lookup"><span data-stu-id="4f2ab-125">Location</span></span>|<span data-ttu-id="4f2ab-126">選取做為虛擬機器容錯回復目標的 Azure 資料中心</span><span class="sxs-lookup"><span data-stu-id="4f2ab-126">Select the Azure Data Center into which the virtual machines where failed over into</span></span>|
|<span data-ttu-id="4f2ab-127">Azure 網路</span><span class="sxs-lookup"><span data-stu-id="4f2ab-127">Azure Network</span></span>|<span data-ttu-id="4f2ab-128">選取做為虛擬機器容錯回復目標的 Azure 虛擬網路 (VNet)</span><span class="sxs-lookup"><span data-stu-id="4f2ab-128">Select the Azure Virtual Network(VNet) that the virtual machines where failed over into.</span></span> <span data-ttu-id="4f2ab-129">如果將虛擬機器容錯回復到多個 Azure VNet，則您需要在每個 VNet 上部署一部處理伺服器</span><span class="sxs-lookup"><span data-stu-id="4f2ab-129">If you failed over virtual machines into multiple Azure VNets, then you need a process server deployed per VNet</span></span>|

4. <span data-ttu-id="4f2ab-130">填入其餘的處理伺服器內容</span><span class="sxs-lookup"><span data-stu-id="4f2ab-130">Fill in the rest of the properties for the process server</span></span>

  ![新增處理伺服器摘要](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-2.png)
|<span data-ttu-id="4f2ab-132">**欄位名稱**</span><span class="sxs-lookup"><span data-stu-id="4f2ab-132">**Field Name**</span></span>|<span data-ttu-id="4f2ab-133">**值**</span><span class="sxs-lookup"><span data-stu-id="4f2ab-133">**Value**</span></span>|
|-|-|
|<span data-ttu-id="4f2ab-134">伺服器名稱</span><span class="sxs-lookup"><span data-stu-id="4f2ab-134">Server Name</span></span>|<span data-ttu-id="4f2ab-135">處理伺服器虛擬機器的顯示名稱與主機名稱</span><span class="sxs-lookup"><span data-stu-id="4f2ab-135">Display name & Host name for your process server virtual machine</span></span>|
| <span data-ttu-id="4f2ab-136">使用者名稱</span><span class="sxs-lookup"><span data-stu-id="4f2ab-136">User Name</span></span>|<span data-ttu-id="4f2ab-137">會成為該虛擬機器上系統管理員的使用者名稱</span><span class="sxs-lookup"><span data-stu-id="4f2ab-137">A user name that becomes an Administrator on that virtual machine</span></span>|
|<span data-ttu-id="4f2ab-138">儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="4f2ab-138">Storage Account</span></span>|<span data-ttu-id="4f2ab-139">放置虛擬機器之虛擬磁碟的儲存體帳戶名稱</span><span class="sxs-lookup"><span data-stu-id="4f2ab-139">Name of the Storage Account where the virtual machine's virtual disk's are placed</span></span>|
|<span data-ttu-id="4f2ab-140">子網路</span><span class="sxs-lookup"><span data-stu-id="4f2ab-140">Subnet</span></span>|<span data-ttu-id="4f2ab-141">虛擬機器應該連接之 Azure VNet 的子網路</span><span class="sxs-lookup"><span data-stu-id="4f2ab-141">The subnet of the Azure VNet to which the virtual machine is connected</span></span>|
| <span data-ttu-id="4f2ab-142">IP 位址</span><span class="sxs-lookup"><span data-stu-id="4f2ab-142">IP Address</span></span>|<span data-ttu-id="4f2ab-143">您想要處理伺服器一旦開機後要採用的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="4f2ab-143">IP Address that you would like the process server to assume once it boots up</span></span>|
5. <span data-ttu-id="4f2ab-144">按一下 [確定] 按鈕來開始部署處理伺服器虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="4f2ab-144">Click the OK button to start deploying the process server virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="4f2ab-145">為了能夠使用此處理伺服器進行容錯回復，您必須向內部部署組態伺服器註冊它。</span><span class="sxs-lookup"><span data-stu-id="4f2ab-145">To be able to use this process server for failback, you need to register it with the on-premises configuration server.</span></span>

## <a name="registering-the-process-server-running-in-azure-to-a-configuration-server-running-on-premises"></a><span data-ttu-id="4f2ab-146">將處理伺服器 (在 Azure 中執行) 註冊到組態伺服器 (在內部部署上執行)</span><span class="sxs-lookup"><span data-stu-id="4f2ab-146">Registering the process server (running in Azure) to a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-the-process-server-to-latest-version"></a><span data-ttu-id="4f2ab-147">將處理伺服器升級到最新版本。</span><span class="sxs-lookup"><span data-stu-id="4f2ab-147">Upgrading the process server to latest version.</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-the-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a><span data-ttu-id="4f2ab-148">從組態伺服器 (在內部部署上執行) 取消註冊處理伺服器 (在 Azure 中執行)</span><span class="sxs-lookup"><span data-stu-id="4f2ab-148">Unregistering the process server (running in Azure) from a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-unregister-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
