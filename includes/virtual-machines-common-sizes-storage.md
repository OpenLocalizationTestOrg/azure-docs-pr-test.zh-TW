
hello 數列最適合用於需要低度延遲暫時存放裝置，例如包括 Cassandra、 MongoDB、 Cloudera 的 NoSQL 資料庫而且 Redis 的工作負載。 hello 系列提供向上 too32 Vcpu、 使用 hello [Intel® Xeon® 處理器 E5 v3 系列](http://www.intel.com/content/www/us/en/processors/xeon/xeon-e5-solutions.html)。 hello 數列取得 hello 相同的 CPU 效能，因為 hello G/GS 系列和隨附的每個 vCPU 記憶體的 8 GiB。  

## <a name="ls-series"></a>Ls 系列

ACU：180 - 240
 
| 大小          | vCPU | 記憶體：GiB | 暫存儲存體 (SSD) GiB | 最大資料磁碟 | 最大快取和暫存儲存體輸送量︰IOPS / MBps (以 GiB 為單位的快取大小) | 最大取消快取的磁碟輸送量︰IOPS / MBps | 最大 NIC/預期的網路效能 (Mbps) | 
|---------------|-----------|-------------|--------------------------|----------------|-------------------------------------------------------------|-------------------------------------------|------------------------------| 
| Standard_L4s  | 4    | 32   | 678   | 8              | NA / NA (0)          | 5,000 / 125                               | 2 / 4000       | 
| Standard_L8s  | 8    | 64   | 1,388 | 16             | NA / NA (0)          | 10,000 / 250                              | 4 / 8000  | 
| Standard_L16s | 16   | 128  | 2,807 | 32             | NA / NA (0)          | 20,000 / 500                              | 8 / 6000 - 16000 &#8224; | 
| Standard_L32s* | 32 | 256  | 5,630 | 64             | NA / NA (0)          | 40,000 / 1,000                            | 8 / 20000 | 
 

hello 最大的磁碟輸送量可能與 Ls 系列 Vm 可能會受限於 hello 數目、 大小和條狀配置的任何連接的磁碟。 如需詳細資訊，請參閱 [進階儲存體：Azure 虛擬機器工作負載適用的高效能儲存體](../articles/storage/common/storage-premium-storage.md)。 

* 執行個體是隔離的 toohardware 專用的 tooa 單一客戶。

