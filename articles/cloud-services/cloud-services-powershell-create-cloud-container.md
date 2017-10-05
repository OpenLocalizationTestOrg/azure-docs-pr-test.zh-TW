---
title: "使用 PowerShell 建立雲端服務容器 | Microsoft Docs"
description: "這篇文章說明如何使用 PowerShell 建立雲端服務容器。 容器會裝載 Web 和背景工作角色。"
services: cloud-services
documentationcenter: .net
author: cawaMS
manager: timlt
editor: 
ms.assetid: c8f32469-610e-4f37-a3aa-4fac5c714e13
ms.service: cloud-services
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 11/18/2016
ms.author: cawa
ms.openlocfilehash: 2023fa7b318f9f76ce1e1ea0a46110297be9a001
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-an-azure-powershell-command-to-create-an-empty-cloud-service-container"></a><span data-ttu-id="5e640-104">使用 Azure PowerShell 命令來建立空白的雲端服務容器</span><span class="sxs-lookup"><span data-stu-id="5e640-104">Use an Azure PowerShell command to create an empty cloud service container</span></span>
<span data-ttu-id="5e640-105">這篇文章說明如何使用 Azure PowerShell Cmdlet 快速建立雲端服務容器。</span><span class="sxs-lookup"><span data-stu-id="5e640-105">This article explains how to quickly create a Cloud Services container using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="5e640-106">請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="5e640-106">Please follow the steps below:</span></span>

1. <span data-ttu-id="5e640-107">從 [Azure PowerShell 下載](http://aka.ms/webpi-azps) 頁面安裝 Microsoft Azure PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="5e640-107">Install the Microsoft Azure PowerShell cmdlet from the [Azure PowerShell downloads](http://aka.ms/webpi-azps) page.</span></span>
2. <span data-ttu-id="5e640-108">開啟 PowerShell 命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="5e640-108">Open the PowerShell command prompt.</span></span>
3. <span data-ttu-id="5e640-109">使用 [Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) 登入。</span><span class="sxs-lookup"><span data-stu-id="5e640-109">Use the [Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) to sign in.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5e640-110">如需安裝 Azure PowerShell Cmdlet 及連接至您的 Azure 訂用帳戶的進一步指示，請參閱 [如何安裝及設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="5e640-110">For further instruction on installing the Azure PowerShell cmdlet and connecting to your Azure subscription, refer to [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
   >
   >
4. <span data-ttu-id="5e640-111">使用 **New-AzureService** Cmdlet 來建立空白的 Azure 雲端服務容器。</span><span class="sxs-lookup"><span data-stu-id="5e640-111">Use the **New-AzureService** cmdlet to create an empty Azure cloud service container.</span></span>

    ```
    New-AzureService [-ServiceName] <String> [-AffinityGroup] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
    New-AzureService [-ServiceName] <String> [-Location] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
   ```
5. <span data-ttu-id="5e640-112">遵循此範例以叫用 Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="5e640-112">Follow this example to invoke the cmdlet:</span></span>

   ```
   New-AzureService -ServiceName "mytestcloudservice" -Location "Central US" -Label "mytestcloudservice"
   ```

<span data-ttu-id="5e640-113">如需建立 Azure 雲端服務的詳細資訊，請執行：</span><span class="sxs-lookup"><span data-stu-id="5e640-113">For more information about creating the Azure cloud service, run:</span></span>

```
Get-help New-AzureService
```

### <a name="next-steps"></a><span data-ttu-id="5e640-114">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5e640-114">Next steps</span></span>
* <span data-ttu-id="5e640-115">若要管理雲端服務部署，請參閱 [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx)、[Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx) 及 [Set-AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx) 命令。</span><span class="sxs-lookup"><span data-stu-id="5e640-115">To manage the cloud service deployment, refer to the [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx), [Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx), and [Set-AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx) commands.</span></span> <span data-ttu-id="5e640-116">另請參閱 [如何設定雲端服務](cloud-services-how-to-configure.md) 以取得進一步的資訊。</span><span class="sxs-lookup"><span data-stu-id="5e640-116">You may also refer to [How to configure cloud services](cloud-services-how-to-configure.md) for further information.</span></span>
* <span data-ttu-id="5e640-117">若要將雲端服務專案發佈至 Azure，請參閱[在 Azure 中持續傳遞雲端服務](cloud-services-dotnet-continuous-delivery.md)中的 **PublishCloudService.ps1** 程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="5e640-117">To publish your cloud service project to Azure, refer to the  **PublishCloudService.ps1** code sample from [Continuous delivery for cloud service in Azure](cloud-services-dotnet-continuous-delivery.md).</span></span>
