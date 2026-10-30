# K6 lab results
## Part 0
- Step 0.1, http_req_duration: avg=255.66ms min=255.66ms med=255.66ms max=255.66ms p(90)=255.66ms p(95)=255.66ms
- Step 0.2, requests, rate and p(95), and why the rate stays below 5: 80, 3.81876/s, p(95)=273.88ms. Because 1 iteration took around 1.3 second which mean the request rate per iteration is 1/1.3 which is only around 0.77.
- Step 0.6, exit code of the normal run and of the run with P95=300: 99
- Step 0.7, rules that passed, p(95), p(99), exit code after your change:✓ 'p(95)<1000', ✓ 'p(99)<1500', EXIT CODE: 0
- Step 0.8, what was wrong, and how the checks showed it: The letter sensitivity, in order first letter is the capital later but the code isn't, so the program not work correctly
## Part A results
| Step | Test type | Users | Req/s | p(95) | Max | Failed | Checks |
| ---- | ------------ | ----- | ----- | ----- | --- | ------ | ------ |
| A1 | Smoke | 1 | 0.487805/s | 342.07ms | 347.11ms | 0.00% | 100.00% |
| A2 | Average load | 3 | 1.277338/s | 371.78ms | 399.41ms  | 0.00% | 100.00% |
| A3 | Stress | 5 | 2.151944/s | 368.23ms | 396.7ms | 0.00% | 100.00% |
| A4 | Spike | 5 | 1.069336/s | 375.88ms | 394.72ms | 0.00% | 100.00% |
| A5 | Soak | 2 | 0.995876/s | 371.29ms | 644.58ms | 0.00% | 100.00% |
## Part B
1. In Part A result
2. Because 1 iteration took around 1.3 second which mean the request rate per iteration is 1/1.3 which is only around 0.77.
3. it change 371.78 ms to 368.23 ms which almost no change, because 5 users is still far inside the operational envelope.
4. It take around 10 seconds to come back.
5. No, it isn't, but a memory leak can be found after long soak test.
6. Because using the average will hide the slow requests while using p(95) shows what most users really get.
7. Because of network delay, and other people testing the same site at the same time.
8. Because it can take the site down for real users, like a DoS attack.
9. "LINE should load fast" becomes "with 50 users, 95% of requests finish within 500 ms and less than 1% fail": `thresholds: { http_req_duration: ['p(95)<500'], http_req_failed: ['rate<0.01'] }`.
