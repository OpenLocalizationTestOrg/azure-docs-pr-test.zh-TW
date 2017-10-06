---
title: "aaaAn 應用程式 Proxy 應用程式會採用太長 tooload |Microsoft 文件"
description: "疑難排解 hello Azure AD Application Proxy 的頁面載入效能問題"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 4c7a51f96840966a1d88933fa4e30f39479d8a5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="an-application-proxy-application-takes-too-long-tooload"></a>應用程式 Proxy 應用程式便會太長 tooload

本文將協助您 toounderstand 為什麼 Azure AD Application Proxy 應用程式可能需要很長的時間 tooload，以及您可以執行 tooresolve 此問題。

## <a name="overview"></a>概觀
如果正在您的應用程式，但您會看到很長的延遲，您可以考慮 tooimprove hello 速度的網路拓撲中可能有做一些調整。 評估不同拓撲，請參閱 hello[網路考量文件](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations)。

如果這些考量沒有幫助，很抱歉我們目前對於效能調整沒有進一步的建議。 由於 hello 應用程式 Proxy 服務會展開，可能會更接近 tooyou toomore 資料中心，您可能會直接啟動 toosee 改善延遲。 toosee hello 的完整清單 Azure 資料中心，您可以查看 hello[延遲測試頁](http://www.azurespeed.com/Azure/Latency)。 

hello 與 hello 應用程式 Proxy 服務的資料中心可以找到以 hello[連接器連接埠測試工具](https://aadap-portcheck.connectorporttest.msappproxy.net/)。 

## <a name="feedback-on-application-proxy-data-center-locations"></a>對 Application Proxy 資料中心位置的意見反應 
可能還不包括應用程式 Proxy，但結果可能會導致 tooa 絕佳延遲改善您的 Azure 資料中心。 hello 資料中心位置< aadapfeedback@microsoft.com >讓我們可做為您的意見反應 tooplan 我們展開。

我們使用一些其他功能，可協助改善 hello 延遲目前看到很長的延遲時間的租用戶，而且是確定 tooshare 文件之後使用。

## <a name="next-steps"></a>後續步驟
[使用現有的內部部署 Proxy 伺服器](application-proxy-working-with-proxy-servers.md)
