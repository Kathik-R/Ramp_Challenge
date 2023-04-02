# Ramp_Challenge
A simple SQL Query that I was asked to solve

/* Provide January 31's rolling 3 day average of total transaction amount processed per day and provide the link to your solution. */

WITH day_wise_data AS(
  SELECT CAST(transaction_time AS DATE) AS transaction_date, 
  SUM(transaction_amount) AS t_amt
  FROM transactions
  WHERE transaction_time>='2021-01-29' AND transaction_time<'2021-02-01'
  GROUP BY CAST(transaction_time AS DATE)
)
SELECT *,

AVG(t_amt) OVER(ORDER BY transaction_date
      ROWS BETWEEN 2 PRECEDING AND CURRENT ROW )
     as three_day_moving_average
FROM day_wise_data
ORDER BY transaction_date
