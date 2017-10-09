---
title: "aaaUse 網站中的 ReportViewer |Microsoft 文件"
description: "本主題描述如何 toobuild Microsoft Azure Web 網站會顯示報表的 hello Visual Studio ReportViewer 控制項一起儲存在 Microsoft Azure 虛擬機器。"
services: virtual-machines-windows
documentationcenter: na
author: guyinacube
manager: erikre
editor: monicar
tags: azure-service-management
ms.assetid: 78b76318-d9bf-48ef-9d9e-d1b7d8cf3042
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/11/2017
ms.author: asaxton
ms.openlocfilehash: 8e0729d6657f96c32a9ac7dffdff7745ff92b48d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-reportviewer-in-a-web-site-hosted-in-azure"></a>在裝載於 Azure 上的網站中使用 ReportViewer
> [!IMPORTANT] 
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../azure-resource-manager/resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。

您可以建立 Microsoft Azure 網站以 hello Visual Studio ReportViewer 控制項，會顯示報表，儲存在 Microsoft Azure 虛擬機器。 hello ReportViewer 控制項是 Web 應用程式中，建立使用 hello ASP.NET Web 應用程式範本。

> [!IMPORTANT]
> hello ASP.NET MVC Web 應用程式範本不支援 hello ReportViewer 控制項。

tooincorporate ReportViewer 您 Microsoft Azure 網站中的，您需要 toocomplete hello 下列工作。

* **新增**組件 toohello 部署套件
* **設定** 驗證和授權
* **發行**hello ASP.NET Web 應用程式 tooAzure

## <a name="prerequisites"></a>必要條件
檢閱中的 hello 「 一般建議和最佳作法 」 一節[Azure 虛擬機器中 SQL Server Business Intelligence](../classic/ps-sql-bi.md)。

> [!NOTE]
> ReportViewer 控制項隨附於 Visual Studio (Standard Edition 以上版本) 中。 如果您使用 hello Web Developer Express 版，您必須安裝 hello [MICROSOFT REPORT VIEWER 2012 RUNTIME](https://www.microsoft.com/download/details.aspx?id=35747) toouse hello ReportViewer 執行階段功能。
> 
> Microsoft Azure 不支援在本機處理模式中設定的 ReportViewer。

## <a name="adding-assemblies-toohello-deployment-package"></a>加入組件 toohello 部署套件
當您裝載 ASP.NET 應用程式在內部時，hello ReportViewer 組件通常會直接在 hello IIS 伺服器的 hello 全域組件快取 (GAC) 中安裝 Visual Studio 安裝期間，並且 hello 應用程式可以直接存取。 不過，當您的主機在 hello 雲端中，Microsoft Azure ASP.NET 應用程式不允許任何項目 toobe 安裝到 hello GAC，因此您必須確定 hello ReportViewer 組件可在本機上提供您的應用程式。 您可以將您的專案中參考 toothem 達到此目的，及設定這些 toobe 在本機複製。

在遠端處理模式中，hello ReportViewer 控制項，請使用下列組件的 hello:

* **Microsoft.ReportViewer.WebForms.dll**： 包含 hello ReportViewer 程式碼，您必須在頁面中 toouse ReportViewer。 當您將 ReportViewer 控制項拖曳到 ASP.NET 頁面放入您的專案時，這個組件的參考會加入 tooyour 專案。
* **Microsoft.ReportViewer.Common.dll**： 包含在執行階段 hello ReportViewer 控制項所使用的類別。 它不會自動加入 tooyour 專案。

### <a name="tooadd-a-reference-toomicrosoftreportviewercommon"></a>tooadd 參考 tooMicrosoft.ReportViewer.Common
* 以滑鼠右鍵按一下您的專案**參考**節點，然後選取**加入參考**，選取 hello 組件以 hello.NET 索引標籤，然後按一下**確定**。

### <a name="toomake-hello-assemblies-locally-accessible-by-your-aspnet-application"></a>在本機上存取您的 ASP.NET 應用程式的 toomake hello 組件
1. 在 [hello**參考**資料夾中，按一下 hello Microsoft.ReportViewer.Common 組件，如此其屬性會顯示 hello 屬性] 窗格中。
2. 在 [hello] 內容窗格中，設定**複製到本機**tooTrue。
3. 對 Microsoft.ReportViewer.WebForms 重複步驟 1 和 2。

### <a name="tooget-reportviewer-language-pack"></a>tooget ReportViewer 語言套件
1. 安裝 hello 適當 Microsoft Report Viewer 2012 Runtime 可轉散發套件從[Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=317386)。
2. 從下拉式清單中 hello 和 hello 頁面選取 hello 語言取得重新導向的 toohello 對應的下載中心頁面。
3. 按一下**下載**toostart hello 下載 ReportViewerLP.exe。
4. 下載 ReportViewerLP.exe 之後，請按一下**執行**tooinstall 立即，或按一下**儲存**toosave 它 tooyour 電腦。 如果您按一下**儲存**，請記住 hello hello 儲存 hello 檔案的資料夾名稱。
5. 找出 hello 資料夾儲存 hello 檔案的位置。 在 ReportViewerLP.exe 上按一下滑鼠右鍵，按一下 以系統管理員身分執行，然後按一下是。
6. 執行 ReportViewerLP.exe 之後，您會看到 hello c:\windows\assembly 具有 hello 資源檔**Microsoft.ReportViewer.Webforms.Resources**和**Microsoft.ReportViewer.Common.Resources**.

### <a name="tooconfigure-for-localized-reportviewer-control"></a>tooconfigure 當地語系化的 ReportViewer 控制項
1. 下載並安裝下列 hello 上面指定的指示由 hello Microsoft Report Viewer 2012 Runtime 可轉散發套件。
2. 建立<language>hello 專案和複製 hello 資料夾相關聯的資源組件檔案。 hello 複製的資源組件檔案 toobe 是： **Microsoft.ReportViewer.Webforms.Resources.dll**和**Microsoft.ReportViewer.Common.Resources.dll**。選取 hello 資源組件檔案，然後在 [hello] 內容窗格中，設定**複製 tooOutput 目錄**太"**永遠複製**"。
3. 設定 hello hello web 專案的 Culture 和 UICulture。 如需有關如何 tooset hello 文化特性和 UI 文化特性的 ASP.NET Web 網頁，請參閱[How to： 設定 ASP.NET Web 網頁全球化 hello 文化特性和 UI 文化特性](http://go.microsoft.com/fwlink/?LinkId=237461)。

## <a name="configuring-authentication-and-authorization"></a>設定驗證和授權
hello ReportViewer 需要 toouse 適當的認證 tooauthenticate 與 hello 報表伺服器，並 hello 認證必須經過 hello report server tooaccess hello 報表您想要授權。 如需驗證資訊，請參閱 hello 白皮書[Reporting Services 報表檢視器控制項和 Microsoft Azure 虛擬機器為基礎的報表伺服器](https://msdn.microsoft.com/library/azure/dn753698.aspx)。

## <a name="publish-hello-aspnet-web-application-tooazure"></a>發佈 ASP.NET Web 應用程式 tooAzure hello
如需發佈 ASP.NET Web 應用程式 tooAzure 指示，請參閱[How to： 移轉並發行從 Visual Studio Web 應用程式 tooAzure](../../../vs-azure-tools-migrate-publish-web-app-to-cloud-service.md)和[開始使用 Web 應用程式和 ASP.NET](../../../app-service-web/app-service-web-get-started-dotnet.md)。

> [!IMPORTANT]
> 如果 hello 加入 Azure 部署專案或加入 Azure 雲端服務專案命令沒有出現在方案總管 中的 hello 快顯功能表中，您可能需要 toochange hello 目標 framework 的 hello 專案 too.NET Framework 4。
> 
> hello 兩個命令提供本質上 hello 相同的功能。 一或 hello 其他命令會出現在 hello 快顯功能表中的 hello Microsoft Azure SDK 版本而定，您已安裝。
> 
> 

## <a name="resources"></a>資源
[Microsoft 報告](http://go.microsoft.com/fwlink/?LinkId=205399)

[Azure 虛擬機器中的 SQL Server Business Intelligence](../classic/ps-sql-bi.md)

[使用 PowerShell tooCreate Azure VM 具有原生模式報表伺服器](../classic/ps-sql-report.md)

