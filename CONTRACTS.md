# Network Protocol (JSON)

Все сообщения между клиентом и сервером передаются по WebSockets в формате JSON.

### Запросы Client -> Server

**1. Появление на сервере:**
```json
{
  "type": "New",
  "data": {}
}

```

**2. Обновление:**

```json
{
  "type": "Update",
  "data": {
    "active_modules": [],
    "used_modules": []
  }
}

```

**3. Выход / Удаление:**

```json
{
  "type": "delete",
  "data": {}
}

```

**4. Запрос ресурса (изображения):**

```json
{
  "type": "Load",
  "data": {
    "filetype": "image",
    "filename": "kolymaga2_ship.png"
  }
}

```

### Ответы Server -> Client

**1. Ответ при заходе на сервер и обновление состояния:**

```json
{
  "type": "Coords",
  "data": {
    "planets": [
      {"image": "pluto.png", "x": 100, "y": 1e+2, "vx": 0.5, "vy": 1e-7, "r": 50},
      {"image": "earth.png", "x": 300, "y": 1e+2, "vx": 0.05, "vy": 1e-3, "r": 80}
    ],
    "ships": [
      {"image": "kolymaga2.png", "x": 0, "y": 0, "angle": 0, "vx": 0, "vy": 0, "w": 0}
    ],
    "self_index": 5
  }
}

```

**2. Ответ с запрошенным ресурсом (Resource):**

```json
{
  "type": "Resource",
  "data": {
    "filename": "kolymaga2_ship.png",
    "href": "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAA..."
  }
}

```

### Описание полей ответа Coords

| Поле | Тип | Описание |
| --- | --- | --- |
| `planets` | `array` | Массив планет в зоне |
| `ships` | `array` | Список всех кораблей в зоне |
| `image` | `string` | Название файла текстуры объекта (планеты или корабля) |
| `x`, `y` | `float` | Координаты объекта на карте |
| `vx`, `vy` | `float` | Вектор линейной скорости по осям X и Y |
| `r` | `float` | Радиус планеты |
| `angle` | `float` | Угол поворота корпуса корабля |
| `w` | `float` | Угловая скорость вращения корабля |
| `self_index` | `int` | Индекс корабля текущего игрока в массиве `ships` |
