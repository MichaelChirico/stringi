# stri\_datetime\_fields: Get Values for Date and Time Fields

## Description

Computes and returns values for all date and time fields.

## Usage

```r
stri_datetime_fields(time, tz = attr(time, "tzone"), locale = NULL)
```

## Arguments

|          |                                                                                                                                                                           |
|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `time`   | an object of class [`POSIXct`](https://stat.ethz.ch/R-manual/R-patched/library/base/html/DateTimeClasses.html) or an object coercible to                                  |
| `tz`     | `NULL` or `''` for the default time zone or a single string with time zone identifier, see [`stri_timezone_list`](stri_timezone_list.md)                                  |
| `locale` | `NULL` or `''` for the current default locale, or a single string with a locale identifier; a non-Gregorian calendar may be specified by setting `@calendar=name` keyword |

## Details

Vectorized over `time`.

## Value

Returns a data frame with the following columns:

1.  Year (0 is 1BC, -1 is 2BC, etc.)

2.  Month (1-based, i.e., 1 stands for the first month, e.g., January; note that the number of months depends on the selected calendar, see [`stri_datetime_symbols`](stri_datetime_symbols.md))

3.  Day

4.  Hour (24-h clock)

5.  Minute

6.  Second

7.  Millisecond

8.  WeekOfYear (this is locale-dependent)

9.  WeekOfMonth (this is locale-dependent)

10. DayOfYear

11. DayOfWeek (1-based, 1 denotes Sunday; see [`stri_datetime_symbols`](stri_datetime_symbols.md))

12. Hour12 (12-h clock)

13. AmPm (see [`stri_datetime_symbols`](stri_datetime_symbols.md))

14. Era (see [`stri_datetime_symbols`](stri_datetime_symbols.md))

## See Also

Other datetime: [`stri_datetime_add()`,](stri_datetime_add.md) [`stri_datetime_create()`,](stri_datetime_create.md) [`stri_datetime_format()`,](stri_datetime_format.md) [`stri_datetime_fstr()`,](stri_datetime_fstr.md) [`stri_datetime_now()`,](stri_datetime_now.md) [`stri_datetime_symbols()`,](stri_datetime_symbols.md) [`stri_timezone_get()`,](stri_timezone_set.md) [`stri_timezone_info()`,](stri_timezone_info.md) `stri_timezone_list()`

## Examples




```r
stri_datetime_fields(stri_datetime_now())
##   Year Month Day Hour Minute Second Millisecond WeekOfYear WeekOfMonth
## 1 2021     5  11   18      0     21         493         20           3
##   DayOfYear DayOfWeek Hour12 AmPm Era
## 1       131         3      6    2   2
stri_datetime_fields(stri_datetime_now(), locale='@calendar=hebrew')
##   Year Month Day Hour Minute Second Millisecond WeekOfYear WeekOfMonth
## 1 5781     9  29   18      0     21         496         35           5
##   DayOfYear DayOfWeek Hour12 AmPm Era
## 1       235         3      6    2   1
stri_datetime_symbols(locale='@calendar=hebrew')$Month[
   stri_datetime_fields(stri_datetime_now(), locale='@calendar=hebrew')$Month
]
## [1] "Iyar"
```