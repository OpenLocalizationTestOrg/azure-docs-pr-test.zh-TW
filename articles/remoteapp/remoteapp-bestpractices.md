---
title: "aaaAzure RemoteApp 最佳作法 |Microsoft 文件"
description: "設定和使用 Azure RemoteApp 的最佳做法。"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b851865b-bec4-4f29-82c0-7b9770c1a520
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: f4d09ef30816eaebb74b69f26f3242c69ea27591
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-configuring-and-using-azure-remoteapp"></a>設定和使用 Azure RemoteApp 的最佳做法
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/12/application-remoting-and-the-cloud/)如需詳細資訊。
> 
> 

hello 下列資訊可協助您設定及有效率地使用 Azure RemoteApp。

## <a name="connectivity"></a>連線能力
* 一律使用最新用戶端版本 hello。 使用舊版的用戶端可能會造成連線問題和其他降級的體驗。 啟用應用程式自動更新為您的裝置，可確保該 hello 最新的用戶端永遠都會安裝。
* 一律使用 hello 最穩定且可靠網際網路連線可用 tooyou。  
* 請使用支援的 Proxy 連線以獲得最佳連線效能。  不支援 hello SOCKS proxy。

## <a name="applications"></a>應用程式
* 儲存並關閉 RemoteApp 應用程式，當您完成 hello 應用程式時。 未關閉 hello 應用程式可能會導致資料遺失。
* 在 Azure RemoteApp 中使用自訂應用程式之前，請先進行驗證。 這包括確保它們有效多重工作階段的平台上並不會消耗不必要的資源，例如記憶體和 CPU 可能會佔用 hello 中的另一位使用者的相同集合。 詳細資訊，請下載並檢閱 hello[遠端桌面服務的應用程式相容性最佳作法](http://www.dabcc.com/resources/Application%20Compatibility%20Best%20Practices%20for%20Remote%20Desktop%20Services.pdf)。

## <a name="configuration-and-management"></a>設定和管理
* 將您的範本映像，向上 toodate，視需要安裝軟體更新和其他重大修正程式。 這可確保當 Azure RemoteApp 自動縮放 toomeet 已修補程式的容量，每個執行個體。  
* 請確認您有安全和可靠的 Active Directory Federation Services (AD FS) 部署。 否則，用戶端驗證可能會失敗，導致使用者無法存取 Azure RemoteApp。
* 使用安裝的應用程式、角色或功能設定範本映像，使它們成為無狀態。 它們不應該仰賴 hello 中的虛擬機器中的永續性狀態是 RemoteApp 服務的任何執行個體。
  * 所有使用者資料都儲存使用者設定檔或其他儲存體位置 toohello 外部服務，例如在內部部署的檔案共用或 OneDrive。
  * 例如，在內部部署的檔案共用或 OneDrive 儲存體位置 toohello 外部服務，儲存共用的資料。
  * 在 hello 範本映像，而不是在服務中的個別虛擬機器上設定任何的全系統設定。
  * 停用自動軟體更新已發行的應用程式-改為手動加以套用 toohello 範本映像，並測試它們，然後再從 hello 範本部署。

