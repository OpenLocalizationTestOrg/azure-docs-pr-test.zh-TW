---
title: "aaaAzure RemoteApp 映像需求 |Microsoft 文件"
description: "深入了解建立與 Azure RemoteApp 搭配使用的映像 toobe hello 需求"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7cbb90f4-6dc9-462c-a429-088cdb57414e
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 4e35203eb93a866d4e0bd591d42b34746c7ffa4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="requirements-for-azure-remoteapp-images"></a>Azure RemoteApp 映像的需求
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
> 
> 

Azure RemoteApp 使用 Windows Server 2012 R2 的映像 toohost 所有 hello 程式，您會想 tooshare 與您的使用者。 toocreate 自訂映像，您可以使用現有的映像開始或[建立一個新](remoteapp-create-custom-image.md)。

> [!TIP]
> 您知道您 Azure RemoteApp 訂用帳戶可讓您存取 tooa Windows Server 2012 R2 的映像中 hello Azure VM 圖庫，您可以使用 toocreate 您自己的範本映像嗎？ [立即使用](remoteapp-image-on-azurevm.md)。  
> 
> 

可以上傳 Azure RemoteApp 搭配使用的 hello 映像的 hello 需求如下：

* 自訂應用程式不在本機儲存資料，hello 映像上。 這些都是無狀態的映像，而且應該只包含應用程式。
* hello 影像未包含資料，可能會遺失。
* hello 映像大小應該是 mb/s 的倍數。 如果您嘗試 tooupload 不精確的多個映像，hello 上傳將會失敗。
* hello 影像大小必須為 127 GB 或更小。
* 必須在 VHD 檔案上 (VHDX 檔案目前不受支援)。
* hello VHD 不能在第 2 代虛擬機器。
* hello VHD 可以是固定大小或動態擴充。 因為它會採用比固定大小的 VHD 檔案的較少時間 tooupload tooAzure，建議您使用動態擴充的 VHD。
* 必須使用 hello 主開機記錄 (MBR) 磁碟分割樣式初始化磁碟 hello。 不支援 hello GUID 磁碟分割表格 (GPT) 磁碟分割樣式。
* hello VHD 必須包含單一 Windows Server 2012 R2 的安裝。 它可包含多個磁碟區，但只有其中一個包含 Windows 安裝。
* 必須安裝 hello 遠端桌面工作階段主機 (RDSH) 角色和 hello 桌面體驗功能。
* hello 遠端桌面連線代理人角色必須*不*安裝。
* 必須停用 hello 加密檔案系統 (EFS)。
* hello 映像必須使用 hello 參數 SYSPREPed **/oobe /generalize /shutdown** (請勿使用 hello **/mode: vm**參數)。
* 不支援從快照鏈結上傳您 VHD。

如需建立 Azure RemoteApp 映像的詳細資訊，請參閱 [建立 Azure RemoteApp 映像](remoteapp-imageoptions.md) 。

