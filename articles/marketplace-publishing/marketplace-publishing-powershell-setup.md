---
title: "PowerShell toocreate hello Marketplace 的 VM 上 aaaSet |Microsoft 文件"
description: "設定 Azure PowerShell，以及使用選擇性程序的指示，toocreate VM 映像 toodeploy 和上銷售，hello Azure Marketplace"
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
ms.openlocfilehash: cd2ebad7472248b8f921706e1a8c82d41f33b9cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-azure-powershell-toocreate-an-offer-for-hello-azure-marketplace"></a><span data-ttu-id="19729-103">設定 Azure PowerShell toocreate hello Azure Marketplace 供應項目</span><span class="sxs-lookup"><span data-stu-id="19729-103">Set up Azure PowerShell toocreate an offer for hello Azure Marketplace</span></span>
<span data-ttu-id="19729-104">如需詳細資訊 tooset 向上 PowerShell 在 Azure 中，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="19729-104">For detailed information on how tooset up PowerShell in Azure, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="19729-105">一個簡單的方法是 toouse hello 憑證方法，它會下載並匯入進行驗證所需的憑證。</span><span class="sxs-lookup"><span data-stu-id="19729-105">A simple approach is toouse hello certificate method, which downloads and imports a certificate needed for authentication.</span></span> <span data-ttu-id="19729-106">tooobtain hello 所需的憑證，請使用 hello **Get-azurepublishsettingsfile** cmdlet。</span><span class="sxs-lookup"><span data-stu-id="19729-106">tooobtain hello needed certificate, use hello **Get-AzurePublishSettingsFile** cmdlet.</span></span> <span data-ttu-id="19729-107">當系統提示您輸入時，請儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="19729-107">Save hello file when you're prompted.</span></span> <span data-ttu-id="19729-108">tooimport hello 憑證到 PowerShell 工作階段，使用 hello **Import-azurepublishsettingsfile** cmdlet。</span><span class="sxs-lookup"><span data-stu-id="19729-108">tooimport hello certificate into a PowerShell session, use hello **Import-AzurePublishSettingsFile** cmdlet.</span></span>

<span data-ttu-id="19729-109">tooconfigure 和市集 hello Microsoft Azure 訂用帳戶的一般設定 hello PowerShell 工作階段，使用 hello**組 AzureSubscription**和**Select-azuresubscription** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="19729-109">tooconfigure and store hello common Microsoft Azure subscription settings for hello PowerShell session, use hello **Set-AzureSubscription** and **Select-AzureSubscription** cmdlets:</span></span>

        Set-AzureSubscription -SubscriptionName “mySubName” -CurrentStorageAccountName “mystorageaccount”
        Select-AzureSubscription -SubscriptionName "mySubName" –Current

<span data-ttu-id="19729-110">hello 第一個命令會將預設儲存體帳戶關聯 hello 訂用帳戶 （在某些 VM 佈建作業時需要）。</span><span class="sxs-lookup"><span data-stu-id="19729-110">hello first command associates a default storage account with hello subscription (needed for some VM provisioning operations).</span></span>  <span data-ttu-id="19729-111">hello 第二個可讓 hello hello （辨識其他的 cmdlet） 的其中一個目前的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="19729-111">hello second makes hello subscription hello current one (recognized by other cmdlets).</span></span>

## <a name="see-also"></a><span data-ttu-id="19729-112">另請參閱</span><span class="sxs-lookup"><span data-stu-id="19729-112">See also</span></span>
* [<span data-ttu-id="19729-113">快速入門： 如何 toopublish 優惠 toohello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="19729-113">Getting started: How toopublish an offer toohello Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)
* [<span data-ttu-id="19729-114">建立虛擬機器映像的 hello Marketplace</span><span class="sxs-lookup"><span data-stu-id="19729-114">Creating a virtual machine image for hello Marketplace</span></span>](marketplace-publishing-vm-image-creation.md)

