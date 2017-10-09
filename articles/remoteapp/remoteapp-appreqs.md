---
title: "Azure RemoteApp aaaApp 需求 |Microsoft 文件"
description: "深入了解應用程式的 toouse Azure RemoteApp 中的 hello 需求"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 4427eef6-288a-49e1-97eb-fee67d99f26a
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 3fa2bcdaab457a6fbee8ac52a81d1c4154bbdce1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="app-requirements"></a>應用程式需求
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
> 
> 

Azure RemoteApp 支援來自 Windows Server 2012 R2 映像的資料流 32 位元或 64 位元 Windows 架構應用程式。 大部分現有 32 位元或 64 位元 Windows 架構應用程式都是「依現狀」在 Azure RemoteApp (遠端桌面服務或舊稱的「終端機服務」) 環境中執行。 不過，執行和良好執行是有差別的，有些應用程式運作正常且完善執行，有些則不是。 下列資訊的 hello 提供遠端桌面服務環境中的應用程式的開發和測試 tooensure 相容性的指引。

提示：我們正在為您建立一些實用的應用程式範例。 您會看到討論如何在 RemoteApp 內使用 Microsoft Access、QuickBooks 和 APP-V 的新主題。

## <a name="requirements"></a>需求
如果遵循下列三個需求，可協助應用程式在 RemoteApp 中順暢執行：

1. 符合所有的應用程式[Windows 桌面應用程式的憑證需求](https://msdn.microsoft.com/library/windows/desktop/hh749939.aspx)和遵守太[程式設計指導方針的遠端桌面服務](https://msdn.microsoft.com/library/aa383490.aspx)必須完成與 RemoteApp 的相容性。
2. 應用程式應該永遠不會將資料儲存在本機 hello 映像或可能會遺失的 RemoteApp 執行個體上。  建立一個 RemoteApp 集合之後，hello 執行個體就會遭到複製，並是無狀態而應該只包含應用程式。 將外部來源中或 hello 使用者設定檔中儲存資料。
3. 自訂映像不應該包含可能會遺失的資料。  

## <a name="testing-your-apps"></a>測試應用程式
使用這些步驟 tootesting 應用程式：

1. 安裝 Windows Server 2012 R2 和您的應用程式
2. 啟用遠端桌面
3. 建立兩個使用者帳戶，使用者 a 和使用者 b，加入這兩個使用者帳戶 toohello 遠端桌面安全性群組。
4. 藉由建立兩個同時 RDS 工作階段 toohello 電腦在啟動 hello 應用程式時檢查多重工作階段相容性。
5. 驗證應用程式行為

## <a name="application-development-guidelines"></a>應用程式開發指導方針
使用下列指導方針來開發應用程式，remoteapp hello。

### <a name="multiple-users"></a>多個使用者
* 安裝 [單一使用者的應用程式 ](https://msdn.microsoft.com/library/aa380661.aspx)可能在多使用者環境中造成問題。
* 應用程式應該[儲存使用者特定資訊](https://msdn.microsoft.com/library/aa383452.aspx)使用者特定位置中分別從全域資訊套用 tooall 使用者。
* RemoteApp 為 [核心物件使用多個命名空間](https://msdn.microsoft.com/library/aa382954.aspx)；主要是藉由用戶端/伺服器應用程式中的服務來使用全域命名空間。
* 它不是電腦名稱或 hello hello 的安全 tooassume [IP 位址](https://msdn.microsoft.com/library/aa382942.aspx)指派的 toohello 電腦與使用者相關聯單一因為多個使用者可以登入同時 tooa 遠端桌面工作階段主機 （RD 工作階段主機） 伺服器。

### <a name="performance"></a>效能
* 停用[圖形效果](https://msdn.microsoft.com/library/aa380822.aspx)新增應用程式 tooRemoteApp 之前。
* 將停用所有使用者，toomaximize CPU 可用性[背景工作](https://msdn.microsoft.com/library/aa380665.aspx)或建立有效率的背景工作不需要大量資源。
* 您應該針對多使用者、多處理器環境微調和平衡應用程式 [執行緒使用量](https://msdn.microsoft.com/library/aa383520.aspx) 。
* toooptimize 效能，應用程式的最佳作法是太[偵測](https://msdn.microsoft.com/library/aa380798.aspx)中用戶端工作階段是否正在執行。

