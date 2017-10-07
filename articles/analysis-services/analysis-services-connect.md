---
title: "aaaConnect tooAzure Analysis Services |Microsoft 文件"
description: "了解 tooconnect tooand 從 Azure 中的 Analysis Services 伺服器所取得的資料。"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: b37f70a0-9166-4173-932d-935d769539d1
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 5df94492feb48034f156b72e83e1009683988fc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-azure-analysis-services-server"></a>Tooan Azure Analysis Services 伺服器連接

本文說明連線的 tooa 伺服器使用的資料模型化和管理應用程式，例如 SQL Server Management Studio (SSMS) 或 SQL Server Data Tools (SSDT)。 或是使用用戶端報表應用程式，例如 Microsoft Excel、Power BI Desktop 或自訂應用程式。 連線 tooAzure Analysis Services 會使用 HTTPS。

## <a name="client-libraries"></a>用戶端程式庫
[取得最新用戶端程式庫 hello](analysis-services-data-providers.md)

所有的連線 tooa 伺服器，不論類型為何，都需要更新 AMO、 ADOMD.NET 和 OLEDB 用戶端程式庫 tooconnect tooand 介面與 Analysis Services 伺服器。 SSMS、 SSDT、 Excel 2016 和 Power BI，hello 最新的用戶端程式庫會安裝或更新與每月發行版本。 不過，在某些情況下，可能會應用程式可能沒有 hello 最新版本。 例如，當更新原則延遲時，Office 365 更新上或位於 hello 延後的通道。

## <a name="server-name"></a>伺服器名稱

當您在 Azure 中建立 Analysis Services 伺服器時，您可以指定其中 hello 伺服器是 toobe 建立的唯一名稱和 hello 區域。 指定在連接中的 hello 伺服器名稱，hello 伺服器命名配置時：

```
<protocol>://<region>/<servername>
```
 其中通訊協定是字串**asazure**，區域是 hello hello 伺服器建立所在的 Uri (例如，westus.asazure.windows.net) 並為您 hello 區域內的唯一伺服器 hello 名稱。

### <a name="get-hello-server-name"></a>取得 hello 伺服器名稱
在**Azure 入口網站**> 伺服器 >**概觀** > **伺服器名稱**，複製 hello 整部伺服器的名稱。 如果您的組織中的其他使用者要太連接 toothis 伺服器，您可以在與其共用此伺服器名稱。 當指定伺服器名稱，就必須使用 hello 完整路徑。

![在 Azure 中取得伺服器名稱](./media/analysis-services-deploy/aas-deploy-get-server-name.png)


## <a name="connection-string"></a>連接字串

連接 tooAzure 時使用的 Analysis Services hello 表格式物件模型中，使用下列連接字串格式的 hello:

###### <a name="integrated-azure-active-directory-authentication"></a>整合型 Azure Active Directory 驗證
整合式的驗證來收取 hello Azure Active Directory 認證快取，如果有的話。 如果沒有，則顯示 hello Azure 登入視窗。

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;"
```


###### <a name="azure-active-directory-authentication-with-username-and-password"></a>以使用者名稱與密碼進行的 Azure Active Directory 驗證

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>;User ID=<user name>;Password=<password>;Persist Security Info=True; Impersonation Level=Impersonate;";
```

###### <a name="windows-authentication-integrated-security"></a>Windows 驗證 (整合式安全性)
使用 hello hello 目前處理序執行的 Windows 帳戶。

```
"Provider=MSOLAP;Data Source=<Azure AS instance name>; Integrated Security=SSPI;Persist Security Info=True;"
```



## <a name="connect-using-an-odc-file"></a>使用 .odc 檔案進行連接
與舊版的 Excel 中，使用者可以連線 tooan Azure Analysis Services 伺服器，使用 Office 資料連線 (.odc) 檔案。 詳細資訊，請參閱 toolearn[建立 Office 資料連線 (.odc) 檔案](analysis-services-odc.md)。


## <a name="next-steps"></a>後續步驟
[使用 Excel 進行連接](analysis-services-connect-excel.md)    
[使用 Power BI 進行連接](analysis-services-connect-pbi.md)   
[管理您的伺服器](analysis-services-manage.md)   

