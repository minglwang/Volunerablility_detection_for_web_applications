# Vulnerability detection of web-applications
Time based algorithm to detect the vulnerability of SQL injection detection
Blind SQL injections are time-based SQL attacks that ask web applications to sleep for a specified amount of time. Typically, the response time of vulnerable web applications will be affected by such attacks while the response time of safe web application will not. However, the response time is contaiminated by the stochastic network delay. So the time-based algorithm will result in false positive decisions which mean we classify the safe web application as a vulnerable one. To deal with the false positive problem, the challenge is to design a time-based algorithm such that the false positive rate is less than 10^(-6) and the test should be completed within a few seconds.

Two solution is proposed: a t-test approach and a chi-square approach. The details of the algorithms can be found in the report file. 

The Python codes are given: solution.py for the t-test approach and solution2.py for the chi-square test approach.
"app.py" is the python code for a simulated web application.
