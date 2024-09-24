
# Linux kernel 3.18.79 for BQS-5020
Это исходный код ядра линукс для портирования дистрибутивов линукс для BQS-5020

### TODO:
* Заставить работать wifi,bt,gps (consys mt6580). echo "1" > /dev/wmtWifi не работает, ошибка io и ошибки в dmesg
* Видео ядро
* Звонки
* Звук

## Сборка ядра
Установка пакетов для сборки
```
sudo apt install -y python2 git fakeroot build-essential ncurses-dev xz-utils libssl-dev bc flex libelf-dev bison
```

Линкуем /usr/bin/python2 >>> /usr/bin/python
```
ln -s /usr/bin/python2 /usr/bin/python
```

Скачиваем тулчейн(в ~ директории):
```
cd ~
git clone https://github.com/LineageOS/android_prebuilts_gcc_linux-x86_arm_arm-linux-androideabi-4.9.git -b cm-14.1
```
Сборка ядра:
```
mkdir out
make O=out ARCH=arm SUBRACH=arm CROSS_COMPILE=/home/mg30/android_prebuilts_gcc_linux-x86_arm_arm-linux-androideabi-4.9/bin/arm-linux-androideabi- v3702_defconfig # заменить mg30 на текущего пользователя
make O=out ARCH=arm SUBRACH=arm CROSS_COMPILE=/home/mg30/android_prebuilts_gcc_linux-x86_arm_arm-linux-androideabi-4.9/bin/arm-linux-androideabi- -j12 # заменить mg30 на текущего пользователя
```

Очистка:
```
make clean
make mrproper
```

Скомпилированное ядро хранится в out/arch/arm/boot/zImage-dtb
