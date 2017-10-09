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
# <a name="building-azure-projects-from-hello-command-line"></a>建置 Azure 專案，從 hello 命令列
您可以使用 hello Microsoft Build Engine (MSBuild)，來建立但尚未安裝 Visual Studio 的組建實驗室環境中的產品。 MSBuild 的專案檔案會採用可擴充且 Microsoft 完全支援的 XML 格式。 使用 hello MSBuild 檔案格式，您可以描述項目必須是針對一個或多個平台和組態建置。

您也可以在 hello 命令列執行 MSBuild，本主題將描述這個方法。 Hello 命令列上設定屬性，您可以建置特定專案的組態。 同樣地，您也可以定義 MSBuild 仍會建置的 hello 目標。 如需有關命令列參數及 MSBuild 的詳細資訊，請參閱 [MSBuild 命令列參考](https://msdn.microsoft.com/library/ms164311.aspx)。

## <a name="msbuild-parameters"></a>MSBuild 參數
最簡單方式 toocreate hello 封裝是以 hello toorun MSBuild`/t:Publish`選項。 根據預設，此命令會建立一個目錄關聯 toohello 根 hello 專案資料夾，例如`<ProjectDirectory>\bin\Configuration\app.publish\`。 當您建置 Azure 專案時，會產生兩個檔案： hello 封裝檔本身和 hello 伴隨的組態檔：

* 套件檔案 (`project.cspkg`)
* 組態檔 (`ServiceConfiguration.TargetProfile.cscfg`)

每個 Azure 專案預設都會包含一個供本機 (偵錯) 組建使用的服務組態檔，以及另一個供雲端 (預備或生產環境) 組建使用的服務組態檔。 不過，您可以視需要新增或移除服務組態檔。 當您建置 Visual Studio 中的封裝時，會要求您的服務組態檔 tooinclude，連同 hello 封裝。 當您使用 MSBuild 建置封裝時，預設會包含 hello 本機服務組態檔。 tooinclude 不同的服務組態檔，設定 hello `TargetProfile` hello MSBuild 命令的屬性 (`MSBuild /t:Publish /p:TargetProfile=ProfileName`)。

如果您想 toouse hello 替代目錄儲存封裝和組態檔，設定 hello 路徑使用 hello`/p:PublishDir=Directory\`選項，包括尾端的反斜線分隔的 hello。

## <a name="next-steps"></a>後續步驟
建立 hello 封裝之後，您可以部署它 tooAzure。 如需教學課程示範如何 tooautomate 處理，請參閱[Azure 雲端服務的持續傳遞](./cloud-services/cloud-services-dotnet-continuous-delivery.md)。

