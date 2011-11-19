.. tkscala documentation master file, created by
   sphinx-quickstart on Sat Oct  1 10:04:22 2011.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

.. title:: 対話環境(REPL)について

対話環境(REPL)について
======================

REPLって？
----------

Read-Eval-Print-Roopの略。

読み込み-評価-表示を繰り返す対話型の評価環境。

Rubyで言うところのirbとか。

REPLの起動
----------

scalaコマンドを引数なしで実行するとREPLが起動します。

.. code-block:: none

    $ scala
    Welcome to Scala version 2.9.1.final (OpenJDK Server VM, Java 1.6.0_23).
    Type in expressions to have them evaluated.
    Type :help for more information.

    scala>

とりあえず基本のHello World
---------------------------

.. code-block:: scala

    scala> println("Hello World")
    Hello World

    scala>

代入・束縛
----------

.. code-block:: scala

    scala> val a = 1
    a: Int = 1

    scala> a + 1
    res1: Int = 2

    scala> println(res1)
    2

    scala>

Tabによる補完
-------------

.. code-block:: none

    scala> 1.<TAB>
    !=             ##             %              &              *
    +              -              /              <              <<
    <=             ==             >              >=             >>
    >>>            ^              asInstanceOf   equals         getClass
    hashCode       isInstanceOf   toByte         toChar         toDouble
    toFloat        toInt          toLong         toShort        toString
    unary_+        unary_-        unary_~        |

    scala> 1.

REPLのコマンド
--------------

.. code-block:: none

    scala> :help
    All commands can be abbreviated, e.g. :he instead of :help.
    Those marked with a * have more detailed help, e.g. :help imports.

    :cp <path>                 add a jar or directory to the classpath
    :help [command]            print this summary or command-specific help
    :history [num]             show the history (optional num is commands to show)
    :h? <string>               search the history
    :imports [name name ...]   show import history, identifying sources of names
    :implicits [-v]            show the implicits in scope
    :javap <path|class>        disassemble a file or class name
    :keybindings               show how ctrl-[A-Z] and other keys are bound
    :load <path>               load and interpret a Scala file
    :paste                     enter paste mode: all input up to ctrl-D compiled together
    :power                     enable power user mode
    :quit                      exit the interpreter
    :replay                    reset execution and replay all previous commands
    :sh <command line>         run a shell command (result is implicitly => List[String])
    :silent                    disable/enable automatic printing of results
    :type <expr>               display the type of an expression without evaluating it

    scala>

コマンドの解説

.. code-block:: none

    :quit

REPLを終了します。

exitでも終了できるが、現在は（当ドキュンメント執筆時点では2.9.1.final）deprecationになっています。

.. code-block:: none

    :help [command]

各コマンドのhelpを表示します。引数なしの場合はコマンドの一覧を表示します。

取り敢えず困ったらコレ。

.. code-block:: none

    :cp <path>

classpathを通します。

.. code-block:: none

    :load <path>

Scalaのスクリプトファイルを読み込みます。

.. code-block:: none

    :history [num]

過去に実行した内容を[num]で指定した世代分表示します。

[num]を省略した場合は20世代分表示。

.. code-block:: none

    :h? <string>

.. code-block:: none

実行履歴から<string>の含まれる履歴を表示します。

.. code-block:: none

    :imports [name name ...]

[name]で指定したもののうち、REPLでimportされているものを表示します。
[name]を省略した場合はすべて表示されます。

.. code-block:: none

    :implicits [-v]

暗黙の型変換（implicit conversion）の一覧を表示します。

REPLで定義されたものは表示されません。

-vのオプションをつけることで、Predefに定義されている暗黙の型変換も表示されます。

.. code-block:: none

    :javap <path|class>

指定したパス/クラスをjavapします。

.. code-block:: none

    :keybindings

キーボードショートカットの一覧が表示されます。

.. code-block:: none

    :paste

複数行を一気に流し込んで評価することができます。

すべて入力後、Ctrl-Dすると、複数行入力された式がまとめて評価されます。

.. code-block:: none

    :replay

直前に評価した式を再度実行します。

.. code-block:: none

    :sh <command line>

<command line>をシェルで実行します。

結果はList[String]で格納されます。

.. code-block:: none

    :silent

式の評価結果の表示/非表示が切り替わります。

デフォルトでは表示になっているため、:silentを実行すると非表示になり、もう一度実行すると表示になります。

.. code-block:: none

    :type <expr>

<expr>の式を実行せず、戻り値の型を表示します。

Power User Modeについて
-----------------------

:powerをREPLで実行することにより、REPLがPowerUserモードになります。

REPL自体を拡張するためのリソースへのアクセスが可能になり、コマンドが追加されます。

.. code-block:: none

    scala> :power
    ** Power User mode enabled - BEEP BOOP SPIZ **
    ** :phase has been set to 'typer'.          **
    ** scala.tools.nsc._ has been imported      **
    ** global._ and definitions._ also imported **
    ** Try  :help,  vals.<tab>,  power.<tab>    **

    scala> :help
    All commands can be abbreviated, e.g. :he instead of :help.
    Those marked with a * have more detailed help, e.g. :help imports.

    :cp <path>                 add a jar or directory to the classpath
    :help [command]            print this summary or command-specific help
    :history [num]             show the history (optional num is commands to show)
    :h? <string>               search the history
    :imports [name name ...]   show import history, identifying sources of names
    :implicits [-v]            show the implicits in scope
    :javap <path|class>        disassemble a file or class name
    :keybindings               show how ctrl-[A-Z] and other keys are bound
    :load <path>               load and interpret a Scala file
    :paste                     enter paste mode: all input up to ctrl-D compiled together
    :power                     enable power user mode
    :quit                      exit the interpreter
    :replay                    reset execution and replay all previous commands
    :sh <command line>         run a shell command (result is implicitly => List[String])
    :silent                    disable/enable automatic printing of results
    :type <expr>               display the type of an expression without evaluating it
    :dump                      displays a view of the interpreter's internal state
    :phase <phase>             set the implicit phase for power commands
    :wrap <method>           * name of method to wrap around each repl line

    scala> vals.
    asInstanceOf   completion     global         history        intp
    isInstanceOf   isettings      phased         power          reader
    repl           toString       vals

    scala> power.
    AnyName             AnySymbol           AnyTree             AnyType
    GlobalType          Implicits           InternalInfo        Name
    Prettifier          StringPrettifier    Symbol              Tree
    Type                asInstanceOf        banner              context
    global              init                intp                isInstanceOf
    phased              repl                rutil               source
    toString            trees               typeOf              unit
    unleash             upDependentName     upDependentSymbol   upDependentTree
    upDependentType

PowerUserモードコマンドの解説

.. code-block:: none

    :dump

REPLで定義された識別子の一覧を表示します。

.. code-block:: none

    :phase <phase>

デフォルトのPhaseをセットします。

<phase>を省略するとアクティブなphaseが表示され、clearを指定するとphaseがクリアされます。

※詳細が良く分かってない…

.. code-block:: none

    :wrap <method>

REPLの式の実行自体をラップして評価処理を拡張します。
