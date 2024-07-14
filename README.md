# Pie Chart Application

Простое приложение на React для отображения круговой диаграммы с использованием библиотеки recharts.

## Функциональность

Приложение отображает круговую диаграмму с двумя сегментами, каждый из которых имеет свою цветовую схему. Сегменты помечены процентным соотношением, отображаемым внутри диаграммы.
<img width="420" alt="react-dashboard" src="https://github.com/user-attachments/assets/8119d082-7ec4-4bf2-b43b-8ad9a451a325">

## Установка

1. Клонируйте репозиторий на ваше локальное устройство:
    ```bash
    git clone https://github.com/Ivan-Inby/react-dashboard.git
    ```
2. Перейдите в директорию проекта:
    ```bash
    cd react-dashboard
    ```
3. Установите зависимости:
    ```bash
    npm install
    ```

## Использование

Для запуска приложения выполните:
```bash
npm start
```
Это запустит сервер разработки и откроет приложение в вашем браузере по умолчанию.

## Структура проекта

```bash
src/
├── App.js               # Главный компонент
├── index.js             # Точка входа
└── index.css            # CSS стили
```

## Обзор кода

### App.js

Главный компонент приложения отвечает за отображение круговой диаграммы с использованием данных и цветов, заданных в константах. Компонент включает кастомную метку, которая отображает процентное значение каждого сегмента диаграммы.

```javascript
import React from "react";
import { PieChart, Pie, Cell } from "recharts";

const data = [
  { name: "Group C", value: 300 },
  { name: "Group D", value: 200 }
];

const COLORS = ["#32CD32", "#FF0000"];

const RADIAN = Math.PI / 180;
const renderCustomizedLabel = ({
  cx,
  cy,
  midAngle,
  innerRadius,
  outerRadius,
  percent,
  index
}) => {
  const radius = innerRadius + (outerRadius - innerRadius) * 0.5;
  const x = cx + radius * Math.cos(-midAngle * RADIAN);
  const y = cy + radius * Math.sin(-midAngle * RADIAN);

  return (
    <text
      x={x}
      y={y}
      fill="white"
      textAnchor={x > cx ? "start" : "end"}
      dominantBaseline="central"
    >
      {`${(percent * 100).toFixed(0)}%`}
    </text>
  );
};

const App = () => {
  return (
    <PieChart width={400} height={400}>
      <Pie
        data={data}
        cx={200}
        cy={200}
        labelLine={false}
        label={renderCustomizedLabel}
        outerRadius={80}
        fill="#8884d8"
        dataKey="value"
      >
        {data.map((entry, index) => (
          <Cell key={`cell-${index}`} fill={COLORS[index % COLORS.length]} />
        ))}
      </Pie>
    </PieChart>
  );
};

export default App;
```

### Взаимодействие с API

В данном проекте взаимодействие с API не предусмотрено.

### Управление состоянием

Управление состоянием в данном проекте не требуется, так как данные диаграммы статичны.
