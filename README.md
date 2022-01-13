# everything-recognition
Программа для распознавания образов, получаемых с веб-камеры. Скрипт запускает вашу камеру и отмечает
в видеопотоке определенные объекты(их можно настроить в файле `config.py`). Распознавание происходит на основе [каскадов Хаара](https://ru.wikipedia.org/wiki/%D0%9F%D1%80%D0%B8%D0%B7%D0%BD%D0%B0%D0%BA%D0%B8_%D0%A5%D0%B0%D0%B0%D1%80%D0%B0)
из библиотеки [OpenCV](https://opencv.org/).

## Требования
1. Наличие  веб-камеры. Параметры камеры можно изменить в файле `run.py`.
Число, которое мы передаем, означает источник. 0 – первая веб-камера в вашей системе, 1 – вторая и т.д.
```
video_capture = cv2.VideoCapture(0)
```
2. Пакет opencv-python версии 3.4.3.18. Установить можно командой:
```
pip install -r requirements.txt
```

## Запуск скрипта
```
python run.py
```

Откроется окно с перехватом потока веб-камеры. Цветными рамками будут выделены объекты, указанные в файле `config.py`.
В текущий реализации алгоритм выделяет:
- лицо анфас - `"Face front"`
- лицо в профиль - `"Face profile"`
- улыбка  - `"Smile"`
- глаза - `"Eyes"`
- тело целиком - `"Full body"`
- кошачья мордочка - `"Cat face"`

Выход из программы - нажать кнопку q.


## Настройки
Настройки находятся в файле `config.py`. Паттерны объектов находятся в словаре `CASCADES`:

```python
  "Face front": {
    "path": "haarcascades/faces/haarcascade_frontalface_default.xml",
    "color": (255, 0, 0),
    "draw": True
  },
```
 `"path"` - путь до xml, в котором хранятся каскады. Все каскады расположены в директории `haarcascades'. Пример кусочка каскада для распознавания улыбки:
 ```xml
 <opencv_storage>
<cascade type_id="opencv-cascade-classifier"><stageType>BOOST</stageType>
  <featureType>HAAR</featureType>
  <height>18</height>
  <width>36</width>
  <stageParams>
    <maxWeakCount>53</maxWeakCount></stageParams>
  <featureParams>
    <maxCatCount>0</maxCatCount></featureParams>
  <stageNum>20</stageNum>
  <stages>
    <_>
      <maxWeakCount>11</maxWeakCount>
      <stageThreshold>-1.2678639888763428e+00</stageThreshold>
      <weakClassifiers>

 ```
 Если хочется разобраться с непонятными циферками, можно прочитать вот эту [статью.](https://habr.com/ru/company/recognitor/blog/228195/)
 
 - `"color"` - цвет рамки 
 - `"draw"` - флаг для отображения объекта. Например у улыбки стоит флаг `False` - ее программа не будет выделять.

В папке `haarcascades` есть также каскады для распознавания  дорожных знаков, автомобилей и бананов.

## Цель проекта
Код написан в образовательных целях на онлайн-курсе для веб-разработчиков dvmn.org.
