### openEuler SBOM 采取的标准
1. 我们采用ISO/IEC 5962:2021 [SPDX v2.2](https://spdx.github.io/spdx-spec/)的标准作为openEuler社区的SBOM标准的基础，同时增加对应用SPDX标准的具体若干要求，2者共同构成openEuler社区的SBOM标准。

### openEuler SBOM 应用SPDX的具体要求：
1. Document Creation Information 必选， 完全采用SPDX要求。
2. 每个开源组件（“广义的组件”，包括：Package, File, Snippet)都有一个ID字段（遵从SPDX）和以下7类基本字段，不同的组件的基本字段会有所区别, 基本字段以外的字段为可选字段：
   1.  Name类： 该组件的的名称。
   2.  Version类： 该组件对应的版本号。
   3.  Supplier类： 对于组件，可以是改组件的直接作者或所属的组织、机构、公司名。
   4.  Copyright类： 该组件的版权人信息，可能与Supplier重复。
   5.  PURL类： 该组件的源头发布地址，对于文件和片段，则是源头发布地址+PATH+(line-range).
   6.  Hash类： 该组件的checksum, 用于验证该组件的完整性。
   7.  License类： 该组件的License信息，表明该组件的授权情况。
3. Package Information
   * 必须存在一个root的Package元素用来描述软件本身。
   * 对于项目通过整包引用的Library, 或者通过包管理器引用的Library,可使用Package元素来描述。对于文件，片段引用的外部对象包，也可以用Library表述。
   * 基本字段：
      1. Name类： Field～ Package name field  Example~ PackageName: glibc
      2. Version类: Field~ Package version field  Example~ PackageVersion: 2.11.1
      3. Supplier类: Field~ Package supplier field  Example~ PackageSupplier: Person: Jane Doe (jane.doe@example.com)
      4. Copyright类：Field~ Copyright text field  Example~ PackageCopyrightText: <text>Copyright 2008-2010 John Smith</text>
      5. PURL类：Field~ Package download location field location  Example~ git+https://git.myproject.org/MyProject 补充～ 可以增加PURL类的表示方法
      6. Hash类: Field~ Package checksum field  Example~ PackageChecksum: MD5: 624c1abb3664f4b35547e7c73864ad24
      7. License类: Field~ Package checksum field  Example~ PackageLicenseDeclared: (LGPL-2.0-only AND LicenseRef-3)
4. File Information
   * 该部分为可选，建议只对从别的开源组件中引入的文件，提供File元素信息。
   * 基本字段
      1.  Name类： 
          1.  Field～ File name field  Example~ FileName: ./package/foo.c
          2.  Field~ Artifact of project name field Example~ ArtifactOfProjectName: Jena 2.0 补充～ 该字段用于表述文件的软件出处，已遗弃，更建议使用面向外部包的关系来描述。
      2.  Version类: 无 补充～可以在Artifact of project name field中提供版本。
      3.  Supplier类: 无 补充～可在外部包中描述
      4.  Copyright类：Field~ Copyright text field  Example~ FileCopyrightText: <text> Copyright 2008-2010 John Smith </text>
      5.  PURL类：Field~ Artifact of project uniform resource identifier field 补充～ 该字段已经遗弃，可以不填写该字段。
      6.  Hash类: Field~ File checksum field  Example~ FileChecksum: SHA1: d6a770ba38583ed4bb4525bd96e50461655d2758
      7.  License类: Field~ License information in file field  Example~ LicenseInfoInFile: GPL-2.0-only
5. Snippet SPDX identifier field
   * 该部分为可选，建议只对从别的开源组件中引入的片段，提供Snippet元素信息。
   * 基本字段
      1. Name类： 
         1. Field～ Snippet line range field  Example~ SnippetLineRange: 5:23
         2. 补充～ 更建议使用面向文件和外部包的关系来描述片段的出处。
      2. Version类: 无 
      3. Supplier类: 无
      4. Copyright类：Field~ Snippet copyright text field Example~ SnippetCopyrightText: <text> Copyright 2008-2010 John Smith </text>
      5. PURL类：无 
      6. Hash类: 无
      7. License类: Field~ License information in snippet field  Example~ LicenseInfoInSnippet: LicenseRef-2
6. Relationships between SPDX elements：
   * CONTAINS or CONTAINED_BY 用于片段/文件/library包含引用，DEPENDS_ON or DEPENDENCY_OF 用于包管理器依赖。
 

