---
title: "使用 Azure Site Recovery 針對實體伺服器到 Azure 的複寫設定來源和目標 | Microsoft Docs"
description: "摘要說明使用 Azure Site Recovery 服務針對將實體伺服器複寫至 Azure 儲存體設定來源和目標設定時所需的步驟"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 2e3d03bc-4e53-4590-8a01-f702d3cc9500
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: e89bbf5a2c1d71852e49da43d3106a05ebfc28a8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="step-7-set-up-the-source-and-target-for-physical-server-replication-to-azure"></a><span data-ttu-id="98f56-103">步驟 7：針對實體伺服器到 Azure 的複寫設定來源和目標</span><span class="sxs-lookup"><span data-stu-id="98f56-103">Step 7: Set up the source and target for physical server replication to Azure</span></span>

<span data-ttu-id="98f56-104">本文說明在 Azure 入口網站中使用 [Azure Site Recovery](site-recovery-overview.md) 服務將內部部署實體伺服器複寫至 Azure 時，如何設定來源和目標設定。</span><span class="sxs-lookup"><span data-stu-id="98f56-104">This article describes how to configure source and target settings when replicating on-premises physical servers to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="98f56-105">請在本文下方或 [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)上張貼意見或問題。</span><span class="sxs-lookup"><span data-stu-id="98f56-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-the-source-environment"></a><span data-ttu-id="98f56-106">設定來源環境</span><span class="sxs-lookup"><span data-stu-id="98f56-106">Set up the source environment</span></span>

<span data-ttu-id="98f56-107">設定組態伺服器、在保存庫中註冊它，然後探索機器。</span><span class="sxs-lookup"><span data-stu-id="98f56-107">Set up the configuration server, register it in the vault, and discover machines.</span></span>

1. <span data-ttu-id="98f56-108">按一下 [Site Recovery] > [步驟 1: 準備基礎結構] > [來源]。</span><span class="sxs-lookup"><span data-stu-id="98f56-108">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Source**.</span></span>
2. <span data-ttu-id="98f56-109">如果您沒有設定伺服器，請按一下 [+設定伺服器]。</span><span class="sxs-lookup"><span data-stu-id="98f56-109">If you don’t have a configuration server, click **+Configuration server**.</span></span>
3. <span data-ttu-id="98f56-110">在 [新增伺服器] 中，檢查 [設定伺服器] 是否出現在 [伺服器類型] 中。</span><span class="sxs-lookup"><span data-stu-id="98f56-110">In **Add Server**, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="98f56-111">下載 Site Recovery 統一安裝的安裝檔案。</span><span class="sxs-lookup"><span data-stu-id="98f56-111">Download the Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="98f56-112">下載保存庫註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="98f56-112">Download the vault registration key.</span></span> <span data-ttu-id="98f56-113">您會在執行統一安裝時用到此金鑰。</span><span class="sxs-lookup"><span data-stu-id="98f56-113">You need this when you run Unified Setup.</span></span> <span data-ttu-id="98f56-114">該金鑰在產生後會維持 5 天有效。</span><span class="sxs-lookup"><span data-stu-id="98f56-114">The key is valid for five days after you generate it.</span></span>

   ![設定來源](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-the-configuration-server-in-the-vault"></a><span data-ttu-id="98f56-116">在保存庫中註冊設定伺服器</span><span class="sxs-lookup"><span data-stu-id="98f56-116">Register the configuration server in the vault</span></span>

<span data-ttu-id="98f56-117">開始之前請先執行下列作業，然後執行統一安裝以安裝組態伺服器、處理序伺服器與主要目標伺服器。</span><span class="sxs-lookup"><span data-stu-id="98f56-117">Do the following before you start, then run Unified Setup to install the configuration server, the process server, and the master target server.</span></span> <span data-ttu-id="98f56-118">影片說明如何針對 VMware VM 到 Azure 的複寫設定元件。</span><span class="sxs-lookup"><span data-stu-id="98f56-118">The video describes setting up the components for VMware VM to Azure replication.</span></span> <span data-ttu-id="98f56-119">不過，相同程序也適用於實體伺服器到 Azure 的複寫。</span><span class="sxs-lookup"><span data-stu-id="98f56-119">However, the same process is valid for physical server to Azure replication.</span></span>

- <span data-ttu-id="98f56-120">在組態伺服器 VM 上，確定系統時鐘與[時間伺服器](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service)同步。</span><span class="sxs-lookup"><span data-stu-id="98f56-120">On the configuration server VM, make sure that the system clock is synchronized with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span></span> <span data-ttu-id="98f56-121">應該相符。</span><span class="sxs-lookup"><span data-stu-id="98f56-121">It should match.</span></span> <span data-ttu-id="98f56-122">如果快慢誤差 15 分鐘，安裝可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="98f56-122">If it's 15 minutes in front or behind, setup might fail.</span></span>
- <span data-ttu-id="98f56-123">在組態伺服器機器上，以本機系統管理員身分執行安裝程式。</span><span class="sxs-lookup"><span data-stu-id="98f56-123">Run setup as a Local Administrator on the configuration server machine.</span></span>
- <span data-ttu-id="98f56-124">確定 VM 上已啟用 TLS 1.0</span><span class="sxs-lookup"><span data-stu-id="98f56-124">Make sure TLS 1.0 is enabled on the VM.</span></span>


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="98f56-125">您也可以[從命令列](http://aka.ms/installconfigsrv)安裝組態伺服器。</span><span class="sxs-lookup"><span data-stu-id="98f56-125">The configuration server can also be installed [from the command line](http://aka.ms/installconfigsrv).</span></span>




## <a name="set-up-the-target-environment"></a><span data-ttu-id="98f56-126">設定目標環境</span><span class="sxs-lookup"><span data-stu-id="98f56-126">Set up the target environment</span></span>

<span data-ttu-id="98f56-127">設定目標環境之前，請確定您已備妥 Azure 儲存體帳戶和虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="98f56-127">Before you set up the target environment, make sure you have an Azure storage account and virtual network set up.</span></span>

1. <span data-ttu-id="98f56-128">按一下 [準備基礎結構] > [目標]，然後選取您要使用的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="98f56-128">Click **Prepare infrastructure** > **Target**, and select the Azure subscription you want to use.</span></span>
2. <span data-ttu-id="98f56-129">指定目標部署模型是以 Resource Manager 為基礎或傳統。</span><span class="sxs-lookup"><span data-stu-id="98f56-129">Specify whether your target deployment model is Resource Manager-based, or classic.</span></span>
3. <span data-ttu-id="98f56-130">Site Recovery 會檢查您是否有一或多個相容的 Azure 儲存體帳戶和網路。</span><span class="sxs-lookup"><span data-stu-id="98f56-130">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

   ![目標](./media/physical-walkthrough-source-target/gs-target.png)

4. <span data-ttu-id="98f56-132">如果您尚未建立儲存體帳戶或網路，請按一下 [+儲存體帳戶] 或[+網路]，以建立 Resource Manager 帳戶或網路內嵌。</span><span class="sxs-lookup"><span data-stu-id="98f56-132">If you haven't created a storage account or network, click **+Storage account** or **+Network**, to create a Resource Manager account or network inline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98f56-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="98f56-133">Next steps</span></span>

<span data-ttu-id="98f56-134">移至[步驟 8：設定複寫原則](physical-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="98f56-134">Go to [Step 8: Set up a replication policy](physical-walkthrough-replication.md)</span></span>
