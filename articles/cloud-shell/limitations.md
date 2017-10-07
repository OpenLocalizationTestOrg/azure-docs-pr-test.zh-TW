---
title: "aaaAzure 雲端殼層 （預覽） 限制 |Microsoft 文件"
description: "Azure Cloud Shell 限制的概觀"
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: 8462b0b9850fcde790a386433009439bbab52c0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-of-azure-cloud-shell"></a>Azure Cloud Shell 限制
Azure 的雲端 Shell 具有 hello 下列已知限制：

## <a name="system-state-and-persistence"></a>系統狀態和持續性
提供您的雲端殼層工作階段的 hello 機器是暫時性的而且您的工作階段未使用達 20 分鐘後回收。 雲端殼層需要裝載檔案共用 toobe。 如此一來，您的訂用帳戶必須是能夠 tooset 總儲存體資源 tooaccess 雲端殼層。 其他考量包括：
* 在掛接的儲存體中，只會保存 `$Home` 目錄或 `clouddrive` 目錄內的修改。
* 只能從您的[已指派區域](persisting-shell-storage.md#mount-a-new-clouddrive)內掛接檔案共用。
* Azure 檔案只支援本機備援儲存體和異地備援儲存體帳戶。

## <a name="user-permissions"></a>使用者權限
權限設定為沒有 sudo 存取權的一般使用者。 將不會保存 `$Home` 目錄之外的任何安裝。
雖然某些命令內 hello`clouddrive`目錄下，例如`git clone`，並沒有適當的權限，您`$Home`目錄沒有權限。

## <a name="browser-support"></a>瀏覽器支援
雲端殼層可支援 Microsoft Edge、 Microsoft Internet Explorer、 Google Chrome、 Mozilla Firefox 及 Apple Safari hello 最新的版本。 不支援 Safari 私密瀏覽模式。

## <a name="copy-and-paste"></a>複製和貼上
Ctrl + C 和 Ctrl + V 無法運作，以及複製/貼上快速鍵在雲端介面中 Windows 電腦上，使用 Ctrl + Insert 和 Shift + Insert toocopy 貼分別。

以滑鼠右鍵按一下複製和貼上選項也可使用，但以滑鼠右鍵按一下函式是主體 toobrowser 特定剪貼簿存取。

## <a name="editing-bashrc"></a>編輯 .bashrc
編輯 .bashrc 時請小心，這麼做可能會導致 Cloud Shell 發生未預期的錯誤。

## <a name="bashhistory"></a>.bash_history
Bash 命令的歷程記錄可能因為 Cloud Shell 工作階段中斷或並行工作階段而出現不一致的情況。

## <a name="usage-limits"></a>使用限制
Cloud Shell 主要用於互動式的使用案例。 因此，任何長時間執行而沒有互動的工作階段會在不發出警告的情況下結束。

## <a name="network-connectivity"></a>網路連線
在雲端介面中的任何延遲主體 toolocal 網際網路連線，雲端殼層會繼續 tooattempt toocarry 時傳送的任何指示。

## <a name="next-steps"></a>後續步驟
[Cloud Shell 快速入門](quickstart.md)
