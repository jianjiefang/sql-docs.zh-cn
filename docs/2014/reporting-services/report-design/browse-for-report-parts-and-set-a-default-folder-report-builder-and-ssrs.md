---
title: 浏览查找报表部件和设置默认文件夹（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 5cf38068-65d1-4fe8-81f3-a404d8fbc663
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2dd881c13b2398f3a1783f53190097653d04d78a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66106462"
---
# <a name="browse-for-report-parts-and-set-a-default-folder-report-builder-and-ssrs"></a>浏览查找报表部件和设置默认文件夹（报表生成器和 SSRS）
  创建报表的最简单方式是从报表部件库将现有报表部件（如表和图表）添加到您的报表。 将报表部件添加到报表时，还将添加它正常工作所需的所有内容。 例如，显示数据的任何报表部件都依赖于数据集，即对某数据源的查询和连接。 将报表部件添加到报表后，可以根据需要进行修改。  
  
 您可以设置一个默认文件夹，以便将报表部件发布到报表服务器或者与报表服务器相集成的 SharePoint 站点。  
  
 有关详细信息，请参阅 [报表部件（报表生成器和 SSRS）](../report-parts-report-builder-and-ssrs.md)。  
  
### <a name="to-browse-for-report-parts"></a>查找报表部件  
  
1.  在 **“插入”** 菜单上，单击 **“报表部件”** 。  
  
     如果尚未建立连接，请单击 **“连接到报表服务器”** ，然后输入名称。  
  
    > [!NOTE]  
    >  您必须连接到报表服务器以便查找报表部件。  
  
2.  可以通过指定有关报表部件的详细信息来缩小搜索范围。 在 **“搜索”** 框中键入所有或部分名称和说明，或单击 **“添加条件”** 以添加以下任意字段的值：  
  
    -   创建者  
  
    -   创建日期  
  
    -   上次修改日期  
  
    -   上次修改者  
  
    -   服务器文件夹  
  
    -   类型  
  
     例如，若要查找图像，请单击 **“添加条件”** ，然后单击 **“类型”** 。 在下拉框中，选中 **“图像”** 复选框，按 Enter 键，然后单击“搜索”放大镜。  
  
    > [!NOTE]  
    >  对于“创建者”和“上次修改者”值，搜索用户的用户名，正如它在报表服务器上显示的那样   。  
  
### <a name="to-set-a-default-folder-for-report-parts"></a>为报表部件设置默认文件夹  
  
1.  单击 **“报表生成器”** ，然后单击 **“选项”** 。  
  
2.  在“选项”对话框的“设置”选项卡中，在“默认将报表部件发布到此文件夹”文本框中键入文件夹名称    。  
  
 如果此文件夹不存在且您具有在报表服务器上创建文件夹的权限，报表生成器将创建此文件夹。  
  
 不需要重新启动报表生成器，此设置就能生效。  
  
## <a name="see-also"></a>另请参阅  
 [检查更新或关闭更新 &#40;报表生成器和 SSRS&#41;](../check-for-updates-or-turn-updates-off-report-builder-and-ssrs.md)   
 [报表部件（报表生成器和 SSRS）](../report-parts-report-builder-and-ssrs.md)   
 [报表生成器中的报表部件和数据集](../report-data/report-parts-and-datasets-in-report-builder.md)   
 [&#40;报表生成器和 SSRS 的报表部件疑难解答&#41;](../troubleshoot-report-parts-report-builder-and-ssrs.md)   
 [发布和重新发布报表部件（报表生成器和 SSRS）](publish-and-republish-report-parts-report-builder-and-ssrs.md)  
  
  
