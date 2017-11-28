---
title: "aaaAzure 服務網狀架構 CLI 指令碼部署的範例"
description: "部署應用程式 tooan Azure Service Fabric 叢集使用 hello Azure Service Fabric CLI"
services: service-fabric
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: adegeo
ms.custom: mvc
ms.openlocfilehash: aaec7042a4fd7ed32ad706cde70361f23d18fb48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-service-fabric-cluster"></a><span data-ttu-id="4e1c8-103">部署應用程式 tooa Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="4e1c8-103">Deploy an application tooa Service Fabric cluster</span></span>

<span data-ttu-id="4e1c8-104">這個範例指令碼複製應用程式封裝 tooa 叢集映像存放區、 hello 叢集中註冊 hello 應用程式類型和建立應用程式執行個體從 hello 應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="4e1c8-104">This sample script copies an application package tooa cluster image store, registers hello application type in hello cluster, and creates an application instance from hello application type.</span></span> <span data-ttu-id="4e1c8-105">在這個階段，還會建立所有預設的服務。</span><span class="sxs-lookup"><span data-stu-id="4e1c8-105">Any default services are also created at this time.</span></span>

<span data-ttu-id="4e1c8-106">如有需要安裝 hello[服務網狀架構 CLI](../service-fabric-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="4e1c8-106">If needed, install hello [Service Fabric CLI](../service-fabric-cli.md).</span></span>

## <a name="sample-script"></a><span data-ttu-id="4e1c8-107">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="4e1c8-107">Sample script</span></span>

[!code-sh[main](../../../cli_scripts/service-fabric/deploy-application/deploy-application.sh "Deploy an application tooa cluster")]

## <a name="clean-up-deployment"></a><span data-ttu-id="4e1c8-108">清除部署</span><span class="sxs-lookup"><span data-stu-id="4e1c8-108">Clean up deployment</span></span>

<span data-ttu-id="4e1c8-109">當完成時，hello[移除](cli-remove-application.md)指令碼可以使用的 tooremove hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4e1c8-109">When done, hello [remove](cli-remove-application.md) script can be used tooremove hello application.</span></span> <span data-ttu-id="4e1c8-110">hello 移除指令碼刪除 hello 應用程式執行個體、 取消登錄 hello 應用程式類型，並刪除映像存放區中的 hello 應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="4e1c8-110">hello remove script deletes hello application instance, unregisters hello application type, and deletes hello application package from the image store.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e1c8-111">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4e1c8-111">Next steps</span></span>

<span data-ttu-id="4e1c8-112">如需詳細資訊，請參閱 hello[服務網狀架構 CLI 文件](../service-fabric-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="4e1c8-112">For more information, see hello [Service Fabric CLI documentation](../service-fabric-cli.md).</span></span>

<span data-ttu-id="4e1c8-113">適用於 Azure Service Fabric 的其他服務網狀架構 CLI 範例可以在 hello[服務網狀架構 CLI 範例](../samples-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="4e1c8-113">Additional Service Fabric CLI samples for Azure Service Fabric can be found in hello [Service Fabric CLI samples](../samples-cli.md).</span></span>
