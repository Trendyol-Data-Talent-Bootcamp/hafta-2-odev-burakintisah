# 3) Bu çalışmada çıkarmak istediğimiz bilgi, günün her bir dakikası için aktif kullanıcı sayısının hesaplanması.

```SQL
with temp1 as (
  select timestamp_trunc(view_ts, minute) as eachMinute,
  count(distinct deviceid) active_user_count,
  from burak_intisah.pageview
  group by eachMinute
  order by eachMinute
)
select eachMinute,
sum(active_user_count) over (rows between 4 preceding and current row) as total
from temp1 

```

Bu query de her gun gelen dataları topladıgım için aynı device id de gelen 4 gun ust usteki dataları tekrar tekrar topluyorum.
O yuzden hata oldugunun farkındayım ama tekrar duzenleme fırsatım olmadı.
