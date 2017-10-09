---
title: "aaaInstall hello 實體伺服器 tooAzure 複寫的行動服務 |Microsoft 文件"
description: "本文說明如何 tooinstall hello 複寫 tooAzure hello Azure Site Recovery 服務的實體伺服器上的行動服務代理程式。"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 3189fbcd-6b5b-4ffb-b5a9-e2080c37f9d9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 48fd2c0ffe67875ed446c8167c2ae7f90d3f537c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-install-hello-mobility-service"></a><span data-ttu-id="68d25-103">步驟 9： 安裝 hello 行動服務</span><span class="sxs-lookup"><span data-stu-id="68d25-103">Step 9: Install hello Mobility service</span></span>


<span data-ttu-id="68d25-104">本文說明如何 tooinstall hello 行動服務元件時複寫在內部部署 Windows/Linux 實體伺服器 tooAzure，使用 hello [Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中的服務。</span><span class="sxs-lookup"><span data-stu-id="68d25-104">This article describes how tooinstall hello Mobility service component when replicating on-premises Windows/Linux physical servers tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="68d25-105">hello 行動服務擷取的電腦上的資料寫入，並將它們轉送 toohello 處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="68d25-105">hello Mobility service captures data writes on a machine, and forwards them toohello process server.</span></span> <span data-ttu-id="68d25-106">它應該安裝在每部伺服器上您想 tooreplicate tooAzure。</span><span class="sxs-lookup"><span data-stu-id="68d25-106">It should be installed on each server that you want tooreplicate tooAzure.</span></span>

<span data-ttu-id="68d25-107">您可以手動安裝 hello 行動服務，或使用從 hello 推入安裝站台復原處理伺服器啟用複寫時，或使用如 System Center Configuration Manager 的工具。</span><span class="sxs-lookup"><span data-stu-id="68d25-107">You can install hello Mobility service manually, or using a push installation from hello Site Recovery process server when replication is enabled, or using a tool such as System Center Configuration Manager.</span></span> <span data-ttu-id="68d25-108">如果您使用推入安裝，hello 服務已安裝 hello 伺服器上，當您啟用複寫。</span><span class="sxs-lookup"><span data-stu-id="68d25-108">If you use push installation, hello service is installed on hello server when you enable replication.</span></span>

<span data-ttu-id="68d25-109">在本文中，或在 hello hello 下方張貼意見或疑問[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="68d25-109">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="install-manually"></a><span data-ttu-id="68d25-110">手動安裝</span><span class="sxs-lookup"><span data-stu-id="68d25-110">Install manually</span></span>

1. <span data-ttu-id="68d25-111">檢查 hello[必要條件](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites)進行手動安裝。</span><span class="sxs-lookup"><span data-stu-id="68d25-111">Check hello [prerequisites](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) for manual installation.</span></span>
2. <span data-ttu-id="68d25-112">請遵循[這些指示](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui)進行手動安裝使用 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="68d25-112">Follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) for manual installation using hello portal.</span></span>
3. <span data-ttu-id="68d25-113">如果您偏好 tooinstall 從 hello 命令列，請遵循[這些指示](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt)。</span><span class="sxs-lookup"><span data-stu-id="68d25-113">If you prefer tooinstall from hello command line, follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span></span>

## <a name="install-from-hello-process-server"></a><span data-ttu-id="68d25-114">從 hello 處理序伺服器安裝</span><span class="sxs-lookup"><span data-stu-id="68d25-114">Install from hello process server</span></span>

<span data-ttu-id="68d25-115">如果您想 toopush hello 從 hello 處理序伺服器的行動服務安裝，當您啟用機器的複寫時，您需要可供 hello 處理序伺服器 tooaccess hello 電腦帳戶。</span><span class="sxs-lookup"><span data-stu-id="68d25-115">If you want toopush hello Mobility service installation from hello process server when you enable replication for a machine, you need an account that can be used by hello process server tooaccess hello machine.</span></span> <span data-ttu-id="68d25-116">hello 帳戶僅用於 hello 推入安裝。</span><span class="sxs-lookup"><span data-stu-id="68d25-116">hello account is only used for hello push installation.</span></span>

1. <span data-ttu-id="68d25-117">如果您尚未建立帳戶，請參考下列指導方針來進行此操作：</span><span class="sxs-lookup"><span data-stu-id="68d25-117">If you haven't created an account, do so using these guidelines:</span></span>

    - <span data-ttu-id="68d25-118">您可以使用網域或本機帳戶</span><span class="sxs-lookup"><span data-stu-id="68d25-118">You can use a domain or local account</span></span>
    - <span data-ttu-id="68d25-119">對於 Windows，如果您不使用網域帳戶，您需要 toodisable hello 本機電腦上的遠端使用者存取控制。</span><span class="sxs-lookup"><span data-stu-id="68d25-119">For Windows, if you're not using a domain account, you need toodisable Remote User Access control on hello local machine.</span></span> <span data-ttu-id="68d25-120">這樣一來，在 hello 註冊下 toodo **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**，新增 hello DWORD 項目**LocalAccountTokenFilterPolicy**，值為 1。</span><span class="sxs-lookup"><span data-stu-id="68d25-120">toodo this, in hello register under **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, add hello DWORD entry **LocalAccountTokenFilterPolicy**, with a value of 1.</span></span>
    - <span data-ttu-id="68d25-121">如果您想要從 CLI Windows tooadd hello 登錄項目，輸入：</span><span class="sxs-lookup"><span data-stu-id="68d25-121">If you want tooadd hello registry entry for Windows from a CLI, type:</span></span>

        ```
        REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.
        ```

    - <span data-ttu-id="68d25-122">適用於 Linux，hello 帳戶應為 hello 來源 Linux 伺服器上的根。</span><span class="sxs-lookup"><span data-stu-id="68d25-122">For Linux, hello account should be root on hello source Linux server.</span></span>

2. <span data-ttu-id="68d25-123">然後依照[這些指示](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery)如果想要在執行 Windows 或 Linux Vm 上的 toopush hello 行動服務。</span><span class="sxs-lookup"><span data-stu-id="68d25-123">Then follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) if you want toopush hello Mobility service on VMs running Windows or Linux.</span></span>

## <a name="other-installation-methods"></a><span data-ttu-id="68d25-124">其他安裝方法</span><span class="sxs-lookup"><span data-stu-id="68d25-124">Other installation methods</span></span>

- <span data-ttu-id="68d25-125">[深入了解](site-recovery-install-mobility-service-using-sccm.md)安裝 hello 使用 Configuration Manager 的行動服務</span><span class="sxs-lookup"><span data-stu-id="68d25-125">[Learn about](site-recovery-install-mobility-service-using-sccm.md) installing hello Mobility service using Configuration Manager</span></span>
- <span data-ttu-id="68d25-126">[了解](site-recovery-automate-mobility-service-install.md)如何使用 Azure Automation DSC 來進行安裝。</span><span class="sxs-lookup"><span data-stu-id="68d25-126">[Learn about](site-recovery-automate-mobility-service-install.md) installing with Azure Automation DSC.</span></span>


## <a name="next-steps"></a><span data-ttu-id="68d25-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="68d25-127">Next steps</span></span>

<span data-ttu-id="68d25-128">跳過[步驟 10： 啟用複寫](physical-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="68d25-128">Go too[Step 10: Enable replication](physical-walkthrough-enable-replication.md)</span></span>
