---
title: "以 Azure 堆疊中的 hello 命令列 aaaDeploy 範本 |Microsoft 文件"
description: "了解如何 toouse hello 跨平台命令列介面 (CLI) toodeploy 範本 tooAzure 堆疊。"
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: 9584177f-4af3-4834-864d-930b09ae0995
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: 6fa6b19ac94d3f020008d04ff07f1ce489aa3418
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-templates-in-azure-stack-using-hello-command-line"></a><span data-ttu-id="46b4f-103">部署 Azure 堆疊使用 hello 命令列中的範本</span><span class="sxs-lookup"><span data-stu-id="46b4f-103">Deploy templates in Azure Stack using hello command line</span></span>
<span data-ttu-id="46b4f-104">使用 hello 命令列 toodeploy Azure Resource Manager 範本 toohello Azure 堆疊開發套件。</span><span class="sxs-lookup"><span data-stu-id="46b4f-104">Use hello command line toodeploy Azure Resource Manager templates toohello Azure Stack Development Kit.</span></span> <span data-ttu-id="46b4f-105">Azure 資源管理員範本部署和佈建您的應用程式在單一、 協調作業中的所有 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="46b4f-105">Azure Resource Manager templates deploy and provision all hello resources for your application in a single, coordinated operation.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="46b4f-106">開始之前</span><span class="sxs-lookup"><span data-stu-id="46b4f-106">Before you begin</span></span>
 - <span data-ttu-id="46b4f-107">[安裝並連接](azure-stack-connect-cli.md)tooAzure 堆疊時會搭配 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="46b4f-107">[Install and connect](azure-stack-connect-cli.md) tooAzure Stack with Azure CLI</span></span>
 - <span data-ttu-id="46b4f-108">下載 hello 檔案*azuredeploy.json*和*azuredeploy.parameters.json*從 hello[建立儲存體帳戶範例範本](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/101-create-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="46b4f-108">Download hello files *azuredeploy.json* and *azuredeploy.parameters.json* from hello [create storage account example template](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/101-create-storage-account).</span></span>
 
## <a name="deploy-template"></a><span data-ttu-id="46b4f-109">部署範本</span><span class="sxs-lookup"><span data-stu-id="46b4f-109">Deploy template</span></span>
<span data-ttu-id="46b4f-110">瀏覽 toohello 資料夾，其中這些檔案已下載並執行下列命令 toodeploy hello 範本 hello:</span><span class="sxs-lookup"><span data-stu-id="46b4f-110">Navigate toohello folder where these files were downloaded and run hello following command toodeploy hello template:</span></span>

    azure group create "cliRG" "local" –f azuredeploy.json –d "testDeploy" –e azuredeploy.parameters.json

<span data-ttu-id="46b4f-111">此命令會將部署 hello 範本 toohello 資源群組**cliRG** hello Azure 堆疊 POC 的預設位置中。</span><span class="sxs-lookup"><span data-stu-id="46b4f-111">This command deploys hello template toohello resource group **cliRG** in hello Azure Stack POC’s default location.</span></span>

## <a name="validate-template-deployment"></a><span data-ttu-id="46b4f-112">驗證範本部署</span><span class="sxs-lookup"><span data-stu-id="46b4f-112">Validate template deployment</span></span>
<span data-ttu-id="46b4f-113">toosee 此資源群組和儲存體帳戶時，使用 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="46b4f-113">toosee this resource group and storage account, use hello following commands:</span></span>

    azure group list

    azure storage account list

## <a name="next-steps"></a><span data-ttu-id="46b4f-114">後續步驟</span><span class="sxs-lookup"><span data-stu-id="46b4f-114">Next steps</span></span>
[<span data-ttu-id="46b4f-115">管理使用者權限</span><span class="sxs-lookup"><span data-stu-id="46b4f-115">Manage user permissions</span></span>](azure-stack-manage-permissions.md)

