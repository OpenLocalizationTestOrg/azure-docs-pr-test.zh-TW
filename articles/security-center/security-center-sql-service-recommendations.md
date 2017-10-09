---
title: "aaaProtecting Azure SQL 服務與 Azure 資訊安全中心中的資料 |Microsoft 文件"
description: "本文件說明「Azure 資訊安全中心」中的建議，這些建議可協助您保護您的資料和 Azure SQL 服務，以及遵守安全性原則。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: bcae6987-05d0-4208-bca8-6a6ce7c9a1e3
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/03/2017
ms.author: terrylan
ms.openlocfilehash: 75d782d3c2418f9645139e4cd6ecb7765c488f91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-azure-sql-service-and-data-in-azure-security-center"></a><span data-ttu-id="0cbd5-103">保護 Azure 資訊安全中心內的 Azure SQL 服務和資料</span><span class="sxs-lookup"><span data-stu-id="0cbd5-103">Protecting Azure SQL service and data in Azure Security Center</span></span>
<span data-ttu-id="0cbd5-104">Azure 資訊安全中心會分析您的 Azure 資源 hello 安全性狀態。</span><span class="sxs-lookup"><span data-stu-id="0cbd5-104">Azure Security Center analyzes hello security state of your Azure resources.</span></span> <span data-ttu-id="0cbd5-105">當資訊安全中心識別潛在的安全性漏洞時，它會建立可引導您完成設定所需的 hello 控制項的 hello 程序的建議。</span><span class="sxs-lookup"><span data-stu-id="0cbd5-105">When Security Center identifies potential security vulnerabilities, it creates recommendations that guide you through hello process of configuring hello needed controls.</span></span>  <span data-ttu-id="0cbd5-106">適用於建議 tooAzure 資源類型： SQL 和資料，以及應用程式網路的虛擬機器 (Vm)。</span><span class="sxs-lookup"><span data-stu-id="0cbd5-106">Recommendations apply tooAzure resource types: virtual machines (VMs), networking, SQL and data, and applications.</span></span>

<span data-ttu-id="0cbd5-107">本文適用 tooAzure SQL 服務和資料的建議。</span><span class="sxs-lookup"><span data-stu-id="0cbd5-107">This article addresses recommendations that apply tooAzure SQL service and data.</span></span> <span data-ttu-id="0cbd5-108">這些建議是以下列主題為中心：為 Azure SQL 伺服器和資料庫啟用稽核、為 SQL 資料庫啟用加密，以及啟用 Azure 儲存體帳戶加密。</span><span class="sxs-lookup"><span data-stu-id="0cbd5-108">Recommendations center around enabling auditing for Azure SQL servers and databases, enabling encryption for SQL databases, and enabling encryption of your Azure storage account.</span></span>  <span data-ttu-id="0cbd5-109">使用 hello 表當做參考 toohelp 您了解 hello 可用 SQL 服務與資料的建議，每個用途如果您將其套用。</span><span class="sxs-lookup"><span data-stu-id="0cbd5-109">Use hello table below as a reference toohelp you understand hello available SQL service and data recommendations and what each one does if you apply it.</span></span>

## <a name="available-sql-service-and-data-recommendations"></a><span data-ttu-id="0cbd5-110">可用的 SQL 服務和資料建議</span><span class="sxs-lookup"><span data-stu-id="0cbd5-110">Available SQL service and data recommendations</span></span>
| <span data-ttu-id="0cbd5-111">建議</span><span class="sxs-lookup"><span data-stu-id="0cbd5-111">Recommendation</span></span> | <span data-ttu-id="0cbd5-112">說明</span><span class="sxs-lookup"><span data-stu-id="0cbd5-112">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="0cbd5-113">在 SQL Server 上啟用稽核與威脅偵測</span><span class="sxs-lookup"><span data-stu-id="0cbd5-113">Enable auditing and threat detection on SQL servers</span></span>](security-center-enable-auditing-on-sql-servers.md) |<span data-ttu-id="0cbd5-114">建議您針對 Azure SQL Server 開啟稽核與威脅偵測 (僅適用於 Azure SQL 服務，不包括在您虛擬機器上執行的 SQL)。</span><span class="sxs-lookup"><span data-stu-id="0cbd5-114">Recommends that you turn on auditing and threat detection for Azure SQL servers (Azure SQL service only; doesn't include SQL running on your virtual machines).</span></span> |
| [<span data-ttu-id="0cbd5-115">在 SQL 資料庫上啟用稽核與威脅偵測</span><span class="sxs-lookup"><span data-stu-id="0cbd5-115">Enable auditing and threat detection on SQL databases</span></span>](security-center-enable-auditing-on-sql-databases.md) |<span data-ttu-id="0cbd5-116">建議您針對 Azure SQL Database 開啟稽核與威脅偵測 (僅適用於 Azure SQL 服務，不包括在您虛擬機器上執行的 SQL)。</span><span class="sxs-lookup"><span data-stu-id="0cbd5-116">Recommends that you turn on auditing and threat detection for Azure SQL databases (Azure SQL service only; doesn't include SQL running on your virtual machines).</span></span> |
| [<span data-ttu-id="0cbd5-117">在 SQL 資料庫上啟用透明資料加密</span><span class="sxs-lookup"><span data-stu-id="0cbd5-117">Enable Transparent Data Encryption on SQL databases</span></span>](security-center-enable-transparent-data-encryption.md) |<span data-ttu-id="0cbd5-118">建議您針對 SQL 資料庫啟用加密 (僅適用於 Azure SQL 服務)。</span><span class="sxs-lookup"><span data-stu-id="0cbd5-118">Recommends that you enable encryption for SQL databases (Azure SQL service only).</span></span> |

## <a name="see-also"></a><span data-ttu-id="0cbd5-119">另請參閱</span><span class="sxs-lookup"><span data-stu-id="0cbd5-119">See also</span></span>
<span data-ttu-id="0cbd5-120">toolearn 深入了解建議，套用 tooother Azure 資源類型，請參閱 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="0cbd5-120">toolearn more about recommendations that apply tooother Azure resource types, see hello following:</span></span>

* [<span data-ttu-id="0cbd5-121">保護 Azure 資訊安全中心內的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="0cbd5-121">Protecting your virtual machines in Azure Security Center</span></span>](security-center-virtual-machine-recommendations.md)
* [<span data-ttu-id="0cbd5-122">保護 Azure 資訊安全中心內的應用程式</span><span class="sxs-lookup"><span data-stu-id="0cbd5-122">Protecting your applications in Azure Security Center</span></span>](security-center-application-recommendations.md)
* [<span data-ttu-id="0cbd5-123">保護 Azure 資訊安全中心內的網路</span><span class="sxs-lookup"><span data-stu-id="0cbd5-123">Protecting your network in Azure Security Center</span></span>](security-center-network-recommendations.md)

<span data-ttu-id="0cbd5-124">toolearn 有關資訊安全中心的詳細資訊，請參閱 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="0cbd5-124">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="0cbd5-125">[在 Azure 資訊安全中心中設定安全性原則](security-center-policies.md)-了解如何 tooconfigure 您的 Azure 訂用帳戶和資源群組的安全性原則。</span><span class="sxs-lookup"><span data-stu-id="0cbd5-125">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="0cbd5-126">[在 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md) -了解如何 toomanage 和回應 toosecurity 警示。</span><span class="sxs-lookup"><span data-stu-id="0cbd5-126">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="0cbd5-127">[Azure 資訊安全中心常見問題集](security-center-faq.md)-尋找使用 hello 服務相關的常見問題集。</span><span class="sxs-lookup"><span data-stu-id="0cbd5-127">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
