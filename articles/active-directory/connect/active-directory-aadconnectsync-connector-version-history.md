---
title: "連接器版本發行歷程記錄 | Microsoft Docs"
description: "本主題列出所有適用於 Forefront Identity Manager (FIM) 和 Microsoft Identity Manager (MIM) 的連接器版本"
services: active-directory
documentationcenter: 
author: fimguy
manager: femila
editor: 
ms.assetid: 6a0c66ab-55df-4669-a0c7-1fe1a091a7f9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: fimguy
ms.openlocfilehash: 313145f4d8e5faa91fb3504cb0fd0ba87ca2e379
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="connector-version-release-history"></a><span data-ttu-id="1725d-103">連接器版本發行歷程記錄</span><span class="sxs-lookup"><span data-stu-id="1725d-103">Connector Version Release History</span></span>
<span data-ttu-id="1725d-104">適用於 Forefront Identity Manager (FIM) 和 Microsoft Identity Manager (MIM) 的連接器會經常更新。</span><span class="sxs-lookup"><span data-stu-id="1725d-104">The Connectors for Forefront Identity Manager (FIM) and Microsoft Identity Manager (MIM) are updated frequently.</span></span>

> [!NOTE]
> <span data-ttu-id="1725d-105">本主題僅討論 FIM 與 MIM。</span><span class="sxs-lookup"><span data-stu-id="1725d-105">This topic is on FIM and MIM only.</span></span> <span data-ttu-id="1725d-106">不支援在 Azure AD Connect 上安裝這些連接器。</span><span class="sxs-lookup"><span data-stu-id="1725d-106">These Connectors are not supported for install on Azure AD Connect.</span></span> <span data-ttu-id="1725d-107">升級至指定的組建時，會在 AADConnect 上預先安裝發行的連接器。</span><span class="sxs-lookup"><span data-stu-id="1725d-107">Released Connectors are preinstalled on AADConnect when upgrading to specified Build.</span></span>

<span data-ttu-id="1725d-108">本主題會列出所有已發行的連接器版本。</span><span class="sxs-lookup"><span data-stu-id="1725d-108">This topic list all versions of the Connectors that have been released.</span></span>

<span data-ttu-id="1725d-109">相關連結：</span><span class="sxs-lookup"><span data-stu-id="1725d-109">Related links:</span></span>

* [<span data-ttu-id="1725d-110">下載最新的連接器</span><span class="sxs-lookup"><span data-stu-id="1725d-110">Download Latest Connectors</span></span>](http://go.microsoft.com/fwlink/?LinkId=717495)
* <span data-ttu-id="1725d-111">[一般 LDAP 連接器](active-directory-aadconnectsync-connector-genericldap.md) 參考文件</span><span class="sxs-lookup"><span data-stu-id="1725d-111">[Generic LDAP Connector](active-directory-aadconnectsync-connector-genericldap.md) reference documentation</span></span>
* <span data-ttu-id="1725d-112">[一般 SQL 連接器](active-directory-aadconnectsync-connector-genericsql.md) 參考文件</span><span class="sxs-lookup"><span data-stu-id="1725d-112">[Generic SQL Connector](active-directory-aadconnectsync-connector-genericsql.md) reference documentation</span></span>
* <span data-ttu-id="1725d-113">[Web 服務連接器](http://go.microsoft.com/fwlink/?LinkID=226245) 參考文件</span><span class="sxs-lookup"><span data-stu-id="1725d-113">[Web Services Connector](http://go.microsoft.com/fwlink/?LinkID=226245) reference documentation</span></span>
* <span data-ttu-id="1725d-114">[PowerShell 連接器](active-directory-aadconnectsync-connector-powershell.md) 參考文件</span><span class="sxs-lookup"><span data-stu-id="1725d-114">[PowerShell Connector](active-directory-aadconnectsync-connector-powershell.md) reference documentation</span></span>
* <span data-ttu-id="1725d-115">[Lotus Domino 連接器](active-directory-aadconnectsync-connector-domino.md) 參考文件</span><span class="sxs-lookup"><span data-stu-id="1725d-115">[Lotus Domino Connector](active-directory-aadconnectsync-connector-domino.md) reference documentation</span></span>


## <a name="116040-aadconnect-pending-release"></a><span data-ttu-id="1725d-116">1.1.604.0 (AADConnect 擱置版本)</span><span class="sxs-lookup"><span data-stu-id="1725d-116">1.1.604.0 (AADConnect Pending Release)</span></span>


### <a name="fixed-issues"></a><span data-ttu-id="1725d-117">已修正的問題：</span><span class="sxs-lookup"><span data-stu-id="1725d-117">Fixed issues:</span></span>

* <span data-ttu-id="1725d-118">一般 Web 服務︰</span><span class="sxs-lookup"><span data-stu-id="1725d-118">Generic Web Services:</span></span>
  * <span data-ttu-id="1725d-119">已修正在有兩個或多個端點時無法建立 SOAP 專案的問題。</span><span class="sxs-lookup"><span data-stu-id="1725d-119">Fixed an issue preventing a SOAP project from being created when there were two or more endpoints.</span></span>
* <span data-ttu-id="1725d-120">一般 SQL：</span><span class="sxs-lookup"><span data-stu-id="1725d-120">Generic SQL:</span></span>
  * <span data-ttu-id="1725d-121">在匯入作業中，當 GSQL 儲存至連接器空間時，並未正確轉換時間。</span><span class="sxs-lookup"><span data-stu-id="1725d-121">In the operation of import the GSQL was not converting time correctly, when saved to connector space.</span></span> <span data-ttu-id="1725d-122">GSQL 連接器空間的預設日期和時間格式已從 'yyyy-MM-dd hh:mm:ssZ' 變更為 'yyyy-MM-dd HH:mm:ssZ'。</span><span class="sxs-lookup"><span data-stu-id="1725d-122">The default date and time format for connector space of the GSQL was changed from 'yyyy-MM-dd hh:mm:ssZ' to 'yyyy-MM-dd HH:mm:ssZ'.</span></span>

## <a name="115510-aadconnect-115530"></a><span data-ttu-id="1725d-123">1.1.551.0 (AADConnect 1.1.553.0)</span><span class="sxs-lookup"><span data-stu-id="1725d-123">1.1.551.0 (AADConnect 1.1.553.0)</span></span>

### <a name="fixed-issues"></a><span data-ttu-id="1725d-124">已修正的問題：</span><span class="sxs-lookup"><span data-stu-id="1725d-124">Fixed issues:</span></span>

* <span data-ttu-id="1725d-125">一般 Web 服務︰</span><span class="sxs-lookup"><span data-stu-id="1725d-125">Generic Web Services:</span></span>
  * <span data-ttu-id="1725d-126">Wsconfig 工具未正確地從 REST 服務方法的「範例要求」轉換 Json 陣列。</span><span class="sxs-lookup"><span data-stu-id="1725d-126">The Wsconfig tool did not convert correctly the Json array from "sample request" for the REST service method.</span></span> <span data-ttu-id="1725d-127">這會造成 REST 要求的 Json 陣列發生序列化問題。</span><span class="sxs-lookup"><span data-stu-id="1725d-127">This caused problems with serialization this Json array for the REST request.</span></span>
  * <span data-ttu-id="1725d-128">Web 服務連接器組態工具不支援在 JSON 屬性名稱中使用空間符號</span><span class="sxs-lookup"><span data-stu-id="1725d-128">Web Service Connector Configuration Tool does not support usage of space symbols in JSON attribute names</span></span> 
    * <span data-ttu-id="1725d-129">可以手動將取代模式新增至 WSConfigTool.exe.config 檔案，例如 ```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```</span><span class="sxs-lookup"><span data-stu-id="1725d-129">A Substitution pattern can be added manually to the WSConfigTool.exe.config file, e.g. ```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```</span></span>

* <span data-ttu-id="1725d-130">Lotus Notes：</span><span class="sxs-lookup"><span data-stu-id="1725d-130">Lotus Notes:</span></span>
  * <span data-ttu-id="1725d-131">當 [允許組織/組織單位使用自訂認證者] 選項停用時，連接器在匯出 (更新) 期間會失敗。在匯出流程之後，所有屬性都匯出至 Domino，但在匯出時，KeyNotFoundException 會傳回給 Sync。</span><span class="sxs-lookup"><span data-stu-id="1725d-131">When the option **Allow custom certifiers for Organization/Organizational Units** is disabled then the connector fails during export (Update) After the export flow all attributes are exported to Domino but at the time of export a KeyNotFoundException is returned to Sync.</span></span> 
    * <span data-ttu-id="1725d-132">這是因為重新命名作業在嘗試變更下列其中一個屬性來變更 DN (UserName 屬性) 時失敗：</span><span class="sxs-lookup"><span data-stu-id="1725d-132">This happens because the rename operation fails when it tries to change DN (UserName attribute) by changing one of the attributes below:</span></span>  
      - <span data-ttu-id="1725d-133">姓氏</span><span class="sxs-lookup"><span data-stu-id="1725d-133">LastName</span></span>
      - <span data-ttu-id="1725d-134">FirstName</span><span class="sxs-lookup"><span data-stu-id="1725d-134">FirstName</span></span>
      - <span data-ttu-id="1725d-135">MiddleInitial</span><span class="sxs-lookup"><span data-stu-id="1725d-135">MiddleInitial</span></span>
      - <span data-ttu-id="1725d-136">AltFullName</span><span class="sxs-lookup"><span data-stu-id="1725d-136">AltFullName</span></span>
      - <span data-ttu-id="1725d-137">AltFullNameLanguage</span><span class="sxs-lookup"><span data-stu-id="1725d-137">AltFullNameLanguage</span></span>
      - <span data-ttu-id="1725d-138">ou</span><span class="sxs-lookup"><span data-stu-id="1725d-138">ou</span></span>
      - <span data-ttu-id="1725d-139">altcommonname</span><span class="sxs-lookup"><span data-stu-id="1725d-139">altcommonname</span></span>

  * <span data-ttu-id="1725d-140">當 [允許組織/組織單位使用自訂認證者] 選項啟用，但必要的認證者仍然空白時，就會出現 KeyNotFoundException。</span><span class="sxs-lookup"><span data-stu-id="1725d-140">When **Allow custom certifiers for Organization/Organizational Units** option is enabled, but required certifiers are still empty, then KeyNotFoundException occurs.</span></span>

### <a name="enhancements"></a><span data-ttu-id="1725d-141">增強功能：</span><span class="sxs-lookup"><span data-stu-id="1725d-141">Enhancements:</span></span>

* <span data-ttu-id="1725d-142">一般 SQL：</span><span class="sxs-lookup"><span data-stu-id="1725d-142">Generic SQL:</span></span>
  * <span data-ttu-id="1725d-143">**情節：重新設計的實作：** "*" 功能</span><span class="sxs-lookup"><span data-stu-id="1725d-143">**Scenario: redesigned Implemented:** "*" feature</span></span>
  * <span data-ttu-id="1725d-144">**解決方案說明：**已變更[多重值參照屬性處理方法](active-directory-aadconnectsync-connector-genericsql.md)。</span><span class="sxs-lookup"><span data-stu-id="1725d-144">**Solution description:** Changed approach for [multi-valued reference attributes handling](active-directory-aadconnectsync-connector-genericsql.md).</span></span>


### <a name="fixed-issues"></a><span data-ttu-id="1725d-145">已修正的問題：</span><span class="sxs-lookup"><span data-stu-id="1725d-145">Fixed issues:</span></span>

* <span data-ttu-id="1725d-146">一般 Web 服務︰</span><span class="sxs-lookup"><span data-stu-id="1725d-146">Generic Web Services:</span></span>
  * <span data-ttu-id="1725d-147">如果 WebService 連接器存在，則無法匯入伺服器組態</span><span class="sxs-lookup"><span data-stu-id="1725d-147">Can’t import Server configuration if WebService Connector is present</span></span>
  * <span data-ttu-id="1725d-148">WebService 連接器不使用多個 Web 服務</span><span class="sxs-lookup"><span data-stu-id="1725d-148">WebService Connector is not working with multiple  Web Services</span></span>

* <span data-ttu-id="1725d-149">一般 SQL：</span><span class="sxs-lookup"><span data-stu-id="1725d-149">Generic SQL:</span></span>
  * <span data-ttu-id="1725d-150">不列出單一值所參照屬性的物件類型</span><span class="sxs-lookup"><span data-stu-id="1725d-150">No object types are listed for single value referenced attribute</span></span>
  * <span data-ttu-id="1725d-151">移除多重值資料表中的值時，變更追蹤策略上的差異匯入會刪除物件</span><span class="sxs-lookup"><span data-stu-id="1725d-151">Delta import on Change Tracking strategy deletes object when value is removed from multi-value table</span></span>
  * <span data-ttu-id="1725d-152">GSQL 連線器中的 OverflowException 與 AS/400 上的 DB2</span><span class="sxs-lookup"><span data-stu-id="1725d-152">OverflowException in GSQL connector with DB2 on AS/400</span></span>

<span data-ttu-id="1725d-153">Lotus：</span><span class="sxs-lookup"><span data-stu-id="1725d-153">Lotus:</span></span>
  * <span data-ttu-id="1725d-154">已新增在開啟 GlobalParameters 頁面之前可啟用\停用搜尋 OU 的選項</span><span class="sxs-lookup"><span data-stu-id="1725d-154">Added option to enable\disable searching OUs before opening GlobalParameters page</span></span>

## <a name="114430"></a><span data-ttu-id="1725d-155">1.1.443.0</span><span class="sxs-lookup"><span data-stu-id="1725d-155">1.1.443.0</span></span>

<span data-ttu-id="1725d-156">發行日期：2017 年 3 月</span><span class="sxs-lookup"><span data-stu-id="1725d-156">Released: 2017 March</span></span>

### <a name="enhancements"></a><span data-ttu-id="1725d-157">增強功能</span><span class="sxs-lookup"><span data-stu-id="1725d-157">Enhancements</span></span>

* <span data-ttu-id="1725d-158">一般 SQL：</span><span class="sxs-lookup"><span data-stu-id="1725d-158">Generic SQL:</span></span></br><span data-ttu-id="1725d-159">
  **案例徵兆︰**SQL 連接器的已知限制，一個物件類型只允許一個參考，且成員需要交互參考。</span><span class="sxs-lookup"><span data-stu-id="1725d-159">
  **Scenario Symptoms:**  It is a well-known limitation with the SQL Connector where we only allow a reference to one object type and require cross reference with members.</span></span> </br><span data-ttu-id="1725d-160">
**解決方案說明︰**在已選擇 "*" 選項之參考的處理步驟中，物件類型的所有組合會傳回給同步處理引擎。</span><span class="sxs-lookup"><span data-stu-id="1725d-160">
**Solution description:** In the processing step for references were "*" option is chosen, ALL combinations of object types will be returned back to the sync engine.</span></span>

>[!Important]
- <span data-ttu-id="1725d-161">這會造成許多預留位置</span><span class="sxs-lookup"><span data-stu-id="1725d-161">This will create many placeholders</span></span>
- <span data-ttu-id="1725d-162">必須確定名稱在物件類型之間是唯一的。</span><span class="sxs-lookup"><span data-stu-id="1725d-162">It is required to make sure the naming is unique cross object types.</span></span>


* <span data-ttu-id="1725d-163">一般 LDAP：</span><span class="sxs-lookup"><span data-stu-id="1725d-163">Generic LDAP:</span></span></br><span data-ttu-id="1725d-164">
 **案例︰**只選取了特定資料分割中的幾個容器時，仍會對整個資料分割執行搜尋。</span><span class="sxs-lookup"><span data-stu-id="1725d-164">
**Scenario:** When only few containers are selected in specific partition, then the search still will be done in whole partition.</span></span> <span data-ttu-id="1725d-165">詳細資料會依同步處理服務來進行篩選，而不是依可能會造成效能降低的 MA。</span><span class="sxs-lookup"><span data-stu-id="1725d-165">Specific will be filtered by Synchronization Service, but not by MA which might cause performance degradation.</span></span> </br>

 <span data-ttu-id="1725d-166">**解決方案說明︰**變更了 GLDAP 連接器的程式碼，使其可以瀏覽過所有容器，並搜尋各容器中的物件，而非在整個資料分割中搜尋。</span><span class="sxs-lookup"><span data-stu-id="1725d-166">**Solution description:** Changed GLDAP connector's code to make it possible go through all containers and search objects in each of them, instead of searching in the whole partition.</span></span>


* <span data-ttu-id="1725d-167">Lotus Domino：</span><span class="sxs-lookup"><span data-stu-id="1725d-167">Lotus Domino:</span></span>

  <span data-ttu-id="1725d-168">**案例︰**在匯出期間移除人員時支援刪除 Domino 郵件。</span><span class="sxs-lookup"><span data-stu-id="1725d-168">**Scenario:** Domino mail deletion support for a person removal during an export.</span></span> </br><span data-ttu-id="1725d-169">
  **解決方案︰**可設定在匯出期間移除人員時刪除 Domino 郵件的支援。</span><span class="sxs-lookup"><span data-stu-id="1725d-169">
**Solution:** Configurable mail deletion support for a person removal during an export.</span></span>

### <a name="fixed-issues"></a><span data-ttu-id="1725d-170">已修正的問題：</span><span class="sxs-lookup"><span data-stu-id="1725d-170">Fixed issues:</span></span>
* <span data-ttu-id="1725d-171">一般 Web 服務︰</span><span class="sxs-lookup"><span data-stu-id="1725d-171">Generic Web Services:</span></span>
 * <span data-ttu-id="1725d-172">透過 WebService 組態工具在預設的 SAP wsconfig 專案中變更服務 URL 時，發生下列錯誤︰找不到路徑的一部分</span><span class="sxs-lookup"><span data-stu-id="1725d-172">When changing the service URL in Default SAP wsconfig projects through WebService Configuration Tool then the following error happens: Could not find a part of the path</span></span>

      ``'C:\Users\cstpopovaz\AppData\Local\Temp\2\e2c9d9b0-0d8a-4409-b059-dceeb900a2b3\b9bedcc0-88ac-454c-8c69-7d6ea1c41d17\cfg.config\cloneconfig.xml'. ``

* <span data-ttu-id="1725d-173">一般 LDAP：</span><span class="sxs-lookup"><span data-stu-id="1725d-173">Generic LDAP:</span></span>
 * <span data-ttu-id="1725d-174">GLDAP 連接器無法看到 AD LDS 中的所有屬性</span><span class="sxs-lookup"><span data-stu-id="1725d-174">GLDAP Connector does not see all attributes in AD LDS</span></span>
 * <span data-ttu-id="1725d-175">從 LDAP 目錄結構描述偵測不到任何 UPN 屬性時，精靈會中斷</span><span class="sxs-lookup"><span data-stu-id="1725d-175">Wizard breaks when no UPN attributes are detected from the LDAP directory schema</span></span>
 * <span data-ttu-id="1725d-176">如果未選取 "objectclass" 屬性，完整匯入期間不會顯示差異匯入的探索失敗錯誤</span><span class="sxs-lookup"><span data-stu-id="1725d-176">Delta Imports Failing with discovery errors not present during full import, when "objectclass" attribute is not selected</span></span>
 * <span data-ttu-id="1725d-177">「設定資料分割和階層」組態頁面，不會在下列位置中顯示類型等於 Novel 伺服器之資料分割的任何物件：一般</span><span class="sxs-lookup"><span data-stu-id="1725d-177">A "Configure Partitions and Hierarchies” configuration page, doesn’t show any objects which type is equal to the partition for Novel servers in the Generic</span></span>  
<span data-ttu-id="1725d-178">LDAP MA。</span><span class="sxs-lookup"><span data-stu-id="1725d-178">LDAP MA.</span></span> <span data-ttu-id="1725d-179">頁面上只會顯示來自 RootDSE 資料分割的物件。</span><span class="sxs-lookup"><span data-stu-id="1725d-179">They showed only objects from RootDSE partition.</span></span>


* <span data-ttu-id="1725d-180">一般 SQL：</span><span class="sxs-lookup"><span data-stu-id="1725d-180">Generic SQL:</span></span>
 * <span data-ttu-id="1725d-181">修正未匯入一般 SQL 浮水印差異匯入多重值屬性的錯誤</span><span class="sxs-lookup"><span data-stu-id="1725d-181">Fix for Generic SQL watermark Delta Import multivalued attribute not imported bug</span></span>
 * <span data-ttu-id="1725d-182">匯出作業刪除\新增多重值屬性的值時，不會在資料來源中刪除\新增這些值。</span><span class="sxs-lookup"><span data-stu-id="1725d-182">When exporting deleted\added values of multivalued attribute, they are not deleted\added in data source.</span></span>  


* <span data-ttu-id="1725d-183">Lotus Notes：</span><span class="sxs-lookup"><span data-stu-id="1725d-183">Lotus Notes:</span></span>
 * <span data-ttu-id="1725d-184">Metaverse 會正確顯示特定欄位 [全名]，但匯出至 Notes 時，屬性值會是 Null 或空白。</span><span class="sxs-lookup"><span data-stu-id="1725d-184">A specific field "Full Name" is shown in the metaverse correctly however when exporting to Notes the value for the attribute is Null or Empty.</span></span>
 * <span data-ttu-id="1725d-185">修正重複認證者錯誤</span><span class="sxs-lookup"><span data-stu-id="1725d-185">Fix for duplicate Certifier error</span></span>
 * <span data-ttu-id="1725d-186">在 Lotus Domino 連接器上連同其他物件選取了沒有任何資料的物件時，我們會在執行完整匯入時收到探索錯誤。</span><span class="sxs-lookup"><span data-stu-id="1725d-186">When the Object without any data is selected on the Lotus Domino Connector with other objects then we receive the Discovery error while performing Full-Import.</span></span>
 * <span data-ttu-id="1725d-187">當 Lotus Domino 連接器上正在執行差異匯入時，於執行結束時，Microsoft.IdentityManagement.MA.LotusDomino.Service.exe 服務有時會傳回應用程式錯誤。</span><span class="sxs-lookup"><span data-stu-id="1725d-187">When Delta Import is being running on the Lotus Domino Connector, at the end of that run, the Microsoft.IdentityManagement.MA.LotusDomino.Service.exe service sometimes returns an Application Error.</span></span>
 * <span data-ttu-id="1725d-188">群組成員資格全都正常運作並保留下來，唯獨在執行匯出以試著從成員資格中移除某位使用者時，雖會顯示更新成功，但使用者實際上並未從 Lotus Notes 的成員資格中移除。</span><span class="sxs-lookup"><span data-stu-id="1725d-188">Group membership overall works fine and is maintained, except when running the export to try to remove a user from membership it shows as successful with an update, but the user doesn’t actually get removed from membership in Lotus Notes.</span></span>
 * <span data-ttu-id="1725d-189">Lotus MA 的組態 GUI 中新增了選擇「將項目附加在底部」做為匯出模式的機會，可在多重值屬性匯出期間將新項目附加在底部。</span><span class="sxs-lookup"><span data-stu-id="1725d-189">An opportunity to choose mode of export as “Append Item at bottom” was added in configuration GUI of Lotus MA to append new items at bottom during the export for multi-valued attributes.</span></span>
 * <span data-ttu-id="1725d-190">連接器會新增從「郵件資料夾」和「識別碼保存庫」中刪除檔案所需要的邏輯。</span><span class="sxs-lookup"><span data-stu-id="1725d-190">Connector will add the needed logic to delete the file from the Mail Folder and ID Vault.</span></span>
 * <span data-ttu-id="1725d-191">刪除成員資格時不會跨 NAB 成員進行。</span><span class="sxs-lookup"><span data-stu-id="1725d-191">Delete membership not working for cross NAB member.</span></span>
 * <span data-ttu-id="1725d-192">值應該會成功從多重值屬性中刪除</span><span class="sxs-lookup"><span data-stu-id="1725d-192">Values should be successfully deleted from multi-valued attribute</span></span>

## <a name="111170"></a><span data-ttu-id="1725d-193">1.1.117.0</span><span class="sxs-lookup"><span data-stu-id="1725d-193">1.1.117.0</span></span>
<span data-ttu-id="1725d-194">發行日期：2016 年 3 月</span><span class="sxs-lookup"><span data-stu-id="1725d-194">Released: 2016 March</span></span>

<span data-ttu-id="1725d-195">**一般 SQL 連接器**</span><span class="sxs-lookup"><span data-stu-id="1725d-195">**New Connector**</span></span>  
<span data-ttu-id="1725d-196">的 [一般 SQL 連接器](active-directory-aadconnectsync-connector-genericsql.md)初始版本。</span><span class="sxs-lookup"><span data-stu-id="1725d-196">Initial release of the [Generic SQL Connector](active-directory-aadconnectsync-connector-genericsql.md).</span></span>

<span data-ttu-id="1725d-197">**新功能︰**</span><span class="sxs-lookup"><span data-stu-id="1725d-197">**New features:**</span></span>

* <span data-ttu-id="1725d-198">一般 LDAP 連接器：</span><span class="sxs-lookup"><span data-stu-id="1725d-198">Generic LDAP Connector:</span></span>
  * <span data-ttu-id="1725d-199">新增使用 Isode 進行差異匯入的支援。</span><span class="sxs-lookup"><span data-stu-id="1725d-199">Added support for delta import with Isode.</span></span>
* <span data-ttu-id="1725d-200">Web 服務連接器：</span><span class="sxs-lookup"><span data-stu-id="1725d-200">Web Services Connector:</span></span>
  * <span data-ttu-id="1725d-201">已更新 csEntryChangeResult 活動和 setImportErrorCode 活動，可讓物件層級的錯誤傳回至同步處理引擎。</span><span class="sxs-lookup"><span data-stu-id="1725d-201">Updated the csEntryChangeResult activity and setImportErrorCode activity to allow object level errors to be returned back to the sync engine.</span></span>
  * <span data-ttu-id="1725d-202">已更新 SAP6 和 SAP6User 範本，以使用新的物件層級錯誤功能。</span><span class="sxs-lookup"><span data-stu-id="1725d-202">Updated the SAP6 and SAP6User templates to use the new object level error functionality.</span></span>
* <span data-ttu-id="1725d-203">Lotus Domino 連接器：</span><span class="sxs-lookup"><span data-stu-id="1725d-203">Lotus Domino Connector:</span></span>
  * <span data-ttu-id="1725d-204">進行匯出時，您需要針對每個通訊錄使用一個認證者。</span><span class="sxs-lookup"><span data-stu-id="1725d-204">For export, you need one certifier per address book.</span></span> <span data-ttu-id="1725d-205">您現在可以針對所有認證者使用相同的密碼，以便於管理。</span><span class="sxs-lookup"><span data-stu-id="1725d-205">You can now use the same password for all certifiers to make the management easier.</span></span>

<span data-ttu-id="1725d-206">**已修正的問題：**</span><span class="sxs-lookup"><span data-stu-id="1725d-206">**Fixed issues:**</span></span>

* <span data-ttu-id="1725d-207">一般 LDAP 連接器：</span><span class="sxs-lookup"><span data-stu-id="1725d-207">Generic LDAP Connector:</span></span>
  * <span data-ttu-id="1725d-208">針對 IBM Tivoli DS，並未正確偵測到某些參考屬性。</span><span class="sxs-lookup"><span data-stu-id="1725d-208">For IBM Tivoli DS, some reference attributes were not detected correctly.</span></span>
  * <span data-ttu-id="1725d-209">針對差異匯入期間的 Open LDAP，已截斷字串開頭和結尾的空格。</span><span class="sxs-lookup"><span data-stu-id="1725d-209">For Open LDAP during a delta import, whitespaces at the beginning and end of strings were truncated.</span></span>
  * <span data-ttu-id="1725d-210">針對 Novell 和 NetIQ，在 OU/容器之間移動物件且同時將物件重新命名的匯出會失敗。</span><span class="sxs-lookup"><span data-stu-id="1725d-210">For Novell and NetIQ, an export that moved an object between OUs/containers and at the same time renamed the object failed.</span></span>
* <span data-ttu-id="1725d-211">Web 服務連接器：</span><span class="sxs-lookup"><span data-stu-id="1725d-211">Web Services Connector:</span></span>
  * <span data-ttu-id="1725d-212">如果 Web 服務針對相同繫結具有多個端點，則連接器不會正確探索這些端點。</span><span class="sxs-lookup"><span data-stu-id="1725d-212">If the web service had multiple end-points for same binding, then the Connector did not correctly discover these end-points.</span></span>
* <span data-ttu-id="1725d-213">Lotus Domino 連接器：</span><span class="sxs-lookup"><span data-stu-id="1725d-213">Lotus Domino Connector:</span></span>
  * <span data-ttu-id="1725d-214">無法將 fullName 屬性匯出到郵件傳入資料庫。</span><span class="sxs-lookup"><span data-stu-id="1725d-214">An export of the fullName attribute to a mail-in database did not work.</span></span>
  * <span data-ttu-id="1725d-215">新增和移除群組成員的匯出只會匯出新增的成員。</span><span class="sxs-lookup"><span data-stu-id="1725d-215">An export which both added and removed member from a group only exported the added members.</span></span>
  * <span data-ttu-id="1725d-216">如果 Notes 文件無效 (將 isValid 屬性設為 false)，則連接器會失敗。</span><span class="sxs-lookup"><span data-stu-id="1725d-216">If a Notes Document is invalid (the attribute isValid set to false), then the Connector fails.</span></span>

## <a name="older-releases"></a><span data-ttu-id="1725d-217">較舊的版本</span><span class="sxs-lookup"><span data-stu-id="1725d-217">Older releases</span></span>
<span data-ttu-id="1725d-218">在 2016 年 3 月之前，已利用支援主題方式發行連接器。</span><span class="sxs-lookup"><span data-stu-id="1725d-218">Before March 2016, the Connectors were released as support topics.</span></span>

<span data-ttu-id="1725d-219">**一般 LDAP**</span><span class="sxs-lookup"><span data-stu-id="1725d-219">**Generic LDAP**</span></span>

* <span data-ttu-id="1725d-220">[KB3078617](https://support.microsoft.com/kb/3078617) - 1.0.0597，2015 年 9 月</span><span class="sxs-lookup"><span data-stu-id="1725d-220">[KB3078617](https://support.microsoft.com/kb/3078617) - 1.0.0597, 2015 September</span></span>
* <span data-ttu-id="1725d-221">[KB3044896](https://support.microsoft.com/kb/3044896) - 1.0.0549，2015 年 3 月</span><span class="sxs-lookup"><span data-stu-id="1725d-221">[KB3044896](https://support.microsoft.com/kb/3044896) - 1.0.0549, 2015 March</span></span>
* <span data-ttu-id="1725d-222">[KB3031009](https://support.microsoft.com/kb/3031009) - 1.0.0534，2015 年 1 月</span><span class="sxs-lookup"><span data-stu-id="1725d-222">[KB3031009](https://support.microsoft.com/kb/3031009) - 1.0.0534, 2015 January</span></span>
* <span data-ttu-id="1725d-223">[KB3008177](https://support.microsoft.com/kb/3008177) - 1.0.0419，2014 年 9 月</span><span class="sxs-lookup"><span data-stu-id="1725d-223">[KB3008177](https://support.microsoft.com/kb/3008177) - 1.0.0419, 2014 September</span></span>
* <span data-ttu-id="1725d-224">[KB2936070](https://support.microsoft.com/kb/2936070) - 4.3.1082，2014 年 3 月</span><span class="sxs-lookup"><span data-stu-id="1725d-224">[KB2936070](https://support.microsoft.com/kb/2936070) - 4.3.1082, 2014 March</span></span>

<span data-ttu-id="1725d-225">**WebServices**</span><span class="sxs-lookup"><span data-stu-id="1725d-225">**WebServices**</span></span>

* <span data-ttu-id="1725d-226">[KB3008178](https://support.microsoft.com/kb/3008178) - 1.0.0419，2014 年 9 月</span><span class="sxs-lookup"><span data-stu-id="1725d-226">[KB3008178](https://support.microsoft.com/kb/3008178) - 1.0.0419, 2014 September</span></span>

<span data-ttu-id="1725d-227">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="1725d-227">**PowerShell**</span></span>

* <span data-ttu-id="1725d-228">[KB3008179](https://support.microsoft.com/kb/3008179) - 1.0.0419，2014 年 9 月</span><span class="sxs-lookup"><span data-stu-id="1725d-228">[KB3008179](https://support.microsoft.com/kb/3008179) - 1.0.0419, 2014 September</span></span>

<span data-ttu-id="1725d-229">**Lotus Domino**</span><span class="sxs-lookup"><span data-stu-id="1725d-229">**Lotus Domino**</span></span>

* <span data-ttu-id="1725d-230">[KB3096533](https://support.microsoft.com/kb/3096533) - 1.0.0597，2015 年 9 月</span><span class="sxs-lookup"><span data-stu-id="1725d-230">[KB3096533](https://support.microsoft.com/kb/3096533) - 1.0.0597, 2015 September</span></span>
* <span data-ttu-id="1725d-231">[KB3044895](https://support.microsoft.com/kb/3044895) - 1.0.0549，2015 年 3 月</span><span class="sxs-lookup"><span data-stu-id="1725d-231">[KB3044895](https://support.microsoft.com/kb/3044895) - 1.0.0549, 2015 March</span></span>
* <span data-ttu-id="1725d-232">[KB2977286](https://support.microsoft.com/kb/2977286) - 5.3.0712，2014 年 8 月</span><span class="sxs-lookup"><span data-stu-id="1725d-232">[KB2977286](https://support.microsoft.com/kb/2977286) - 5.3.0712, 2014 August</span></span>
* <span data-ttu-id="1725d-233">[KB2932635](https://support.microsoft.com/kb/2932635) - 5.3.1003，2014 年 2 月</span><span class="sxs-lookup"><span data-stu-id="1725d-233">[KB2932635](https://support.microsoft.com/kb/2932635) - 5.3.1003, 2014 February</span></span>  
* <span data-ttu-id="1725d-234">[KB2899874](https://support.microsoft.com/kb/2899874) - 5.3.0721，2013 年 10 月</span><span class="sxs-lookup"><span data-stu-id="1725d-234">[KB2899874](https://support.microsoft.com/kb/2899874) - 5.3.0721, 2013 October</span></span>
* <span data-ttu-id="1725d-235">[KB2875551](https://support.microsoft.com/kb/2875551) - 5.3.0534，2013 年 8 月</span><span class="sxs-lookup"><span data-stu-id="1725d-235">[KB2875551](https://support.microsoft.com/kb/2875551) - 5.3.0534, 2013 August</span></span>

## <a name="next-steps"></a><span data-ttu-id="1725d-236">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1725d-236">Next steps</span></span>
<span data-ttu-id="1725d-237">深入了解 [Azure AD Connect 同步](active-directory-aadconnectsync-whatis.md) 組態。</span><span class="sxs-lookup"><span data-stu-id="1725d-237">Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="1725d-238">深入了解 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="1725d-238">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
