---
title: "Azure Active Directory B2C：區域可用性和資料存留處 | Microsoft Docs"
description: "在 Azure Active Directory B2C 租用戶 hello 類型上的主題"
services: active-directory-b2c
documentationcenter: 
author: gsacavdm
manager: krassk
editor: bryanla
ms.assetid: 8a0644da-b825-4edc-8ce9-541c3c976afb
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: gsacavdm
ms.openlocfilehash: d382921fe9d62183b6d52c47d62f952dabd116c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-region-availability--data-residency"></a>Azure Active Directory B2C：區域可用性和資料存留處
區域可用性和資料 residency 是兩個非常不同的概念會分別套用 tooAzure AD B2C 於 Azure hello 其餘部分。 本文將說明這些兩個概念的 hello 差異，並比較它們應如何套用與 Azure AD B2C tooAzure。

## <a name="summary"></a>摘要
是 azure AD B2C**上市全球**以 hello 選項**在美國和歐洲的資料 residency**。

## <a name="concepts"></a>概念
* **區域可用性**參考 toowhere 服務是可供使用。
* **資料 residency**參考 toowhere 使用者資料會儲存。

## <a name="region-availability"></a>區域可用性
Azure AD B2C 全球皆可使用透過 hello Azure 公用雲端。 

這不同於 hello 模型大部分其他 Azure 服務後續的結合資料 residency 與可用性。 您可以看到這兩個 Azure 中的範例[產品可用的地區](https://azure.microsoft.com/regions/services/)頁面和 hello [Active Directory B2C 定價計算機](https://azure.microsoft.com/pricing/details/active-directory-b2c/)。

## <a name="data-residency"></a>資料存留處
Azure AD B2C 會將使用者資料儲存在美國或歐洲。

資料存留處是根據[建立 Azure AD B2C 租用戶](active-directory-b2c-get-started.md)時所選取的國家/地區來決定。

![預覽租用戶的螢幕擷取畫面](./media/active-directory-b2c-reference-tenant-type/data-residency-b2c-tenant.png)

資料所在 hello 美國境內取得下列國家/地區的 hello:

> 美國、加拿大、哥斯大黎加、多明尼加共和國、薩爾瓦多、瓜地馬拉、墨西哥、巴拿馬、波多黎各和千里達及托巴哥

資料會遵循國家/地區的 hello 位於歐洲：

> 阿爾及利亞、奧地利、亞塞拜然、巴林、白俄羅斯、比利時、保加利亞、克羅埃西亞、賽普勒斯、捷克共和國、丹麥、埃及、愛沙尼亞、芬蘭、法國、德國、希臘、匈牙利、冰島、愛爾蘭、以色列、義大利、約旦、哈薩克、肯亞、科威特、拉脫維亞、黎巴嫩、列支敦斯登、立陶宛、盧森堡、馬其頓 (FYRO)、馬爾他、蒙特內哥羅、摩洛哥、荷蘭、奈及利亞、挪威、阿曼、巴基斯坦、波蘭、葡萄牙、卡達、羅馬尼亞、俄羅斯、沙烏地阿拉伯、塞爾維亞、斯洛伐克、斯洛維尼亞、南非、西班牙、瑞典、瑞士、突尼西亞、土耳其、烏克蘭、阿拉伯聯合大公國和英國。

hello 剩餘國家 （地區） 是 hello 處理序正在加入 toohello 清單中。  現在，您仍然可以使用 Azure AD B2C 所挑選的 hello 國家/地區上述任何。

> 阿富汗、阿根廷、澳洲、巴西、智利、哥倫比亞、厄瓜多、香港特別行政區、印度、印尼、伊拉克、日本、韓國、馬來西亞、紐西蘭、巴拉圭、祕魯、菲律賓、新加坡、斯里蘭卡、台灣、泰國、烏拉圭和委內瑞拉。

## <a name="preview-tenant"></a>預覽租用戶
如果您已在 Azure AD B2C 的預覽期間建立 B2C 租用戶，您的 [租用戶類型] 可能會顯示為 [預覽租用戶]。 如果這是 hello 情況下，您必須使用您的租用戶，僅適用於開發和測試用途，不能用於實際執行應用程式。

> [!IMPORTANT]
> 沒有從預覽 B2C 租用戶 tooa 生產調整 B2C 租用戶移轉路徑。 請注意，那里已知問題時刪除預覽 B2C 租用戶和重新建立生產調整 B2C 租用戶與 hello 相同的網域名稱。 您有 toocreate 生產調整 B2C 租用戶和不同的網域名稱。


![預覽租用戶的螢幕擷取畫面](./media/active-directory-b2c-reference-tenant-type/preview-b2c-tenant.png)
