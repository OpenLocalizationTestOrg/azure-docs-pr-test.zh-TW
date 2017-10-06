---
title: "設定 hello 來源環境 (實體伺服器 tooAzure) |Microsoft 文件"
description: "本文說明如何註冊您複寫至 Azure 中執行 Windows 或 Linux 實體伺服器的內部部署環境 toostart tooset。"
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
ms.openlocfilehash: d4702265bf36910015685d2bba99d6e577531bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-source-environment-physical-server-tooazure"></a><span data-ttu-id="ff40d-103">設定 hello 來源環境 (實體伺服器 tooAzure)</span><span class="sxs-lookup"><span data-stu-id="ff40d-103">Set up hello source environment (physical server tooAzure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ff40d-104">VMware tooAzure</span><span class="sxs-lookup"><span data-stu-id="ff40d-104">VMware tooAzure</span></span>](./site-recovery-set-up-vmware-to-azure.md)
> * [<span data-ttu-id="ff40d-105">實體 tooAzure</span><span class="sxs-lookup"><span data-stu-id="ff40d-105">Physical tooAzure</span></span>](./site-recovery-set-up-physical-to-azure.md)

<span data-ttu-id="ff40d-106">本文說明如何註冊您複寫至 Azure 中執行 Windows 或 Linux 實體伺服器的內部部署環境 toostart tooset。</span><span class="sxs-lookup"><span data-stu-id="ff40d-106">This article describes how tooset up your on-premises environment toostart replicating physical servers running Windows or Linux into Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff40d-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="ff40d-107">Prerequisites</span></span>

<span data-ttu-id="ff40d-108">hello 文章假設您已經：</span><span class="sxs-lookup"><span data-stu-id="ff40d-108">hello article assumes that you already have:</span></span>
1. <span data-ttu-id="ff40d-109">復原服務保存庫中 hello [Azure 入口網站](http://portal.azure.com "Azure 入口網站")。</span><span class="sxs-lookup"><span data-stu-id="ff40d-109">A Recovery Services vault in hello [Azure portal](http://portal.azure.com "Azure portal").</span></span>
3. <span data-ttu-id="ff40d-110">哪些 tooinstall hello 組態伺服器上的實體電腦。</span><span class="sxs-lookup"><span data-stu-id="ff40d-110">A physical computer on which tooinstall hello configuration server.</span></span>

### <a name="configuration-server-minimum-requirements"></a><span data-ttu-id="ff40d-111">組態伺服器最低需求</span><span class="sxs-lookup"><span data-stu-id="ff40d-111">Configuration server minimum requirements</span></span>
<span data-ttu-id="ff40d-112">hello 下表列出 hello 最低硬體、 軟體和組態伺服器的網路需求。</span><span class="sxs-lookup"><span data-stu-id="ff40d-112">hello following table lists hello minimum hardware, software, and network requirements for a configuration server.</span></span>
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> <span data-ttu-id="ff40d-113">Hello 組態伺服器不支援 HTTPS 為基礎的 proxy 伺服器。</span><span class="sxs-lookup"><span data-stu-id="ff40d-113">HTTPS-based proxy servers are not supported by hello configuration server.</span></span>

## <a name="choose-your-protection-goals"></a><span data-ttu-id="ff40d-114">選擇您的保護目標</span><span class="sxs-lookup"><span data-stu-id="ff40d-114">Choose your protection goals</span></span>

1. <span data-ttu-id="ff40d-115">在 hello Azure 入口網站，移 toohello**復原服務**保存庫刀鋒視窗，然後選取您的保存庫。</span><span class="sxs-lookup"><span data-stu-id="ff40d-115">In hello Azure portal, go toohello **Recovery Services** vaults blade and select your vault.</span></span>
2. <span data-ttu-id="ff40d-116">在 hello**資源**功能表 hello 保存庫中，按一下**入門** > **Site Recovery** > **步驟 1： 準備基礎結構** > **保護目標**。</span><span class="sxs-lookup"><span data-stu-id="ff40d-116">In hello **Resource** menu of hello vault, click **Getting Started** > **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>

    ![選擇目標](./media/site-recovery-set-up-physical-to-azure/choose-goals.png)
3. <span data-ttu-id="ff40d-118">中**保護目標**，選取**tooAzure**和**未虛擬化/其他**，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="ff40d-118">In **Protection goal**, select **tooAzure** and **Not virtualized/Other**, and then click **OK**.</span></span>

    ![選擇目標](./media/site-recovery-set-up-physical-to-azure/physical-protection-goal.PNG)

## <a name="set-up-hello-source-environment"></a><span data-ttu-id="ff40d-120">設定 hello 來源環境</span><span class="sxs-lookup"><span data-stu-id="ff40d-120">Set up hello source environment</span></span>

1. <span data-ttu-id="ff40d-121">在**準備來源**，如果您不需要設定伺服器，按一下  **+ 設定伺服器**tooadd 其中一個。</span><span class="sxs-lookup"><span data-stu-id="ff40d-121">In **Prepare source**, if you don’t have a configuration server, click **+Configuration server** tooadd one.</span></span>

  ![設定來源](./media/site-recovery-set-up-physical-to-azure/plus-config-srv.png)
2. <span data-ttu-id="ff40d-123">在 hello**新增伺服器**刀鋒視窗中，檢查**組態伺服器**會出現在**伺服器類型**。</span><span class="sxs-lookup"><span data-stu-id="ff40d-123">In hello **Add Server** blade, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="ff40d-124">下載 hello Site Recovery 整合安裝程式安裝檔案。</span><span class="sxs-lookup"><span data-stu-id="ff40d-124">Download hello Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="ff40d-125">下載 hello 保存庫註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="ff40d-125">Download hello vault registration key.</span></span> <span data-ttu-id="ff40d-126">當您執行整合安裝程式時，您會需要 hello 註冊金鑰。</span><span class="sxs-lookup"><span data-stu-id="ff40d-126">You need hello registration key when you run Unified Setup.</span></span> <span data-ttu-id="ff40d-127">hello 金鑰有效期為您產生它之後的五天。</span><span class="sxs-lookup"><span data-stu-id="ff40d-127">hello key is valid for five days after you generate it.</span></span>

    ![設定來源](./media/site-recovery-set-up-physical-to-azure/set-source2.png)
6. <span data-ttu-id="ff40d-129">在您使用當作 hello 組態伺服器 hello 機器上執行**Azure Site Recovery 整合安裝**tooinstall hello 組態伺服器、 hello 處理序伺服器和 hello 主要目標伺服器。</span><span class="sxs-lookup"><span data-stu-id="ff40d-129">On hello machine you’re using as hello configuration server, run **Azure Site Recovery Unified Setup** tooinstall hello configuration server, hello process server, and hello master target server.</span></span>

#### <a name="run-azure-site-recovery-unified-setup"></a><span data-ttu-id="ff40d-130">執行 Azure Site Recovery 統一安裝</span><span class="sxs-lookup"><span data-stu-id="ff40d-130">Run Azure Site Recovery Unified Setup</span></span>

> [!TIP]
> <span data-ttu-id="ff40d-131">組態伺服器註冊失敗，則電腦的系統時鐘 hello 時間超過五分鐘從本機時間。</span><span class="sxs-lookup"><span data-stu-id="ff40d-131">Configuration server registration fails if hello time on your computer's system clock is more than five minutes off of local time.</span></span> <span data-ttu-id="ff40d-132">同步處理您的系統時鐘與[時間伺服器](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service)開始 hello 安裝之前。</span><span class="sxs-lookup"><span data-stu-id="ff40d-132">Synchronize your system clock with a [time server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) before starting hello installation.</span></span>

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="ff40d-133">hello 組態伺服器可以透過命令列安裝。</span><span class="sxs-lookup"><span data-stu-id="ff40d-133">hello configuration server can be installed via a command line.</span></span> <span data-ttu-id="ff40d-134">如需詳細資訊，請參閱[使用命令列工具安裝組態伺服器](http://aka.ms/installconfigsrv)。</span><span class="sxs-lookup"><span data-stu-id="ff40d-134">For more information, see [Installing configuration server using command-line tools](http://aka.ms/installconfigsrv).</span></span>


## <a name="common-issues"></a><span data-ttu-id="ff40d-135">常見問題</span><span class="sxs-lookup"><span data-stu-id="ff40d-135">Common issues</span></span>

[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a><span data-ttu-id="ff40d-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ff40d-136">Next steps</span></span>

<span data-ttu-id="ff40d-137">下一個步驟是在 Azure 中[設定目標環境](./site-recovery-prepare-target-physical-to-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="ff40d-137">Next step involves [setting up your target environment](./site-recovery-prepare-target-physical-to-azure.md) in Azure.</span></span>
