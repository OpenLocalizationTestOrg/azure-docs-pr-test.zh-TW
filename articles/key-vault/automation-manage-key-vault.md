---
title: "使用 Azure 自動化管理 Azure 金鑰保存庫 | Microsoft Docs"
description: "了解如何使用 Azure 自動化服務來管理 Azure 金鑰保存庫。"
services: Key-Vault, automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 4e780762-19b6-4ca6-b894-ebb44c538f35
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: magoedte;csand
ms.openlocfilehash: dee39662472fe54776b591977f2b1ecb39d15b00
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-key-vault-using-azure-automation"></a><span data-ttu-id="0428f-103">使用 Azure 自動化管理 Azure 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="0428f-103">Managing Azure Key Vault using Azure Automation</span></span>
<span data-ttu-id="0428f-104">本指南將為您介紹 Azure 自動化服務，以及如何使用它來簡化管理 Azure 金鑰保存庫中的金鑰和密碼。</span><span class="sxs-lookup"><span data-stu-id="0428f-104">This guide will introduce you to the Azure Automation service and how it can be used to simplify management of your keys and secrets in Azure Key Vault.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="0428f-105">什麼是 Azure 自動化？</span><span class="sxs-lookup"><span data-stu-id="0428f-105">What is Azure Automation?</span></span>
<span data-ttu-id="0428f-106">[Azure 自動化](../automation/automation-intro.md) 是一項 Azure 服務，可經由程序自動化和所要的狀態組態簡化雲端管理。</span><span class="sxs-lookup"><span data-stu-id="0428f-106">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation and desired state configuration.</span></span> <span data-ttu-id="0428f-107">使用 Azure 自動化，可以自動執行手動、重複、長時間執行及容易出錯的工作，以提高您的組織的可靠性、效率和時間價值。</span><span class="sxs-lookup"><span data-stu-id="0428f-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="0428f-108">Azure 自動化提供高度可靠、高度可用的工作流程執行引擎，可加以調整以符合您的需求。</span><span class="sxs-lookup"><span data-stu-id="0428f-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales to meet your needs.</span></span> <span data-ttu-id="0428f-109">在 Azure 自動化中，可以手動方式、由協力廠商系統或依排定的間隔開始執行程序，讓工作只發生在必要時刻。</span><span class="sxs-lookup"><span data-stu-id="0428f-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="0428f-110">將您的雲端管理工作交由「Azure 自動化」自動執行，以減少營運負擔並釋出 IT 和開發維運人力，使其專注於能夠為企業創造價值的工作上。</span><span class="sxs-lookup"><span data-stu-id="0428f-110">Reduce operational overhead and free up IT and DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-key-vault"></a><span data-ttu-id="0428f-111">Azure 自動化如何協助管理 Azure 金鑰保存庫？</span><span class="sxs-lookup"><span data-stu-id="0428f-111">How can Azure Automation help manage Azure Key Vault?</span></span>
<span data-ttu-id="0428f-112">您可以使用 [AzureRM 金鑰保存庫 Cmdlet](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) 和 [Azure 傳統金鑰保存庫 Cmdlet](https://msdn.microsoft.com/library/azure/dn868052.aspx)，在 Azure 自動化中管理金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="0428f-112">Key Vault can be managed in Azure Automation by using the [AzureRM Key Vault cmdlets](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) and [Azure Classic Key Vault cmdlets](https://msdn.microsoft.com/library/azure/dn868052.aspx).</span></span> <span data-ttu-id="0428f-113">管理傳統金鑰保存庫的 Azure 模組會自動出現在 Azure 自動化中供您使用，而且您可以將 [AzureRM-KeyVault 模組](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) 匯入 Azure 自動化，以便在服務中執行許多金鑰保存庫管理工作。</span><span class="sxs-lookup"><span data-stu-id="0428f-113">The Azure module for managing classic Key Vault is available automatically in Azure Automation, and you can import the [AzureRM-KeyVault module](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) into Azure Automation, so that you can perform many of your Key Vault management tasks within the service.</span></span> <span data-ttu-id="0428f-114">您也可以將 Azure 自動化中的這些 Cmdlet 與其他 Azure 服務的 Cmdlet 搭配，以透過 Azure 服務和協力廠商系統自動執行複雜的工作。</span><span class="sxs-lookup"><span data-stu-id="0428f-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="0428f-115">使用 Azure 金鑰保存庫 Cmdlet，您可以執行以下工作和其他工作︰</span><span class="sxs-lookup"><span data-stu-id="0428f-115">With the Azure Key Vault cmdlets you can perform these tasks among others:</span></span> 

* <span data-ttu-id="0428f-116">建立和設定金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="0428f-116">Create and configure a key vault</span></span>
* <span data-ttu-id="0428f-117">建立或匯入金鑰</span><span class="sxs-lookup"><span data-stu-id="0428f-117">Create or import a key</span></span>
* <span data-ttu-id="0428f-118">建立或更新密碼</span><span class="sxs-lookup"><span data-stu-id="0428f-118">Create or update a secret</span></span>
* <span data-ttu-id="0428f-119">更新金鑰的屬性</span><span class="sxs-lookup"><span data-stu-id="0428f-119">Update attributes of a key</span></span>
* <span data-ttu-id="0428f-120">取得金鑰或密碼</span><span class="sxs-lookup"><span data-stu-id="0428f-120">Get a key or secret</span></span>
* <span data-ttu-id="0428f-121">刪除金鑰或密碼</span><span class="sxs-lookup"><span data-stu-id="0428f-121">Delete a key or secret</span></span>

<span data-ttu-id="0428f-122">以下是使用 PowerShell 來管理金鑰保存庫的一些範例︰</span><span class="sxs-lookup"><span data-stu-id="0428f-122">Here are some examples of using PowerShell to manage Key Vault:</span></span>  

* [<span data-ttu-id="0428f-123">Azure 金鑰保存庫 - 逐步解說</span><span class="sxs-lookup"><span data-stu-id="0428f-123">Azure Key Vault - Step by Step</span></span>](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step)
* [<span data-ttu-id="0428f-124">設定 Azure 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="0428f-124">Setting Up and Configuring an Azure Key Vault</span></span>](https://www.simple-talk.com/cloud/platform-as-a-service/setting-up-and-configuring-an-azure-key-vault)

## <a name="next-steps"></a><span data-ttu-id="0428f-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0428f-125">Next steps</span></span>
<span data-ttu-id="0428f-126">了解 Azure 自動化的基本概念以及如何用它來管理 Azure 金鑰保存庫之後，請參考下列連結，以深入了解 Azure 自動化。</span><span class="sxs-lookup"><span data-stu-id="0428f-126">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure Key Vault, follow these links to learn more about Azure Automation.</span></span>

* <span data-ttu-id="0428f-127">請參閱 Azure 自動化 [快速入門教學課程](../automation/automation-first-runbook-graphical.md)。</span><span class="sxs-lookup"><span data-stu-id="0428f-127">See the Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md).</span></span>
* <span data-ttu-id="0428f-128">請參閱 [Azure 金鑰保存庫 PowerShell 指令碼](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5)。</span><span class="sxs-lookup"><span data-stu-id="0428f-128">See the [Azure Key Vault PowerShell scripts](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5).</span></span>

