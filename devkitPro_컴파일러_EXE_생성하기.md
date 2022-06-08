

windows bash 에서 devkitARM 빌드하기
=================================

매뉴얼대로 하고난후 bash shell 에서 mingw32를 설치해서 windows 용 binary를 생성해야 한다.

https://marc.xn--wckerlin-0za.ch/computer/cross-compile-on-ubuntu-linux-for-windows-using-mingw

~~~
sudo apt-get install mingw-w64
~~~

이상태에서는 mingw-w64에는 gcc에 필요한 3개의 라이브러리가 없다.

MSYS2 mintty shell 에서 작업하기로 추가함.. 2022.6.8

~~~
GMP
---
URL : https://gmplib.org/
내가 설치한 URL : https://gmplib.org/download/gmp/gmp-6.1.1.tar.bz2
압축 해제tar -xvf mpfr-3.1.5.tar.gz압축 해제 후 $ 
./configure
make install

MPFR
----
URL : http://www.mpfr.org/mpfr-current/
내가 받은 URL : http://www.mpfr.org/mpfr-current/mpfr-3.1.5.tar.gz
압축 해제tar -xvf mpfr-3.1.5.tar.gz
압축 해제 후 $ ./configure --enable-static --disable-share
dmake install

MPC
---
URL : http://www.multiprecision.org/index.php?prog=mpc&page=download
내가 받은 URL : ftp://ftp.gnu.org/gnu/mpc/mpc-1.0.3.tar.gz
압축 해제tar -xvf mpfr-3.1.5.tar.gz
압축 해제 후 $ ./configure --enable-static --disable-shared
make install

~~~

~~

GMP
---
~~~
wget https://gmplib.org/download/gmp/gmp-6.1.2.tar.bz2
./configure  --host=x86_64-w64-mingw32 --prefix=/usr/x86_64-w64-mingw32/
make
sudo make install
<<- 이거 해 줘야 gmp.h 가 x86_64-w64-mingw32 의 include에 들어간다.
~~~

MPFR
----
~~~
wget https://www.mpfr.org/mpfr-current/mpfr-4.0.2.tar.bz2
./configure  --host=x86_64-w64-mingw32 --prefix=/usr/x86_64-w64-mingw32/ --enable-static --disable-shared
make
sudo make install
~~~

update

~~~
wget https://www.mpfr.org/mpfr-current/mpfr-4.1.0.tar.bz2
./configure  --host=x86_64-w64-mingw32 --prefix=/usr/x86_64-w64-mingw32/ --enable-static --disable-shared \
--with-gmp-include=/usr/x86_64-w64-mingw32/include/ --with-gmp-lib=/usr/x86_64-w64-mingw32/lib
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
~~
이렇게 3개를 설치한 후 

cross-build-x86_64-w64-mingw32.sh 

를


~~~
#!/bin/bash
export CROSSBUILD=x86_64-w64-mingw32
export CROSSPATH=/usr/x86_64-w64-mingw32
export CROSSLIBPATH=$CROSSPATH/lib
export CROSSBINPATH=/usr/bin
~~~


이렇게 고치고. 컴파일 하니 안되었다. ㅠ.ㅠ

이게 없어서.. zlib

ZLIB 
----
### 크로스 컴파일을 위해서 할일  

오래된 라이브러리라서 그런지 --host= 의 구문은 안먹는다 

```
wget https://zlib.net/zlib-1.2.11.tar.xz
CHOST=x86_64-w64-mingw32 ./configure --prefix=/usr/x86_64-w64-mingw32 --static
make
sudo make install
```

update

```
wget https://zlib.net/zlib-1.2.12.tar.xz
./configure
make
make install
ln /usr/local/lib/libz.a /usr/lib -s
```

이렇게 해서 zlib.h를 설치한후 계속 진행하자..

***

~~아래의 방법은 인터넷에 나와있는것인데 bash shell 에서는 안된다. 
안되므로 쓰지말자.
위에것은 안된다-> 아니다 위의 방법으로 된다.. zlib내의 win32/Makefile.gcc를 수정해야 한다.
PREFIX =  
이렇게 된 곳을
PREFIX = x86_64-w64-mingw32-
이렇게 바꾼후
make -f win32/Makefile.gcc BINARY_PATH=/usr/bin INCLUDE_PATH=/usr/x86_64-w64-mingw32/include LIBRARY_PATH=/usr/x86_64-w64-mingw32/lib install
로 빌드한뒤에 라이브러리 인스톨~~

***
드디어 컴파일
===

```
. cross-build-x86_64-w64-mingw32.sh 
```

<- 현재의 스크립트를 sub envioment가 아닌 현재의 enviroment에 반영하게 한후

~~~
./build-devkit.sh로 빌드시작하면 됨!!!
~~~

여기서 인스톨 디렉토리에 `:` 가 있으면 에러가 나므로 

```
Please enter the directory where you would like 'devkitARM' to be installed:
for mingw/msys you must use <drive>:/<install path> or you will have include path problems
this is the top level directory for devkitpro, i.e. e:/devkitPro
```
요 문구가 나오면 

```
/f/_DEVELOP_/devkitPro 
```
이렇게 해 줘야 한다.

추가작업
---

### 1. gp32-tools 빌드 에러 안나게 하려면 

```
sudo apt-get install pkg-config
pkg-config zlib --libs
```

### 2. dfu-util 빌드 에러 안나게 하려면 
```
sudo apt-get install libusb-1.0.0
```

### 3. 3dstools 빌드 에러 안나게 하려면 

~~sudo apt-get install libgraphicsmagick1-dev~~    
``` 
sudo apt-get install libmagick++-dev
```


***
사실은 컴파일을 안해도 되는 것이었다 ~!~~!
===

gcc도 패치해 보고 binutil도 패치를 해서 thumb -> arm 실행시 BLX 코드가 생성되게 해 보았는데 

사실은 arm-none-eabi-gcc 가 ld를 호출할때 ds_arm9.specs를 읽어 들이는데 여기에 링커 옵션을 추가해 주면 되는 것이었다.. ㅡ,.ㅡ

즉,

ds_arm9.specs 는 이렇게 되어 있는데 

```
%rename link                old_link

*link:
%(old_link) -T ds_arm9.mem%s -T ds_arm9.ld%s --gc-sections

*startfile:
ds_arm9_crt0%O%s crti%O%s crtbegin%O%s

```

이것을 

```
%rename link                old_link

*link:
%(old_link) -T ds_arm9.mem%s -T ds_arm9.ld%s --gc-sections --no-fix-arm1176

*startfile:
ds_arm9_crt0%O%s crti%O%s crtbegin%O%s

```

이렇게 --no-fix-arm1176 옵션을 주면 cpu 버그를 우회하기 위한 stub 코드를 생성하지 않고 직접  BLX 코드를 생셩하게 된다 .

***

끝 ~~~~
-----------

