---
title: "針對 VMware 到 Azure 的複寫安裝行動服務 | Microsoft Docs"
description: "本文說明如何使用 Azure Site Recovery 服務，針對 VMware 到 Azure 的複寫安裝行動服務代理程式。"
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
ms.openlocfilehash: bc520bd2ea54208889861a7a3b275e3008a05d53
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="step-10-install-the-mobility-service"></a><span data-ttu-id="e2387-103">步驟 10：安裝行動服務</span><span class="sxs-lookup"><span data-stu-id="e2387-103">Step 10: Install the Mobility service</span></span>


<span data-ttu-id="e2387-104">本文說明在 Azure 入口網站中使用 [Azure Site Recovery](site-recovery-overview.md) 服務將內部部署 VMware 虛擬機器複寫至 Azure 時，如何設定來源和目標設定。</span><span class="sxs-lookup"><span data-stu-id="e2387-104">This article describes how to configure source and target settings when replicating on-premises VMware virtual machines to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="e2387-105">行動服務會擷取機器上的資料寫入，然後將它們轉送到處理伺服器。</span><span class="sxs-lookup"><span data-stu-id="e2387-105">The Mobility service captures data writes on a machine, and forwards them to the process server.</span></span> <span data-ttu-id="e2387-106">此服務應該安裝在您想要複寫至 Azure 的每部機器上。</span><span class="sxs-lookup"><span data-stu-id="e2387-106">It should be installed on each machine that you want to replicate to Azure.</span></span>

<span data-ttu-id="e2387-107">您可以透過手動方式、使用來自 Site Recovery 處理伺服器的推入安裝 (當啟用複寫時)，或使用 System Center Configuration Manager 工具，來安裝行動服務。</span><span class="sxs-lookup"><span data-stu-id="e2387-107">You can install the Mobility service manual, using a push installation from the Site Recovery process server when replication is enabled, or use a tool System Center Configuration Manager.</span></span> <span data-ttu-id="e2387-108">如果您使用推入安裝，則在啟用複寫時，服務就會安裝在 VM 上。</span><span class="sxs-lookup"><span data-stu-id="e2387-108">If you use push installation, the service is installed on the VM when replication is enabled.</span></span>

<span data-ttu-id="e2387-109">請在本文下方或 [Azure 復原服務論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)上張貼意見或問題。</span><span class="sxs-lookup"><span data-stu-id="e2387-109">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="install-manually"></a><span data-ttu-id="e2387-110">手動安裝</span><span class="sxs-lookup"><span data-stu-id="e2387-110">Install manually</span></span>

1. <span data-ttu-id="e2387-111">查看[必要條件](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites)來進行手動安裝。</span><span class="sxs-lookup"><span data-stu-id="e2387-111">Check the [prerequisites](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) for manual installation.</span></span>
2. <span data-ttu-id="e2387-112">依照[這些指示](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui)來使用入口網站進行手動安裝。</span><span class="sxs-lookup"><span data-stu-id="e2387-112">Follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) for manual installation using the portal.</span></span>
3. <span data-ttu-id="e2387-113">如果您偏好從命令列進行安裝，請依照[這些指示](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt)操作。</span><span class="sxs-lookup"><span data-stu-id="e2387-113">If you prefer to install from the command line, follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span></span>

## <a name="install-from-the-process-server"></a><span data-ttu-id="e2387-114">從處理伺服器安裝</span><span class="sxs-lookup"><span data-stu-id="e2387-114">Install from the process server</span></span>

<span data-ttu-id="e2387-115">如果您想要在為 VM 啟用複寫時，從處理伺服器推送行動服務安裝，則需要有一個可供處理伺服器用來存取該 VM 的帳戶。</span><span class="sxs-lookup"><span data-stu-id="e2387-115">If you want to push the Mobility service installation from the process server when you enable replication for a VM, you need an account that can be used by the process server to access the VM.</span></span> <span data-ttu-id="e2387-116">此帳戶僅用於推入安裝。</span><span class="sxs-lookup"><span data-stu-id="e2387-116">The account is only used for the push installation.</span></span>

1. <span data-ttu-id="e2387-117">您應該[已建立一個帳戶](vmware-walkthrough-prepare-vmware.md)來供推入安裝使用。</span><span class="sxs-lookup"><span data-stu-id="e2387-117">You should have [created an account](vmware-walkthrough-prepare-vmware.md) that can be used for push installation.</span></span> <span data-ttu-id="e2387-118">接著，您可以指定進行 Site Recovery 部署期間，在設定來源設定時要使用的帳戶。</span><span class="sxs-lookup"><span data-stu-id="e2387-118">You then specify the account you want to use when you configure source settings during Site Recovery deployment.</span></span>
2. <span data-ttu-id="e2387-119">接著，如果您想要在執行 Windows 或 Linux 的 VM 上推送行動服務，請依照[這些指示](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery)操作。</span><span class="sxs-lookup"><span data-stu-id="e2387-119">Then follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) if you want to push the Mobility service on VMs running Windows or Linux.</span></span>

## <a name="other-methods"></a><span data-ttu-id="e2387-120">其他方法</span><span class="sxs-lookup"><span data-stu-id="e2387-120">Other methods</span></span>

<span data-ttu-id="e2387-121">了解如何[使用 Configuration Manager](site-recovery-install-mobility-service-using-sccm.md) 或 [Azure Automation DSC](site-recovery-automate-mobility-service-install.md) 來安裝行動服務。</span><span class="sxs-lookup"><span data-stu-id="e2387-121">Learn more about [installing the Mobility service using Configuration Manager](site-recovery-install-mobility-service-using-sccm.md), or using [Azure Automation DSC](site-recovery-automate-mobility-service-install.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2387-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e2387-122">Next steps</span></span>

<span data-ttu-id="e2387-123">移至[步驟 11：啟用複寫](vmware-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="e2387-123">Go to [Step 11: Enable replication](vmware-walkthrough-enable-replication.md)</span></span>
