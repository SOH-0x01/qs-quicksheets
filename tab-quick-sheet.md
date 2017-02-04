

### Base helpers for quick table calculation tweaks
! Index Partiion: INDEX()						
! Is Partition Last: LAST()=0
! Is Partition First: FIST()=0


## Time Intelligence

[Date Dim] is your reference date
[Measure] is your raw measure

! Value Date (MIN):MIN([Date Dim])
! Value Date (MAX):MAX([Date Dim])
! Number of Weekdays:
DATEDIFF("weekday", [! Range Date (MIN)], [! Range Date (MAX)])
- 2 * (DATEPART('week', [! Range Date (MAX)]) - DATEPART('week', [! Range Date (MIN)]))
+ (IF DATENAME('weekday',[! Range Date (MAX)]) = 'Saturday' OR DATENAME('weekday',[! Range Date (MIN)]) = 'Sunday' THEN 0 ELSE 1 END)

### xTD: Periode to date
IF [Date Dim] <=TODAY() AND DATEDIFF('year',[Date Dim],Today())= 0 THEN [Measure] ELSE 0 END
IF [Date Dim] <=TODAY() AND DATEDIFF('quarter',[Date Dim],Today())= 0 THEN [Measure] ELSE 0 END
IF [Date Dim] <=TODAY() AND DATEDIFF('month',[Date Dim],Today())= 0 THEN [Measure] ELSE 0 END
IF [Date Dim] <=TODAY() AND DATEDIFF('week',[Date Dim],Today())= 0 THEN [Measure] ELSE 0 END

### MA: Moving Average (Assuming Periode = days)
WINDOW_AVG([Measure], DATEDIFF('day',[Date Dim],Today()), 0)

### x-1: Last periode relative (Within)
IF YEAR([Date Dim]) = YEAR(today)-1 THEN [Measure] ELSE 0 END

#### Within the same year
IF YEAR([Date Dim]) = YEAR(today) AND QUARTER([Date Dim]) = QUARTER(today)-1 THEN [Measure] ELSE 0 END
IF YEAR([Date Dim]) = YEAR(today) AND MONTH([Date Dim]) = MONTH(today)-1 THEN [Measure] ELSE 0 END
IF YEAR([Date Dim]) = YEAR(today) AND WEEK([Date Dim]) = WEEK(today)-1 THEN [Measure] ELSE 0 END

#### Accross years
IF QUARTER([Date Dim]) = QUARTER(today)-1 THEN [Measure] ELSE 0 END
IF MONTH([Date Dim]) = MONTH(today)-1 THEN [Measure] ELSE 0 END
IF WEEK([Date Dim]) = WEEK(today)-1 THEN [Measure] ELSE 0 END

### xTD-1 : Last year, same periode to date
IF YEAR([Date Dim]) = YEAR(today)-1 AND [Date Dim] <= DATEADD('year',TODAY(),-1) AND DATEDIFF('quarter',[Date Dim],Today())= 4 THEN [Measure] ELSE 0 END
IF YEAR([Date Dim]) = YEAR(today)-1 AND [Date Dim] <= DATEADD('year',TODAY(),-1) AND DATEDIFF('month',[Date Dim],Today())= 12 THEN [Measure] ELSE 0 END
IF YEAR([Date Dim]) = YEAR(today)-1 AND [Date Dim] <= DATEADD('year',TODAY(),-1) AND DATEDIFF('week',[Date Dim],Today())= 52 THEN [Measure] ELSE 0 END

### PIN: Point In Time Relative
### PIN: Two Point compare
