---
title: "上傳 Azure RemoteApp 的自訂映像 | Microsoft Docs"
description: "了解如何上傳 Azure RemoteApp 的自訂映像"
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
ms.openlocfilehash: 5a235fac88d6e95ea294bda197641108acb4a09f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="upload-a-custom-image-for-azure-remoteapp"></a>上傳 Azure RemoteApp 的自訂映像
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。
> 
> 

現在，您已建立自訂範本映像或已更新變更，您必須將該映像上傳至您的 Azure RemoteApp 映像庫。 使用這些步驟。

## <a name="before-you-start"></a>開始之前
1. 請確認您的自訂映像符合[映像需求](remoteapp-imagereqs.md)和[應用程式需求](remoteapp-appreqs.md)。
2. 安裝 [Azure PowerShell 模組](/powershell/azure/overview)。

## <a name="step-by-step-on-how-to-upload-custom-image"></a>逐步解說如何上傳自訂映像
1. 開啟 Azure 管理入口網站，並瀏覽至 [RemoteApp] 頁面。
2. 在 [範本映像] 索引標籤上，按一下頁面底部的 [上傳]。
3. 為您的映像輸入一個易記名稱，並指定儲存體帳戶位置。 請確定此位置會是與 RemoteApp 集合相同的位置或是您要建立 RemoteApp 集合的位置。
4. 當系統出現提示時，請將指令碼下載到本機電腦。
5. 將文字方塊中的命令參數複製到您的剪貼簿。
6. 開啟提升權限的 Windows PowerShell 視窗。
7. 從提升權限的 Windows PowerShell 視窗，瀏覽至您下載指令碼的相同目錄。
8. 貼上複製的命令，並按 **Enter**鍵。
   
   系統便會開始上傳程序，持續時間會取決於許多因素，其中包括您的網路速度和影像的大小
9. 如果因為網路中斷或類似原因導致上傳失敗，您可以繼續您已開始的上傳程序。 若要繼續上傳，您可以再次使用相同的命令列來執行指令碼。

> [!WARNING]
> 切勿修改上傳指令碼。 已實作可確保映像符合映像需求和應用程式需求的特定檢查。
> 
> 

## <a name="common-problems"></a>常見問題
* 請確定使用的是 Windows PowerShell，而不是 Azure PowerShell。 您必須安裝 Azure PowerShell 模組，因為上傳過程中會需要某些特定模組。
* 切勿更改指令碼，該指令碼已提供驗證，方便您使用。
* 如果 vhd 檔案在上傳期間遭到鎖定，請將檔案複製或移動到新位置，並再次嘗試上傳。 有些 Windows 程序可能會阻止上傳。  

