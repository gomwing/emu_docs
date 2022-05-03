"# emu_docs" 

[����] ��ũ�ٿ� markdown �ۼ���
======================

# 1. ��ũ�ٿ ���Ͽ�
## 1.1. ��ũ�ٿ��̶�?
[**Markdown**](http://whatismarkdown.com/)�� �ؽ�Ʈ ����� ��ũ������ 2004�� ���׷���� ���� ����������� ���� ���� ���� �� ������ HTML�� ��ȯ�� �����ϴ�. Ư����ȣ�� ���ڸ� �̿��� �ſ� ������ ������ ������ ����Ͽ� �������� ���� ������ �������� �ۼ��ϰ� ���� ���������� �ν��� �� �ִ�.
��ũ�ٿ��� �ֱ� �����ޱ� ������ ������ ����([https://github.com](https://github.com)) �����̴�. ������ �����Repository�� ���� ������ ����ϴ� README.md�� ������ ����ϴ� ����̶�� ������ ���� ���� ���ϰ� �Ǵ� ��ũ�ٿ� ��������. ��ũ�ٿ��� ���ؼ� ��ġ���, �ҽ��ڵ� ����, �̽� ���� �����ϰ� ����ϰ� �������� ���� �� �ִٴ� ������ �ΰ��Ǹ鼭 ���� ���� ������ �������� �ȴ�.

## 1.2. ��ũ�ٿ��� ��-����
### 1.2.1. ����
	1. �����ϴ�.
	2. ������ �������� �ۼ������ϴ�.
	3. �پ��� ���·� ��ȯ�� �����ϴ�.
	4. �ؽ�Ʈ(Text)�� ����Ǳ� ������ �뷮�� ���� ������ �����ϴ�.
	5. �ؽ�Ʈ�����̱� ������ ���������ý����� �̿��Ͽ� �����̷��� ������ �� �ִ�.
	6. �����ϴ� ���α׷��� �÷����� �پ��ϴ�.

### 1.2.2. ����
	1. ǥ���� ����.
	2. ǥ���� ���� ������ ������ ���� ��ȯ����̳� �������� �ٸ���.
	3. ��� HTML ��ũ���� ������� ���Ѵ�.

****
# 2. ��ũ�ٿ� ����(����)
## 2.1. ���Headers
* ū����: ���� ����
    ```
    This is an H1
    =============
    ```
    This is an H1
    =============

* ��������: ���� ������
    ```
    This is an H2
    -------------
    ```
    This is an H2
    -------------

* �۸Ӹ�: 1~6������ ����
```
# This is a H1
## This is a H2
### This is a H3
#### This is a H4
##### This is a H5
###### This is a H6
```
# This is a H1
## This is a H2
### This is a H3
#### This is a H4
##### This is a H5
###### This is a H6
####### This is a H7(�������� ����)

## 2.2. BlockQuote
�̸��Ͽ��� ����ϴ� ```>``` ���ο빮�ڸ� �̿��Ѵ�.
```
> This is a first blockqute.
>	> This is a second blockqute.
>	>	> This is a third blockqute.
```
> This is a first blockqute.
>	> This is a second blockqute.
>	>	> This is a third blockqute.

�� �ȿ����� �ٸ� ��ũ�ٿ� ��Ҹ� ������ �� �ִ�.
> ### This is a H3
> * List
>	```
>	code
>	```

## 2.3. ���
### �� �����ִ� ���(��ȣ)
�����ִ� ����� ���ڿ� ���� ����Ѵ�.
```
1. ù��°
2. �ι�°
3. ����°
```
1. ù��°
2. �ι�°
3. ����°

**��������� � ��ȣ�� �Է��ص� ������ ������������ ���ǵȴ�.**
```
1. ù��°
3. ����°
2. �ι�°
```
1. ù��°
3. ����°
2. �ι�°

���� ������ �� ������ �ʴ�. �� �׷���� �Ű�Ⱦ��� �ִٰ�...

### �� �������� ���(�۸Ӹ� ��ȣ: `*`, `+`, `-` ����)
```
* ����
  * ���
    * �Ķ�

+ ����
  + ���
    + �Ķ�

- ����
  - ���
    - �Ķ�
```
* ����
  * ���
    * �Ķ�

+ ����
  + ���
    + �Ķ�

- ����
  - ���
    - �Ķ�

ȥ���ؼ� ����ϴ� �͵� �����ϴ�(���� ��ȣ�ϴ� ���)

```
* 1�ܰ�
  - 2�ܰ�
    + 3�ܰ�
      + 4�ܰ�
```

* 1�ܰ�
  - 2�ܰ�
    + 3�ܰ�
      + 4�ܰ�

## 2.4. �ڵ�
4���� ���� �Ǵ� �ϳ��� ������ �鿩���⸦ ������ ��ȯ�Ǳ� �����Ͽ� �鿩���� ���� ���� ���������� ��ȯ�� ��ӵȴ�.

### 2.4.1. �鿩����
```
This is a normal paragraph:

    This is a code block.
    
end code block.
```

������ �����غ���,

���뿹:

*****
This is a normal paragraph:

    This is a code block.

end code block.
*****

> ���� ���� ������ �ν��� ����� �ȵǴ� ������ �߻��մϴ�.

```
This is a normal paragraph:
    This is a code block.
end code block.
```

���뿹:

*****
This is a normal paragraph:
    This is a code block.
end code block.
*****

### 2.4.1. �ڵ��
�ڵ���� ������ ���� 2���� ����� ����� �� �ֽ��ϴ�:

* `<pre><code>{code}</code></pre>` �̿���

```
<pre>
<code>
public class BootSpringBootApplication {
  public static void main(String[] args) {
    System.out.println("Hello, Honeymon");
  }

}
</code>
</pre>
```

<pre>
<code>
public class BootSpringBootApplication {
  public static void main(String[] args) {
    System.out.println("Hello, Honeymon");
  }
}
</code>
</pre>

* �ڵ���ڵ�("\```") �� �̿��ϴ� ���

<pre>
<code>
```
public class BootSpringBootApplication {
  public static void main(String[] args) {
    System.out.println("Hello, Honeymon");
  }
}
```
</code>
</pre>

```
public class BootSpringBootApplication {
  public static void main(String[] args) {
    System.out.println("Hello, Honeymon");
  }
}
```

**����**������ �ڵ���ڵ�("\```") �������� ����ϴ� �� �����Ͽ� [��������(Syntax highlighting)](https://docs.github.com/en/github/writing-on-github/creating-and-highlighting-code-blocks#syntax-highlighting)�� �����ϴ�.

<pre>
<code>
```java
public class BootSpringBootApplication {
  public static void main(String[] args) {
    System.out.println("Hello, Honeymon");
  }
}
```
</code>
</pre>

```java
public class BootSpringBootApplication {
  public static void main(String[] args) {
    System.out.println("Hello, Honeymon");
  }
}
```


## 2.5. ���� ```<hr/>```
�Ʒ� ���� ��� ������ �����. ��ũ�ٿ� ������ �̸������ ����� �� *������ ������* �뵵�� ���� ����Ѵ�.

```
* * *

***

*****

- - -

---------------------------------------
```

* ���뿹
* * *

***

*****

- - -

---------------------------------------


## 2.6. ��ũ
* ������ũ

```
[link keyword][id]

[id]: URL "Optional Title here"

// code
Link: [Google][googlelink]

[googlelink]: https://google.com "Go google"
```

Link: [Google][googlelink]

[googlelink]: https://google.com "Go google"

* �ܺθ�ũ
```
��빮��: [Title](link)
���뿹: [Google](https://google.com, "google link")
```
Link: [Google](https://google.com, "google link")

* �ڵ�����
```
�Ϲ����� URL Ȥ�� �̸����ּ��� ��� ������ �������� ��ũ�� �����Ѵ�.

* �ܺθ�ũ: <http://example.com/>
* �̸��ϸ�ũ: <address@example.com>
```

* �ܺθ�ũ: <http://example.com/>
* �̸��ϸ�ũ: <address@example.com>

## 2.7. ����
```
*single asterisks*
_single underscores_
**double asterisks**
__double underscores__
~~cancelline~~
```

* *single asterisks*
* _single underscores_
* **double asterisks**
* __double underscores__
* ~~cancelline~~

> ```���� �߰��� ����� ��쿡�� **����** �� ����ϴ� ���� ����.```   
> ���� �߰��� ����� ��쿡�� ���⸦ ����ϴ� ���� ����.


## 2.8. �̹���
```
![Alt text](/path/to/img.jpg)
![Alt text](/path/to/img.jpg "Optional title")
```
![����ȣ�� ������](http://cfile6.uf.tistory.com/image/2426E646543C9B4532C7B0)
![����ȣ�� ������](http://cfile6.uf.tistory.com/image/2426E646543C9B4532C7B0 "RubberDuck")

������ ���� ����� ���� ������ ```<img width="" height=""></img>```�� �̿��Ѵ�.

��
```
<img src="/path/to/img.jpg" width="450px" height="300px" title="px(�ȼ�) ũ�� ����" alt="RubberDuck"></img><br/>
<img src="/path/to/img.jpg" width="40%" height="30%" title="px(�ȼ�) ũ�� ����" alt="RubberDuck"></img>
```

<img src="http://cfile6.uf.tistory.com/image/2426E646543C9B4532C7B0" width="450px" height="300px" title="px(�ȼ�) ũ�� ����" alt="RubberDuck"></img><br/>
<img src="http://cfile6.uf.tistory.com/image/2426E646543C9B4532C7B0" width="40%" height="30%" title="%(����) ũ�� ����" alt="RubberDuck"></img>

## 2.9. �ٹٲ�
3ĭ �̻� ����(` `)�� �ϸ� ���� �ٲ��.

```
* �� �ٲ��� �ϱ� ���ؼ��� ���� ���������� 3ĭ�̻��� �����ؾ� �Ѵ�. 
�̷���

* �� �ٲ��� �ϱ� ���ؼ��� ���� ���������� 3ĭ�̻��� �����ؾ� �Ѵ�.___\\ ����
�̷���
```

* �� �ٲ��� �ϱ� ���ؼ��� ���� ���������� 3ĭ�̻��� �����ؾ� �Ѵ�. �̷���

* �� �ٲ��� �ϱ� ���ؼ��� ���� ���������� 3ĭ�̻��� �����ؾ� �Ѵ�.    \
�̷���


****
# 3. ��ũ�ٿ� ����
## 3.1. ������(WSYWIG) ������
�츮�� ���ϰ� ���ϴ� ������ ���Ǵ� ������(���̹�, ����, ���� ��)�� ��κ� ������ �����Ϳ� ���ϸ� �⺻������ HTML�� �̿��Ͽ� ��Ÿ���� �����Ͽ� ������ �ٹ̴� ���¸� ���ϰ� �ȴ�. �׷��� �Ϸ��е�� ���� ��ũ�ٿ� �������� View ������ ������ �����Ͽ� �ٿ��ֱ⸦ �ϸ� ��ü������ View�������� ���̴� �״�� ����Ǵ� ���̴�. �ٸ�, �ٿ��ֱ� ���Ŀ� ������� �����Ϸ��� �� �� ������ �Ǵµ�, �̴� ��Ÿ���� ���Ե� �±װ� ������������ �����Ǹ鼭 ��ü���� ������ ��ġ�� ſ�̴�. Ƽ���丮 ��α׿����� ���� �ʰ�... ������������ ��쿡�� ��ũ�ٿ����� �ۼ��� ����Ʈ�� HTML�� ��ȯ���ִ� ����� Ȱ���ϴ� ���� ����.
�����, **�����ؼ� �ٿ��ֱ��ϸ� �������̸� ������ �������� �ʴ� ���� ����.**

## 3.2. ����Github, ��Ʈ��ŶBitbucket�� ���Yobi ��
�ֱ� �����ϴ� ���������÷����� ��쿡�� ��ũ�ٿ��� ��ȯ�ϴ� ������ ����� �⺻ž���ϰ� �ֱ� ������ ��ũ�ٿ� �������� �ۼ��� �ؽ�Ʈ�� �״�� �����ؼ� �ٿ��ְų� ���ε��ϴ� �͸����� ��ũ�ٿ��� ������ �����ϴ�.

## 3.3. MS���� ����
View ������ �׸��� �״�� �ٿ��ְų� HTML �������� ������ ������ ������ �ҷ����� ���·� ��밡���ϴ�. ������ ����� ���尡 �о�帮�鼭 ������ �����ϱ� ������ �̸� Ȱ���ϸ� ���������� �ս��� ������ ����������.

*****

# 4. ����
��ũ�ٿ��� �⺻������ �˰��ִٸ� �Ϲ� �ؽ�Ʈ�����⿡���� �ս��� �ۼ��� ������ ��ũ������. ���� �پ��� ������ �÷������� �����ϰ� �ֱ� ������ ���� �ս��� ��Ÿ������� ������ �ۼ��� �� �־� ���� �θ� ���ǰ� �ִ�.   

> ��ũ�ٿ��� �����ϰ� ����ϸ鼭 ���� ������ ��Ÿ�Ϲ����� �ۼ��غ�����.

���� Dropbox ���θ� �����ؼ� ��-��ž-����Ʈ���� ���� ������ ���Ѽ� ����ϰ� �ֽ��ϴ�. ����ڽ��� ����� ��ũ�ٿ� ������ Dropbox ������ �󿡼� �����ϱ� ������ ���󿡼� �ٷ� ������ ���� �־� ��ũ�� �ɾ �ٸ� ����� �����ϴ� �������� ����ϰ� �ִ�.
* ��ũ ��: [Markdown ����](https://www.dropbox.com/s/mzp9tq4qtfjdlif/20141021_markdown_use_tip.md?dl=0)

***** 

# P.S.
�ֱٿ��� [Notion](https://www.notion.so/product) �� ���ݾ� ������̴�. Notion ���� �ۼ��� ������ Atom(<https://atom.io/>), Visual Studio Code(<https://code.visualstudio.com/>), Notepad++(<https://notepad-plus-plus.org/>)�ؽ�Ʈ �����⿡ ����(�����ϰ� �ٿ��ֱ�)�ϸ� ��ũ�ٿ������ �ۼ��� ������ ���Եǰ� ������ �����͸� �����ϴ� �������Ϳ� �ٿ��ֱ� �ϸ� ���� �Ϻ��� ���·� ����ȴ�. �׷��� �ֿ����̴�.

## �� ������
* [78 Tools for writing and previewing Markdown](http://mashable.com/2013/06/24/markdown-tools/)
* [John gruber ��ũ�ٿ� ����](http://nolboo.github.io/blog/2013/09/07/john-gruber-markdown/)
* [����� ������ ��ũ�ٿ� ����](http://nolboo.github.io/blog/2014/03/25/github-flavored-markdown/)
* [��ϸ��� ��ũ�ٿ� �ۼ���](http://www.slideshare.net/ihoneymon/ss-40575068)
* Notion.so(<https://www.notion.so/product>)
* Atom(<https://atom.io/>)
* Visual Studio Code(<https://code.visualstudio.com/>)
* Notepad++(<https://notepad-plus-plus.org/>)