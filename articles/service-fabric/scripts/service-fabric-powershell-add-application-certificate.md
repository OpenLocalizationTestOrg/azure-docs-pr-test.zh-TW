---
title: "Azure PowerShell 指令碼範例 - 將應用程式憑證新增到叢集 | Microsoft Docs"
description: "Azure PowerShell 指令碼範例 - 將應用程式憑證新增到 Service Fabric 叢集。"
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
ms.openlocfilehash: 9ccd6bb0458bc03e52103fa70cad26bd6bf98bd5
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2017
---
# <a name="add-an-application-certificate-to-a-service-fabric-cluster"></a><span data-ttu-id="0dbf8-103">將應用程式憑證新增到 Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="0dbf8-103">Add an application certificate to a Service Fabric cluster</span></span>

<span data-ttu-id="0dbf8-104">這個範例指令碼在指定的 Azure Key Vault 中建立自我簽署的憑證，並將它安裝到 Service Fabric 叢集的所有節點。</span><span class="sxs-lookup"><span data-stu-id="0dbf8-104">This sample script creates a self-signed certificate in the specified Azure key vault and installs it to all nodes of the Service Fabric cluster.</span></span> <span data-ttu-id="0dbf8-105">憑證也會下載至本機資料夾。</span><span class="sxs-lookup"><span data-stu-id="0dbf8-105">The certificate also downloads to a local folder.</span></span> <span data-ttu-id="0dbf8-106">下載的憑證名稱會與金鑰保存庫中的憑證名稱相同。</span><span class="sxs-lookup"><span data-stu-id="0dbf8-106">The name of the downloaded certificate is the same as the name of the certificate in the key vault.</span></span> <span data-ttu-id="0dbf8-107">視需要自訂參數。</span><span class="sxs-lookup"><span data-stu-id="0dbf8-107">Customize the parameters as needed.</span></span>

<span data-ttu-id="0dbf8-108">您可以視需要使用 [Azure PowerShell 指南 (英文)](/powershell/azure/overview) 中的指示來安裝 Azure PowerShell，然後執行 `Login-AzureRmAccount` 來建立與 Azure 的連線。</span><span class="sxs-lookup"><span data-stu-id="0dbf8-108">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview) and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span> 

## <a name="sample-script"></a><span data-ttu-id="0dbf8-109">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="0dbf8-109">Sample script</span></span>

<span data-ttu-id="0dbf8-110">[!code-powershell[主要](../../../powershell_scripts/service-fabric/add-application-certificate/add-new-application-certificate.ps1 "將應用程式憑證新增到叢集")]</span><span class="sxs-lookup"><span data-stu-id="0dbf8-110">[!code-powershell[main](../../../powershell_scripts/service-fabric/add-application-certificate/add-new-application-certificate.ps1 "Add an application certificate to a cluster")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="0dbf8-111">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="0dbf8-111">Script explanation</span></span>

<span data-ttu-id="0dbf8-112">此指令碼會使用下列命令：下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="0dbf8-112">This script uses the following commands: Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="0dbf8-113">命令</span><span class="sxs-lookup"><span data-stu-id="0dbf8-113">Command</span></span> | <span data-ttu-id="0dbf8-114">注意事項</span><span class="sxs-lookup"><span data-stu-id="0dbf8-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0dbf8-115">Add-AzureRmServiceFabricApplicationCertificate</span><span class="sxs-lookup"><span data-stu-id="0dbf8-115">Add-AzureRmServiceFabricApplicationCertificate</span></span>](/powershell/module/azurerm.servicefabric/Add-AzureRmServiceFabricApplicationCertificate) | <span data-ttu-id="0dbf8-116">將新的應用程式憑證新增到組成叢集的虛擬機器擴展集。</span><span class="sxs-lookup"><span data-stu-id="0dbf8-116">Add a new application certificate to the virtual machine scale set that make up the cluster.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="0dbf8-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0dbf8-117">Next steps</span></span>

<span data-ttu-id="0dbf8-118">如需有關 Azure PowerShell 模組的詳細資訊，請參閱 [Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="0dbf8-118">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="0dbf8-119">您可以在 [Azure PowerShell 範例](../service-fabric-powershell-samples.md)中找到適用於 Azure Service Fabric 的其他 Azure PowerShell 範例。</span><span class="sxs-lookup"><span data-stu-id="0dbf8-119">Additional Azure Powershell samples for Azure Service Fabric can be found in the [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
