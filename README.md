# <center>TMS</center>

## <center>Home Work #4</center>

1. Добавил диск ``/dev/sdc`` (2Gb) к ВМ
![alt text](images/image1.png)
2. Отмонтировал диск, который монтировал в предыдущем ДЗ
![alt text](images/image2.png)
3. С помощью fdisk разбил его на три раздела(3GB+3GB+4GB)
![alt text](images/image3.png)
4. Из нового диска и двух разделов из п2 собрать volume group с именем vgdata

- Создал физические тома(PV) командой:
``pvcreate /dev/sdc /dev/sdb1 /dev/sdb2``
- Создал Volume Group командой:
``vgcreate vgdata /dev/sdc /dev/sdb1 /dev/sdb2``

- Проверил:
![alt text](images/image4.png)
![alt text](images/image4-1.png)

5. На volume group vgdata создаю два logical volume размера mysql(3GB) и postgres (3GB)
```bash
   lvcreate -n mysql -L 3G vgdata
   lvcreate -n postgres -L 3G vgdata
```
![alt text](images/image5.png)


6. Создать директории ``/opt/mysql`` и ``/opt/postgres`` и монтирую в них logical volume. Но сразу получаю ошибку, что на логических томах нет ФС
![alt text](images/image6.png)
7. Создаю ФС на логических томах
![alt text](images/image7.png)
8. Монтирую logical volume в ``/opt/mysql`` и ``/opt/postgres``
![alt text](images/image8.png)
9. Добавляю в volume group третий раздел диска ``/dev/sdb`` 
![alt text](images/image9.png)
- Проверяю:
![alt text](images/image9-1.png)
10. Расширяю logical volume mysql на весь доступный объем volume group
![alt text](images/image9-2.png)
- Смотрю вывод lsblk и проверяю
![alt text](images/image9-3.png)