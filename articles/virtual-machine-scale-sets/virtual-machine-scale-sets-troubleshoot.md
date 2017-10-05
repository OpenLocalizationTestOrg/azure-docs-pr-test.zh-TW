---
title: "針對使用虛擬機器擴展集的自動調整進行疑難排解 | Microsoft Docs"
description: "針對使用虛擬機器擴展集的自動調整進行疑難排解。 了解所遇到的一般問題和解決方式。"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7d87b72-ee24-4e52-9377-a42f337f76fa
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: windows
ms.devlang: na
ms.topic: article
ms.date: 10/28/2016
ms.author: guybo
ms.openlocfilehash: bd45a0fb99a77851aa7b91d23bd4b830b6f5cc7b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-autoscale-with-virtual-machine-scale-sets"></a>針對使用虛擬機器擴展集的自動調整進行疑難排解
**問題** – 您已使用 VM 擴展集在 Azure Resource Manager 中建立自動調整基礎結構，例如藉由部署範本，如下所示︰https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale – 您有已定義的調整規則，並且運作良好，美中不足的是無論您在 VM 上放置多少負載，它都不會自動調整。

## <a name="troubleshooting-steps"></a>疑難排解步驟
要考量的事項包括：

* 每個 VM 擁有多少核心，以及您是否讓每個核心都有負載？
  上述的範例 Azure 快速入門範本具有 do_work.php 指令碼，它會載入單一核心。 如果您使用大於單一核心大小類似 Standard_A1 或 D1 的 VM，則您需要多次執行此負載。 藉由檢閱 [Azure 中 Windows 虛擬機器的大小](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* VM 擴展集中有多少 VM，您是否在每一個 VM 上執行工作？
  
    相應放大只會在擴展集中 **所有** VM 的平均 CPU，經過自動調整規則中定義的內部時間之後超過臨界值時發生。
* 您是否遺漏任何調整事件？
  
    在 Azure 入口網站中檢查調整事件的稽核記錄檔。 或許遺漏相應增加和相應減少。 您可以依「調整」進行篩選。
  
    ![稽核記錄檔][audit]
* 您的相應縮小和相應放大的臨界值是否有足夠的差異？
  
    假設您在平均 CPU 於 5 分鐘後大於 50% 時將規則設為相應放大，而在平均 CPU 小於 50% 時將規則設為相應縮小。 當 CPU 使用量很接近此臨界值時，且調整動作經常增加和減少集合的大小，會導致「flapping」問題。 因為這個緣故，自動調整服務會嘗試防止「flapping」，可以表示為未調整。 因此請確定您的相應放大和相應縮小的臨界值有足夠的差異，以便在調整之間容許一些空間。
* 您是否撰寫自己的 JSON 範本？
  
    很容易發生錯誤，所以請從如上所述已經過證明可以運作的範本開始，並且進行小的增量變更。 
* 是否可以手動相應縮小或相應放大？
  
    請嘗試使用不同的「容量」設定重新部署 VM 擴展集資源，以手動變更 VM 數目。 執行這項操作的範例範本如下︰https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing – 您可能需要編輯範本以確定它有與您的擴展集所使用的相同機器大小。 如果您可以成功手動變更 VM 數目，則您知道問題與自動調整無關。
* 請在 [Azure 資源總管](https://resources.azure.com/)中檢查您的 Microsoft.Compute/virtualMachineScaleSet 和 Microsoft.Insights 資源。
  
    這是向您顯示 Azure Resource Manager 資源的狀態不可或缺的疑難排解工具。 按一下您的訂用帳戶，查看您正在進行疑難排解的資源群組。 在「計算」資源提供者下查看您建立的 VM 擴展集，並且檢查執行個體檢視，它會顯示部署的狀態。 也請檢查 VM 擴展集中的 VM 執行個體檢視。 然後進入 Microsoft.Insights 資源提供者，並且檢查自動調整規則看起來是否沒有問題。
* 診斷擴充是否正常運作，而且發出效能資料？
  
    **更新︰**已增強 Azure 自動調整，以使用不再需要安裝診斷擴充功能的主機型度量管線。 這表示如果您使用新的管線建立自動調整應用程式，則不再適用於後續幾個段落。 已經轉換為使用主機管線的 Azure 範本範例在：https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale。 
  
    使用主機型度量進行自動調整較佳，原因如下︰
  
  * 無需安裝診斷延伸模組，因此移動組件較少。
  * 更簡單的範本。 只將 insights 自動調整規則新增至現有的擴展集範本。
  * 新 VM 的報告更可靠且啟動更快速。
    
    您可能想要繼續使用診斷延伸模組的唯一原因是您需要記憶體診斷報告/調整大小。 主機型度量資訊不會報告記憶體。
    
    記住這點之後，如果您仍在使用診斷延伸模組進行自動調整，才需依照本文的其餘部分。
    
    Azure Resource Manager 中的自動調整可以 (但不再必要) 透過稱為診斷擴充功能的 VM 延伸模組運作。 它會將效能資料發出至您在範本中定義的儲存體帳戶。 然後 Azure 監視器服務會彙總此資料。
    
    如果 Insights 服務無法讀取來自 VM 的資料，就會傳送電子郵件給您，例如，如果 VM 關閉，請查看您的電子郵件 (您在建立 Azure 帳戶所指定的電子郵件)。
    
    您也可以自行前往並查看資料。 使用雲端總管查看 Azure 儲存體帳戶。 例如使用 [Visual Studio 雲端總管](https://visualstudiogallery.msdn.microsoft.com/aaef6e67-4d99-40bc-aacf-662237db85a2)、登入，並且挑選您使用的 Azure 訂用帳戶，以及您的部署範本中的診斷擴充定義中參考的診斷儲存體帳戶名稱.
    
    ![雲端總管][explorer]
    
    您會在這裡看到許多資料表，在其中儲存每個 VM 的資料。 以 Linux 和 CPU 度量為例，查看最新的資料列。 Visual Studio 雲端總管支援一種查詢語言，因此您可以執行類似 “Timestamp gt datetime’2016-02-02T21:20:00Z’” 的查詢，以確定取得最新的事件 (假設時間是 UTC 格式)。 您在那裡看到的資料是否對應您設定的調整規則？ 在下列範例中，機器 20 的 CPU 在過去 5 分鐘開始增加到 100%.
    
    ![儲存體資料表][tables]
    
    如果資料不存在，則表示問題是出在 VM 中執行的診斷擴充。 如果有資料，則表示您的調整規則或 Insights 服務有問題。 檢查 [Azure 狀態](https://azure.microsoft.com/status/)。
    
    一旦您完成這些步驟後，如果仍有自動調整問題，您可以嘗試 [MSDN](https://social.msdn.microsoft.com/forums/azure/home?category=windowsazureplatform%2Cazuremarketplace%2Cwindowsazureplatformctp) 上的論壇，或 [Stack Overflow](http://stackoverflow.com/questions/tagged/azure)，或記錄支援呼叫。 請準備共用範本和效能資料的檢視。

[audit]: ./media/virtual-machine-scale-sets-troubleshoot/image3.png
[explorer]: ./media/virtual-machine-scale-sets-troubleshoot/image1.png
[tables]: ./media/virtual-machine-scale-sets-troubleshoot/image4.png
