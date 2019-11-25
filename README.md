# xin_phd_study
Weekly summaries of Xin Zhang. Latest summaries come first.

## Date: 2019/11/18 – Weekly Summary

1. **Progress:**
	* run code https://github.com/BertMoons/QuantizedNeuralNetworks-Keras-Tensorflow on the server and get a rough result
	* CNN结构：若干Convolution Layer (ReLU) + pooling layer (no activation function) + fully connected layers(FC for short) + softmax..... (https://www.cnblogs.com/pinard/p/6483207.html)
	** Convolution Layer $ s(i,j) = (X*W)(i,j) = \sum_m \sum_n X(i+m,j+n)W(m,n) $
	
2. **Plan:**
  * 统计QNN代码的执行结果，并绘制图形
  #### 其他所有参数相同，bit数不同，横坐标epoch，总坐标精确度+时间
  #### bit数相同，网络层数和宽度不同
  * 学习chap2

## Date: 2019/11/18 – Weekly Summary

1. **Progress:**
	* Contect to server via Putty
	* learn a part of chap2 《深度学习框架PyTorch：入门与实践》
	
2. **Plan:**
  * run code https://github.com/BertMoons/QuantizedNeuralNetworks-Keras-Tensorflow on the server and get a rough result
  * learn chap2 and chap3, the more the better

## Date: 2019/11/13 – Weekly Summary

1. **Progress:**
	* learn the basic knowledge about DNN 
	* read paper about how to use limited-precision to train model.

2. **Plan:**
  * learn https://github.com/chenyuntc/pytorch-book/blob/master/chapter2-%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/chapter2:%20PyTorch%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8.ipynb
  * try to run some code about limited-precision

## Date: 2019/10/07 – Weekly Summary

1. **Progress:**
	* learn how to use OpenCV-python: OpenCV Python tutorial (https://www.youtube.com/watch?v=kdLM6AOd2vc&list=PLS1QulWo1RIa7D1O6skqDQ-JZ1GGHKK-K) and pysource (https://pysource.com/2018/01/31/object-detection-using-hsv-color-space-opencv-3-4-with-python-3-tutorial-9/)
	* OpenCV mannual (https://docs.opencv.org/4.1.1/)
	* See papers_and_notes/OpenCV for more information.

2. **Plan:**
  * Watch all the classes in youtube
  * Focus on Object detection

## Date: 2019/09/09 – Weekly Summary

1. **Progress:**
	* Read Paper DSN19' ML-based Fault Injection for Autonomous Vehicles (random FI + ML-based fault selection engine)
	![image](https://github.com/quz105/xin_phd_study/blob/master/images/ADSArchitecture.png)
	* An Overview of Publicly Available Driving Datasets and Virtual Testing Environments (37 dataset and 22 simulations)
	* Autoware.AI
	![image](https://github.com/quz105/xin_phd_study/blob/master/images/autowave.ai1.png)
	![image](https://github.com/quz105/xin_phd_study/blob/master/images/autowave.ai2.png)
	
2. **Challenges:**
	* The architecture of ADS is not standardized (exists difference).
	* Open-loop testing and closed-loop testing (in the overview paper). The former means using dataset to train and improve the ML-based algorithm, the latter means test in simulation environment or reality vehicles.
	


3. **Plan:**
  * Find more resource about the Plan&Control layer
  * Learn Apollo of Baidu and do a presentaion


## Date: 2019/09/02 – Weekly Summary

1. **Progress:**
	* Read Paper AirSim: High-Fidelity Visual and Physical simulation for autonomous vehicles
	* Learn how to use APIS to control vehicle in AirSim, front, rear, left, right and brake.
	* Use APIS to collect photoes generated by camera.
	* University of Passua (Alessio Gambi) focus on Software Testing, Testing self-driving cars and cloud computing. Focus on ADS in 2018 or 2019.
	![image](https://github.com/quz105/xin_phd_study/blob/master/images/UP%20work.png)
	
	
2. **Challenges:**
	* Difficult to generate the test environement. The model is pre-builded, no way to change it by code.
	* Consider Using Drone to control AV? 


3. **Plan:**
  * Read DSN19' ML-based Fault injection.
  * Find more papers about the testing of ADS.

## Date: 2019/08/26 – First presentation

1. **Progress:**
	* Read Paper Software Engineering for Automated Vehicles: Addressing the Needs of Cars That Run on Software and Data
	* ASFAULT: Testing Self-Driving Car Software Using Search-based Procedural Content Generation
	![image](https://github.com/quz105/xin_phd_study/blob/master/images/AsFault.jpg)
	![image](https://github.com/quz105/xin_phd_study/blob/master/images/genroad.jpg)
	* Generating Effective Test Cases for Self-Driving Cars from Police Reports
	![image](https://github.com/quz105/xin_phd_study/blob/master/images/AC3R.jpg)
	* AirSim by Microsoft
	
	
2. **Challenges:**
	* A bug in AsFault, the file direction is not right and a lot of function can find corresponding resourse.
	* Build the environment of AirSim. Pay attentation to the version of used software(VS2017, Python 3.4 and so on. Find more in https://github.com/Microsoft/AirSim/#how-to-use-it).


3. **Plan:**
  * Find more papers about how to test Auto-car software efficiently and effectively;
  * Try to learn AirSim (FSR 17’), find ways to control ego-cars and gather data;
  * Follow the work of University of Passau.
