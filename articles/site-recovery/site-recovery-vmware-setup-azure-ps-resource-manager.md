---
title: " 管理在 Azure 中執行的處理伺服器 (Resource Manager) | Microsoft Doc"
description: "本文說明如何 tooset 向上容錯回復程序 （資源管理員） 在 Azure 中。"
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
ms.openlocfilehash: 70426b96095cc42befff6c4114fb56536284a667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-process-server-running-in-azure-resource-manager"></a><span data-ttu-id="321af-103">管理在 Azure 中執行的處理伺服器 (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="321af-103">Manage a process server running in Azure (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="321af-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="321af-104">Resource Manager</span></span>](./site-recovery-vmware-setup-azure-ps-resource-manager.md)
> * [<span data-ttu-id="321af-105">傳統</span><span class="sxs-lookup"><span data-stu-id="321af-105">Classic </span></span>](./site-recovery-vmware-setup-azure-ps-classic.md)

<span data-ttu-id="321af-106">容錯回復期間建議 toodeploy 處理序伺服器在 Azure 中的如果有高延遲 hello Azure 虛擬網路與內部部署網路之間。</span><span class="sxs-lookup"><span data-stu-id="321af-106">During failback, it is recommended toodeploy process server in Azure if there is high latency between hello Azure Virtual Network and your on-premises network.</span></span> <span data-ttu-id="321af-107">本文說明如何設定、 設定和管理在 Azure 中執行的 hello 處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="321af-107">This article describes how you can set up, configure, and manage hello process servers running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="321af-108">本文是如果您使用使用 toobe**資源管理員**為 hello 虛擬機器在容錯移轉期間的 hello 部署模型。</span><span class="sxs-lookup"><span data-stu-id="321af-108">This article is toobe used if you used **Resource Manager** as hello deployment model for hello virtual machines during failover.</span></span> <span data-ttu-id="321af-109">如果您使用**傳統**為 hello 部署模型，請依照下列中的 hello 步驟[如何 tooset 向上及設定容錯移轉處理伺服器 （傳統）](./site-recovery-vmware-setup-azure-ps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="321af-109">If you used **Classic** as hello deployment model, follow hello steps in [How tooset up & configure a Failback process server (Classic)](./site-recovery-vmware-setup-azure-ps-classic.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="321af-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="321af-110">Prerequisites</span></span>

[!INCLUDE [site-recovery-vmware-process-server-prerequ](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a><span data-ttu-id="321af-111">在 Azure 上部署處理伺服器</span><span class="sxs-lookup"><span data-stu-id="321af-111">Deploy a process server on Azure</span></span>
1. <span data-ttu-id="321af-112">在 hello 保存庫 > **Site Recovery 基礎結構**（在 hello 「 管理 」 標題） >**設定伺服器**（在 「 適用於 VMware 和實體機器 」 標題下），選取 hello 組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="321af-112">In hello Vault > **Site Recovery Infrastructure** (under hello "Manage" heading) > **Configuration Servers** (under "For VMware and Physical Machines" heading), select hello configuration server.</span></span>
2. <span data-ttu-id="321af-113">在開啟的 hello 組態伺服器詳細資料頁面中按一下"+ 處理伺服器 」</span><span class="sxs-lookup"><span data-stu-id="321af-113">In hello Configuration Server details page that opens click "+ Process server"</span></span>

  ![新增處理伺服器資源庫](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps.png)

3.  <span data-ttu-id="321af-115">在 hello**新增處理序伺服器**頁面上，選取下列值的 hello</span><span class="sxs-lookup"><span data-stu-id="321af-115">On hello **Add process server** page, select hello following values</span></span>

  ![新增處理伺服器資源庫項目](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-1.png)
|<span data-ttu-id="321af-117">**欄位名稱**</span><span class="sxs-lookup"><span data-stu-id="321af-117">**Field Name**</span></span>|<span data-ttu-id="321af-118">**值**</span><span class="sxs-lookup"><span data-stu-id="321af-118">**Value**</span></span>|
|-|-|
|<span data-ttu-id="321af-119">選擇您希望 toodeploy 處理序伺服器</span><span class="sxs-lookup"><span data-stu-id="321af-119">Choose where you want toodeploy your process server</span></span>|<span data-ttu-id="321af-120">選取 hello 值**部署在 Azure 中的容錯回復處理序伺服器**</span><span class="sxs-lookup"><span data-stu-id="321af-120">Select hello value **Deploy a failback process server in Azure**</span></span> |
|<span data-ttu-id="321af-121">訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="321af-121">Subscription</span></span>|<span data-ttu-id="321af-122">選取 hello 容錯 hello 虛擬機器的 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="321af-122">Select hello Azure Subscription where you failed over hello virtual machines</span></span>|
|<span data-ttu-id="321af-123">資源群組</span><span class="sxs-lookup"><span data-stu-id="321af-123">Resource Group</span></span>|<span data-ttu-id="321af-124">您可以建立資源群組 toodeploy 此處理序伺服器，或在現有的資源群組中選擇 toodeploy hello 處理序伺服器</span><span class="sxs-lookup"><span data-stu-id="321af-124">You can create a Resource Group toodeploy this process server or choose toodeploy hello process server in an existing Resource Group</span></span>|
|<span data-ttu-id="321af-125">位置</span><span class="sxs-lookup"><span data-stu-id="321af-125">Location</span></span>|<span data-ttu-id="321af-126">Hello Azure 資料中心選取成哪一個 hello 虛擬機器在容錯移轉至</span><span class="sxs-lookup"><span data-stu-id="321af-126">Select hello Azure Data Center into which hello virtual machines where failed over into</span></span>|
|<span data-ttu-id="321af-127">Azure 網路</span><span class="sxs-lookup"><span data-stu-id="321af-127">Azure Network</span></span>|<span data-ttu-id="321af-128">選取 hello Azure hello 虛擬機器的虛擬 Network(VNet) 容錯移轉到其中。</span><span class="sxs-lookup"><span data-stu-id="321af-128">Select hello Azure Virtual Network(VNet) that hello virtual machines where failed over into.</span></span> <span data-ttu-id="321af-129">如果將虛擬機器容錯回復到多個 Azure VNet，則您需要在每個 VNet 上部署一部處理伺服器</span><span class="sxs-lookup"><span data-stu-id="321af-129">If you failed over virtual machines into multiple Azure VNets, then you need a process server deployed per VNet</span></span>|

4. <span data-ttu-id="321af-130">在 hello 之處理序伺服器 hello 屬性 hello 其餘部分填滿</span><span class="sxs-lookup"><span data-stu-id="321af-130">Fill in hello rest of hello properties for hello process server</span></span>

  ![新增處理伺服器摘要](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-2.png)
|<span data-ttu-id="321af-132">**欄位名稱**</span><span class="sxs-lookup"><span data-stu-id="321af-132">**Field Name**</span></span>|<span data-ttu-id="321af-133">**值**</span><span class="sxs-lookup"><span data-stu-id="321af-133">**Value**</span></span>|
|-|-|
|<span data-ttu-id="321af-134">伺服器名稱</span><span class="sxs-lookup"><span data-stu-id="321af-134">Server Name</span></span>|<span data-ttu-id="321af-135">處理伺服器虛擬機器的顯示名稱與主機名稱</span><span class="sxs-lookup"><span data-stu-id="321af-135">Display name & Host name for your process server virtual machine</span></span>|
| <span data-ttu-id="321af-136">使用者名稱</span><span class="sxs-lookup"><span data-stu-id="321af-136">User Name</span></span>|<span data-ttu-id="321af-137">會成為該虛擬機器上系統管理員的使用者名稱</span><span class="sxs-lookup"><span data-stu-id="321af-137">A user name that becomes an Administrator on that virtual machine</span></span>|
|<span data-ttu-id="321af-138">儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="321af-138">Storage Account</span></span>|<span data-ttu-id="321af-139">Hello 放置 hello 虛擬機器的虛擬磁碟的儲存體帳戶的名稱</span><span class="sxs-lookup"><span data-stu-id="321af-139">Name of hello Storage Account where hello virtual machine's virtual disk's are placed</span></span>|
|<span data-ttu-id="321af-140">子網路</span><span class="sxs-lookup"><span data-stu-id="321af-140">Subnet</span></span>|<span data-ttu-id="321af-141">hello hello Azure VNet toowhich hello 虛擬機器的子網路連線</span><span class="sxs-lookup"><span data-stu-id="321af-141">hello subnet of hello Azure VNet toowhich hello virtual machine is connected</span></span>|
| <span data-ttu-id="321af-142">IP 位址</span><span class="sxs-lookup"><span data-stu-id="321af-142">IP Address</span></span>|<span data-ttu-id="321af-143">IP 位址，您想要的 hello 處理序伺服器 tooassume 一次它開機。</span><span class="sxs-lookup"><span data-stu-id="321af-143">IP Address that you would like hello process server tooassume once it boots up</span></span>|
5. <span data-ttu-id="321af-144">按一下 hello 「 確定 」 按鈕 toostart hello 處理序伺服器的虛擬機器部署。</span><span class="sxs-lookup"><span data-stu-id="321af-144">Click hello OK button toostart deploying hello process server virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="321af-145">toobe 無法 toouse 此處理序伺服器進行容錯回復，您需要 tooregister 它與 hello 在內部部署組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="321af-145">toobe able toouse this process server for failback, you need tooregister it with hello on-premises configuration server.</span></span>

## <a name="registering-hello-process-server-running-in-azure-tooa-configuration-server-running-on-premises"></a><span data-ttu-id="321af-146">註冊 hello 處理序伺服器 （在 Azure 中執行） tooa 組態伺服器 （執行內部部署）</span><span class="sxs-lookup"><span data-stu-id="321af-146">Registering hello process server (running in Azure) tooa Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-hello-process-server-toolatest-version"></a><span data-ttu-id="321af-147">升級 hello 處理序伺服器 toolatest 版本。</span><span class="sxs-lookup"><span data-stu-id="321af-147">Upgrading hello process server toolatest version.</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-hello-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a><span data-ttu-id="321af-148">取消註冊 hello 處理序伺服器 （在 Azure 中執行），從組態伺服器 （執行內部部署）</span><span class="sxs-lookup"><span data-stu-id="321af-148">Unregistering hello process server (running in Azure) from a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-unregister-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
