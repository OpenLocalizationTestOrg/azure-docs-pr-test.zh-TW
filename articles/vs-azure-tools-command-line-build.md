---
title: "azure aaaCommand 行組建 |Microsoft 文件"
description: "Azure 的命令列建置"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 94b35d0d-0d35-48b6-b48b-3641377867fd
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/05/2017
ms.author: kraigb
ms.openlocfilehash: 295b61ba162dd4373ee3f56cc1462decb3e16762
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="building-azure-projects-from-hello-command-line"></a><span data-ttu-id="49430-103">建置 Azure 專案，從 hello 命令列</span><span class="sxs-lookup"><span data-stu-id="49430-103">Building Azure projects from hello command line</span></span>
<span data-ttu-id="49430-104">您可以使用 hello Microsoft Build Engine (MSBuild)，來建立但尚未安裝 Visual Studio 的組建實驗室環境中的產品。</span><span class="sxs-lookup"><span data-stu-id="49430-104">Using hello Microsoft Build Engine (MSBuild), you can build products in build-lab environments where Visual Studio is not installed.</span></span> <span data-ttu-id="49430-105">MSBuild 的專案檔案會採用可擴充且 Microsoft 完全支援的 XML 格式。</span><span class="sxs-lookup"><span data-stu-id="49430-105">MSBuild uses an XML format for project files that's extensible and fully supported by Microsoft.</span></span> <span data-ttu-id="49430-106">使用 hello MSBuild 檔案格式，您可以描述項目必須是針對一個或多個平台和組態建置。</span><span class="sxs-lookup"><span data-stu-id="49430-106">Using hello MSBuild file format, you can describe what items must be built for one or more platforms and configurations.</span></span>

<span data-ttu-id="49430-107">您也可以在 hello 命令列執行 MSBuild，本主題將描述這個方法。</span><span class="sxs-lookup"><span data-stu-id="49430-107">You can also run MSBuild at hello command line, and this topic describes that approach.</span></span> <span data-ttu-id="49430-108">Hello 命令列上設定屬性，您可以建置特定專案的組態。</span><span class="sxs-lookup"><span data-stu-id="49430-108">By setting properties on hello command line, you can build specific configurations of a project.</span></span> <span data-ttu-id="49430-109">同樣地，您也可以定義 MSBuild 仍會建置的 hello 目標。</span><span class="sxs-lookup"><span data-stu-id="49430-109">Similarly, you can also define hello targets that MSBuild builds.</span></span> <span data-ttu-id="49430-110">如需有關命令列參數及 MSBuild 的詳細資訊，請參閱 [MSBuild 命令列參考](https://msdn.microsoft.com/library/ms164311.aspx)。</span><span class="sxs-lookup"><span data-stu-id="49430-110">For more information about command-line parameters and MSBuild, see [MSBuild Command-Line Reference](https://msdn.microsoft.com/library/ms164311.aspx).</span></span>

## <a name="msbuild-parameters"></a><span data-ttu-id="49430-111">MSBuild 參數</span><span class="sxs-lookup"><span data-stu-id="49430-111">MSBuild parameters</span></span>
<span data-ttu-id="49430-112">最簡單方式 toocreate hello 封裝是以 hello toorun MSBuild`/t:Publish`選項。</span><span class="sxs-lookup"><span data-stu-id="49430-112">hello simplest way toocreate a package is toorun MSBuild with hello `/t:Publish` option.</span></span> <span data-ttu-id="49430-113">根據預設，此命令會建立一個目錄關聯 toohello 根 hello 專案資料夾，例如`<ProjectDirectory>\bin\Configuration\app.publish\`。</span><span class="sxs-lookup"><span data-stu-id="49430-113">By default, this command creates a directory in relation toohello root folder for hello project, such as `<ProjectDirectory>\bin\Configuration\app.publish\`.</span></span> <span data-ttu-id="49430-114">當您建置 Azure 專案時，會產生兩個檔案： hello 封裝檔本身和 hello 伴隨的組態檔：</span><span class="sxs-lookup"><span data-stu-id="49430-114">When you build an Azure project, two files are generated: hello package file itself and hello accompanying configuration file:</span></span>

* <span data-ttu-id="49430-115">套件檔案 (`project.cspkg`)</span><span class="sxs-lookup"><span data-stu-id="49430-115">Package File (`project.cspkg`)</span></span>
* <span data-ttu-id="49430-116">組態檔 (`ServiceConfiguration.TargetProfile.cscfg`)</span><span class="sxs-lookup"><span data-stu-id="49430-116">Configuration File (`ServiceConfiguration.TargetProfile.cscfg`)</span></span>

<span data-ttu-id="49430-117">每個 Azure 專案預設都會包含一個供本機 (偵錯) 組建使用的服務組態檔，以及另一個供雲端 (預備或生產環境) 組建使用的服務組態檔。</span><span class="sxs-lookup"><span data-stu-id="49430-117">By default, each Azure project includes one service-configuration file for local (debugging) builds and another for cloud (staging or production) builds.</span></span> <span data-ttu-id="49430-118">不過，您可以視需要新增或移除服務組態檔。</span><span class="sxs-lookup"><span data-stu-id="49430-118">However, you can add or remove service-configuration files as needed.</span></span> <span data-ttu-id="49430-119">當您建置 Visual Studio 中的封裝時，會要求您的服務組態檔 tooinclude，連同 hello 封裝。</span><span class="sxs-lookup"><span data-stu-id="49430-119">When you build a package within Visual Studio, you are asked which service-configuration file tooinclude alongside hello package.</span></span> <span data-ttu-id="49430-120">當您使用 MSBuild 建置封裝時，預設會包含 hello 本機服務組態檔。</span><span class="sxs-lookup"><span data-stu-id="49430-120">When you build a package by using MSBuild, hello local service-configuration file is included by default.</span></span> <span data-ttu-id="49430-121">tooinclude 不同的服務組態檔，設定 hello `TargetProfile` hello MSBuild 命令的屬性 (`MSBuild /t:Publish /p:TargetProfile=ProfileName`)。</span><span class="sxs-lookup"><span data-stu-id="49430-121">tooinclude a different service-configuration file, set hello `TargetProfile` property of hello MSBuild command (`MSBuild /t:Publish /p:TargetProfile=ProfileName`).</span></span>

<span data-ttu-id="49430-122">如果您想 toouse hello 替代目錄儲存封裝和組態檔，設定 hello 路徑使用 hello`/p:PublishDir=Directory\`選項，包括尾端的反斜線分隔的 hello。</span><span class="sxs-lookup"><span data-stu-id="49430-122">If you want toouse an alternate directory for hello stored package and configuration files, set hello path by using hello `/p:PublishDir=Directory\` option, including hello trailing backslash separator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="49430-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="49430-123">Next steps</span></span>
<span data-ttu-id="49430-124">建立 hello 封裝之後，您可以部署它 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="49430-124">After hello package is built, you can deploy it tooAzure.</span></span> <span data-ttu-id="49430-125">如需教學課程示範如何 tooautomate 處理，請參閱[Azure 雲端服務的持續傳遞](./cloud-services/cloud-services-dotnet-continuous-delivery.md)。</span><span class="sxs-lookup"><span data-stu-id="49430-125">For a tutorial that demonstrates how tooautomate that process, see [Continuous Delivery for Cloud Services in Azure](./cloud-services/cloud-services-dotnet-continuous-delivery.md).</span></span>

