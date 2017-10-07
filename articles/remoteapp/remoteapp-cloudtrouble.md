---
title: "aaaTroubleshoot RemoteApp 雲端集合建立 |Microsoft 文件"
description: "了解如何 tootroubleshoot RemoteApp 雲端集合建立失敗"
services: remoteapp
documentationcenter: 
author: vkbucha
manager: mbaldwin
ms.assetid: 95eb7797-7b5e-4781-ad23-f15dd85b213d
ms.service: remoteapp
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 9484ecbdb048ede8df725215b313e049cc7648f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-remoteapp-cloud-collections"></a>建立 RemoteApp 雲端集合疑難排解
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
> 
> 

若您有建立雲端集合的問題，請查看下列資訊的 hello。

## <a name="your-image-is-invalid"></a>您的映像無效
如果您正在等候 Azure tooprovision 您的集合時，您會看到類似 「 GoldImageInvalid 」 的訊息，表示您的範本映像不符合 hello[定義映像需求](remoteapp-imagereqs.md)。 因此，請移讀取這些[需求](remoteapp-imagereqs.md)，修正您的映像，然後再試 toocreate 集合一次。

## <a name="common-errors-seen-in-hello-azure-management-portal"></a>在 hello Azure 管理入口網站中看到的常見錯誤
    DNS server could not be reached
    ProvisioningTimeout

雲端集合通常會因為您在建立期間使用自訂映像而失敗。  如果您看到上述錯誤 hello 的而且您使用自訂映像 toocreate hello 集合，請參閱 hello 下列事項：

* 確定您已上傳該 hello 自訂映像符合映像需求。
* 最常 hello 常見的問題是該 hello 映像未正確 syspreped。  
* 確認 hello 映像可以開機 HYPER-V 中，或嘗試直接在您使用 hello 映像的 Azure 訂用帳戶中建立的 IAAS VM。 如果 hello VM 失敗 tooboot 並不會啟動，則這通常表示該 hello 自訂映像未準備正確。  確認 hello 自訂映像已建立下列 hello 如何 toocreate 自訂的範本映像的 RemoteApp

如果您使用其中一個 hello Microsoft 映像包含您訂用帳戶，請嘗試再次 toocreate hello 集合。 如果 hello 問題持續發生請連絡 Microsoft 支援。

    PlatformImageTrialModeOnly

如果您看到此錯誤通常表示尚未升級的 tooa 付費帳戶，但您嘗試 toouse 在 hello hello 服務試用模式期間才是有效的 Microsoft 提供的映像。 在此情況下，嘗試 toocreate 您雲端的集合，但會確定 toospecify hello 正確的映像。

