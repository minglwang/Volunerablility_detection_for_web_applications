# Web_application_vulnerability_detection
> Time based algorithm to detect the vulnerability of SQL injection attacks
<p align ="center">
  <img width ="400" height ="300", src = https://github.com/minglwang/Web_App_Vulnerability_Detection/blob/master/confidence%20interval.png>
</p>  

# Table of Content
- [Description](#discription)
- [Network delay data analysis](#data_analysis)
- [Solutions](#solutions)
- [How To Use](#how-to-use)

# Description
**Blind SQL injections** are time-based SQL attacks that request web applications to sleep for a specified amount of time (*Sleep time*). Typically, the response time to url request in **vulnerable web applications will be affected** by such SQL attacks **while safe web application will not**. However, the response time is also contaiminated by the *network delay*. Therefore,
for a safe web application,

> *Response time = network delay*,

while for a vulnerable web application,

> *Response time = Sleep time + network delay*,

where *network delay* is a stochastic phenonmenon in the trassmission bettween the server and local user. Using the response time to classify a web application as safe or not will result in **false positive** (type I error, which means we classify the safe web application as a vulnerable one) due to stochastic *network delay*. 

# Network delay data analysis
To get the network delay data, we
1. send N (N = 20 in this case) requests to the safe and vulnerable web application, 10 for each,
2. Record the response time of each request.

An dataset for understanding the network delay is stored in network delay.txt" which composed by two columns: column 1 is urls which are in string type and column 2 is the response times which are real numbers.
An example of the log is like this:
<p align="center">  
  <img width = "400", height = "60" src = "https://user-images.githubusercontent.com/45757826/57514015-d367a700-730f-11e9-9ee3-67fc1962e8bf.png">
</p>

  
  A plot of data is given in Fig. 1 which shows network delays exist in both safe and vulnerable and varied in each request. This indicates the stochastic nature of the network delay. The statistics of the data are given in Tab. 1
from which we see the statistics of network delays in requesting the two urls are close. This means the network delays are independent of the types of web application we request. Now, we can assume the network work delay follows a certain probability distribution.

<p align="center">  
  <img width = "600", height = "300" src = "https://user-images.githubusercontent.com/45757826/57514329-86d09b80-7310-11e9-8b2e-f15e0eac38c0.png">
</p>

# Solutions

To deal with the false positive problem and make sure the is online appliable, we designed a time-based algorithm such that **the false positive rate** less than a small positive value, e.g. 0.01% and can be **completed within a few seconds**. 

Two approaches are developed
1. a t-test approach
2. Chi-square test approach. 

Both approaches contain sampling the *stochastic network delay* which may take 1 or 2 minutes. This sampling can do offline.
The t-test approach takes about 30 seconds which is too long for online usage.
The advantage of Chi-square test is that it require only one sample of the response time which will **complete within a few seconds** and maintain the **the false positive rate** at the same time.

The basic ideas of the two approaches are explained in 
[report file](https://github.com/minglwang/Web_App_Vulnerability_Detection/blob/master/Mingliang_Report.pdf). 

# How To Use
To use the code, one need to 

1. run "app.py" using spider ("app.py" is a Python code simulating the web applications (both safe and unsafe ones).
2. In the IPython console panel, open a new consol panel to run the t test or chi_square test.
2. run the "t_test.py" to run the t-test approach
3. run the "chi_square_test.py" to run the proposed chi-square test approach 

[Back To The Top](#Web_application_vulnerability_detection)

