![](https://github.com/yaowenqing/leetcode/blob/master/images/4.png)

### 代码

```
select Email from
(
  select Email, count(Email) as num
  from Person
  group by Email
) as statistic
where num > 1
;
```
