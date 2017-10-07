---
title: "aaaWindows 10 漫遊設定參考 |Microsoft 文件"
description: "所有的 hello 設定將會漫遊或在 Windows 10 中備份的完整清單。"
services: active-directory
keywords: "企業狀態漫遊, windows 雲端"
documentationcenter: 
author: tanning
manager: femila
editor: curtand
ms.assetid: 17cffc3e-2928-4235-91f7-a685bd6bdcbf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: 381e2220b698bb0e477c207984ff96c03ed132ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="windows-10-roaming-settings-reference"></a>Windows 10 漫遊設定參考
hello 以下是所有 hello 設定將會漫遊或在 Windows 10 中備份的完整清單。 

## <a name="devices-and-endpoints"></a>裝置和端點
請參閱下表摘要 hello 裝置和備份、 同步 hello 處理所支援的帳戶類型的 hello 和還原 Windows 10 中的架構。

| 帳戶類型和作業 | 桌上型 | 行動 |
| --- | --- | --- |
| Azure Active Directory：同步處理 |是 |否 |
| Azure Active Directory：備份/還原 |否 |否 |
| Microsoft 帳戶：同步處理 |是 |是 |
| Microsoft 帳戶：備份/還原 |否 |是 |

## <a name="what-is-backup"></a>什麼是備份？
根據預設，通常同步 Windows 設定，但某些設定只能備份，例如 hello 裝置上安裝應用程式清單。 備份僅適用於行動裝置，目前不適用企業狀態漫遊使用者。 備份使用 Microsoft 帳戶，並將 hello 設定和應用程式資料儲存到 OneDrive。 如果使用者停用同步處理 hello 裝置上使用 hello 設定應用程式，通常是同步的應用程式資料會成為備份只。 備份資料只在透過 hello 還原作業期間第一次執行經驗來新增裝置 hello 中存取。 備份可以停用透過 hello 裝置設定，並可以受到管理，並且透過 hello 使用者的 OneDrive 帳戶刪除。

## <a name="windows-settings-overview"></a>Windows 設定概觀
hello 下列設定群組可供使用者 tooenable/停用設定同步處理 Windows 10 裝置上。

* 佈景主題：桌面背景、使用者圖格、工作列位置等 
* Internet Explorer 設定：瀏覽歷程記錄、輸入的 URL、我的最愛等 
* 密碼： [Windows 認證保險箱](https://technet.microsoft.com/library/jj554668.aspx)，包括 Wi-Fi 設定檔 
* 語言喜好設定：拼字檢查字典、系統語言設定 
* 輕鬆存取：朗讀程式、螢幕小鍵盤、放大鏡 
* 其他 Windows 設定：請參閱 Windows 設定詳細資料

![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-individual-sync-settings.png)

使用者可以透過 Edge 瀏覽器 [設定] 功能表選項，啟用或停用 Edge 瀏覽器設定群組同步處理 (我的最愛，讀取清單)。

![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-sync-content.png)

## <a name="windows-settings-details"></a>Windows 設定詳細資料
在下表的 hello，hello 設定群組的資料行中的其他項目是指可以停用移 tooSettings toosettings > 帳戶 > 同步您的設定 > 其他 Windows 設定。 

Toosettings 和應用程式，可以只停用從同步處理 hello 應用程式本身內，或是停用使用行動裝置管理 (MDM)] 或 [群組原則設定的 hello 整個裝置的同步處理，請參閱內部 hello 設定群組的資料行中的項目。
不會漫遊的設定或同步處理將不屬於 tooa 群組。

| 設定 | 桌上型 | 行動 | 群組 |
| --- | --- | --- | --- |
| **帳戶**：帳戶圖片 |sync |X |佈景主題 |
| **帳戶**：其他帳戶設定 |X |X | |
| **進階行動寬頻**：網際網路連接共用網路名稱 (透過藍牙啟用行動 Wi-Fi 作用區的自動探索) |X |X |密碼 |
| **應用程式資料**：個別應用程式可以同步處理資料 |同步處理備份 |同步處理備份 |內部 |
| **應用程式清單**：已安裝應用程式的清單 |X |backup |其他 |
| **藍牙**：所有藍牙設定 |X |X | |
| **命令提示字元**：命令提示字元「預設值」設定 |sync |X | |
| **認證**：認證保險箱 |sync |sync |password |
| **日期、時間和區域**：自動時間 (網際網路時間同步處理) |sync |sync |語言 |
| **日期、時間和區域**：24 小時制時鐘 |sync |X |語言 |
| **日期、時間和區域**：日期和時間 |sync |X |語言 |
| **日期、時間和區域**：時區 | |X |語言 |
| **日期、時間和區域**：日光節約時間 |sync |X |語言 |
| **日期、時間和區域**：國家/地區 |sync |X |語言 |
| **日期、時間和區域**：一週的第一天 |sync |X |語言 |
| **日期、時間和區域**：區域格式 (地區設定) |sync |X |語言 |
| **日期、時間和區域**：簡短日期 |sync |X |語言 |
| **日期、時間和區域**：完整日期 |sync |X |語言 |
| **日期、時間和區域**：簡短時間 |sync |X |語言 |
| **日期、時間和區域**：完整時間 |sync |X |語言 |
| **桌面個人化**：桌面主題 (背景、系統色彩、預設系統音效、螢幕保護裝置) |sync |X |佈景主題 |
| **桌面個人化**：投影片放映底色圖案 |sync |X |佈景主題 |
| **桌面個人化**：工作列設定 (位置、自動隱藏等) |sync |X |佈景主題 |
| **桌面個人化**：開始畫面版面配置 |X |backup | |
| **裝置**： 共用過，您已連接的印表機|X |X |其他 |
| **Edge 瀏覽器**：閱讀清單 |sync |sync |內部 |
| **Edge 瀏覽器**：我的最愛 |sync |sync |內部 |
| **Edge 瀏覽器**：熱門網站 <sup>[[1]](#footnote-1)</sup> |sync |sync |內部 |
| **Edge 瀏覽器**：輸入的 URL <sup>[[1]](#footnote-1)</sup> |sync |sync |內部 |
| **Edge 瀏覽器**：我的最愛列設定 <sup>[[1]](#footnote-1)</sup> |sync |sync |內部 |
| **Edge 瀏覽器**： 顯示 hello [首頁] 按鈕<sup> [[1]](#footnote-1)</sup> |sync |sync |內部 |
| **Edge 瀏覽器**：封鎖快顯 <sup>[[1]](#footnote-1)</sup> |sync |sync |內部 |
| **Edge 瀏覽器**： 詢問每個下載使用何種 toodo <sup> [[1]](#footnote-1)</sup> |sync |sync |內部 |
| **Edge 瀏覽器**： 提供 toosave 密碼<sup> [[1]](#footnote-1)</sup> |sync |sync |內部 |
| **Edge 瀏覽器**：傳送「不要追蹤」要求 <sup>[[1]](#footnote-1)</sup> |sync |sync |內部 |
| **Edge 瀏覽器**：儲存表單項目 <sup>[[1]](#footnote-1)</sup> |sync |sync |內部 |
| **Edge 瀏覽器**：在我輸入的同時顯示搜尋與網站建議 <sup>[[1]](#footnote-1)</sup> |sync |sync |內部 |
| **Edge 瀏覽器**：Cookie 喜好設定 <sup>[[1]](#footnote-1)</sup> |sync |sync |內部 |
| **Edge 瀏覽器**：讓網站在我的裝置上儲存受保護的媒體授權 <sup>[[1]](#footnote-1)</sup> |sync |sync |內部 |
| **Edge 瀏覽器**：螢幕助讀程式設定 <sup>[[1]](#footnote-1)</sup> |sync |sync |內部 |
| **高對比**：開啟或關閉 |sync |X |輕鬆存取 |
| **高對比**：佈景主題設定 |sync |X |輕鬆存取 |
| **Internet Explorer**：開啟索引標籤 (URL 和標題) |sync |sync |Internet Explorer |
| **Internet Explorer**：閱讀清單 |sync |sync |Internet Explorer |
| **Internet Explorer**：輸入的 URL |sync |sync |Internet Explorer |
| **Internet Explorer**：瀏覽歷程記錄 |sync |sync |Internet Explorer |
| **Internet Explorer**：我的最愛 |sync |sync |Internet Explorer |
| **Internet Explorer**：排除的 URL |sync |sync |Internet Explorer |
| **Internet Explorer**：首頁 |sync |sync |Internet Explorer |
| **Internet Explorer**：網域建議 |sync |sync |Internet Explorer |
| **鍵盤**：使用者可以開啟/關閉螢幕小鍵盤 |sync |X |輕鬆存取 |
| **鍵盤**：開啟相黏鍵 (預設為關閉) |sync |X |輕鬆存取 |
| **鍵盤**：開啟篩選鍵 (預設為關閉) |sync |X |輕鬆存取 |
| **鍵盤**：開啟切換鍵 (預設為關閉) |sync |X |輕鬆存取 |
| **Internet Explorer**：網域語言：中文 (CHS) QWERTY - 啟用自我學習 |sync |X |語言 |
| **語言**：CHS QWERTY - 啟用動態候選項目排名 |sync |X |語言 |
| **語言**：CHS QWERTY - 字元集簡體中文 |sync |X |語言 |
| **語言**：CHS QWERTY - 字元集繁體中文 |sync |X |語言 |
| **語言**：CHS QWERTY - 模糊拼音 |sync |backup |語言 |
| **語言**：CHS QWERTY - 模糊配對 |sync |backup |語言 |
| **語言**：CHS QWERTY - 完整拼音 |sync |X |語言 |
| **語言**：CHS QWERTY - 雙拼音 |sync |X |語言 |
| **語言**：CHS QWERTY - 閱讀自動更正 |sync |X |語言 |
| **語言**：CHS QWERTY - C/E 切換鍵，shift 鍵 |sync |X |語言 |
| **語言**：CHS QWERTY - C/E 切換鍵，Ctrl 鍵 |sync |X |語言 |
| **語言**：CHS WUBI - 單一字元輸入模式 |sync |X |語言 |
| **語言**： 簡體中文 WUBI-顯示 hello 剩餘 hello 候選的編碼 |sync |X |語言 |
| **語言**：CHS WUBI - 4-coding 無效時發出嗶聲 |sync |X |語言 |
| **語言**：CHT 注音符號 - 包括 CJK Ext-A |sync |X |語言 |
| **語言**：日文輸入法 - 預測輸入和自訂文字 |sync |sync |語言 |
| **語言**：韓文 (KOR) 輸入法 |X |X |語言 |
| **語言**：手寫辨識 |X |X |語言 |
| **語言**：語言設定檔 |sync |backup |語言 |
| **語言**：拼字檢查 - 自動校正和反白顯示拼字錯誤 |sync |backup |語言 |
| **語言**：鍵盤的清單 |sync |backup |語言 |
| **鎖定畫面**：所有鎖定畫面設定 |X |X | |
| **放大鏡**：開啟或關閉 (主切換) |X |X |輕鬆存取 |
| **放大鏡**：開啟或關閉反轉色彩 (預設為關閉) |sync |X |輕鬆存取 |
| **[放大鏡]**： 追蹤-遵循 hello 鍵盤焦點 |sync |X |輕鬆存取 |
| **[放大鏡]**： 追蹤-遵循 hello 滑鼠游標 |sync |X |輕鬆存取 |
| **放大鏡**：當使用者登入時啟動 (預設為關閉) |sync |X |輕鬆存取 |
| **滑鼠**： 將滑鼠游標的 hello 大小變更 |sync |X |其他 |
| **滑鼠**： 將滑鼠游標 hello 色彩變更 |sync |X |其他 |
| **滑鼠**：所有其他設定 |X |X | |
| **朗讀程式**：快速啟動 |sync |X |輕鬆存取 |
| **朗讀程式**：使用者可以變更朗讀程式朗讀音調 |sync |X |輕鬆存取 |
| **朗讀程式**：使用者可以開啟或關閉朗讀程式對於常用項目的閱讀提示 (預設為開啟) |sync |X |輕鬆存取 |
| **朗讀程式**：使用者可以開啟或關閉是否聽到輸入的字元 (預設為開啟) |sync |X |輕鬆存取 |
| **朗讀程式**：使用者可以開啟或關閉是否聽到輸入的文字 (預設為開啟) |sync |X |輕鬆存取 |
| **朗讀程式**：在朗讀程式之後有插入游標 (預設為開啟) |sync |X |輕鬆存取 |
| **朗讀程式**：啟用朗讀程式的游標視覺反白顯示 (預設為開啟) |sync |X |輕鬆存取 |
| **朗讀程式**：播放音訊提示 (預設為開啟) |sync |X |輕鬆存取 |
| **[朗讀程式]**： 啟動 hello 觸控鍵盤上的按 enter 鍵時將手指 （預設為關閉） |sync |X |輕鬆存取 |
| **輕鬆存取**： 設定 hello 閃爍的游標 hello 粗細 |sync |X |輕鬆存取 |
| **輕鬆存取**：移除背景影像 (預設為關閉) |sync |X |輕鬆存取 |
| **電源與睡眠**：所有設定 |X |X | |
| **開始畫面個人化**：輔色 (僅限手機) |X |sync |佈景主題 |
| **輸入**：拼字檢查字典 |sync |backup |語言 |
| **輸入**：自動校正拼錯文字 |sync |backup |語言 |
| **輸入**：醒目提示拼錯的單字 |sync |backup |語言 |
| **輸入**：在我輸入時顯示文字建議 |sync |backup |語言 |
| **輸入**：在我選擇文字建議後加上空格 |sync |backup |語言 |
| **輸入**： 加上句號之後我點選 hello 空格鍵 |sync |backup |語言 |
| **輸入**: hello 的每個句子的第一個字母大寫 |sync |backup |語言 |
| **輸入**：在我點兩下 Shift 鍵時全部使用大寫字母 |sync |backup |語言 |
| **輸入**：在我輸入時播放按鍵音 |sync |backup |語言 |
| **輸入**：觸控式鍵盤的個人化資料 |sync |backup |語言 |
| **Wi-Fi**：Wi-Fi 設定檔 (僅限 WPA) |sync |sync |密碼 |

###### <a name="footnote-1"></a>註腳 1
最低支援的 OS 版本為 Windows Creators Update (組建 15063)。 

## <a name="related-topics"></a>相關主題
* [企業狀態漫遊概觀](active-directory-windows-enterprise-state-roaming-overview.md)
* [在 Azure Active Directory 中啟用企業狀態漫遊](active-directory-windows-enterprise-state-roaming-enable.md)
* [設定和資料漫遊常見問題集](active-directory-windows-enterprise-state-roaming-faqs.md)
* [設定同步處理的群組原則和 MDM 設定](active-directory-windows-enterprise-state-roaming-group-policy-settings.md)
* [疑難排解](active-directory-windows-enterprise-state-roaming-troubleshooting.md)
