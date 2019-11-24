# doxygen配置语法说明

**DOXYFILE_ENCODING**
指定文件中所有字符的编码格式。在此标记出现之前默认使用UTF-8。Doxygen 可以使用libiconv(或在libc中创建iconv)实现编码转换。查阅http://www.gnu.org/software/libiconv 中列出的编码格式。

**PROJECT_NAME**
此标记是一个单词(或者使用双引号可包含一个字串),用于标识生成的文档项目,这个名称可用于大多数生成页面的标题或某些地方。

**PROJECT_NUMBER**
此标记能用于记录一个项目或是修订版本号,能非常容易地将生成的文档进行归类,或是被一些版本控制系统所使用。

**OUTPUT_DIRECTORY**
指定一个(相对或绝对)的路径,用于生成文档的写入点。如果是一个相对路径,它将会关联到启动doxygen的位置。如果留空则表示当前目录将被使用

**CREATE_SUBDIRS**
如果此标记设定为YES,在每种输出格式的输出目录下,doxygen 将创建4096个子目录(主输出目录的下2 层中),并分发生成文件到这些目录中。当提供了一个数量巨大的源码文件集给doxygen 时,如果将所有的生成文件都放置到同一目录下,这将导致文件系统的性能问题,而此时有效CREATE_SUBDIRS 选项将非常有益处。

**OUTPUT_LANGUAGE**
用于指定所有生成文档的语言,doxygen 将使用此信息,生成指定语言的所有常规输出。默认语言是英语,其他支持的语言有:南非荷兰语,阿拉伯语,巴西语,加泰罗尼亚语,汉语,克罗地亚语,捷克语,丹麦语,荷兰语,芬兰语,法语,德语,希腊语,匈牙利语,意大利语,日语,韩语,立陶宛语,挪威语,波斯语,波兰语,葡萄牙语,罗马尼亚语,俄语,塞尔维亚语,斯洛伐克语,斯洛文尼亚语,西班牙语,瑞典语,乌克兰语。

**BRIEF_MEMBER_DESC**
假如此标记设为YES(默认值),doxygen 将在文件和类文档(类似于JavaDoc)中列出的成员之后加入简明的成员描述,若设为NO则无效。

**REPEAT_BRIEF**

如果此标记设为YES(默认值),doxygen 将会在详细描述之前加入一个成员或函数的简明描述。
注意,若HIDE_UNDOC_MEMBERS和 BRIEF_MEMBER_DESC 都设为NO,简明描述将被完全隐藏。

**ABBREVIATE_BRIEF**
这个标记采用了一种仿智能的简明描述的缩写工具,用于多个列表中的文本。在列表的每个字串中,如果查找到简明描述的首位字符,会在整个列表处理之后的结果和文本中剔除,可看成为附加说明的文本。否则将维持原状。
如果标记之后留空,下面的值将被使用(“\$name”自动替换某些实体的名称):$name 类,$name 部件,以及$name文件。If left blank, the following values are used (“\$name” is automatically replaced with the name
of the entity): “The $name class” “The $name widget” “The $name file” “is” “provides” “specifies”“contains” “represents” “a” “an” “the”.

**ALWAYS_DETAILED_SEC**
如果ALWAYS_DETAILED_SEC 和 REPEAT_BRIEF 都设为YES,在只有一个简明描述的地方doxygen 将生成一个详细的小节。

**INLINE_INHERITED_MEMB**
若设为YES,doxygen 将在类文档中显示类的所有派生成员。并假定这些成员均为普通类成员。基类的构造器,析构器以及赋值操作符将不会显示。

**FULL_PATH_NAMES**
若设为YES,doxygen 将在文件列表和头文件中的文件名之前加入完整路径。若设为NO,将使用能保证文件名唯一性的最短路径。

**STRIP_FROM_PATH**
若FULL_PATH_NAMES 设为YES,STRIP_FROM_PATH 用于去除路径中用户自定义的部分,且只会去除与路径左起匹配的多个指定字串,此标记能够显示文件列表中相关的路径,假如标记后留白此标记无效。

**STRIP_FROM_INC_PATH**
从类文档内所涉及的路径中,去除用户自定义的部分,它将告知阅读者一个类将包含那些头文件。假如标记后留白,只会使用类定义中的头文件名。否则将会在正常编译时使用-I 参数指定,此标记之后的包含路径。

**CASE_SENSE_NAMES**
若设为NO,doxygen 将只生成小写字母的文件名,若设为YES,允许使用大写字母。如果你的类或文件名之间存在同名但有大小写的差异,以及你的文件系统支持大小写敏感的文件名,那么这个标记是非常有用的。Windows用户可设为NO忽略它。

**SHORT_NAMES**
若设为YES,doxygen 将生成最短(但可读)的文件名。当你的文件系统不支持长文件名,如DOS,Mac,CD-ROM时,这个标记是非常有用的。

**JAVADOC_AUTOBRIEF**
若设为YES,doxygen将会使用一个JavaDoc 风格的注释,作为简明描述来表述第一行(直到第一行结束)。若设为NO(默认值),JavaDoc 风格看上去更象是一个标准的Qt注释(这里需要一个@brief命令来生成一个简明描述)。QT_AUTOBRIEF
若设为YES,doxygen 将会使用一个Qt 风格的注释,作为简明描述来表述第一行(直到第一行结束)。若设为NO(默认值),Qt风格看上去更象是一个标准的Qt注释(这里需要一个\brief命令来生成一个简明描述)。

**BUILTIN_STL_SUPPORT**
如果你使用了STL 类(如std::string,std::vector 等等),但又不希望包含(在一个标记中)STL 库,那么可将此标记设为YES,使得doxygen能够匹配包含STL 类的函数声明和定义(例如func(std::string)等同于
func(std::string) {}),这也使得继承和协作图中,涉及到STL类的部分更加完整和准确。

**CPP_CLI_SUPPORT**
假如你使用了微软的C++/CLI 语言,可设为YES 使能解析支持。

**SIP_SUPPORT**
如果你的项目中只包含SIP 源码可设为YES,doxygen 解析时会将其看成一般的C++代码,但是当protection 关键字没有出现时,会假定所有的类都使用了公有继承而不是私有继承。
** SIP 是一个自动生成C/C++库的Python 绑定端的工具,原本是为了PyQt(Qt GUI 工具包的绑定端)而开发的,时间始于1998年。但它更适合生成任意C/C++库的绑定端。参考页面:
http://www.riverbankcomputing.co.uk/static/Docs/sip4/introduction.html

**IDL_PROPERTY_SUPPORT**
微软IDL 的获取和设定特性,用于表示一个属性获取和设定的方法。设置这个选项为YES(默认),使得doxygen在文档中覆盖掉属性的获取和设定方法,这只能工作在这些方法获取和设定简单类型时。如果不是这种情况,而总是希望显示这些方法,那么将此选项设为NO。

**DISTRIBUTE_GROUP_DOC**
如果在文档中使用了成员组,以及此选项设为YES,为了组中的其他成员,doxygen 将会重复使用用文档中组第一个成员(如果有),then doxygen will reuse the documentation of the first member in the group (if
any) for the other members of the group组默认情况下,所有的组成员必须被显示文档化MULTILINE

**MULTILINE_CPP_IS_BRIEF**
若设为YES,doxygen 需要处理一个多行的C++特殊注释块(如,//!或///的注释块),类似于一个简明描述。这是一个默认状态。最新修订后的默认状态则是将上述的特殊注释块看作一个细节描述。如果你接受修改后的默认状态,可将此标记设为YES,注意,此标记设为YES,也就意味着rational rose的注释无法被完全辨别。

**INHERIT_DOCS**
若设为YES(默认值),那么一个未文档化成员继承于其他文档化成员,它将重新执行文档化。If the INHERIT_DOCStag is set to YES (the default) then an undocumented member inherits the documentation from any documented member that it re-implements

**SEPARATE_MEMBER_PAGES**
若设为YES,doxygen 将为每一个成员建立一个新页,若设为NO,成员文档将成为文件/类/名字空间文档中的一部分。

**TAB_SIZE**
设置制表符的大小,doxygen 使用这个数值替换掉代码段中的空格数。

**ALIASES**
在文档中用于指定一定数量的alias,等同于命令。一个alias 有以下的格式,
name=value
这里增加一个例子:
“sideeffect=\par Side Effects:\n”
它允许你放置\sideeffect(或@sideeffect)命令在文档中,这将导致在用户定义的段落标题为“Side Effects:”,你可放置\Side Effects:插入换行符。You can put \n’s in the value part of an alias to insert newlines.

**OPTIMIZE_OUTPUT_FOR_C**
若设为YES,如果你的项目中只包含C 源码,doxygen 将为C 生成更适合的输出,比如,使用一些不同的名称,忽略所有成员的列表,等等。

**OPTIMIZE_OUTPUT_JAVA**
若设为YES,如果你的项目中只包含Java 或Python 的源码,doxygen 将为这些语言生成更适合的输出,比如出现的名字空间将被看做包,获取认证的范围将会有差异,等等。

**OPTIMIZE_FOR_FORTRAN**
若设为YES,如果你的项目中只包含Fortran的源码,doxygen 将为它生成更适合的输出。

**OPTIMIZE_OUTPUT_VHDL**
若设为YES,如果你的项目中只包含VHDL 的源码,doxygen 将为它生成更适合的输出。

E**XTENSION_MAPPING**
Doxygen 使用它能够解析的文件扩展名,来选择解析器, 此标记能为解析器分配一个给定的扩展名,doxygen 有一个内建的映射,但你可以使用此标记覆盖或扩展它。格式为ext=language,ext 即文件的扩展名,language则为doxygen 所支持的解析器中的一个:IDL, Java, Javascript, C#, C, C++, D, PHP, Objective-C, Python,Fortran, VHDL, C, C++。比如使得doxygen 将.inc看做Fortran 文件(默认为PHP文件),.f 看做C文件(默认为Fortran文件),可以使用:inc=Fortran,f=C。

**SUBGROUPING**
若设为YES(默认),允许相同类型的类成员组(比如一个公有函数组)被放置到此类型的子分组中(如在Public Functions小节下),设为NO 禁用子分组。另外,对每个类使用\nosubgrouping 命令同样可禁用子分组。

**TYPEDEF_HIDES_STRUCT**
若设为YES,文档化的结构,联合或枚举的类型定义,将被看做它们类型的名称。如typedef struct TypeS {} TypeT,那么文档中就存在一个名为TypeT 的结构,当无效这个类型定义时,它有可能是文件,名字空间或类的成员,这个结构将被命令为TypeS,这对于C 代码是非常有价值的,可在编码约定中指定所有的混合类型的定义,以只对此类型定义进行引用,而不需要标记名称。

与创建有关的选项
**EXTRACT_ALL**
若设为YES, doxygen 会假定文档中的所有主体将被文档化,即使在未提供文档的情况下。私有类成员和文件静态成员将隐藏,直到EXTRACT_PRIVATE 和EXTRACT_STATIC 标记设为YES。

注意:
当WARNINGS 设为YES 时,将无效生成过程中未文档化成员发出的警告。

**EXTRACT_PRIVATE**
若设为YES,在文档中将包含所有类私有成员。

**EXTRACT_STATIC**
若设为YES,在文档中将包含所有文件的静态成员

**EXTRACT_LOCAL_CLASSES**
若设为YES,在文档中将包含在源文件中定义的类(和结构),若设为NO,只包含在头文件中定义的类。对于Java
源码无任何影响。

**EXTRACT_ANON_NSPACES**
若设为YES,匿名空间的成员将被提取到文档中,并被称为anonymous_namespace{file}的名字空间,file 可使用匿名空间包含的文件基类名进行替换。默认情况下,匿名空间将被隐藏。

**EXTRACT_LOCAL_METHODS**
这个标记只对Object-C 代码有效,当设为YES 时,在文档中包含的局部方法将在执行部分被定义,而不会在接
口中。若设为NO(默认),只有在接口中的方法才会被包含到文档。

**HIDE_UNDOC_MEMBERS**
若设为YES,doxygen 将隐藏在文档化的类或文件中的所有未文档化的成员,若设为NO(默认),这些成员将包含在一些预览中,但不会有文档小节生成,如果EXTRACT_ALL 为YES,此选项无效。

**HIDE_UNDOC_CLASSES**
若设为YES,doxygen 将隐藏所有未文档化的类,若设为NO(默认),这些类将被包含在一些预览中,但不会有文档小节生成,如果EXTRACT_ALL为YES,此选项无效。

**HIDE_FRIEND_COMPOUNDS**
若设为YES,doxygen 将隐藏所有友元(类|结构|联合)声明,若设为NO(默认),这些声明将包含在文档中。

**HIDE_IN_BODY_DOCS**
若设为YES,doxygen 将隐藏函数主体中的一些文档块,若设为NO(默认),这些块将出现在函数的细节文档块中

**INTERNAL_DOCS**
用于确认在一个\internal 命令之后能否包含文档。若设为NO(默认),那么文档将被移除,如设为YES,将包含内部文档。

**HIDE_SCOPE_NAMES**
若设为NO(默认),doxygen 将显示文档中类成员和名字空间的作用域,若设为YES,此作用域将被隐藏。

**SHOW_INCLUDE_FILES**
若设为YES(默认),doxygen 将在文件的文档中放置它所包含文件的列表。

**FORCE_LOCAL_INCLUDES**
若设为YES,doxygen 将会在文档中使用双引号列出所包含的文件,而不是尖括号。

**INLINE_INFO**
若设为YES(默认),将在文档中插入inline标记来指示inline 成员。

**SORT_MEMBER_DOCS**
若设为YES(默认),doxygen 将按英文字母的顺序对文件和类的成员名字进行文档排序,若设为NO,成员将按声明的顺序出现。

**SORT_BRIEF_DOCS**
若设为YES,doxygen 会按英文字母的顺序将文件,名字空间和类的成员名字,作为它们简明描述的排序依据,若设为NO(默认),成员将按声明的顺序出现。

**SORT_GROUP_NAMES**
若设为YES,doxygen 会按英文字母的顺序对组名的层级进行排序。若设为NO(默认),组名将按定义的顺序出现。

**SORT_BY_SCOPE_NAME**
若设为YES,将由类的全称(即包含名字空间)对类列表进行排序。若设为NO(默认),类列表排序只能由不包
含名字空间的类名决定。
注意:
如果HIDE_SCOPE_NAMES设为YES,这个选项不太有价值。
此选项只适用于类列表,且不是按字母排序的列表。

**SORT_MEMBERS_CTORS_1ST**
若设为YES,doxygen 将对类成员的(简明和细节描述)文档进行排序,且构造器和析构器将位于列表首部。若设为NO(默认),构造器将出现在SORT_MEMBER_DOCS,SORT_BRIEF_DOCS 所设定的各自定义的位置。
注意:
若SORT_BRIEF_DOCS设为NO,此选项将忽略成员简明描述的排序。
若SORT_MEMBER_DOCS 设为NO,此选项将忽略成员细节描述的排序。

**GENERATE_DEPRECATEDLIST**
用于有效(YES)或失效(NO)废弃列表(主要针对类和类方法),通过放置\deprecated命令来创建废弃列表。

**GENERATE_TESTLIST**
用于有效(YES)或失效(NO)测试列表,通过放置\test命令来创建测试列表。

**GENERATE_BUGLIST**
用于有效(YES)或失效(NO)bug 列表,通过放置\bug 命令来创建bug列表。

**ENABLED_SECTIONS**
用于有效某些条件化文档小节,可使用标记,\if <小节标号> … \endif 和\cond <小节标号> … \endcond 的块结构。

**MAX_INITIALIZER_LINES**
用于确定一个变量或定义初始化时能使用的最大文本行数,如果初始化时的行数超过最大值,那么它将被隐藏。
将最大值设为0 将完全隐藏初始化的文本。可在文档中使用\showinitializer 和\hideinitializer 命令,来控
制个别变量和定义的初始化文本。

**SHOW_USED_FILES**
若设为NO,在类和结构文档的底部无效文件列表的生成。若设为YES,列表将会提取那些已被用于生成文档的文件。

**SHOW_FILES**
若设为NO,将无效文件页面的生成,并将文件从快速索引和文件树浏览(如果指定)中移除。默认设定为YES。
SHOW_NAMESPACES

若设定为NO,将无效名字空间页面的生成,并将名字空间从快速索引和文件树浏览(如果指定)中移除。默认设定为YES。

与警告和处理消息相关的选项

**QUIET**
用于打开或关闭doxygen生成输出时的消息,若设定YES表明关闭消息,若留白则设定为NO。

**WARNINGS**
用于打开或关闭doxygen生成错误记录时的警告消息,若设定YES表明打开警告消息,若留白则设定为NO。
技巧:当写文档时应打开警告消息。

**WARN_IF_UNDOCUMENTED**
若设为YES,doxygen 将为未文档化的成员生成警告消息,如果EXTRACT_ALL设为YES,那么该标记将自动失效。

**WARN_IF_DOC_ERROR**
若设为YES,doxygen 将为文档中潜在的错误生成警告消息,例如在一个文档化函数中并没有文档化一些参数,或文档化的参数并不存在,又或者使用了错误的标记命令。

**WARN_NO_PARAMDOC**
用于获得文档化函数所生成警告消息,但不能兼顾到它的参数和返回值。若设为NO(默认)doxygen只能生成错误或参数文档不完整的警告,而不能监控文档的缺失。

**WARN_FORMAT**
确定doxygen 所生成警告消息的格式,消息字串会包含$file, $line, $text 标记,并且这些标记将被发出警告的文件名,行号,以及相应的文本所替换。

**WARN_LOGFILE**
用于指定一个警告和错误消息写入的日志文件,如果留空表示将消息写入stderr。

与输入相关的选项
**INPUT**
用于指定将被文档化的源文件和目录,你可以输入myfile.cpp 文件名或/usr/src/myproject 目录名,多个文件名或目录名可用空格进行分离。
注意:如果此标记留空,那么将搜索当前目录。

**INPUT_ENCODING**
用于指定doxygen解析源文件所使用字符编码,doxygen内部使用UTF-8编码,同样也是默认的输入编码。 Doxygen
可使用libiconv(或者在libc中创建iconv)进行编码转换。查看http://www.gnu.org/software/libiconv/ 中
编码列表。

**FILE_PATTERNS**
如果INPUT包含有目录,可用此选项指定一个或多个通配符(如*.cpp和*.h)在目录过滤源文件。假如选项后留空,以下的扩展名将用于过滤:.c *.cc *.cxx *.cpp *.c++ *.java *.ii *.ixx *.ipp *.i++ *.inl *.h *.hh*.hxx *.hpp .h++ *.idl *.odl *.cs *.php *.php3 *.inc *.m *.mm 。

**FILE_VERSION_FILTER**
用于指定一个程序或脚本,使得doxygen 能调用每个文件以获得当前版本(一般通过CVS 版本控制系统获取),
且doxygen 将会执行(使用popen())command input-file 命令来调用该程序,其中command 为
FILE_VERSION_FILTER 后跟的设定名称,input-file 则为doxygen所支持的输入文件名。无论该程序向标准输出
写入任何内容,都将被用做文件版本。

**LAYOUT_FILE**
用于指定一个能被doxygen 解析的布局文件。在一种独立的输出格式中,此布局文件可以控制所生成的输出文件的全局结构。创建默认的布局文件可运行doxygen附带-l 选项,并且可选择在选项之后是否指定一个文件名,如果文件名被忽略将使用DoxygenLayout.xml,注意,如果你运行doxygen 的目录中已经包含了一个名为DoxygenLayout.xml的文件时,倘若LAYOUT_FILE之后留空doxygen 将自动解析该文件。

**RECURSIVE**
用于是否在子目录中搜索可用的输入文件,如果选项之后留空则设为NO。

**EXCLUDE**
用于指定那些文件和目录将从INPUT选项中将被移除。这种方式使你很容易得从INPUT选项设定根目录树中,移除一个子目录。

**EXCLUDE_SYMLINKS**
用于选择是否从输出中移除文件或者目录的符号链接(一个Unix文件系统的特性)。

**EXCLUDE_PATTERNS**
在INPUT 选项设定的目录中,使用该选项指定的一个或多个通配符来移除匹配的文件。
注意,通配符将对文件的绝对路径进行匹配,如移除所有的测试目录,可使用*/test/*的样式。

**EXAMPLE_PATH**
指定一个或多个包含例子代码段的文件或包含例子文件的目录。(在\include 小节中查看\include 命令)

**EXAMPLE_RECURSIVE**
若设为YES,将在子目录中搜索输入例子文件,可使用\include 或\dontinclude 命令,它与RECURSIVE无关,如果选项之后留空则设为NO。

**EXAMPLE_PATTERNS**
若EXAMPLE_PATH 选项之后含有目录,可用此标记指定一个或多个通配符(如*.cpp和*.h),从上述目录中过滤掉匹配的文件,如果选项后留空则设为NO。

**IMAGE_PATH**
用于在文档中指定一个或多个包含图片的文件或是包含图片文件的目录。(查看\image命令)

**INPUT_FILTER**
指定一个程序,使得doxygen 对每一个输入文件进行过滤,doxygen 调用过滤程序可以执行(使用popen())这个命令,则为INPUT_FILTER 的设定值,则为输入文件名,doxygen 会将过滤程序的输出写入到标准输出中。

**FILTER_PATTERNS**
用于在每种文件样式的基础上指定过滤规则。Doxygen 将会比较文件名和每一种样式,并检查是否与过滤规则匹配。这些过滤规则来自一个列表:pattern=filter(如*.cpp=my_cpp_filter),查看INPUT_FILTER 进一步获如何使用过滤器的信息,假设选项后留空,INPUT_FILTER将用于全部文件。

**FILTER_SOURCE_FILES**
若设为YES,输入过滤器(可使用INPUT_FILTER 设定)既可过滤输入文件,也可用于生成源文件的浏览(当SOURCE_BROWSER 设为YES时)。

与源码浏览相关的选项

**SOURCE_BROWSER**
若设为YES,将生成一个源码文件的列表。文档主体部分将对这些源码进行交叉引用。注意,在生成输出的过程中与所有源码的关联有可能失效,因此要确认VERBATIM_HEADERS是否设为NO。

**INLINE_SOURCES**
若设为YES,在文档中将直接包含函数,类,枚举的代码段。

**STRIP_CODE_COMMENTS**
若为YES(默认),告知doxygen隐藏一些来自源码段中特殊的注释块,正常情况下C和C++的注释始终可见。

**REFERENCED_BY_RELATION**
若为YES,所有的文档化函数都将会列出其引用过的函数。

**REFERENCES_RELATION**
若为YES,所有的文档化实体都将会列出其调用或使用过的函数。

**REFERENCES_LINK_SOURCE**
若为YES(默认),且SOURCE_BROWSER 也为YES,那么REFERENCES_RELATION,REFERENCED_BY_RELATION 所生成列表中函数的超链接将指向源码,否则将指向该函数的文档。

**VERBATIM_HEADERS**
若为YES(默认),doxygen 将为类所指定的头文件,生成一个相同的副本,doxygen will generate a verbatim copy of the header file for each class for which an include is specified 若为NO 则无效。
也可查看\class 小节。

**USE_HTAGS**
若为YES,对于源码的引用,将指向由htags工具而非doxygen内建的源码浏览器生成的HTML。Htags工具是GNU
全局源码标签系统GNU’s global source tagging system的一部分(参看http://www.gnu.org/software/global/global.html)。按以下步骤使用htags工具:
1.安装最新的版本(如4.8.6 或更新的)2.有效SOURCE_BROWSER,USE_HTAGS3.确认INPUT指向的是源码树的根目录4.正常运行doxygen

Doxygen 将调用htags(依次调用gtags),这些工具只有在命令行下才有效(并存在于系统的检索路径中)。

得到的结果,可替代doxygen 所生成的源码浏览器,指向源码的链接将会指向htags 的输出。

与字母索引相关的选项
**ALPHABETICAL_INDEX**
若为YES,将会生成一个所有合成部分的字母索引。如果项目中包含一些类,结构,联合和接口时,应有效此标记。

**COLS_IN_ALPHA_INDEX**
如果ALPHABETICAL_INDEX有效,那么此标记可用于指定每列的间距(间距的范围是1~20)。

**IGNORE_PREFIX**
项目中所有的类都是由一个公共的前缀开始,那么所有的类也将被放置到字母索引中相同的首部之下。此标记可指定一个特殊的前缀(或是一个前缀列表),当生成索引首部时却可以忽略掉。