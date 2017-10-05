---
title: "Azure Cloud Shell (預覽) 功能 | Microsoft Docs"
description: "Azure Cloud Shell 的功能概觀"
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: 67f03d5857e37b253ac57536e289b5468d69e9b5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="features-and-tools-for-azure-cloud-shell"></a><span data-ttu-id="ce964-103">Azure Cloud Shell 的功能和工具</span><span class="sxs-lookup"><span data-stu-id="ce964-103">Features and Tools for Azure Cloud Shell</span></span>
<span data-ttu-id="ce964-104">Azure Cloud Shell 是以瀏覽器為基礎的殼層經驗，用於管理和開發 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="ce964-104">Azure Cloud Shell is a browser-based shell experience to manage and develop Azure resources.</span></span>

<span data-ttu-id="ce964-105">Cloud Shell 提供可從瀏覽器存取、預先設定的殼層功能來管理 Azure 資源，您不需要另外自行安裝、版本控制和維護電腦。</span><span class="sxs-lookup"><span data-stu-id="ce964-105">Cloud Shell offers a browser-accessible, pre-configured shell experience for managing Azure resources without the overhead of installing, versioning, and maintaining a machine yourself.</span></span>

<span data-ttu-id="ce964-106">Cloud Shell 依照要求而佈建電腦，因此，不會在工作階段之間保存電腦狀態。</span><span class="sxs-lookup"><span data-stu-id="ce964-106">Cloud Shell provisions machines on a per-request basis and as a result machine state will not persist across sessions.</span></span> <span data-ttu-id="ce964-107">由於 Cloud Shell 是針對互動式工作階段而建置，所以殼層會在殼層閒置 20 分鐘後自動終止。</span><span class="sxs-lookup"><span data-stu-id="ce964-107">Since Cloud Shell is built for interactive sessions, shells automatically terminate after 20 minutes of shell inactivity.</span></span>

## <a name="bash-in-cloud-shell"></a><span data-ttu-id="ce964-108">Cloud Shell 中的 Bash</span><span class="sxs-lookup"><span data-stu-id="ce964-108">Bash in Cloud Shell</span></span>
### <a name="tools"></a><span data-ttu-id="ce964-109">工具</span><span class="sxs-lookup"><span data-stu-id="ce964-109">Tools</span></span>
|<span data-ttu-id="ce964-110">類別</span><span class="sxs-lookup"><span data-stu-id="ce964-110">Category</span></span>   |<span data-ttu-id="ce964-111">名稱</span><span class="sxs-lookup"><span data-stu-id="ce964-111">Name</span></span>   |
|---|---|
|<span data-ttu-id="ce964-112">Linux 殼層直譯器</span><span class="sxs-lookup"><span data-stu-id="ce964-112">Linux shell interpreter</span></span>|<span data-ttu-id="ce964-113">Bash</span><span class="sxs-lookup"><span data-stu-id="ce964-113">Bash</span></span><br> <span data-ttu-id="ce964-114">sh</span><span class="sxs-lookup"><span data-stu-id="ce964-114">sh</span></span>               |
|<span data-ttu-id="ce964-115">Azure 工具</span><span class="sxs-lookup"><span data-stu-id="ce964-115">Azure tools</span></span>            |<span data-ttu-id="ce964-116">[Azure CLI 2.0](https://github.com/Azure/azure-cli) \(英文\) 和 [1.0](https://github.com/Azure/azure-xplat-cli) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="ce964-116">[Azure CLI 2.0](https://github.com/Azure/azure-cli) and [1.0](https://github.com/Azure/azure-xplat-cli)</span></span><br> [<span data-ttu-id="ce964-117">AzCopy</span><span class="sxs-lookup"><span data-stu-id="ce964-117">AzCopy</span></span>](https://docs.microsoft.com/azure/storage/storage-use-azcopy)<br> [<span data-ttu-id="ce964-118">Batch Shipyard</span><span class="sxs-lookup"><span data-stu-id="ce964-118">Batch Shipyard</span></span>](https://github.com/Azure/batch-shipyard)     |
|<span data-ttu-id="ce964-119">文字編輯器</span><span class="sxs-lookup"><span data-stu-id="ce964-119">Text editors</span></span>           |<span data-ttu-id="ce964-120">vim</span><span class="sxs-lookup"><span data-stu-id="ce964-120">vim</span></span><br> <span data-ttu-id="ce964-121">nano</span><span class="sxs-lookup"><span data-stu-id="ce964-121">nano</span></span><br> <span data-ttu-id="ce964-122">emacs</span><span class="sxs-lookup"><span data-stu-id="ce964-122">emacs</span></span>       |
|<span data-ttu-id="ce964-123">原始檔控制</span><span class="sxs-lookup"><span data-stu-id="ce964-123">Source control</span></span>         |<span data-ttu-id="ce964-124">git</span><span class="sxs-lookup"><span data-stu-id="ce964-124">git</span></span>                    |
|<span data-ttu-id="ce964-125">建置工具</span><span class="sxs-lookup"><span data-stu-id="ce964-125">Build tools</span></span>            |<span data-ttu-id="ce964-126">make</span><span class="sxs-lookup"><span data-stu-id="ce964-126">make</span></span><br> <span data-ttu-id="ce964-127">maven</span><span class="sxs-lookup"><span data-stu-id="ce964-127">maven</span></span><br> <span data-ttu-id="ce964-128">npm</span><span class="sxs-lookup"><span data-stu-id="ce964-128">npm</span></span><br> <span data-ttu-id="ce964-129">pip</span><span class="sxs-lookup"><span data-stu-id="ce964-129">pip</span></span>         |
|<span data-ttu-id="ce964-130">容器</span><span class="sxs-lookup"><span data-stu-id="ce964-130">Containers</span></span>             |<span data-ttu-id="ce964-131">[Docker CLI](https://github.com/docker/cli) \(英文\)/[Docker Machine](https://github.com/docker/machine) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="ce964-131">[Docker CLI](https://github.com/docker/cli)/[Docker Machine](https://github.com/docker/machine)</span></span><br> <span data-ttu-id="ce964-132">[Kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="ce964-132">[Kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/)</span></span><br> <span data-ttu-id="ce964-133">[Draft](https://github.com/Azure/draft)(英文\)</span><span class="sxs-lookup"><span data-stu-id="ce964-133">[Draft](https://github.com/Azure/draft)</span></span><br> <span data-ttu-id="ce964-134">[DC/OS CLI](https://github.com/dcos/dcos-cli) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="ce964-134">[DC/OS CLI](https://github.com/dcos/dcos-cli)</span></span>         |
|<span data-ttu-id="ce964-135">資料庫</span><span class="sxs-lookup"><span data-stu-id="ce964-135">Databases</span></span>              |<span data-ttu-id="ce964-136">MySQL 用戶端</span><span class="sxs-lookup"><span data-stu-id="ce964-136">MySQL client</span></span><br> <span data-ttu-id="ce964-137">PostgreSql 用戶端</span><span class="sxs-lookup"><span data-stu-id="ce964-137">PostgreSql client</span></span><br> <span data-ttu-id="ce964-138">[sqlcmd 公用程式](https://docs.microsoft.com/sql/tools/sqlcmd-utility) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="ce964-138">[sqlcmd Utility](https://docs.microsoft.com/sql/tools/sqlcmd-utility)</span></span><br> [<span data-ttu-id="ce964-139">mssql-scripter</span><span class="sxs-lookup"><span data-stu-id="ce964-139">mssql-scripter</span></span>](https://github.com/Microsoft/sql-xplat-cli) |
|<span data-ttu-id="ce964-140">其他</span><span class="sxs-lookup"><span data-stu-id="ce964-140">Other</span></span>                  |<span data-ttu-id="ce964-141">iPython 用戶端</span><span class="sxs-lookup"><span data-stu-id="ce964-141">iPython Client</span></span><br> <span data-ttu-id="ce964-142">[Cloud Foundry CLI](https://github.com/cloudfoundry/cli) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="ce964-142">[Cloud Foundry CLI](https://github.com/cloudfoundry/cli)</span></span><br> |

### <a name="language-support"></a><span data-ttu-id="ce964-143">語言支援</span><span class="sxs-lookup"><span data-stu-id="ce964-143">Language support</span></span>
|<span data-ttu-id="ce964-144">語言</span><span class="sxs-lookup"><span data-stu-id="ce964-144">Language</span></span>   |<span data-ttu-id="ce964-145">版本</span><span class="sxs-lookup"><span data-stu-id="ce964-145">Version</span></span>   |
|---|---|
|<span data-ttu-id="ce964-146">.NET</span><span class="sxs-lookup"><span data-stu-id="ce964-146">.NET</span></span>       |<span data-ttu-id="ce964-147">1.01</span><span class="sxs-lookup"><span data-stu-id="ce964-147">1.01</span></span>       |
|<span data-ttu-id="ce964-148">Go</span><span class="sxs-lookup"><span data-stu-id="ce964-148">Go</span></span>         |<span data-ttu-id="ce964-149">1.7</span><span class="sxs-lookup"><span data-stu-id="ce964-149">1.7</span></span>        |
|<span data-ttu-id="ce964-150">Java</span><span class="sxs-lookup"><span data-stu-id="ce964-150">Java</span></span>       |<span data-ttu-id="ce964-151">1.8</span><span class="sxs-lookup"><span data-stu-id="ce964-151">1.8</span></span>        |
|<span data-ttu-id="ce964-152">Node.js</span><span class="sxs-lookup"><span data-stu-id="ce964-152">Node.js</span></span>    |<span data-ttu-id="ce964-153">6.9.4</span><span class="sxs-lookup"><span data-stu-id="ce964-153">6.9.4</span></span>      |
|<span data-ttu-id="ce964-154">Python</span><span class="sxs-lookup"><span data-stu-id="ce964-154">Python</span></span>     |<span data-ttu-id="ce964-155">2.7 和 3.5 (預設)</span><span class="sxs-lookup"><span data-stu-id="ce964-155">2.7 and 3.5 (default)</span></span>|

## <a name="secure-automatic-authentication"></a><span data-ttu-id="ce964-156">安全的自動驗證</span><span class="sxs-lookup"><span data-stu-id="ce964-156">Secure automatic authentication</span></span>
<span data-ttu-id="ce964-157">Cloud Shell 會安全地自動驗證 Azure CLI 2.0 的帳戶存取。</span><span class="sxs-lookup"><span data-stu-id="ce964-157">Cloud Shell securely and automatically authenticates account access for the Azure CLI 2.0.</span></span>

## <a name="azure-files-persistence"></a><span data-ttu-id="ce964-158">Azure 檔案持續性</span><span class="sxs-lookup"><span data-stu-id="ce964-158">Azure Files persistence</span></span>
<span data-ttu-id="ce964-159">因為 Cloud Shell 會依照要求而使用暫時電腦來配置，所以不會在工作階段之間保存位於您 $Home 外面的檔案和電腦狀態。</span><span class="sxs-lookup"><span data-stu-id="ce964-159">Since Cloud Shell is allocated on a per-request basis using a temporary machine, files outside of your $Home and machine state are not persisted across sessions.</span></span>
<span data-ttu-id="ce964-160">若要在工作階段之間保存檔案，Cloud Shell 會在第一次啟動時逐步引導您連結 Azure 檔案共用。</span><span class="sxs-lookup"><span data-stu-id="ce964-160">To persist files across sessions, Cloud Shell walks you through attaching an Azure file share on first launch.</span></span>
<span data-ttu-id="ce964-161">完成後，Cloud Shell 會自動連結儲存體，供所有未來的工作階段使用。</span><span class="sxs-lookup"><span data-stu-id="ce964-161">Once completed Cloud Shell will automatically attach your storage for all future sessions.</span></span>

[<span data-ttu-id="ce964-162">深入了解將 Azure 檔案共用連結至 Cloud Shell。</span><span class="sxs-lookup"><span data-stu-id="ce964-162">Learn more about attaching Azure file shares to Cloud Shell.</span></span>](persisting-shell-storage.md)

## <a name="next-steps"></a><span data-ttu-id="ce964-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ce964-163">Next steps</span></span>
[<span data-ttu-id="ce964-164">Cloud Shell 快速入門</span><span class="sxs-lookup"><span data-stu-id="ce964-164">Cloud Shell Quickstart</span></span>](quickstart.md) <br><span data-ttu-id="ce964-165">
[了解 Azure CLI 2.0](https://docs.microsoft.com/cli/azure/) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="ce964-165">
[Learn about Azure CLI 2.0](https://docs.microsoft.com/cli/azure/)</span></span> <br>