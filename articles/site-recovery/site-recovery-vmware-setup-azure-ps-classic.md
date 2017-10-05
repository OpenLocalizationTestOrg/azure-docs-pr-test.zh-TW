---
title: " 管理在 Azure 中執行的處理伺服器 (傳統) | Microsoft Docs"
description: "此文章說明如何在 Azure 中設定容錯回復處理伺服器 (傳統)。"
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
ms.openlocfilehash: 479bbd207bcf715138c340f9e4d2634120bab85c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-a-process-server-running-in-azure-classic"></a><span data-ttu-id="6bfcb-103">管理在 Azure 中執行的處理伺服器 (傳統)</span><span class="sxs-lookup"><span data-stu-id="6bfcb-103">Manage a Process Server running in Azure (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6bfcb-104">Azure 傳統</span><span class="sxs-lookup"><span data-stu-id="6bfcb-104">Azure Classic </span></span>](./site-recovery-vmware-setup-azure-ps-classic.md)
> * [<span data-ttu-id="6bfcb-105">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6bfcb-105">Resource Manager</span></span>](./site-recovery-vmware-setup-azure-ps-resource-manager.md)

<span data-ttu-id="6bfcb-106">在容錯回復期間，如果 Azure 虛擬網路和您的內部部署網路之間發生高延遲，則建議在 Azure 中部署處理伺服器。</span><span class="sxs-lookup"><span data-stu-id="6bfcb-106">During failback, it is recommended to deploy Process Server in Azure if there is high latency between the Azure Virtual Network and your on-premises network.</span></span> <span data-ttu-id="6bfcb-107">此文章說明如何設定、配置及管理在 Azure 中執行的處理伺服器。</span><span class="sxs-lookup"><span data-stu-id="6bfcb-107">This article describes how you can set up, configure, and manage the process servers running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="6bfcb-108">如果在容錯移轉期間使用「傳統」作為虛擬機器部署模型，可以參考此文章。</span><span class="sxs-lookup"><span data-stu-id="6bfcb-108">This article is to be used if you used Classic as the deployment model for the virtual machines during failover.</span></span> <span data-ttu-id="6bfcb-109">如果您使用 Resource Manager 作為部署模型，請依照[如何設定及配置容錯回復處理伺服器 (Resource Manager)](./site-recovery-vmware-setup-azure-ps-resource-manager.md) 中的步驟執行</span><span class="sxs-lookup"><span data-stu-id="6bfcb-109">If you used Resource Manager as the deployment model follow the steps in [How to set up & configure a Failback Process Server (Resource Manager)](./site-recovery-vmware-setup-azure-ps-resource-manager.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6bfcb-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="6bfcb-110">Prerequisites</span></span>

[!INCLUDE [site-recovery-vmware-process-server-prereq](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a><span data-ttu-id="6bfcb-111">在 Azure 上部署處理伺服器</span><span class="sxs-lookup"><span data-stu-id="6bfcb-111">Deploy a Process Server on Azure</span></span>

1. <span data-ttu-id="6bfcb-112">在 Azure Marketplace 中，使用 **Microsoft Azure Site Recovery 處理伺服器 V2** 建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="6bfcb-112">In Azure Marketplace, create a virtual machine using the **Microsoft Azure Site Recovery Process Server V2**</span></span> </br>
    <span data-ttu-id="6bfcb-113">![Marketplace_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image.png)</span><span class="sxs-lookup"><span data-stu-id="6bfcb-113">![Marketplace_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image.png)</span></span>
2. <span data-ttu-id="6bfcb-114">請確定您選取**傳統**做為部署模型</span><span class="sxs-lookup"><span data-stu-id="6bfcb-114">Ensure that you select the deployment model as **Classic**</span></span> </br><span data-ttu-id="6bfcb-115">
  ![Marketplace_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image-classic.png)</span><span class="sxs-lookup"><span data-stu-id="6bfcb-115">
![Marketplace_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image-classic.png)</span></span>
3. <span data-ttu-id="6bfcb-116">在 [建立虛擬機器精靈] > [基本設定] 中，請確定您選取要容錯回復虛擬機器的訂用帳戶和位置。</span><span class="sxs-lookup"><span data-stu-id="6bfcb-116">In the Create virtual machine wizard > Basic Settings, ensure you select the Subscription and Location to where you failed over the virtual machines.</span></span></br><span data-ttu-id="6bfcb-117">
  ![create_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-basic-info.png)</span><span class="sxs-lookup"><span data-stu-id="6bfcb-117">
![create_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-basic-info.png)</span></span>
4. <span data-ttu-id="6bfcb-118">請確認虛擬機器已連線到容錯回復虛擬機器連線的 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="6bfcb-118">Ensure that the virtual machine is connected to the Azure Virtual Network to which the failed over virtual machine is connected.</span></span></br><span data-ttu-id="6bfcb-119">
  ![create_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-settings.png)</span><span class="sxs-lookup"><span data-stu-id="6bfcb-119">
![create_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-settings.png)</span></span>
5. <span data-ttu-id="6bfcb-120">一旦佈建處理伺服器虛擬機器，您需要登入並向組態伺服器註冊它。</span><span class="sxs-lookup"><span data-stu-id="6bfcb-120">Once the Process Server virtual machine is provisioned, you need to log in and register it with the Configuration Server.</span></span>

> [!NOTE]
> <span data-ttu-id="6bfcb-121">為了能夠使用此處理伺服器進行容錯回復，您必須向內部部署組態伺服器註冊它。</span><span class="sxs-lookup"><span data-stu-id="6bfcb-121">To be able to use this Process Server for failback, you need to register it with the on-premises configuration server.</span></span>

## <a name="registering-the-process-server-running-in-azure-to-a-configuration-server-running-on-premises"></a><span data-ttu-id="6bfcb-122">將處理伺服器 (在 Azure 中執行) 註冊到組態伺服器 (在內部部署上執行)</span><span class="sxs-lookup"><span data-stu-id="6bfcb-122">Registering the Process Server (running in Azure) to a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-the-process-server-to-latest-version"></a><span data-ttu-id="6bfcb-123">將處理伺服器升級到最新版本。</span><span class="sxs-lookup"><span data-stu-id="6bfcb-123">Upgrading the Process Server to latest version.</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-the-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a><span data-ttu-id="6bfcb-124">從組態伺服器 (在內部部署上執行) 取消註冊處理伺服器 (在 Azure 中執行)</span><span class="sxs-lookup"><span data-stu-id="6bfcb-124">Unregistering the Process Server (running in Azure) from a Configuration Server (running on-premises)</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
