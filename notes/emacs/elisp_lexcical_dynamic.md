Emacs Lisp������ lexcial scoping�� dynamic scoping


���� : http://yoo2080.wordpress.com/2011/12/31/lexical-scoping-and-dynamic-scoping-in-emacs-lisp/


�� ������ ������ �͵�:

1. `Emacs Lisp`������ **lexcial scoping**�� **dynamic scoping**�� ������
2. **dynamic scoping**���� �����ؾ��� ��
3. **lexical scoping**�� **lexical closures**�� �� �� �ִ� ��
4. **lexical scoping**�ڵ�� **dynamic scoping**�ڵ带 ������ �߻��ϴ� ��


`Emacs Lisp`�� Emacs 23(����)���� ���������� �׻� **dynamically scope**�����ϴ�. Emacs 24���� **lexical scoping**�� ������ �߰��Ǿ����ϴ�. ���� �̵��� ��κ��� ��� **dynamic scoping**���� **lexical scoping�� ���ٴµ� �����ϱ⿡, ����� ���� ���Դϴ�. �� �׷����� ���ؼ��� �������� �� Ȯ���Ͻ� �� ���� ���Դϴ�.

**lexical scoping**���� �������� �ϴ� el������ �ִٸ�, ù�ٿ� `-*- lexical-binding: t -*-`�� �߰��ϱ⸸ �ϸ� �˴ϴ�. �׷���, Emacs 24�� ������ ������, �� el���ϼ� �ڵ忡 **lexical scoping**�� �����ϰ� �˴ϴ�.
 

�������, ���� init ������ ù���� ������ �����ϴ�.

```elisp
;; -*- coding: utf-8 -*-
```

�׸���, ������ ���� �ٲٰڽ��ϴ�.

```elisp
;; -*- coding: utf-8; lexical-binding: t -*-
```

�̸��ϸ�, �� init���Ͽ� �ִ� �ڵ�� Emacs24���� **lexically scope**�� �� ���Դϴ�. �ڼ��� ���� [file variables]�� Ȯ���� ���ñ� �ٶ��ϴ�. 

**lexcial scoping**�� �������� Ȯ���غ��� ����, �켱 �� el������ ���� (`C-x C-f lexical-scratch.el RET`) ���� ������ �߰��� ���ô�:

```elisp
;; -*- lexical-binding: t -*-
```

������ ��, ���۸� ���������ϴ� (`M-x revert-buffer`). ���� ����� **lexical scoping**�� ���� `scratch`����ó�� ����� �� �ֽ��ϴ�.

**dynamic scoping**�� **lexical scoping**�� �����ϱ��? ������ ���� ������ ���캸���� �ϰڽ��ϴ�.

```elisp
(setq a 17)
(defun my-print-a ()
  (print a))
(setq a 1717)
(let ((a 8))
  (my-print-a))
```

`my-print-a`�� `a`�� �������� �ʾҴٴ� ����� �ָ��Ͻñ� �ٶ��ϴ�. �̷��� ���� ���� **"free variable"**�̶� �θ��ϴ�.

 �� �ڵ带 �������� ����� ��� ���ñ��? `1717`�� ����ұ��? �ƴϸ� `8`�ϱ��? **dynamic scoping**�̶�� `8`�� ����ϰ�, **lexical scoping**�̶�� `1717`�� ����մϴ�.  **dynamic scoping**����, `my-print-a`�� �ִ� `a`�� `my-print-a`�� **ȣ��ɶ�(when my-print-a is called)**  �����˴ϴ�. **lexical scoping**���� `my-print-a`�� **���ǵ� ���(where my-print-a is defined)**�� ���� �����˴ϴ�.

**dynamic scoping**������ �ڵ�� `8`�� ����ϴµ�, `my-print-a`�� ȣ��ɽ� `a`�� `8`�� local bind�� let form�� �ֱ� �����Դϴ�. let form���Ŀ� `my-print-a`�� ȣ���Ѵٸ�, `1717`�� ����� ���Դϴ�..

**lexical scoping**������ �ڵ�� `1717`�� ����մϴ�. �켱, `my-print-a`�� ���ǵ� ���� let form ���̹Ƿ�, `my-print-a`�� �ִ� `a`�� let form���� ������ **local binding**�� �ƴ� **global binding**�� `a`�� �����ϱ� �����Դϴ�. ��������, `my-print-a`�� ȣ��ɽ�, `8`�̵� **local value "a"**�� �޸�, **global value "a"**�� `1717`�̱� �����Դϴ�. ���� `my-print-a`�� ���Ǹ� let form���� �ű�ٸ�, ��µ� ���� `8`�� �� ���Դϴ�. `my-print-a`�� �ִ� `a`�� let form���� ������� **local binding�� a**�� ������ ���̱� �����Դϴ�.

������ �ڵ带 Javascript�� �Űܺý��ϴ�.

```elisp
var a;
a = 17;
function myPrintA() {
  console.log(a);
}
a = 1717;
(function () {
  var a = 8;
  myPrintA();
}());
```

�� �ڵ�� `1717`�� ����մϴ�. ���ó� ���α׷��� ��� ��κ��� **lexically scoped**�Դϴ�.

�����в��� Emacs 24�� ����ϽŴٸ�, ���� �ڵ带 scratch���ۿ��� �������ν� `1717`�� ����ϴ� ���� Ȯ���� �� �� �ֽ��ϴ�.

```elisp
(eval
 '(progn
    (setq a 17)
    (defun my-print-a ()
      (print a))
    (setq a 1717)
    (let ((a 8))
      (my-print-a)))
 t)
```

Emacs 24������ `eval`�Լ��� �ι�° ����(optional)�� �޽��ϴ�. �̰� `t`���, **lexical scoping**���� ���մϴ�. `(progn ...)`�տ� '�� ���̴� ���� ���� ���ñ� �ٶ��ϴ�.

**Lexical scoping**�� **lecical closures**�� ������ �մϴ�. �׷��ٸ� **lexcial closure**�� �����ϱ��? ���� �ڵ带 ���캸���� �ϰڽ��ϴ�.

```elisp
(setq a 0)
(let ((a 17))
  (defun my-print-a ()
    (print a))
  (setq a 1717))
(let ((a 8))
  (my-print-a))
```

**lexical scoping**����, �� �ڵ�� `1717`�� ����մϴ�. ������ `Alice`�� ������ ���Դϴ�:

> ó������ �̻����� �ʾҴµ�, �ٽú��� ���� �� �̻��ѵ�. ����, "**lexical scoping** �̹Ƿ�, `my-print-a`�� �ִ� `a`�� ù��° `let` form������ ������� **local binding** �� �����ؼ� `1717`�� ����" ��� ��������. �ٽ� ���캸��, `my-print-a`�� ȣ��ɽ� ù��° `let` form�� ���� ������� **local binding**�� �����(expired)�Ŷ�� �ž�! ��¥ ����(expired) ������ ���� �� ���ݾ�! "�̾�, ���� ���̻� �������� �ʾ�" ��� �� `1717`�� ��µ� ����? ������ Ŀ�� **lexcial scope**�� ���ư��� ������ ����?

ù��° let form�� �������� ���Ŀ��� ù��° `a`�� **local biding**�� ��Ƴ���, `my-print-a`�� �����ϱ⸸�� ��ٸ��ϴ�. `my-print-a`�� �����ϰ� ù��° `a`�� `local biding`�� ���� ��� ������ ����˴ϴ�. �̴� Emacs�� �ڿ��� �������� �ϵ��� �����ϸ�, **lexical scoping**�� **"������"**���� �� ���� ���� �� �� �ְԵǾ��ٴ� ���� �ǹ��մϴ�.

�׷���, **lexcial closure**�� �����ϱ��? �̴� "**lexical scoping**�� ���� �� ���� ���� �� �� �ִ�"��� ���� ȭ�� �ڿ��� ��� �����Ǵ����� �����ֽ��ϴ�. `(symbol-function 'my-print-a)`�� ���ϸ� �� �� �ִ� ��ó��, `my-print-a`�� �Լ� ����([function cell])�� a�� ���� ����� binding�� ���� link�� ��� �ֽ��ϴ�. �Լ� ���ǿ� �Լ� ������ scope�� ���� link�� ����(combination)�� **lexical closure** �� �θ��ϴ�. Ȥ��, ����� binding�� �����ϴ� **lexically scoped** �� �Լ��� **lexical closure** �� �θ����� �ֽ��ϴ�. **lexical closures** �� ���� �ܼ��ϰ� **closures** �� �Ҹ��⵵ �մϴ�. **lexically scoped** ������ ��� **closures** �� �����ϴ°� �ƴմϴ�.


**lexical scoping** ����, �Լ��� �ִ� `a`�� �����ϴ� ���� �������� Ȯ���ϱ� ���ؼ�, �Լ� ��ü �ֺ��� ������ binding�� ���캸��˴ϴ�. **lexical scoping** �� �ڵ忡�� ������ ������ �ֺ��� ���캸�� �Ǳ⿡ ����ϱ� �����, ����� binding�� ���� ����Ǵ����� ���� ������ �ʿ䰡 �����ϴ�.

��, JavaScript�� �� �ڵ带 ���캾�ô�:

```elisp
var a, myPrintA;
a = 0;
(function () {
  // local variable a
  var a = 17;
  myPrintA = function () {
    console.log(a);
  };
  a = 1717;
}());
(function () {
  // local variable a
  var a = 8;
  myPrintA();
}());
```

Javascript�� **lexical closures** �� �����ϱ⿡ `1717`�� ����� ���Դϴ�:

Emacs 24����, **lexically scoped** (interpreted) �Լ����� `(closure ENV ARGS BODY...)`�� ���� �Լ� �� ���·� ǥ���Ǵ� �ݸ�, **dynamically scoped** �Լ����� �͸��Լ�(anonymous function)�� �ۼ��Ҷ� ����� �Ͱ� ������ ������ `(lambda ARGS BODY...)`�� ���� ���·� ǥ���˴ϴ�.

���� �ڵ�� **dynamic scoping**���� `(lambda (x y) (+ x y))`�� �ι� ����ϴ� �ڵ��Դϴ�.

```elisp
(defun my-sum (x y)
  (+ x y))
;; print the contents of function cell of my-sum
(print (symbol-function 'my-sum))
;; print an anonymous function
(print (lambda (x y) (+ x y)))
```

 **lexical scoping** �̶�� �� �ڵ�� `(closure (t) (x y) (+ x y))`�� �ι� ����� ���Դϴ�. **dynamic scoping**���� `(lambda ...)`�� �� ��ü�� �򰡵�����, **lexical scoping** ���� `(closure ...)`�� �򰡵˴ϴ� 

���� ���� �İ��� ���ô�. **lexcial scoping** ����, `�Լ� A`�� `�Լ� B`�� �����ϰ�, `�Լ� B`�� `�Լ� C`�� �����ϰ�, �� `�Լ� C`�� `a`�� ����ϸ�, `a`�� �켱 `C`�� ã�ƺ��� ������, `B`�� ����� ã�ƺ��� �˴ϴ�.

 **dynamic scoping**���� `my-func1`�� �Լ��� �����ٰ� �����غ��ô�. �� �Լ��� `my-func2`��� �Լ��� ȣ���ϰ�, `my-func2`�� `my-func3`�� `my-func3`�� `a`�� ����մϴ�. �׸��� `my-func2`�� `my-func3`�� ȣ���Ҷ� ���������� `a`�� `2`�� �����Ѵٰ� �غ��ô�. **dynamic scoping** ���� `my-func1`�� ȣ���ϸ� ����� �߻��ұ��? �̴� `2`�� ����մϴ�. `a`�� `1`�� ȯ�濡�� `my-func1`�� ȣ���ϸ� ����? ������ `1`��� `2`�� ����մϴ�. ���� �ڵ带 �������ô�.

```elisp
(defun my-func1 ()
  (my-func2))
(defun my-func2 ()
  (let ((a 2))
    (my-func3)))
(defun my-func3 ()
  (print a))
(let ((a 1))
  (my-func1))
```

`my-func1`�� ȣ��ǰ� `my-func2`�� ȣ��ǰ� ��� ���� ����, `a`�� `1`�� �� **local binding** �� ����ֽ��ϴ�. `my-func2`�� `a`�� `1`���Ͽ� ���� binding�� �������� �� �ٸ� **local binding** �� ��������ϴ�. �� ��������, ���� X��� ���ҿ� �ִٸ� `(let ((a 1)) (let ((a 2)) X ))`�� �ִ� �Ͱ� �����ϴ�. �� �������� `my-func3`�� ȣ��Ǿ� `2`�� ��µǰ� �˴ϴ�.

**dynamic scoping** ���� ��ġ�������� �������� �� �˾ƾ߸� �� ���� �ֽ��ϴ�. �Լ��� �Լ��� ���ڷ� ���ϵ��� ����� ���Ѵٰ� ������ ���ô�. ������ ���� �Լ��� �غ�Ǿ��ֽ��ϴ�.

```elisp
(defun my-call (f n)
  (funcall f n))

(my-call #'1+ 5) ; => 6
(my-call #'oddp 5) ; => t

(dolist (i (list 1 2 3))
  (print
   (my-call (lambda (x) (* i x)) 5))) ; prints 5 10 15
```

���ݱ��� ������Ѱ� �����ϴ�. �������� �Ѿ ������ �ϰڽ��ϴ�.

```elisp
(dolist (n (list 1 2 3))
  (print
   (my-call (lambda (x) (* n x)) 5))) ; prints 25 25 25 in dynamic scoping.
```

�������� �߻��� ���ϱ��? �� �̷��� �ൿ�� �ұ��? ������ `(lambda (x) (* n x))`���� ���� `n`�� `my-call`�� ������ �̸��� �ϳ��� ���� �����Դϴ�. ���� `n`�� `5`�� bind�� `my-call`���ο���, �͸��Լ� `(lambda (x) (* n x))`�� ȣ��˴ϴ�. **lexical scoping** ����, �� �ڵ�� ����Ѵ�� `5 10 15`�� ����մϴ�.

 * __�߰��Ѱ� 1__ - **dynamically scoped** �Լ��� �ٸ� �Լ��� ���ڷ� �Ѱ��ִ� ����, ���߿� �߸��� ���� �� �ִ�!

�ϳ� �� �߰��غ��ô�. `f`�� `g` �Լ��� ����, `g`�� ���� �����ϰ� `f`�� �����Ų �Ͱ� ������ �ռ��Լ��� ��ȯ�ϴ� �Լ��� ������ ���ô�.

```elisp
;; in dynamic scoping
(defun my-compose (f g)
  (lambda (x)
    (funcall f (funcall g x))))

(funcall
 (my-compose (lambda (n) (+ n 3)) (lambda (n) (+ n 20)))
 100) ; results in error, Lisp error: (void-variable f)
```

������ `f`�� ���ǵ��� �ʾҴٰ� �����ְ� �ֽ��ϴ�. �� �׷����? `my-compose`���� �Լ��� �ռ��Ǿ�����, `f`�� `g`�� bind���� ���� ������ ȣ��Ǿ����ϴ�. �ٽõ��ƿͼ�, **lexical scoping** ����, �� �ڵ�� ����� ��� �����մϴ�.

 * __�߰��Ѱ� 2__ - **dynamically scoped** �Լ����� ��ȯ�� �Լ��� �̿��ϴ� ����, ���߿� �߸��� ���� �� �ִ�.

Emacs 24����, `defvar`�� special variables�� �Ҹ��� ���� �����մϴ�. Special variables��, **lexically scoped** �Լ� ���̶� ������ dynamically�ϰ� bind�Ǵ�, **dynamically scoped** ����(variables)�Դϴ�. `case-fold-search`�� special variable�� �� ���Դϴ�. ��ҹ��ڸ� �����ϴ� �Լ� `search-forward`�� special variable `case-fold-search`�� ���� ������ �޽��ϴ�. `(search-forward "hello")`�� `case-fold-search`�� `t`�϶� `HELLO`�� ã����, `case-fold-search`�� `nil`�϶��� �׷��� �ʽ��ϴ�. **lexically scoped el** ���Ͽ��� ��ҹ��ڸ� �����ϱ� ���� `case-fold-search`�� �̿��ϵ� �߰� �ɼ��� ����, `my-search-forward` �Լ��� �����Ѵٰ� �����غ��ô�. `case-fold-search`�� special variable�̱⿡, ������ ȣ���ϸ�

```elisp
(let ((case-fold-search t))
  (my-search-forward "hello"))
```

��ҹ��ڸ� �������� �ʰ� �˻��Ѵٴ� ���� Ȯ���� �� ���� ���Դϴ�.

variable�� special���� Ȯ���ϱ� ����, �Լ� `special-variable-p`�� �̿��� �� �ֽ��ϴ�

```elisp
(special-variable-p 'print-level) ; => t
(special-variable-p 'print-length) ; => t
(special-variable-p 'debug-on-error) ; => t
(special-variable-p 'debug-on-quit) ; => t
```

Special variables�� ������ �� �ֽ��ϴ�. [reddit�� gsg�� ���ұ�][reddit's emacs_lisp_now_lexically_scoped]:

> Dynamic scope�� ��������� ���ڸ� �ѱ��� �ʰ� �ڵ带 ������ �� �ֽ��ϴ�. �̴� ���� ���� ������, ��� �ڵ�� �̷κ��� ���� ���ϴ�.

[kragensitaker�� ���ϱ�][reddit's emacs_lisp_now_lexically_scoped]:

> Thread-local variables, exception handlers, current locale, current clipping region, image transform���� dynamically�ϰ� scope�ϱ⿡ ���� ���Դϴ� .

�׷� ����, **lexical closures** �� �� �� �ִ� ���� ���캾�ô�.

���� �ڵ带 **lexical scoping** ���� �������ô�.

```elisp
(let (c)
  (defun my-get-c ()
    c)
  (defun my-set-c (new-c)
    (setq c new-c))
  (defun my-add-to-c (x)
    (setq c (+ x c))))
```

������ �Լ��� �̿��ϴ� ���� �ڵ带 �������ô�. **lexical scoping** ���� �����ų� �׷��� ���� ������ �����ų� ����� ������, **dynamically scoped** ȯ�濡�� ȣ��� **lexically scoped** �Լ����� ������ **lexically scoped** �Լ��̱� �����Դϴ�.

```elisp
(my-set-c 10)
(my-add-to-c 5)
(print (my-get-c)) ; prints 15.
(my-add-to-c 1)
(print (my-get-c)) ; prints 16
(let ((c 0))
  (print c) ; prints 0
  (print (my-get-c))) ; prints 16.
```

`my-get-c`, `my-set-c`, `my-add-to-c`�� �����ϴ� `c`�� ���� binding��, private ����ó�� �ൿ�ϸ� `(let ((c 0)) ...)`ó�� `c`�� ���� �ٸ� binding�� ���� �������Դϴ�. �̴� ������ `defun` form�� ���δ� `let `form���� ������� `c`�� ���� binding��, �� ������ �Լ��� ������ �����ϰ�� �� �����Ű�� �����Դϴ�.

���� **lexical closure** �� �̿��Ͽ� C������ static ������ �ϴ� ���� �غ��ô�.

```elisp
(require 'cl) ; for incf
(eval
 '(let ((i 0))
    (defun my-counter ()
      (prog1
          i
        (incf i))))
 t)
(my-counter) ; => 0
(my-counter) ; => 1
(my-counter) ; => 2
(let ((i 10))
  (my-counter)) ; => 3
(my-counter) ; => 4
```

�� �ڵ尡 ��� �����ϴ��� ������Ͻô� ���� ����, ���� �ڼ��� �����ڵ尡 �ֽ��ϴ�.

```elisp
(eval
 '(let ((i1 0))
    (defun my-test ()
      (let ((i2 0))
        (prog1
            (list i1 i2)
          (incf i1)
          (incf i2)))))
 t)
(my-test) ; => (0 0)
(my-test) ; => (1 0)
(my-test) ; => (2 0)
```

`my-test`�� �����ϰ� 3�� ȣ���Ͽ����ϴ�. `my-test`�� (`let ((i2 0)) ..)` form�� `my-test`�� ȣ��ɶ����� ����Ǿ� 3�� ȣ��Ǿ����ϴ�. �ݸ�, `(let ((i1 0)) ... )` form�� `my-test`�� ���ǵɶ� �� �ѹ��� ����˴ϴ�. ����Ǽ̱� �ٶ��ϴ�.

���� **lexical closure** �� �Լ��� ��ȯ�ϴ� �Լ��� �׽�Ʈ �غ��ô�.

```elisp
(eval
 '(defun my-get-counter (start step)
    (let ((count start))
      (lambda ()
        (prog1
            count
          (setq count (+ count step)))))
    )
 t)

(setq my-get-even-numbers (my-get-counter 0 2)
      my-get-odd-numbers (my-get-counter 1 2))

(funcall my-get-even-numbers) ; => 0
(funcall my-get-even-numbers) ; => 2
(funcall my-get-even-numbers) ; => 4

(funcall my-get-odd-numbers) ; => 1
(funcall my-get-odd-numbers) ; => 3
(funcall my-get-odd-numbers) ; => 5

(funcall my-get-even-numbers) ; => 6
(funcall my-get-even-numbers) ; => 8

(setq my-get-even-numbers-2 (my-get-counter 0 2))
(funcall my-get-even-numbers-2) ; => 0
(funcall my-get-even-numbers-2) ; => 2
(funcall my-get-even-numbers-2) ; => 4

(funcall my-get-even-numbers) ; => 10
(funcall my-get-even-numbers) ; => 12
(funcall my-get-even-numbers) ; => 14
```

�����е��� �Ƹ� `my-get-even-numbers`, `my-get-odd-numbers`, `my-get-even-numbers-2`�� `�ϳ��� count`�� �����ϴ� ��� �� `�ڱ⸸�� count`�� ������ �ִ��� ȥ�������� �Ͻ����� �𸣰ڽ��ϴ�. �̵��� ������ `�ڽŸ��� count`�� ������ �ֽ��ϴ�. ȥ��������� �������� ����, ���� �ڵ带 **lexical scoping** ���� �����ٸ� ��Եɱ��?

```elisp
(let ((count 0))
  (setq my-count
        (lambda ()
          (prog1
              count
            (setq count (1+ count))))))
(let ((count 0))
  (setq my-count-2
        (lambda ()
          (prog1
              count
            (setq count (1+ count))))))
```

`my-count`�� `my-count-2`�� `�ڱ⸸�� count`�� ���ϰ��ֽ��ϴ�. �� `let` form�� ���� `(setq .. (lambda ...))` forms�� ���ΰ� �ֽ��ϴ�. �̴� ���� `my-get-counter`�� �ϴ� �ϰ� �����ϴ�. `(my-get-counter ..)`�� ����� ������, `(let ((count ..)) (lambda ..))`�� �ٽ� ����Ǹ�, `count`�� ���� �и��� ���ο� binding�� ���� ���ο� �Լ����� ������ �� �ֵ��� ����� �ݴϴ�. `(my-get-counter ..)`�� 3�� �����Ű��, `(let ((count ..)) (lambda ..))`�� 3�� ����Ǿ�, `count`�� ���� 3���� binding�� 3���� ��ȯ �Լ��� �������ϴ�.

`Alice`�� ���� **lexically scopeȯ���� el** ���Ͽ��� ���ο� Emacs Lisp �ڵ带 �ۼ��ϰ��ֽ��ϴ�. `Alice`�� ���ο� �ۼ��� **lexically scoped** �ڵ�� �ٸ��̰� �ۼ��� **dynamically scoped** �ڵ带 ����(interact)�ٸ�, ����� ���������? ���ߴ°� �ƴұ��?

������ ������ �غ��ô�.

```elisp
(eval
 '(defun my-bah ())
 t)

(eval
 '(fset 'my-bah-2 (symbol-function 'my-bah))
 nil)
```

 `my-bah`�Լ��� **lexically scoped** ȯ�濡�� ���ǵǾ����ϴ�. ���� �̴� **lexically scoped** �Լ��� �Ǿ�߸� �մϴ�. �׷��� `my-bah-2`�� �����?

> Alice : "`my-bah-2`�� **dynamically scoped** ȯ�濡�� ���ǵǾ���. ���� �̴� **dynamically scoped** �Լ��� �Ǿ�߸� ��."

> Bob   : "`my-bah-2`�� �Լ� ������ `my-bah`�� �Լ� ����(cell)�� �����߾�. `my-bah`�� �Լ� ������ **lexically scoped** �Լ��� �����ϰ� ����. `my-bah-2`�� �Լ� ������ �ִ� ���� **lexically scoped** �Լ��� ������"

> Alice : "���. �� �Լ����� �ƹ��͵� ���� ���ݾ�. �հ� �� �غ����� ������. ��ȯ������ **lexically scoped**���� �˷��ֵ��� ������."

 ���� �ڵ�� **lexically scoped**ȯ�濡�� `t`��, �׷��� ������ `nil`�� ��ȯ�մϴ�. [���⼭ lexical-binding ���� Ȯ���ϴ� ���� ���� ���� �����Դϴ�][yoo2080's how-to-check-dynamically].

```elisp
(let ((x nil)
      (f (let ((x t)) (lambda () x))))
  (funcall f))
```

Alice�� the my-bah & my-bah-2 �ڵ带 �����߽��ϴ�.

```elisp
(eval
 '(defun my-bah ()
    (let ((x nil)
          (f (let ((x t)) (lambda () x))))
      (funcall f)))
 t)

(eval
 '(fset 'my-bah-2 (symbol-function 'my-bah))
 nil)
```

`my-bah-2`�� **lexically scoped** �Լ����� Ȯ���� ���ô�.

```elisp
(my-bah) ; => t
(my-bah-2) ; => t
```

�׷�, `Bob`�� �����Ѱ� �����ǰ���? �̿� ������, defun�� ������� ���� �ڵ�� �׽�Ʈ�غ��ô�.

```elisp
(eval
 '(setq my-nah
        (lambda ()
          (let ((x nil)
                (f (let ((x t)) (lambda () x))))
            (funcall f))))
 t)

(eval
 '(setq my-nah-2 my-nah)
 nil)

(funcall my-nah) ; => t
(funcall my-nah-2) ; => t
```

 `(setq abc (+ 1 1))`�� ������, ������ ����ϴ� ǥ���� `(+ 1 1)`�� �켱 �򰡵ǰ�, �򰡰�� ���� `2`�� ���� `abc`�� �Ҵ�˴ϴ�. ��ó��, `(setq my-nah (lambda ...))`�� ������, �͸��Լ��� ����ϴ� ǥ���� `(lambda ...`)�� ���� �򰡵˴ϴ�. **lexical scoping** ����, �򰡰���� **lexically scoped** �Լ� ���� `(closure ....)`ó�� ���Դϴ�. �׸��� �� ��� `(closure ....)`�� ���� `my-nah`�� �Ҵ�˴ϴ�.

`(setq abc (+ 1 1))`�� ������ (`setq abc-2 abc)`�� ������, ǥ���� `(+ 1 1)`�� ���� �򰡴� �� �ѹ��� �Ͼ�ϴ�. `(setq abc-2 abc)`�� `(+ 1 1)`�� �Ǵٽ� ������ �ʰ�, ���� �̹� ���� ��� `2`�� `abc-2`�� �����մϴ�. `(setq abc-2 abc)`���� ���� ���� symbol `abc` ��ü�̸�, symbol `abc`�� ���ϸ� `2`�Դϴ�. ��ó��, `my-nah` & `my-nah-2` �����ڵ忡�� `(lambda ...)` ǥ������ �򰡴� �� �ѹ��� �Ͼ��, `(setq my-nah-2 my-nah)`�� ������ ��� `(closure ...)`�� �򰡵��� ������ �ܼ��� `my-nah-2`�� ����˴ϴ�. `(setq my-nah-2 my-nah)`�� **dynamically scoped** ȯ�濡�� ���ư� ����, anonymous function ǥ���Ŀ� ���� �򰡰� **lexically scoped** ȯ�濡�� �߻��ϱ⿡, ���� `my-nah-2`�� �ᱹ **lexically scoped** �Լ��� ���ϰ� �˴ϴ�.

**lexically scoped** �Լ��� ������� **dynamically scoped** ȯ�濡 ���� �ǵ�, �Լ��� ������ **lexically scoped** �Լ��� �����ֽ��ϴ�.

`defun my-bah` ���� �����մϴ�. symbol `my-bah`�� �Լ� ����(cell)�� **lexically scoped** �Լ��� ����ֽ��ϴ�. ���� �׽�Ʈ�� ���캸�ڽ��ϴ�.

```elisp
(print my-nah-2)
(print (symbol-function 'my-bah-2))
```

**lexically scoped el** ���Ͽ��� `defun`�� ������ �ְ�, ���ο��� free variable�� �ش��ϴ� ���� Ȯ���Ϸ���, **dynamically scoped** ���Ͽ� �ִ� �� �ٸ� �̸��� �Լ����, el ���Ͽ��� �� �ֺ��� ���캸�⸸ �ϸ� �˴ϴ�.

���� `my-nah-2` & `my-bah-2` ������ �������� ���Դϴ�. `my-get-counter`�� �ٽ� ���캸���� �ϰڽ��ϴ�. `(defun my-get-counter ...)`�� **lexically scoped el** ���Ͽ� �ִ� ����, `my-get-counter`�� ��ȯ�ϴ� �Լ����� **lexically scoped** �Դϴ�. Ȯ���غ��ô�.

```elisp
(eval
 '(progn
    (setq my-get-even-numbers (my-get-counter 0 2))
    (print (funcall my-get-even-numbers))
    (print (funcall my-get-even-numbers))
    (print (funcall my-get-even-numbers)))
 nil)
```

�̴� `0 2 4`�� ����մϴ�. ���⼭ `Alice`�� �ٽ� "`my-get-even-numbers` �Լ��� **dynamically scoped** ȯ�濡�� ���ǉ��. �׷��� �� **lexically scoped** �Լ�ó�� �ൿ�ϴ� �ž�?" ��� �ǹ��� ǥ������ �𸨴ϴ�. ���� `my-get-even-numbers`�� `my-nah-2`�� ���������� **lexically scoped** �Լ��� ���ϰ� �ֽ��ϴ�. ���ذ� ������ �е��� ����, �켱 `my-get-sum`�� ���캸���� �ϰڽ��ϴ�.

```elisp
(defun my-get-sum (x y)
  (+ x y))
```

`my-get-sum`�� �ִ� ������ ����ϴ� `(+ x y)`�� ǥ�����̸�, `my-get-sum` �� `(+ x y)`�� �򰡰���� ��ȯ����, ǥ���� `(+ x y)`��ü�� ��ȯ������ �ʽ��ϴ�. `(my-get-sum 1 2)`�� �������ٸ�, ǥ���� `(+ x y)`�״�θ� ��ȯ���� �ʰ�, `my-get-sum`�ȿ��� `(+ x y)`�� �򰡵� `3`�� ��ȯ�մϴ�

`my-get-counter`�� ���ư����ô�. `my-get-counter`�� `(lambda ...)`�� �͸� �Լ��� ��Ÿ���� ǥ�����Դϴ�. �� ǥ������ `my-get-counter` ���ο��� �ѹ��� �򰡵˴ϴ�. �򰡰���� ���� `my-get-even-numbers`�� ����� ���� ��ȯ���� `(closure ...)`�Դϴ�. `(lambda ...)`�� �򰡴� �� �ѹ��� �̷������, �̴� **lexically scoped �Լ�** `my-get-counter`���� �̷�����ϴ�. **lexically scoped** �Լ������� `lambda` form�� �򰡴� �׻� `(closure ...)`�� �˴ϴ�. �̰��� �ٷ� ��� `my-get-even-numbers`�� **lexically scoped** �Լ��� ���Ҽ� �ִ����� ���� �����Դϴ�.

�װ� �׷���, ��°������ ������ `lambda` form�� �򰡸� ���ƹ����ٸ�, **lexically scoped** �Լ��� **dynamically scoped** �Լ��� �����ϰ� ��ȯ�� �� �ֽ��ϴ�.

```elisp
(eval
 '(defun my-return-dynamically-scoped-function ()
    (list 'lambda '() 'a)
    )
 t)

(eval
 '(defun my-return-dynamically-scoped-function ()
    '(lambda () a) ; quoted lambda
    )
 t)
```

�� �̷��� �ߴ���, �ǵ��� �� �𸣰�����, ��¶�� �����մϴ�.

���� `my-call` ���� �ٽ� ���캸���� �ϰڽ��ϴ�.

```elisp
(eval
 '(defun my-call (f n)
    (funcall f n))
 nil)

(eval
 '(dolist (n (list 1 2 3))
    (print
     (my-call (lambda (x) (* n x)) 5)))
 t)
```

�̴� `5 10 15`�� ����մϴ�. `Alice`�� �ٽ� ���ϱ� "�Լ� `f`�� **dynamically scoped**���� ���ǵǾ��ݾ�. �׷��� �� **lexically scoped** �Լ�ó�� �ൿ�ϴ� �ž�?" `my-call`�� ���� �͸��Լ����� **lexically scoped** ȯ�濡�� ���ǵǾ��⿡, `my-call`�� ���� �Ķ� **lexically scoped** ó�� ���¸� �����մϴ�. �׷��� ���ذ� ������ �е��� ���ؼ�. `(lambda ...)`�� �򰡵ǰ� �� ����� `my-call`�� �����ϴ�. `my-call`�� �� ����� **��������(local variable)** `f`�� �����߽��ϴ�. ���� `f`�� **lexically scoped** �Լ��� �����ϰ� �˴ϴ�.

`mapcar*` �Լ��� �Լ��� ���ڷ� �ް�, **dynamically scoped el** ���Ͽ��� ���ǵǾ��ٴ� ������ `my-call`�� ����մϴ�. ���� **dynamic scoping** ������ [StackOverflow �亯]���� ���� ���Դϴ�.

```elisp
(let ((cl-x 10))
  (mapcar* (lambda (elt) (* cl-x elt)) '(1 2 3)))
```

 name `cl-x`�� `mapcar*`�� ���ǿ��� argument name���� ���˴ϴ�. ���� **dynamically scoped** ȯ�濡�� �� �ڵ带 ������ ��¦ ���� �� ���Դϴ�(�߰��Ѱ� 1). ������ **lexically scoped** ȯ�濡�� �ڵ带 ������, ���������� �����ϴµ� `mapcar*`�� ���� **lexically scoped** �͸� �Լ��� ������ **lexically scoped** �Լ��� �����ϱ� �����Դϴ�.

�� ������ ����, **lexically scoped** �ڵ尡 �� ��︮�°� �����ϴ�. ���� **lexical scoping** �� ��ⷯ ������ �ð��Դϴ�!


 [file variables]: http://www.gnu.org/software/emacs/manual/html_node/emacs/File-Variables.html
 [function cell]: http://www.gnu.org/software/emacs/manual/html_node/elisp/Function-Cells.html
 [yoo2080's how-to-check-dynamically]: http://yoo2080.wordpress.com/2011/12/30/how-to-check-dynamically-if-lexical-scoping-is-active-in-emacs-lisp/
 [reddit's emacs_lisp_now_lexically_scoped]: http://www.reddit.com/r/programming/comments/ggmc2/emacs_lisp_now_lexically_scoped_oh_very_funny_no/c1nfngv
 [StackOverflow �亯]: http://stackoverflow.com/a/3791877/37664