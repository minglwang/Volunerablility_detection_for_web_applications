# Web_application_vulnerability_detection
> Time based algorithm to detect the vulnerability of SQL injection attacks
<p align ="center">
  <img width ="400" height ="300", src = https://github.com/minglwang/Web_App_Vulnerability_Detection/blob/master/confidence%20interval.png>
</p>  

# Table of Content
- [Description](#discription)
- [Network delay data analysis](#network_delay_data_analysis)
- [Solutions](#solutions)
- [How To Use](#how-to-use)

# Description
**Blind SQL injections** are time-based SQL attacks that request web applications to sleep for a specified amount of time (*Sleep time*). Typically, the response time to url request in **vulnerable web applications will be affected** by the SQL attacks **while safe web application will not**. In addition, the response time is contaiminated by the *network delay*. 
Therefore, for a safe web application,

> *Response time = network delay*,

while for a vulnerable web application,

> *Response time = Sleep time + network delay*,

where *network delay* is a stochastic phenonmenon in the trassmission bettween the server and local user. Using the response time to classify a web application as safe or not will result in **false positive** (type I error) which means we classify the safe web application as a vulnerable one due to the stochastic *network delay*. 

# Network delay data analysis
To get the network delay data, we
1. send N (N = 20 in this case) requests to the safe and vulnerable web application, 10 for each,
2. Record the response time of each request.

An dataset for understanding the network delay is stored in network delay.txt" which is composed by two columns: column 1 is urls which are in string type and column 2 is the response times which are real numbers.
An example of the log is like this:
<p align="center">  
  <img width = "400", height = "60" src = "https://user-images.githubusercontent.com/45757826/57514015-d367a700-730f-11e9-9ee3-67fc1962e8bf.png">
</p>

  A plot of data is given in Fig. 1 which shows network delays exist in both safe and vulnerable and varied in each request. This indicates the stochastic nature of the network delay. The statistics of the data are given in Tab. 1
from which we see the statistics of network delays in requesting the two urls are close. This means the network delays are independent of the types of web application we request. Now, we can assume the network work delay follows a certain probability distribution.

<p align="center">  
  <img width = "550", height = "250" src = "https://user-images.githubusercontent.com/45757826/57514329-86d09b80-7310-11e9-8b2e-f15e0eac38c0.png">
</p>
Figure 1. Network delay data and the histogram

<p align="center">  
  <img width = "400", height = "110" src = "https://user-images.githubusercontent.com/45757826/57515548-39096280-7313-11e9-8130-2d290a36af30.png">
</p>

# Solutions

The response times of safe and volunerable web applications are studied by sending differet type of requests (normal and attactive) 
The data of response time is presented in Fig. 2.
<p align="center">  
  <img width = "600", height = "250" src = "https://user-images.githubusercontent.com/45757826/57514987-ec715780-7311-11e9-9fd2-0803d983da1a.png">
</p>
Figure 2. Boxplot of response times

##### The hypothesises for this problem are 

- Null hypothesis: "The web application is safe".

- Alternative hypothesis: "The web application is vulnerable".

To deal with the false positive problem and make sure the is online appliable, we designed a time-based algorithm such that **the false positive rate** less than a small positive value, e.g. 0.01% and can be **completed within a few seconds**. 

Two approaches are developed
1. a t-test approach
2. a Chi-square test approach. 

The technical details of the two approaches are explained in 
[report file](https://github.com/minglwang/Web_App_Vulnerability_Detection/blob/master/Mingliang_Report.pdf). 

The results of the two approaches are summaried in Tab. 2 and Tab.3.

<p align="center">  
  <img width = "450", height = "100" src = "https://user-images.githubusercontent.com/45757826/57515907-fa27dc80-7313-11e9-8e92-e2c7f0f649f1.png">
</p>
<p align="center">  
  <img width = "450", height = "100" src = "https://user-images.githubusercontent.com/45757826/57515942-07dd6200-7314-11e9-9a0b-cccd80af69ae.png">
</p>

Both approaches contain sampling the *stochastic network delay* which may take 1 or 2 minutes. This sampling can be done offline.
The t-test approach takes about 30 seconds which is too long for online usage.
The advantage of Chi-square test is that it require only one sample of the response time which will **complete within a few seconds** and maintain the **the false positive rate** at the same time.

# How To Use
To use the code, one need to 

1. run "app.py" using spider ("app.py" is a Python code simulating the web applications (both safe and unsafe ones).
2. open a new console to run the t test or chi_square test in the IPython console panel,.
3. run the "t_test.py" to run the t-test approach
4. run the "chi_square_test.py" to run the proposed chi-square test approach 

[Back To The Top](#Web_application_vulnerability_detection)

