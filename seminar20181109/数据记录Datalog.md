Datalog是一种声明性逻辑编程语言，在语法上是Prolog的子集。它经常被用来作为一个查询语言的演绎数据库。近年来，Datalog在数据集成，信息提取，网络，程序分析，安全性和云计算方面找到了新的应用。
它的起源可以追溯到逻辑编程的开始，但是在1977年HervéGallaire和Jack Minker组织了一个关于逻辑和数据库的研讨会时，它成为一个独立的区域。[2] David Maier因创造Datalog一词而受到赞誉。[3]
## 功能，限制和扩展
与Prolog不同，Datalog程序的陈述可以按任何顺序陈述。此外，[有限集](https://en.wikipedia.org/wiki/Finite_sets)上的Datalog查询保证[终止](https://en.wikipedia.org/wiki/Algorithm#Termination)，因此Datalog没有Prolog的[cut](https://en.wikipedia.org/wiki/Cut_(logic_programming))操作符。这使得Datalog成为一种完全[声明性的语言](https://en.wikipedia.org/wiki/Declarative_language)。
与Prolog，Datalog相反
1. 不允许复杂的术语作为[谓词的](https://en.wikipedia.org/wiki/Predicate_(logic))参数，例如，p（1,2）是可接受的但不是p（f（1），2），
2. 对使用否定和[递归](https://en.wikipedia.org/wiki/Recursion)施加某些[分层](https://en.wikipedia.org/wiki/Stratification_(mathematics))限制，
3. 要求出现在[子句](https://en.wikipedia.org/wiki/Clause_(logic))头部的每个变量也出现在[子句](https://en.wikipedia.org/wiki/Clause_(logic))主体中的非算术正（即未否定）[字面](https://en.wikipedia.org/wiki/Literal_(mathematical_logic))中，
4. 要求出现在条款正文中的负面文字中的每个变量也出现在条款正文中的某些正文字中[[4]](https://en.wikipedia.org/wiki/Datalog#cite_note-4)

与数据记录查询评估是基于[一阶逻辑](https://en.wikipedia.org/wiki/First-order_logic)，并且因此[声音](https://en.wikipedia.org/wiki/Soundness)和[完整](https://en.wikipedia.org/wiki/Completeness_(logic))。但是，Datalog不是[Turing完整的](https://en.wikipedia.org/wiki/Turing_completeness)，因此可以用作[特定](https://en.wikipedia.org/wiki/Domain-specific_language)于[域的语言](https://en.wikipedia.org/wiki/Domain-specific_language)，可以利用为查询解析开发的高效算法。实际上，已经提出了各种方法来有效地执行查询，例如，魔术集算法，[[5]](https://en.wikipedia.org/wiki/Datalog#cite_note-5)表格逻辑编程[[6]](https://en.wikipedia.org/wiki/Datalog#cite_note-6)或SLG分辨率。[[7]](https://en.wikipedia.org/wiki/Datalog#cite_note-7)
一些广泛使用的数据库系统包括为Datalog开发的想法和算法。例如，[SQL：1999](https://en.wikipedia.org/wiki/SQL:1999)标准包括[递归查询](https://en.wikipedia.org/wiki/Hierarchical_and_recursive_queries_in_SQL)，而Magic Sets算法（最初为更快地评估Datalog查询而开发）是在IBM的[DB2中](https://en.wikipedia.org/wiki/IBM_DB2)实现的。[[8]](https://en.wikipedia.org/wiki/Datalog#cite_note-8)此外，Datalog引擎支持专门的[数据库系统，](https://en.wikipedia.org/wiki/Database_system)例如Intellidimension的[语义网](https://en.wikipedia.org/wiki/Semantic_web)数据库。[ [引证需要](https://en.wikipedia.org/wiki/Wikipedia:Citation_needed) ]
已对Datalog进行了若干扩展，例如，支持[聚合函数](https://en.wikipedia.org/wiki/Aggregate_function)，允许[面向对象的编程](https://en.wikipedia.org/wiki/Object-oriented_programming)，或允许作为[子句的](https://en.wikipedia.org/wiki/Clause_(logic))头部的[析取](https://en.wikipedia.org/wiki/Disjunction)。这些扩展对Datalog的语义定义和相应的Datalog解释器的实现有重大影响。
## 示例
这两行定义了两个*事实*，即总是持有的东西：
```
parent(bill, mary).
parent(mary, john).
```
这是他们的意思：*法案是玛丽的父母*和*玛丽是约翰的父母*。名称以小写字母书写，因为大写字母代表变量。
这两行定义了*规则*，这些*规则*定义了如何从已知事实推断出新事实。
```
ancestor(X, Y) :- parent(X, Y).
ancestor(X, Y) :- parent(X, Z), ancestor(Z, Y).
```
* *如果X是Y的父亲，则X是Y的祖先。*
* *如果X是某个Z的父亲，则X是Y的祖先，Z是Y的祖先。*

这一行是一个查询：
```
?- ancestor(bill, X).
```
它询问以下内容：*该法案的祖先是X的全部是谁？*当针对包含上述事实和规则的Datalog系统提出时，它将返回*玛丽*和*约翰*。
关于规则的更多信息：规则有*： -*中间的符号：此符号左侧的部分是规则的*头部*，右侧的部分是*主体*。规则如下所示：*如果已知<body>为真，则<head>已知为真*。规则中的大写字母代表变量：在示例中，我们不知道*X*或*Y*是谁，但是如果*X*是*Y*的父，则某些*X*是某些*Y*的祖先。子句的排序在Datalog中是无关紧要的，而Prolog则依赖于计算查询调用结果的子句的顺序。
Datalog区分*Extensional谓词符号*（由事实定义）和*内涵谓词符号*（由规则定义）。[[9]](https://en.wikipedia.org/wiki/Datalog#cite_note-9)在上面的例子中ancestor是一个内涵谓词符号，并且parent是伸展的。谓词也可以由事实和规则定义，因此既不是纯粹的扩展也不是内涵，但任何Datalog程序都可以重写为等效程序，而不具有重复角色的谓词符号。
## 实现数据记录的系统[ [编辑](https://en.wikipedia.org/w/index.php?title=Datalog&action=edit&section=3)]
以下是基于Datalog或提供Datalog解释器的系统的简短列表：
### 免费软件/开源[ [编辑](https://en.wikipedia.org/w/index.php?title=Datalog&action=edit&section=4)]
| **写在**   | **名称**   | **在线尝试**   | **外部数据库**   | **描述**   | **执照**   | 
|:----:|:----:|:----|:----|:----|:----:|
| **在**[Java中](https://en.wikipedia.org/wiki/Java_(programming_language))   | IRIS [[10]](https://en.wikipedia.org/wiki/Datalog#cite_note-10)   |    |    | IRIS使用函数符号，内置谓词，局部分层或非分层逻辑程序（使用有根据的语义），不安全规则和XML模式数据类型扩展Datalog   | [GNU LGPL](https://en.wikipedia.org/wiki/GNU_Lesser_General_Public_License) v2.1   | 
|    | [耶拿](https://en.wikipedia.org/wiki/Jena_(framework))   |    |    | 一个语义Web框架，它包含一个Datalog实现，作为其通用规则引擎的一部分，提供[OWL](https://en.wikipedia.org/wiki/Web_Ontology_Language)和[RDFS](https://en.wikipedia.org/wiki/RDFS)支持。[[11]](https://en.wikipedia.org/wiki/Datalog#cite_note-11)   | Apache v2   | 
|    | SociaLite [[12]](https://en.wikipedia.org/wiki/Datalog#cite_note-12)   |    |    | SociaLite是斯坦福大学开发的大规模图形分析的数据记录变体   | Apache v2   | 
|    | 格拉尔[[13]](https://en.wikipedia.org/wiki/Datalog#cite_note-13)   |    |    | Graal是一个Java工具包，专门用于在存在规则框架内查询知识库，即Datalog +/-。   | CeCILL v2.1   | 
|    | Flix [[14]](https://en.wikipedia.org/wiki/Datalog#cite_note-14)   | 是的[[15]](https://en.wikipedia.org/wiki/Datalog#cite_note-15)   |    | 一种功能和逻辑编程语言，受Datalog的启发，扩展了用户定义的格子和单调滤波器/传递函数。   | Apache v2   | 
| **在**[C.](https://en.wikipedia.org/wiki/C_(programming_language))   | [XSB](https://en.wikipedia.org/wiki/XSB)   |    |    | 用于[Unix](https://en.wikipedia.org/wiki/POSIX)和[MS Windows](https://en.wikipedia.org/wiki/MS_Windows)的逻辑编程和演绎数据库系统，具有表格，提供类似Datalog的终止和效率，包括增量评估[[16]](https://en.wikipedia.org/wiki/Datalog#cite_note-16)   | [GNU LGPL](https://en.wikipedia.org/wiki/GNU_Lesser_General_Public_License)   | 
| **在**[C ++中](https://en.wikipedia.org/wiki/C%2B%2B)   | 珊瑚[[17]](https://en.wikipedia.org/wiki/Datalog#cite_note-17)   |    |    | 用C ++编写的演绎数据库系统，具有半天真的数据记录评估。发展于1988 - 1997年。   | 自定义许可证，免费用于非商业用途   | 
|    | Inter4QL [[18]](https://en.wikipedia.org/wiki/Datalog#cite_note-18)   |    |    | 用于Windows，Mac OS X和Linux的C ++实现的类似数据目录的4QL查询语言的开源命令行解释器。规则的头部和主体以及递归都允许否定   | [GNU GPL](https://en.wikipedia.org/wiki/GNU_General_Public_License) v3   | 
|    | RDFox [[19]](https://en.wikipedia.org/wiki/Datalog#cite_note-19)   |    |    | 带有Datalog推理的RDF三重存储。实现FBF算法以进行增量评估。   | 自定义许可证，免费用于非商业用途[[20]](https://en.wikipedia.org/wiki/Datalog#cite_note-20)   | 
|    | 蛋奶酥[[21]](https://en.wikipedia.org/wiki/Datalog#cite_note-21)   |    |    | 一个开源的Datalog-to-C ++编译器，将Datalog转换为高性能的并行C ++代码，专门用于大型数据集上的复杂Datalog查询，例如在静态程序分析的上下文中遇到的   | UPL v1.0   | 
| **在**[Python中](https://en.wikipedia.org/wiki/Python_(programming_language))   | [pyDatalog](https://sites.google.com/site/pydatalog/)   |    | 11种方言的SQL   | 将逻辑编程添加到Python的工具箱中。它可以对数据库或Python对象运行逻辑查询，并使用逻辑子句来定义Python类的行为。   | [GNU LGPL](https://en.wikipedia.org/wiki/GNU_Lesser_General_Public_License)   | 
| **在**[Ruby中](https://en.wikipedia.org/wiki/Ruby_(programming_language))   | [绽放](http://bloom-lang.net/index.html) /萌芽   |    |    | 用于使用以数据为中心的构造进行编程的Ruby [DSL](https://en.wikipedia.org/wiki/Domain-specific_language)，基于Datalog 的[Dedalus](https://www2.eecs.berkeley.edu/Pubs/TechRpts/2009/EECS-2009-173.html)扩展，为逻辑增加了时间维度。   | [BSD](https://en.wikipedia.org/wiki/BSD_licenses) 3条款   | 
| **在**[Lua](https://en.wikipedia.org/wiki/Lua_(programming_language))   | 数据记录[[22]](https://en.wikipedia.org/wiki/Datalog#cite_note-22)   | 是的[[23]](https://en.wikipedia.org/wiki/Datalog#cite_note-23)   |    | 轻量级演绎数据库系统。   | [GNU LGPL](https://en.wikipedia.org/wiki/GNU_Lesser_General_Public_License)   | 
| **在**[Prolog](https://en.wikipedia.org/wiki/Prolog)   | [DES ](http://des.sourceforge.net/)[[24]](https://en.wikipedia.org/wiki/Datalog#cite_note-24)   |    |    | 一个开源实现，用于在课程中教授Datalog   | [GNU LGPL](https://en.wikipedia.org/wiki/GNU_Lesser_General_Public_License)   | 
| **在**[Clojure](https://en.wikipedia.org/wiki/Clojure)   | [Cascalog](http://cascalog.org/)   |    | [Hadoop的](https://en.wikipedia.org/wiki/Hadoop)   | 用于查询存储在Hadoop集群上的数据的Clojure库   | 阿帕奇   | 
|    | [Clojure Datalog](http://code.google.com/p/clojure-contrib/wiki/DatalogOverview)   |    |    | 实现Datalog方面的贡献库   | Eclipse Public License 1.0   | 
|    | [Datascript](https://github.com/tonsky/datascript)   |    | 在记忆中   | 在浏览器中运行的不可变数据库和Datalog查询引擎   | Eclipse Public License 1.0   | 
| **在**[Racket](https://en.wikipedia.org/wiki/Racket_(programming_language))   | 球拍数据记录[[25]](https://en.wikipedia.org/wiki/Datalog#cite_note-25)   |    |    |    | [GNU LGPL](https://en.wikipedia.org/wiki/GNU_Lesser_General_Public_License)   | 
|    | Datafun [[26]](https://en.wikipedia.org/wiki/Datalog#cite_note-26)   |    |    | 半格的广义数据记录   | [GNU LGPL](https://en.wikipedia.org/wiki/GNU_Lesser_General_Public_License)   | 
| **在**[Tcl](https://en.wikipedia.org/wiki/Tcl)   | [tclbdd ](https://chiselapp.com/user/kbk/repository/tclbdd/)[[27]](https://en.wikipedia.org/wiki/Datalog#cite_note-27)   |    |    | 基于[二元决策图的实现](https://en.wikipedia.org/wiki/Binary_decision_diagram)。旨在支持为Tcl开发优化编译器。   | BSD   | 
| **在**[哈斯克尔](https://en.wikipedia.org/wiki/Haskell_(programming_language))   | Dyna [[28]](https://en.wikipedia.org/wiki/Datalog#cite_note-28)   |    |    | Dyna是用于统计AI编程的声明性编程语言。该语言基于Datalog，支持前向和后向链接以及增量评估。   | GNU AGPL v3   | 
| **在其他或未知的语言**   | bddbddb[[29]](https://en.wikipedia.org/wiki/Datalog#cite_note-29)   |    |    | 在[斯坦福大学](https://en.wikipedia.org/wiki/Stanford_University)完成的Datalog实现。它主要用于查询Java字节码，包括对大型Java程序的点分析   | [GNU LGPL](https://en.wikipedia.org/wiki/GNU_Lesser_General_Public_License)   | 
|    | ConceptBase[[30]](https://en.wikipedia.org/wiki/Datalog#cite_note-30)   |    |    | 基于Datalog查询评估器的演绎和面向对象的数据库系统：用于触发程序和重写的Prolog，用于（元）建模的公理化Datalog，称为“Telos”。它主要用于概念建模和元模型   | [BSD](https://en.wikipedia.org/wiki/BSD_licenses)（FreeBSD风格许可证）Prolog，Java，C ++。   | 
|    | 

### 非自由软件[ [编辑](https://en.wikipedia.org/w/index.php?title=Datalog&action=edit&section=5)]
* [Datomic](https://en.wikipedia.org/wiki/Datomic)是一个分布式数据库，旨在实现在新的云架构上运行的可扩展，灵活和智能的应用程序。它使用Datalog作为查询语言。
* [DLV](https://en.wikipedia.org/wiki/DLV)是商业Datalog扩展，支持析取头条款。
* [FoundationDB](https://en.wikipedia.org/wiki/FoundationDB)为pyDatalog提供了免费的数据库绑定，并附有使用它的教程。[[31]](https://en.wikipedia.org/wiki/Datalog#cite_note-31)
* [Leapsight语义数据空间](https://en.wikipedia.org/w/index.php?title=Leapsight_Semantic_Dataspace&action=edit&redlink=1)（LSD）是一种分布式演绎数据库，提供高可用性，容错性，操作简单性和可伸缩性。LSD使用Leaplog（Datalog实现）进行查询和推理，由Leapsight创建。[[32]](https://en.wikipedia.org/wiki/Datalog#cite_note-32)
* [LogicBlox](https://en.wikipedia.org/w/index.php?title=LogicBlox&action=edit&redlink=1)，Datalog的商业实现，用于基于Web的零售计划和保险应用程序。
* [Profium](https://en.wikipedia.org/wiki/Profium) Sense是一个用Java编写的原生RDF兼容[图形数据库](https://en.wikipedia.org/wiki/Graph_database)。它为用户定义的规则提供Datalog评估支持。
* [.QL](https://en.wikipedia.org/wiki/.QL)，由Semmle创建的Datalog的商业面向对象变体。[[33]](https://en.wikipedia.org/wiki/Datalog#cite_note-33)
* [SecPAL](https://en.wikipedia.org/wiki/SecPAL)是[Microsoft Research](https://en.wikipedia.org/wiki/Microsoft_Research)开发的一种安全策略语言。[[34]](https://en.wikipedia.org/wiki/Datalog#cite_note-34)
* [Stardog](https://en.wikipedia.org/w/index.php?title=Stardog&action=edit&redlink=1)是一个用[Java](https://en.wikipedia.org/wiki/Java_(programming_language))实现的[图形数据库](https://en.wikipedia.org/wiki/Graph_database)。它为[RDF](https://en.wikipedia.org/wiki/Resource_Description_Framework)和所有[OWL 2](https://en.wikipedia.org/wiki/OWL_2)配置文件提供支持，提供广泛的推理功能，包括数据记录评估。
* StrixDB：商业RDF图形存储，符合[Lua](https://en.wikipedia.org/wiki/Lua_(programming_language)) API和Datalog推理功能的[SPARQL](https://en.wikipedia.org/wiki/SPARQL)。可以用作httpd（[Apache HTTP Server](https://en.wikipedia.org/wiki/Apache_HTTP_Server)）模块或独立版（虽然beta版本属于Perl Artistic License 2.0）。
## 另见[ [编辑](https://en.wikipedia.org/w/index.php?title=Datalog&action=edit&section=6)]
* [答案集编程](https://en.wikipedia.org/wiki/Answer_set_programming)
* [SWRL](https://en.wikipedia.org/wiki/Semantic_Web_Rule_Language)
* [D（数据语言规范）](https://en.wikipedia.org/wiki/D_(data_language_specification))
* [D4（编程语言）](https://en.wikipedia.org/wiki/D4_(programming_language))
* [联合查询](https://en.wikipedia.org/wiki/Conjunctive_query)

