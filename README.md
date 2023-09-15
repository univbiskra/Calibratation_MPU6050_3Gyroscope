# Calibratation_MPU6050_3Gyroscope
this code is the process of calibration 3D gyroscope MPU6050
Sensor Error Models (SEM) is a depiction of sensors, including uncalibrated primary-element measurement and its offset, misaligned axes and measurement scale factors, and in certain sensors, the magnetization effect, shown as hard iron and soft iron. The IMU calibration process needs pre-determination SEM for both Gyro and ACC. They come in a variety of representations with the same parameters, the calibration procedure is the only variable [78-80]. The SEM in equation 3.1 and 3.2, they are comprised of nine unknown values each, including three offsets, three correction scale factors, and three non-orthogonal angles.
ACC_f=T_no S_f (ACC_n-b)=[■(ACC_fx@ACC_fy@ACC_fz )]=[■(1&0&0@T_xy&1&0@T_xy&T_xy&1)][■(s_fx&0&0@0&s_fy&0@0&0&s_fz )]([■(acc_nx@acc_ny@acc_nz )]-[■(b_x@b_y@b_z )])    	         (3.1)
Where:
〖ACC〗_n is the measured acceleration vector.
〖ACC〗_f is the vector of compensated ACC final readings.
S_f is the matrix of scale factors 
T_no is matrix of non-orthogonality, transformation from the non-orthogonal to orthogonal frame. 
b is vector corresponding to sensor offset.

The gyro SEM is represented by the equation 3.2:
Y_g-B_g=〖T_g M_g S〗_g U_g  ⇒[■(Y_gx-b_gx@Y_gy-b_gy@Y_gz-b_gz )]=[■(c_θ c_ψ&-c_φ s_ψ+s_φ s_θ c_ψ&s_φ s_ψ+c_φ s_θ c_ψ@c_θ s_ψ&c_φ c_ψ+s_φ s_θ s_ψ&-s_φ c_ψ+c_φ s_θ s_ψ@-s_θ&s_φ c_θ&c_φ c_θ )]^T*
     [■(1&0&0@α_xy&1&0@α_zx&α_zy&1)][■(S_gx&0&0@0&S_gy&0@0&0&S_gz )][■(u_gx@u_gy@u_gz )].       						        (3.2)
 Where:
Y_g is measured vector of the angular rates for the gyro undergoing calibration. B_g is offsets vector that prior-determined. S_g is matrix of scale factors. T_g is matrix represent the transformation from the non-orthogonal to orthogonal frame. M_g is the misalignment matrix between gyro and the referential frames Ug is vector of measured angular rates. c_i=cos⁡i, s_i= sin⁡i and θ,ψ,φ represent Euler angles. 
       B) Calibration Process
The static approach is utilized as an example of one of these common approaches in the calibration field. The calibration of the ACC is based on the ACC data set gathered at different orientations in static conditions with only gravitational impact. It is advised to collect the outputs of ACC at least in 21 orientations according to the Thin-Shell approach [81] and the reliability of this technique analysis reported in [82]. Moreover, to reduce the effect of temperature drift, it is recommended to warm up the ACC before starting the calibration process, in which it should hold the ACC in each orientation in static conditions and give some time for raw data averaging, which would minimize the impact of random noise. All averages have been conducted along all axes x, y, and z, with at least eight orientations along each axis Figure 3.6, where exact knowledge of these orientations is not necessary [82]. Using the minimization function approach to estimate the nine unknown coefficient of SEM, as a criteria function for minimization, the Root Mean Square Error (RMSE) presented in equation 3.4 has been utilized. This calibration technique assumes that in a static condition where there is no movement the ACC-measured output should equal gravity ‘g’.
Figure 3.6: ACC calibration around eight orientations along “x” axis
In static conditions, the only force impacting the accelerometer is gravitational forces in the downward direction; this fact results in equation 3.3.
g_x^2+g_y^2+g_z^2=|g|^2                                        					         (3.3)
Where g_i   represents the projection of the gravity vector onto axes i. As a criterion function for minimization, RMSE is used. 
 RMSE(Θ,g)=√((∑_1^N▒(|a_i (Θ)|-g)^2 )/N), n=24,                          				        (3.4)
Where   |a_i (Θ)| = √(〖〖acc〗_x〗^2+〖〖acc〗_y〗^2+〖〖acc〗_z〗^2 )        					        (3.5)
and Θ = (Θ_1,Θ_2,…,Θ_9)  is SEM nine coefficient being estimated, the total number of orientations about all axis is N (in our case n=9), m=24 in our case, g=1 is gravity vector, a_i (Θ) represent the SEM acceleration vector being estimated.
 
