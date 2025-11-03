# Table of Contents
- [Calendar](#calendar)
	- [Calendar.Date](#calendar-date)
- [CalendarLocale](#calendarlocale)

---

# <a id="calendar"></a>Calendar
Inherits: `RefCounted < Object`

**A utility library for generating calendar data.**

## Description
Calendar is a comprehensive library for creating calendar views, including yearly, monthly, weekly overviews, and agendas. It follows Godot's Time conventions (Sunday = 0 to Saturday = 6) and uses the Proleptic Gregorian Calendar (the day before 1582-10-15 is 1582-10-14).  
Calendar works with the helper class [Calendar.Date](#calendar-date) and can localize output via a [CalendarLocale](#calendarlocale) resource.

## Properties
**[calendar_locale](#calendar-prop-calendar_locale)** : CalendarLocale  
**[first_weekday](#calendar-prop-first_weekday)** : Time.Weekday  
**[week_number_system](#calendar-prop-week_number_system)** : WeekNumberSystem

## Methods
[get_calendar_month](#calendar-method-get_calendar_month)(year: int, month: int, include_adjacent_days: bool = false, force_six_weeks: bool = false) : Array  
[get_calendar_week](#calendar-method-get_calendar_week)(year: int, month: int, day: int, days_in_week: int = 7) : Array\[Date]   
[get_calendar_year](#calendar-method-get_calendar_year)(year: int, include_adjacent_days: bool = false, force_six_weeks: bool = true) : Array  
[get_date_formatted](#calendar-method-get_date_formatted)(year: int, month: int, day: int, format: String = '%Y-%m-%d') : String  
[get_date_locale_format](#calendar-method-get_date_locale_format)(year: int, month: int, day: int, four_digit_year: bool = true) : String  
[get_day_of_year](#calendar-method-get_day_of_year)(year: int, month: int, day: int) : int  
[get_days_in_month](#calendar-method-get_days_in_month)(year: int, month: int) : int  
[get_days_in_year](#calendar-method-get_days_in_year)(year: int) : int  
[get_days_of_range](#calendar-method-get_days_of_range)(days: int, year: int, month: int, day: int, exclusive: bool = false) : Array\[Date]   
[get_leap_days](#calendar-method-get_leap_days)(from_year: int, to_year: int, exclusive_to: bool = true) : int  
[get_month_formatted](#calendar-method-get_month_formatted)(month: int, month_format: MonthFormat = 1) : String  
[get_months_formatted](#calendar-method-get_months_formatted)(month_format: MonthFormat = 1) : Array\[String]   
[get_today](#calendar-method-get_today)() : Date  
[get_week_number](#calendar-method-get_week_number)(year: int, month: int, day: int) : int  
[get_weekday](#calendar-method-get_weekday)(year: int, month: int, day: int) : Time.Weekday   
[get_weekday_formatted](#calendar-method-get_weekday_formatted)(year: int, month: int, day: int, weekday_format: WeekdayFormat = 0) : String  
[get_weekdays](#calendar-method-get_weekdays)() : Array\[Time.Weekday]  
[get_weekdays_formatted](#calendar-method-get_weekdays_formatted)(weekday_format: WeekdayFormat = 1) : Array\[String]   
[get_weeks_of_month](#calendar-method-get_weeks_of_month)(year: int, month: int, force_six_weeks: bool = false) : Array\[int]   
[is_leap_year](#calendar-method-is_leap_year)(year: int) : bool  
[set_calendar_locale](#calendar-method-set_calendar_locale)(path: String) : void  
[set_first_weekday](#calendar-method-set_first_weekday)(first_weekday: Time.Weekday) : void  
[set_week_number_system](#calendar-method-set_week_number_system)(week_number_system: WeekNumberSystem) : void  

## Enumerations
**<a id="calendar-enumerations"></a>WeekdayFormat** : enum  
`WEEKDAY_FORMAT_FULL = 0`  
>Full weekday name.

`WEEKDAY_FORMAT_ABBR = 1`  
>Abbreviated (e.g. 'Mon').

`WEEKDAY_FORMAT_SHORT = 2`  
>Short (e.g. 'M').

**MonthFormat** : enum  
`MONTH_FORMAT_FULL = 0`  
>Full month name.

`MONTH_FORMAT_ABBR = 1`  
>Abbreviated (e.g. 'Jan').

`MONTH_FORMAT_SHORT = 2`  
>Short (e.g. 'J').

**WeekNumberSystem** : enum  
`WEEK_NUMBER_FOUR_DAY = 0`  
>First week has at least four days (respects [first_weekday](#calendar-prop-first_weekday). This how ISO 8601 works.

`WEEK_NUMBER_TRADITIONAL = 1`  
>First week is the one containing January 1.

## Property Descriptions

<a id="calendar-prop-calendar_locale"></a>**calendar_locale** : CalendarLocale
>The calendar's localization settings for retrieving preformatted values. Each calendar is assigned a `CalendarLocale`, defaulting to English. Assign a custom resource to localize names and formats.  
See [CalendarLocale](#calendarlocale).

<a id="calendar-prop-first_weekday"></a>**first_weekday** : Time.Weekday \[default: Time.WEEKDAY_MONDAY]
>The weekday considered the first day of the week. Uses `Time.Weekday` where `Sunday = 0` and `Saturday = 6`.

<a id="calendar-prop-week_number_system"></a>**week_number_system** : WeekNumberSystem \[defalt: WeekNumberSystem.WEEK_NUMBER_FOUR_DAY]
>Which system to use when calculating week numbers. See [WeekNumberSystem](#calendar-enumerations).


## Method Descriptions

<a id="calendar-method-get_calendar_month"></a>**get_calendar_month(year: int, month: int, include_adjacent_days: bool = false, force_six_weeks: bool = false)** : Array  
>Returns an array of weeks, where each week is an array of `Date` objects for the given month.  
>`include_adjacent_days` includes days from the previous/next month in the outer weeks; otherwise those slots are `0`.  
>`force_six_weeks` ensures the month is represented using six weeks for consistent grid layouts.

<a id="calendar-method-get_calendar_week"></a>**get_calendar_week(year: int, month: int, day: int, days_in_week: int = 7)** : Array\[Date].   
>Returns a `Date` array for the week that contains the given date. `days_in_week` can be shorter (for workweeks, etc.).

<a id="calendar-method-get_calendar_year"></a>**get_calendar_year(year: int, include_adjacent_days: bool = false, force_six_weeks: bool = true)** : Array.   
>Returns an array of months for the year. Each month is an array of weeks of `Date` objects.  
>`include_adjacent_days` and `force_six_weeks` behave like in `get_calendar_month`.

<a id="calendar-method-get_date_formatted"></a>**get_date_formatted(year: int, month: int, day: int, format: String = '%Y-%m-%d')** : String.   
>Returns a formatted string for the given date using a POSIX-like pattern. Supported placeholders include:  
>`%Y` four-digit year, `%y` two-digit year, `%-y` two-digit no pad, `%m` zero-padded month, `%-m` month, `%d` zero-padded day, `%-d` day, `%F` ISO8601 date, `%B`/`%b`/`%-b` month names via `CalendarLocale`, `%A`/`%a`/`%-a` weekday names via `CalendarLocale`, `%j`/`%-j` day of year, `%u` ISO weekday (Mon=1), `%w` weekday (Sun=0).

<a id="calendar-method-get_date_locale_format"></a>**get_date_locale_format(year: int, month: int, day: int, four_digit_year: bool = true)** : String.   
>Formats the date using the active `CalendarLocale`'s `date_format` and `divider_symbol`.  
See [CalendarLocale](#calendarlocale).

<a id="calendar-method-get_day_of_year"></a>**get_day_of_year(year: int, month: int, day: int)** : int.   
>Returns the ordinal day index of the year.

<a id="calendar-method-get_days_in_month"></a>**get_days_in_month(year: int, month: int)** : int.   
>Returns the number of days in the given month. February returns `29` in leap years.

<a id="calendar-method-get_days_in_year"></a>**get_days_in_year(year: int)** : int.   
>Returns `365` or `366` depending on leap year status.

<a id="calendar-method-get_days_of_range"></a>**get_days_of_range(days: int, year: int, month: int, day: int, exclusive: bool = false)** : Array\[Date].   
>Returns a sequence of `Date` objects spanning `days`, starting from the given date.  
>If `exclusive` is `true`, the last day is included in the range length.

<a id="calendar-method-get_leap_days"></a>**get_leap_days(from_year: int, to_year: int, exclusive_to: bool = true)** : int.   
>Returns the number of leap days between `from_year` and `to_year`. If `exclusive_to` is `false`, includes `to_year`.

<a id="calendar-method-get_month_formatted"></a>**get_month_formatted(month: int, month_format: MonthFormat = 1)** : String.   
>Returns the localized month name for `month` (`1–12`), formatted per `MonthFormat`.  
See [MonthFormat](#calendar-enumerations) and [CalendarLocale](#calendarlocale).

<a id="calendar-method-get_months_formatted"></a>**get_months_formatted(month_format: MonthFormat = 1)** : Array\[String].   
>Returns all month names in order using `month_format`.

<a id="calendar-method-get_today"></a>**get_today()** : Date.   
>Returns the current date as a `Calendar.Date`.

<a id="calendar-method-get_week_number"></a>**get_week_number(year: int, month: int, day: int)** : int.   
>Returns the week number for the given date, using the configured `week_number_system`.  
See [WeekNumberSystem](#calendar-enumerations).

<a id="calendar-method-get_weekday"></a>**get_weekday(year: int, month: int, day: int)** : Time.Weekday.   
>Returns the weekday for the date (`Sunday = 0 ... Saturday = 6`).

<a id="calendar-method-get_weekday_formatted"></a>**get_weekday_formatted(year: int, month: int, day: int, weekday_format: WeekdayFormat = 0)** : String.   
>Returns the localized weekday name using `weekday_format`.  
See [WeekdayFormat](#calendar-enumerations) and [CalendarLocale](#calendarlocale).

<a id="calendar-method-get_weekdays"></a>Weekday] **get_weekdays()** : Array\[Time.   
>Returns all weekdays starting from `first_weekday`.

<a id="calendar-method-get_weekdays_formatted"></a>**get_weekdays_formatted(weekday_format: WeekdayFormat = 1)** : Array\[String].   
>Returns weekday names starting at `first_weekday`, formatted by `weekday_format`.

<a id="calendar-method-get_weeks_of_month"></a>**get_weeks_of_month(year: int, month: int, force_six_weeks: bool = false)** : Array\[int].   
>Returns all week numbers present in the month.  
>`force_six_weeks` ensures a six-row layout alignment across months.

<a id="calendar-method-is_leap_year"></a>**is_leap_year(year: int)** : bool.   
>Returns whether `year` is a leap year.

<a id="calendar-method-set_calendar_locale"></a>**set_calendar_locale(path: String)** : void.   
>Assigns a `CalendarLocale` resource to the calendar.

<a id="calendar-method-set_first_weekday"></a>**set_first_weekday(first_weekday: Time.Weekday)** : void.   
>Sets the first day of the week for the calendar.

<a id="calendar-method-set_week_number_system"></a>**set_week_number_system(week_number_system: WeekNumberSystem)** : void.   
>Sets the week numbering system. See [WeekNumberSystem](#calendar-enumerations).

---

# <a id="calendar-date"></a>Calendar.Date
Inherits: `RefCounted < Object`

**A utility class for storing and handling dates.**

## Description
Calendar.Date holds a specific date composed of year, month, and day. It is used throughout Calendar wherever a full date object is required.

## Properties
**[day](#date-prop-day)** : int  
**[month](#date-prop-month)** : int  
**[year](#date-prop-year)** : int  

## Methods
[add_days](#date-method-add_days)(days: int) : void  
[add_months](#date-method-add_months)(months: int) : void  
[add_years](#date-method-add_years)(years: int) : void  
[days_to](#date-method-days_to)(date: Date) : int  
[duplicate](#date-method-duplicate)() : Date  
[from_dict](#date-method-from_dict)(date: Dictionary) : void  
[get_day_of_year](#date-method-get_day_of_year)() : int  
[get_weekday](#date-method-get_weekday)() : Time.Weekday  
[get_weekday_iso](#date-method-get_weekday_iso)() : int  
[is_after](#date-method-is_after)(date: Date) : bool  
[is_before](#date-method-is_before)(date: Date) : bool  
[is_equal](#date-method-is_equal)(date: Date) : bool  
[is_leap_year](#date-method-is_leap_year)() : bool  
[is_valid](#date-method-is_valid)() : bool  
[set_date](#date-method-set_date)(year: int, month: int, day: int) : void  
[set_today](#date-method-set_today)() : void  
[subtract_days](#date-method-subtract_days)(days: int) : void  
[subtract_months](#date-method-subtract_months)(months: int) : void  
[subtract_years](#date-method-subtract_years)(years: int) : void  
[today](#date-method-today)() : Date (static)  

## Property Descriptions

<a id="date-prop-day"></a>**day** : int  
>The day of this date. Valid range: `1–31` depending on the month.

<a id="date-prop-month"></a>**month** : int  
>The month of this date (`1–12`) representing January–December.

<a id="date-prop-year"></a>**year** : int  
>The year of this date.

## Method Descriptions

<a id="date-method-add_days"></a>**add_days(days: int)** : void  
>Adds `days` to this date.

<a id="date-method-add_months"></a>**add_months(months: int)** : void  
>Adds `months` to this date. If the target month has fewer days, the day is clamped to the last valid day.  
>February 29 becomes February 28 in non-leap years.

<a id="date-method-add_years"></a>**add_years(years: int)** : void  
>Adds `years` to this date. February 29 becomes February 28 if the resulting year is not a leap year.

<a id="date-method-days_to"></a>**days_to(date: Date)** : int  
>Returns the number of days between this date and `date`. Accurate for dates after 1582.

<a id="date-method-duplicate"></a>**duplicate()** : Date  
>Returns a new `Date` copy of this date.

<a id="date-method-from_dict"></a>**from_dict(date: Dictionary)** : void  
>Sets this date from a dictionary containing `year`, `month`, and `day`. Intended to convert dictionaries returned by `Time`.

<a id="date-method-get_day_of_year"></a>**get_day_of_year()** : int  
>Returns the ordinal day index of the year.

<a id="date-method-get_weekday"></a>**get_weekday()** : Time.Weekday  
>Returns the weekday (`Sunday = 0 ... Saturday = 6`).

<a id="date-method-get_weekday_iso"></a>**get_weekday_iso()** : int  
>Returns ISO weekday number (`Monday = 1 ... Sunday = 7`).

<a id="date-method-is_after"></a>**is_after(date: Date)** : bool  
>Returns whether this date is after `date`.

<a id="date-method-is_before"></a>**is_before(date: Date)** : bool  
>Returns whether this date is before `date`.

<a id="date-method-is_equal"></a>**is_equal(date: Date)** : bool  
>Returns whether this date is equal to `date`.

<a id="date-method-is_leap_year"></a>**is_leap_year()** : bool  
>Returns whether this date's year is a leap year.

<a id="date-method-is_valid"></a>**is_valid()** : bool  
>Returns whether this date is a valid calendar date.

<a id="date-method-set_date"></a>**set_date(year: int, month: int, day: int)** : void  
>Sets the year, month, and day of this date. Errors if the date is invalid.

<a id="date-method-set_today"></a>**set_today()** : void  
>Sets this date to today's system date.

<a id="date-method-subtract_days"></a>**subtract_days(days: int)** : void  
>Subtracts `days` from this date.

<a id="date-method-subtract_months"></a>**subtract_months(months: int)** : void  
>Subtracts `months` from this date. If the target month has fewer days, the day is clamped to the last valid day.  
>February 29 becomes February 28 in non-leap years.

<a id="date-method-subtract_years"></a>**subtract_years(years: int)** : void  
>Subtracts `years` from this date. February 29 becomes February 28 if the resulting year is not a leap year.

<a id="date-method-today"></a>**today()** : Date (static)  
>Returns a new `Calendar.Date` set to today's system date.

---

# <a id="calendarlocale"></a>CalendarLocale
Inherits: `Resource < RefCounted < Object`

**A resource to define localized names for weekdays and months.**

## Description
CalendarLocale is used by Calendar to provide localized weekday and month naming and formatting. Create and assign a CalendarLocale to a Calendar instance to localize output.

## Properties
**Month Names (full)**  
**[january](#locale-prop-january)** : String  
**[february](#locale-prop-february)** : String  
**[march](#locale-prop-march)** : String  
**[april](#locale-prop-april)** : String  
**[may](#locale-prop-may)** : String  
**[june](#locale-prop-june)** : String  
**[july](#locale-prop-july)** : String  
**[august](#locale-prop-august)** : String  
**[september](#locale-prop-september)** : String  
**[october](#locale-prop-october)** : String  
**[november](#locale-prop-november)** : String  
**[december](#locale-prop-december)** : String  

**Month Names (abbreviated)**  
**[abbr_january](#locale-prop-abbr_january)** : String  
**[abbr_february](#locale-prop-abbr_february)** : String  
**[abbr_march](#locale-prop-abbr_march)** : String  
**[abbr_april](#locale-prop-abbr_april)** : String  
**[abbr_may](#locale-prop-abbr_may)** : String  
**[abbr_june](#locale-prop-abbr_june)** : String  
**[abbr_july](#locale-prop-abbr_july)** : String  
**[abbr_august](#locale-prop-abbr_august)** : String  
**[abbr_september](#locale-prop-abbr_september)** : String  
**[abbr_october](#locale-prop-abbr_october)** : String  
**[abbr_november](#locale-prop-abbr_november)** : String  
**[abbr_december](#locale-prop-abbr_december)** : String  

**Month Names (short)**  
**[short_january](#locale-prop-short_january)** : String  
**[short_february](#locale-prop-short_february)** : String  
**[short_march](#locale-prop-short_march)** : String  
**[short_april](#locale-prop-short_april)** : String  
**[short_may](#locale-prop-short_may)** : String  
**[short_june](#locale-prop-short_june)** : String  
**[short_july](#locale-prop-short_july)** : String  
**[short_august](#locale-prop-short_august)** : String  
**[short_september](#locale-prop-short_september)** : String  
**[short_october](#locale-prop-short_october)** : String  
**[short_november](#locale-prop-short_november)** : String  
**[short_december](#locale-prop-short_december)** : String  

**Weekday Names (full)**  
**[sunday](#locale-prop-sunday)** : String  
**[monday](#locale-prop-monday)** : String  
**[tuesday](#locale-prop-tuesday)** : String  
**[wednesday](#locale-prop-wednesday)** : String  
**[thursday](#locale-prop-thursday)** : String  
**[friday](#locale-prop-friday)** : String  
**[saturday](#locale-prop-saturday)** : String  

**Weekday Names (abbreviated)**  
**[abbr_sunday](#locale-prop-abbr_sunday)** : String  
**[abbr_monday](#locale-prop-abbr_monday)** : String  
**[abbr_tuesday](#locale-prop-abbr_tuesday)** : String  
**[abbr_wednesday](#locale-prop-abbr_wednesday)** : String  
**[abbr_thursday](#locale-prop-abbr_thursday)** : String  
**[abbr_friday](#locale-prop-abbr_friday)** : String  
**[abbr_saturday](#locale-prop-abbr_saturday)** : String  

**Weekday Names (short)**  
**[short_sunday](#locale-prop-short_sunday)** : String  
**[short_monday](#locale-prop-short_monday)** : String  
**[short_tuesday](#locale-prop-short_tuesday)** : String  
**[short_wednesday](#locale-prop-short_wednesday)** : String  
**[short_thursday](#locale-prop-short_thursday)** : String  
**[short_friday](#locale-prop-short_friday)** : String  
**[short_saturday](#locale-prop-short_saturday)** : String  

**Formatting Settings**  
**[date_format](#locale-prop-date_format)** : int  
**[divider_symbol](#locale-prop-divider_symbol)** : String  

## Property Descriptions

### Month Names (full)

<a id="locale-prop-january"></a>**january** : String \[default: 'January']  

<a id="locale-prop-february"></a>**february** : String \[default: 'February']  

<a id="locale-prop-march"></a>**march** : String \[default: 'March']  

<a id="locale-prop-april"></a>**april** : String \[default: 'April']  

<a id="locale-prop-may"></a>**may** : String \[default: 'May']  

<a id="locale-prop-june"></a>**june** : String \[default: 'June']  

<a id="locale-prop-july"></a>**july** : String \[default: 'July']  

<a id="locale-prop-august"></a>**august** : String \[default: 'August']  

<a id="locale-prop-september"></a>**september** : String \[default: 'September']  

<a id="locale-prop-october"></a>**october** : String \[default: 'October']  

<a id="locale-prop-november"></a>**november** : String \[default: 'November']  

<a id="locale-prop-december"></a>**december** : String \[default: 'December']  


### Month Names (abbreviated)

<a id="locale-prop-abbr_january"></a>**abbr_january** : String \[default: 'Jan']  

<a id="locale-prop-abbr_february"></a>**abbr_february** : String \[default: 'Feb']  

<a id="locale-prop-abbr_march"></a>**abbr_march** : String \[default: 'Mar']  

<a id="locale-prop-abbr_april"></a>**abbr_april** : String \[default: 'Apr']  

<a id="locale-prop-abbr_may"></a>**abbr_may** : String \[default: 'May']  

<a id="locale-prop-abbr_june"></a>**abbr_june** : String \[default: 'Jun']  

<a id="locale-prop-abbr_july"></a>**abbr_july** : String \[default: 'Jul']  

<a id="locale-prop-abbr_august"></a>**abbr_august** : String \[default: 'Aug']  

<a id="locale-prop-abbr_september"></a>**abbr_september** : String \[default: 'Sep']  

<a id="locale-prop-abbr_october"></a>**abbr_october** : String \[default: 'Oct']  

<a id="locale-prop-abbr_november"></a>**abbr_november** : String \[default: 'Nov']  

<a id="locale-prop-abbr_december"></a>**abbr_december** : String \[default: 'Dec']  


### Month Names (short)

<a id="locale-prop-short_january"></a>**short_january** : String \[default: 'J']  

<a id="locale-prop-short_february"></a>**short_february** : String \[default: 'F']  

<a id="locale-prop-short_march"></a>**short_march** : String \[default: 'M']  

<a id="locale-prop-short_april"></a>**short_april** : String \[default: 'A']  

<a id="locale-prop-short_may"></a>**short_may** : String \[default: 'M']  

<a id="locale-prop-short_june"></a>**short_june** : String \[default: 'J']  

<a id="locale-prop-short_july"></a>**short_july** : String \[default: 'J']  

<a id="locale-prop-short_august"></a>**short_august** : String \[default: 'A']  

<a id="locale-prop-short_september"></a>**short_september** : String \[default: 'S']  

<a id="locale-prop-short_october"></a>**short_october** : String \[default: 'O']  

<a id="locale-prop-short_november"></a>**short_november** : String \[default: 'N']  

<a id="locale-prop-short_december"></a>**short_december** : String \[default: 'D']  


### Weekday Names (full)

<a id="locale-prop-sunday"></a>**sunday** : String \[default: 'Sunday']  

<a id="locale-prop-monday"></a>**monday** : String \[default: 'Monday']  

<a id="locale-prop-tuesday"></a>**tuesday** : String \[default: 'Tuesday']  

<a id="locale-prop-wednesday"></a>**wednesday** : String \[default: 'Wednesday']  

<a id="locale-prop-thursday"></a>**thursday** : String \[default: 'Thursday']  

<a id="locale-prop-friday"></a>**friday** : String \[default: 'Friday']  

<a id="locale-prop-saturday"></a>**saturday** : String \[default: 'Saturday']  


### Weekday Names (abbreviated)

<a id="locale-prop-abbr_sunday"></a>**abbr_sunday** : String \[default: 'Sun']  

<a id="locale-prop-abbr_monday"></a>**abbr_monday** : String \[default: 'Mon']  

<a id="locale-prop-abbr_tuesday"></a>**abbr_tuesday** : String \[default: 'Tue']  

<a id="locale-prop-abbr_wednesday"></a>**abbr_wednesday** : String \[default: 'Wed']  

<a id="locale-prop-abbr_thursday"></a>**abbr_thursday** : String \[default: 'Thu']  

<a id="locale-prop-abbr_friday"></a>**abbr_friday** : String \[default: 'Fri']  

<a id="locale-prop-abbr_saturday"></a>**abbr_saturday** : String \[default: 'Sat']  


### Weekday Names (short)

<a id="locale-prop-short_sunday"></a>**short_sunday** : String \[default: 'S']  

<a id="locale-prop-short_monday"></a>**short_monday** : String \[default: 'M']  

<a id="locale-prop-short_tuesday"></a>**short_tuesday** : String \[default: 'T']  

<a id="locale-prop-short_wednesday"></a>**short_wednesday** : String \[default: 'W']  

<a id="locale-prop-short_thursday"></a>**short_thursday** : String \[default: 'T']  

<a id="locale-prop-short_friday"></a>**short_friday** : String \[default: 'F']  

<a id="locale-prop-short_saturday"></a>**short_saturday** : String \[default: 'S']  


### Formatting Settings

<a id="locale-prop-date_format"></a>**date_format** : int \[default: 0]  
>The standard date format index for the locale. Use `Calendar.get_date_locale_format()` to format dates.

<a id="locale-prop-divider_symbol"></a>**divider_symbol** : String \[default: '-']  
>Symbol dividing year, month, and day in the locale's date format.
