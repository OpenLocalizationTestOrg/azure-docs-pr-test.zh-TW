---
title: "Azure 金鑰保存庫使用 Azure 自動化 aaaManage |Microsoft 文件"
description: "深入了解如何 hello Azure 自動化服務可以使用的 toomanage Azure 金鑰保存庫。"
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
ms.openlocfilehash: 7f46ecc1206a96e8aeb1d086285461cb5b205472
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-key-vault-using-azure-automation"></a><span data-ttu-id="f21b6-103">使用 Azure 自動化管理 Azure 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="f21b6-103">Managing Azure Key Vault using Azure Automation</span></span>
<span data-ttu-id="f21b6-104">本指南將介紹 toohello Azure 自動化服務，而且可以如何使用的 toosimplify 管理您的金鑰和 Azure 金鑰保存庫中的密碼。</span><span class="sxs-lookup"><span data-stu-id="f21b6-104">This guide will introduce you toohello Azure Automation service and how it can be used toosimplify management of your keys and secrets in Azure Key Vault.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="f21b6-105">什麼是 Azure 自動化？</span><span class="sxs-lookup"><span data-stu-id="f21b6-105">What is Azure Automation?</span></span>
<span data-ttu-id="f21b6-106">[Azure 自動化](../automation/automation-intro.md) 是一項 Azure 服務，可經由程序自動化和所要的狀態組態簡化雲端管理。</span><span class="sxs-lookup"><span data-stu-id="f21b6-106">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation and desired state configuration.</span></span> <span data-ttu-id="f21b6-107">使用 Azure 自動化，自動化的 tooincrease 可靠性、 效率與時間 toovalue 為您的組織可能會手動、 重複、 長時間執行，而且容易產生錯誤的工作。</span><span class="sxs-lookup"><span data-stu-id="f21b6-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="f21b6-108">Azure 自動化會提供您的需求調整 toomeet 的非常可靠、 高可用性的工作流程執行引擎。</span><span class="sxs-lookup"><span data-stu-id="f21b6-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales toomeet your needs.</span></span> <span data-ttu-id="f21b6-109">在 Azure 自動化中，程序可透過手動方式、經由協力廠商系統，或依照排程的間隔啟動，讓工作精準地在需要時執行。</span><span class="sxs-lookup"><span data-stu-id="f21b6-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="f21b6-110">降低操作費用並釋出 IT 和 DevOps 人員 toofocus 移動您的雲端管理工作 toobe 商務價值的工作自動執行的 Azure 自動化。</span><span class="sxs-lookup"><span data-stu-id="f21b6-110">Reduce operational overhead and free up IT and DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-key-vault"></a><span data-ttu-id="f21b6-111">Azure 自動化如何協助管理 Azure 金鑰保存庫？</span><span class="sxs-lookup"><span data-stu-id="f21b6-111">How can Azure Automation help manage Azure Key Vault?</span></span>
<span data-ttu-id="f21b6-112">金鑰保存庫可以使用來管理 Azure 自動化中 hello [AzureRM 金鑰保存庫 cmdlet](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4)和[傳統 Azure 金鑰保存庫 cmdlet](https://msdn.microsoft.com/library/azure/dn868052.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f21b6-112">Key Vault can be managed in Azure Automation by using hello [AzureRM Key Vault cmdlets](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) and [Azure Classic Key Vault cmdlets](https://msdn.microsoft.com/library/azure/dn868052.aspx).</span></span> <span data-ttu-id="f21b6-113">管理傳統金鑰保存庫可自動在 Azure 自動化中的 hello Azure 模組，您可以匯入 hello [AzureRM KeyVault 模組](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4)到 Azure 自動化中，以便您可以執行許多您金鑰保存庫的管理hello 服務內的工作。</span><span class="sxs-lookup"><span data-stu-id="f21b6-113">hello Azure module for managing classic Key Vault is available automatically in Azure Automation, and you can import hello [AzureRM-KeyVault module](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) into Azure Automation, so that you can perform many of your Key Vault management tasks within hello service.</span></span> <span data-ttu-id="f21b6-114">您也可以跨 Azure 服務和第 3 個合作對象系統配對這些 cmdlet 在 Azure 自動化中利用 hello 適用於其他 Azure 服務、 tooautomate 複雜工作的 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="f21b6-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="f21b6-115">Hello Azure 金鑰保存庫 cmdlet，您可以執行這些工作和其他項目：</span><span class="sxs-lookup"><span data-stu-id="f21b6-115">With hello Azure Key Vault cmdlets you can perform these tasks among others:</span></span> 

* <span data-ttu-id="f21b6-116">建立和設定金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="f21b6-116">Create and configure a key vault</span></span>
* <span data-ttu-id="f21b6-117">建立或匯入金鑰</span><span class="sxs-lookup"><span data-stu-id="f21b6-117">Create or import a key</span></span>
* <span data-ttu-id="f21b6-118">建立或更新密碼</span><span class="sxs-lookup"><span data-stu-id="f21b6-118">Create or update a secret</span></span>
* <span data-ttu-id="f21b6-119">更新金鑰的屬性</span><span class="sxs-lookup"><span data-stu-id="f21b6-119">Update attributes of a key</span></span>
* <span data-ttu-id="f21b6-120">取得金鑰或密碼</span><span class="sxs-lookup"><span data-stu-id="f21b6-120">Get a key or secret</span></span>
* <span data-ttu-id="f21b6-121">刪除金鑰或密碼</span><span class="sxs-lookup"><span data-stu-id="f21b6-121">Delete a key or secret</span></span>

<span data-ttu-id="f21b6-122">以下是使用 PowerShell toomanage 金鑰保存庫的一些範例：</span><span class="sxs-lookup"><span data-stu-id="f21b6-122">Here are some examples of using PowerShell toomanage Key Vault:</span></span>  

* [<span data-ttu-id="f21b6-123">Azure 金鑰保存庫 - 逐步解說</span><span class="sxs-lookup"><span data-stu-id="f21b6-123">Azure Key Vault - Step by Step</span></span>](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step)
* [<span data-ttu-id="f21b6-124">設定 Azure 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="f21b6-124">Setting Up and Configuring an Azure Key Vault</span></span>](https://www.simple-talk.com/cloud/platform-as-a-service/setting-up-and-configuring-an-azure-key-vault)

## <a name="next-steps"></a><span data-ttu-id="f21b6-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f21b6-125">Next steps</span></span>
<span data-ttu-id="f21b6-126">既然您已經學會 hello 的 Azure 自動化，而且可以如何使用的 toomanage Azure 金鑰保存庫的基本概念，請遵循這些連結 toolearn 深入了解 Azure 自動化。</span><span class="sxs-lookup"><span data-stu-id="f21b6-126">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure Key Vault, follow these links toolearn more about Azure Automation.</span></span>

* <span data-ttu-id="f21b6-127">請參閱 hello Azure 自動化[入門教學課程](../automation/automation-first-runbook-graphical.md)。</span><span class="sxs-lookup"><span data-stu-id="f21b6-127">See hello Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md).</span></span>
* <span data-ttu-id="f21b6-128">請參閱 hello [Azure 金鑰保存庫的 PowerShell 指令碼](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5)。</span><span class="sxs-lookup"><span data-stu-id="f21b6-128">See hello [Azure Key Vault PowerShell scripts](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5).</span></span>

