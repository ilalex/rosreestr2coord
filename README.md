ROSREESTR TO COORDINATE
=======================
Инструмент, позволяющий получать координаты участка по его кадастровому номеру
Данные берутся с сайта публичной кадастровой карты [http://pkk5.rosreestr.ru/](http://pkk5.rosreestr.ru/)

[DEMO](http://geonote.ru/pkk/)

## Requirements

* Python 2.7.x
* numpy
* [OpenCV](http://opencv.org/)

## Usage

Из консоли:

    python rosreestr2coord.py -c 38:06:144003:4723
    
Опции:

  * -h - справка
  * -c - кадастровый номер
  * -p - путь для промежуточных файлов
  * -o - путь для полученого geojson файла
  * -e - параметр, определяющий точность аппроксимации
  * -t - тип плащади: Участки 1, ОКС 5, Кварталы 2, Районы 3, Округа 4, Границы 7, ЗОУИТ 10, Тер. зоны 6, Красные линии 13, Лес 12, СРЗУ 15, ОЭЗ 16, ГОК 9
    
programmatically:
    
    from rosreestr2coord import Area
    
    area = Area("38:06:144003:4723") # дополнительные аргументы area_type=1 epsilum=5.5, media-path=MEDIA
    area.to_geojson()
    area.to_geojson_poly()
    area.get_coord() # [[[area1_xy], [hole1_xy], [hole2_xy]], [[area2_xyl]]]
    area.get_attrs()
    
## Журнал
* 03.10.2016 - Добавлена возможность выбора типа площади
* 05.09.2016 - Изменен формат записи координат, добавлена возможность хранить мультиполигональную геометрию. 
* 23.05.2016 - В тестовом режиме работает восстановление полигонов с отверстиями по PNG.
* 21.05.2016 - Были внесены изменения, чтобы вернуть работу с распознаванием точек по PNG. Упала точность, пропала способность рисовать полигоны и выделять отверстия
* 21.05.2016 - На публичных кадастровых картах заблокировали SVG и внесли ещё некоторые изменения в работу сервисов. В связи с этим перестало работать приложение

## TODO
* Увеличить точность для крупных полигонов (округа, кварталы, районы и др.)
* Различать мультиполигональную геометрию
* ~~Рисовать полигон~~ в тестовом режима
* ~~В полигоне находить отверстия~~ в тестовом режиме
* ~~Увеличить точность распознования углов~~ в тестовом режиме
