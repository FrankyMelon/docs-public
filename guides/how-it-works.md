# Как работает документация

Url страниц генерируется на основе пути до папки в файловой системе (см. примеры ниже).

## Локализация

Папка docs может содержать любое количество языков. Притом необязательно, чтобы файловая структура внутри языков совпадала.

## Типы страниц

Существует несколько типов страниц:

- Корневые страницы
- Страницы разделов
- Страницы статей

### Корневые страницы

Внутри папки с языком содержатся корневые страницы, которые можно редактировать, на данный момент это contacts и main.

- contact – это страница обратной связи
- main – это главная страница документации

Внутри main как и в любой другой папке обязательно должен быть .meta.json-файл, конфигурирующий эту страницу.

### Страницы разделов

Папки вложенные в папку main являются страницами разделов, разделы могут содержать любое количество подразделов или страниц статей.
Пример страницы разделов [../docs/ru/main/bigdata](../docs/ru/main/bigdata), там же есть .meta.json

Описание свойств этого файла:

- title - заголовок страницы
- sectionTitle - заголовок в левом меню навигации, обычно совпадает с title
- metaTitle - заголовок который показывается в табе в браузере
- metaDescription - описание для поисковиков
- weight - порядок вывода страницы в родительском разделе, чем меньше, тем выше
- shortDescription - краткое описание этой промежуточной страницы для внешней страницы
- markdown - описание промежуточной страницы на самой странице, поддерживает markdown (необязательное)
- uuid - любой уникальный uuidv4 (не требуется указывать вручную)

### Страницы статей

Если в папку не вложены другие папки (кроме папки assets), то страница считается статьей, такая папка кроме .meta.json должна содержать .md-файл с разметкой статьи, если в статье есть какие-то медиа-файлы, то можно создать папку assets и положить их туда.

Пример статьи [../docs/ru/main//base/iaas/vm-volumes//volume-resize/](../docs/ru/main//base/iaas/vm-volumes//volume-resize/)

Важно, что путь до страницы в документации генерируется на основе файловой системы, т.е. статья
[../docs/ru/main/base/iaas/vm-volumes/volume-resize/](../docs/ru/main/base/iaas/vm-volumes/volume-resize/)

будет доступна по адресу [mcs.mail.ru/docs/ru/main/base/iaas/vm-volumes/volume-resize](https://mcs.mail.ru/docs/ru/main/base/iaas/vm-volumes/volume-resize), а так же по более короткому варианту [mcs.mail.ru/docs/base/iaas/vm-volumes/volume-resize/](https://mcs.mail.ru/docs/ru/base/iaas/vm-volumes/volume-resize)

## Автосоздание редиректов

В документации реализована система автосоздания редиректов, система отслеживает изменение url-страницы, отслеживание происходит по уникальной строке (uuidv4), которая присватается каждой странице **автоматически** после мержа ветки в мастер.

```
Важно отметить, что группа редиректов может начать выдавать ошибку 404 только в том случае, если страница была удалена. Это может влиять на доступность внешних ссылок, так что удаляя статьи подумайте, возможно вы можете перенести uuid страницы на новую версию статьи, чтобы группа редиректов продолжила работу!
```

## Внешние ссылки (external-sections)

Позволяют создавать на группы из существующих статей и надежно ссылаться на эти группы из внешних источников. Даже если url-статьи изменится, она так же останется доступна.

В проекте с документацией существует папка externals/sections/, эту папку можно заполнить для того, чтобы создать набор ссылок, доступных черех api.

Мы используем это, например, для меню "Помощь" в [личном кабинете VK Cloud](https://mcs.mail.ru/app)

Как заполнять папку
В папке externals/sections/ можно создать любое количество подпапок соответствующее языкам, которые используются в папке docs.

В папке с языком, например, externals/sections/ru можно создать любое количество .json файлов с произвольными названиями, но лучше, чтобы названия соответствовали path страниц, для которых предназначается этот .json.

Как формируется .json-файл

```
{
    "meta": "Резервное копирование виртуальных машин",
    "groups": [
        {
            "title": "Информация",
            "links": [
                "docs/ru/main/additionals/start/user-account/mgmt-interfaces",
                "docs/ru/main/networks/vnet",
                ...любое количество ссылок на страницы
            ]
        },
        {
            "title": "Продвинутые настройки",
            "links": [
                "docs/ru/main/base/iaas/fs",
                "docs/ru/main/additionals/mp"
                ...может быть любое количство элементов
            ]
        }
        ...любое количество элементов
    ]
}
```

Описание полей:

- meta – не используется в интерфейсе, но в нем должно быть описано человекочитаемо в каком разделе админки/суперадминки нужно отображать этот json.
- links – автоматически берет актуальный заголовок страницы из указанного файла.

## Пайплайн: линтеры, валидаторы, тесты

В момент создания реквеста система автоматически запустит линтеры, валидаторы и тесты для проверки корректности внесенных изменений, в случае успешного прохождения этого этапа реквест будет рассатриваться как возможный для слияния в мастер. Если вы открыли реквест со своими изменениями и система выявила ошибки, требуется исправить их для того, чтобы ваш реквест рассматривался как возможный для слияния с мастером.