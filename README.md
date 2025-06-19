**Part 1：The calculation methods of different time sequences occurrence probabilities in the manuscript**

#3-1
import scipy.integrate as integrate
import numpy as np
def f(t1, t2, t3):
    x1=3.2267*10**(-6)*np.exp(-3.2257*10**(-6)*t1)
    x2 =2.1812*10**(-6)*np.exp(-2.1812*10**(-6)*t2)
    x3=1/1000000
    fx=x1*x2*x3
    return fx


def inner_integral(t3):
    def inner_innermost(t2):
        upper_limit = t3 - t2
        return integrate.quad(lambda t1: f(t1, t2, t3), 0, upper_limit)[0] 
    return integrate.quad(inner_innermost, 0, t3)[0]
    
result = integrate.quad(inner_integral, 0, 5000)[0]
print("三重积分的值为:", result)

D:\桌面\高度测量\venv\Scripts\python.exe D:/桌面/高度测量/test.py 

三重积分的值为: 1.456395059004462e-07

进程已结束,退出代码0

#3-2
import scipy.integrate as integrate
import numpy as np

def f(t1, t2, t3):
    x1=3.2267*10**(-6)*np.exp(-3.2267*10**(-6)*t1)
    x2 =2.1812*10**(-6)*np.exp(-2.1812*10**(-6)*t2)
    x3=1/1000000
    fx=x1*x2*x3
    return fx

def inner_integral(t2):
    def inner_innermost(t1):
        upper_limit = t2 + t1
        return integrate.quad(lambda t3: f(t1, t2, t3), 0, upper_limit)[0]
    return integrate.quad(inner_innermost, 0, 5000-t2)[0]
result = integrate.quad(inner_integral, 0, 5000)[0]
print("三重积分的值为:", result)

D:\桌面\高度测量\venv\Scripts\python.exe D:/桌面/高度测量/test.py 
三重积分的值为: 2.9029593713041986e-07
进程已结束,退出代码0

#3-3
import scipy.integrate as integrate
import numpy as np
def f2(t1, t2):
    x1=3.2267*10**(-6)*np.exp(-3.2267*10**(-6)*t1)
    x2 =2.1812*10**(-6)*np.exp(-2.1812*10**(-6)*t2)
    fx=x1*x2
    return fx
def inner_function(t2):
    upper_limit = 5000 - t2
    return integrate.quad(lambda t1: f2(t1, t2), 0, upper_limit)[0]
result1 = integrate.quad(inner_function, 0, 5000)[0]

def f3(t3):
    return 1/1000000
result21 = integrate.quad(lambda t3: f3(t3), 0, 5000)[0]
result2=1-result21
result=result1*result2
print("三重积分的值为:", result)

D:\桌面\高度测量\venv\Scripts\python.exe D:/桌面/高度测量/test.py 
三重积分的值为: 8.675115316314236e-05

进程已结束,退出代码0

#3-5
import scipy.integrate as integrate
import numpy as np
def f(t1, t2, t3):
    x1=3.2267 * 10 ** (-6)*np.exp(-3.2267 * 10 ** (-6)*t1)
    x2 =2.1812 * 10 ** (-6)*np.exp(-2.1812 * 10 ** (-6)*t2)
    x3=1/1000000
    fx=x1*x2*x3
    return fx

def inner_integral(t1):
    def inner_innermost(t2):
        return integrate.quad(lambda t3: f(t1, t2, t3), 0, t1)[0]
    return integrate.quad(inner_innermost, 5000-t1, 10000000)[0]
result = integrate.quad(inner_integral, 0, 5000)[0]
print("三重积分的值为:", result)
D:\桌面\高度测量\venv\Scripts\python.exe D:/桌面/高度测量/test.py 
三重积分的值为: 3.975749379070766e-05

进程已结束,退出代码0



2-3的积分代码
def inner_function(t2):
    upper_limit = 3000 - t2
    return integrate.quad(lambda t1: f2(t1, t2), 0, upper_limit)[0]# Compute result1 (double integral over t1 and t2)
result1 = integrate.quad(inner_function, 0, 3000)[0]

def f3(t3):
    return 1e-5 * np.exp(-1e-5 * t3)
result21 = integrate.quad(lambda t3: f3(t3), 0, 3000)[0]
result2=1-result21
result=result1*result2
print("三重积分的值为:", result)
print("三重积分的值为:", result1)

#4-1
def inner_integral(t5):
    def inner_inner(t4):
        def inner_innermost(t3):
            def innermost(t2):
                return integrate.quad(lambda t1: f1(t1, t2, t3, t4, t5),0, t5-t2-t3-t4)[0]
            return integrate.quad(innermost, 0, t5-t3-t4)[0]
        return integrate.quad(inner_innermost, 0, t5-t4)[0]
    return integrate.quad(inner_inner, 0, t5)[0]

result= integrate.quad(inner_integral, 0, 10000)[0]
print("五维积分的值:", result)

D:\桌面\高度测量\venv\Scripts\python.exe D:/桌面/高度测量/ASTAR/RA.py 
五维积分的值: 6.971966605300514e-17

进程已结束,退出代码0

#4-2
def inner_integral(t4):
    def inner_inner(t3):
        def inner_innermost(t2):
            def innermost(t1):
                return integrate.quad(lambda t5: f1(t1, t2, t3, t4, t5),0, t1+t2+t3+t4)[0]
            return integrate.quad(innermost, 0, 20000-t2-t3-t4)[0]
        return integrate.quad(inner_innermost, 0, 20000-t3-t4)[0]
    return integrate.quad(inner_inner, 0, 20000-t4)[0]

result= integrate.quad(inner_integral, 0, 20000)[0]
print("五维积分的值:", result)

D:\桌面\高度测量\venv\Scripts\python.exe D:/桌面/高度测量/ASTAR/RA.py 
五维积分的值: 3.5004529767293606e-16

进程已结束,退出代码0

#4-3
def f2(t1, t2, t3, t4):
    x1 = 10**(-9)
    x2 = (3.2257*10**(-6)*2.1802/(-3.2257+2.1802))* (np.exp(-3.2257*10**(-6) * t2)- np.exp(-2.1802*10**(-6)* t2))
    x3 = 2.32*10**(-6)* np.exp(-2.32*10**(-6)  * t3)
    x4 = 5*10**(-8) * np.exp(-5*10**(-8) * t4)
    return x1 * x2 * x3 * x4

def inner_inner(t4):
    def inner_innermost(t3):
        def innermost(t2):
            return integrate.quad(lambda t1: f2(t1, t2, t3, t4),0, 20000-t2-t3-t4)[0]
        return integrate.quad(innermost, 0, 20000-t3-t4)[0]
    return integrate.quad(inner_innermost, 0, 20000-t4)[0]

S1=integrate.quad(inner_inner, 0, 20000)[0]
S2=np.exp(-1*10**(-6)*20000)
result=S1*S2

#result= integrate.quad(inner_integral, 20000, 1000000000)[0]
print("五维积分的值:", result)
D:\桌面\高度测量\venv\Scripts\python.exe D:/桌面/高度测量/ASTAR/RA.py 
五维积分的值: 2.0779065308042953e-14

进程已结束,退出代码0

#4-5
def f5A(t1, t2, t5):
    x1 = 10**(-9)
    x2 = (3.2257*10**(-6)*2.1802/(-3.2257+2.1802))* (np.exp(-3.2257*10**(-6) * t2)- np.exp(-2.1802*10**(-6)* t2))
    x5 = 1 * 10 ** (-6) * np.exp(-1 * 10 ** (-6) * t5)
    return x1 * x2 * x5
def inner_innermost(t1):
    def innermost(t2):
        return integrate.quad(lambda t5: f5A(t1, t2, t5),0, t1)[0]
    return integrate.quad(innermost, 20000-t1, np.inf)[0]
result= integrate.quad(inner_innermost, 0, 20000)[0]
print("五维积分的值:", result)
D:\桌面\高度测量\venv\Scripts\python.exe D:/桌面/高度测量/ASTAR/RA.py 
五维积分的值: 1.9842740211160597e-07

进程已结束,退出代码0


#4-6
def inner_inner(t2):
    def inner_innermost(t1):
        def innermost(t3):
            return integrate.quad(lambda t5: f6A(t1, t2, t3,t5),0, t1)[0]
        return integrate.quad(innermost, 20000-t1-t2,100000000)[0]
    return integrate.quad(inner_innermost, 0, 20000-t2)[0]
result= integrate.quad(inner_inner, 0, 20000)[0]
print("五维积分的值:", result)
D:\桌面\高度测量\venv\Scripts\python.exe D:/桌面/高度测量/ASTAR/RA.py 
五维积分的值: 4.527950014621854e-11

进程已结束,退出代码0

**Part 2  The finite integration problem when the upper bound is not infinite**

As you can see, the upper limit integrals np.inf of some time series such as 4-5, 4-6, and 4-7 have been replaced with a maximum number.
Limited by the limited equipment，all tests are conducted on the PC with 3.40 GHz, 20G of running memory, Intel(R) Core(TM) i5-8250U Windows 10 system environment and PyCharm 2022.2 compilation environment.
Therefore, when np.inf is adopted as the upper limit of integration, the actual number of operations of the device may only be 10^5 to 10^6. 
Existing studies avoid differences in integration through the adaptive truncation error method. 
The authors change the order of magnitude of the upper limit of integration. When the integration result converges, the operation result is taken as the output result of integration.
