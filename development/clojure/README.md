backup
=========================================================================


```
    ����ϰ�, ǥ������ ���� �ڵ�
     '�ڵ�� �������� ���°� ����'�� Lisp�� Ư��
    ���� �����ϸ� �ӵ��� ���� �ڹٿ��� ��ȣ�ۿ�
    ��� ������ ���¸� �� �������̽��� �ٷ�� ���ִ� ������ ���̺귯��
    ���뼺�� ���̰� ������ ���̴� �Լ��� ���α׷���
    ��(lock)����� �ƴ�, ���� ���� ���� ���α׷���.

 

�Լ��� ���ڴ� ����Ʈ()��� ����[]�� ǥ���ȴ�.

 

defn : �Լ�����
def : �Լ� �Ӹ� �ƴ϶� �����͵� ����.
defref : ���۷����� �����ϴ� ���� ���캽.(����� @)

#{} �� ����(set)�� ǥ��

 

conj (conjoin)
 : ���� �÷��ǿ� �� �������� �߰��ϴµ� ���.
(conj coll item)


ref (reference) : ����
(ref initial-state)

alter :
(alter r update-fn & args)

dosync : Ʈ������� ����.
(dosync & exprs)

require : Ŭ���� ���̺귯�� �ε�
(require quoted-namespace-symbol)

refer : ���� �̸� ������ ��� �̸��� ���ο� �̸� �������� ����
(refer quoted-namespace-symbol)

use : require�� refer�� �Ѳ����� �̷����.
(use quoted-namespace-symbol)
:reload-all �÷��� : ������ ���̺귯���� �ٽ� �ε�.


doc : �ּ��̳� ������ REPL���� �ٷ� ��
(doc name)

    (defn hello
      "Writes hello message to *out*. Calls you by username.
      Knows if you have been here before"
      [username]
      (dosync
        (let [past-visitor (@visitors username)]
          (if past-visitor
            (str "Welcom back, " username)
            (do
              (alter visitors conj username)
    (doc hello)


find-doc : �˻�� �Ǵ� ���ڿ� �Ǵ� ���Խ��� �ѱ�� �ش� �˻�� �����ϴ� ��� ������ ã����
(find-doc s)

' : �ο�(quoting)��ȣ.

Lancet : ������ ��� ���� �ý���
- Ŭ���� �ڵ� �״�θ� ���.
- �������� ���� ǥ���� �ʿ䰡 ����.
- ��Ʈ�� �½�ũ ���̺귯���� ȣ���ؼ� Ȱ���� �� �� �ִ�.
```



```
�ڷ���
nil - nil
boolean - true /false
character - \a
number - 1,2,3
string - "Hello"
keyword - :tag
symbol - user/foo, java.lang.String
list - (1,2,3)
set - #{:snap :crackle :pop}
map - {:name "Bill"}
vector - [1,2,3]

 

(class CLASS)
(rem REMAINDER)
(quot QUOTIENT)

 

Symbol
�Լ�
������(�ᱹ���� �Լ�)
�ڹ� Ŭ����
�ڹ� ��Ű��
�ڷᱸ�� �� ���۷���(ref)

(print "hello") ==> hello | nil
//println
(str & args)
(str 1 2 3) ==> "123"
(.toUpperCase "hello") ==> "HELLO"
(apply f args* argseq) - args�� argseq�� Ǯ������ f�� ���ڷ� �ѱ��.
(take-nth 2 ������) : ���ڿ��κ��� ù ���ں��� ��ĭ ������ ���ڸ� ����.

boolean & nil
(find-doc #"\?$")
nil ��� false != true
Ŭ���������� �� ����Ʈ()�� true�� ���

(true? true) ==> true
(false? nil) ==> false
(nil? false) ==> false
(zero? 0) ==> true

    1:40 user=> (def inventors {"Lisp" "McCarthy" "Clojure" "Hickey"})
    #'user/inventors
    1:41 user=> (inventors "Lisp")
    "McCarthy"
    1:43 user=> (inventors "xxx")
    nil

 

    (get a-map key not-found-val?)
    1:44 user=> (get inventors "Lisp" "����?")
    "McCarthy"
    1:45 user=> (get inventors "xxx" "����?")
    "����?"


keyword (�ݷ�, :)
keyword�� ���ϸ� keyword��ü�� ��ȯ.

    1:47 user=> (def inventors {:Lisp "McCarthy" :Clojure "Hickey"})
    #'user/inventors
    1:50 user=> (inventors :Clojure)
    "Hickey"
    1:51 user=> (:Clojure inventors)
    "Hickey"

 
����ü ����

(defstruct name & keys)
(defstruct book :title :author)

    CL-USER> (defstruct book title author)
    STYLE-WARNING: redefining MAKE-BOOK in DEFUN
    BOOK
    CL-USER> (make-book :title "hi" :author "test")
    #S(BOOK :TITLE "hi" :AUTHOR "test")

 
����ü�ν��Ͻ� ����

(struct name & vals)
(def no1 (struct book "
(struct-map name & inits) - �Ӽ��� ���� ���� �߰� �� �� �� �ִ�.
Reader Macro
;����� - �ּ�
~ - �򰡱�ȣ
~@ - ���� �򰡱�ȣ
@form == (deref form) - deref
^form == (meta form) - meta
`x - ���� ����ǥ
'form == (quote form) - �ο�
#^metadata form - ��Ÿ������
#(.toUpperCase %) - �͸��Լ�
#"foo" => a java.util.regex.Pattern - ����ǥ����
#'x == (var x) - var-quote

���ο� ���� ��ũ�θ� ������ �� �ֵ��� ������� ����.

 
Function

(defn name doc-string? attr-map?
  [params*] body)

(defn name doc-string? attr-map?
  ([params*] body))

anonymouse function

    �Լ��� �ʹ��� �����Ͽ�, �Լ��� �̸��� ���̴°��� �ڵ带 �� �а� ��ư� ����� ���
    �ٸ� �Լ��� ���ο����� ���̴� �Լ��� �ֻ��� �������� �̸��� ���� �ʿ䰡 ������.
    �Լ� ���ο��� �����͸� �̿��� �������� �Լ��� ����� ���� ���.

(fn [params*] body) ==> #(body)
���ڴ� %1, %2������ ǥ�ð���(ù��° ������ ��� %��� ����)

(defn make-greeter [greeting-prefix]
  (fn [username] (str greeting-prefix ", " username)))

1:1 user=> (def hello-greeting (make-greeter "Hello"))
#'user/hello-greeting
1:2 user=> (hello-greeting "world")
"Hello, world"

make-greeter�� ��ȯ�ϴ� �Լ��� greeting-prefix���� ���� Closure.

 
Var

(var a-symbol)
Binding

(let [bindings*] exprs*)
Destructuring

���ε��� �Ǵ� �̸��� �� �ڸ��� ��� ���ͳ� ���� �־� ���ϴ� �κи� ���ε�.

(defn greet-author-1 [author]
  (println "Hello, " (:first-name author)))

(defn greet-author-2 [{fname :first-name}]
  (println "Hello, " fname))

(greet-author-1 {:last-name "Vinge" :first-name "Vernor"})
(greet-author-2 {:last-name "Vinge" :first-name "Vernor"})


������ھ�(_) - �� ���ε����� �Ű澲�� �ʰڴٴ� �ǹ̸� ǥ���ϱ� ���� ���̴� ���������� ���Ǵ� �ɹ�
(let [[_ _ z] [1 2 3]]
  z)

:as - ��Ʈ��ó�� ǥ���� ������ ����ϸ� �÷��� ��ü�� ���ε� �� �� �ִ�.
(let [[x y :as coords] [1 2 3 4 5 6]]
  (str " x: " x " y: " y " total count:" (count coords)))

 
Name space

(resolve sym)
 : �ɹ��� ���� �̸� �������� ����Ű�� ������ Ŭ���� ���� ��ȯ�Ѵ�.
(in-ns name)
 : in-namespace. �̸� ������ �����ϰų� �� �̸������� ���� �� �ִ�.
(import '(package Class+))
 : �ڹ�Ŭ������ ���� �̸� �������� import�ؿ´�.
(use 'xxx)
 : ���� �̸� �������� �����´�.

(use '[clojure.contrib.math :only (round)])
(round 1.2)


(use :reload 'examples.exploring) - �̸������� �ٽ� �ε�
(use :reload-all 'examples.exploring) - ���õ� �̸��������� �ٽ� �ε�.

(ns name & reference)
 : ���� �̸�����(*ns*�� ����������)�� name�� �ش��ϴ� �̸� �������� �ٲ۴�.

if, do

(defn is-small? [number]
  (if (< number 100)
    "yes"
    (do
      (println "Saw a big number:" number)
      "no")))

(loop [bindings *] exprs*)
(recur exprs*)

(loop [result [] x 5]
  (if (zero? x)
    result
      (recur (conj result x) (dec x))))

Metadata

'��ü���� ������ ������ ������ ������'
(with-meta object metadata)

(def stu {:name "Stu" :email "stu@thinkrelevance.com"})
(def serializable-stu (with-meta stu {:serializable true}))
(= stu serializable-stu)
(meta stu)
(meta serializable-stu)
= �� ���� ������ �Ǵ�.
identical? �� ref�� ������ �Ǵ�.(java�� ==)

(assoc map k v & more-kvs)
���� �ʿ� Ű&���� �߰��� ���� ���� �� �ִ�.


Reader Metadata

:arglists - ���� ��
:doc - ����
:file - �ҽ� ����
:line - �ҽ� �� ��ȣ
:macro - ��ũ�� ����
:name - ���� �̸�
:ns - �̸� ����
:tag - ����Ǵ� ���� or ��ȯ Ÿ��


(meta #'str)
==>
{:ns #<Namespace clojure.core>,
 :name str, :file "clojure/core.clj",
 :line 356, :arglists ([] [x] [x & ys]),
 :tag java.lang.String,
 :doc "With no args, returns the empty string. With one arg x, returns\n  x.toString().  (str nil) returns the empty string. With more than\n  one arg, returns the concatenation of the str values of the args."}
```