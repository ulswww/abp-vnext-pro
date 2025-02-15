# 文件模块

- 与 abp 自带的文件模块不一样，此模块接入阿里云 oss 作为云存储。
- 前端上传文件到 OSS,文件模块保存相对路径。

![](../../../img/file.png)

## 安装

- Lion.Abp.FileManagement.Application
- Lion.Abp.FileManagement.Application.Contracts
- Lion.Abp.FileManagement.Domain
- Lion.Abp.FileManagement.Domain.Shared
- Lion.Abp.FileManagement.EntityFrameworkCore
- Lion.Abp.FileManagement.HttpApi
- Lion.Abp.FileManagement.HttpApi.Client

## 模块依赖

- 添加 DependsOn(typeof(FileManagementXxxModule)) 特性到对应模块。
- 在 EntityFrameworkCore 层添加数据库配置在 AbpProDbContext.cs 的 OnModelCreating()方法中添加 builder.ConfigureFileManagement();

## 实体

**File** 表结构：

| 字段名               | 描述         | 类型     |
| :------------------- | :----------- | :------- |
| Id                   | Id           | Guid     |
| TenantId             | 租户 id      | Guid?    |
| FileName             | 文件名称     | string   |
| FilePath             | 文件路径     | string   |
| IsDeleted            | 是否删除     | bool     |
| DeleterId            | 删除人       | Guid?    |
| DeletionTime         | 删除时间     | DateTime |
| LastModifierId       | 最后修改人   | Guid?    |
| LastModificationTime | 最后修改时间 | DateTime |
| CreatorId            | 创建人       | Guid?    |
| CreationTime         | 创建时间     | DateTime |

## OSS 配置

[阿里云 OSS 配置](https://help.aliyun.com/document_detail/100624.html)

- 将 OSS 配置添加到 AppSetting

## AppSetting 配置

```Json
  "AliYun": {
    "OSS": {
      "AccessKeyId": "LTAI5tLkt3vvScGPVZ5qKJDc1S",
      "AccessKeySecret": "BixV8vP5uPrbsdwjYzzsEXOPjkxPST12S",
      "Endpoint": "oss-cn-shenzhen.aliyuncs.com",
      "ContainerName": "lion-abp-pro",
      "RegionId": "oss-cn-shenzhen",
      "RoleArn": "acs:ram::1846393972471789:role/ramosst1t"
    }
  }
```

## 上传组件

- [前端 UploadOss.ts](https://github.com/WangJunZzz/abp-vnext-pro/blob/main/vben28/src/views/admin/files/UploadOss.ts)
