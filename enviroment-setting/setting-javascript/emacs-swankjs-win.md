��ġ�� ȯ��

nodejs v0.10.5 - 64bit
windows 8 - 64bit

# �����ڷ�
 - [node.js�� �����ΰ�? #1]
 - [github swank-js]
 - [connect to nodejs and chrome from emacs]
 - [emacsrocks e11]

# nodejs && npm��ġ
http://nodejs.org/download/ ���� ��ġ������ �ٿ� �޴´�.

# swank-js��ġ
cmdâ�� ���� `npm install -g swank-js`�� swank-js�� ��ġ���ش�.


# emacs����

```elisp
;; [== packages ==]
(package-initialize)
(setq package-archives
      '(
	("ELPA" . "http://tromey.com/elpa/")
	("gnu" . "http://elpa.gnu.org/packages/")
	("marmalade" . "http://marmalade-repo.org/packages/")
	("melpa" . "http://melpa.milkbox.net/packages/")
	))
```

`M-x package-list`���� ������ ��ġ������
- js2-mode
- swank-js


# �������� emacs��������ֱ�.
- emacs�󿡼� `M-x slime-connect`�� Host: `127.0.0.1`, Port: `4005`�� ����.
- �������� ����� http://127.0.0.1:8009/swank-js/test.html �� �̵�.
- emacs�󿡼� `,`��, Command: `select-remote`, Remote: `��������`

�����ϴ��� �׽�Ʈ.

```
Remote selected: (browser) Firefox20.0
NODE> alert("test!")
undefined
FIREFOX-20.0> 
```

# .js���Ͽ��� �ٷ� eval�ϰ� �ʹٰ�?
- js������ �ƹ��ų� ����, 
- major�� `M-x js2-mode` ���ְ�,
- minor�� `M-x slime-js-minor-mode`�� ������.

 [nodejs]: http://nodejs.org/download/
 [node.js�� �����ΰ�? #1]: http://blog.outsider.ne.kr/480?category=42
 [github swank-js]: https://github.com/swank-js/swank-js
 [connect to nodejs and chrome from emacs]: http://e-arrows.sakura.ne.jp/2011/06/connect-to-nodejs-and-chrome-from-emacs.html
 [emacsrocks e11]: http://emacsrocks.com/e11.html