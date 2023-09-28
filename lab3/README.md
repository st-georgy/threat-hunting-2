Информационно-аналитические технологии поиска угроз информационной
безопасности
================
Zhidkov Georgy

Лабораторная работа №3

## Цель

1.  Развить практические навыки использования языка программирования R
    для обработки данных
2.  Закрепить знания базовых типов данных языка R
3.  Развить пркатические навыки использования функций обработки данных
    пакета dplyr – функции select(), filter(), mutate(), arrange(),
    group_by()

## Исходные данные

1.  ОС Windows 11
2.  RStudio Desktop
3.  Интерпретатор языка R 4.2.2
4.  dplyr
5.  nycflights13

## План

1.  Установить пакет ‘dplyr’
2.  Установить пакет ‘nycflights13’
3.  Выполнить задания

## Шаги

### Установка dplyr

Пакет dplyr можно установить в RStudio Desktop с помощью команды
install.packages(“dplyr”). Далее подключим пакет к текущему проекте с
помощью library(dplyr)

``` r
library(dplyr)
```

    Warning: пакет 'dplyr' был собран под R версии 4.2.3


    Присоединяю пакет: 'dplyr'

    Следующие объекты скрыты от 'package:stats':

        filter, lag

    Следующие объекты скрыты от 'package:base':

        intersect, setdiff, setequal, union

### Установка nycflights13

Пакет dplyr можно установить в RStudio Desktop с помощью команды
install.packages(“nycflights13”). Далее подключим пакет к текущему
проекте с помощью library(nycflights13)

``` r
library(nycflights13)
```

    Warning: пакет 'nycflights13' был собран под R версии 4.2.3

### Выполнение заданий

#### 1. Сколько встроенных в пакет nycflights13 датафреймов?

В пакет nycflights13 встроено 5 датафреймов: airlines, airports,
flights, planes, weather

#### 2. Сколько строк в каждом датафрейме?

``` r
airlines %>% 
  nrow()
```

    [1] 16

``` r
airports %>%
  nrow()
```

    [1] 1458

``` r
flights %>%
  nrow()
```

    [1] 336776

``` r
planes %>%
  nrow()
```

    [1] 3322

``` r
weather %>%
  nrow()
```

    [1] 26115

#### 3. Сколько столбцов в каждом датафрейме?

``` r
airlines %>% 
  ncol()
```

    [1] 2

``` r
airports %>%
  ncol()
```

    [1] 8

``` r
flights %>%
  ncol()
```

    [1] 19

``` r
planes %>%
  ncol()
```

    [1] 9

``` r
weather %>%
  ncol()
```

    [1] 15

#### 4. Как просмотреть примерный вид датафрейма?

1 способ:

``` r
planes %>% 
  glimpse()
```

    Rows: 3,322
    Columns: 9
    $ tailnum      <chr> "N10156", "N102UW", "N103US", "N104UW", "N10575", "N105UW…
    $ year         <int> 2004, 1998, 1999, 1999, 2002, 1999, 1999, 1999, 1999, 199…
    $ type         <chr> "Fixed wing multi engine", "Fixed wing multi engine", "Fi…
    $ manufacturer <chr> "EMBRAER", "AIRBUS INDUSTRIE", "AIRBUS INDUSTRIE", "AIRBU…
    $ model        <chr> "EMB-145XR", "A320-214", "A320-214", "A320-214", "EMB-145…
    $ engines      <int> 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, …
    $ seats        <int> 55, 182, 182, 182, 55, 182, 182, 182, 182, 182, 55, 55, 5…
    $ speed        <int> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    $ engine       <chr> "Turbo-fan", "Turbo-fan", "Turbo-fan", "Turbo-fan", "Turb…

2 способ:

``` r
planes %>%
  head()
```

    # A tibble: 6 × 9
      tailnum  year type               manufacturer model engines seats speed engine
      <chr>   <int> <chr>              <chr>        <chr>   <int> <int> <int> <chr> 
    1 N10156   2004 Fixed wing multi … EMBRAER      EMB-…       2    55    NA Turbo…
    2 N102UW   1998 Fixed wing multi … AIRBUS INDU… A320…       2   182    NA Turbo…
    3 N103US   1999 Fixed wing multi … AIRBUS INDU… A320…       2   182    NA Turbo…
    4 N104UW   1999 Fixed wing multi … AIRBUS INDU… A320…       2   182    NA Turbo…
    5 N10575   2002 Fixed wing multi … EMBRAER      EMB-…       2    55    NA Turbo…
    6 N105UW   1999 Fixed wing multi … AIRBUS INDU… A320…       2   182    NA Turbo…

#### 5. Сколько компаний-перевозчиков (carrier) учитывают эти наборы данных (представлено в наборах данных)?

``` r
airlines %>%
  nrow()
```

    [1] 16

#### 6. Сколько рейсов принял аэропорт John F Kennedy Intl в мае?

``` r
faa_jfk <- airports %>%
  filter(name == "John F Kennedy Intl") %>%
  select(faa)

flights %>%
  filter(month == 5 & dest == as.character(faa_jfk)) %>%
  nrow()
```

    [1] 0

#### 7. Какой самый северный аэропорт?

``` r
airports %>%
  filter(lat == max(lat))
```

    # A tibble: 1 × 8
      faa   name                      lat   lon   alt    tz dst   tzone
      <chr> <chr>                   <dbl> <dbl> <dbl> <dbl> <chr> <chr>
    1 EEN   Dillant Hopkins Airport  72.3  42.9   149    -5 A     <NA> 

#### 8. Какой аэропорт самый высокогорный (находится выше всех над уровнем моря)?

``` r
airports %>%
  filter(alt == max(alt))
```

    # A tibble: 1 × 8
      faa   name        lat   lon   alt    tz dst   tzone         
      <chr> <chr>     <dbl> <dbl> <dbl> <dbl> <chr> <chr>         
    1 TEX   Telluride  38.0 -108.  9078    -7 A     America/Denver

#### 9. Какие бортовые номера у самых старых самолетов?

``` r
planes %>%
  arrange(year) %>%
  head(10) %>%
  select(tailnum)
```

    # A tibble: 10 × 1
       tailnum
       <chr>  
     1 N381AA 
     2 N201AA 
     3 N567AA 
     4 N378AA 
     5 N575AA 
     6 N14629 
     7 N615AA 
     8 N425AA 
     9 N383AA 
    10 N364AA 

#### 10. Какая средняя температура воздуха была в сентябре в аэропорту John F Kennedy Intl (в градусах Цельсия).

``` r
faa_jfk <- airports %>%
  filter(name == "John F Kennedy Intl") %>%
  select(faa)

weather %>%
  filter(origin == as.character(faa_jfk) & month == 9) %>%
  summarize(mean_temp = mean(temp, na.rm = TRUE))
```

    # A tibble: 1 × 1
      mean_temp
          <dbl>
    1      66.9

#### 11. Самолеты какой авиакомпании совершили больше всего вылетов в июне?

``` r
flights %>%
  filter(month == 6) %>%
  group_by(carrier) %>%
  summarize(total_flights = n()) %>%
  arrange(desc(total_flights)) %>%
  head(1)
```

    # A tibble: 1 × 2
      carrier total_flights
      <chr>           <int>
    1 UA               4975

### 12. Самолеты какой авиакомпании задерживались чаще других в 2013 году?

``` r
flights %>%
  filter(year == 2013) %>%
  group_by(carrier) %>%
  summarize(total_delays = sum(arr_delay > 0, na.rm = TRUE)) %>%
  arrange(desc(total_delays)) %>%
  head(1)
```

    # A tibble: 1 × 2
      carrier total_delays
      <chr>          <int>
    1 EV             24484

## Оценка результата

В результате лабораторной работы были выполнены задания с использованием
пакета dplyr на датафреймах из пакета nycflights13

## Вывод

Мы получили базовые навыки работы с пакетом dplyr для языка R с новыми
наборами данных
