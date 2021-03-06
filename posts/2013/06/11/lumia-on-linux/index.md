# Заводим передачу файлов с Nokia Lumia 520 в Ubuntu 13.04

* * *
Купил новый телефон, но вот беда — к ПК под управлением Ubuntu 13.04 его не подключить.
* * *

SpaceFM его как флешку не определяет.  
gvfs устройство не видит.  
udev молчит.

Спросил совета на reddit'е, ткнули сюда: [Transferring Files Between Windows Phone 8 and Ubuntu](http://blog.wapreview.com/19006/)

Выяснилось, что, Nokia Lumia 520 как Mass Storage устройство не работает, но умеет передавать данные по Media Transfer Protocol.

Поставил Nautilus, который недавно дропнул при переезде.

Nautilus телефон видит, доступ к нему ведет по протоколу gphoto2 — попробуем покопать в этом направлении.

- Ставим gphotofs

        sudo apt-get install gphotofs

- Редактируем /etc/fuse.conf, раскомментируя строку

        user_allow_other

- Монтируем устройство

        sudo gphotofs -o allow_other /mnt

Теперь содержимое телефона доступно по адресу /mnt.

Чтобы отмонтировать телефон, необходимо выполнить

    fusermount -u /mnt

**UPD:** с недавнего времени PCManFM научился нормально работать с MTP-устройствами, так что файловые операции можно спокойно выполнять в нем. Однако, внесение указанных изменений в /etc/fuse.conf все равно требуется.

При подключении телефона придется выполнить команду

    sudo mtpfs