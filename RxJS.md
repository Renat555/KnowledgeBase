# Содержание
[Структура](#Структура)  
[Операторы](#Операторы)

# Структура

## Observable
```
const observable = new Observable(subscriber => {
  subscriber.next(1);
  subscriber.next(2);
  subscriber.next(3);
  setTimeout(() => {
    subscriber.next(4);
    subscriber.complete();
  }, 1000);
});
```

## Observer
```
const observer = {
  next: x => console.log('Observer got a next value: ' + x),
  error: err => console.error('Observer got an error: ' + err),
  complete: () => console.log('Observer got a complete notification'),
};
```

# Операторы

map - меняет каждое значение  
`of(1, 2, 3).pipe(map(x => x*2)) // 2, 4, 6`

filter - пропускает значения для которых коллбэк вернет истину  
`of(1, 2, 3, 4).pipe(filter(x => x%2 == 0)) // 2, 4`

reduce - сводит все значения к одному  
`of(1, 2, 3, 4).pipe(reduce((acc, curr) => acc + curr, 2)) // 12`

scan - то же самое, но выдает промежуточные значения тоже  
`of(1, 2, 3, 4).pipe(scan((acc, curr) => acc + curr, 2)) // 3, 5, 8, 12`

take - берет определенное количество результатов  
first/last, min/max - первый/последний, минимальный/максимальный результат  
`of(1, 2, 3, 4).pipe(take(2)) // 1, 2`  


tap - вывод побочных эффектов, например console.log  
`of(1, 2, 3, 4).pipe(tap(x => console.log(x)))`
