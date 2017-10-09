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
# <a name="rotate-login-credentials-for-inputs-and-outputs-in-stream-analytics-jobs"></a><span data-ttu-id="c19eb-104">在串流分析工作中替換輸入和輸出的登入認證</span><span class="sxs-lookup"><span data-stu-id="c19eb-104">Rotate login credentials for inputs and outputs in Stream Analytics Jobs</span></span>
## <a name="abstract"></a><span data-ttu-id="c19eb-105">摘要</span><span class="sxs-lookup"><span data-stu-id="c19eb-105">Abstract</span></span>
<span data-ttu-id="c19eb-106">Azure Stream Analytics 目前不允許取代 hello 認證於輸入/輸出 hello 作業執行時。</span><span class="sxs-lookup"><span data-stu-id="c19eb-106">Azure Stream Analytics today doesn’t allow replacing hello credentials on an input/output while hello job is running.</span></span>

<span data-ttu-id="c19eb-107">雖然 Azure Stream Analytics 支援繼續從最後的輸出工作，我們想 tooshare hello 整個程序將停止的 hello 與 hello 工作的開始和旋轉 hello 登入認證之間的 hello 延隔時間降到最低。</span><span class="sxs-lookup"><span data-stu-id="c19eb-107">While Azure Stream Analytics does support resuming a job from last output, we wanted tooshare hello entire process for minimizing hello lag between hello stopping and starting of hello job and rotating hello login credentials.</span></span>

## <a name="part-1---prepare-hello-new-set-of-credentials"></a><span data-ttu-id="c19eb-108">第 1 部-準備 hello 組新的認證：</span><span class="sxs-lookup"><span data-stu-id="c19eb-108">Part 1 - Prepare hello new set of credentials:</span></span>
<span data-ttu-id="c19eb-109">這部分適用 toohello 後面輸入/輸出：</span><span class="sxs-lookup"><span data-stu-id="c19eb-109">This part is applicable toohello following inputs/outputs:</span></span>

* <span data-ttu-id="c19eb-110">Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="c19eb-110">Blob Storage</span></span>
* <span data-ttu-id="c19eb-111">事件中樞</span><span class="sxs-lookup"><span data-stu-id="c19eb-111">Event Hubs</span></span>
* <span data-ttu-id="c19eb-112">SQL Database</span><span class="sxs-lookup"><span data-stu-id="c19eb-112">SQL Database</span></span>
* <span data-ttu-id="c19eb-113">資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="c19eb-113">Table Storage</span></span>

<span data-ttu-id="c19eb-114">針對其他的輸入/輸出，請參考第 2 部分。</span><span class="sxs-lookup"><span data-stu-id="c19eb-114">For other inputs/outputs, proceed with Part 2.</span></span>

### <a name="blob-storagetable-storage"></a><span data-ttu-id="c19eb-115">Blob 儲存體/資料表儲存體 </span><span class="sxs-lookup"><span data-stu-id="c19eb-115">Blob storage/Table storage</span></span>
1. <span data-ttu-id="c19eb-116">Hello Azure 管理入口網站中上移 toohello 儲存副檔名：</span><span class="sxs-lookup"><span data-stu-id="c19eb-116">Go toohello Storage extention on hello Azure Management portal:</span></span>  
   ![graphic1][graphic1]
2. <span data-ttu-id="c19eb-118">找出您的工作所使用的 hello 儲存體，並移入它：</span><span class="sxs-lookup"><span data-stu-id="c19eb-118">Locate hello storage used by your job and go into it:</span></span>  
   ![graphic2][graphic2]
3. <span data-ttu-id="c19eb-120">按一下 hello 管理存取金鑰的命令：</span><span class="sxs-lookup"><span data-stu-id="c19eb-120">Click hello Manage Access Keys command:</span></span>  
   ![graphic3][graphic3]
4. <span data-ttu-id="c19eb-122">Hello 主要存取金鑰和次要存取金鑰，hello 之間**挑選其中一個不由您的工作 hello**。</span><span class="sxs-lookup"><span data-stu-id="c19eb-122">Between hello Primary Access Key and hello Secondary Access Key, **pick hello one not used by your job**.</span></span>
5. <span data-ttu-id="c19eb-123">按重新產生：</span><span class="sxs-lookup"><span data-stu-id="c19eb-123">Hit regenerate:</span></span>  
   ![graphic4][graphic4]
6. <span data-ttu-id="c19eb-125">複製 hello 新產生的金鑰：</span><span class="sxs-lookup"><span data-stu-id="c19eb-125">Copy hello newly generated key:</span></span>  
   ![graphic5][graphic5]
7. <span data-ttu-id="c19eb-127">繼續 tooPart 2。</span><span class="sxs-lookup"><span data-stu-id="c19eb-127">Continue tooPart 2.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="c19eb-128">事件中樞</span><span class="sxs-lookup"><span data-stu-id="c19eb-128">Event hubs</span></span>
1. <span data-ttu-id="c19eb-129">Hello Azure 管理入口網站中上移 toohello 服務匯流排延伸模組：</span><span class="sxs-lookup"><span data-stu-id="c19eb-129">Go toohello Service Bus extension on hello Azure Management portal:</span></span>  
   ![graphic6][graphic6]
2. <span data-ttu-id="c19eb-131">找出 hello 您的工作所使用的服務匯流排命名空間，並將它：</span><span class="sxs-lookup"><span data-stu-id="c19eb-131">Locate hello Service Bus Namespace used by your job and go into it:</span></span>  
   ![graphic7][graphic7]
3. <span data-ttu-id="c19eb-133">如果您的工作會使用 hello 服務匯流排命名空間上的共用的存取原則，跳 toostep 6</span><span class="sxs-lookup"><span data-stu-id="c19eb-133">If your job uses a shared access policy on hello Service Bus Namespace, jump toostep 6</span></span>  
4. <span data-ttu-id="c19eb-134">請移 toohello 事件中樞 索引標籤：</span><span class="sxs-lookup"><span data-stu-id="c19eb-134">Go toohello Event Hubs tab:</span></span>  
   ![graphic8][graphic8]
5. <span data-ttu-id="c19eb-136">找出 hello 您的工作所使用的事件中樞，並將它：</span><span class="sxs-lookup"><span data-stu-id="c19eb-136">Locate hello Event Hub used by your job and go into it:</span></span>  
   ![graphic9][graphic9]
6. <span data-ttu-id="c19eb-138">請移 toohello 設定 索引標籤：</span><span class="sxs-lookup"><span data-stu-id="c19eb-138">Go toohello Configure Tab:</span></span>  
   ![graphic10][graphic10]
7. <span data-ttu-id="c19eb-140">上 hello 原則名稱 下拉式清單中，找出您的工作所使用的 hello 共用存取原則：</span><span class="sxs-lookup"><span data-stu-id="c19eb-140">On hello Policy Name drop-down, locate hello shared access policy used by your job:</span></span>  
   ![graphic11][graphic11]
8. <span data-ttu-id="c19eb-142">Hello 主索引鍵與 hello 次要的索引鍵之間**挑選其中一個不由您的工作 hello**。</span><span class="sxs-lookup"><span data-stu-id="c19eb-142">Between hello Primary Key and hello Secondary Key, **pick hello one not used by your job**.</span></span>  
9. <span data-ttu-id="c19eb-143">按重新產生：</span><span class="sxs-lookup"><span data-stu-id="c19eb-143">Hit regenerate:</span></span>  
   ![graphic12][graphic12]
10. <span data-ttu-id="c19eb-145">複製 hello 新產生的金鑰：</span><span class="sxs-lookup"><span data-stu-id="c19eb-145">Copy hello newly generated key:</span></span>  
   ![graphic13][graphic13]
11. <span data-ttu-id="c19eb-147">繼續 tooPart 2。</span><span class="sxs-lookup"><span data-stu-id="c19eb-147">Continue tooPart 2.</span></span>  

### <a name="sql-database"></a><span data-ttu-id="c19eb-148">SQL Database</span><span class="sxs-lookup"><span data-stu-id="c19eb-148">SQL Database</span></span>
> [!NOTE]
> <span data-ttu-id="c19eb-149">注意： 您需要 tooconnect toohello SQL Database 服務。</span><span class="sxs-lookup"><span data-stu-id="c19eb-149">Note: you will need tooconnect toohello SQL Database Service.</span></span> <span data-ttu-id="c19eb-150">我們 tooshow toodo 此使用 hello 上的管理體驗如何 hello Azure 管理入口網站，但您可以選擇 toouse SQL Server Management Studio 等某些用戶端工具以及。</span><span class="sxs-lookup"><span data-stu-id="c19eb-150">We are going tooshow how toodo this using hello management experience on hello Azure Management portal but you may choose toouse some client-side tool such as SQL Server Management Studio as well.</span></span>
>
> 

1. <span data-ttu-id="c19eb-151">Hello Azure 管理入口網站中上移 toohello SQL 資料庫的擴充功能：</span><span class="sxs-lookup"><span data-stu-id="c19eb-151">Go toohello SQL Databases extension on hello Azure Management portal:</span></span>  
   ![graphic14][graphic14]
2. <span data-ttu-id="c19eb-153">找出您的工作所使用的 SQL 資料庫 hello 和**hello 伺服器上按一下**相同連結上 hello 行：</span><span class="sxs-lookup"><span data-stu-id="c19eb-153">Locate hello SQL Database used by your job and **click on hello server** link on hello same line:</span></span>  
   <span data-ttu-id="c19eb-154">![graphic15][graphic15]</span><span class="sxs-lookup"><span data-stu-id="c19eb-154">![graphic15][graphic15]</span></span>
3. <span data-ttu-id="c19eb-155">按一下 hello 管理命令：</span><span class="sxs-lookup"><span data-stu-id="c19eb-155">Click hello Manage command:</span></span>  
   ![graphic16][graphic16]
4. <span data-ttu-id="c19eb-157">輸入主要資料庫：</span><span class="sxs-lookup"><span data-stu-id="c19eb-157">Type Database Master:</span></span>  
   ![graphic17][graphic17]
5. <span data-ttu-id="c19eb-159">輸入使用者名稱和密碼，然後按一下 [登入]：</span><span class="sxs-lookup"><span data-stu-id="c19eb-159">Type in your User Name, Password, and click Log on:</span></span>  
   ![graphic18][graphic18]
6. <span data-ttu-id="c19eb-161">按一下 [新增查閱]：</span><span class="sxs-lookup"><span data-stu-id="c19eb-161">Click New Query:</span></span>  
   ![graphic19][graphic19]
7. <span data-ttu-id="c19eb-163">型別在下列查詢取代 < login_name > 與您的使用者名稱和取代 hello<enterStrongPasswordHere>使用新的密碼：</span><span class="sxs-lookup"><span data-stu-id="c19eb-163">Type in hello following query replacing <login_name> with your User Name and replacing <enterStrongPasswordHere> with your new password:</span></span>  
   `CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>'`
8. <span data-ttu-id="c19eb-164">按一下 [執行]：</span><span class="sxs-lookup"><span data-stu-id="c19eb-164">Click Run:</span></span>  
   ![graphic20][graphic20]
9. <span data-ttu-id="c19eb-166">返回 toostep 2，這次按一下 hello 資料庫：</span><span class="sxs-lookup"><span data-stu-id="c19eb-166">Go back toostep 2 and this time click hello database:</span></span>  
   ![graphic21][graphic21]
10. <span data-ttu-id="c19eb-168">按一下 hello 管理命令：</span><span class="sxs-lookup"><span data-stu-id="c19eb-168">Click hello Manage command:</span></span>  
   ![graphic22][graphic22]
11. <span data-ttu-id="c19eb-170">輸入使用者名稱和密碼，然後按一下 [登入]：</span><span class="sxs-lookup"><span data-stu-id="c19eb-170">type in your User Name, Password, and click Logon:</span></span>  
   ![graphic23][graphic23]
12. <span data-ttu-id="c19eb-172">按一下 [新增查閱]：</span><span class="sxs-lookup"><span data-stu-id="c19eb-172">Click New Query:</span></span>  
   ![graphic24][graphic24]
13. <span data-ttu-id="c19eb-174">輸入下列查詢取代 < 使用者名稱 > 想 tooidentify 所用的名稱與 hello hello 這個資料庫內容中的此登入 (您可以提供 hello 相同的值指定給資料庫的 < login_name >，例如)，並以取代 < login_name >新的使用者名稱：</span><span class="sxs-lookup"><span data-stu-id="c19eb-174">Type in hello following query replacing <user_name> with a name by which you want tooidentify this login in hello context of this database (you can provide hello same value you gave for <login_name>, for example) and replacing <login_name> with your new user name:</span></span>  
   `CREATE USER <user_name> FROM LOGIN <login_name>`
14. <span data-ttu-id="c19eb-175">按一下 [執行]：</span><span class="sxs-lookup"><span data-stu-id="c19eb-175">Click Run:</span></span>  
   ![graphic25][graphic25]
15. <span data-ttu-id="c19eb-177">您現在應該提供您新的使用者以 hello 相同角色與您的原始使用者的權限。</span><span class="sxs-lookup"><span data-stu-id="c19eb-177">You should now provide your new user with hello same roles and privileges your original user had.</span></span>
16. <span data-ttu-id="c19eb-178">繼續 tooPart 2。</span><span class="sxs-lookup"><span data-stu-id="c19eb-178">Continue tooPart 2.</span></span>

## <a name="part-2-stopping-hello-stream-analytics-job"></a><span data-ttu-id="c19eb-179">第 2 部分： 停止 hello 串流分析工作</span><span class="sxs-lookup"><span data-stu-id="c19eb-179">Part 2: Stopping hello Stream Analytics Job</span></span>
1. <span data-ttu-id="c19eb-180">Hello Azure 管理入口網站中上移 toohello 資料流分析擴充功能：</span><span class="sxs-lookup"><span data-stu-id="c19eb-180">Go toohello Stream Analytics extension on hello Azure Management portal:</span></span>  
   ![graphic26][graphic26]
2. <span data-ttu-id="c19eb-182">找出您的工作，然後進到裡面： </span><span class="sxs-lookup"><span data-stu-id="c19eb-182">Locate your job and go into it:</span></span>  
   ![graphic27][graphic27]
3. <span data-ttu-id="c19eb-184">前往 toohello 輸入 索引標籤或 hello 輸出索引標籤，根據是否輪替 hello 認證輸入或輸出。</span><span class="sxs-lookup"><span data-stu-id="c19eb-184">Go toohello Inputs tab or hello Outputs tab based on whether you are rotating hello credentials on an Input or on an Output.</span></span>  
   ![graphic28][graphic28]
4. <span data-ttu-id="c19eb-186">按一下 hello 停止命令，並確認 hello 作業已停止：</span><span class="sxs-lookup"><span data-stu-id="c19eb-186">Click hello Stop command and confirm hello job has stopped:</span></span>  
   <span data-ttu-id="c19eb-187">![graphic29][graphic29]等候 hello 作業 toostop。</span><span class="sxs-lookup"><span data-stu-id="c19eb-187">![graphic29][graphic29] Wait for hello job toostop.</span></span>
5. <span data-ttu-id="c19eb-188">找出 hello 輸入/輸出要 toorotate 認證並移到其中：</span><span class="sxs-lookup"><span data-stu-id="c19eb-188">Locate hello input/output you want toorotate credentials on and go into it:</span></span>  
   ![graphic30][graphic30]
6. <span data-ttu-id="c19eb-190">繼續 tooPart 3。</span><span class="sxs-lookup"><span data-stu-id="c19eb-190">Proceed tooPart 3.</span></span>

## <a name="part-3-editing-hello-credentials-on-hello-stream-analytics-job"></a><span data-ttu-id="c19eb-191">第 3 部分： Hello 串流分析工作上，編輯 hello 認證</span><span class="sxs-lookup"><span data-stu-id="c19eb-191">Part 3: Editing hello credentials on hello Stream Analytics Job</span></span>
### <a name="blob-storagetable-storage"></a><span data-ttu-id="c19eb-192">Blob 儲存體/資料表儲存體 </span><span class="sxs-lookup"><span data-stu-id="c19eb-192">Blob storage/Table storage</span></span>
1. <span data-ttu-id="c19eb-193">尋找 hello 儲存體帳戶金鑰 欄位，並貼上您新產生的金鑰：</span><span class="sxs-lookup"><span data-stu-id="c19eb-193">Find hello Storage Account Key field and paste your newly generated key into it:</span></span>  
   ![graphic31][graphic31]
2. <span data-ttu-id="c19eb-195">按一下 hello 儲存 命令，並確認 儲存變更：</span><span class="sxs-lookup"><span data-stu-id="c19eb-195">Click hello Save command and confirm saving your changes:</span></span>  
   ![graphic32][graphic32]
3. <span data-ttu-id="c19eb-197">當您儲存所做的變更時，系統會自動測試連線，以保證萬無一失。</span><span class="sxs-lookup"><span data-stu-id="c19eb-197">A connection test will automatically start when you save your changes, make sure that is has successfully passed.</span></span>
4. <span data-ttu-id="c19eb-198">繼續 tooPart 4。</span><span class="sxs-lookup"><span data-stu-id="c19eb-198">Proceed tooPart 4.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="c19eb-199">事件中樞</span><span class="sxs-lookup"><span data-stu-id="c19eb-199">Event hubs</span></span>
1. <span data-ttu-id="c19eb-200">找出 hello 事件中樞原則機碼欄位，並將新產生的金鑰貼到它：</span><span class="sxs-lookup"><span data-stu-id="c19eb-200">Find hello Event Hub Policy Key field and paste your newly generated key into it:</span></span>  
   ![graphic33][graphic33]
2. <span data-ttu-id="c19eb-202">按一下 hello 儲存 命令，並確認 儲存變更：</span><span class="sxs-lookup"><span data-stu-id="c19eb-202">Click hello Save command and confirm saving your changes:</span></span>  
   ![graphic34][graphic34]
3. <span data-ttu-id="c19eb-204">當您儲存所做的變更時，系統會自動測試連線，以保證萬無一失。</span><span class="sxs-lookup"><span data-stu-id="c19eb-204">A connection test will automatically start when you save your changes, make sure that it has successfully passed.</span></span>
4. <span data-ttu-id="c19eb-205">繼續 tooPart 4。</span><span class="sxs-lookup"><span data-stu-id="c19eb-205">Proceed tooPart 4.</span></span>

### <a name="power-bi"></a><span data-ttu-id="c19eb-206">Power BI</span><span class="sxs-lookup"><span data-stu-id="c19eb-206">Power BI</span></span>
1. <span data-ttu-id="c19eb-207">按一下 hello 更新授權：</span><span class="sxs-lookup"><span data-stu-id="c19eb-207">Click hello Renew authorization:</span></span>  

   ![graphic35][graphic35]
2. <span data-ttu-id="c19eb-209">您會收到下列確認 hello:</span><span class="sxs-lookup"><span data-stu-id="c19eb-209">You will get hello following confirmation:</span></span>  

   ![graphic36][graphic36]
3. <span data-ttu-id="c19eb-211">按一下 hello 儲存 命令，並確認 儲存變更：</span><span class="sxs-lookup"><span data-stu-id="c19eb-211">Click hello Save command and confirm saving your changes:</span></span>  
   ![graphic37][graphic37]
4. <span data-ttu-id="c19eb-213">當您儲存所做的變更時，系統會自動測試連線，以保證萬無一失。</span><span class="sxs-lookup"><span data-stu-id="c19eb-213">A connection test will automatically start when you save your changes, make sure it has successfully passed.</span></span>
5. <span data-ttu-id="c19eb-214">繼續 tooPart 4。</span><span class="sxs-lookup"><span data-stu-id="c19eb-214">Proceed tooPart 4.</span></span>

### <a name="sql-database"></a><span data-ttu-id="c19eb-215">SQL Database</span><span class="sxs-lookup"><span data-stu-id="c19eb-215">SQL Database</span></span>
1. <span data-ttu-id="c19eb-216">尋找 hello 使用者名稱和密碼的欄位，並將您新建立的認證集貼到它們：</span><span class="sxs-lookup"><span data-stu-id="c19eb-216">Find hello User Name and Password fields and paste your newly created set of credentials into them:</span></span>  
   ![graphic38][graphic38]
2. <span data-ttu-id="c19eb-218">按一下 hello 儲存 命令，並確認 儲存變更：</span><span class="sxs-lookup"><span data-stu-id="c19eb-218">Click hello Save command and confirm saving your changes:</span></span>  
   ![graphic39][graphic39]
3. <span data-ttu-id="c19eb-220">當您儲存所做的變更時，系統會自動測試連線，以保證萬無一失。</span><span class="sxs-lookup"><span data-stu-id="c19eb-220">A connection test will automatically start when you save your changes, make sure that it has successfully passed.</span></span>  
4. <span data-ttu-id="c19eb-221">繼續 tooPart 4。</span><span class="sxs-lookup"><span data-stu-id="c19eb-221">Proceed tooPart 4.</span></span>

## <a name="part-4-starting-your-job-from-last-stopped-time"></a><span data-ttu-id="c19eb-222">第 4 部分：從上次停止的時間開始您的工作</span><span class="sxs-lookup"><span data-stu-id="c19eb-222">Part 4: Starting your job from last stopped time</span></span>
1. <span data-ttu-id="c19eb-223">離開 hello 輸入/輸出：</span><span class="sxs-lookup"><span data-stu-id="c19eb-223">Navigate away from hello Input/Output:</span></span>  
   ![graphic40][graphic40]
2. <span data-ttu-id="c19eb-225">按一下 hello 啟動命令：</span><span class="sxs-lookup"><span data-stu-id="c19eb-225">Click hello Start command:</span></span>  
   ![graphic41][graphic41]
3. <span data-ttu-id="c19eb-227">挑選 hello 上次停止時間，然後按一下 確定:</span><span class="sxs-lookup"><span data-stu-id="c19eb-227">Pick hello Last Stopped Time and click OK:</span></span>  
   ![graphic42][graphic42]
4. <span data-ttu-id="c19eb-229">繼續 tooPart 5。</span><span class="sxs-lookup"><span data-stu-id="c19eb-229">Proceed tooPart 5.</span></span>  

## <a name="part-5-removing-hello-old-set-of-credentials"></a><span data-ttu-id="c19eb-230">第 5 部分： 移除 hello 舊一組認證</span><span class="sxs-lookup"><span data-stu-id="c19eb-230">Part 5: Removing hello old set of credentials</span></span>
<span data-ttu-id="c19eb-231">這部分適用 toohello 後面輸入/輸出：</span><span class="sxs-lookup"><span data-stu-id="c19eb-231">This part is applicable toohello following inputs/outputs:</span></span>

* <span data-ttu-id="c19eb-232">Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="c19eb-232">Blob Storage</span></span>
* <span data-ttu-id="c19eb-233">事件中樞</span><span class="sxs-lookup"><span data-stu-id="c19eb-233">Event Hubs</span></span>
* <span data-ttu-id="c19eb-234">SQL Database</span><span class="sxs-lookup"><span data-stu-id="c19eb-234">SQL Database</span></span>
* <span data-ttu-id="c19eb-235">資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="c19eb-235">Table Storage</span></span>

### <a name="blob-storagetable-storage"></a><span data-ttu-id="c19eb-236">Blob 儲存體/資料表儲存體 </span><span class="sxs-lookup"><span data-stu-id="c19eb-236">Blob storage/Table storage</span></span>
<span data-ttu-id="c19eb-237">重複第 1 部分 hello 先前使用您的工作的存取金鑰 toorenew hello 現在未使用的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="c19eb-237">Repeat Part 1 for hello Access Key that was previously used by your job toorenew hello now unused Access Key.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="c19eb-238">事件中樞</span><span class="sxs-lookup"><span data-stu-id="c19eb-238">Event hubs</span></span>
<span data-ttu-id="c19eb-239">Hello 先前使用您的工作的索引鍵的重複第 1 部分 toorenew hello 現在未使用的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="c19eb-239">Repeat Part 1 for hello Key that was previously used by your job toorenew hello now unused Key.</span></span>

### <a name="sql-database"></a><span data-ttu-id="c19eb-240">SQL Database</span><span class="sxs-lookup"><span data-stu-id="c19eb-240">SQL Database</span></span>
1. <span data-ttu-id="c19eb-241">從組件 1 步驟 7 和 hello 下列查詢，以 hello 先前使用您的工作的使用者名稱取代 < previous_login_name > 中的型別上返回 toohello 查詢視窗中：</span><span class="sxs-lookup"><span data-stu-id="c19eb-241">Go back toohello query window from Part 1 Step 7 and type in hello following query, replacing <previous_login_name> with hello User Name that was previously used by your job:</span></span>  
   `DROP LOGIN <previous_login_name>`  
2. <span data-ttu-id="c19eb-242">按一下 [執行]：</span><span class="sxs-lookup"><span data-stu-id="c19eb-242">Click Run:</span></span>  
   ![graphic43][graphic43]  

<span data-ttu-id="c19eb-244">您應該取得 hello 下列確認：</span><span class="sxs-lookup"><span data-stu-id="c19eb-244">You should get hello following confirmation:</span></span> 

    Command(s) completed successfully.

## <a name="get-help"></a><span data-ttu-id="c19eb-245">取得說明</span><span class="sxs-lookup"><span data-stu-id="c19eb-245">Get help</span></span>
<span data-ttu-id="c19eb-246">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="c19eb-246">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="c19eb-247">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c19eb-247">Next steps</span></span>
* [<span data-ttu-id="c19eb-248">簡介 tooAzure 資料流分析</span><span class="sxs-lookup"><span data-stu-id="c19eb-248">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="c19eb-249">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="c19eb-249">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="c19eb-250">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="c19eb-250">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="c19eb-251">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="c19eb-251">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="c19eb-252">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="c19eb-252">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

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

