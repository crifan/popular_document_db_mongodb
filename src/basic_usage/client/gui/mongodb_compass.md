# MongoDB Compass

TODO:

* [【已解决】MongoDB Compass中如何快速高效地刷新数据](http://www.crifan.com/mongo_compass_fast_effective_reload_refresh_latest_data%0A)

## 下载和安装MongoDB Compass

根据官网介绍

[Download and Install Compass — MongoDB Compass stable](https://docs.mongodb.com/compass/master/install/)

去下载页面

[Compass | MongoDB](https://www.mongodb.com/products/compass)

下载安装包

比如Mac的是

https://downloads.mongodb.com/compass/mongodb-compass-1.14.5-darwin-x64.dmg

下载后，安装即可。安装后是：

![mac_installed_mongodb_compass](../../../assets/img/mac_installed_mongodb_compass.png)

当前版本是：`1.14.5`

![mongodb_compass_version](../../../assets/img/mongodb_compass_version.png)

## 基本使用

打开后，进入连接数据库页：

![mongodb_compass_connect_to_host](../../../assets/img/mongodb_compass_connect_to_host.png)

点击连接后，进入数据库列表页：

### 创建数据库和集合

![mongodb_compass_create_database](../../../assets/img/mongodb_compass_create_database.png)

![mongodb_compass_db_collection_name](../../../assets/img/mongodb_compass_db_collection_name.png)

![mongodb_compass_db_list](../../../assets/img/mongodb_compass_db_list.png)

![mongodb_compass_collection_list](../../../assets/img/mongodb_compass_collection_list.png)

### 写入数据

点击`INSERT DOCUMENT`：

![mongodb_compass_click_insert_document](../../../assets/img/mongodb_compass_click_insert_document.png)

会出现编辑数据的弹框：

![mongodb_compass_insert_document_popup](../../../assets/img/mongodb_compass_insert_document_popup.png)

输入对应的数据的`key`和`value`，如果想要新增字段，则点击左边的 `加号` ➕，会弹出 `Add Field after xxx`：

![mongodb_compass_insert_key_value_str](../../../assets/img/mongodb_compass_insert_key_value_str.png)

数据的类型，除了默认的`String`，还支持其他类型，比如`Array`数组：

![mongodb_compass_insert_array](../../../assets/img/mongodb_compass_insert_array.png)

分别输入数组的每项的值后，点击`INSERT`：

![mongodb_compass_input_array_values](../../../assets/img/mongodb_compass_input_array_values.png)

即可返回列表页，看到刚插入的数据：

![mongodb_compass_inserted_new_document](../../../assets/img/mongodb_compass_inserted_new_document.png)

### 删除数据库

![mongodb_compass_drop_database](../../../assets/img/mongodb_compass_drop_database.png)

## 好用之处

### 直接编辑内容

截图举例：

![mongodb compass edit in place](../../../assets/img/mongodb_compass_edit_in_place.png)

### 字段可以很方便的折叠和展开

点击每条记录前面的箭头：

![mongodb key can expand](../../../assets/img/mongodb_compass_key_can_expand.png)

即可展开所有字段：

![mongodb expand all info](../../../assets/img/mongodb_compass_expanded_all_info.png)

再次点击，即可缩回。

## 其他实际使用效果举例

![mongodb_compass_screenshot_1](../../../assets/img/mongodb_compass_screenshot_1.png)

![mongodb_compass_expand_detail](../../../assets/img/mongodb_compass_expand_detail.png)

## 功能特性介绍=引导页

引导页有截图介绍其好用的功能和特点，供参考：

### Perfromance Charts

![mongodb_compass_guide_1](../../../assets/img/mongodb_compass_guide_1.png)

### Sidebar Redesigned

![mongodb_compass_guide_2](../../../assets/img/mongodb_compass_guide_2.png)

### Visualize your Schema

![mongodb_compass_guide_3](../../../assets/img/mongodb_compass_guide_3.png)

### Build Geo Queries

![mongodb_compass_guide_4](../../../assets/img/mongodb_compass_guide_4.png)

### Interactive Document Editor

![mongodb_compass_guide_5](../../../assets/img/mongodb_compass_guide_5.png)

### Visual Explain Plains

![mongodb_compass_guide_6](../../../assets/img/mongodb_compass_guide_6.png)

### Index Management

![mongodb_compass_guide_7](../../../assets/img/mongodb_compass_guide_7.png)

### Document Validation

![mongodb_compass_guide_8](../../../assets/img/mongodb_compass_guide_8.png)

### Improved CURD

![mongodb_compass_guide_9](../../../assets/img/mongodb_compass_guide_9.png)

### Deployment Awareness

![mongodb_compass_guide_10](../../../assets/img/mongodb_compass_guide_10.png)

### Query History

![mongodb_compass_guide_11](../../../assets/img/mongodb_compass_guide_11.png)
