---
title: "準備 Hyper-V 主機 (不含 System Center VMM) 以複寫至 Azure | Microsoft Docs"
description: "描述如何使用 Azure Site Recovery 準備 Hyper-V 主機以複寫至 Azure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 0f204e24-8d78-4076-95c5-8137d1be9c01
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: f9bcaa8e55be6e8fddaf88ebc3f18f5dbb2811e4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="step-6-prepare-hyper-v-hosts-for-replication-to-azure"></a><span data-ttu-id="d3ca0-103">步驟 6：準備 Hyper-V 主機複寫至 Azure</span><span class="sxs-lookup"><span data-stu-id="d3ca0-103">Step 6: Prepare Hyper-V hosts for replication to Azure</span></span>

<span data-ttu-id="d3ca0-104">使用本文中的指示來準備內部部署 Hyper-V 主機與 Azure Site Recovery 進行互動。</span><span class="sxs-lookup"><span data-stu-id="d3ca0-104">Use the instructions in this article to prepare on-premises Hyper-V hosts to interact with Azure Site Recovery.</span></span>

<span data-ttu-id="d3ca0-105">閱讀本文之後，在本文下方張貼意見，或在 [Azure Recovery Services Forum (Azure 復原服務論壇)](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr) 提出技術問題。</span><span class="sxs-lookup"><span data-stu-id="d3ca0-105">After reading this article, post any comments at the bottom, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="prepare-hosts"></a><span data-ttu-id="d3ca0-106">準備主機</span><span class="sxs-lookup"><span data-stu-id="d3ca0-106">Prepare hosts</span></span>

- <span data-ttu-id="d3ca0-107">確定 Hyper-V 主機符合[必要條件](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm)。</span><span class="sxs-lookup"><span data-stu-id="d3ca0-107">Make sure that the Hyper-V hosts meet the [prerequisites](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm).</span></span>
- <span data-ttu-id="d3ca0-108">請確定主機可以存取必要的 URL：</span><span class="sxs-lookup"><span data-stu-id="d3ca0-108">Make sure that the hosts can access the required URLs:</span></span>

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- <span data-ttu-id="d3ca0-109">如果您有以 IP 位址為基礎的防火牆規則，請確定這些規則允許對 Azure 的通訊。</span><span class="sxs-lookup"><span data-stu-id="d3ca0-109">If you have IP address-based firewall rules, ensure they allow communication to Azure.</span></span>
- <span data-ttu-id="d3ca0-110">允許 [Azure 資料中心 IP 範圍](https://www.microsoft.com/download/confirmation.aspx?id=41653)和 HTTPS (443) 連接埠。</span><span class="sxs-lookup"><span data-stu-id="d3ca0-110">Allow the [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and the HTTPS (443) port.</span></span>
- <span data-ttu-id="d3ca0-111">允許訂用帳戶的 Azure 區域和美國西部使用 IP 位址範圍 (用於存取控制和身分識別管理)。</span><span class="sxs-lookup"><span data-stu-id="d3ca0-111">Allow IP address ranges for the Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

<span data-ttu-id="d3ca0-112">在 Site Recovery 部署期間，您可以新增 Hyper-V 主機，當中包含您想要複寫到 Hyper-V 網站的 VM。</span><span class="sxs-lookup"><span data-stu-id="d3ca0-112">During Site Recovery deployment, you add Hyper-V hosts that contain VMs you want to replicate to a Hyper-V site.</span></span> <span data-ttu-id="d3ca0-113">Site Recovery 提供者和復原服務代理程式會安裝在每一部主機上。</span><span class="sxs-lookup"><span data-stu-id="d3ca0-113">The Site Recovery Provider, and Recovery Services agent are installed on each host.</span></span> <span data-ttu-id="d3ca0-114">Hyper-V 站台會在復原服務保存庫中註冊。</span><span class="sxs-lookup"><span data-stu-id="d3ca0-114">The Hyper-V site is registered in the Recovery Services vault.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d3ca0-115">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d3ca0-115">Next steps</span></span>

<span data-ttu-id="d3ca0-116">移至[步驟 7：建立保存庫](hyper-v-site-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="d3ca0-116">Go to [Step 7: Create a vault](hyper-v-site-walkthrough-create-vault.md)</span></span>

