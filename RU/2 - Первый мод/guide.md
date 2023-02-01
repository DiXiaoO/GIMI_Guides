Первый мод
========================
# Короткое описание этого гайда
В этом гайде мы создадим свой первый простенький мод!  
Данный мод будет отключать Определённый 3D обьект.  

# Создание мода
1. Заходим в папку Mods и создаём там папку mod_1  
![](https://raw.githubusercontent.com/DiXiaoO/GIMI_Guides/main/files/2/0.png)  
2. В папке создадим файл Mod.ini  
![](https://raw.githubusercontent.com/DiXiaoO/GIMI_Guides/main/files/2/1.png)  
3. Откройте файл и вставьте в него следующее:  
```
[TextureOverrideMod]  
hash =  
handling = skip  
```
4. Обьяснение каждой строчки:  
[TextureOverrideMod]	- Открытие блока TextureOverride  
hash =					- Фильтрация по нужному хешу  
handling = skip			- Отключение отрисовки  
5. Заходим в некую аниме игру или нажимаем F10 и видим ошибку:
![](https://raw.githubusercontent.com/DiXiaoO/GIMI_Guides/main/files/2/2.png)  
GIMI(3D Migoto) показывает что у hash нет значения!  
Давайте найдём VB хеш нашего не любимого обьекта...  
Мне не понравились эти горшки с цветами!  
![](https://raw.githubusercontent.com/DiXiaoO/GIMI_Guides/main/files/2/3.png)  

Хеш этих горшков в версии 3.4.0 9d6e5632  
![](https://raw.githubusercontent.com/DiXiaoO/GIMI_Guides/main/files/2/4.png)  
6. Внесём найденный хеш в файл мода:  
![](https://raw.githubusercontent.com/DiXiaoO/GIMI_Guides/main/files/2/5.png)  
7. Нажимаем F10 и радуемся что больше не увидим модель этих горшков!  
![](https://raw.githubusercontent.com/DiXiaoO/GIMI_Guides/main/files/2/6.png)  

# Послесловие
В следующих гайдах я постораюсь подробнее описать, как редактировать ini файл мода.  