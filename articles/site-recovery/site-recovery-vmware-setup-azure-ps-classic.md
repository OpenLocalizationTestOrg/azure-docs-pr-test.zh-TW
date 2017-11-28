---
title: " 管理在 Azure 中執行的處理伺服器 (傳統) | Microsoft Docs"
description: "本文說明如何 tooset 容錯回復程序 Server(Classic) 在 Azure 上的。"
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
ms.openlocfilehash: eadcc0236c77c9ebbbc885c4a7ee81098f1f4e72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-process-server-running-in-azure-classic"></a><span data-ttu-id="9bdd4-103">管理在 Azure 中執行的處理伺服器 (傳統)</span><span class="sxs-lookup"><span data-stu-id="9bdd4-103">Manage a Process Server running in Azure (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9bdd4-104">Azure 傳統</span><span class="sxs-lookup"><span data-stu-id="9bdd4-104">Azure Classic </span></span>](./site-recovery-vmware-setup-azure-ps-classic.md)
> * [<span data-ttu-id="9bdd4-105">資源管理員</span><span class="sxs-lookup"><span data-stu-id="9bdd4-105">Resource Manager</span></span>](./site-recovery-vmware-setup-azure-ps-resource-manager.md)

<span data-ttu-id="9bdd4-106">容錯回復期間建議 toodeploy 在 Azure 中的處理序伺服器是否有高延遲 hello Azure 虛擬網路與內部部署網路之間。</span><span class="sxs-lookup"><span data-stu-id="9bdd4-106">During failback, it is recommended toodeploy Process Server in Azure if there is high latency between hello Azure Virtual Network and your on-premises network.</span></span> <span data-ttu-id="9bdd4-107">本文說明如何設定、 設定和管理在 Azure 中執行的 hello 處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="9bdd4-107">This article describes how you can set up, configure, and manage hello process servers running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="9bdd4-108">本文是 toobe 如果您使用傳統做 hello 部署模型為 hello 虛擬機器在容錯移轉期間使用。</span><span class="sxs-lookup"><span data-stu-id="9bdd4-108">This article is toobe used if you used Classic as hello deployment model for hello virtual machines during failover.</span></span> <span data-ttu-id="9bdd4-109">如果您使用資源管理員部署模型後續 hello 步驟中的 hello[如何 tooset 向上及設定容錯移轉處理伺服器 （資源管理員）](./site-recovery-vmware-setup-azure-ps-resource-manager.md)</span><span class="sxs-lookup"><span data-stu-id="9bdd4-109">If you used Resource Manager as hello deployment model follow hello steps in [How tooset up & configure a Failback Process Server (Resource Manager)](./site-recovery-vmware-setup-azure-ps-resource-manager.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9bdd4-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="9bdd4-110">Prerequisites</span></span>

[!INCLUDE [site-recovery-vmware-process-server-prereq](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a><span data-ttu-id="9bdd4-111">在 Azure 上部署處理伺服器</span><span class="sxs-lookup"><span data-stu-id="9bdd4-111">Deploy a Process Server on Azure</span></span>

1. <span data-ttu-id="9bdd4-112">在 Azure Marketplace 中建立虛擬機器使用 hello **Microsoft Azure 站台復原處理序伺服器 V2**</span><span class="sxs-lookup"><span data-stu-id="9bdd4-112">In Azure Marketplace, create a virtual machine using hello **Microsoft Azure Site Recovery Process Server V2**</span></span> </br>
    <span data-ttu-id="9bdd4-113">![Marketplace_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image.png)</span><span class="sxs-lookup"><span data-stu-id="9bdd4-113">![Marketplace_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image.png)</span></span>
2. <span data-ttu-id="9bdd4-114">請確定您選取做為 hello 部署模型**傳統**</span><span class="sxs-lookup"><span data-stu-id="9bdd4-114">Ensure that you select hello deployment model as **Classic**</span></span> </br><span data-ttu-id="9bdd4-115">
  ![Marketplace_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image-classic.png)</span><span class="sxs-lookup"><span data-stu-id="9bdd4-115">
![Marketplace_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image-classic.png)</span></span>
3. <span data-ttu-id="9bdd4-116">在 hello 建立虛擬機器精靈 > 基本設定，請確定您選取 hello 訂用帳戶和位置 toowhere 您容錯 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="9bdd4-116">In hello Create virtual machine wizard > Basic Settings, ensure you select hello Subscription and Location toowhere you failed over hello virtual machines.</span></span></br><span data-ttu-id="9bdd4-117">
  ![create_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-basic-info.png)</span><span class="sxs-lookup"><span data-stu-id="9bdd4-117">
![create_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-basic-info.png)</span></span>
4. <span data-ttu-id="9bdd4-118">請確認 hello 虛擬機器已連線 toohello Azure 虛擬網路 toowhich hello 容錯移轉虛擬機器已連線。</span><span class="sxs-lookup"><span data-stu-id="9bdd4-118">Ensure that hello virtual machine is connected toohello Azure Virtual Network toowhich hello failed over virtual machine is connected.</span></span></br><span data-ttu-id="9bdd4-119">
  ![create_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-settings.png)</span><span class="sxs-lookup"><span data-stu-id="9bdd4-119">
![create_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-settings.png)</span></span>
5. <span data-ttu-id="9bdd4-120">Hello 處理序伺服器的虛擬機器已佈建之後，您需要在 toolog，並向 hello 組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="9bdd4-120">Once hello Process Server virtual machine is provisioned, you need toolog in and register it with hello Configuration Server.</span></span>

> [!NOTE]
> <span data-ttu-id="9bdd4-121">toobe 無法 toouse 此處理序伺服器進行容錯回復，您需要 tooregister 它與 hello 在內部部署組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="9bdd4-121">toobe able toouse this Process Server for failback, you need tooregister it with hello on-premises configuration server.</span></span>

## <a name="registering-hello-process-server-running-in-azure-tooa-configuration-server-running-on-premises"></a><span data-ttu-id="9bdd4-122">註冊 hello （在 Azure 中執行） 的處理序伺服器 tooa 組態伺服器 （執行內部部署）</span><span class="sxs-lookup"><span data-stu-id="9bdd4-122">Registering hello Process Server (running in Azure) tooa Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-hello-process-server-toolatest-version"></a><span data-ttu-id="9bdd4-123">Hello 處理序伺服器 toolatest 版本升級。</span><span class="sxs-lookup"><span data-stu-id="9bdd4-123">Upgrading hello Process Server toolatest version.</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-hello-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a><span data-ttu-id="9bdd4-124">正在移除註冊 hello 處理序伺服器 （在 Azure 中執行） 從組態伺服器 （執行內部部署）</span><span class="sxs-lookup"><span data-stu-id="9bdd4-124">Unregistering hello Process Server (running in Azure) from a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
