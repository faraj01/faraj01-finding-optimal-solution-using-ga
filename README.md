# faraj01-finding-optimal-solution-using-ga
This project is to find the minimum cost using Genetic Algorithms (GA).

Assume that there are 2 heaters with modes On (m1: heter1 , m2 for heter2) and mode Off  (m0) and the temperaturekeep in a room needs to be kept between Vmin=18 °C and Vmax= 22 °C within Tmax=7 hours. and the initial temperature (v0) in the room at t0 is 18 °C. Every time the mode is switiched on (m1 or m2) there is a discrete cost is paid PiD(m1)= 30 $ and PiD(m2)= 10 $ and the continuous cost for staying in this mode is PiC(m1) = 10 $/h and PiC(m2) = 20 $/h while there is no cost for switich off PiD(m0) = PiC(m0) = 0. 
The modes parameter (A) are as follows: A(m1)=4/3 °C, A(m2)=2 °C and A(m0)=-4 °C.

For example, the temperature in the room needs 3 hours to reach Vmax using (m1) and 2 hours to reach Vmax using (m2) while just 1 hour to be cooled from Vmax to Vmin.

Throw genetic algorithms, find the optimal schedule (alpha) that returns the minimum cost.

alpha=<(m0,t0),(m1,t1), (m2,t2),(m3,t3),...(mi-1,ti-1),(mi,ti)>
with the following constraints in order to calculate the the cost of alpha, Pi(alpha)= sumPiD+ sumPiC*ti

mi Not equal mi+1
run(alpha)=<v0,v1,v2,v3,...,vi-1,v0)> within T(alpha)=<t0,t1,t2,t3,...,ti-1,ti>
% Vmin <= V(i) <= Vmax
% 0 < ti <=Tmax
% sum(ti)= Tmax
%
% V(t0) = V(0) = V0 = 18
% V(i) not equal V(i+1), either greater or lower depending on the mode.
% V(i)= V(i-1)+(A(m i)*[((sum(from i=0 to t(i)) ti))-(sum(from i=0 to t(i-1)) ti))]
% V(t) = V(i-1)+A(m i)*(t-(sum(from i=1 to t(i-1)) ti)) , the temperature at any point of time
% t = (V(i-1)/A(m i))-t(i-1)
Can someone help me please with creating a foor loop that generates 50 safe shedules (alpha), and schedule that does not meet the previous features is considered irrelevnt. To calculate the cost Pi(alpha). Here is my units definition

%------------------------------------------------------------------------%
clear variables; 
close all;
clc;
%------------------------------------------------------------------------%%
%% Define units
%-------------------------------------------------------------------------------------------------------
Vmax = 22;           % The highest temperature we can reach                       [°C]
Vmin = 18;           % The lowest temperature we can reach                        [°C]
V0 = 18;             % Inetial temperature at time = 0
K = 2;               % Number of heaters 
Tmax = 7;            % Total time                                                 [h]
PiC = [10 20];       % Continuous cost                                            [$/h]
PiD = [30 10];       % Discrete cost                                              [$]
A = [4/3 2];         % Heating parameters for mode 1,2                            [°C/h]
A0 = -4;             % Cooling parameters for mode 0, when the heaters are off    [°C/h]
%------------------------------------------------------------------------------------------------------
