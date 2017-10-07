---
title: "aaaAzure SDK for.NET 3.0 版本資訊 |Microsoft 文件"
description: "Azure SDK for .NET 3.0 版本資訊"
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
ms.date: 03/07/2017
ms.author: juliako
ms.openlocfilehash: 8970b4c9b64de40dc29a33d69006a00ae5e38a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-30-release-notes"></a>Azure SDK for .NET 3.0 版本資訊

本主題包含適用於.NET 的 3.0 版的 hello Azure SDK 版本資訊。

##<a name="azure-sdk-for-net-30-release-summary"></a>Azure SDK for .NET 3.0 發行摘要

發行日期︰2017/03/07
 
在此版本中引進了沒有重大變更 toohello Azure SDK 3.0。 沒有也需要升級的程序 tooleverage 此 SDK 與現有的雲端服務專案。 tooallow 使用 hello Azure SDK 3.0 而不需要升級程序，Azure SDK 3.0 安裝 toohello 為 Azure SDK 2.9 中相同的目錄。 大部分的 hello 元件並未從 2.9 變更 hello 主要版本，但改為更新 hello 組建編號。

## <a name="visual-studio-2017-rtw"></a>Visual Studio 2017 RTW

- 在 Visual Studio 2017，這一版的 hello Azure SDK for.NET 內建 toohello Azure 工作負載。 Toodo Azure 開發所需的所有 hello 工具將會都是 Visual Studio 2017 往後的一部分。 Visual Studio 2015 的 hello SDK 仍可透過 WebPI。 現在既然已釋出 Visual Studio 2017，我們已不再提供 Visual Studio 2013 適用的 Azure SDK .NET 版本。

### <a name="azure-diagnostics"></a>Azure 診斷

- 已變更的 hello 行為 tooonly 儲存部分連接字串與 hello 索引鍵的雲端服務診斷儲存體連接字串語彙基元所取代。 hello 實際的儲存體金鑰現在會儲存在 hello 使用者設定檔資料夾，所以可以控制其存取權。 Visual Studio 會從本機偵錯和發行程序的使用者設定檔資料夾讀取 hello 儲存體金鑰。 
- 在回應 toohello 變更上面所述，Visual Studio Online team 增強的 hello Azure 雲端服務部署工作範本讓使用者可以指定發佈 tooAzure 連續整合時，設定診斷延伸模組的 hello 儲存體金鑰與部署。
- 我們已經可能 toostore 安全的連接字串和 token 化的 Azure 診斷 (WAD)，toohelp 您跨 environements 解決組態問題。
 
### <a name="windows-server-2016-virtual-machines"></a>Windows Server 2016 虛擬機器

- Visual Studio 現在支援部署雲端服務 tooOS 系列 5 (Windows Server 2016) 的虛擬機器。 對於現有的雲端服務，您可以變更設定 tootarget hello 新的 OS 系列。 在建立新的雲端服務，如果您選擇使用.net 4.6 或更高的 toocreate hello 服務時，它將預設 hello 服務 toouse OS 系列 5。  如需詳細資訊，您可以檢閱 hello[客體作業系統系列支援資料表](../cloud-services/cloud-services-guestos-update-matrix.md)。

### <a name="known-issues"></a>已知問題

- Azure .NET SDK 3.0 中造成了在 Visual Studio 2015 的並存組態中移除 Visual Studio 2017 時的問題。  如果您擁有 hello Azure SDK for Visual Studio 2015 安裝，hello Microsoft Azure 儲存體模擬器與 Microsoft Azure 計算模擬器將會移除當您解除安裝 Visual Studio 2017。  這會在 Visual Studio 2015 建立和偵錯新雲端服務專案時產生錯誤。 在排序 toofix 此問題，重新安裝 hello Web Platform Installer 從 hello Azure SDK。  hello 問題將獲得解決在未來的 Visual Studio 2017 更新中。  .

 
### <a name="azure-in-role-cache"></a>Azure In-Role Cache 

- 2016 年 11 月 30 日終止支援 Azure In-Role Cache。 如需詳細資訊，請按一下[這裡](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/)。




