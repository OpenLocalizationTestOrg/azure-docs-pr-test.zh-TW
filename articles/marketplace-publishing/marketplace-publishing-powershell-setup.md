---
title: "設定 PowerShell 以建立 Marketplace 的 VM | Microsoft Docs"
description: "設定 Azure PowerShell 的指示，可做為選擇性處理流程來建立要部署至 Azure Marketplace 並在其上銷售的 VM 映像"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e19d6cda-76df-4e42-be84-c9fe47a636db
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/04/2016
ms.author: hascipio
ms.openlocfilehash: bbcce5093d2bbd5326523063db7d0e565fe4de6d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-azure-powershell-to-create-an-offer-for-the-azure-marketplace"></a><span data-ttu-id="64d5f-103">設定 Azure PowerShell 以在 Azure Marketplace 上建立供應項目</span><span class="sxs-lookup"><span data-stu-id="64d5f-103">Set up Azure PowerShell to create an offer for the Azure Marketplace</span></span>
<span data-ttu-id="64d5f-104">如需如何設定 Azure PowerShell 的詳細資訊，請參閱 [如何安裝及設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="64d5f-104">For detailed information on how to set up PowerShell in Azure, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="64d5f-105">簡單的方式就是使用憑證方法，該方法會下載並匯入驗證所需的憑證。</span><span class="sxs-lookup"><span data-stu-id="64d5f-105">A simple approach is to use the certificate method, which downloads and imports a certificate needed for authentication.</span></span> <span data-ttu-id="64d5f-106">若要取得所需的憑證，請使用 **Get-AzurePublishSettingsFile** Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="64d5f-106">To obtain the needed certificate, use the **Get-AzurePublishSettingsFile** cmdlet.</span></span> <span data-ttu-id="64d5f-107">出現系統提示時儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="64d5f-107">Save the file when you're prompted.</span></span> <span data-ttu-id="64d5f-108">若要將憑證匯入 PowerShell 工作階段，請使用 **Import-AzurePublishSettingsFile** Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="64d5f-108">To import the certificate into a PowerShell session, use the **Import-AzurePublishSettingsFile** cmdlet.</span></span>

<span data-ttu-id="64d5f-109">若要設定和儲存 PowerShell 工作階段的常見 Microsoft Azure 訂用帳戶設定，請使用 **Set-AzureSubscription** 和 **Select-AzureSubscription** Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="64d5f-109">To configure and store the common Microsoft Azure subscription settings for the PowerShell session, use the **Set-AzureSubscription** and **Select-AzureSubscription** cmdlets:</span></span>

        Set-AzureSubscription -SubscriptionName “mySubName” -CurrentStorageAccountName “mystorageaccount”
        Select-AzureSubscription -SubscriptionName "mySubName" –Current

<span data-ttu-id="64d5f-110">第一個命令會讓預設儲存體帳戶與訂用帳戶 (有些 VM 佈建作業所需) 產生關聯。</span><span class="sxs-lookup"><span data-stu-id="64d5f-110">The first command associates a default storage account with the subscription (needed for some VM provisioning operations).</span></span>  <span data-ttu-id="64d5f-111">第二個命令會讓訂用帳戶成為目前的訂用帳戶 (由其他 Cmdlet 辨識)。</span><span class="sxs-lookup"><span data-stu-id="64d5f-111">The second makes the subscription the current one (recognized by other cmdlets).</span></span>

## <a name="see-also"></a><span data-ttu-id="64d5f-112">另請參閱</span><span class="sxs-lookup"><span data-stu-id="64d5f-112">See also</span></span>
* [<span data-ttu-id="64d5f-113">使用者入門：如何將供應項目發佈至 Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="64d5f-113">Getting started: How to publish an offer to the Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)
* [<span data-ttu-id="64d5f-114">建立 Marketplace 的虛擬機器映像</span><span class="sxs-lookup"><span data-stu-id="64d5f-114">Creating a virtual machine image for the Marketplace</span></span>](marketplace-publishing-vm-image-creation.md)

