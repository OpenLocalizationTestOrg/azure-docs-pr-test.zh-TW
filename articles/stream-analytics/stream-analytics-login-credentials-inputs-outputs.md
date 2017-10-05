---
title: "串流分析：替換輸入和輸出的登入認證 | Microsoft Docs"
description: "了解如何更新 Azure Stream Analytics 的輸入和輸出認證。"
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
ms.openlocfilehash: 2cb995a3969a8cb025f371ed0ab160cd04b0454d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="rotate-login-credentials-for-inputs-and-outputs-in-stream-analytics-jobs"></a><span data-ttu-id="64687-104">在串流分析工作中替換輸入和輸出的登入認證</span><span class="sxs-lookup"><span data-stu-id="64687-104">Rotate login credentials for inputs and outputs in Stream Analytics Jobs</span></span>
## <a name="abstract"></a><span data-ttu-id="64687-105">摘要</span><span class="sxs-lookup"><span data-stu-id="64687-105">Abstract</span></span>
<span data-ttu-id="64687-106">Azure Stream Analytics 目前不允許在工作執行的時候，取代輸入/輸出中的認證。</span><span class="sxs-lookup"><span data-stu-id="64687-106">Azure Stream Analytics today doesn’t allow replacing the credentials on an input/output while the job is running.</span></span>

<span data-ttu-id="64687-107">雖然 Azure 串流分析不支援從上次的輸出繼續工作，但我們還是要和您分享如何盡量縮短工作停止和開始之間的延遲時間，以及替換登入認證的整個程序。</span><span class="sxs-lookup"><span data-stu-id="64687-107">While Azure Stream Analytics does support resuming a job from last output, we wanted to share the entire process for minimizing the lag between the stopping and starting of the job and rotating the login credentials.</span></span>

## <a name="part-1---prepare-the-new-set-of-credentials"></a><span data-ttu-id="64687-108">第 1 部分 - 準備一組新的認證：</span><span class="sxs-lookup"><span data-stu-id="64687-108">Part 1 - Prepare the new set of credentials:</span></span>
<span data-ttu-id="64687-109">此部分適用於下列的輸入/輸出：</span><span class="sxs-lookup"><span data-stu-id="64687-109">This part is applicable to the following inputs/outputs:</span></span>

* <span data-ttu-id="64687-110">Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="64687-110">Blob Storage</span></span>
* <span data-ttu-id="64687-111">事件中樞</span><span class="sxs-lookup"><span data-stu-id="64687-111">Event Hubs</span></span>
* <span data-ttu-id="64687-112">SQL Database</span><span class="sxs-lookup"><span data-stu-id="64687-112">SQL Database</span></span>
* <span data-ttu-id="64687-113">資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="64687-113">Table Storage</span></span>

<span data-ttu-id="64687-114">針對其他的輸入/輸出，請參考第 2 部分。</span><span class="sxs-lookup"><span data-stu-id="64687-114">For other inputs/outputs, proceed with Part 2.</span></span>

### <a name="blob-storagetable-storage"></a><span data-ttu-id="64687-115">Blob 儲存體/資料表儲存體 </span><span class="sxs-lookup"><span data-stu-id="64687-115">Blob storage/Table storage</span></span>
1. <span data-ttu-id="64687-116">在 Azure 管理入口網站中，瀏覽至 [儲存體] 擴充：</span><span class="sxs-lookup"><span data-stu-id="64687-116">Go to the Storage extention on the Azure Management portal:</span></span>  
   ![graphic1][graphic1]
2. <span data-ttu-id="64687-118">找出工作使用的儲存體，然後進到裡面：</span><span class="sxs-lookup"><span data-stu-id="64687-118">Locate the storage used by your job and go into it:</span></span>  
   ![graphic2][graphic2]
3. <span data-ttu-id="64687-120">按一下 [管理存取金鑰] 命令：</span><span class="sxs-lookup"><span data-stu-id="64687-120">Click the Manage Access Keys command:</span></span>  
   ![graphic3][graphic3]
4. <span data-ttu-id="64687-122">在主要存取金鑰和次要存取金鑰之間， **挑選工作使用的金鑰**。</span><span class="sxs-lookup"><span data-stu-id="64687-122">Between the Primary Access Key and the Secondary Access Key, **pick the one not used by your job**.</span></span>
5. <span data-ttu-id="64687-123">按重新產生：</span><span class="sxs-lookup"><span data-stu-id="64687-123">Hit regenerate:</span></span>  
   ![graphic4][graphic4]
6. <span data-ttu-id="64687-125">複製剛剛產生的金鑰：</span><span class="sxs-lookup"><span data-stu-id="64687-125">Copy the newly generated key:</span></span>  
   ![graphic5][graphic5]
7. <span data-ttu-id="64687-127">繼續第 2 部分。</span><span class="sxs-lookup"><span data-stu-id="64687-127">Continue to Part 2.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="64687-128">事件中樞</span><span class="sxs-lookup"><span data-stu-id="64687-128">Event hubs</span></span>
1. <span data-ttu-id="64687-129">在 Azure 管理入口網站中，瀏覽至 [服務匯流排] 擴充：</span><span class="sxs-lookup"><span data-stu-id="64687-129">Go to the Service Bus extension on the Azure Management portal:</span></span>  
   ![graphic6][graphic6]
2. <span data-ttu-id="64687-131">找出工作使用的服務匯流排命名空間，然後進到裡面：</span><span class="sxs-lookup"><span data-stu-id="64687-131">Locate the Service Bus Namespace used by your job and go into it:</span></span>  
   ![graphic7][graphic7]
3. <span data-ttu-id="64687-133">如果工作會在「服務匯流排命名空間」上使用共用存取原則，請跳到步驟 6</span><span class="sxs-lookup"><span data-stu-id="64687-133">If your job uses a shared access policy on the Service Bus Namespace, jump to step 6</span></span>  
4. <span data-ttu-id="64687-134">移至 [事件中樞] 索引標籤：</span><span class="sxs-lookup"><span data-stu-id="64687-134">Go to the Event Hubs tab:</span></span>  
   ![graphic8][graphic8]
5. <span data-ttu-id="64687-136">找出工作使用的事件中樞，然後進到裡面：</span><span class="sxs-lookup"><span data-stu-id="64687-136">Locate the Event Hub used by your job and go into it:</span></span>  
   ![graphic9][graphic9]
6. <span data-ttu-id="64687-138">移至 [設定] 索引標籤：</span><span class="sxs-lookup"><span data-stu-id="64687-138">Go to the Configure Tab:</span></span>  
   ![graphic10][graphic10]
7. <span data-ttu-id="64687-140">在 [原則名稱] 下拉式清單中，找出工作使用的共用存取原則：</span><span class="sxs-lookup"><span data-stu-id="64687-140">On the Policy Name drop-down, locate the shared access policy used by your job:</span></span>  
   ![graphic11][graphic11]
8. <span data-ttu-id="64687-142">在主要金鑰和次要金鑰之間， **挑選工作未使用的金鑰**。</span><span class="sxs-lookup"><span data-stu-id="64687-142">Between the Primary Key and the Secondary Key, **pick the one not used by your job**.</span></span>  
9. <span data-ttu-id="64687-143">按重新產生：</span><span class="sxs-lookup"><span data-stu-id="64687-143">Hit regenerate:</span></span>  
   ![graphic12][graphic12]
10. <span data-ttu-id="64687-145">複製剛剛產生的金鑰：</span><span class="sxs-lookup"><span data-stu-id="64687-145">Copy the newly generated key:</span></span>  
   ![graphic13][graphic13]
11. <span data-ttu-id="64687-147">繼續第 2 部分。</span><span class="sxs-lookup"><span data-stu-id="64687-147">Continue to Part 2.</span></span>  

### <a name="sql-database"></a><span data-ttu-id="64687-148">SQL Database</span><span class="sxs-lookup"><span data-stu-id="64687-148">SQL Database</span></span>
> [!NOTE]
> <span data-ttu-id="64687-149">注意：您必須連接到 SQL Database 服務。</span><span class="sxs-lookup"><span data-stu-id="64687-149">Note: you will need to connect to the SQL Database Service.</span></span> <span data-ttu-id="64687-150">為了示範整個過程，我們會借鑑 Azure 管理入口網站的管理經驗，不過您也可以選擇使用其他類似 SQL Server Management Studio 的用戶端工具。</span><span class="sxs-lookup"><span data-stu-id="64687-150">We are going to show how to do this using the management experience on the Azure Management portal but you may choose to use some client-side tool such as SQL Server Management Studio as well.</span></span>
>
> 

1. <span data-ttu-id="64687-151">在 Azure 管理入口網站中，瀏覽至 [SQL 資料庫] 擴充：</span><span class="sxs-lookup"><span data-stu-id="64687-151">Go to the SQL Databases extension on the Azure Management portal:</span></span>  
   ![graphic14][graphic14]
2. <span data-ttu-id="64687-153">找出工作使用的 SQL Database，然後在同一行上**按一下伺服器**連結：</span><span class="sxs-lookup"><span data-stu-id="64687-153">Locate the SQL Database used by your job and **click on the server** link on the same line:</span></span>  
   <span data-ttu-id="64687-154">![graphic15][graphic15]</span><span class="sxs-lookup"><span data-stu-id="64687-154">![graphic15][graphic15]</span></span>
3. <span data-ttu-id="64687-155">按一下 [管理] 命令：</span><span class="sxs-lookup"><span data-stu-id="64687-155">Click the Manage command:</span></span>  
   ![graphic16][graphic16]
4. <span data-ttu-id="64687-157">輸入主要資料庫：</span><span class="sxs-lookup"><span data-stu-id="64687-157">Type Database Master:</span></span>  
   ![graphic17][graphic17]
5. <span data-ttu-id="64687-159">輸入使用者名稱和密碼，然後按一下 [登入]：</span><span class="sxs-lookup"><span data-stu-id="64687-159">Type in your User Name, Password, and click Log on:</span></span>  
   ![graphic18][graphic18]
6. <span data-ttu-id="64687-161">按一下 [新增查閱]：</span><span class="sxs-lookup"><span data-stu-id="64687-161">Click New Query:</span></span>  
   ![graphic19][graphic19]
7. <span data-ttu-id="64687-163">輸入下列查詢，即可將 <login_name> 換成您的使用者名稱，以及將 <enterStrongPasswordHere> 換成您的新密碼：</span><span class="sxs-lookup"><span data-stu-id="64687-163">Type in the following query replacing <login_name> with your User Name and replacing <enterStrongPasswordHere> with your new password:</span></span>  
   `CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>'`
8. <span data-ttu-id="64687-164">按一下 [執行]：</span><span class="sxs-lookup"><span data-stu-id="64687-164">Click Run:</span></span>  
   ![graphic20][graphic20]
9. <span data-ttu-id="64687-166">回到步驟 2，這一次按一下資料庫：</span><span class="sxs-lookup"><span data-stu-id="64687-166">Go back to step 2 and this time click the database:</span></span>  
   ![graphic21][graphic21]
10. <span data-ttu-id="64687-168">按一下 [管理] 命令：</span><span class="sxs-lookup"><span data-stu-id="64687-168">Click the Manage command:</span></span>  
   ![graphic22][graphic22]
11. <span data-ttu-id="64687-170">輸入使用者名稱和密碼，然後按一下 [登入]：</span><span class="sxs-lookup"><span data-stu-id="64687-170">type in your User Name, Password, and click Logon:</span></span>  
   ![graphic23][graphic23]
12. <span data-ttu-id="64687-172">按一下 [新增查閱]：</span><span class="sxs-lookup"><span data-stu-id="64687-172">Click New Query:</span></span>  
   ![graphic24][graphic24]
13. <span data-ttu-id="64687-174">輸入下列查詢，即可將 <user_name> 換成當您登入此資料庫內容時想用的識別名稱 (例如，您可以提供之前提供給 <login_name>, 的相同值)，並將 <login_name> 換成新的使用者名稱：</span><span class="sxs-lookup"><span data-stu-id="64687-174">Type in the following query replacing <user_name> with a name by which you want to identify this login in the context of this database (you can provide the same value you gave for <login_name>, for example) and replacing <login_name> with your new user name:</span></span>  
   `CREATE USER <user_name> FROM LOGIN <login_name>`
14. <span data-ttu-id="64687-175">按一下 [執行]：</span><span class="sxs-lookup"><span data-stu-id="64687-175">Click Run:</span></span>  
   ![graphic25][graphic25]
15. <span data-ttu-id="64687-177">現在您應該為新使用者提供與原始使用者相同的角色和權限。</span><span class="sxs-lookup"><span data-stu-id="64687-177">You should now provide your new user with the same roles and privileges your original user had.</span></span>
16. <span data-ttu-id="64687-178">繼續第 2 部分。</span><span class="sxs-lookup"><span data-stu-id="64687-178">Continue to Part 2.</span></span>

## <a name="part-2-stopping-the-stream-analytics-job"></a><span data-ttu-id="64687-179">第 2 部分：停止 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="64687-179">Part 2: Stopping the Stream Analytics Job</span></span>
1. <span data-ttu-id="64687-180">在 Azure 管理入口網站中，移至 [串流分析] 擴充：</span><span class="sxs-lookup"><span data-stu-id="64687-180">Go to the Stream Analytics extension on the Azure Management portal:</span></span>  
   ![graphic26][graphic26]
2. <span data-ttu-id="64687-182">找出您的工作，然後進到裡面： </span><span class="sxs-lookup"><span data-stu-id="64687-182">Locate your job and go into it:</span></span>  
   ![graphic27][graphic27]
3. <span data-ttu-id="64687-184">根據您是否想替換輸入或輸出時的認證，然後移至 [輸入] 或 [輸出] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="64687-184">Go to the Inputs tab or the Outputs tab based on whether you are rotating the credentials on an Input or on an Output.</span></span>  
   ![graphic28][graphic28]
4. <span data-ttu-id="64687-186">按一下 [停止] 命令並確認工作已停止：</span><span class="sxs-lookup"><span data-stu-id="64687-186">Click the Stop command and confirm the job has stopped:</span></span>  
   <span data-ttu-id="64687-187">![graphic29][graphic29] 等候工作停止。</span><span class="sxs-lookup"><span data-stu-id="64687-187">![graphic29][graphic29] Wait for the job to stop.</span></span>
5. <span data-ttu-id="64687-188">找出您要替換認證的輸入或輸出，然後進到裡面：</span><span class="sxs-lookup"><span data-stu-id="64687-188">Locate the input/output you want to rotate credentials on and go into it:</span></span>  
   ![graphic30][graphic30]
6. <span data-ttu-id="64687-190">繼續第 3 部分。</span><span class="sxs-lookup"><span data-stu-id="64687-190">Proceed to Part 3.</span></span>

## <a name="part-3-editing-the-credentials-on-the-stream-analytics-job"></a><span data-ttu-id="64687-191">第 3 部分：編輯 Stream Analytics 工作的認證</span><span class="sxs-lookup"><span data-stu-id="64687-191">Part 3: Editing the credentials on the Stream Analytics Job</span></span>
### <a name="blob-storagetable-storage"></a><span data-ttu-id="64687-192">Blob 儲存體/資料表儲存體 </span><span class="sxs-lookup"><span data-stu-id="64687-192">Blob storage/Table storage</span></span>
1. <span data-ttu-id="64687-193">尋找 [儲存體帳戶金鑰] 欄位，然後貼上剛剛產生的金鑰：</span><span class="sxs-lookup"><span data-stu-id="64687-193">Find the Storage Account Key field and paste your newly generated key into it:</span></span>  
   ![graphic31][graphic31]
2. <span data-ttu-id="64687-195">按一下 [儲存] 命令，然後確認儲存所做的變更：</span><span class="sxs-lookup"><span data-stu-id="64687-195">Click the Save command and confirm saving your changes:</span></span>  
   ![graphic32][graphic32]
3. <span data-ttu-id="64687-197">當您儲存所做的變更時，系統會自動測試連線，以保證萬無一失。</span><span class="sxs-lookup"><span data-stu-id="64687-197">A connection test will automatically start when you save your changes, make sure that is has successfully passed.</span></span>
4. <span data-ttu-id="64687-198">繼續第 4 部分。</span><span class="sxs-lookup"><span data-stu-id="64687-198">Proceed to Part 4.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="64687-199">事件中樞</span><span class="sxs-lookup"><span data-stu-id="64687-199">Event hubs</span></span>
1. <span data-ttu-id="64687-200">尋找 [事件中樞原則金鑰] 欄位，然後貼上剛剛產生的金鑰：</span><span class="sxs-lookup"><span data-stu-id="64687-200">Find the Event Hub Policy Key field and paste your newly generated key into it:</span></span>  
   ![graphic33][graphic33]
2. <span data-ttu-id="64687-202">按一下 [儲存] 命令，然後確認儲存所做的變更：</span><span class="sxs-lookup"><span data-stu-id="64687-202">Click the Save command and confirm saving your changes:</span></span>  
   ![graphic34][graphic34]
3. <span data-ttu-id="64687-204">當您儲存所做的變更時，系統會自動測試連線，以保證萬無一失。</span><span class="sxs-lookup"><span data-stu-id="64687-204">A connection test will automatically start when you save your changes, make sure that it has successfully passed.</span></span>
4. <span data-ttu-id="64687-205">繼續第 4 部分。</span><span class="sxs-lookup"><span data-stu-id="64687-205">Proceed to Part 4.</span></span>

### <a name="power-bi"></a><span data-ttu-id="64687-206">Power BI</span><span class="sxs-lookup"><span data-stu-id="64687-206">Power BI</span></span>
1. <span data-ttu-id="64687-207">按一下 [更新授權]：</span><span class="sxs-lookup"><span data-stu-id="64687-207">Click the Renew authorization:</span></span>  

   ![graphic35][graphic35]
2. <span data-ttu-id="64687-209">系統會要求您進行以下確認：</span><span class="sxs-lookup"><span data-stu-id="64687-209">You will get the following confirmation:</span></span>  

   ![graphic36][graphic36]
3. <span data-ttu-id="64687-211">按一下 [儲存] 命令，然後確認儲存所做的變更：</span><span class="sxs-lookup"><span data-stu-id="64687-211">Click the Save command and confirm saving your changes:</span></span>  
   ![graphic37][graphic37]
4. <span data-ttu-id="64687-213">當您儲存所做的變更時，系統會自動測試連線，以保證萬無一失。</span><span class="sxs-lookup"><span data-stu-id="64687-213">A connection test will automatically start when you save your changes, make sure it has successfully passed.</span></span>
5. <span data-ttu-id="64687-214">繼續第 4 部分。</span><span class="sxs-lookup"><span data-stu-id="64687-214">Proceed to Part 4.</span></span>

### <a name="sql-database"></a><span data-ttu-id="64687-215">SQL Database</span><span class="sxs-lookup"><span data-stu-id="64687-215">SQL Database</span></span>
1. <span data-ttu-id="64687-216">尋找 [使用者名稱] 和 [密碼] 欄位，然後貼上剛剛建立的一組認證：</span><span class="sxs-lookup"><span data-stu-id="64687-216">Find the User Name and Password fields and paste your newly created set of credentials into them:</span></span>  
   ![graphic38][graphic38]
2. <span data-ttu-id="64687-218">按一下 [儲存] 命令，然後確認儲存所做的變更：</span><span class="sxs-lookup"><span data-stu-id="64687-218">Click the Save command and confirm saving your changes:</span></span>  
   ![graphic39][graphic39]
3. <span data-ttu-id="64687-220">當您儲存所做的變更時，系統會自動測試連線，以保證萬無一失。</span><span class="sxs-lookup"><span data-stu-id="64687-220">A connection test will automatically start when you save your changes, make sure that it has successfully passed.</span></span>  
4. <span data-ttu-id="64687-221">繼續第 4 部分。</span><span class="sxs-lookup"><span data-stu-id="64687-221">Proceed to Part 4.</span></span>

## <a name="part-4-starting-your-job-from-last-stopped-time"></a><span data-ttu-id="64687-222">第 4 部分：從上次停止的時間開始您的工作</span><span class="sxs-lookup"><span data-stu-id="64687-222">Part 4: Starting your job from last stopped time</span></span>
1. <span data-ttu-id="64687-223">離開輸入/輸出：</span><span class="sxs-lookup"><span data-stu-id="64687-223">Navigate away from the Input/Output:</span></span>  
   ![graphic40][graphic40]
2. <span data-ttu-id="64687-225">按一下 [開始] 命令：</span><span class="sxs-lookup"><span data-stu-id="64687-225">Click the Start command:</span></span>  
   ![graphic41][graphic41]
3. <span data-ttu-id="64687-227">挑選 [上次停止時間]，然後按一下 [確定]： </span><span class="sxs-lookup"><span data-stu-id="64687-227">Pick the Last Stopped Time and click OK:</span></span>  
   ![graphic42][graphic42]
4. <span data-ttu-id="64687-229">繼續第 5 部分。</span><span class="sxs-lookup"><span data-stu-id="64687-229">Proceed to Part 5.</span></span>  

## <a name="part-5-removing-the-old-set-of-credentials"></a><span data-ttu-id="64687-230">第 5 部分：移除舊的認證集</span><span class="sxs-lookup"><span data-stu-id="64687-230">Part 5: Removing the old set of credentials</span></span>
<span data-ttu-id="64687-231">此部分適用於下列的輸入/輸出：</span><span class="sxs-lookup"><span data-stu-id="64687-231">This part is applicable to the following inputs/outputs:</span></span>

* <span data-ttu-id="64687-232">Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="64687-232">Blob Storage</span></span>
* <span data-ttu-id="64687-233">事件中樞</span><span class="sxs-lookup"><span data-stu-id="64687-233">Event Hubs</span></span>
* <span data-ttu-id="64687-234">SQL Database</span><span class="sxs-lookup"><span data-stu-id="64687-234">SQL Database</span></span>
* <span data-ttu-id="64687-235">資料表儲存體</span><span class="sxs-lookup"><span data-stu-id="64687-235">Table Storage</span></span>

### <a name="blob-storagetable-storage"></a><span data-ttu-id="64687-236">Blob 儲存體/資料表儲存體 </span><span class="sxs-lookup"><span data-stu-id="64687-236">Blob storage/Table storage</span></span>
<span data-ttu-id="64687-237">為工作以前使用的存取金鑰，重複第 1 部分，以更新現在未使用的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="64687-237">Repeat Part 1 for the Access Key that was previously used by your job to renew the now unused Access Key.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="64687-238">事件中樞</span><span class="sxs-lookup"><span data-stu-id="64687-238">Event hubs</span></span>
<span data-ttu-id="64687-239">為工作以前使用的金鑰，重複第 1 部分，以更新現在未使用的金鑰。</span><span class="sxs-lookup"><span data-stu-id="64687-239">Repeat Part 1 for the Key that was previously used by your job to renew the now unused Key.</span></span>

### <a name="sql-database"></a><span data-ttu-id="64687-240">SQL Database</span><span class="sxs-lookup"><span data-stu-id="64687-240">SQL Database</span></span>
1. <span data-ttu-id="64687-241">從第 1 部分的步驟 7 回到查詢視窗，然後輸入下列查詢，即可將 <previous_login_name> 換成作業先前使用的使用者名稱：</span><span class="sxs-lookup"><span data-stu-id="64687-241">Go back to the query window from Part 1 Step 7 and type in the following query, replacing <previous_login_name> with the User Name that was previously used by your job:</span></span>  
   `DROP LOGIN <previous_login_name>`  
2. <span data-ttu-id="64687-242">按一下 [執行]：</span><span class="sxs-lookup"><span data-stu-id="64687-242">Click Run:</span></span>  
   ![graphic43][graphic43]  

<span data-ttu-id="64687-244">系統應該會要求您進行以下確認：</span><span class="sxs-lookup"><span data-stu-id="64687-244">You should get the following confirmation:</span></span> 

    Command(s) completed successfully.

## <a name="get-help"></a><span data-ttu-id="64687-245">取得說明</span><span class="sxs-lookup"><span data-stu-id="64687-245">Get help</span></span>
<span data-ttu-id="64687-246">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="64687-246">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="64687-247">後續步驟</span><span class="sxs-lookup"><span data-stu-id="64687-247">Next steps</span></span>
* [<span data-ttu-id="64687-248">Azure Stream Analytics 介紹</span><span class="sxs-lookup"><span data-stu-id="64687-248">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="64687-249">開始使用 Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="64687-249">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="64687-250">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="64687-250">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="64687-251">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="64687-251">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="64687-252">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="64687-252">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

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

