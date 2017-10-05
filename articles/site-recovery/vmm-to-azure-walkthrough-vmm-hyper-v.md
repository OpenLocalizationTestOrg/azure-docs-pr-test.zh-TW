---
title: "準備 System Center VMM 以將 Hyper-V 複寫至 Azure | Microsoft Docs"
description: "描述如何準備 System Center VMM 伺服器，以使用 Azure Site Recovery 將 Hyper-V 複寫至 Azure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: afcd81ae-d192-4013-a0af-3dac45b3c7e9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: ec118ed837dbf140083b3ae1e4ecd41c81562018
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2017
---
# <a name="step-6-prepare-vmm-servers-and-hyper-v-hosts-for-hyper-v-replication-to-azure"></a><span data-ttu-id="890d9-103">步驟 6：準備 VMM 伺服器和 Hyper-V 主機以將 Hyper-V 複寫至 Azure</span><span class="sxs-lookup"><span data-stu-id="890d9-103">Step 6: Prepare VMM servers and Hyper-V hosts for Hyper-V replication to Azure</span></span>

<span data-ttu-id="890d9-104">設定好部署所需的 [Azure 元件](vmm-to-azure-walkthrough-prepare-azure.md)後，請使用本文中的指示來準備內部部署 VMM 伺服器和 Hyper-V 主機，以和 Azure Site Recovery 進行互動。</span><span class="sxs-lookup"><span data-stu-id="890d9-104">After setting up [Azure components](vmm-to-azure-walkthrough-prepare-azure.md) for the deployment, use the instructions in this article to prepare on-premises VMM servers and Hyper-V hosts to interact with Azure Site Recovery.</span></span>

<span data-ttu-id="890d9-105">閱讀本文之後，在本文下方張貼意見，或在 [Azure Recovery Services Forum (Azure 復原服務論壇)](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr) 提出技術問題。</span><span class="sxs-lookup"><span data-stu-id="890d9-105">After reading this article, post any comments at the bottom, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="prepare-vmm-servers"></a><span data-ttu-id="890d9-106">準備 VMM 伺服器</span><span class="sxs-lookup"><span data-stu-id="890d9-106">Prepare VMM servers</span></span>

- <span data-ttu-id="890d9-107">您至少需要一部符合 Site Recovery 複寫支援需求的 VMM 伺服器 (site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers)。</span><span class="sxs-lookup"><span data-stu-id="890d9-107">You need at least one VMM server that meet the support requirements for Site Recovery replication (site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers).</span></span>
- <span data-ttu-id="890d9-108">請確定您已備妥的 VMM 伺服器[網路對應](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure)。</span><span class="sxs-lookup"><span data-stu-id="890d9-108">Make sure you've prepared the VMM server for [network mapping](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span></span>
- <span data-ttu-id="890d9-109">請確定 VMM 伺服器可以存取這些 URL</span><span class="sxs-lookup"><span data-stu-id="890d9-109">Make sure that the VMM server can access these URLs</span></span>

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- <span data-ttu-id="890d9-110">如果您有以 IP 位址為基礎的防火牆規則，請確定這些規則允許對 Azure 的通訊。</span><span class="sxs-lookup"><span data-stu-id="890d9-110">If you have IP address-based firewall rules, ensure they allow communication to Azure.</span></span>
- <span data-ttu-id="890d9-111">允許 [Azure 資料中心 IP 範圍](https://www.microsoft.com/download/confirmation.aspx?id=41653)和 HTTPS (443) 連接埠。</span><span class="sxs-lookup"><span data-stu-id="890d9-111">Allow the [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and the HTTPS (443) port.</span></span>
- <span data-ttu-id="890d9-112">允許訂用帳戶的 Azure 區域和美國西部使用 IP 位址範圍 (用於存取控制和身分識別管理)。</span><span class="sxs-lookup"><span data-stu-id="890d9-112">Allow IP address ranges for the Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

<span data-ttu-id="890d9-113">在 Site Recovery 部署期間，您要在每部 VMM 伺服器上下載並安裝 Site Recovery Provider。</span><span class="sxs-lookup"><span data-stu-id="890d9-113">During Site Recovery deployment, you download the Site Recovery Provider and install it on each VMM server.</span></span> <span data-ttu-id="890d9-114">VMM 伺服器會在復原服務保存庫中註冊。</span><span class="sxs-lookup"><span data-stu-id="890d9-114">The VMM server is registered in the Recovery Services vault.</span></span>




## <a name="next-steps"></a><span data-ttu-id="890d9-115">後續步驟</span><span class="sxs-lookup"><span data-stu-id="890d9-115">Next steps</span></span>

<span data-ttu-id="890d9-116">移至[步驟 7：建立保存庫](vmm-to-azure-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="890d9-116">Go to [Step 7: Create a vault](vmm-to-azure-walkthrough-create-vault.md)</span></span>
