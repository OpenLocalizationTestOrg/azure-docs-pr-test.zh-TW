---
title: "aaaAzure CDN 規則引擎比對條件 |Microsoft 文件"
description: "Azure CDN 規則引擎比對條件和功能的參考文件。"
services: cdn
documentationcenter: 
author: Lichard
manager: akucer
editor: 
ms.assetid: 669ef140-a6dd-4b62-9b9d-3f375a14215e
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: 5e79f8f0c75a646e13bf315c492b9f2a9defc396
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine-match-conditions"></a>Azure CDN 規則引擎比對條件
此主題清單的詳細的描述 hello 可比對條件的 Azure 內容傳遞網路 (CDN)[規則引擎](cdn-rules-engine.md)。

規則的 hello 第二個部分是 hello 比對條件。 比對條件會識別特定類型的要求，系統將針對這類要求執行一組功能。

例如，它可能是使用的 toofilter 要求內容的特定位置，從特定的 IP 位址或國家/地區，或標頭資訊所產生的要求。

## <a name="always"></a>一律

hello 永遠比對條件是設計的 tooapply 功能 tooall 要求的設定預設值。

## <a name="device"></a>裝置

hello 裝置符合條件來識別從行動裝置根據其內容所提出的要求。  行動裝置偵測可以透過 [WURFL](http://wurfl.sourceforge.net/) 達成。  以下列出 WURFL 功能和其 CDN 規則引擎變數。

> [!NOTE] 
> 支援下列的 hello 變數 hello**修改用戶端要求標頭**和**修改用戶端的回應標頭**功能。

功能 | 變數 | 說明 | 範例值
-----------|----------|-------------|----------------
品牌名稱 | %{wurfl_cap_brand_name} | 表示 hello 裝置 hello 品牌名稱的字串。 | Samsung
裝置作業系統 | %{wurfl_cap_device_os} | 字串，表示 hello 裝置上安裝的 hello 作業系統。 | iOS
裝置作業系統版本 | %{wurfl_cap_device_os_version} | 表示 hello hello hello 裝置上安裝作業系統版本號碼的字串。 | 1.0.1
雙向 | %{wurfl_cap_dual_orientation} | 布林值，指出 hello 裝置是否支援雙重方向。 | true
HTML 慣用 DTD | %{wurfl_cap_html_preferred_dtd} | 字串，表示 hello 行動裝置的慣用的文件類型定義 (DTD) HTML 內容。 | 無<br/>xhtml_basic<br/>html5
內嵌影像 | %{wurfl_cap_image_inlining} | 布林值，指出是否 hello 裝置支援 Base64 編碼的影像。 | false
是 Android | %{wurfl_vcap_is_android} | 布林值，指出 hello 裝置是否使用 hello Android 作業系統。 | true
是 iOS | %{wurfl_vcap_is_ios} | 布林值，指出 hello 裝置是否使用 iOS。 | false
是智慧型電視 | %{wurfl_cap_is_smarttv} | 布林值，指出 hello 裝置是否為智慧電視。 | false
是智慧型手機 | %{wurfl_vcap_is_smartphone} | 布林值，指出 hello 裝置是否在智慧型手機。 | true
是平板電腦 | %{wurfl_cap_is_tablet} | 布林值，指出 hello 裝置是否在平板電腦。 這是獨立於作業系統的描述。 | true
是無線裝置 | %{wurfl_cap_is_wireless_device} | 布林值，指出是否 hello 裝置將被視為無線裝置。 | true
行銷名稱 | %{wurfl_cap_marketing_name} | 表示 hello 裝置行銷名稱的字串。 | BlackBerry 8100 Pearl
行動瀏覽器 | %{wurfl_cap_mobile_browser} | 字串，表示 hello 瀏覽器使用 toorequest hello 裝置內容。 | Chrome
行動瀏覽器版本 | %{wurfl_cap_mobile_browser_version} | 字串，表示 hello hello 瀏覽器版本使用 toorequest hello 裝置內容。 | 31
模型名稱 | %{wurfl_cap_model_name} | 表示 hello 裝置的型號名稱的字串。 | s3
漸進式下載 | %{wurfl_cap_progressive_download} | 布林值，指出是否 hello 裝置支援播放音訊/視訊 hello 仍在下載時。 | true
發行日期 | %{wurfl_cap_release_date} | 字串，表示 hello 年和月在哪一個 hello 裝置已加入 toohello WURFL 資料庫。<br/><br/>格式： `yyyy_mm` | 2013_december
解析高度 | %{wurfl_cap_resolution_height} | 整數，表示裝置 hello 的高度，單位為像素為單位。 | 768
解析寬度 | %{wurfl_cap_resolution_width} | 整數，指出裝置 hello 的寬度，以像素為單位。 | 1024


## <a name="location"></a>位置

這些符合條件設計的 tooidentify 要求根據 hello 要求者的位置。

名稱 | 目的
-----|--------
AS 號碼 | 識別源自特定網路的要求。
國家 (地區) | 識別指定 hello 源自要求國家 （地區)。


## <a name="origin"></a>來源

這些符合條件會設計的 tooidentify 要求該點 tooCDN 儲存體或客戶原始伺服器。

名稱 | 目的
-----|--------
CDN 原點 | 識別對儲存於 CDN 儲存體之內容的要求。
客戶原點 | 識別對儲存於特定客戶原始伺服器上之內容的要求。


## <a name="request"></a>要求

這些符合條件會根據其內容的設計的 tooidentify 要求。

名稱 | 目的
-----|--------
用戶端 IP 位址 | 識別源自特定 IP 位址的要求。
Cookie 參數 | 檢查 hello 與 hello 指定每個要求相關聯的 cookie 值。
Cookie 參數 Regex | 檢查每個要求的 hello 與相關聯的 hello cookie 指定規則運算式。
邊緣 Cname | 識別點 tooa 特定邊緣 CNAME 的要求。
轉介網域 | 會從所參考的要求識別 hello 指定 hostname(s)。
要求標頭常值 | 識別包含指定的 hello 的要求標頭集合 tooa 指定值。
要求標頭 Regex | 識別包含指定的 hello 的要求標頭符合 hello 組 tooa 值指定規則運算式。
要求標頭萬用字元 | 識別包含指定的 hello 的要求標頭設定 tooa 值符合指定的模式的 hello。
要求方法 | 依其 HTTP 方法來識別要求。
要求配置 | 依其 HTTP 通訊協定來識別要求。

## <a name="url"></a>URL

這些符合條件會根據其 Url 的設計的 tooidentify 要求。

名稱 | 目的
-----|--------
URL 路徑目錄 | 依其相對路徑來識別要求。
URL 路徑的副檔名 | 依其副檔名來識別要求。
URL 路徑的檔案名稱 | 依其檔案名稱來識別要求。
URL 路徑常值 | 會比較要求的相對路徑 toohello 指定的值。
URL 路徑 Regex | 會比較要求的相對路徑 toohello 指定規則運算式。
URL 路徑萬用字元 | 會比較要求的相對路徑 toohello 指定的模式。
URL 查詢常值 | 會比較要求查詢字串 toohello 指定指定的值。
URL 查詢參數 | 識別包含 hello 指定的查詢字串參數設定 tooa 值符合指定的模式的要求。
URL 查詢 Regex | 識別包含 hello 指定的查詢字串參數設定 tooa 值符合指定之規則運算式的要求。
URL 查詢萬用字元 | 比較 hello 指定針對 hello 要求查詢字串值。


## <a name="next-steps"></a>後續步驟
* [Azure CDN 概觀](cdn-overview.md)
* [規則引擎參考](cdn-rules-engine-reference.md)
* [規則引擎條件運算式](cdn-rules-engine-reference-conditional-expressions.md)
* [規則引擎功能](cdn-rules-engine-reference-features.md)
* [覆寫使用 hello 規則引擎的預設 HTTP 行為](cdn-rules-engine.md)

