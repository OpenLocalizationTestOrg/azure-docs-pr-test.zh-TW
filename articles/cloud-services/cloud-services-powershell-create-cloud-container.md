---
title: "使用 PowerShell 的雲端服務容器 aaaCreate |Microsoft 文件"
description: "本文說明如何 toocreate 雲端服務使用 PowerShell 的容器。 hello 容器會裝載 web 和背景工作角色。"
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
ms.openlocfilehash: 4c47b10b5ba1f9cc39594a45cd869bf04fcaadf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-an-azure-powershell-command-toocreate-an-empty-cloud-service-container"></a><span data-ttu-id="0620e-104">使用 Azure PowerShell 命令 toocreate 空的雲端服務容器</span><span class="sxs-lookup"><span data-stu-id="0620e-104">Use an Azure PowerShell command toocreate an empty cloud service container</span></span>
<span data-ttu-id="0620e-105">本文說明如何 tooquickly 建立雲端服務容器，使用 Azure PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="0620e-105">This article explains how tooquickly create a Cloud Services container using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="0620e-106">請遵循下列步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="0620e-106">Please follow hello steps below:</span></span>

1. <span data-ttu-id="0620e-107">安裝 hello Microsoft Azure PowerShell cmdlet 從 hello [Azure PowerShell 下載](http://aka.ms/webpi-azps)頁面。</span><span class="sxs-lookup"><span data-stu-id="0620e-107">Install hello Microsoft Azure PowerShell cmdlet from hello [Azure PowerShell downloads](http://aka.ms/webpi-azps) page.</span></span>
2. <span data-ttu-id="0620e-108">開啟 hello PowerShell 命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="0620e-108">Open hello PowerShell command prompt.</span></span>
3. <span data-ttu-id="0620e-109">使用 hello [Add-azureaccount](https://msdn.microsoft.com/library/dn495128.aspx) toosign 中的。</span><span class="sxs-lookup"><span data-stu-id="0620e-109">Use hello [Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) toosign in.</span></span>

   > [!NOTE]
   > <span data-ttu-id="0620e-110">如需有關安裝 hello Azure PowerShell cmdlet 及連線 tooyour Azure 訂用帳戶的進一步指示，請參閱太[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="0620e-110">For further instruction on installing hello Azure PowerShell cmdlet and connecting tooyour Azure subscription, refer too[How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
   >
   >
4. <span data-ttu-id="0620e-111">使用 hello**新 AzureService** cmdlet toocreate 空白的 Azure 雲端服務容器。</span><span class="sxs-lookup"><span data-stu-id="0620e-111">Use hello **New-AzureService** cmdlet toocreate an empty Azure cloud service container.</span></span>

    ```
    New-AzureService [-ServiceName] <String> [-AffinityGroup] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
    New-AzureService [-ServiceName] <String> [-Location] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
   ```
5. <span data-ttu-id="0620e-112">請依照這個範例 tooinvoke hello 指令程式：</span><span class="sxs-lookup"><span data-stu-id="0620e-112">Follow this example tooinvoke hello cmdlet:</span></span>

   ```
   New-AzureService -ServiceName "mytestcloudservice" -Location "Central US" -Label "mytestcloudservice"
   ```

<span data-ttu-id="0620e-113">如需有關建立 hello Azure 雲端服務的詳細資訊，請執行：</span><span class="sxs-lookup"><span data-stu-id="0620e-113">For more information about creating hello Azure cloud service, run:</span></span>

```
Get-help New-AzureService
```

### <a name="next-steps"></a><span data-ttu-id="0620e-114">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0620e-114">Next steps</span></span>
* <span data-ttu-id="0620e-115">toomanage hello 雲端服務部署，請參閱 toohello [Get-azureservice](https://msdn.microsoft.com/library/azure/dn495131.aspx)，[移除 AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx)，和[組 AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx)命令。</span><span class="sxs-lookup"><span data-stu-id="0620e-115">toomanage hello cloud service deployment, refer toohello [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx), [Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx), and [Set-AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx) commands.</span></span> <span data-ttu-id="0620e-116">您也可能是指太[tooconfigure 雲端服務的方式](cloud-services-how-to-configure.md)以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="0620e-116">You may also refer too[How tooconfigure cloud services](cloud-services-how-to-configure.md) for further information.</span></span>
* <span data-ttu-id="0620e-117">toopublish 您的雲端服務專案 tooAzure，請參閱 toohello **PublishCloudService.ps1**中的程式碼範例[在 Azure 雲端服務的持續傳遞](cloud-services-dotnet-continuous-delivery.md)。</span><span class="sxs-lookup"><span data-stu-id="0620e-117">toopublish your cloud service project tooAzure, refer toohello  **PublishCloudService.ps1** code sample from [Continuous delivery for cloud service in Azure](cloud-services-dotnet-continuous-delivery.md).</span></span>
