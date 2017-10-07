---
title: "即時資料流 aaaTroubleshooting 指南 |Microsoft 文件"
description: "本主題提供如何 tootroubleshoot 即時串流處理問題的建議。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 3a7f6c1d-ce57-4fa4-a7a6-edb526b3ffbf
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 8549bae947ff3b225ce624220d1e48b63f90208c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-live-streaming"></a>為即時串流而設的疑難排解指南
本主題提供如何建議 tootroubleshoot 一些即時串流處理的問題。

## <a name="issues-related-tooon-premises-encoders"></a>問題相關的 tooon 內部編碼器
本節提供如何 tootroubleshoot 問題相關的 tooon 內部編碼器，會設定 toosend 的建議為即時編碼啟用單一位元速率串流 tooAMS 通道。

### <a name="problem-would-like-toosee-logs"></a>問題： 希望 toosee 記錄檔
* 潛在問題：找不到可能有助於偵錯問題的編碼器記錄檔。
  
  * **Telestream Wirecas**：您通常可以在 C:\Users\{使用者名稱}\AppData\Roaming\Wirecast\ 下找到記錄檔 
  * **元素 Live**： 您可以尋找已連結 toologs hello 管理入口網站上。 依序按一下 [統計] 及 [記錄檔]。 在 [hello**記錄檔**] 頁面上，您會看到所有的記錄檔清單 hello LiveEvent 項目時，請選擇其中一個比對您目前的工作階段的 hello。 
  * **快閃媒體即時編碼程式**： 您可以找到 hello**記錄檔目錄...**瀏覽 toohello**編碼方式記錄** 索引標籤。

### <a name="problem-there-is-no-option-for-outputting-a-progressive-stream"></a>問題：沒有輸出漸進式資料流的選項
* **可能的問題**: hello 編碼器正在使用不會自動非交錯。 
  
    **疑難排解步驟**： 尋找 hello 編碼器介面中的取消交錯式選項。 一旦啟用非交錯處理，請再次檢查漸進式的輸出設定。 

### <a name="problem-tried-several-encoder-output-settings-and-still-unable-tooconnect"></a>問題： 嘗試幾個編碼器輸出設定，並將仍然無法 tooconnect。
* **可能的問題**：未正確重設 Azure 編碼通道。 
  
    **疑難排解步驟**： 請確定 hello 編碼器不會再推入 tooAMS、 停止及重設 hello 通道。 執行一次之後, 再試一次您的編碼器連接的 hello 新設定。 如果這仍無法更正 hello 問題，請嘗試完全建立新的通道，有時數次嘗試失敗之後通道可能會損毀。  
* **可能的問題**: hello GOP 大小或主要畫面格設定不佳。 
  
    **疑難排解步驟**：建議的 GOP 大小或主要畫面間隔為 2 秒。 某些編碼器以畫面數目計算此設定，某些則使用秒。 例如： 輸出 30fps 時, hello GOP 大小會是 60 框架，這是對等 too2 秒。  
* **可能的問題**： 封鎖 hello 資料流已關閉的連接埠。 
  
    **疑難排解步驟**： 當 RTMP 透過串流處理，請檢查防火牆和/或 proxy 設定 tooconfirm 1935 和 1936年的輸出連接埠已開啟。 使用 RTP 資料流時，請確認輸出連接埠 2010 已開啟。 

### <a name="problem-when-configuring-hello-encoder-toostream-with-hello-rtp-protocol-there-is-no-place-tooenter-a-host-name"></a>問題： 在設定 hello 編碼器 toostream 以 hello RTP 通訊協定時，沒有無處 tooenter 主機名稱。
* **可能的問題**： 許多 RTP 編碼器不允許的主機名稱和 IP 位址必須 toobe 取得。  
  
    **疑難排解步驟**: toofind hello IP 位址，請開啟命令提示字元的任何電腦上。 這在 Windows 中，開啟 toodo hello 執行啟動器 （WIN + R），並輸入"cmd"tooopen。  
  
    一旦開啟 hello 命令提示字元，輸入 「 Ping [AMS 主機名稱]"。 
  
    可以藉由略過從 hello Azure 內嵌 URL 以反白顯示 hello 下列範例中的 hello 連接埠號碼衍生 hello 主機名稱： 
  
    rtp://test2-amstest009.rtp.channel.mediaservices.windows.net:2010/ 
  
    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle10.png)

> [!NOTE]
> 如果後您仍無法成功地串流處理 hello 疑難排解步驟，提交支援票證使用 hello Azure 入口網站。
> 
> 

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

