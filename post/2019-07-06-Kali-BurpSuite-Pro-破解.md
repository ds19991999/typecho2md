# Kali BurpSuite Pro 破解

## 环境准备

- `jdk1.8`: https://pan.baidu.com/s/1fYQZ_DFRX64IrOTQ2g0_vg
- `Burp Suite Pro Loader&Keygen By surferxyz`: https://pan.baidu.com/s/1adX8-aTXVLltwdxGMINayw ，提取码 `mhui`

### jdk 1.8 环境

```shell
tar -xzvf jdk-8u191-linux-x64.tar.gz
mv jdk1.8.0_191/ /usr/local/lib/jvm
cd /usr/local/lib
mv jvm jdk1.8
export JAVA_HOME=/usr/local/lib/jdk1.8/ 
export JRE_HOME=JAVAHOME/jreexportCLASSPATH=.:{JAVA_HOME}/lib:JREHOME/libexportPATH={JAVA_HOME}/bin:$PATH
update-alternatives --install /usr/bin/java java /usr/local/lib/jdk1.8/bin/java 1 
update-alternatives --install /usr/bin/javac javac /usr/local/lib/jdk1.8/bin/javac 1
update-alternatives --set java /usr/local/lib/jdk1.8/bin/java
update-alternatives --set javac /usr/local/lib/jdk1.8/bin/javac
java -version 
```

### BurbSuite Pro and BurpLoader.jar

![](https://raw.githubusercontent.com/ds19991999/image/master/picgo/20190706214247.png)

```shell
java -jar BurpLoader.jar
```

之后就是粘贴复制了。

## 替换`kali`自带的社区版

```shell
mkdir /opt/burpsuite/
mv BurpLoader.jar /opt/burpsuite/
mv burpsuite_pro_v1.7.37.jar /opt/burpsuite/

cd /usr/bin/
mv burpsuite burpsuite.bak
rm /usr/bin/burpsuite

ln -s /opt/burpsuite/BurpLoader.jar /usr/bin/burpsuite
chmod +x /opt/burpsuite/BurpLoader.jar
```

`ok`了，现在打开左侧默认的`burpsuite`就已经是破解的专业版`1.7.37`了。