---
title: "Azure Service Fabric CLI 指令碼部署範例"
description: "使用 Azure Service Fabric CLI 將應用程式部署至 Azure Service Fabric 叢集"
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
ms.openlocfilehash: c77ecfccdf7d3e34b0b3133e9c63810a04fb1132
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-an-application-to-a-service-fabric-cluster"></a><span data-ttu-id="b2f2c-103">將應用程式部署到 Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="b2f2c-103">Deploy an application to a Service Fabric cluster</span></span>

<span data-ttu-id="b2f2c-104">這個範例指令碼會將應用程式封裝複製到叢集映像存放區、在叢集中註冊應用程式類型，並從應用程式類型建立應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="b2f2c-104">This sample script copies an application package to a cluster image store, registers the application type in the cluster, and creates an application instance from the application type.</span></span> <span data-ttu-id="b2f2c-105">在這個階段，還會建立所有預設的服務。</span><span class="sxs-lookup"><span data-stu-id="b2f2c-105">Any default services are also created at this time.</span></span>

<span data-ttu-id="b2f2c-106">如有需要，請安裝[ Service Fabric SDK](../service-fabric-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="b2f2c-106">If needed, install the [Service Fabric CLI](../service-fabric-cli.md).</span></span>

## <a name="sample-script"></a><span data-ttu-id="b2f2c-107">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="b2f2c-107">Sample script</span></span>

<span data-ttu-id="b2f2c-108">[!code-sh[主要](../../../cli_scripts/service-fabric/deploy-application/deploy-application.sh "將應用程式部署到叢集")]</span><span class="sxs-lookup"><span data-stu-id="b2f2c-108">[!code-sh[main](../../../cli_scripts/service-fabric/deploy-application/deploy-application.sh "Deploy an application to a cluster")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="b2f2c-109">清除部署</span><span class="sxs-lookup"><span data-stu-id="b2f2c-109">Clean up deployment</span></span>

<span data-ttu-id="b2f2c-110">完成時，可以使用[移除](cli-remove-application.md)指令碼將應用程式移除。</span><span class="sxs-lookup"><span data-stu-id="b2f2c-110">When done, the [remove](cli-remove-application.md) script can be used to remove the application.</span></span> <span data-ttu-id="b2f2c-111">移除指令碼會刪除應用程式執行個體、將應用程式類型取消登錄，並從映像存放區刪除應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="b2f2c-111">The remove script deletes the application instance, unregisters the application type, and deletes the application package from the image store.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b2f2c-112">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b2f2c-112">Next steps</span></span>

<span data-ttu-id="b2f2c-113">如需詳細資訊，請參閱 [Service Fabric CLI 文件](../service-fabric-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="b2f2c-113">For more information, see the [Service Fabric CLI documentation](../service-fabric-cli.md).</span></span>

<span data-ttu-id="b2f2c-114">您可以在 [Service Fabric CLI 範例](../samples-cli.md)中找到適用於 Azure Service Fabric 的其他 Service Fabric CLI 範例。</span><span class="sxs-lookup"><span data-stu-id="b2f2c-114">Additional Service Fabric CLI samples for Azure Service Fabric can be found in the [Service Fabric CLI samples](../samples-cli.md).</span></span>
