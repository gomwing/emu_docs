

windows bash ���� devkitARM �����ϱ�
=================================

�Ŵ����� �ϰ��� bash shell ���� mingw32�� ��ġ�ؼ� windows �� binary�� �����ؾ� �Ѵ�.

https://marc.xn--wckerlin-0za.ch/computer/cross-compile-on-ubuntu-linux-for-windows-using-mingw

~~~
sudo apt-get install mingw-w64
~~~

�̻��¿����� mingw-w64���� gcc�� �ʿ��� 3���� ���̺귯���� ����.

GMP
---
~~~
wget https://gmplib.org/download/gmp/gmp-6.1.2.tar.bz2
./configure  --host=x86_64-w64-mingw32 --prefix=/usr/x86_64-w64-mingw32/
make
sudo make install
<<- �̰� �� ��� gmp.h �� x86_64-w64-mingw32 �� include�� ����.
~~~

MPFR
----
~~~
wget https://www.mpfr.org/mpfr-current/mpfr-4.0.2.tar.bz2
./configure  --host=x86_64-w64-mingw32 --prefix=/usr/x86_64-w64-mingw32/ --enable-static --disable-shared
make
sudo make install
~~~

MPC
---

~~~
wget https://ftp.gnu.org/gnu/mpc/mpc-1.1.0.tar.gz
./configure  --host=x86_64-w64-mingw32 --prefix=/usr/x86_64-w64-mingw32/ --enable-static --disable-shared
make
sudo make install
~~~

�̷��� 3���� ��ġ�� �� 

cross-build-x86_64-w64-mingw32.sh 

��


~~~
#!/bin/bash
export CROSSBUILD=x86_64-w64-mingw32
export CROSSPATH=/usr/x86_64-w64-mingw32
export CROSSLIBPATH=$CROSSPATH/lib
export CROSSBINPATH=/usr/bin
~~~


�̷��� ��ġ��. ������ �ϴ� �ȵǾ���. ��.��

�̰� ���.. zlib

ZLIB 
----
### ũ�ν� �������� ���ؼ� ����  

������ ���̺귯���� �׷��� --host= �� ������ �ȸԴ´� 

```
wget https://zlib.net/zlib-1.2.11.tar.xz
CHOST=x86_64-w64-mingw32 ./configure --prefix=/usr/x86_64-w64-mingw32 --static
make
sudo make install
```

�̷��� �ؼ� zlib.h�� ��ġ���� 

***

~~�Ʒ��� ����� ���ͳݿ� �����ִ°��ε� bash shell ������ �ȵȴ�. 
�ȵǹǷ� ��������.
�������� �ȵȴ�-> �ƴϴ� ���� ������� �ȴ�.. zlib���� win32/Makefile.gcc�� �����ؾ� �Ѵ�.
PREFIX =  
�̷��� �� ����
PREFIX = x86_64-w64-mingw32-
�̷��� �ٲ���
make -f win32/Makefile.gcc BINARY_PATH=/usr/bin INCLUDE_PATH=/usr/x86_64-w64-mingw32/include LIBRARY_PATH=/usr/x86_64-w64-mingw32/lib install
�� �����ѵڿ� ���̺귯�� �ν���~~

***
���� ������
===

```
. cross-build-x86_64-w64-mingw32.sh 
```

<- ������ ��ũ��Ʈ�� sub envioment�� �ƴ� ������ enviroment�� �ݿ��ϰ� ����

~~~
./build-devkit.sh�� ��������ϸ� ��!!!
~~~

���⼭ �ν��� ���丮�� `:` �� ������ ������ ���Ƿ� 

```
Please enter the directory where you would like 'devkitARM' to be installed:
for mingw/msys you must use <drive>:/<install path> or you will have include path problems
this is the top level directory for devkitpro, i.e. e:/devkitPro
```
�� ������ ������ 

```
/f/_DEVELOP_/devkitPro 
```
�̷��� �� ��� �Ѵ�.

�߰��۾�
---

### 1. gp32-tools ���� ���� �ȳ��� �Ϸ��� 

```
sudo apt-get install pkg-config
pkg-config zlib --libs
```

### 2. dfu-util ���� ���� �ȳ��� �Ϸ��� 
```
sudo apt-get install libusb-1.0.0
```

### 3. 3dstools ���� ���� �ȳ��� �Ϸ��� 

~~sudo apt-get install libgraphicsmagick1-dev~~    
``` 
sudo apt-get install libmagick++-dev
```


***
����� �������� ���ص� �Ǵ� ���̾��� ~!~~!
===

gcc�� ��ġ�� ���� binutil�� ��ġ�� �ؼ� thumb -> arm ����� BLX �ڵ尡 �����ǰ� �� ���Ҵµ� 

����� arm-none-eabi-gcc �� ld�� ȣ���Ҷ� ds_arm9.specs�� �о� ���̴µ� ���⿡ ��Ŀ �ɼ��� �߰��� �ָ� �Ǵ� ���̾���.. ��,.��

��,

ds_arm9.specs �� �̷��� �Ǿ� �ִµ� 

```
%rename link                old_link

*link:
%(old_link) -T ds_arm9.mem%s -T ds_arm9.ld%s --gc-sections

*startfile:
ds_arm9_crt0%O%s crti%O%s crtbegin%O%s

```

�̰��� 

```
%rename link                old_link

*link:
%(old_link) -T ds_arm9.mem%s -T ds_arm9.ld%s --gc-sections --no-fix-arm1176

*startfile:
ds_arm9_crt0%O%s crti%O%s crtbegin%O%s

```

�̷��� --no-fix-arm1176 �ɼ��� �ָ� cpu ���׸� ��ȸ�ϱ� ���� stub �ڵ带 �������� �ʰ� ����  BLX �ڵ带 �����ϰ� �ȴ� .

***

�� ~~~~
-----------

