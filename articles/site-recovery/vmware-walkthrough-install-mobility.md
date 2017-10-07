---
title: "aaaInstall hello VMware tooAzure 複寫的行動服務 |Microsoft 文件"
description: "本文說明如何 tooinstall hello VMware tooAzure 複寫 hello Azure Site Recovery 服務的行動服務代理程式。"
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
ms.openlocfilehash: d3b7bc9c4d84d13317e0b0b47adcf38e8c41d0bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-install-hello-mobility-service"></a><span data-ttu-id="ba2a4-103">步驟 10： 安裝 hello 行動服務</span><span class="sxs-lookup"><span data-stu-id="ba2a4-103">Step 10: Install hello Mobility service</span></span>


<span data-ttu-id="ba2a4-104">本文說明如何 tooconfigure 來源和目標設定複寫時 VMware 虛擬機器 tooAzure，使用內部 hello [Azure Site Recovery](site-recovery-overview.md) hello Azure 入口網站中的服務。</span><span class="sxs-lookup"><span data-stu-id="ba2a4-104">This article describes how tooconfigure source and target settings when replicating on-premises VMware virtual machines tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="ba2a4-105">hello 行動服務擷取的電腦上的資料寫入，並將它們轉送 toohello 處理序伺服器。</span><span class="sxs-lookup"><span data-stu-id="ba2a4-105">hello Mobility service captures data writes on a machine, and forwards them toohello process server.</span></span> <span data-ttu-id="ba2a4-106">它應該安裝在每部電腦上您想 tooreplicate tooAzure。</span><span class="sxs-lookup"><span data-stu-id="ba2a4-106">It should be installed on each machine that you want tooreplicate tooAzure.</span></span>

<span data-ttu-id="ba2a4-107">您可以安裝 hello 行動服務手動啟用複寫時，使用從 hello 站台復原處理序伺服器推入安裝，或是使用 System Center Configuration Manager 的工具。</span><span class="sxs-lookup"><span data-stu-id="ba2a4-107">You can install hello Mobility service manual, using a push installation from hello Site Recovery process server when replication is enabled, or use a tool System Center Configuration Manager.</span></span> <span data-ttu-id="ba2a4-108">如果您使用推入安裝，hello 服務已安裝在 hello VM 上，啟用複寫時。</span><span class="sxs-lookup"><span data-stu-id="ba2a4-108">If you use push installation, hello service is installed on hello VM when replication is enabled.</span></span>

<span data-ttu-id="ba2a4-109">在本文中，或在 hello hello 下方張貼意見或疑問[Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)。</span><span class="sxs-lookup"><span data-stu-id="ba2a4-109">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="install-manually"></a><span data-ttu-id="ba2a4-110">手動安裝</span><span class="sxs-lookup"><span data-stu-id="ba2a4-110">Install manually</span></span>

1. <span data-ttu-id="ba2a4-111">檢查 hello[必要條件](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites)進行手動安裝。</span><span class="sxs-lookup"><span data-stu-id="ba2a4-111">Check hello [prerequisites](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) for manual installation.</span></span>
2. <span data-ttu-id="ba2a4-112">請遵循[這些指示](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui)進行手動安裝使用 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="ba2a4-112">Follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) for manual installation using hello portal.</span></span>
3. <span data-ttu-id="ba2a4-113">如果您偏好 tooinstall 從 hello 命令列，請遵循[這些指示](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt)。</span><span class="sxs-lookup"><span data-stu-id="ba2a4-113">If you prefer tooinstall from hello command line, follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span></span>

## <a name="install-from-hello-process-server"></a><span data-ttu-id="ba2a4-114">從 hello 處理序伺服器安裝</span><span class="sxs-lookup"><span data-stu-id="ba2a4-114">Install from hello process server</span></span>

<span data-ttu-id="ba2a4-115">如果您想 toopush hello 行動服務安裝從 hello 處理序伺服器，當您啟用 VM 的複寫時，您需要可供 hello 處理序伺服器 tooaccess hello VM 的帳戶。</span><span class="sxs-lookup"><span data-stu-id="ba2a4-115">If you want toopush hello Mobility service installation from hello process server when you enable replication for a VM, you need an account that can be used by hello process server tooaccess hello VM.</span></span> <span data-ttu-id="ba2a4-116">hello 帳戶僅用於 hello 推入安裝。</span><span class="sxs-lookup"><span data-stu-id="ba2a4-116">hello account is only used for hello push installation.</span></span>

1. <span data-ttu-id="ba2a4-117">您應該[已建立一個帳戶](vmware-walkthrough-prepare-vmware.md)來供推入安裝使用。</span><span class="sxs-lookup"><span data-stu-id="ba2a4-117">You should have [created an account](vmware-walkthrough-prepare-vmware.md) that can be used for push installation.</span></span> <span data-ttu-id="ba2a4-118">然後，您會指定您想要讓 toouse，當您設定來源站台復原 」 部署期間的 hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ba2a4-118">You then specify hello account you want toouse when you configure source settings during Site Recovery deployment.</span></span>
2. <span data-ttu-id="ba2a4-119">然後依照[這些指示](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery)如果想要在執行 Windows 或 Linux Vm 上的 toopush hello 行動服務。</span><span class="sxs-lookup"><span data-stu-id="ba2a4-119">Then follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) if you want toopush hello Mobility service on VMs running Windows or Linux.</span></span>

## <a name="other-methods"></a><span data-ttu-id="ba2a4-120">其他方法</span><span class="sxs-lookup"><span data-stu-id="ba2a4-120">Other methods</span></span>

<span data-ttu-id="ba2a4-121">深入了解[安裝 hello 行動服務使用 Configuration Manager](site-recovery-install-mobility-service-using-sccm.md)，或使用[Azure Automation DSC](site-recovery-automate-mobility-service-install.md)。</span><span class="sxs-lookup"><span data-stu-id="ba2a4-121">Learn more about [installing hello Mobility service using Configuration Manager](site-recovery-install-mobility-service-using-sccm.md), or using [Azure Automation DSC](site-recovery-automate-mobility-service-install.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ba2a4-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ba2a4-122">Next steps</span></span>

<span data-ttu-id="ba2a4-123">跳過[步驟 11： 啟用複寫](vmware-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="ba2a4-123">Go too[Step 11: Enable replication](vmware-walkthrough-enable-replication.md)</span></span>
