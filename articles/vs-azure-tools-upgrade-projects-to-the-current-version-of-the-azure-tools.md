---
title: "aaaHow tooupgrade 專案 toohello 目前版本的 hello Azure tools |Microsoft 文件"
description: "了解如何 tooupgrade Azure 專案的 Visual Studio toohello 目前版本的 hello Azure tools"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1d64070a-078d-468a-87f4-e6715de6475f
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: c89ba43af0f2fd9db46ce0c90f0da3d70dc1510b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupgrade-projects-toohello-current-version-of-hello-azure-tools-for-visual-studio"></a>Tooupgrade 專案 toohello 最新版 hello Azure Tools for Visual Studio 的方式
## <a name="overview"></a>概觀
使用 Azure Tools 所建立的任何專案安裝 hello hello Azure Tools （或之前的版本比 1.6 版本更新） 的目前版本之後，早於 1.6 版 (11 月版 2011) 將會自動升級在您開啟。 如果您使用建立專案 hello 1.6 (11 月版 2011) 版本的工具和您仍然必須安裝該版本，您可以在 hello 較舊版本中開啟這些專案，並在稍後決定是否 tooupgrade 它們。

## <a name="how-your-project-changes-when-you-upgrade-it"></a>專案升級時有何變更
如果專案會自動升級，或者您指定您要它，您的專案是的 tooupgrade 修改 toowork 與目前版本的特定組件，和某些屬性也會變更，如本節所述。 如果您的專案需要其他變更 toobe 相容 hello 工具 hello 較新版本，您必須手動進行這些變更。

* hello web.config 檔案的 web 角色和背景工作角色的 hello app.config 檔案會更新的 tooreference hello 較新版的 Microsoft.WindowsAzure.Diagnostics.DiagnosticMonitoirTraceListener.dll。
* hello Microsoft.WindowsAzure.StorageClient.dll、 Microsoft.WindowsAzure.Diagnostics.dll 和 microsoft.windowsazure.serviceruntime.dll 等組件會升級的 toohello 新版本。
* 儲存在 hello Azure 專案檔 (.ccproj) 中的發行設定檔會移動的 tooa 個別檔案，與 hello 副檔名為.azurePubXml 且位於 hello**發行**子目錄。
* Hello 中的某些屬性將發行設定檔的更新的 toosupport 新增和變更功能。 **AllowUpgrade** 會取代為 **DeploymentReplacementMethod**，因為您可以同時或以累加方式更新已部署的雲端服務。
* hello 屬性**UseIISExpressByDefault**加入並設定 toofalse hello 用來偵錯的網頁伺服器將不會自動將變更網際網路資訊服務 (IIS) tooIIS Express。 IIS Express 是 hello 與 hello 工具 hello 較新版本所建立專案的預設 web 伺服器。
* Azure 快取裝載在一或多個專案的角色，如果升級專案時，會變更 hello 服務組態 （.cscfg 檔） 和服務定義 （.csdef 檔） 中的某些屬性。 如果 hello 專案使用 hello Azure Caching NuGet 封裝，hello 專案是升級的 toohello hello 封裝最新版本。 您應該開啟 hello web.config 檔案，並確認 hello 用戶端組態已 hello 升級程序期間適當維護。 如果您沒有使用 hello NuGet 套件加入 hello 參考 tooAzure Caching 用戶端組件，這些組件不會更新。您必須手動更新這些參考 toohello 新版本。

> [!IMPORTANT]
> F # 專案，您必須手動更新參考 tooAzure 組件，使其參考這些組件的 hello 較新版本。
> 
> 

### <a name="how-tooupgrade-an-azure-project-toohello-current-release"></a>如何 tooupgrade Azure 專案 toohello 目前版本
1. 安裝 hello 目前版本的 Visual Studio 的 hello 安裝到 hello Azure Tools 的 toouse hello 升級專案，以及您想 tooupgrade hello 然後開啟專案。 如果使用 Azure Tools 所建立 hello 專案早於 1.6 版 (2011 年 11 月)，hello 專案會自動升級的 toohello 目前版本。 如果 hello 專案已建立 hello 2011 年 11 月發行的仍安裝的版本，hello 專案會開啟該版本。
2. 在 方案總管 中，開啟 hello hello 的專案節點的捷徑功能表選擇 **屬性**，然後選擇 hello**應用程式**hello 會出現對話方塊索引標籤。
   
    hello**應用程式**索引標籤會顯示 hello 與 hello 專案相關聯的工具版本。 如果出現 hello 目前版本的 Azure Tools，已經升級 hello 專案。 如果您已安裝較新版的 hello 工具哪些 hello 索引標籤會顯示，比**升級**按鈕隨即顯示。
3. 選擇 hello**升級**按鈕 tooupgrade hello tools 專案 toohello 目前版本。
4. 建置 hello 專案，然後處理 API 變更而造成的任何錯誤。 如需如何 toomodify 您的程式碼 hello 新版本，請參閱 hello 文件 hello 特定 API。

