
# Linux kernel 3.18.79 for BQS-5020
Это исходный код ядра линукс для портирования дистрибутивов линукс для BQS-5020

Работа ядра тестировалось на 3 ревизии. Не тестировалось на RPiOS.

### Что работает/неработает: 
(не тестированно)

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
mkdir modules
make O=out ARCH=arm SUBRACH=arm CROSS_COMPILE=/home/mg30/android_prebuilts_gcc_linux-x86_arm_arm-linux-androideabi-4.9/bin/arm-linux-androideabi- TARGET_BUILD_VARIANT=user v3702_defconfig # заменить mg30 на текущего пользователя
make O=out ARCH=arm SUBRACH=arm CROSS_COMPILE=/home/mg30/android_prebuilts_gcc_linux-x86_arm_arm-linux-androideabi-4.9/bin/arm-linux-androideabi- TARGET_BUILD_VARIANT=user -j12 # заменить mg30 на текущего пользователя
find -type f -name *.ko -exec cp '{}' modules \; # Скомпилированные модули помещаем в modules
# При каждой новой компиляции вы должы будете помещать новые модули вместе с ядром (тоесть, пересобрал ядро поставил новые модули)
```

Очистка:
```
make O=out ARCH=arm SUBRACH=arm CROSS_COMPILE=/home/mg30/android_prebuilts_gcc_linux-x86_arm_arm-linux-androideabi-4.9/bin/arm-linux-androideabi- TARGET_BUILD_VARIANT=user CONFIG_MTK_COMBO_CHIP="CONSYS_6580" mrproper
```

Скомпилированное ядро хранится в out/arch/arm/boot/zImage-dtb, модули в modules
