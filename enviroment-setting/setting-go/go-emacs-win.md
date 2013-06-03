 Emacs�� �̿��� Go ȯ�漳�� - Windows��.
====================================


----------------------------------
# Go ȯ�漳��
----------------------------------

## ��ǥ
 - 30�оȿ�, go "�ڵ�ȯ�� ����".

## ȯ��
 - Windows8-64bit

### go
- Go�� ������ ������ ������ �÷��� ����� �ִ� ������, ���༺(concurrent) ���α׷��� ����̴�. -  [wiki:Go_(���α׷��־��)](http://ko.wikipedia.org/wiki/Go_%28%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D_%EC%96%B8%EC%96%B4%29)

    ![go-character](http://golang.org/doc/gopher/frontpage.png)

- ���Ļ���Ʈ : [lang:go](http://golang.org/)
- ���� : [An Introduction to Programming in Go](http://www.golang-book.com/)
- ������ : [Go by Example](https://gobyexample.com/)

## Go ��ġ
- [go:download_list](http://code.google.com/p/go/downloads/list)�� ����,
- Windows (x86 64-bit) MSI installer Featured �ٿ�ε�

## ȯ�溯��
- ȯ�溯�� �߰��� [rapidee](http://www.rapidee.com/en/)�� �̿��ϸ� ���ϴ�.
- ������ �߰�������.
 - `PATH` : git.exe�� �ִ� ��ġ. `C:\Program Files (x86)\Git\cmd\`
 - `GOPATH` : go�� ��ġ�� ��ġ. `C:\Go\`

## gocode ��ġ
- [gocode](https://github.com/nsf/gocode)�� ��ġ�ҷ��� [git](http://msysgit.github.io/)�� ��

> go get -u github.com/nsf/gocode

## emacs ��ġ
- [kaist-ftp:emacs](http://ftp.kaist.ac.kr/gnu/gnu/emacs/windows/)���� �ٿ�ε�.

## emacs ȯ�漳��
* `~/.emacs.d/init.el` �� ������ �߰�������.
 - emacs�� �ѹ� ����Ű��, `~/.emacs.d/`������ ����(�� `~`�� `HOME`������)

````lisp
;; [== packages ==]
(package-initialize)
(setq package-archives
      '(
	("ELPA" . "http://tromey.com/elpa/")
	("gnu" . "http://elpa.gnu.org/packages/")
	("marmalade" . "http://marmalade-repo.org/packages/")
	("melpa" . "http://melpa.milkbox.net/packages/")
	))
````

* `M-x load-file`�� �ѵ�,  `~/.emacs.d/init.el`
* `M-x list-packages`�� �� ��, `init-loader`, `auto-complete`, `quickrun`, `auto-complete`, `go-autocomplete`�� ��ġ������.
* `~/.emacs.d/init.el`�� ������ �߰�������.

````lisp
;; [== init-loader ==]
(require 'init-loader)
(init-loader-load "~/.emacs.d/conf.d/")
```

* `~/.emacs.d/conf.d/0000_go.el`�� ������ �߰�������.

```lisp
(require 'auto-complete)
(require 'go-autocomplete)
(require 'auto-complete-config)

(add-hook 'go-mode-hook 'auto-complete-mode)
```


## Ȯ��.
* auto-complete Ȯ�� : emacs�� ����Ű��, `test.go`���� ��� �ڵ��ϼ��� �Ǹ� ����.
* quickrun Ȯ�� : ������ �Է��ϰ�, `F7`�� ����, `Hello World`�� ��µǸ� ����.

```go
package main

import "fmt"

func main() {
	fmt.Println("Hello World")
}
```
