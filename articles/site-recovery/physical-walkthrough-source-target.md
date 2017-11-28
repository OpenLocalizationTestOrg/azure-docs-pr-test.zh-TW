---
title: "hello 來源和目標與 Azure Site Recovery 的實體伺服器複寫 tooAzure aaaSet |Microsoft 文件"
description: "摘要說明 hello 步驟 tooset 以 hello Azure Site Recovery 服務的實體伺服器 tooAzure 存放裝置複寫的來源和目標設定"
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
ms.openlocfilehash: e75ef23174d77509bf54380eba8f251a7337a45f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-hello-source-and-target-for-physical-server-replication-tooazure"></a><span data-ttu-id="23a23-103">步驟 7： 設定 hello 來源和目標的實體伺服器複寫 tooAzure</span><span class="sxs-lookup"><span data-stu-id="23a23-103">Step 7: Set up hello source and target for physical server replication tooAzure</span></span>

<span data-ttu-id="23a23-104">本文說明如何 tooconfigure 來源和目標設定複寫時使用在內部實體伺服器 tooAzure hello [Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中的服務。</span><span class="sxs-lookup"><span data-stu-id="23a23-104">This article describes how tooconfigure source and target settings when replicating on-premises physical servers tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="23a23-105">在本文中，或在 hello hello 下方張貼意見或疑問[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="23a23-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-hello-source-environment"></a><span data-ttu-id="23a23-106">設定 hello 來源環境</span><span class="sxs-lookup"><span data-stu-id="23a23-106">Set up hello source environment</span></span>

<span data-ttu-id="23a23-107">設定 hello 組態伺服器、 註冊在保存庫 hello 和探索電腦。</span><span class="sxs-lookup"><span data-stu-id="23a23-107">Set up hello configuration server, register it in hello vault, and discover machines.</span></span>

1. <span data-ttu-id="23a23-108">按一下 [Site Recovery] > [步驟 1: 準備基礎結構] > [來源]。</span><span class="sxs-lookup"><span data-stu-id="23a23-108">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Source**.</span></span>
2. <span data-ttu-id="23a23-109">如果您沒有設定伺服器，請按一下 [+設定伺服器]。</span><span class="sxs-lookup"><span data-stu-id="23a23-109">If you don’t have a configuration server, click **+Configuration server**.</span></span>
3. <span data-ttu-id="23a23-110">在 [新增伺服器] 中，檢查 [設定伺服器] 是否出現在 [伺服器類型] 中。</span><span class="sxs-lookup"><span data-stu-id="23a23-110">In **Add Server**, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="23a23-111">下載 hello Site Recovery 整合安裝程式安裝檔案。</span><span class="sxs-lookup"><span data-stu-id="23a23-111">Download hello Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="23a23-112">下載 hello 保存庫註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="23a23-112">Download hello vault registration key.</span></span> <span data-ttu-id="23a23-113">您會在執行統一安裝時用到此金鑰。</span><span class="sxs-lookup"><span data-stu-id="23a23-113">You need this when you run Unified Setup.</span></span> <span data-ttu-id="23a23-114">hello 金鑰有效期為您產生它之後的五天。</span><span class="sxs-lookup"><span data-stu-id="23a23-114">hello key is valid for five days after you generate it.</span></span>

   ![設定來源](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-hello-configuration-server-in-hello-vault"></a><span data-ttu-id="23a23-116">Hello 保存庫中註冊伺服器 hello 組態</span><span class="sxs-lookup"><span data-stu-id="23a23-116">Register hello configuration server in hello vault</span></span>

<span data-ttu-id="23a23-117">請勿 hello 下列之前啟動，然後執行整合安裝 tooinstall hello 組態伺服器、 hello 處理序伺服器，以及 hello 主要目標伺服器。</span><span class="sxs-lookup"><span data-stu-id="23a23-117">Do hello following before you start, then run Unified Setup tooinstall hello configuration server, hello process server, and hello master target server.</span></span> <span data-ttu-id="23a23-118">hello 視訊描述 hello VMware VM tooAzure 複寫元件的設定。</span><span class="sxs-lookup"><span data-stu-id="23a23-118">hello video describes setting up hello components for VMware VM tooAzure replication.</span></span> <span data-ttu-id="23a23-119">不過，hello 相同的程序僅適用於實體伺服器 tooAzure 複寫。</span><span class="sxs-lookup"><span data-stu-id="23a23-119">However, hello same process is valid for physical server tooAzure replication.</span></span>

- <span data-ttu-id="23a23-120">在 hello 組態伺服器 VM，請確定該 hello 系統時鐘與同步[時間伺服器](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service)。</span><span class="sxs-lookup"><span data-stu-id="23a23-120">On hello configuration server VM, make sure that hello system clock is synchronized with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span></span> <span data-ttu-id="23a23-121">應該相符。</span><span class="sxs-lookup"><span data-stu-id="23a23-121">It should match.</span></span> <span data-ttu-id="23a23-122">如果快慢誤差 15 分鐘，安裝可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="23a23-122">If it's 15 minutes in front or behind, setup might fail.</span></span>
- <span data-ttu-id="23a23-123">Hello 組態伺服器電腦上執行安裝程式做為本機系統管理員。</span><span class="sxs-lookup"><span data-stu-id="23a23-123">Run setup as a Local Administrator on hello configuration server machine.</span></span>
- <span data-ttu-id="23a23-124">請確定 hello VM 上啟用 TLS 1.0。</span><span class="sxs-lookup"><span data-stu-id="23a23-124">Make sure TLS 1.0 is enabled on hello VM.</span></span>


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="23a23-125">也可以安裝 hello 組態伺服器[hello 命令列從](http://aka.ms/installconfigsrv)。</span><span class="sxs-lookup"><span data-stu-id="23a23-125">hello configuration server can also be installed [from hello command line](http://aka.ms/installconfigsrv).</span></span>




## <a name="set-up-hello-target-environment"></a><span data-ttu-id="23a23-126">Hello 目標環境設定</span><span class="sxs-lookup"><span data-stu-id="23a23-126">Set up hello target environment</span></span>

<span data-ttu-id="23a23-127">您設定 hello 目標環境之前，請確定您有 Azure 儲存體帳戶和虛擬網路設定。</span><span class="sxs-lookup"><span data-stu-id="23a23-127">Before you set up hello target environment, make sure you have an Azure storage account and virtual network set up.</span></span>

1. <span data-ttu-id="23a23-128">按一下**準備基礎結構** > **目標**，並選取 hello 想 toouse 的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="23a23-128">Click **Prepare infrastructure** > **Target**, and select hello Azure subscription you want toouse.</span></span>
2. <span data-ttu-id="23a23-129">指定目標部署模型是以 Resource Manager 為基礎或傳統。</span><span class="sxs-lookup"><span data-stu-id="23a23-129">Specify whether your target deployment model is Resource Manager-based, or classic.</span></span>
3. <span data-ttu-id="23a23-130">Site Recovery 會檢查您是否有一或多個相容的 Azure 儲存體帳戶和網路。</span><span class="sxs-lookup"><span data-stu-id="23a23-130">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

   ![目標](./media/physical-walkthrough-source-target/gs-target.png)

4. <span data-ttu-id="23a23-132">如果您尚未建立儲存體帳戶或網路，按一下**+ 儲存體帳戶**或**+ 網路**，toocreate 資源管理員帳戶或網路內嵌。</span><span class="sxs-lookup"><span data-stu-id="23a23-132">If you haven't created a storage account or network, click **+Storage account** or **+Network**, toocreate a Resource Manager account or network inline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="23a23-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="23a23-133">Next steps</span></span>

<span data-ttu-id="23a23-134">跳過[步驟 8： 設定複寫原則](physical-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="23a23-134">Go too[Step 8: Set up a replication policy](physical-walkthrough-replication.md)</span></span>
