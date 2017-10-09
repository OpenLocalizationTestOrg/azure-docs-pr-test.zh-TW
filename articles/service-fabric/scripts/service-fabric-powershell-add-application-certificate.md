---
title: "aaaAzure PowerShell 指令碼範例-新增應用程式憑證 tooa 叢集 |Microsoft 文件"
description: "Azure PowerShell 指令碼範例-新增應用程式憑證 tooa Service Fabric 叢集。"
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: aba62598e2e4775012f89b5070bef5e61aec64f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-an-application-certificate-tooa-service-fabric-cluster"></a><span data-ttu-id="42a89-103">新增應用程式憑證 tooa Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="42a89-103">Add an application certificate tooa Service Fabric cluster</span></span>

<span data-ttu-id="42a89-104">這個範例指令碼 hello 指定 Azure 金鑰保存庫中建立的自我簽署的憑證，並將它安裝 tooall hello Service Fabric 叢集節點。</span><span class="sxs-lookup"><span data-stu-id="42a89-104">This sample script creates a self-signed certificate in hello specified Azure key vault and installs it tooall nodes of hello Service Fabric cluster.</span></span> <span data-ttu-id="42a89-105">hello 憑證也會下載 tooa 本機資料夾。</span><span class="sxs-lookup"><span data-stu-id="42a89-105">hello certificate also downloads tooa local folder.</span></span> <span data-ttu-id="42a89-106">hello hello 下載憑證名稱是 hello 與 hello hello 金鑰保存庫中的 hello 憑證名稱相同。</span><span class="sxs-lookup"><span data-stu-id="42a89-106">hello name of hello downloaded certificate is hello same as hello name of hello certificate in hello key vault.</span></span> <span data-ttu-id="42a89-107">視需要自訂 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="42a89-107">Customize hello parameters as needed.</span></span>

<span data-ttu-id="42a89-108">如有需要安裝 Azure PowerShell 中使用 hello 指令位於 hello hello [Azure PowerShell 指南](/powershell/azure/overview)，然後執行`Login-AzureRmAccount`toocreate 與 Azure 的連線。</span><span class="sxs-lookup"><span data-stu-id="42a89-108">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview) and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span> 

## <a name="sample-script"></a><span data-ttu-id="42a89-109">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="42a89-109">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/add-application-certificate/add-new-application-certificate.ps1 "Add an application certificate tooa cluster")]

## <a name="script-explanation"></a><span data-ttu-id="42a89-110">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="42a89-110">Script explanation</span></span>

<span data-ttu-id="42a89-111">此指令碼會使用下列命令的 hello: hello 資料表中的每個命令連結 toocommand 特定文件。</span><span class="sxs-lookup"><span data-stu-id="42a89-111">This script uses hello following commands: Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="42a89-112">命令</span><span class="sxs-lookup"><span data-stu-id="42a89-112">Command</span></span> | <span data-ttu-id="42a89-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="42a89-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="42a89-114">Add-AzureRmServiceFabricApplicationCertificate</span><span class="sxs-lookup"><span data-stu-id="42a89-114">Add-AzureRmServiceFabricApplicationCertificate</span></span>](/powershell/module/azurerm.servicefabric/Add-AzureRmServiceFabricApplicationCertificate) | <span data-ttu-id="42a89-115">加入新的應用程式憑證 toohello 虛擬機器規模集 hello 叢集構成。</span><span class="sxs-lookup"><span data-stu-id="42a89-115">Add a new application certificate toohello virtual machine scale set that make up hello cluster.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="42a89-116">後續步驟</span><span class="sxs-lookup"><span data-stu-id="42a89-116">Next steps</span></span>

<span data-ttu-id="42a89-117">如需有關 hello Azure PowerShell 模組的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="42a89-117">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="42a89-118">適用於 Azure Service Fabric 的其他 Azure Powershell 範例可以在 hello [Azure PowerShell 範例](../service-fabric-powershell-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="42a89-118">Additional Azure Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
