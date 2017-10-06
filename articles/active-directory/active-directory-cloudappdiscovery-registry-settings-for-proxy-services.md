---
title: "aaaCloud Proxy 服務的應用程式探索登錄設定 |Microsoft 文件"
description: "本主題的 hello 目標是您以 hello 會引導您 tooprovide 需要 tooperform tooset hello 需要連接埠 hello 執行 hello Cloud App Discovery 代理程式的電腦上。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8d78e925-e331-40ba-904a-e4ef14260cac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: bb1fe20016459160b4f67cb0125b1781a0260c4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-app-discovery-registry-settings-for-proxy-services"></a>Proxy 服務的 Cloud App Discovery 登錄設定
根據預設，hello Cloud App Discovery 代理程式是設定的 toouse 只有 hello 連接埠 80 或 443。 如果您打算在與 proxy 伺服器使用自訂連接埠 （非 80 或 443） 的環境中安裝雲端應用程式探索，您需要 tooconfigure 代理程式 toouse 此連接埠。 hello 組態根據登錄機碼。

本主題的 hello 目標是您以 hello 會引導您 tooprovide 需要 tooperform tooset hello 需要連接埠 hello 執行 hello Cloud App Discovery 代理程式的電腦上。

**toomodify hello 連接埠供 hello 電腦執行 hello Cloud App Discovery 代理程式，執行下列步驟的 hello:**

1. 啟動 hello 登錄編輯程式。 <br> ![執行](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy01.png)
2. 瀏覽 tooor 建立下列登錄機碼的 hello: <br> **HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint** 
3. 建立新的**多字串**值，稱為**連接埠**。 ![](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)
4. tooopen hello**編輯多字串**] 對話方塊中，按兩下 hello 連接埠值。
5. 在 hello 值資料] 文字方塊中，輸入下列值的 hello 並加入您的組織所使用的所有自訂連接埠： <br><br>
   **80** <br>
   **8080** <br>
   **8118** <br>
   **8888** <br>
   **81** <br>
   **12080** <br>
   **6999** <br>
   **30606** <br>
   **31595** <br>
   **4080** <br>
   **443** <br>
   **1110** <br><br>
   ![編輯多字串](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)
6. 按一下**確定**tooclose hello**編輯多字串**對話方塊。

**其他資源**

* [如何探索組織內使用未經批准的雲端應用程式](active-directory-cloudappdiscovery-whatis.md) 

