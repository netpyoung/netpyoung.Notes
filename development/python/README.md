BACKUP

http://www.python.org/

pypy - http://pypy.org/

 

package manager

http://packages.python.org/distribute/

http://doc.pypy.org/en/latest/getting-started.html#installing-pypy (for pypy)

 

clojure-py

https://github.com/halgari/clojure-py

 

emacs-for-python

https://github.com/gabrielelanaro/emacs-for-python

    for windows excute : https://bugs.launchpad.net/pyflakes/+bug/794331

 

Attest

http://packages.python.org/Attest/

 

Python�� ����� �ϴ� ����
http://kldp.org/node/77727

--------------------------------------------------------------------------------



```
�ѱ� ó��

�ҽ� �ֻ�ܿ�  >>> # -*- coding: euc-kr -*-

 

>> a = "Python"
>> print(a)
>> print("i eat %d apples. so i was %s" %(number, day))

 

���Ό��
>>> import sys
>>> sys.exit()

 

���� : ��ҹ��� ����, �̸�ũ�� �������.
ù���ڿ� ���ڳ� Ư����ȣ ���Ұ�, ����� ���Ұ�(Ȯ���Ϸ��� import keyword�� keyword.kwlist)

 

����Ʈ
����Ʈ�� '[' �� ']' ���� �ѷ��Ѵ�
����Ʈ�� ���� ����, ����, ������ �����ϴ�
listName[start:end:step]
>>> a = [1,2,3]
>>> b = a // == >>> b = a[:]
>>> a[::-1]
[3, 2, 1]
>>> a[::2]
[1, 3]
>>>

 

����
������ '('�� ')'���� �ѷ��Ѵ�.
������ ���� ��ȭ��ų �� ����.
�޸�(,)�� �����ϸ� Ʃ���� �ƴ϶� �ܼ��� ���������� ���ǵȴ�.

 

��ųʸ�(�� ����)
, Key�� Value�ֵ��� �������� '{'�� '}'���� �ѷ��ο��ִ�.
 ������ ��Ҵ� Key : Value���·� �̷���� �ְ� ��ǥ(',')�� ���еǾ��� �ִ�.
����� �ߺ��Ǵ� Key�� ������� ����.
Key�� ����Ʈ�� �� ���� ����
.keys(), .values(), .items()

 

pass : ���ǹ����� �ƹ��� �ൿ�� ���ϰ� ���� ��

 

number = int(input(""))

>>> test_list = ['one', 'two', 'three']
>>> for i in test_list:
...     print i

a = [(1,2), (3,4), (5, 6)]
for (first, last) in a:
    print(first+last)

 

�Է°��� �� ���� �� �� �� ��
>>> def sum_many(*args):
. . .     sum = 0
. . .     for i in args:
. . .         sum = sum + i
. . .     return sum

�ʱ�ȭ ��Ű�� ���� �Է� �������� �׻� ���ʿ� ��ġ���Ѿ� ��


���ڿ� ����� �޸���

print("Hellow")
print("Hellow", end = '')

==================================================

sys ���
#sys1.py
import sys

args = sys.argv[1:]
for i in args:
    print i

sys.path
sys.path.append

reload(���)
import ��� (��� ��ü�� �ҷ��´�.)
from ��� import ������ �Լ�(��⿡�� �ʿ��� �͵鸸 �ҷ��´�.)
==================================================
# -*- encoding: euc-kr -*-

class Service:
    secret = "������ ����� �ΰ���."

pey = Service();
print(pey.secret)
==================================================
Ŭ�������� �Լ��� ù��° ���ڴ�
"������ self�� ����� �ؾ� �ν��Ͻ��� �Լ��� ����� �� �ִ�."
(this�� ����� ����)
==================================================
���
>>> class HouseKim(HousePark):
. . .      lastname = "�衰
==================================================


__init__     ������(Constructor), �ν��Ͻ��� ����� �� �� ȣ��     

__del__     �Ҹ���(Destructor) �ν��Ͻ��� ����� �� ȣ��     

 __add__     ������ "+"     X + Y
__or__     ������ "|"     X | Y
__repr__     print     print X
__call__     �Լ�ȣ�� X()���� �� ȣ��     
__getattr__     �ڰݺο�     X.�޼ҵ�
__getitem__     �ε���     X[i]
__setitem__     �ε��� ġȯ     X[key] = value
__getslice__     �����̽�     X[i:j]
__cmp__     ��     X > Y

===================================================
���� �����ϸ� �۵�, ��ȭ�� ���������ͳ� �ٸ� ��⿡�� �ҷ��ö� �۵�����.
if __name__ == "__main__":

 

 

import [module]
from [module] import [module function]

if __name__ == "__main__":

try
    ...
except [�߻�����][,�����޽�������]:
    ...


=====================================
����ó���ϱ�

try:
    ...
except [�߻�����[, �����޽�������]]:
    ...

=====================================
���� �߻���Ű��
raise
=====================================
�����Լ�
abs, chr
>>> pow(2,4)
16 (2�� 4��)
=====================================
lambda �μ�1, �μ�2,,, : �μ��� �̿��� ǥ����
>>> l = [lambda a,b:a+b, lambda a,b:a*b]
>>> l
[at 0x811eb2c>, at 0x811eb64>]
>>> l[0]
at 0x811eb2c>
>>> l[0](3,4)
7
>>> l[1](3,4)
12
======================================
map
>>> def two_times(x): return x*2
. . .
>>> map(two_times, [1,2,3,4])
[2, 4, 6, 8]
>>> map(lambda a: a*2, [1,2,3,4])
[2, 4, 6, 8]
def plus_one(x):
    return x+1
print(map(plus_one, [1,2,3,4,5]))
======================================
repr(object)�� ��ü�� ����� �� �ִ� ���ڿ� ���·� ��ȯ�Ͽ� �����ִ� �Լ�
======================================
str(object)�� ��ü�� ����� �� �ִ� ���ڿ� ���·� ��ȯ�Ͽ� �����ִ� �Լ��̴�. �� ���ڿ� �� ��ü�θ� �����ִ� �Լ��̴�.
======================================

zip �Լ��� ������ ������ ��Ұ��� ���� ������ �ڷ����� �����ִ� ������ �Ѵ�.

 

import sys


atoi
atof

zfill
 
```