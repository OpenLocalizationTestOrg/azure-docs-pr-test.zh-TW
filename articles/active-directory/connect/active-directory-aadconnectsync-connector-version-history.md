---
title: "aaaConnector 版本發行記錄 |Microsoft 文件"
description: "本主題列出 hello 連接器的所有版本 Forefront Identity Manager (FIM) 和 Microsoft Identity Manager (MIM)"
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
ms.openlocfilehash: 3522f17c30e46542eaa367ecdefdfd2fc47f71a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connector-version-release-history"></a><span data-ttu-id="ea208-103">連接器版本發行歷程記錄</span><span class="sxs-lookup"><span data-stu-id="ea208-103">Connector Version Release History</span></span>
<span data-ttu-id="ea208-104">Forefront Identity Manager (FIM) 和 Microsoft Identity Manager (MIM) hello 連接器會經常更新。</span><span class="sxs-lookup"><span data-stu-id="ea208-104">hello Connectors for Forefront Identity Manager (FIM) and Microsoft Identity Manager (MIM) are updated frequently.</span></span>

> [!NOTE]
> <span data-ttu-id="ea208-105">本主題僅討論 FIM 與 MIM。</span><span class="sxs-lookup"><span data-stu-id="ea208-105">This topic is on FIM and MIM only.</span></span> <span data-ttu-id="ea208-106">不支援在 Azure AD Connect 上安裝這些連接器。</span><span class="sxs-lookup"><span data-stu-id="ea208-106">These Connectors are not supported for install on Azure AD Connect.</span></span> <span data-ttu-id="ea208-107">發行的連接器在升級 toospecified 組建時，會預先安裝在 AADConnect。</span><span class="sxs-lookup"><span data-stu-id="ea208-107">Released Connectors are preinstalled on AADConnect when upgrading toospecified Build.</span></span>

<span data-ttu-id="ea208-108">本主題列出 hello 連接器已發行的所有的版本。</span><span class="sxs-lookup"><span data-stu-id="ea208-108">This topic list all versions of hello Connectors that have been released.</span></span>

<span data-ttu-id="ea208-109">相關連結：</span><span class="sxs-lookup"><span data-stu-id="ea208-109">Related links:</span></span>

* [<span data-ttu-id="ea208-110">下載最新的連接器</span><span class="sxs-lookup"><span data-stu-id="ea208-110">Download Latest Connectors</span></span>](http://go.microsoft.com/fwlink/?LinkId=717495)
* <span data-ttu-id="ea208-111">[一般 LDAP 連接器](active-directory-aadconnectsync-connector-genericldap.md) 參考文件</span><span class="sxs-lookup"><span data-stu-id="ea208-111">[Generic LDAP Connector](active-directory-aadconnectsync-connector-genericldap.md) reference documentation</span></span>
* <span data-ttu-id="ea208-112">[一般 SQL 連接器](active-directory-aadconnectsync-connector-genericsql.md) 參考文件</span><span class="sxs-lookup"><span data-stu-id="ea208-112">[Generic SQL Connector](active-directory-aadconnectsync-connector-genericsql.md) reference documentation</span></span>
* <span data-ttu-id="ea208-113">[Web 服務連接器](http://go.microsoft.com/fwlink/?LinkID=226245) 參考文件</span><span class="sxs-lookup"><span data-stu-id="ea208-113">[Web Services Connector](http://go.microsoft.com/fwlink/?LinkID=226245) reference documentation</span></span>
* <span data-ttu-id="ea208-114">[PowerShell 連接器](active-directory-aadconnectsync-connector-powershell.md) 參考文件</span><span class="sxs-lookup"><span data-stu-id="ea208-114">[PowerShell Connector](active-directory-aadconnectsync-connector-powershell.md) reference documentation</span></span>
* <span data-ttu-id="ea208-115">[Lotus Domino 連接器](active-directory-aadconnectsync-connector-domino.md) 參考文件</span><span class="sxs-lookup"><span data-stu-id="ea208-115">[Lotus Domino Connector](active-directory-aadconnectsync-connector-domino.md) reference documentation</span></span>


## <a name="116040-aadconnect-pending-release"></a><span data-ttu-id="ea208-116">1.1.604.0 (AADConnect 擱置版本)</span><span class="sxs-lookup"><span data-stu-id="ea208-116">1.1.604.0 (AADConnect Pending Release)</span></span>


### <a name="fixed-issues"></a><span data-ttu-id="ea208-117">已修正的問題：</span><span class="sxs-lookup"><span data-stu-id="ea208-117">Fixed issues:</span></span>

* <span data-ttu-id="ea208-118">一般 Web 服務︰</span><span class="sxs-lookup"><span data-stu-id="ea208-118">Generic Web Services:</span></span>
  * <span data-ttu-id="ea208-119">已修正在有兩個或多個端點時無法建立 SOAP 專案的問題。</span><span class="sxs-lookup"><span data-stu-id="ea208-119">Fixed an issue preventing a SOAP project from being created when there were two or more endpoints.</span></span>
* <span data-ttu-id="ea208-120">一般 SQL：</span><span class="sxs-lookup"><span data-stu-id="ea208-120">Generic SQL:</span></span>
  * <span data-ttu-id="ea208-121">Hello 匯入作業中 hello GSQL 已不會將轉換時間是否正確，當儲存 tooconnector 空間。</span><span class="sxs-lookup"><span data-stu-id="ea208-121">In hello operation of import hello GSQL was not converting time correctly, when saved tooconnector space.</span></span> <span data-ttu-id="ea208-122">hello 預設日期和時間格式的 hello GSQL 連接器空間已經從 'yyyy MM dd: ssz' too'yyyy-MM-dd: ssz '。</span><span class="sxs-lookup"><span data-stu-id="ea208-122">hello default date and time format for connector space of hello GSQL was changed from 'yyyy-MM-dd hh:mm:ssZ' too'yyyy-MM-dd HH:mm:ssZ'.</span></span>

## <a name="115510-aadconnect-115530"></a><span data-ttu-id="ea208-123">1.1.551.0 (AADConnect 1.1.553.0)</span><span class="sxs-lookup"><span data-stu-id="ea208-123">1.1.551.0 (AADConnect 1.1.553.0)</span></span>

### <a name="fixed-issues"></a><span data-ttu-id="ea208-124">已修正的問題：</span><span class="sxs-lookup"><span data-stu-id="ea208-124">Fixed issues:</span></span>

* <span data-ttu-id="ea208-125">一般 Web 服務︰</span><span class="sxs-lookup"><span data-stu-id="ea208-125">Generic Web Services:</span></span>
  * <span data-ttu-id="ea208-126">hello Wsconfig 工具未轉換正確 hello Json 陣列，從 「 範例要求 」 hello REST 服務方法。</span><span class="sxs-lookup"><span data-stu-id="ea208-126">hello Wsconfig tool did not convert correctly hello Json array from "sample request" for hello REST service method.</span></span> <span data-ttu-id="ea208-127">這會造成問題的序列化 hello REST 要求此 Json 陣列。</span><span class="sxs-lookup"><span data-stu-id="ea208-127">This caused problems with serialization this Json array for hello REST request.</span></span>
  * <span data-ttu-id="ea208-128">Web 服務連接器組態工具不支援在 JSON 屬性名稱中使用空間符號</span><span class="sxs-lookup"><span data-stu-id="ea208-128">Web Service Connector Configuration Tool does not support usage of space symbols in JSON attribute names</span></span> 
    * <span data-ttu-id="ea208-129">取代模式可以手動新增 toohello WSConfigTool.exe.config 檔案，例如：```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```</span><span class="sxs-lookup"><span data-stu-id="ea208-129">A Substitution pattern can be added manually toohello WSConfigTool.exe.config file, e.g. ```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```</span></span>

* <span data-ttu-id="ea208-130">Lotus Notes：</span><span class="sxs-lookup"><span data-stu-id="ea208-130">Lotus Notes:</span></span>
  * <span data-ttu-id="ea208-131">當 hello 選項**公司/組織單位可讓自訂 certifiers**已停用將 hello 連接器無法在匯出後 hello 匯出傳送所有屬性 （更新） 期間會匯出的 tooDomino，但在 hello 時間匯出 KeyNotFoundException 會傳回 tooSync。</span><span class="sxs-lookup"><span data-stu-id="ea208-131">When hello option **Allow custom certifiers for Organization/Organizational Units** is disabled then hello connector fails during export (Update) After hello export flow all attributes are exported tooDomino but at hello time of export a KeyNotFoundException is returned tooSync.</span></span> 
    * <span data-ttu-id="ea208-132">藉由變更下列 hello 屬性的其中一個主要原因是嘗試 toochange DN （使用者名稱屬性） 時，hello 重新命名作業將會失敗：</span><span class="sxs-lookup"><span data-stu-id="ea208-132">This happens because hello rename operation fails when it tries toochange DN (UserName attribute) by changing one of hello attributes below:</span></span>  
      - <span data-ttu-id="ea208-133">姓氏</span><span class="sxs-lookup"><span data-stu-id="ea208-133">LastName</span></span>
      - <span data-ttu-id="ea208-134">FirstName</span><span class="sxs-lookup"><span data-stu-id="ea208-134">FirstName</span></span>
      - <span data-ttu-id="ea208-135">MiddleInitial</span><span class="sxs-lookup"><span data-stu-id="ea208-135">MiddleInitial</span></span>
      - <span data-ttu-id="ea208-136">AltFullName</span><span class="sxs-lookup"><span data-stu-id="ea208-136">AltFullName</span></span>
      - <span data-ttu-id="ea208-137">AltFullNameLanguage</span><span class="sxs-lookup"><span data-stu-id="ea208-137">AltFullNameLanguage</span></span>
      - <span data-ttu-id="ea208-138">ou</span><span class="sxs-lookup"><span data-stu-id="ea208-138">ou</span></span>
      - <span data-ttu-id="ea208-139">altcommonname</span><span class="sxs-lookup"><span data-stu-id="ea208-139">altcommonname</span></span>

  * <span data-ttu-id="ea208-140">當 [允許組織/組織單位使用自訂認證者] 選項啟用，但必要的認證者仍然空白時，就會出現 KeyNotFoundException。</span><span class="sxs-lookup"><span data-stu-id="ea208-140">When **Allow custom certifiers for Organization/Organizational Units** option is enabled, but required certifiers are still empty, then KeyNotFoundException occurs.</span></span>

### <a name="enhancements"></a><span data-ttu-id="ea208-141">增強功能：</span><span class="sxs-lookup"><span data-stu-id="ea208-141">Enhancements:</span></span>

* <span data-ttu-id="ea208-142">一般 SQL：</span><span class="sxs-lookup"><span data-stu-id="ea208-142">Generic SQL:</span></span>
  * <span data-ttu-id="ea208-143">**情節：重新設計的實作：** "*" 功能</span><span class="sxs-lookup"><span data-stu-id="ea208-143">**Scenario: redesigned Implemented:** "*" feature</span></span>
  * <span data-ttu-id="ea208-144">**解決方案說明：**已變更[多重值參照屬性處理方法](active-directory-aadconnectsync-connector-genericsql.md)。</span><span class="sxs-lookup"><span data-stu-id="ea208-144">**Solution description:** Changed approach for [multi-valued reference attributes handling](active-directory-aadconnectsync-connector-genericsql.md).</span></span>


### <a name="fixed-issues"></a><span data-ttu-id="ea208-145">已修正的問題：</span><span class="sxs-lookup"><span data-stu-id="ea208-145">Fixed issues:</span></span>

* <span data-ttu-id="ea208-146">一般 Web 服務︰</span><span class="sxs-lookup"><span data-stu-id="ea208-146">Generic Web Services:</span></span>
  * <span data-ttu-id="ea208-147">如果 WebService 連接器存在，則無法匯入伺服器組態</span><span class="sxs-lookup"><span data-stu-id="ea208-147">Can’t import Server configuration if WebService Connector is present</span></span>
  * <span data-ttu-id="ea208-148">WebService 連接器不使用多個 Web 服務</span><span class="sxs-lookup"><span data-stu-id="ea208-148">WebService Connector is not working with multiple  Web Services</span></span>

* <span data-ttu-id="ea208-149">一般 SQL：</span><span class="sxs-lookup"><span data-stu-id="ea208-149">Generic SQL:</span></span>
  * <span data-ttu-id="ea208-150">不列出單一值所參照屬性的物件類型</span><span class="sxs-lookup"><span data-stu-id="ea208-150">No object types are listed for single value referenced attribute</span></span>
  * <span data-ttu-id="ea208-151">移除多重值資料表中的值時，變更追蹤策略上的差異匯入會刪除物件</span><span class="sxs-lookup"><span data-stu-id="ea208-151">Delta import on Change Tracking strategy deletes object when value is removed from multi-value table</span></span>
  * <span data-ttu-id="ea208-152">GSQL 連線器中的 OverflowException 與 AS/400 上的 DB2</span><span class="sxs-lookup"><span data-stu-id="ea208-152">OverflowException in GSQL connector with DB2 on AS/400</span></span>

<span data-ttu-id="ea208-153">Lotus：</span><span class="sxs-lookup"><span data-stu-id="ea208-153">Lotus:</span></span>
  * <span data-ttu-id="ea208-154">加入的選項 tooenable\disable 開啟 GlobalParameters 頁面之前搜尋的 Ou</span><span class="sxs-lookup"><span data-stu-id="ea208-154">Added option tooenable\disable searching OUs before opening GlobalParameters page</span></span>

## <a name="114430"></a><span data-ttu-id="ea208-155">1.1.443.0</span><span class="sxs-lookup"><span data-stu-id="ea208-155">1.1.443.0</span></span>

<span data-ttu-id="ea208-156">發行日期：2017 年 3 月</span><span class="sxs-lookup"><span data-stu-id="ea208-156">Released: 2017 March</span></span>

### <a name="enhancements"></a><span data-ttu-id="ea208-157">增強功能</span><span class="sxs-lookup"><span data-stu-id="ea208-157">Enhancements</span></span>

* <span data-ttu-id="ea208-158">一般 SQL：</span><span class="sxs-lookup"><span data-stu-id="ea208-158">Generic SQL:</span></span></br><span data-ttu-id="ea208-159">
  **案例徵兆：**它是以 hello SQL Connector 我們只允許參考 tooone 物件類型而且需要與成員的交叉參考已知的限制。</span><span class="sxs-lookup"><span data-stu-id="ea208-159">
  **Scenario Symptoms:**  It is a well-known limitation with hello SQL Connector where we only allow a reference tooone object type and require cross reference with members.</span></span> </br><span data-ttu-id="ea208-160">
**方案的描述：** hello 處理步驟的參考是"*"選擇選項，回復 toohello 同步處理引擎會傳回所有物件類型的組合。</span><span class="sxs-lookup"><span data-stu-id="ea208-160">
**Solution description:** In hello processing step for references were "*" option is chosen, ALL combinations of object types will be returned back toohello sync engine.</span></span>

>[!Important]
- <span data-ttu-id="ea208-161">這會造成許多預留位置</span><span class="sxs-lookup"><span data-stu-id="ea208-161">This will create many placeholders</span></span>
- <span data-ttu-id="ea208-162">它是必要的 toomake 確定 hello 命名為唯一跨物件類型。</span><span class="sxs-lookup"><span data-stu-id="ea208-162">It is required toomake sure hello naming is unique cross object types.</span></span>


* <span data-ttu-id="ea208-163">一般 LDAP：</span><span class="sxs-lookup"><span data-stu-id="ea208-163">Generic LDAP:</span></span></br><span data-ttu-id="ea208-164">
 **案例：**只有幾個容器會選取特定的資料分割中，然後 hello 搜尋仍會執行整個分割區中。</span><span class="sxs-lookup"><span data-stu-id="ea208-164">
**Scenario:** When only few containers are selected in specific partition, then hello search still will be done in whole partition.</span></span> <span data-ttu-id="ea208-165">詳細資料會依同步處理服務來進行篩選，而不是依可能會造成效能降低的 MA。</span><span class="sxs-lookup"><span data-stu-id="ea208-165">Specific will be filtered by Synchronization Service, but not by MA which might cause performance degradation.</span></span> </br>

 <span data-ttu-id="ea208-166">**方案的描述：**變更 GLDAP 連接器的程式碼 toomake 它可能瀏覽所有容器，並在每個項目，而不是在 hello 整個分割區中搜尋中搜尋物件。</span><span class="sxs-lookup"><span data-stu-id="ea208-166">**Solution description:** Changed GLDAP connector's code toomake it possible go through all containers and search objects in each of them, instead of searching in hello whole partition.</span></span>


* <span data-ttu-id="ea208-167">Lotus Domino：</span><span class="sxs-lookup"><span data-stu-id="ea208-167">Lotus Domino:</span></span>

  <span data-ttu-id="ea208-168">**案例︰**在匯出期間移除人員時支援刪除 Domino 郵件。</span><span class="sxs-lookup"><span data-stu-id="ea208-168">**Scenario:** Domino mail deletion support for a person removal during an export.</span></span> </br><span data-ttu-id="ea208-169">
  **解決方案︰**可設定在匯出期間移除人員時刪除 Domino 郵件的支援。</span><span class="sxs-lookup"><span data-stu-id="ea208-169">
**Solution:** Configurable mail deletion support for a person removal during an export.</span></span>

### <a name="fixed-issues"></a><span data-ttu-id="ea208-170">已修正的問題：</span><span class="sxs-lookup"><span data-stu-id="ea208-170">Fixed issues:</span></span>
* <span data-ttu-id="ea208-171">一般 Web 服務︰</span><span class="sxs-lookup"><span data-stu-id="ea208-171">Generic Web Services:</span></span>
 * <span data-ttu-id="ea208-172">則會發生下列錯誤 hello 預設變更 hello 服務 URL 時 SAP wsconfig 規劃透過 web 服務組態工具： 找不到 hello 路徑的一部分</span><span class="sxs-lookup"><span data-stu-id="ea208-172">When changing hello service URL in Default SAP wsconfig projects through WebService Configuration Tool then hello following error happens: Could not find a part of hello path</span></span>

      ``'C:\Users\cstpopovaz\AppData\Local\Temp\2\e2c9d9b0-0d8a-4409-b059-dceeb900a2b3\b9bedcc0-88ac-454c-8c69-7d6ea1c41d17\cfg.config\cloneconfig.xml'. ``

* <span data-ttu-id="ea208-173">一般 LDAP：</span><span class="sxs-lookup"><span data-stu-id="ea208-173">Generic LDAP:</span></span>
 * <span data-ttu-id="ea208-174">GLDAP 連接器無法看到 AD LDS 中的所有屬性</span><span class="sxs-lookup"><span data-stu-id="ea208-174">GLDAP Connector does not see all attributes in AD LDS</span></span>
 * <span data-ttu-id="ea208-175">精靈偵測不到任何 UPN 屬性從 hello LDAP 目錄結構描述時的符號</span><span class="sxs-lookup"><span data-stu-id="ea208-175">Wizard breaks when no UPN attributes are detected from hello LDAP directory schema</span></span>
 * <span data-ttu-id="ea208-176">如果未選取 "objectclass" 屬性，完整匯入期間不會顯示差異匯入的探索失敗錯誤</span><span class="sxs-lookup"><span data-stu-id="ea208-176">Delta Imports Failing with discovery errors not present during full import, when "objectclass" attribute is not selected</span></span>
 * <span data-ttu-id="ea208-177">「 設定資料分割和階層 」 設定 頁面中，不會顯示哪種類型是等於 toohello Novel 伺服器 hello 泛型中的資料分割的任何物件</span><span class="sxs-lookup"><span data-stu-id="ea208-177">A "Configure Partitions and Hierarchies” configuration page, doesn’t show any objects which type is equal toohello partition for Novel servers in hello Generic</span></span>  
<span data-ttu-id="ea208-178">LDAP MA。</span><span class="sxs-lookup"><span data-stu-id="ea208-178">LDAP MA.</span></span> <span data-ttu-id="ea208-179">頁面上只會顯示來自 RootDSE 資料分割的物件。</span><span class="sxs-lookup"><span data-stu-id="ea208-179">They showed only objects from RootDSE partition.</span></span>


* <span data-ttu-id="ea208-180">一般 SQL：</span><span class="sxs-lookup"><span data-stu-id="ea208-180">Generic SQL:</span></span>
 * <span data-ttu-id="ea208-181">修正未匯入一般 SQL 浮水印差異匯入多重值屬性的錯誤</span><span class="sxs-lookup"><span data-stu-id="ea208-181">Fix for Generic SQL watermark Delta Import multivalued attribute not imported bug</span></span>
 * <span data-ttu-id="ea208-182">匯出作業刪除\新增多重值屬性的值時，不會在資料來源中刪除\新增這些值。</span><span class="sxs-lookup"><span data-stu-id="ea208-182">When exporting deleted\added values of multivalued attribute, they are not deleted\added in data source.</span></span>  


* <span data-ttu-id="ea208-183">Lotus Notes：</span><span class="sxs-lookup"><span data-stu-id="ea208-183">Lotus Notes:</span></span>
 * <span data-ttu-id="ea208-184">「 完整名稱 」 顯示 hello metaverse 中正確但是時匯出 tooNotes hello 值 hello 屬性是 Null 或空的特定欄位。</span><span class="sxs-lookup"><span data-stu-id="ea208-184">A specific field "Full Name" is shown in hello metaverse correctly however when exporting tooNotes hello value for hello attribute is Null or Empty.</span></span>
 * <span data-ttu-id="ea208-185">修正重複認證者錯誤</span><span class="sxs-lookup"><span data-stu-id="ea208-185">Fix for duplicate Certifier error</span></span>
 * <span data-ttu-id="ea208-186">與其他物件的 hello Lotus Domino 連接器上選取 hello 物件沒有任何資料時然後我們收到 hello 探索錯誤時執行完整匯入。</span><span class="sxs-lookup"><span data-stu-id="ea208-186">When hello Object without any data is selected on hello Lotus Domino Connector with other objects then we receive hello Discovery error while performing Full-Import.</span></span>
 * <span data-ttu-id="ea208-187">差異匯入時正在執行上 hello Lotus Domino 連接器，在該回合，hello 的 hello 結尾 Microsoft.IdentityManagement.MA.LotusDomino.Service.exe 服務有時會傳回應用程式錯誤。</span><span class="sxs-lookup"><span data-stu-id="ea208-187">When Delta Import is being running on hello Lotus Domino Connector, at hello end of that run, hello Microsoft.IdentityManagement.MA.LotusDomino.Service.exe service sometimes returns an Application Error.</span></span>
 * <span data-ttu-id="ea208-188">群組成員資格的整體運作正常，仍會保留，但執行 hello 匯出 tootry tooremove 使用者時從成員資格顯示為成功安裝更新後，但不會實際取得 Lotus Notes 的成員資格中移除 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="ea208-188">Group membership overall works fine and is maintained, except when running hello export tootry tooremove a user from membership it shows as successful with an update, but hello user doesn’t actually get removed from membership in Lotus Notes.</span></span>
 * <span data-ttu-id="ea208-189">匯出為 「 在下方的附加項目 」 的機會 toochoose 模式已在組態中加入 GUI Lotus MA tooappend 新項目底部多重值屬性的 hello 匯出期間。</span><span class="sxs-lookup"><span data-stu-id="ea208-189">An opportunity toochoose mode of export as “Append Item at bottom” was added in configuration GUI of Lotus MA tooappend new items at bottom during hello export for multi-valued attributes.</span></span>
 * <span data-ttu-id="ea208-190">連接器會將 hello 需要邏輯 toodelete hello 檔案從 hello 郵件資料夾和識別碼保存庫。</span><span class="sxs-lookup"><span data-stu-id="ea208-190">Connector will add hello needed logic toodelete hello file from hello Mail Folder and ID Vault.</span></span>
 * <span data-ttu-id="ea208-191">刪除成員資格時不會跨 NAB 成員進行。</span><span class="sxs-lookup"><span data-stu-id="ea208-191">Delete membership not working for cross NAB member.</span></span>
 * <span data-ttu-id="ea208-192">值應該會成功從多重值屬性中刪除</span><span class="sxs-lookup"><span data-stu-id="ea208-192">Values should be successfully deleted from multi-valued attribute</span></span>

## <a name="111170"></a><span data-ttu-id="ea208-193">1.1.117.0</span><span class="sxs-lookup"><span data-stu-id="ea208-193">1.1.117.0</span></span>
<span data-ttu-id="ea208-194">發行日期：2016 年 3 月</span><span class="sxs-lookup"><span data-stu-id="ea208-194">Released: 2016 March</span></span>

<span data-ttu-id="ea208-195">**一般 SQL 連接器**</span><span class="sxs-lookup"><span data-stu-id="ea208-195">**New Connector**</span></span>  
<span data-ttu-id="ea208-196">初始版本的 hello[泛型 SQL Connector](active-directory-aadconnectsync-connector-genericsql.md)。</span><span class="sxs-lookup"><span data-stu-id="ea208-196">Initial release of hello [Generic SQL Connector](active-directory-aadconnectsync-connector-genericsql.md).</span></span>

<span data-ttu-id="ea208-197">**新功能︰**</span><span class="sxs-lookup"><span data-stu-id="ea208-197">**New features:**</span></span>

* <span data-ttu-id="ea208-198">一般 LDAP 連接器：</span><span class="sxs-lookup"><span data-stu-id="ea208-198">Generic LDAP Connector:</span></span>
  * <span data-ttu-id="ea208-199">新增使用 Isode 進行差異匯入的支援。</span><span class="sxs-lookup"><span data-stu-id="ea208-199">Added support for delta import with Isode.</span></span>
* <span data-ttu-id="ea208-200">Web 服務連接器：</span><span class="sxs-lookup"><span data-stu-id="ea208-200">Web Services Connector:</span></span>
  * <span data-ttu-id="ea208-201">更新的 hello csEntryChangeResult 活動和 setImportErrorCode 活動 tooallow 物件層級錯誤 toobe 傳回後 toohello 同步處理引擎。</span><span class="sxs-lookup"><span data-stu-id="ea208-201">Updated hello csEntryChangeResult activity and setImportErrorCode activity tooallow object level errors toobe returned back toohello sync engine.</span></span>
  * <span data-ttu-id="ea208-202">更新的 hello SAP6 和 SAP6User 範本 toouse hello 新物件層級錯誤功能。</span><span class="sxs-lookup"><span data-stu-id="ea208-202">Updated hello SAP6 and SAP6User templates toouse hello new object level error functionality.</span></span>
* <span data-ttu-id="ea208-203">Lotus Domino 連接器：</span><span class="sxs-lookup"><span data-stu-id="ea208-203">Lotus Domino Connector:</span></span>
  * <span data-ttu-id="ea208-204">進行匯出時，您需要針對每個通訊錄使用一個認證者。</span><span class="sxs-lookup"><span data-stu-id="ea208-204">For export, you need one certifier per address book.</span></span> <span data-ttu-id="ea208-205">您可以現在使用 hello 相同密碼的所有 certifiers toomake hello 管理更容易。</span><span class="sxs-lookup"><span data-stu-id="ea208-205">You can now use hello same password for all certifiers toomake hello management easier.</span></span>

<span data-ttu-id="ea208-206">**已修正的問題：**</span><span class="sxs-lookup"><span data-stu-id="ea208-206">**Fixed issues:**</span></span>

* <span data-ttu-id="ea208-207">一般 LDAP 連接器：</span><span class="sxs-lookup"><span data-stu-id="ea208-207">Generic LDAP Connector:</span></span>
  * <span data-ttu-id="ea208-208">針對 IBM Tivoli DS，並未正確偵測到某些參考屬性。</span><span class="sxs-lookup"><span data-stu-id="ea208-208">For IBM Tivoli DS, some reference attributes were not detected correctly.</span></span>
  * <span data-ttu-id="ea208-209">若為差異匯入期間開啟 LDAP，已截斷空白字元 hello 開頭和結尾的字串。</span><span class="sxs-lookup"><span data-stu-id="ea208-209">For Open LDAP during a delta import, whitespaces at hello beginning and end of strings were truncated.</span></span>
  * <span data-ttu-id="ea208-210">Novell 與 NetIQ，Ou/容器之間，而在 hello 移動物件的匯出相同的時間已重新命名的 hello 物件失敗。</span><span class="sxs-lookup"><span data-stu-id="ea208-210">For Novell and NetIQ, an export that moved an object between OUs/containers and at hello same time renamed hello object failed.</span></span>
* <span data-ttu-id="ea208-211">Web 服務連接器：</span><span class="sxs-lookup"><span data-stu-id="ea208-211">Web Services Connector:</span></span>
  * <span data-ttu-id="ea208-212">如果 hello web 服務在相同的繫結的多個端點，然後 hello 連接器未正確地探索這些端點。</span><span class="sxs-lookup"><span data-stu-id="ea208-212">If hello web service had multiple end-points for same binding, then hello Connector did not correctly discover these end-points.</span></span>
* <span data-ttu-id="ea208-213">Lotus Domino 連接器：</span><span class="sxs-lookup"><span data-stu-id="ea208-213">Lotus Domino Connector:</span></span>
  * <span data-ttu-id="ea208-214">匯出的 hello fullName 屬性 tooa mail 在資料庫無法運作。</span><span class="sxs-lookup"><span data-stu-id="ea208-214">An export of hello fullName attribute tooa mail-in database did not work.</span></span>
  * <span data-ttu-id="ea208-215">匯出會同時加入和從群組移除成員，只匯出的 hello 加入成員。</span><span class="sxs-lookup"><span data-stu-id="ea208-215">An export which both added and removed member from a group only exported hello added members.</span></span>
  * <span data-ttu-id="ea208-216">如果是無效的資訊文件 （hello 屬性 isValid 設定 toofalse），然後 hello 連接器會失敗。</span><span class="sxs-lookup"><span data-stu-id="ea208-216">If a Notes Document is invalid (hello attribute isValid set toofalse), then hello Connector fails.</span></span>

## <a name="older-releases"></a><span data-ttu-id="ea208-217">較舊的版本</span><span class="sxs-lookup"><span data-stu-id="ea208-217">Older releases</span></span>
<span data-ttu-id="ea208-218">2016 年 3 月前 hello 連接器已經發行支援 主題。</span><span class="sxs-lookup"><span data-stu-id="ea208-218">Before March 2016, hello Connectors were released as support topics.</span></span>

<span data-ttu-id="ea208-219">**一般 LDAP**</span><span class="sxs-lookup"><span data-stu-id="ea208-219">**Generic LDAP**</span></span>

* <span data-ttu-id="ea208-220">[KB3078617](https://support.microsoft.com/kb/3078617) - 1.0.0597，2015 年 9 月</span><span class="sxs-lookup"><span data-stu-id="ea208-220">[KB3078617](https://support.microsoft.com/kb/3078617) - 1.0.0597, 2015 September</span></span>
* <span data-ttu-id="ea208-221">[KB3044896](https://support.microsoft.com/kb/3044896) - 1.0.0549，2015 年 3 月</span><span class="sxs-lookup"><span data-stu-id="ea208-221">[KB3044896](https://support.microsoft.com/kb/3044896) - 1.0.0549, 2015 March</span></span>
* <span data-ttu-id="ea208-222">[KB3031009](https://support.microsoft.com/kb/3031009) - 1.0.0534，2015 年 1 月</span><span class="sxs-lookup"><span data-stu-id="ea208-222">[KB3031009](https://support.microsoft.com/kb/3031009) - 1.0.0534, 2015 January</span></span>
* <span data-ttu-id="ea208-223">[KB3008177](https://support.microsoft.com/kb/3008177) - 1.0.0419，2014 年 9 月</span><span class="sxs-lookup"><span data-stu-id="ea208-223">[KB3008177](https://support.microsoft.com/kb/3008177) - 1.0.0419, 2014 September</span></span>
* <span data-ttu-id="ea208-224">[KB2936070](https://support.microsoft.com/kb/2936070) - 4.3.1082，2014 年 3 月</span><span class="sxs-lookup"><span data-stu-id="ea208-224">[KB2936070](https://support.microsoft.com/kb/2936070) - 4.3.1082, 2014 March</span></span>

<span data-ttu-id="ea208-225">**WebServices**</span><span class="sxs-lookup"><span data-stu-id="ea208-225">**WebServices**</span></span>

* <span data-ttu-id="ea208-226">[KB3008178](https://support.microsoft.com/kb/3008178) - 1.0.0419，2014 年 9 月</span><span class="sxs-lookup"><span data-stu-id="ea208-226">[KB3008178](https://support.microsoft.com/kb/3008178) - 1.0.0419, 2014 September</span></span>

<span data-ttu-id="ea208-227">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="ea208-227">**PowerShell**</span></span>

* <span data-ttu-id="ea208-228">[KB3008179](https://support.microsoft.com/kb/3008179) - 1.0.0419，2014 年 9 月</span><span class="sxs-lookup"><span data-stu-id="ea208-228">[KB3008179](https://support.microsoft.com/kb/3008179) - 1.0.0419, 2014 September</span></span>

<span data-ttu-id="ea208-229">**Lotus Domino**</span><span class="sxs-lookup"><span data-stu-id="ea208-229">**Lotus Domino**</span></span>

* <span data-ttu-id="ea208-230">[KB3096533](https://support.microsoft.com/kb/3096533) - 1.0.0597，2015 年 9 月</span><span class="sxs-lookup"><span data-stu-id="ea208-230">[KB3096533](https://support.microsoft.com/kb/3096533) - 1.0.0597, 2015 September</span></span>
* <span data-ttu-id="ea208-231">[KB3044895](https://support.microsoft.com/kb/3044895) - 1.0.0549，2015 年 3 月</span><span class="sxs-lookup"><span data-stu-id="ea208-231">[KB3044895](https://support.microsoft.com/kb/3044895) - 1.0.0549, 2015 March</span></span>
* <span data-ttu-id="ea208-232">[KB2977286](https://support.microsoft.com/kb/2977286) - 5.3.0712，2014 年 8 月</span><span class="sxs-lookup"><span data-stu-id="ea208-232">[KB2977286](https://support.microsoft.com/kb/2977286) - 5.3.0712, 2014 August</span></span>
* <span data-ttu-id="ea208-233">[KB2932635](https://support.microsoft.com/kb/2932635) - 5.3.1003，2014 年 2 月</span><span class="sxs-lookup"><span data-stu-id="ea208-233">[KB2932635](https://support.microsoft.com/kb/2932635) - 5.3.1003, 2014 February</span></span>  
* <span data-ttu-id="ea208-234">[KB2899874](https://support.microsoft.com/kb/2899874) - 5.3.0721，2013 年 10 月</span><span class="sxs-lookup"><span data-stu-id="ea208-234">[KB2899874](https://support.microsoft.com/kb/2899874) - 5.3.0721, 2013 October</span></span>
* <span data-ttu-id="ea208-235">[KB2875551](https://support.microsoft.com/kb/2875551) - 5.3.0534，2013 年 8 月</span><span class="sxs-lookup"><span data-stu-id="ea208-235">[KB2875551](https://support.microsoft.com/kb/2875551) - 5.3.0534, 2013 August</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea208-236">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ea208-236">Next steps</span></span>
<span data-ttu-id="ea208-237">深入了解 hello [Azure AD Connect 同步處理](active-directory-aadconnectsync-whatis.md)組態。</span><span class="sxs-lookup"><span data-stu-id="ea208-237">Learn more about hello [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="ea208-238">深入了解 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。</span><span class="sxs-lookup"><span data-stu-id="ea208-238">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
