---
title: SQL Server 安全性
ms.date: 03/30/2017
ms.assetid: 9053724d-a1fb-4f0f-b9dc-7f6dd893e8ff
ms.openlocfilehash: c5fd9cc82a3b1e4ffa217d65c542376fe067db06
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/07/2019
ms.locfileid: "70791632"
---
# <a name="sql-server-security"></a>SQL Server 安全性
SQL Server 具有多个支持创建安全数据库应用程序的功能。  
  
 不管您要使用哪个版本的 SQL Server，一般性的安全注意事项（如数据盗窃和蓄意破坏）都适用。 数据完整性也应视为安全问题。 如果数据不加保护，则在允许对数据执行临时操作并且数据被有意或无意修改（添加错误的值或完全删除）的情况下，数据可能会变得毫无价值。 此外，通常还有一些必须遵守的法定要求，如正确存储机密信息。 完全禁止存储某些类型的个人数据，具体取决于特定司法范围内适用的法律。  
  
 和每个版本的 Windows 一样，每个版本的 SQL Server 都具有不同的安全功能，版本越高，功能越强。 必须了解的是，安全功能本身不能保证数据库应用程序的安全。 每个数据库应用程序都具有独特的要求、执行环境、部署模型、物理位置和用户人群。 范围限于本地的一些应用程序可能只需要最低的安全性，而其他本地应用程序或通过 Internet 部署的应用程序可能需要严格的安全措施和实时监控和评估。  
  
 SQL Server 数据库应用程序的安全要求应该在设计时加以考虑，而不应事后考虑。 在开发周期的初期评估危胁可以减轻检测到漏洞时造成的潜在损害。  
  
 即使应用程序的初始设计非常可靠，但随着系统的发展，仍可能会出现新的危胁。 通过在数据库周围构建多道防线，可以最大程度地减轻安全侵犯事件所造成的损害。 第一道防线是通过仅授予完全必要的权限而不授予更多权限来减小攻击面。  
  
 本节中的主题简要说明 SQL Server 中与开发人员相关的安全功能，并提供到 SQL Server 联机丛书中相关主题和提供更详细说明的其他资源的链接。  
  
## <a name="in-this-section"></a>本节内容  
 [SQL Server 安全性概述](overview-of-sql-server-security.md)  
 说明 SQL Server 的体系结构和安全功能。  
  
 [SQL Server 中的应用程序安全性方案](application-security-scenarios-in-sql-server.md)  
 包含论述 ADO.NET 和 SQL Server 应用程序各种应用程序安全方案的主题。  
  
 [SQL Server Express 安全性](sql-server-express-security.md)  
 描述 SQL Server Express 的安全注意事项。  
  
## <a name="related-sections"></a>相关章节  
[SQL Server 数据库引擎和 Azure SQL Database 的安全中心](/sql/relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database)  
描述 SQL Server 和 Azure SQL 数据库的安全注意事项。

[SQL Server 安装的安全注意事项](/sql/sql-server/install/security-considerations-for-a-sql-server-installation)  
描述在安装 SQL Server 之前要考虑的安全问题。

## <a name="see-also"></a>请参阅

- [保证 ADO.NET 应用程序的安全](../securing-ado-net-applications.md)
- [SQL Server 和 ADO.NET](index.md)
