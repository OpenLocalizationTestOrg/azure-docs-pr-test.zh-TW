---
title: "以命令列部署 Azure Stack 中的範本 | Microsoft Docs"
description: "了解如何使用跨平台命令列介面 (CLI) 部署範本到 Azure Stack 上。"
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
ms.openlocfilehash: cd1b61899ead7b4e86a81125841c1b37d019280b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-templates-in-azure-stack-using-the-command-line"></a><span data-ttu-id="2971f-103">使用命令列部署 Azure Stack 中的範本</span><span class="sxs-lookup"><span data-stu-id="2971f-103">Deploy templates in Azure Stack using the command line</span></span>
<span data-ttu-id="2971f-104">使用命令列將 Azure Resource Manager 範本部署到 Azure Stack 開發套件。</span><span class="sxs-lookup"><span data-stu-id="2971f-104">Use the command line to deploy Azure Resource Manager templates to the Azure Stack Development Kit.</span></span> <span data-ttu-id="2971f-105">Azure Resource Manager 範本可藉由單一協調作業，來部署和佈建應用程式的所有資源。</span><span class="sxs-lookup"><span data-stu-id="2971f-105">Azure Resource Manager templates deploy and provision all the resources for your application in a single, coordinated operation.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2971f-106">開始之前</span><span class="sxs-lookup"><span data-stu-id="2971f-106">Before you begin</span></span>
 - <span data-ttu-id="2971f-107">使用 Azure CLI [安裝並連線](azure-stack-connect-cli.md)至 Azure Stack</span><span class="sxs-lookup"><span data-stu-id="2971f-107">[Install and connect](azure-stack-connect-cli.md) to Azure Stack with Azure CLI</span></span>
 - <span data-ttu-id="2971f-108">從 [建立儲存體帳戶範例範本](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/101-create-storage-account) 下載 *azuredeploy.json* 和 *azuredeploy.parameters.json* 檔案。</span><span class="sxs-lookup"><span data-stu-id="2971f-108">Download the files *azuredeploy.json* and *azuredeploy.parameters.json* from the [create storage account example template](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/101-create-storage-account).</span></span>
 
## <a name="deploy-template"></a><span data-ttu-id="2971f-109">部署範本</span><span class="sxs-lookup"><span data-stu-id="2971f-109">Deploy template</span></span>
<span data-ttu-id="2971f-110">瀏覽至下載這些檔案的資料夾，並執行下列命令來部署範本：</span><span class="sxs-lookup"><span data-stu-id="2971f-110">Navigate to the folder where these files were downloaded and run the following command to deploy the template:</span></span>

    azure group create "cliRG" "local" –f azuredeploy.json –d "testDeploy" –e azuredeploy.parameters.json

<span data-ttu-id="2971f-111">此命令會將範本部署至 Azure Stack POC 預設位置中的資源群組 **cliRG**。</span><span class="sxs-lookup"><span data-stu-id="2971f-111">This command deploys the template to the resource group **cliRG** in the Azure Stack POC’s default location.</span></span>

## <a name="validate-template-deployment"></a><span data-ttu-id="2971f-112">驗證範本部署</span><span class="sxs-lookup"><span data-stu-id="2971f-112">Validate template deployment</span></span>
<span data-ttu-id="2971f-113">若要查看此資源群組和儲存體帳戶，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="2971f-113">To see this resource group and storage account, use the following commands:</span></span>

    azure group list

    azure storage account list

## <a name="next-steps"></a><span data-ttu-id="2971f-114">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2971f-114">Next steps</span></span>
[<span data-ttu-id="2971f-115">管理使用者權限</span><span class="sxs-lookup"><span data-stu-id="2971f-115">Manage user permissions</span></span>](azure-stack-manage-permissions.md)

