---
title: "與虛擬機器擴展集的自動調整規模 aaaTroubleshoot |Microsoft 文件"
description: "針對使用虛擬機器擴展集的自動調整進行疑難排解。 了解所遇到的典型問題及如何 tooresolve 它們。"
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
ms.openlocfilehash: 4c9a70992348d87fb43646421a90a027bf400a17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-autoscale-with-virtual-machine-scale-sets"></a>針對使用虛擬機器擴展集的自動調整進行疑難排解
**問題**– 您已建立的自動調整基礎結構，Azure 資源管理員中使用 VM 規模集 – 例如藉由部署的範本，就像這樣： https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss bottle 規模 – 您必須定義標尺規則，它非常適合，不同之處在於無論您將在 hello Vm 多少負載，就不會自動調整規模。

## <a name="troubleshooting-steps"></a>疑難排解步驟
某些事項 tooconsider 包括：

* 每個 VM 有多少個核心，以及會載入每個核心？上述的 hello 範例 Azure 快速入門範本已載入單一核心 do_work.php 指令碼。 如果您使用單一核心的 VM 大小大於 VM Standard_A1 或 D1 然後您就必須 toorun 此負載多次。 藉由檢閱 [Azure 中 Windows 虛擬機器的大小](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* 在虛擬機器擴展集 hello 多少 Vm 做每一項工作？
  
    擴充事件只會發生時 hello 平均 CPU 跨**所有**hello Vm 規模集中的超過 hello 臨界值，透過內部 hello 時間 hello 自動調整規模規則中定義。
* 您是否遺漏任何調整事件？
  
    檢查 hello 稽核記錄檔以 hello Azure 入口網站的標尺事件。 或許遺漏相應增加和相應減少。 您可以依「調整」進行篩選。
  
    ![稽核記錄檔][audit]
* 您的相應縮小和相應放大的臨界值是否有足夠的差異？
  
    假設您設定規則 tooscale 出平均 CPU 時超過 50%，超過 5 分鐘和 tooscale 中平均 CPU 時小於 50%。 這會導致 「 拍打 」 的問題時的 CPU 使用量是關閉 toothis 臨界值，與不斷增加，並減少 hello 的調整動作 hello 集的大小。 因為這個緣故，hello 自動調整規模服務會嘗試 tooprevent"出現 flapping 的現象"，這可以呈現為非比例。 因此請確定您的向外延展和小數位數在閾值差異不足 tooallow 一些空間之間縮放比例。
* 您是否撰寫自己的 JSON 範本？
  
    很容易 toomake 錯誤、 因此開頭的範本，例如其上方的其中一個來證明 toowork，hello 和小型的累加變更。 
* 是否可以手動相應縮小或相應放大？
  
    請手動嘗試重新部署的 hello 與不同的 「 容量 」 設定 toochange hello Vm 數目的虛擬機器擴展集資源。 這是在此範例範本 toodo: https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing – 您可能需要確定它擁有 hello 的 tooedit hello 範本 toomake 相同機器大小，因為小數位數設定為使用。 如果您已成功可以手動變更 hello Vm 數目，您便知道 hello 問題是隔離的 tooautoscale。
* 請檢查您 Microsoft.Compute/virtualMachineScaleSet Microsoft.Insights 中和資源 hello [Azure 資源總管](https://resources.azure.com/)
  
    這是不可或缺的疑難排解工具，它會顯示 hello Azure 資源管理員資源的狀態。 按一下訂用帳戶，並查看 hello 您正在疑難排解的資源群組。 Hello 計算資源提供者下查看您建立虛擬機器擴展集 hello 和檢查執行個體檢視中，它會顯示 hello hello 部署的狀態。 另請檢查 Vm 的 hello VM 規模調整集合中的 hello 執行個體檢視。 然後移至 hello Microsoft.Insights 資源提供者，並檢查 hello 自動調整規模規則能呈現最佳效果。
* 正在 hello 診斷延伸模組工作，並發出時的效能資料？
  
    **更新：** Azure 自動調整規模已增強的 toouse 主機基礎不再需要安裝診斷延伸模組 toobe 度量管線。 這表示 hello 下一步的幾個段落不再套用如果您建立使用 hello 新管線的自動調整應用程式。 Azure 的範本已被轉換的 toouse hello 主應用程式管線的範例： https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale。 
  
    使用主機型度量自動調整規模適合 hello 下列原因：
  
  * 較少的移動組件做為沒有診斷擴充功能需要安裝 toobe。
  * 更簡單的範本。 只要加入 insights 自動調整規模規則 tooan 現有規模調整集合範本。
  * 新 VM 的報告更可靠且啟動更快速。
    
    hello 您可能會想使用的診斷延伸模組的 tookeep 的原因是如果您需要在記憶體診斷報告/縮放比例。 主機型度量資訊不會報告記憶體。
    
    這一點之後，才遵循 hello 本文其餘部分您仍在使用診斷擴充功能為您自動調整。
    
    自動調整 Azure 資源管理員中可以搭配使用 （但不會再對） 透過呼叫 hello 診斷延伸模組的 VM 延伸模組。 它會發出您在 hello 範本中定義的效能資料 tooa 儲存體帳戶。 這項資料會接著彙總 hello Azure 監視服務。
    
    如果 Vm hello hello Insights 服務無法讀取資料，它應該 toosend 您電子郵件-例如，如果 hello Vm 已關閉，因此請查看您的電子郵件 (建立 hello Azure 帳戶時，您會指定一個 hello)。
    
    您也可以前往並自行查看 hello 資料。 查看 hello 使用雲端總管的 Azure 儲存體帳戶。 如需範例使用 hello [Visual Studio Cloud Explorer](https://visualstudiogallery.msdn.microsoft.com/aaef6e67-4d99-40bc-aacf-662237db85a2)，登入，並挑選 hello Azure 訂用帳戶使用，並 hello 診斷儲存體帳戶名稱中 hello 部署中的診斷延伸模組定義參考範本...
    
    ![雲端總管][explorer]
    
    這裡您會看到一堆儲存每個 VM 的 hello 資料資料表。 讓 Linux 和 hello CPU 度量，做為範例，看看 hello 最新的資料列。 hello Visual Studio cloud explorer 支援的查詢語言，因此您可以執行類似的查詢 「 時間戳記 gt datetime' 2016年-02-02T21:20:00Z'"toomake 確定取得 hello 最新事件 （假設時間為 utc 格式）。 您在中看到那里對應 toohello hello 資料調整規模設定的規則嗎？ Hello 下列範例中，在機器 20 hello CPU 會啟動隨 hello 前 5 分鐘增加 too100%...
    
    ![儲存體資料表][tables]
    
    如果 hello 資料不存在，則表示 hello 問題是出在 hello hello Vm 中執行的診斷延伸模組。 如果有 hello 資料，則表示沒有問題以標尺規則，或與 hello Insights 服務。 檢查 [Azure 狀態](https://azure.microsoft.com/status/)。
    
    一旦您已經完成這些步驟，如果您仍無法自動調整您可以嘗試 hello 論壇[MSDN](https://social.msdn.microsoft.com/forums/azure/home?category=windowsazureplatform%2Cazuremarketplace%2Cwindowsazureplatformctp)，或[堆疊溢位](http://stackoverflow.com/questions/tagged/azure)，或記錄的支援通話。 是已備妥的 tooshare hello 範本和 hello 效能資料的檢視。

[audit]: ./media/virtual-machine-scale-sets-troubleshoot/image3.png
[explorer]: ./media/virtual-machine-scale-sets-troubleshoot/image1.png
[tables]: ./media/virtual-machine-scale-sets-troubleshoot/image4.png
