# Soru 1) 1980’den itibaren spor grubu bazında en çok madalya alan 1. 3. 5. ülkeyi bulalım.

```SQL

with after1980 as
(
  select
    sport,
    country,
    COUNT(1) as countMedals,
  from burak_intisah.summer_medals
  where year >= 1980
  Group By Sport,country
  Order by sport,countMedals DESC
)
Select Distinct sport,
first_value(country) over(partition by sport order by countMedals DESC range between unbounded preceding and unbounded following) as country_rank1,
nth_value(country,3) over(partition by sport order by countMedals DESC range between unbounded preceding and unbounded following) as country_rank3,
nth_value(country,5) over(partition by sport order by countMedals DESC range between unbounded preceding and unbounded following) as country_rank5,
  from after1980
  
```
