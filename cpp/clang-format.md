# Preferred .clang-format

```txt

---  
Language: Cpp  
BasedOnStyle:  Microsoft  
AccessModifierOffset: -4  
AlignAfterOpenBracket: Align  
AlignConsecutiveMacros: false  
AlignConsecutiveAssignments: false  
AlignConsecutiveBitFields: false  
AlignConsecutiveDeclarations: false  
AlignEscapedNewlines: Left  
AlignOperands: Align  
AlignTrailingComments: true  
AllowAllArgumentsOnNextLine: true  
AllowAllConstructorInitializersOnNextLine: false  
AllowAllParametersOfDeclarationOnNextLine: false  
AllowShortBlocksOnASingleLine: Never  
AllowShortCaseLabelsOnASingleLine: false  
AllowShortEnumsOnASingleLine: false  
AllowShortFunctionsOnASingleLine: None  
AllowShortIfStatementsOnASingleLine: Never  
AllowShortLambdasOnASingleLine: All  
AllowShortLoopsOnASingleLine: false  
AlwaysBreakAfterDefinitionReturnType: None  
AlwaysBreakAfterReturnType: None  
AlwaysBreakBeforeMultilineStrings: false  
AlwaysBreakTemplateDeclarations: Yes  
BinPackArguments: false  
BinPackParameters: false  
BraceWrapping:  
  AfterCaseLabel:  true  
  AfterClass: true  
  AfterControlStatement: Always  
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
  IndentBraces: false  
  SplitEmptyFunction: true  
  SplitEmptyRecord: true  
  SplitEmptyNamespace: true  
BreakBeforeBinaryOperators: None  
BreakBeforeBraces: Custom  
BreakBeforeTernaryOperators: true  
BreakConstructorInitializers: BeforeComma  
BreakBeforeInheritanceComma: false  
BreakInheritanceList: BeforeComma  
BreakConstructorInitializersBeforeComma: false  
BreakAfterJavaFieldAnnotations: false  
BreakStringLiterals: false  
ColumnLimit: 100  
CommentPragmas: '^ IWYU pragma:'  
CompactNamespaces: false  
ConstructorInitializerAllOnOneLineOrOnePerLine: false  
ConstructorInitializerIndentWidth: 4  
ContinuationIndentWidth: 4  
Cpp11BracedListStyle: true  
DeriveLineEnding: true  
DerivePointerAlignment: false  
DisableFormat: false  
ExperimentalAutoDetectBinPacking: false  
FixNamespaceComments: false  
ForEachMacros:  
  - foreach  
  - Q_FOREACH  
  - BOOST_FOREACH  
IncludeBlocks:   Regroup  
IncludeCategories:  
  - Regex:           '^"(llvm|llvm-c|clang|clang-c)/'  
    Priority:        2  
    SortPriority:    0  
  - Regex:           '^(<|"(gtest|gmock|isl|json)/)'  
    Priority:        3  
    SortPriority:    0  
  - Regex:           '.*'  
    Priority:        1  
    SortPriority:    0  
IncludeIsMainRegex: '(Test)?$'  
IncludeIsMainSourceRegex: ''  
IndentCaseBlocks: true  
IndentCaseLabels: true  
IndentGotoLabels: true  
IndentPPDirectives: BeforeHash  
IndentExternBlock: NoIndent  
IndentWidth: 4  
IndentWrappedFunctionNames: false  
InsertTrailingCommas: None  
JavaScriptQuotes: Leave  
JavaScriptWrapImports: true  
KeepEmptyLinesAtTheStartOfBlocks: false  
MacroBlockBegin: ''  
MacroBlockEnd:   ''  
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
PointerAlignment: Middle  
ReflowComments: true  
SortIncludes: true  
SortUsingDeclarations: true  
SpaceAfterCStyleCast: true  
SpaceAfterLogicalNot: true  
SpaceAfterTemplateKeyword: true  
SpaceBeforeAssignmentOperators: true  
SpaceBeforeCpp11BracedList: true  
SpaceBeforeCtorInitializerColon: true  
SpaceBeforeInheritanceColon: true  
SpaceBeforeParens: Always  
SpaceBeforeRangeBasedForLoopColon: true  
SpaceInEmptyBlock: false  
SpaceInEmptyParentheses: false  
SpacesBeforeTrailingComments: 1  
SpacesInAngles: false  
SpacesInConditionalStatement: false  
SpacesInContainerLiterals: false  
SpacesInCStyleCastParentheses: false  
SpacesInParentheses: false  
SpacesInSquareBrackets: false  
SpaceBeforeSquareBrackets: true  
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
...


```

Save this file to a file named `.clang-format` in the root of your project. This has very similar style to the default JUCE project format

#cpp 