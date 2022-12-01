# 2022년 12월  

## TIL20221201  

### RStudio에서 tibble로 출력 시 pretty floating point numbers로 소수점 잘려서 출력됨

```r
df %>%
    summarise(mean = mean(body_mass_g)) %>%
    as.data.frame() # 소수점 이하 정상출력을 위해
```
