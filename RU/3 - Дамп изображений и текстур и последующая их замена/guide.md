Дамп изображений и текстур и последующая их замена
========================
# Короткое описание этого гайда
В этом гайде мы разберём как правильно дампить и изменять текстуры с помощью GIMI(3D Migoto)

# Предисловие
В основном информацию я буду брать из этого гайда  
https://github.com/SilentNightSound/GI-Model-Importer/blob/main/Guides/TextureModdingTutorial.md  
Так же я добавил ещё один способ который более лёгкий но не всегда рабочий.

# Приготовления к дампу
По умолчанию версия 3dmigoto для разработчиков настроена на сброс ВСЕХ текстур и буферов всякий раз, когда вы нажимаете F8, что вызвано этой строкой в ​​d3dx.ini:  
analyse_options = dump_rt dump_tex dump_cb dump_vb dump_ib buf txt  
![](https://raw.githubusercontent.com/DiXiaoO/GIMI_Guides/main/files/3/0.png)  
Это часто приводит к массивным (5-10 ГБ+) дампам кадров — я настоятельно рекомендую закомментировать эту строку следующим образом:  
; analyse_options = dump_rt dump_tex dump_cb dump_vb dump_ib buf txt  
![](https://raw.githubusercontent.com/DiXiaoO/GIMI_Guides/main/files/3/1.png)  

Теперь нам нужно загрузить программу с помощью которой мы сможем открыть и редактировать текстуры:
paint.net:
https://www.getpaint.net/download.html

Так же желательно установить аддон для редактирование альфа канала. (У некоротых текстур альфа канал отвечает за свечение)

# Дамп текстур через ShaderOverride
1. Для дампа текстур нам понадобится создать отдельный ini файл с помощью которого мы будет фильтровать большинство ненужной информации:
В папке Mods создадим папку dump:  
3dmigoto\Mods\dump  
Создадим в папке dump.ini  
Откроем файл. Он нам понадобится позднее.  
2. Заходим в игру и ищем текстуру которую хотим поменять.  
Я выбрал эту картину:  
![](https://raw.githubusercontent.com/DiXiaoO/GIMI_Guides/main/files/3/2.png)  
3. С помощью клавиш 1 и 2 (по умолчанию они используются для поиска PS хеша) ищем хеш картины (Картина должна пропасть):  
![](https://raw.githubusercontent.com/DiXiaoO/GIMI_Guides/main/files/3/3.png)  
В моём случае PS хеш = 1722be2ad18656fa  
Напомню что с помощью клавиши 3 можно копировать хеш (Только PS хеш. Для других хешей свои кнопки)  
4. Вставим в dump.ini следующее:  
```
[ShaderOverrideDump]  
hash = 1722be2ad18656fa  ; Тут может быть хеш который вы нашли
analyse_options = dump_rt dump_tex dump_cb dump_vb dump_ib buf txt dds  
```  
5. Обновляем моды через F10. Делаем дамп кадра через F8.  
Игра может зависнуть на некоротое время.  
Если всё хорошо то вы увидите это:  
![](https://raw.githubusercontent.com/DiXiaoO/GIMI_Guides/main/files/3/4.png)  
6. Переходим в папку 3dmigoto и видим сверху папку FrameAnalysis-XXXX-XX-XX-XXXXXX:  
![](https://raw.githubusercontent.com/DiXiaoO/GIMI_Guides/main/files/3/5.png)  
В данной папке находятся всё что было связано с данным хешем:  
![](https://raw.githubusercontent.com/DiXiaoO/GIMI_Guides/main/files/3/6.png)  
7. Ищем текстуру нашей картины:  
![](https://raw.githubusercontent.com/DiXiaoO/GIMI_Guides/main/files/3/7.png)  
Ничего страшного если их появилось две. Просто эта текстура отрисовывалась на двух этапах отрисовки.  
Точнее на 000048 и 000049 этапе (первые 6 цифр)  
Возьмём первую текстуру:  
000048-ps-t0=3222d659-vs=f444688ac976914d-ps=1722be2ad18656fa.dds  
Скорее всего хешем текстуры является ps-t0 = 3222d659  
Давайте проверим с помощью "Первого мода"  
```  
[TextureOverrideMod]  
hash = 3222d659  
handling = skip  
```  
В результате мы увидим что не только картина, но и некоротые другие объекты интерьера пропали!  
Это было ожидаемо так как текстура содержала не только текстуру для картины но и для других объектов.  
![](https://raw.githubusercontent.com/DiXiaoO/GIMI_Guides/main/files/3/8.png)  

# Дамп текстур через TextureOverride  
1. Следуем 1 и 2 шагу из способа с ShaderOverride  
2. В этом способе нам не нужно искать хеш!  
Прописываем в dump.ini следующее:  
```
[TextureOverrideDump]  
match_type = Texture2D  
dump = dump_tex share_dupes this  
```
![](https://raw.githubusercontent.com/DiXiaoO/GIMI_Guides/main/files/3/9.png)  
3. Обновляем моды через F10. Делаем дамп кадра через F8.  
Игра может зависнуть на некоротое время.  
(Аналогично шагу 5 из способа с ShaderOverride)  
4. У нас появилось две папки:  
FrameAnalysis-2023-02-01-185454 - Обычный дамп со всеми вытикающими.  
FrameAnalysisDeduped - Отфильтрованая часть содержащая только Texture2D.  
![](https://raw.githubusercontent.com/DiXiaoO/GIMI_Guides/main/files/3/10.png)  
5. Пытаемся найти текстуру:  
![](https://raw.githubusercontent.com/DiXiaoO/GIMI_Guides/main/files/3/11.png)  
Текстура не сдампилась...  
Не удивительно. Этот способ больше подходит для массового дампа нескольких элементов интерфейса.  
Хотя с его помощью так же можно дампить объекты.  

# Замена текстуры
1. Первым делом создадим папку для мода и ini файл:  
![](https://raw.githubusercontent.com/DiXiaoO/GIMI_Guides/main/files/3/12.png)  
Так же я сразу переместил туда текстуру которую мы будем изменять.  
2. Откроем ini файл запишем туда следующее:  
```  
[TextureOverrideMod]  
hash = 3222d659  
this = ResourceMod  
  
[ResourceMod]  
filename = 000048-ps-t0=3222d659-vs=f444688ac976914d-ps=1722be2ad18656fa.dds  
```  
Где:  
this - Текстура которую мы меняем.  
Resource - Раздел ресурсов. !!!Этот раздел должен быть в самом конце фала!!!  
filename - Путь до файла  
3. Попробуем перезагрузить моды с помощью F10.  
Если два или более модов используют один хеш то появляется данная ошибка:  
![](https://raw.githubusercontent.com/DiXiaoO/GIMI_Guides/main/files/3/13.png)  
Она не должна влиять на работу остальных модов, но это может вызвать конфликт модов использующих один хеш.  
4. Используя paint.net открываем текстуру.  
![](https://raw.githubusercontent.com/DiXiaoO/GIMI_Guides/main/files/3/14.png)  
Редактируем и сохраняем текстуру.  
В зависимости от вида текстуры мы должны сохранить её в:  
	1. BC7 Линейный DXT11+	- Обычно в этом формате хранятся текстуры без альфаканала  
	2. BC7 sRGB DXT11+		- Обычно в этом формате хранятся текстуры с альфаканалом  
![](https://raw.githubusercontent.com/DiXiaoO/GIMI_Guides/main/files/3/15.png)  
5. Перезагружаем моды F10:  
![](https://raw.githubusercontent.com/DiXiaoO/GIMI_Guides/main/files/3/16.png)  
Если сохранить не в том формате:  
![](https://raw.githubusercontent.com/DiXiaoO/GIMI_Guides/main/files/3/17.png)  

# Послесловие  
Я посторался сделать подробный, но короткий гайд на эту тему...  