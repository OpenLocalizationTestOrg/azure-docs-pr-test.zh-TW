---
title: "串流分析：替換輸入和輸出的登入認證 | Microsoft Docs"
description: "了解如何 tooupdate hello 認證的資料流分析的輸入和輸出。"
keywords: "登入認證"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 42ae83e1-cd33-49bb-a455-a39a7c151ea4
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: ac2374c539012b66ab390656c5750024e02f6bdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="rotate-login-credentials-for-inputs-and-outputs-in-stream-analytics-jobs"></a>在串流分析工作中替換輸入和輸出的登入認證
## <a name="abstract"></a>摘要
Azure Stream Analytics 目前不允許取代 hello 認證於輸入/輸出 hello 作業執行時。

雖然 Azure Stream Analytics 支援繼續從最後的輸出工作，我們想 tooshare hello 整個程序將停止的 hello 與 hello 工作的開始和旋轉 hello 登入認證之間的 hello 延隔時間降到最低。

## <a name="part-1---prepare-hello-new-set-of-credentials"></a>第 1 部-準備 hello 組新的認證：
這部分適用 toohello 後面輸入/輸出：

* Blob 儲存體
* 事件中樞
* SQL Database
* 資料表儲存體

針對其他的輸入/輸出，請參考第 2 部分。

### <a name="blob-storagetable-storage"></a>Blob 儲存體/資料表儲存體 
1. Hello Azure 管理入口網站中上移 toohello 儲存副檔名：  
   ![graphic1][graphic1]
2. 找出您的工作所使用的 hello 儲存體，並移入它：  
   ![graphic2][graphic2]
3. 按一下 hello 管理存取金鑰的命令：  
   ![graphic3][graphic3]
4. Hello 主要存取金鑰和次要存取金鑰，hello 之間**挑選其中一個不由您的工作 hello**。
5. 按重新產生：  
   ![graphic4][graphic4]
6. 複製 hello 新產生的金鑰：  
   ![graphic5][graphic5]
7. 繼續 tooPart 2。

### <a name="event-hubs"></a>事件中樞
1. Hello Azure 管理入口網站中上移 toohello 服務匯流排延伸模組：  
   ![graphic6][graphic6]
2. 找出 hello 您的工作所使用的服務匯流排命名空間，並將它：  
   ![graphic7][graphic7]
3. 如果您的工作會使用 hello 服務匯流排命名空間上的共用的存取原則，跳 toostep 6  
4. 請移 toohello 事件中樞 索引標籤：  
   ![graphic8][graphic8]
5. 找出 hello 您的工作所使用的事件中樞，並將它：  
   ![graphic9][graphic9]
6. 請移 toohello 設定 索引標籤：  
   ![graphic10][graphic10]
7. 上 hello 原則名稱 下拉式清單中，找出您的工作所使用的 hello 共用存取原則：  
   ![graphic11][graphic11]
8. Hello 主索引鍵與 hello 次要的索引鍵之間**挑選其中一個不由您的工作 hello**。  
9. 按重新產生：  
   ![graphic12][graphic12]
10. 複製 hello 新產生的金鑰：  
   ![graphic13][graphic13]
11. 繼續 tooPart 2。  

### <a name="sql-database"></a>SQL Database
> [!NOTE]
> 注意： 您需要 tooconnect toohello SQL Database 服務。 我們 tooshow toodo 此使用 hello 上的管理體驗如何 hello Azure 管理入口網站，但您可以選擇 toouse SQL Server Management Studio 等某些用戶端工具以及。
>
> 

1. Hello Azure 管理入口網站中上移 toohello SQL 資料庫的擴充功能：  
   ![graphic14][graphic14]
2. 找出您的工作所使用的 SQL 資料庫 hello 和**hello 伺服器上按一下**相同連結上 hello 行：  
   ![graphic15][graphic15]
3. 按一下 hello 管理命令：  
   ![graphic16][graphic16]
4. 輸入主要資料庫：  
   ![graphic17][graphic17]
5. 輸入使用者名稱和密碼，然後按一下 [登入]：  
   ![graphic18][graphic18]
6. 按一下 [新增查閱]：  
   ![graphic19][graphic19]
7. 型別在下列查詢取代 < login_name > 與您的使用者名稱和取代 hello<enterStrongPasswordHere>使用新的密碼：  
   `CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>'`
8. 按一下 [執行]：  
   ![graphic20][graphic20]
9. 返回 toostep 2，這次按一下 hello 資料庫：  
   ![graphic21][graphic21]
10. 按一下 hello 管理命令：  
   ![graphic22][graphic22]
11. 輸入使用者名稱和密碼，然後按一下 [登入]：  
   ![graphic23][graphic23]
12. 按一下 [新增查閱]：  
   ![graphic24][graphic24]
13. 輸入下列查詢取代 < 使用者名稱 > 想 tooidentify 所用的名稱與 hello hello 這個資料庫內容中的此登入 (您可以提供 hello 相同的值指定給資料庫的 < login_name >，例如)，並以取代 < login_name >新的使用者名稱：  
   `CREATE USER <user_name> FROM LOGIN <login_name>`
14. 按一下 [執行]：  
   ![graphic25][graphic25]
15. 您現在應該提供您新的使用者以 hello 相同角色與您的原始使用者的權限。
16. 繼續 tooPart 2。

## <a name="part-2-stopping-hello-stream-analytics-job"></a>第 2 部分： 停止 hello 串流分析工作
1. Hello Azure 管理入口網站中上移 toohello 資料流分析擴充功能：  
   ![graphic26][graphic26]
2. 找出您的工作，然後進到裡面：   
   ![graphic27][graphic27]
3. 前往 toohello 輸入 索引標籤或 hello 輸出索引標籤，根據是否輪替 hello 認證輸入或輸出。  
   ![graphic28][graphic28]
4. 按一下 hello 停止命令，並確認 hello 作業已停止：  
   ![graphic29][graphic29]等候 hello 作業 toostop。
5. 找出 hello 輸入/輸出要 toorotate 認證並移到其中：  
   ![graphic30][graphic30]
6. 繼續 tooPart 3。

## <a name="part-3-editing-hello-credentials-on-hello-stream-analytics-job"></a>第 3 部分： Hello 串流分析工作上，編輯 hello 認證
### <a name="blob-storagetable-storage"></a>Blob 儲存體/資料表儲存體 
1. 尋找 hello 儲存體帳戶金鑰 欄位，並貼上您新產生的金鑰：  
   ![graphic31][graphic31]
2. 按一下 hello 儲存 命令，並確認 儲存變更：  
   ![graphic32][graphic32]
3. 當您儲存所做的變更時，系統會自動測試連線，以保證萬無一失。
4. 繼續 tooPart 4。

### <a name="event-hubs"></a>事件中樞
1. 找出 hello 事件中樞原則機碼欄位，並將新產生的金鑰貼到它：  
   ![graphic33][graphic33]
2. 按一下 hello 儲存 命令，並確認 儲存變更：  
   ![graphic34][graphic34]
3. 當您儲存所做的變更時，系統會自動測試連線，以保證萬無一失。
4. 繼續 tooPart 4。

### <a name="power-bi"></a>Power BI
1. 按一下 hello 更新授權：  

   ![graphic35][graphic35]
2. 您會收到下列確認 hello:  

   ![graphic36][graphic36]
3. 按一下 hello 儲存 命令，並確認 儲存變更：  
   ![graphic37][graphic37]
4. 當您儲存所做的變更時，系統會自動測試連線，以保證萬無一失。
5. 繼續 tooPart 4。

### <a name="sql-database"></a>SQL Database
1. 尋找 hello 使用者名稱和密碼的欄位，並將您新建立的認證集貼到它們：  
   ![graphic38][graphic38]
2. 按一下 hello 儲存 命令，並確認 儲存變更：  
   ![graphic39][graphic39]
3. 當您儲存所做的變更時，系統會自動測試連線，以保證萬無一失。  
4. 繼續 tooPart 4。

## <a name="part-4-starting-your-job-from-last-stopped-time"></a>第 4 部分：從上次停止的時間開始您的工作
1. 離開 hello 輸入/輸出：  
   ![graphic40][graphic40]
2. 按一下 hello 啟動命令：  
   ![graphic41][graphic41]
3. 挑選 hello 上次停止時間，然後按一下 確定:  
   ![graphic42][graphic42]
4. 繼續 tooPart 5。  

## <a name="part-5-removing-hello-old-set-of-credentials"></a>第 5 部分： 移除 hello 舊一組認證
這部分適用 toohello 後面輸入/輸出：

* Blob 儲存體
* 事件中樞
* SQL Database
* 資料表儲存體

### <a name="blob-storagetable-storage"></a>Blob 儲存體/資料表儲存體 
重複第 1 部分 hello 先前使用您的工作的存取金鑰 toorenew hello 現在未使用的存取金鑰。

### <a name="event-hubs"></a>事件中樞
Hello 先前使用您的工作的索引鍵的重複第 1 部分 toorenew hello 現在未使用的索引鍵。

### <a name="sql-database"></a>SQL Database
1. 從組件 1 步驟 7 和 hello 下列查詢，以 hello 先前使用您的工作的使用者名稱取代 < previous_login_name > 中的型別上返回 toohello 查詢視窗中：  
   `DROP LOGIN <previous_login_name>`  
2. 按一下 [執行]：  
   ![graphic43][graphic43]  

您應該取得 hello 下列確認： 

    Command(s) completed successfully.

## <a name="get-help"></a>取得說明
如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>後續步驟
* [簡介 tooAzure 資料流分析](stream-analytics-introduction.md)
* [開始使用 Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [調整 Azure Stream Analytics 工作](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics 查詢語言參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure 串流分析管理 REST API 參考](https://msdn.microsoft.com/library/azure/dn835031.aspx)

[graphic1]: ./media/stream-analytics-login-credentials-inputs-outputs/1-stream-analytics-login-credentials-inputs-outputs.png
[graphic2]: ./media/stream-analytics-login-credentials-inputs-outputs/2-stream-analytics-login-credentials-inputs-outputs.png
[graphic3]: ./media/stream-analytics-login-credentials-inputs-outputs/3-stream-analytics-login-credentials-inputs-outputs.png
[graphic4]: ./media/stream-analytics-login-credentials-inputs-outputs/4-stream-analytics-login-credentials-inputs-outputs.png
[graphic5]: ./media/stream-analytics-login-credentials-inputs-outputs/5-stream-analytics-login-credentials-inputs-outputs.png
[graphic6]: ./media/stream-analytics-login-credentials-inputs-outputs/6-stream-analytics-login-credentials-inputs-outputs.png
[graphic7]: ./media/stream-analytics-login-credentials-inputs-outputs/7-stream-analytics-login-credentials-inputs-outputs.png
[graphic8]: ./media/stream-analytics-login-credentials-inputs-outputs/8-stream-analytics-login-credentials-inputs-outputs.png
[graphic9]: ./media/stream-analytics-login-credentials-inputs-outputs/9-stream-analytics-login-credentials-inputs-outputs.png
[graphic10]: ./media/stream-analytics-login-credentials-inputs-outputs/10-stream-analytics-login-credentials-inputs-outputs.png
[graphic11]: ./media/stream-analytics-login-credentials-inputs-outputs/11-stream-analytics-login-credentials-inputs-outputs.png
[graphic12]: ./media/stream-analytics-login-credentials-inputs-outputs/12-stream-analytics-login-credentials-inputs-outputs.png
[graphic13]: ./media/stream-analytics-login-credentials-inputs-outputs/13-stream-analytics-login-credentials-inputs-outputs.png
[graphic14]: ./media/stream-analytics-login-credentials-inputs-outputs/14-stream-analytics-login-credentials-inputs-outputs.png
[graphic15]: ./media/stream-analytics-login-credentials-inputs-outputs/15-stream-analytics-login-credentials-inputs-outputs.png
[graphic16]: ./media/stream-analytics-login-credentials-inputs-outputs/16-stream-analytics-login-credentials-inputs-outputs.png
[graphic17]: ./media/stream-analytics-login-credentials-inputs-outputs/17-stream-analytics-login-credentials-inputs-outputs.png
[graphic18]: ./media/stream-analytics-login-credentials-inputs-outputs/18-stream-analytics-login-credentials-inputs-outputs.png
[graphic19]: ./media/stream-analytics-login-credentials-inputs-outputs/19-stream-analytics-login-credentials-inputs-outputs.png
[graphic20]: ./media/stream-analytics-login-credentials-inputs-outputs/20-stream-analytics-login-credentials-inputs-outputs.png
[graphic21]: ./media/stream-analytics-login-credentials-inputs-outputs/21-stream-analytics-login-credentials-inputs-outputs.png
[graphic22]: ./media/stream-analytics-login-credentials-inputs-outputs/22-stream-analytics-login-credentials-inputs-outputs.png
[graphic23]: ./media/stream-analytics-login-credentials-inputs-outputs/23-stream-analytics-login-credentials-inputs-outputs.png
[graphic24]: ./media/stream-analytics-login-credentials-inputs-outputs/24-stream-analytics-login-credentials-inputs-outputs.png
[graphic25]: ./media/stream-analytics-login-credentials-inputs-outputs/25-stream-analytics-login-credentials-inputs-outputs.png
[graphic26]: ./media/stream-analytics-login-credentials-inputs-outputs/26-stream-analytics-login-credentials-inputs-outputs.png
[graphic27]: ./media/stream-analytics-login-credentials-inputs-outputs/27-stream-analytics-login-credentials-inputs-outputs.png
[graphic28]: ./media/stream-analytics-login-credentials-inputs-outputs/28-stream-analytics-login-credentials-inputs-outputs.png
[graphic29]: ./media/stream-analytics-login-credentials-inputs-outputs/29-stream-analytics-login-credentials-inputs-outputs.png
[graphic30]: ./media/stream-analytics-login-credentials-inputs-outputs/30-stream-analytics-login-credentials-inputs-outputs.png
[graphic31]: ./media/stream-analytics-login-credentials-inputs-outputs/31-stream-analytics-login-credentials-inputs-outputs.png
[graphic32]: ./media/stream-analytics-login-credentials-inputs-outputs/32-stream-analytics-login-credentials-inputs-outputs.png
[graphic33]: ./media/stream-analytics-login-credentials-inputs-outputs/33-stream-analytics-login-credentials-inputs-outputs.png
[graphic34]: ./media/stream-analytics-login-credentials-inputs-outputs/34-stream-analytics-login-credentials-inputs-outputs.png
[graphic35]: ./media/stream-analytics-login-credentials-inputs-outputs/35-stream-analytics-login-credentials-inputs-outputs.png
[graphic36]: ./media/stream-analytics-login-credentials-inputs-outputs/36-stream-analytics-login-credentials-inputs-outputs.png
[graphic37]: ./media/stream-analytics-login-credentials-inputs-outputs/37-stream-analytics-login-credentials-inputs-outputs.png
[graphic38]: ./media/stream-analytics-login-credentials-inputs-outputs/38-stream-analytics-login-credentials-inputs-outputs.png
[graphic39]: ./media/stream-analytics-login-credentials-inputs-outputs/39-stream-analytics-login-credentials-inputs-outputs.png
[graphic40]: ./media/stream-analytics-login-credentials-inputs-outputs/40-stream-analytics-login-credentials-inputs-outputs.png
[graphic41]: ./media/stream-analytics-login-credentials-inputs-outputs/41-stream-analytics-login-credentials-inputs-outputs.png
[graphic42]: ./media/stream-analytics-login-credentials-inputs-outputs/42-stream-analytics-login-credentials-inputs-outputs.png
[graphic43]: ./media/stream-analytics-login-credentials-inputs-outputs/43-stream-analytics-login-credentials-inputs-outputs.png

