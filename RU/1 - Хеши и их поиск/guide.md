Хеши и их поиск  
========================
# Коротко про хеши в GIMI(3D Migoto) и зачем они нужны
GIMI(3D Migoto) использует хеши, что бы узнать, какую часть памяти он должен изменять.

# Виды хешей в GIMI(3D Migoto)
- VS - vertexshader  
	По умолчнанию переключается с помощью кнопок '4', '5', '6' на Numpad(Дополнительные клавиши клавиатуры справа)  
	
- PS - pixelshader  
	По умолчнанию переключается с помощью кнопок '1', '2', '3' на Numpad(Дополнительные клавиши клавиатуры справа)  
	
- VB - vertexbuffer  
	По умолчнанию переключается с помощью кнопок '/', '*', '-' на Numpad(Дополнительные клавиши клавиатуры справа)  
	
- IB - indexbuffer  
	По умолчнанию переключается с помощью кнопок '7', '8', '9' на Numpad(Дополнительные клавиши клавиатуры справа)  
	
- CS - computeshader  
- GS - geometryshader  
- DS - domainshader  
- HS - hullshader  

# Поиск хешей
1. Входим в некую аниме игру.  
2. Видим наш любимый зелёный текст) (Вы ведь зашли через версию разработчика?)  
![](https://raw.githubusercontent.com/DiXiaoO/GIMI_Guides/main/files/1/0.png)    
3. Нажимаем на клавишу 1 на Numpad и видим следующее
![](https://raw.githubusercontent.com/DiXiaoO/GIMI_Guides/main/files/1/1.png)
Слева сверху появился некий PS хеш  
По умолчанию в GIMI(3D Migoto) отключается отрисовка выбранного обьекта  
Оригинал  
![](https://raw.githubusercontent.com/DiXiaoO/GIMI_Guides/main/files/1/2.png)  
Выбранн хеш отвечающий за листву на дереве  
![](https://raw.githubusercontent.com/DiXiaoO/GIMI_Guides/main/files/1/3.png)  
4. Нажав клавишу 2 на Numpad, мы перелистываем на превидущий PS хеш  
С помощью клавиши 3 на Numpad мы скопируем PS хеш в буфер обмена  
Аналогично для VS, VB и IB хешей

# Впорос-ответ
1. Что делать если у меня нет Numpad на клавиатуре?
	1. Ответ: Вы можете изменить клавишы в конфиг файле GIMI(3D Migoto)  
	Пример изменения одной клавиши:    
		1. Открываем d3dx.ini  
		2. Находим строчку "previous_pixelshader"  
		3. Находим "previous_pixelshader = no_modifiers NO_VK_DECIMAL VK_Numpad1"
		4. Заменяем "VK_Numpad1" на "VK_OEM_4"
		5. В игре нажимаем F10 или перезагружаем игру.
		6. Всё! Теперь при нажатии клавиши "[{" будет перелистываться PS хеш
	
	Коды клавиш можно найти тут https://learn.microsoft.com/en-us/windows/win32/inputdev/virtual-key-codes
	
	2. Ответ: Используйте экранную клавиатуру  