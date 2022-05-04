

Visual Studio Community 로 ESP-IDF 빌드하기
=================================

https://esp32.com/viewtopic.php?t=18924

~~https://www.esp32.com/viewtopic.php?t=18924&start=10~~

위 주소를 참고, .. 하지만 버전이 달라서 안된다.. 고칠 부분은

현재 매뉴얼의 디렉토리에 있는 ..

1. CMakeSettings.json 으로 윈래의 CMakeSettings.json을 대치 

2. task.vs.json 을 대치

3. F:\_DEVELOP_\esp-idf\tools 를 Path에 추가

~~~
F:\_DEVELOP_\esp-idf\tools
~~~

4. idf_py_flash_monitor.cmd , idf_py_menuconfig.cmd , idf_py_monitor.cmd 를 F:\_DEVELOP_\esp-idf\tools 에 복사


***

끝 ~~~~
-----------

