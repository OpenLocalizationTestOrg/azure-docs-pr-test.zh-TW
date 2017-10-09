## <a name="incremental-and-complete-deployments"></a>累加部署與完整部署
在部署您的資源，您可以指定 hello 部署是累加式更新或完整更新。 hello 這兩種模式之間的主要差異是資源管理員處理 hello 資源群組中的 hello 範本中的現有資源的方式：

* 在完整模式中，資源管理員**刪除**hello 資源群組中存在但 hello 範本中未指定的資源。 
* 在累加式模式中，資源管理員**會保留不變**hello 資源群組中存在但 hello 範本中未指定的資源。

這兩種模式中的資源管理員會嘗試 tooprovision hello 範本中指定的所有資源。 如果 hello 資源已存在於 hello 資源群組，而且其設定維持不變，hello 操作就會導致沒有變更。 如果您變更資源的 hello 設定，這些新的設定佈建 hello 資源。 如果您嘗試 tooupdate hello 位置或現有的資源類型，hello 部署會失敗並發生錯誤。 相反地，部署新的資源與 hello 位置，或輸入您需要。

根據預設，資源管理員會使用 hello 累加模式。

tooillustrate hello 差異增量和完整模式，請考慮下列案例中的 hello。

**現有資源群組**包含︰

* 資源 A
* 資源 B
* 資源 C

**範本**定義：

* 資源 A
* 資源 B
* 資源 D

在部署時**累加**模式中，hello 資源群組包含：

* 資源 A
* 資源 B
* 資源 C
* 資源 D

若部署在**完整**模式中，資源 C 會遭到刪除。 hello 資源群組包含：

* 資源 A
* 資源 B
* 資源 D
