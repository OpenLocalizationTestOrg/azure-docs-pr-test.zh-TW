---
title: "自訂映像的 Azure RemoteApp aaaUpload |Microsoft 文件"
description: "了解如何 tooupload 自訂映像的 Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: 299e0510-1a6b-4fdf-914a-3631b061a360
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: ericor
ms.openlocfilehash: 6ad40fe58795ece37f4c7900be01bc713938da87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-custom-image-for-azure-remoteapp"></a>上傳 Azure RemoteApp 的自訂映像
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
> 
> 

既然您已建立您的自訂範本映像，或已更新的變更，您需要 tooupload 該映像 tooyour Azure RemoteApp 映像庫。 使用這些步驟。

## <a name="before-you-start"></a>開始之前
1. 確認您的自訂映像符合 hello[映像需求](remoteapp-imagereqs.md)和[應用程式的需求](remoteapp-appreqs.md)。
2. 安裝 hello [Azure PowerShell 模組](/powershell/azure/overview)。

## <a name="step-by-step-on-how-tooupload-custom-image"></a>逐步解說有關 tooupload 自訂映像
1. 開啟 Azure 管理入口網站，並瀏覽 toohello RemoteApp 頁面。
2. 在 hello**範本映像**索引標籤上，按一下 **上傳**hello hello 頁底端。
3. 輸入您的映像的易記名稱並指定 hello 儲存體帳戶位置。 請 hello 位置 hello 與您的 RemoteApp 集合或想 toocreate 其中的位置相同的位置。
4. 出現提示時，下載 hello 指令碼 tooyour 本機電腦。
5. 複製 hello 命令參數中的 hello 文字方塊 tooyour 剪貼簿。
6. 開啟提升權限的 Windows PowerShell 視窗。
7. Hello 從提高權限的 Windows PowerShell 視窗中，瀏覽 toohello hello 指令碼的下載位置的相同目錄。
8. 貼上 hello 複製命令並按**Enter**。
   
   hello 上傳程序就會開始，持續時間取決於許多因素，包括您的網路速度和 hello 映像的大小
9. 如果您上傳未成功因為網路中斷或項目類似的您一律可以繼續 hello 上傳程序開始。 tooresume 上傳，執行一次使用的 hello 指令碼 hello 相同命令列。

> [!WARNING]
> 永遠不會修改 hello 上傳指令碼。 指定檢查已實作 hello 映像符合 hello 映像需求和應用程式需求的 tooensure。
> 
> 

## <a name="common-problems"></a>常見問題
* 請確定使用的是 Windows PowerShell，而不是 Azure PowerShell。 您需要 tooinstall hello Azure PowerShell 模組，因為某些模組會在必要時 hello 上傳程序。
* 永遠不會改變 hello 指令碼，驗證是為了方便起見。
* 如果 hello vhd 檔案上傳期間取得鎖定，hello 檔案複製或移動它 tooa 新位置，並嘗試上傳一次。 有些 Windows 程序可能會阻止上傳。  

