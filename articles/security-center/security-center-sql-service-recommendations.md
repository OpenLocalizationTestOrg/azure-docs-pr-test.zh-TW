---
title: "保護 Azure 資訊安全中心內的  Azure SQL 服務和資料 | Microsoft Docs"
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
ms.openlocfilehash: 0c3a11e9a86767641533b16de1b96b4c59bfdf51
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="protecting-azure-sql-service-and-data-in-azure-security-center"></a><span data-ttu-id="8be77-103">保護 Azure 資訊安全中心內的 Azure SQL 服務和資料</span><span class="sxs-lookup"><span data-stu-id="8be77-103">Protecting Azure SQL service and data in Azure Security Center</span></span>
<span data-ttu-id="8be77-104">「Azure 資訊安全中心」會分析 Azure 資源的安全性狀態。</span><span class="sxs-lookup"><span data-stu-id="8be77-104">Azure Security Center analyzes the security state of your Azure resources.</span></span> <span data-ttu-id="8be77-105">當資訊安全中心發現潛在的安全性弱點時，它會建立可引導您完成所需控制之設定程序的建議。</span><span class="sxs-lookup"><span data-stu-id="8be77-105">When Security Center identifies potential security vulnerabilities, it creates recommendations that guide you through the process of configuring the needed controls.</span></span>  <span data-ttu-id="8be77-106">這些建議適用於下列 Azure 資源類型︰虛擬機器 (VM)、網路、SQL 和資料，以及應用程式。</span><span class="sxs-lookup"><span data-stu-id="8be77-106">Recommendations apply to Azure resource types: virtual machines (VMs), networking, SQL and data, and applications.</span></span>

<span data-ttu-id="8be77-107">本文說明適用於 Azure SQL 服務和資料的建議。</span><span class="sxs-lookup"><span data-stu-id="8be77-107">This article addresses recommendations that apply to Azure SQL service and data.</span></span> <span data-ttu-id="8be77-108">這些建議是以下列主題為中心：為 Azure SQL 伺服器和資料庫啟用稽核、為 SQL 資料庫啟用加密，以及啟用 Azure 儲存體帳戶加密。</span><span class="sxs-lookup"><span data-stu-id="8be77-108">Recommendations center around enabling auditing for Azure SQL servers and databases, enabling encryption for SQL databases, and enabling encryption of your Azure storage account.</span></span>  <span data-ttu-id="8be77-109">請使用下表作為參考來協助您了解可用的 SQL 服務和資料建議，以及每一項建議在套用後將產生的作用。</span><span class="sxs-lookup"><span data-stu-id="8be77-109">Use the table below as a reference to help you understand the available SQL service and data recommendations and what each one does if you apply it.</span></span>

## <a name="available-sql-service-and-data-recommendations"></a><span data-ttu-id="8be77-110">可用的 SQL 服務和資料建議</span><span class="sxs-lookup"><span data-stu-id="8be77-110">Available SQL service and data recommendations</span></span>
| <span data-ttu-id="8be77-111">建議</span><span class="sxs-lookup"><span data-stu-id="8be77-111">Recommendation</span></span> | <span data-ttu-id="8be77-112">說明</span><span class="sxs-lookup"><span data-stu-id="8be77-112">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="8be77-113">在 SQL Server 上啟用稽核與威脅偵測</span><span class="sxs-lookup"><span data-stu-id="8be77-113">Enable auditing and threat detection on SQL servers</span></span>](security-center-enable-auditing-on-sql-servers.md) |<span data-ttu-id="8be77-114">建議您針對 Azure SQL Server 開啟稽核與威脅偵測 (僅適用於 Azure SQL 服務，不包括在您虛擬機器上執行的 SQL)。</span><span class="sxs-lookup"><span data-stu-id="8be77-114">Recommends that you turn on auditing and threat detection for Azure SQL servers (Azure SQL service only; doesn't include SQL running on your virtual machines).</span></span> |
| [<span data-ttu-id="8be77-115">在 SQL 資料庫上啟用稽核與威脅偵測</span><span class="sxs-lookup"><span data-stu-id="8be77-115">Enable auditing and threat detection on SQL databases</span></span>](security-center-enable-auditing-on-sql-databases.md) |<span data-ttu-id="8be77-116">建議您針對 Azure SQL Database 開啟稽核與威脅偵測 (僅適用於 Azure SQL 服務，不包括在您虛擬機器上執行的 SQL)。</span><span class="sxs-lookup"><span data-stu-id="8be77-116">Recommends that you turn on auditing and threat detection for Azure SQL databases (Azure SQL service only; doesn't include SQL running on your virtual machines).</span></span> |
| [<span data-ttu-id="8be77-117">在 SQL 資料庫上啟用透明資料加密</span><span class="sxs-lookup"><span data-stu-id="8be77-117">Enable Transparent Data Encryption on SQL databases</span></span>](security-center-enable-transparent-data-encryption.md) |<span data-ttu-id="8be77-118">建議您針對 SQL 資料庫啟用加密 (僅適用於 Azure SQL 服務)。</span><span class="sxs-lookup"><span data-stu-id="8be77-118">Recommends that you enable encryption for SQL databases (Azure SQL service only).</span></span> |

## <a name="see-also"></a><span data-ttu-id="8be77-119">另請參閱</span><span class="sxs-lookup"><span data-stu-id="8be77-119">See also</span></span>
<span data-ttu-id="8be77-120">若要深入了解適用於其他 Azure 資源類型的建議，請參閱下列文章︰</span><span class="sxs-lookup"><span data-stu-id="8be77-120">To learn more about recommendations that apply to other Azure resource types, see the following:</span></span>

* [<span data-ttu-id="8be77-121">保護 Azure 資訊安全中心內的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="8be77-121">Protecting your virtual machines in Azure Security Center</span></span>](security-center-virtual-machine-recommendations.md)
* [<span data-ttu-id="8be77-122">保護 Azure 資訊安全中心內的應用程式</span><span class="sxs-lookup"><span data-stu-id="8be77-122">Protecting your applications in Azure Security Center</span></span>](security-center-application-recommendations.md)
* [<span data-ttu-id="8be77-123">保護 Azure 資訊安全中心內的網路</span><span class="sxs-lookup"><span data-stu-id="8be77-123">Protecting your network in Azure Security Center</span></span>](security-center-network-recommendations.md)

<span data-ttu-id="8be77-124">如要深入了解資訊安全中心，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="8be77-124">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="8be77-125">[在 Azure 資訊安全中心設定安全性原則](security-center-policies.md) -- 了解如何為您的 Azure 訂用帳戶及資源群組設定安全性原則。</span><span class="sxs-lookup"><span data-stu-id="8be77-125">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="8be77-126">[管理與回應 Azure 資訊安全中心的安全性警示](security-center-managing-and-responding-alerts.md) -- 了解如何管理與回應安全性警示。</span><span class="sxs-lookup"><span data-stu-id="8be77-126">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="8be77-127">[Azure 資訊安全中心常見問題集](security-center-faq.md) -- 尋找有關使用服務的常見問題。</span><span class="sxs-lookup"><span data-stu-id="8be77-127">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
