�ܾ��� "�ǹ�"�� ���̼�.
=========================================================================

```��
�����


���� ���� �̸��� �ҷ� �ֱ� ������
�״� �ٸ�
�ϳ��� ������ ������ �ʾҴ�.

���� ���� �̸��� �ҷ� �־��� ��
�״� �����Է� �ͼ�
���� �Ǿ���.

���� ���� �̸��� �ҷ� �� ��ó��
���� �� ����� ���(��Ѩ)�� �˸´�
���� ���� �̸��� �ҷ��ٿ�.
�׿��Է� ���� ����
���� ���� �ǰ� �ʹ�.

�츮���� ���
������ �ǰ� �ʹ�.
�ʴ� ������ ���� �ʿ���
�������� �ʴ� �ϳ��� �ǹ̰� �ǰ� �ʹ�.

<���� �ҹ�(����), ���ڻ�, 1959>
```


# ����.
��ü��
* send  : deliver, dispatch, announce, distribute, route
* find  : search, extract, locate, recover
* start : launch, create, begin, open
* make  : create, set up, build, generate, compose, add, new

# ������ �������(����ģ ������ ����)
* tmp => tmp_file

* `i,j,k`�� ������? `ci, mi, ui`�� ������?

```cpp
for (int i = 0; i < clubs.size(); i++)
    for (int j = 0; j < clubs[i].members.size(); j++)
        for (int k = 0; k < users.size(); k++)
            if (clubs[i].members[k] == users[j])
                cout << "user[" << j << "] is in club[" << i << "]" << endl;
```

* ThrottleDownload(float limit) limit => max_kbps
* password => plaintext_password

# ������ ����?
* ������ ���Ǵ� �󵵼��� �°� ����.

# ��ġ�� ����Ģ
```note
[1,2,3,4,5][]
```
* first : 1
* last  : 5
* begin : 1
* end   : []


# �οﰪ(��, ������� __������__���Ұ�)
is, has, can, should 

# �ּ�
* TODO: �Ӹ� �ؾߵ�.
* FIXME: ���� ��������.
* HACK: ������� ������ ���ư��� ����.
* BOOM: �ǵ�� �����Ͱ��� �ڵ�.
* ref: ���۷���

# �ּ�
```cpp
// Force vector to relinquish its memory (look up "STL swap trick")
vector<float>().swap(data);
```

```cpp
// bad
// Return the number of lines in this file.
int CountLines(string filename) { ... }
// ? "" (an empty file)?0 or 1 line?
// ? "hello"?0 or 1 line?
// ? "hello\n"?1 or 2 lines?
// ? "hello\n world"?1 or 2 lines?
// ? "hello\n\r cruel\n world\r"?2, 3, or 4 lines?

// good
// Count how many newline bytes ('\n') are in the file.
int CountLines(string filename) { ... }
```


```cpp
// Example: Partition([8 5 9 8 2], 8) might result in [5 2 | 8 9 8] and return 1
```