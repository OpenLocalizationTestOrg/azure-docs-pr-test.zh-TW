---
title: "aaaAzure 資料目錄版本資訊 |Microsoft 文件"
description: "Azure 資料目錄的版本資訊。"
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 3aca9c49-45a4-4352-92e6-bd25ee3eacf7
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 661826f66020ba72a885c6b14522b53c8b469d20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-release-notes"></a>Azure 資料目錄版本資訊
## <a name="notes-for-hello-november-20-2015-release-of-azure-data-catalog"></a>Hello 2015 年 11 月 20 日版本的 Azure 資料目錄資訊
### <a name="opening-data-sources-in-power-bi-desktop"></a>在 Power BI Desktop 中開啟資料來源
使用從 hello hello 」 開啟中 Power BI Desktop 」 選項時**Azure 資料目錄**入口網站中，使用者可能會遇到的其中一個 hello Power BI Desktop 的應用程式中的兩個問題：

* 會顯示 hello 標題 」 無法 tooOpen 文件 」 的對話方塊
* hello Power BI Desktop 的應用程式開啟，但 hello 檔案會出現空白 toobe

每種情況下，可以解決 hello 問題下載和安裝 hello 最新版本的 Power BI Desktop 從[PowerBI.com](https://powerbi.com)。

## <a name="notes-for-hello-november-13-2015-release-of-azure-data-catalog"></a>Hello 2015 年 11 月 13 日版本的 Azure 資料目錄資訊
### <a name="registering-and-connecting-tooteradata"></a>註冊及連接 tooTeradata
當連接 tooTeradata 資料來源的使用者必須已安裝 hello 正確的 Teradata ODBC 驅動程式符合 hello 的位元版本 （32 位元或 64 位元） 所使用的 hello 軟體。

為準，此 ADC 發行日期、 hello 最近[Teradata ODBC 驅動程式，適用於 windows （版本 15.10）](http://downloads.teradata.com/download/connectivity/odbc-driver/windows)相容使用 Office 2013，而非 Office 2016。

## <a name="notes-for-hello-july-13-2015-release-of-azure-data-catalog"></a>Hello 2015 年 7 月 13 日版本的 Azure 資料目錄資訊
### <a name="registering-and-connecting-toooracle-database"></a>註冊及連接 tooOracle 資料庫
當連接 tooOracle 資料庫資料來源的使用者必須已安裝 hello 正確 Oracle 驅動程式符合 hello 的位元版本 （32 位元或 64 位元） 所使用的 hello 軟體。

* 註冊時執行 32 位元 Windows 的電腦上的 Oracle 資料來源，將會使用 hello 32 位元 Oracle 驅動程式
* 註冊時執行 64 位元 Windows 的電腦上的 Oracle 資料來源，將會使用 hello 64 位元 Oracle 驅動程式
* 當連接 tooOracle 執行 hello 32 位元版本的 Microsoft Office 的電腦上使用 Excel 的資料來源，包括在 64 位元 Windows 上 hello 32 位元 Oracle 驅動程式會使用
* 當連線 tooOracle 執行 hello 64 位元版本的 Microsoft Office 的電腦上使用 Excel 的資料來源時，會使用 hello 64 位元 Oracle 驅動程式

### <a name="registering-and-connecting-toosql-server-reporting-services"></a>註冊及連接 tooSQL Server Reporting Services
目前有限制的 tooNative 模式伺服器只支援 SQL Server Reporting Services (SSRS) 的資料來源。 未來版本將加入在 SharePoint 模式中支援 SSRS。

### <a name="opening-data-assets-in-excel"></a>在 Excel 中開啟資料資產
從 hello 開啟 Microsoft Excel 中的資料資產時**Azure 資料目錄**入口網站中，使用者可能會提示您使用**Microsoft Excel 安全性注意事項** 對話方塊。 這是標準版，預期的行為，以及使用者可以選取**啟用**toocontinue。

如需詳細資訊，請參閱 [啟用或停用可疑網站之連結和檔案的安全性警告](https://support.office.com/article/Enable-or-disable-security-alerts-about-links-and-files-from-suspicious-websites-A1AC6AE9-5C4A-4EB3-B3F8-143336039BBE)。

### <a name="proxy-and-policy-configuration-and-data-source-registration"></a>Proxy 與原則設定及資料來源註冊
使用者可能會遇到的情況下，它們可以在其中記錄 toohello Azure 資料目錄入口網站，但當它們嘗試 toolog toohello 資料來源註冊工具遇到錯誤訊息，讓它們無法登入。

此問題行為有兩個可能的原因：

**原因 1: Active Directory Federation Services 設定**hello 資料來源註冊工具會使用表單驗證對 Active Directory toovalidate 使用者登入。 成功的登入表單驗證必須啟用 hello 全域驗證原則中的 Active Directory 系統管理員。

在某些情況下，只有當 hello 使用者位於 hello 公司網路，或是只 hello 使用者從外部 hello 公司網路連線，可能會發生此錯誤行為。 hello 全域驗證原則可以讓驗證方法 toobe 分別啟用內部網路和外部網路的連線。 如果使用者連線從哪些 hello hello 網路不啟用表單驗證，可能會發生登入錯誤。

如需詳細資訊，請參閱 [設定驗證原則](https://technet.microsoft.com/library/dn486781.aspx)。

**原因 2： 網路 proxy 設定**hello 註冊工具如果 hello 公司網路使用 proxy 伺服器，可能無法透過 hello proxy 可以 tooconnect tooAzure Active Directory。 使用者可以確保該 hello 註冊工具藉由編輯 hello 工具的組態檔，會加入此節 toohello 檔案：

      <system.net>
        <defaultProxy useDefaultCredentials="true" enabled="true">
          <proxy usesystemdefault="True"
                          proxyaddress="http://<your corporate network proxy url>"
                          bypassonlocal="True"/>
        </defaultProxy>
      </system.net>


toolocate hello RegistrationTool.exe.config 檔案，啟動 hello 註冊工具，然後再開啟 hello Windows 工作管理員公用程式。 Hello 詳細資料 索引標籤上 工作管理員中，以滑鼠右鍵按一下 RegistrationTool.exe 和從 hello 快顯功能表中選擇 開啟檔案位置。
