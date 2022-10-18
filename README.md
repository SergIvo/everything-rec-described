# Everything Recognition
## О проекте
Данное приложение распознает те или иные объекты в изображении, полученном с веб-камеры пользователя. Список распозноваемых образов может быть изменен - для этого необходимо отредактировать файл `config.py`, добавив в него подходящие модели распознавания. Файлы доступных моделей расположены в директории `haarcascades`. Для распознования используется [каскадный классификатор](https://habr.com/ru/company/smartengines/blog/499962/) на [признаках Хаара](https://ru.wikipedia.org/wiki/%D0%9F%D1%80%D0%B8%D0%B7%D0%BD%D0%B0%D0%BA%D0%B8_%D0%A5%D0%B0%D0%B0%D1%80%D0%B0).

## Установка и настройка
1. Скачайте файлы с GitHub с помощью комманды `git clone`:
```
git clone https://github.com/SergIvo/everything-rec-described
```
2. Создайте виртуальное окружение с помощью библиотеки [venv](https://docs.python.org/3/library/venv.html). Это позволит избежать конфликтов версий, если другие версии библиотек, используемых в проекте, уже установлены на вашем компютере:
```
python -m venv venv
```
3. Воспользуйтесь командой `pip install`, чтобы установить необходимые библиотеки из файла "requirements.txt" в виртуальное окружение:
```
pip install -r requirements.txt
```
4. Чтобы добавить или убрать объекты из списка распознаваемых, нужно отредактировать список в файле `config.py`. Каждый распознаваемый объект в списке представлен записью следующего вида:
```
"Face profile": {
        "path": "haarcascades/faces/haarcascade_profileface.xml",
        "color": (255, 0, 0),
        "draw": True
    },
```
Ключевое значение имеют переменные `path`, `color` и `draw`. Названия этих переменных нельзя менять. Значения переменных должны быть следующими:
- В переменной `path` должен быть указан путь до файла с настройками классификатора. Файлы доступных классификаторов находятся в папке `haarcascades`;
- В переменной `color` указывается RGB-код цвета, которым распознаваемый объект будет обведен на итоговом изображении;
- Чтобы приложение отметило объект на изображении, переменная `draw` должна иметь значение `True`. Если нужно убрать объект из списка распознаваемых, достаточно изменить для него значение переменной `draw` на `False`.
## Запуск приложения
Запустите приложение следующей командой:
```
python run.py
```
Приложение будет использовать изображение с веб-камеры. Если веб-камера не доступна, приложение выведет в консоль сообщение: 
```
Couldn't find your webcam... Sorry :c
```
после чего завершится с ошибкой.
Если приложение сможет получить изображение с веб-камеры, это изображение будет выведено на экран в окне, при этом распознанные объекты будут обведены поверх изображения цветными прямоугольниками. В текущей конфигурации приложение распознает следующие объекты:
- Лицо, вид спереди, обводится красным цветом;
- Лицо, вид сбоку, обводится красным цветом;
- Глаза, каждый обводится зеленым цветом.

Получение изображений с веб-камеры и распознавание объектов происходит в бесконечном цикле. Чтобы прервать его и завершить работу приложения, нажмите клавишу `q`.
