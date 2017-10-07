---
title: "aaaAzure SDK for.NET 2.9 版本資訊"
description: "Azure SDK for .NET 2.9 版本資訊"
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: c83d815b-fc19-4260-821e-7d2a7206dffc
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: 96df2b80224190cc2093e6bf350eaec224ac2e98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-29-release-notes"></a>Azure SDK for .NET 2.9 版本資訊

本主題包含 Azure SDK for .NET 2.9 和 2.9.6 版的版本資訊。

##<a name="azure-sdk-for-net-296-release-summary"></a>Azure SDK for .NET 2.9.6 發行摘要

發行日期︰2016/11/16
 
在此版本中引進了沒有重大變更 toohello Azure SDK 2.9 中。 沒有也需要升級的程序 tooleverage 此 SDK 與現有的雲端服務專案。

### <a name="visual-studio-2017-release-candidate"></a>Visual Studio 2017 候選版

- 在 Visual Studio 2017 RC 中，這一版的 hello Azure SDK for.NET 是內建在 hello Azure 工作負載。 Toodo Azure 開發所需的所有 hello 工具將會都是 Visual Studio 2017 RC 往後的一部分。 Visual Studio 2015 和 Visual Studio 2013，hello SDK 仍可透過 WebPI。 當 Visual Studio 2017 以最終產品發行時，我們就不再提供適用於 Visual Studio 2013 的 Azure SDK for .NET 版本。 請依照此連結 toodownload Visual Studio 2017 RC: https://www.visualstudio.com/vs/visual-studio-2017-rc/

### <a name="azure-diagnostics"></a>Azure 診斷

- 已變更的 hello 行為 tooonly 儲存部分連接字串與 hello 索引鍵的雲端服務診斷儲存體連接字串語彙基元所取代。 hello 實際的儲存體金鑰現在會儲存在 hello 使用者設定檔資料夾，所以可以控制其存取權。 Visual Studio 會從本機偵錯和發行程序的使用者設定檔資料夾讀取 hello 儲存體金鑰。 
- 在回應 toohello 變更上面所述，Visual Studio Online team 增強的 hello Azure 雲端服務部署工作範本讓使用者可以指定發佈 tooAzure 連續整合時，設定診斷延伸模組的 hello 儲存體金鑰與部署。
- 我們已經可能 toostore 安全的連接字串和 token 化的 Azure 診斷 (WAD)，toohelp 您跨 environements 解決組態問題。
 
### <a name="windows-server-2016-virtual-machines"></a>Windows Server 2016 虛擬機器

- Visual Studio 現在支援部署雲端服務 tooOS 系列 5 (Windows Server 2016) 的虛擬機器。 對於現有的雲端服務，您可以變更設定 tootarget hello 新的 OS 系列。 在建立新的雲端服務，如果您選擇使用.net 4.6 或更高的 toocreate hello 服務時，它將預設 hello 服務 toouse OS 系列 5。  如需詳細資訊，您可以檢閱 hello[客體作業系統系列支援資料表](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/)。

#### <a name="known-issues"></a>已知問題

- Azure.NET SDK 2.9.6 引入的限制，會封鎖部署的專案使用不支援的.NET 架構 （例如.NET 4.6) tooany OS 系列 < 5。 因應措施提供於[這裡](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9)。

 
### <a name="azure-in-role-cache"></a>Azure In-Role Cache 

- 2016 年 11 月 30 日終止支援 Azure In-Role Cache。 如需詳細資訊，請按一下[這裡](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/)。

### <a name="azure-resource-manager-templates-for-azure-stack"></a>適用於 Azure Stack 的 Azure Resource Manager 範本

- 我們已引進 Azure Stack 做為 Azure Resource Manager 範本的部署目標。


## <a name="azure-sdk-for-net-29-summary"></a>Azure SDK for .NET 2.9 摘要

## <a name="overview"></a>概觀
本文件包含 hello hello Azure SDK for.NET 2.9 版的版本資訊。 

如需此版本中更新的詳細資訊，請參閱 hello [Azure SDK 2.9 公告文章](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/)。

## <a name="azure-sdk-29-for-visual-studio-2015-update-2-and-visual-studio-15-preview"></a>Azure SDK 2.9 for Visual Studio 2015 Update 2 和 Visual Studio "15" 預覽
此更新包含下列錯誤修正 hello:

* 發出相關的 tooREST API 產生用戶端中的 hello 字串中 「 未知的型別 」 會顯示成 hello hello 產生程式碼資料夾名稱和/或 hello hello 放入 hello 產生程式碼的命名空間名稱。
* 發出的驗證資訊失敗 toobe 傳遞 toohello 排程器佈建程序中的 hello 相關的 tooScheduled WebJobs。

此更新包含下列新功能的 hello:

* Hello App Service 佈建對話方塊 hello 「 服務 」 索引標籤中的第二個應用程式服務的支援。 

## <a name="azure-data-lake-tools-for-visual-studio-2015-update-2"></a>Azure Data Lake Tools for Visual Studio 2015 Update 2
此更新包含下列 hello:

* **Azure Data Lake Tools** Visual Studio 現在合併成 hello Azure SDK for.NET 版本。 當您安裝 Azure SDK，hello 工具會自動安裝。 
  
    hello 工具經常更新，請移[這裡](http://aka.ms/datalaketool)tooget hello 更新。
* **伺服器總管**現在可讓您 tooview 所有，並建立一些 U-SQL 中繼資料實體。 如需詳細資訊，請參閱 [此部落格](https://azure.microsoft.com/documentation/services/data-lake-analytics/) 。

## <a name="hdinsight-tools"></a>HDInsight 工具
**HDInsight Tools** for Visual Studio 現在支援 HDInsight 3.3 版，包括顯示 Tez 圖形和其他語言修正。

## <a name="azure-resource-manager"></a>Azure Resource Manager
此版本為 Resource Manager 範本新增[金鑰保存庫](../azure-resource-manager/resource-manager-keyvault-parameter.md)支援。

## <a name="see-also"></a>另請參閱
[Azure SDK 2.9 公告文章](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/)

