<h2>Compare Ingress Controllers Performance with Azure DevOps Load Test</h2>

Let's see which Ingress Controller has better performance rather than others.</br>
We will use Azure DevOps to testing performances of ingress controllers.</br>
First we need to define load test scenarios on Azure DevOps.</br>
Our Load Test Scenario is designed as instantly 1000 users in 2 minutes for all ingress types.</br></br>

This is sample scenario for nginx-ingress. 
![Load_Test_Scenario_Sample](https://github.com/tayyip61/aks-ingress-loadtest/blob/master/nginx-ingress-loadtest.png)

After that we should add 2 more scenarios for traefik-ingress and contour-ingress.</br>
Then, let's run test and examine results.

<h4>Nginx Ingress Controller Load Test Summary</h4>

![nginx_Ingress_LoadTest_Summary](https://github.com/tayyip61/aks-ingress-loadtest/blob/master/nginx-ingress-loadtest-1.PNG)

<h4>Nginx Ingress Controller Load Test Chart Details</h4>

![nginx_Ingress_LoadTest_Summary](https://github.com/tayyip61/aks-ingress-loadtest/blob/master/nginx-ingress-loadtest-2.PNG)


<h4>Traefik Ingress Controller Load Test Summary</h4>

![nginx_Ingress_LoadTest_Summary](https://github.com/tayyip61/aks-ingress-loadtest/blob/master/traefik-ingress-loadtest-1.PNG)

<h4>Traefik Ingress Controller Load Test Chart Details</h4>

![nginx_Ingress_LoadTest_Summary](https://github.com/tayyip61/aks-ingress-loadtest/blob/master/traefik-ingress-loadtest-2.PNG)


<h4>Contour Ingress Controller Load Test Summary</h4>

![nginx_Ingress_LoadTest_Summary](https://github.com/tayyip61/aks-ingress-loadtest/blob/master/contour-ingress-loadtest-1.PNG)

<h4>Contour Ingress Controller Load Test Chart Details</h4>

![nginx_Ingress_LoadTest_Summary](https://github.com/tayyip61/aks-ingress-loadtest/blob/master/contour-ingress-loadtest-2.PNG)


<b>Summary</b></br>
We can see the Average Response Times for each ingress controllers.</br>
According to test results, it is obvious which ingress controller type has best performance for load balancing.</br>
Contour Ingress Controller has lowest average response time with 5.7 ms.</br>
Then, Traefik Ingress Conroller has the second lowest average response time with 7.5 ms.</br>
Finally, Nginx Ingress Controller has the highest average response time with 11 ms.</br>
