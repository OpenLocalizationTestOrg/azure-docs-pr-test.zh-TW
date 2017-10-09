
### <a name="cacheskuname"></a>cacheSKUName
hello 定價層的 hello 新的 Azure Redis 快取。

    "cacheSKUName": {
      "type": "string",
      "allowedValues": [
        "Basic",
        "Standard"
      ],
      "defaultValue": "Basic",
      "metadata": {
        "description": "hello pricing tier of hello new Azure Redis Cache."
      }
    },

hello 範本定義 hello 值，允許這個參數 （基本或標準），並指派的預設值 （基本），如果未不指定任何值。 Basic 提供具有向上 too53 GB 可用的多個大小的單一節點。
標準提供兩個節點主要/複本可用總 too53 GB 和 99.9 %sla 的多個大小。

### <a name="cacheskufamily"></a>cacheSKUFamily
hello hello sku 系列。

    "cacheSKUFamily": {
      "type": "string",
      "allowedValues": [
        "C"
      ],
      "defaultValue": "C",
      "metadata": {
        "description": "hello family for hello sku."
      }
    },


### <a name="cacheskucapacity"></a>cacheSKUCapacity
hello hello 新 Azure Redis 快取執行個體的大小。 

    "cacheSKUCapacity": {
      "type": "int",
      "allowedValues": [
        0,
        1,
        2,
        3,
        4,
        5,
        6
      ],
      "defaultValue": 0,
      "metadata": {
        "description": "hello size of hello new Azure Redis Cache instance. "
      }
    }


hello 範本可定義 hello （0、 1、 2、 3、 4、 5 或 6），此參數允許的值，並指派的預設值 (1)，如果未不指定任何值。 這些數字對應 toofollowing 快取大小： 0 = 250 MB，1 = 1 GB，2 = 2.5 GB，3 = 6 GB，4 = 13 GB，5 = 26 GB，6 = 53 GB

