# CVE_2022_38181-Mali-SAMSUNG-S6-Lite-Tablet

We flashed the Samsung tablet with the firmware that i downloaded from SAMFW(https://samfw.com/firmware/SM-P610/TUR) -> P610XXS2CUG5(https://samfw.com/firmware/SM-P610/TUR/P610XXS2CUG5)

It’s the Turkish version of the Samsung Galaxy s6 lite SM-P610

I extracted the AP_** file inside the Firmware and extracted the boot.img.lz4 file.

tar -xf AP_P610XXS2CUG5_CL21663430_QB41743119_REV00_user_low_ship_meta_OS11.tar.md5
Then extracted the boot img

lz4 -d boot.img.lz4

Used the bad_io_uring script to extract the kernel (https://github.com/marin-m/vmlinux-to-elf/tree/master)

python3 bad_io_uring/tools/unpack_bootimg.py –boot_img boot.img –out out

Used the kallsyms-finder to find all symbols of the kernel

./bad_io_uring//tools/vmlinux-to-elf/kallsyms-finder out/kernel > samsungS6.kallsyms

Seems it worked and when i try to run the PoC tablet gets a crash so the vulnerability is existed

![image](https://github.com/user-attachments/assets/f4df657f-db55-433e-9662-760418353200)
