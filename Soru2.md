# Soru 2) 1980’den itibaren herhangi bir spor grubunda üst üste 3 veya daha fazla madalya almış atletleri bulalım.


```SQL

with after1980 as
(
  select
    sport,
    Athlete,
    year,
  from burak_intisah.summer_medals
  where year >= 1980 
  Group By Sport,Athlete,year
  Order by sport,Athlete,year DESC
)

select distinct a1.Athlete
from after1980 a1 inner join after1980 a2 on a1.Athlete = a2.Athlete and a2.year - 4 = a1.year
inner join after1980 a3 on a1.Athlete = a3.Athlete and a2.year = a3.year -4
order by a1.athlete

```

