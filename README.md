# Lenovo-Z50-70-OpenCore-EFI-Sonoma-Mavericks
Lenovo IdeaPad Z50-70 (i5-4210U) — OpenCore EFI & Install Guide (macOS Sonoma & OS X 10.9 Mavericks)

English Guide | Русский туториал

Download EFI: Grab larpintosh.zip from the Releases section on the right!

───

English

Complete OpenCore EFI configurations and step-by-step installation guide for Lenovo IdeaPad Z50-70 (Intel Core i5-4210U, HD 4400) supporting both macOS Sonoma and OS X 10.9 Mavericks.

───

Step 1: BIOS Configuration
Enter BIOS (Fn + F2 or Novo button on power-on) and set the following:
• Boot Mode -> Legacy Support
• Boot Priority -> UEFI First(recommended for stable booting of both Sonoma and legacy Mavericks)
• Secure Boot -> Disabled
• Intel Virtual Technology (VT-d) -> Disabled
• Fast Boot -> Disabled
• SATA Controller Mode -> AHCI
• Note: You don't need to disable the discrete NVIDIA GPU in BIOS — it is already disabled in both OpenCore configurations.

───

Step 2: Prepare USB Installer & Replace EFI
1. Flash your macOS .dmg or .raw image onto a USB stick (using BalenaEtcher, TransMac, or dd).
2. Mount the USB drive's EFI partition (using Explorer++, DiskGenius, or diskutil on macOS).
3. Delete all existing files inside the USB's EFI partition.
4. Copy the folder you need from the archive (EFI-Sonoma or EFI-Mavericks, depending on which OS image you flashed) into the EFI partition.
5. Rename the copied folder to simply EFI (so the path is EFI/BOOT and EFI/OC).

───

Step 3: Generate Unique SMBIOS (Mandatory!)
Before booting, generate your own serial numbers so Apple services work properly:
1. Download GenSMBIOS and open EFI/OC/config.plist in ProperTree.
2. Generate SMBIOS: 
◦ For macOS Sonoma: use MacBookPro15,2.
◦ For OS X Mavericks: use MacBookPro11,1 (native Haswell SMBIOS).
3. Fill in PlatformInfo -&gt; Generic: 
◦ SystemSerialNumber
◦ MLB
◦ SystemUUID
◦ ROM

───

Step 4: Installing macOS Sonoma
1. Boot from the USB (Fn + F12), press Space in the OpenCore menu -> Reset NVRAM, then launch the macOS Sonoma installer.
2. Format your target drive/partition as APFS (GUID Partition Map) in Disk Utility and install the system.
3. Post-Install (Graphics Acceleration):
◦ Sonoma dropped native support for Intel HD 4400 (Haswell).
◦ Download and run OpenCore Legacy Patcher (OCLP) -> click Post-Install Root Patch -> install patches and reboot.
4. Copy the Sonoma EFI folder to your internal SSD's EFI partition so you can boot without the USB stick.

───

Known Mavericks Limitations:
• Brightness slider is missing (downgrade Lilu + WhateverGreen to 2020–2021 versions to restore it).
• Trackpad requires an older 10.9-compatible VoodooPS2Controller.kext.

───

Русский


Шаг 1: Настройка BIOS
Зайдите в BIOS (Fn + F2 или кнопка Novo при включении) и выставьте параметры:
• Boot Mode -> Legacy Support
• Boot Priority -> UEFI First
• Secure Boot -> Disabled
• Fast Boot -> Disabled
• SATA Controller Mode -> AHCI
• Примечание: отключать дискретную видеокарту NVIDIA в BIOS не обязательно — она уже отключена на уровне обоих конфигов OpenCore.

───

Шаг 2: Запись образа на флешку и замена EFI
1. Запишите установочный образ .dmg или .raw нужной macOS на флешку (через BalenaEtcher, TransMac или dd).
2. Смонтируйте скрытый раздел EFI на флешке (через DiskGenius, Explorer++ или diskutil в macOS).
3. Удалите все старые файлы из раздела EFI на флешке.
4. Скопируйте туда нужную папку из архива (EFI-Sonoma или EFI-Mavericks — в зависимости от того, какой образ вы записали).
5. Обязательно переименуйте скопированную папку просто в EFI (чтобы внутри неё сразу лежали папки BOOT и OC).

───

Шаг 3: Генерация серийных номеров (Обязательно!)
Перед запуском сгенерируйте свои уникальные серийники:
1. Скачайте GenSMBIOS и откройте EFI/OC/config.plist в ProperTree.
2. Сгенерируйте данные (для Sonoma — ваш актуальный SMBIOS, для Mavericks — нативный Haswell MacBookPro11,1) и впишите в раздел PlatformInfo -&gt; Generic: 
◦ SystemSerialNumber
◦ MLB
◦ SystemUUID
◦ ROM

───

Шаг 4: Установка macOS Sonoma
1. Загрузитесь с флешки (Fn + F12), в меню OpenCore нажмите Пробел -> Reset NVRAM, затем запустите установку macOS Sonoma.
2. В Дисковой утилите отформатируйте диск (или раздел под Sonoma) в APFS (схема GUID) и установите систему.
3. После установки (завод графики HD 4400):
◦ В Sonoma вырезана нативная поддержка графики Haswell.
◦ Скачайте и запустите OpenCore Legacy Patcher (OCLP) -> нажмите Post-Install Root Patch -> установите патчи и перезагрузитесь.
4. Скопируйте папку EFI от Sonoma на внутренний EFI-раздел SSD, чтобы система загружалась без флешки.
   
Известные нюансы в Mavericks:
• Отсутствует ползунок яркости экрана (лечится откатом Lilu + WhateverGreen до версий 2020–2021 гг.).
• Не работает тачпад (требуется более старая версия VoodooPS2Controller.kext под 10.9).
