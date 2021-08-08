# zClang-Format

最近在考虑团队代码风格的问题，无意间发现了一个代码格式化神器“**clang-format**”工具

在了解clang-format工具之前，我们先来了解一下什么是clang，什么是LLVM，什么是gcc，什么又是GNU

## GNU

从百度百科上可以看到，GNU是一个类unix操作系统，其内容软件完全以GPL协议发布。全称GNU's Not Unix

## GCC

![gccegg-65](https://gitee.com/LucasXm/img/raw/master/img//gccegg-65.png)

GCC是一套基于GNU系统开发的编译器，目前支持编译 C, C++, Objective-C,Fortran, Ada, Go, D等多种语言

其详细信息可以查看  [GCC, the GNU Compiler Collection](https://www.gnu.org/software/gcc/)

## LLVM

LLVM最初由美国UIUC大学的chris Lattner博士主持开展，之后Apple雇了Chris Lattner，LLVM相当于也就成了Apple官方支持的编译器。

LLVM提供了编译器的相关支持，以C++编写而成，用于优化以任意程序语言编写的程序的编译时间、链接时间、运行时间、空闲时间。

其详情可以查看 [The LLVM Compiler Infrastructure](https://llvm.org/)

## clang

clang是一个由Apple主导编写的，以LLVM为后端的前端C、C++、Objective-C语言编译器，他具有如下优势

	*	编译速度快
	*	内存占用小
	*	兼容gcc

其详情可以查看 [Clang: a C language family frontend for LLVM][Clang C Language Family Frontend for LLVM](https://clang.llvm.org/)



## clang-format

上面了解了一些基础知识点，现在开始本篇的主要内容介绍，使用clang-format工具格式化代码。本位以VSCode为例，作为讲解。

1. 想要使用clang-format工具，我们需要一个名为“.clang-format”的配置文件，可以按照如下方法获取

   1. vscode安装C/C++扩展，扩展程序将自动安装clang-format

   2. 在vsc用户设置里面搜索clang，可以找到一个名为“C_Cpp: Clang_format_style”的选项，查看他的介绍，我们可以把代码格式化风格设置为如下几种

      * Visual Studio
      * LLVM
      * Google
      * Chromium
      * Mozilla
      * WebKit
      * file

   3. 如果将代码设置成file，那将从当前目录或父目录中的.clang-format文件来格式化代码

   4. 找到c/cc插件按照目录下的**clang-format.exe**工具，笔者的目录如下

      “C:\Users\\<User Name>\\.vscode\extensions\ms-vscode.cpptools-1.5.1\LLVM\bin”

   5. 打开命令行，输入.\clang-format.exe -style="llvm" -dump-config > .clang-format命令，即可获取到一个名为**.clang-format**的文件，把此文件放到工程代码的根目录下，即可生效。

      ![image-20210808144231050](https://gitee.com/LucasXm/img/raw/master/img//image-20210808144231050.png)

2. 如果需要定制自己代码格式化风格，可以按照 [Clang-Format Style Options](https://clang.llvm.org/docs/ClangFormatStyleOptions.html)文章修改.clang-format内容

3. 笔者的.clang-format配置如下

   ```yaml
   ---
   Language: Cpp
   # BasedOnStyle:  LLVM
   AccessModifierOffset: -2
   AlignAfterOpenBracket: Align
   AlignConsecutiveMacros: AcrossEmptyLines
   AlignConsecutiveAssignments: AcrossEmptyLines
   AlignConsecutiveBitFields: AcrossEmptyLines
   AlignConsecutiveDeclarations: AcrossEmptyLines
   AlignEscapedNewlines: Left
   AlignOperands: Align
   AlignTrailingComments: true
   AllowAllArgumentsOnNextLine: true
   AllowAllConstructorInitializersOnNextLine: true
   AllowAllParametersOfDeclarationOnNextLine: true
   AllowShortEnumsOnASingleLine: false
   
   AllowShortBlocksOnASingleLine: false
   AllowShortCaseLabelsOnASingleLine: false
   AllowShortFunctionsOnASingleLine: false
   
   AllowShortLambdasOnASingleLine: All
   AllowShortIfStatementsOnASingleLine: false
   AllowShortLoopsOnASingleLine: false
   AlwaysBreakAfterDefinitionReturnType: None
   AlwaysBreakAfterReturnType: None
   AlwaysBreakBeforeMultilineStrings: false
   AlwaysBreakTemplateDeclarations: MultiLine
   AttributeMacros:
       - __capability
   BinPackArguments: false
   BinPackParameters: false
   
   BraceWrapping:
       AfterCaseLabel: true
       AfterClass: true
       AfterControlStatement: true
       AfterEnum: true
       AfterFunction: true
       AfterNamespace: true
       AfterObjCDeclaration: true
       AfterStruct: true
       AfterUnion: true
       AfterExternBlock: true
       BeforeCatch: true
       BeforeElse: true
       BeforeLambdaBody: true
       BeforeWhile: true
       IndentBraces: true
       SplitEmptyFunction: true
       SplitEmptyRecord: true
       SplitEmptyNamespace: true
   BreakBeforeBinaryOperators: None
   BreakBeforeConceptDeclarations: true
   BreakBeforeBraces: Allman
   BreakBeforeInheritanceComma: true
   BreakInheritanceList: BeforeColon
   BreakBeforeTernaryOperators: true
   BreakConstructorInitializersBeforeComma: false
   BreakConstructorInitializers: BeforeColon
   BreakAfterJavaFieldAnnotations: false
   BreakStringLiterals: false
   ColumnLimit: 80
   CommentPragmas: "^ IWYU pragma:"
   CompactNamespaces: false
   ConstructorInitializerAllOnOneLineOrOnePerLine: false
   ConstructorInitializerIndentWidth: 4
   ContinuationIndentWidth: 4
   Cpp11BracedListStyle: true
   DeriveLineEnding: true
   DerivePointerAlignment: false
   DisableFormat: false
   EmptyLineBeforeAccessModifier: LogicalBlock
   ExperimentalAutoDetectBinPacking: false
   FixNamespaceComments: true
   ForEachMacros:
       - foreach
       - Q_FOREACH
       - BOOST_FOREACH
   StatementAttributeLikeMacros:
       - Q_EMIT
   IncludeBlocks: Preserve
   IncludeCategories:
       - Regex: '^"(llvm|llvm-c|clang|clang-c)/'
         Priority: 2
         SortPriority: 0
         CaseSensitive: false
       - Regex: '^(<|"(gtest|gmock|isl|json)/)'
         Priority: 3
         SortPriority: 0
         CaseSensitive: false
       - Regex: ".*"
         Priority: 1
         SortPriority: 0
         CaseSensitive: false
   IncludeIsMainRegex: "(Test)?$"
   IncludeIsMainSourceRegex: ""
   IndentCaseLabels: false
   IndentCaseBlocks: false
   IndentGotoLabels: true
   IndentPPDirectives: BeforeHash
   IndentExternBlock: AfterExternBlock
   IndentRequires: false
   IndentWidth: 2
   IndentWrappedFunctionNames: false
   InsertTrailingCommas: None
   JavaScriptQuotes: Leave
   JavaScriptWrapImports: true
   KeepEmptyLinesAtTheStartOfBlocks: false
   MacroBlockBegin: ""
   MacroBlockEnd: ""
   MaxEmptyLinesToKeep: 1
   NamespaceIndentation: None
   ObjCBinPackProtocolList: Auto
   ObjCBlockIndentWidth: 2
   ObjCBreakBeforeNestedBlockParam: true
   ObjCSpaceAfterProperty: false
   ObjCSpaceBeforeProtocolList: true
   PenaltyBreakAssignment: 2
   PenaltyBreakBeforeFirstCallParameter: 19
   PenaltyBreakComment: 300
   PenaltyBreakFirstLessLess: 120
   PenaltyBreakString: 1000
   PenaltyBreakTemplateDeclaration: 10
   PenaltyExcessCharacter: 1000000
   PenaltyReturnTypeOnItsOwnLine: 60
   PenaltyIndentedWhitespace: 0
   PointerAlignment: Right
   ReflowComments: true
   SortIncludes: false
   SortJavaStaticImport: Before
   SortUsingDeclarations: false
   SpaceAfterCStyleCast: false
   SpaceAfterLogicalNot: false
   SpaceAfterTemplateKeyword: true
   SpaceBeforeAssignmentOperators: true
   SpaceBeforeCaseColon: false
   SpaceBeforeCpp11BracedList: true
   SpaceBeforeCtorInitializerColon: true
   SpaceBeforeInheritanceColon: true
   SpaceBeforeParens: ControlStatements
   SpaceAroundPointerQualifiers: Default
   SpaceBeforeRangeBasedForLoopColon: true
   SpaceInEmptyBlock: false
   SpaceInEmptyParentheses: false
   SpacesBeforeTrailingComments: 1
   SpacesInAngles: false
   SpacesInConditionalStatement: false
   SpacesInContainerLiterals: true
   SpacesInCStyleCastParentheses: false
   SpacesInParentheses: false
   SpacesInSquareBrackets: false
   SpaceBeforeSquareBrackets: false
   BitFieldColonSpacing: Both
   Standard: Latest
   StatementMacros:
       - Q_UNUSED
       - QT_REQUIRE_VERSION
   TabWidth: 4
   UseCRLF: false
   UseTab: Never
   WhitespaceSensitiveMacros:
       - STRINGIZE
       - PP_STRINGIZE
       - BOOST_PP_STRINGIZE
       - NS_SWIFT_NAME
       - CF_SWIFT_NAME
   ---
   ```





> **笔者留言：**
>
> ​	笔者正在嵌入式学习路上摸爬滚打 :muscle:
>
> ​	对于一些知识点的理解难免会有出入，还请读者不吝赐教 :raised_hand:
>
> ​	[github地址](https://github.com/lucas-zgp?tab=repositories) :pray:
>
> ​	**扫码关注微信公众号** :pray:
>
> ![image-20210808145651937](https://gitee.com/LucasXm/img/raw/master/img//image-20210808145651937.png)

