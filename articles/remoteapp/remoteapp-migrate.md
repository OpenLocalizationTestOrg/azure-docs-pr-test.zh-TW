---
title: "aaaMigrate 使用者資料與 Azure RemoteApp |Microsoft 文件"
description: "深入了解如何 toomigrate 您的使用者資料和 Azure RemoteApp。"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: d7e4fbf1-cb42-4430-94a0-ed6d4676fc86
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: aefc6ccc2c6173754acf6cad06102f27c8cb1d26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-data-into-and-out-of-azure-remoteapp"></a>如何 toomigrate 資料傳入活動和從 Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
> 
> 

您可以使用許多不同的工具和方法 tootransfer[使用者資料](remoteapp-upd.md)進出 Azure RemoteApp。 以下是幾個方法︰

* 使用剪貼簿共用複製並貼上
* 複製檔案和資料 tooa 檔案伺服器
* 複製檔案 tooOneDrive 商務透過瀏覽器
* 使用重新導向複製檔案

> [!NOTE]
> 您無法啟用 hello OneDrive for Business 或取用者的同步處理代理程式-它們[不支援](remoteapp-onedrive.md)Azure RemoteApp 中。
> 
> 

## <a name="use-copy-and-paste-in-file-explorer"></a>在 [檔案總管] 中使用複製及貼上
RemoteApp 部署中已啟用複製與貼上使用 hello 剪貼簿[預設](remoteapp-redirection.md)。 這可讓使用者在他們的本機電腦和 RemoteApp 應用程式之間複製檔案。 通常，hello 正常操作程序使用 RemoteApp 中的應用程式，透過使用者儲存檔案 tootheir Upd-移動 RemoteApp 中的資料很容易：

1. 在 RemoteApp 集合中[將 [檔案總管] 發佈為應用程式](remoteapp-publish.md)。 (請注意，這是系統管理工作。)
2. 直接您使用者 toolaunch hello 檔案總管 中您發行應用程式和 toouse 該 toocopy 和貼上檔案到其 UPD 和不使用。

## <a name="upload-files-and-data-tooa-file-server-by-using-standard-network-file-copy"></a>上傳檔案及資料 tooa 檔案伺服器，方法是使用標準網路檔案複本
通常組織使用檔案伺服器 toostore 一般資料。 如果您知道 hello 伺服器名稱或位置，您的使用者可以瀏覽 hello hello 伺服器的區域網路，並方式一樣上方，然後複製其檔案。 再次將想 toopublish 檔案總管 tooRemoteApp，然後分享您的使用者。

> [!NOTE]
> hello 檔案伺服器必須位於 RemoteApp 部署進入 hello 可路由網路上。
> 
> 

## <a name="copy-files-tooonedrive-for-business"></a>複製檔案 tooOneDrive for Business
雖然您無法啟用 RemoteApp 的商務同步代理程式 」 的 hello OneDrive，您還是可以複製檔案從 UPD tooOneDrive 商務透過瀏覽器。 

1. 發行 tooRemoteApp 檔案總管]，然後告訴 [使用者 tooaccess hello 透過該應用程式的檔案。 
2. 如果它是最簡單的 tootransfer 檔案壓縮，因此使用者應該建立.zip 檔案，其中包含所有 hello 檔案 toomove tooOneDrive 商務。
3. 詢問使用者 toogo toohello Office 365 入口網站，並前往 tooOneDrive 及上傳 hello.zip 檔案。

## <a name="copy-files-by-using-drive-redirection"></a>使用磁碟重新導向複製檔案
如果您已啟用 [磁碟重新導向](remoteapp-redirection.md)，您已為您的使用者建立對應磁碟機。 在此情況下，它們可以 zip hello 重新導向磁碟機上的檔案，然後將它們儲存 tootheir 本機電腦。

## <a name="how-administrators-can-export-data"></a>系統管理員如何匯出資料

管理訂用帳戶 tooAzure 使用 Azure PowerShell 的儲存體中的所有集合的 Azure RemoteApp 可以匯出所有的使用者設定檔磁碟 (UPD) 的 cmdlet，匯出 AzureRemoteAppUserDisk。  沒有任何能力 tooselect 個別 UPD 的。  Hello PowerShell 命令執行時，每個使用者磁碟會為固定的磁碟大小的 50 gb，並匯出的 tooAzure 儲存體。  會立即對此儲存體產生 Azure 儲存體成本。  當執行這個命令，請確定沒有否則 hello 匯出將會失敗的工作階段。

只能在 RDS 部署中重新使用已加入網域之 Azure RemoteApp 部署的 UPD，並無法使用未加入網域的部署。  如果這些磁碟將會使用 RDS 部署建議 toouse 我們[自動化指令碼](https://github.com/arcadiahlyy/aramigration)，以便匯出、 轉換，並且 hello UPD 的匯入 RDS 部署。

