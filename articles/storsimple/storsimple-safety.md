---
title: "StorSimple 裝置的 aaaSafety |Microsoft 文件"
description: "描述安全性慣例、 指導方針與考量，並說明 toosafely 安裝及操作您的 StorSimple 裝置的方式。"
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: dae6d535-1ca2-4d2b-b221-6819043aa068
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/16/2016
ms.author: alkohli
ms.openlocfilehash: cb5e24582c0391d7b68cb5c74586815af4b58a8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="safely-install-and-operate-your-storsimple-device"></a>安全地安裝和操作您的 StorSimple 裝置
![警告圖示](./media/storsimple-safety/IC740879.png)
 ![閱讀安全性注意事項圖示](./media/storsimple-safety/IC740885.png) **讀取的安全性和健全狀況資訊**

讀取所有 hello 安全和本文適用於 tooyour Microsoft Azure StorSimple 裝置的健全狀況資訊。 保留所有 hello 書面的指南，隨附於您的 StorSimple 裝置，供日後參考。 失敗 toofollow 指示並正確設定、 使用及保護本產品可以提高嚴重傷害或死亡，或損壞 toohello 裝置或裝置 hello 風險。 [本指南的可下載版本](http://www.microsoft.com/download/details.aspx?id=44233) 也可供使用。

## <a name="safety-icon-conventions"></a>安全性圖示慣例
以下是您會發現，當您檢閱設定和執行您的 Microsoft Azure StorSimple 裝置時，觀察到的 hello 安全預防措施 toobe hello 圖示。

| 圖示 | 說明 |
|:--- |:--- |
| ![危險圖示](./media/storsimple-safety/IC740879.png) **危險！** |指出危險的情況，如果無法避免，將會導致死亡或嚴重傷害。 此一指示文字是 toobe 有限 toohello 最危險的狀況。 |
| ![警告圖示](./media/storsimple-safety/IC740879.png) **警告！** |指出危險的情況，如果無法避免，可能會導致死亡或嚴重傷害。 |
| ![警告圖示](./media/storsimple-safety/IC740879.png) **小心！** |指出危險的情況，如果無法避免，可能會導致次要或中度的傷害。 |
| ![注意事項圖示](./media/storsimple-safety/IC740881.png) **注意事項：** |表示重要資訊，但與危險無關。 |
| ![電擊圖示](./media/storsimple-safety/IC740882.png) **電擊危險** |高電壓 |
| ![超重圖示](./media/storsimple-safety/IC740883.png) **重量** | |
| ![沒有使用者可自行維修零件圖示](./media/storsimple-safety/IC740879.png) **沒有使用者可自行維修的零件** |除非受過適當訓練，否則請勿觸碰。 |
| ![閱讀安全性注意事項圖示](./media/storsimple-safety/IC740885.png)**請先閱讀所有指示** | |
| ![傾倒危險圖示](./media/storsimple-safety/IC740886.png) **傾倒危險** | |

## <a name="handling-precautions"></a>處理預防措施
![警告圖示](./media/storsimple-safety/IC740879.png) ![超重圖示](./media/storsimple-safety/IC740883.png) **警告！** 

tooreduce hello 造成傷害的風險：

* 完全設定的機箱重量向上 too32 公斤 （70 磅）;請勿嘗試 toolift 它自己。
* 之前移動 hello 機箱，務必確定兩個人員是可用 toohandle hello 權數。 請注意，一個人嘗試 toolift 此重量受傷。
* 不提起 hello 機箱 hello 電源和冷卻模組 (Pcm) 上的 hello 控點位於 hello 背面固定的 hello 單位。 這些不是設計 tootake hello 權數。

## <a name="connection-precautions"></a>連接預防措施
![Warning Icon](./media/storsimple-safety/IC740879.png) ![Electrical Shock Icon](./media/storsimple-safety/IC740882.png) **警告！**

tooreduce hello 發生傷害、 電擊或死亡的可能性：

* 由多個 AC 來源提供電源時，請中斷所有供應電源以達完全隔離。
* 在移動它之前，或如果您認為裝置已損壞以任何方式永久拔下 hello 單位。
* 提供安全電子接地連線 toohello 電源供應器線。 確認 hello 機箱的 hello 通電之前套用電源符合 hello 國家和當地要求。
* 請確定 hello 電源連線一律中斷連線之前 toohello 卸下 PCM 從 hello 機箱。
* 假設 hello 上 hello 電源線的插頭是主要的 hello 中斷連線的裝置，請確定 hello 插座位於 hello 設備附近並可輕易存取。

![Warning Icon](./media/storsimple-safety/IC740879.png) ![Electrical Shock Icon](./media/storsimple-safety/IC740882.png) **警告！**

tooreduce hello 發生過熱或火災的 hello 電子連線的可能性：

* 提供的適當電源來源具有電路超載保護 toomeet hello hello 技術規格中詳述的需求。
* 請勿使用分叉的電源線 ("Y" 引線)。
* 應移除 toocomply 與適用的安全、 放射性和熱力需求，無封面及所有機槽都必須填入外掛模組或磁碟機空殼。
* 請 hello 設備用於 hello 製造商所指定的方式。 如果未指定 hello 製造商的方式使用此設備，可能會減損 hello hello 設備所提供的保護。

![注意事項圖示](./media/storsimple-safety/IC740881.png) **注意事項：**

設備與 tooprevent 產品損毀 hello 正常運作：

* 在 hello hello 裝置背面的 hello RJ45 連接埠是只將乙太網路連線。 這些不能連接的 tooa 電信網路。
* 是確定 tooinstall hello 裝置可以容納由前至後冷卻設計的機架中。
* 所有外掛模組和盲屬於 hello 系統機箱。 立即加入替代項目時必須只能將其移除。 必須執行 hello 系統，不所有模組或空殼的位置。

## <a name="rack-system-precautions"></a>機架系統預防措施
hello 下列安全需求時，必須考慮掛接在機架封包中的 hello 裝置。

![警告圖示](./media/storsimple-safety/IC740879.png) ![傾倒危險圖示](./media/storsimple-safety/IC740886.png) **警告！**

提示，以透過造成傷害 tooreduce hello 可能性：

* hello 機架設計應支援 hello 總 hello 安裝機箱重量，而且應具備適當的穩定功能適合 tooprevent hello 機架傾倒或被推倒在安裝或正常使用期間從。
* 載入機架時, 填滿從 hello 下 hello 機架和 hello 由上而下清空。
* 不滑出 hello 機架在時間 tooavoid hello hello 機架傾倒的危險的多個機箱。

![Warning Icon](./media/storsimple-safety/IC740879.png) ![Electrical Shock Icon](./media/storsimple-safety/IC740882.png) **警告！**

tooreduce hello 發生傷害、 電擊或死亡的可能性：

* hello 機架應有安全的配電系統。 它必須提供 hello 機箱的電流保護，而且必須未多載所安裝機箱的 hello 總數。 應該要觀察 hello 名牌上顯示的 hello 電力消耗評等。
* hello 配電系統必須 hello 機架中的每個機箱提供可靠的接地。
* hello 設計 hello 配電系統必須將納入考量 hello 總接地外洩目前從所有機箱中的所有電源供應器。 請注意，每個機箱中的每個電源供應器都有最大值 1.0 mA，60 Hz、264 伏特的漏地電流。 hello 機架可能必須標示為 「 HIGH LEAKAGE CURRENT。 在連接供應電源之前，接地 (接地) 是不可或缺的。
* hello 機架，hello 機箱設定時，必須符合 UL 60950-1 和 IEC 60950-1/EN 60950-1 的 hello 安全需求。

![注意事項圖示](./media/storsimple-safety/IC740881.png) **注意事項：**

適當的機架系統冷卻 hello:

* 請確定 hello 機架設計列入考量 hello 最大機箱作業周圍溫度攝氏 35 度 （華氏 95 度）。
* hello 系統以低壓、 尾段排氣安裝操作 （背壓建立機架門和障礙物所產生不 tooexceed 5 帕 [0.5 mm 水位計]）。

## <a name="power-cooling-module-pcm-precautions"></a>電源冷卻模組 (PCM) 預防措施
hello 裝置是設計的 toooperate 搭配兩個 Pcm。 每個 Pcm hello 有電源供應器和雙軸風扇。 在嚴重狀況下，hello 系統允許一個電源供應器同時繼續正常運作所發生的失敗。 兩個 PCM (因此和電源供應器) 必須一律安裝。 單一 PCM 不會提供備援電源。 因此，即使一個 PCM hello 失敗可能會導致停機時間或資料遺失。

![Warning Icon](./media/storsimple-safety/IC740879.png) ![Electrical Shock Icon](./media/storsimple-safety/IC740882.png) **警告！**

tooreduce hello 發生傷害、 電擊或死亡的可能性：

* 不要移除 hello PCM hello 涵蓋。 沒有內部觸電的危險。 tooreturn hello PCM 並取得替換品，[連絡 Microsoft 支援服務](storsimple-contact-microsoft-support.md)。

![注意事項圖示](./media/storsimple-safety/IC740881.png) **注意事項：**

設備與 tooprevent 產品損毀 hello 正常運作：

* 您必須取代 hello 24 小時內失敗的 PCM。 卸下 PCM 以便更換之後，必須移除後 10 分鐘內完成 hello 取代。
* 請勿移除 PCM，除非可以立即安裝替代項目。 hello 機箱不必須沒有備妥所有模組來操作。

## <a name="electrostatic-discharge-esd-precautions"></a>靜電放電 (ESD) 預防措施
![注意事項圖示](./media/storsimple-safety/IC740881.png) **注意事項：**

觀察下列 ESD 相關預防措施 hello。

* 請確定您已安裝並檢查適合的抗靜電腕或踝帶。
* 處理模組和元件時，請觀察所有傳統的 ESD 預防措施。
* 避免接觸後擋板元件和模組連接器。
* 瑕疵擔保未涵蓋 ESD 損害。

## <a name="battery-disposal-precautions"></a>電池處置預防措施
hello 電源供應器在暫時、 短期斷電期間所使用記憶體的特殊電池 tooprotect hello 的內容。 hello 電池的固定於 hello PCM 中。 保留 hello 下列幾點 hello 電池相關的資訊。

![警告圖示](./media/storsimple-safety/IC740879.png) **警告！**

tooreduce hello shorts、 火災、 爆炸、 起火或死亡的風險：

* 根據國家/地區規定處置使用過的電池。
* 請勿拆解、損毀或加熱至高於攝氏 60 度 (華氏 140 度) 或焚毀。 取代提供電池 hello PCM 電池。 使用另一個電池可能有火災或爆炸的風險。
* 如果從 hello 電源供應器卸下電池 hello 使用蓋。

![注意事項圖示](./media/storsimple-safety/IC740881.png) **注意事項：**

當運送或 hello 電池的空運，請遵循 hello IATA 鋰電池指南文件位於[http://www.iata.org/whatwedo/cargo/dgr/Pages/lithium-batteries.aspx](http://www.iata.org/whatwedo/cargo/dgr/Pages/lithium-batteries.aspx)

您已檢閱這些安全注意事項後，hello 下一個步驟是 toounpack，機架並連接裝置纜線。

## <a name="next-steps"></a>後續步驟
* 8100 裝置跳過[安裝 StorSimple 8100 裝置](storsimple-8100-hardware-installation.md)。
* 8600 裝置跳過[安裝 StorSimple 8600 裝置](storsimple-8600-hardware-installation.md)。

