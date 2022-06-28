# Long-System-description-for-IPIN2022 Track3
System Overview
The system is mainly divided into two parts: model training and location estimation. The model training part constructs a fingerprint map and constructs map features associated with the location information based on multi-sensor information. In the location estimation part, location estimation is performed by sensor information, location correction is performed using the trained model, and the final trajectory is generated.

 ![image](https://user-images.githubusercontent.com/108048503/176123608-accb8e59-3909-4173-8cfa-84e28cd507a5.png)  
Fig.1 Model training diagram 

Model training：
As shown in the Fig.1, the model training consists of four main parts, which are map feature construction, pedestrian step estimation model, floor estimation model and action modality recognition model. In order to get the correct correlation information between map features and locations, the pedestrian step estimation model training is performed first, and the peak and valley values of acceleration modal values and related parameters are used as features for step estimation model training, which can get the location information between reference points.
The constructed map features mainly include WiFi fingerprints, magnetic field features, and digital maps. The approximate location of WiFi signal source is estimated by Range-Only SLAM algorithm, and the fingerprint information with large error is eliminated, while the WiFi strength information of the unknown area is predicted. Segment the magnetic field information, compare the variability of magnetic field features in each segment, and construct magnetic field fingerprints according to the degree of variability. The barometer data are used as key parameters to train the floor estimation model using support vector machine. A motion mode recognition model is built to determine mainly whether the pedestrian is moving and the current motion mode.

 ![image](https://user-images.githubusercontent.com/108048503/176123447-590d20ad-e12b-48d8-ae75-903f66a77665.png)  
Fig.2 Location estimation diagram 

Location estimation：
The location estimation part is divided into three main parts, which are pedestrian heading estimation, location correction based on map features and floor ID estimation. The pedestrian heading estimation is performed by IMU and magnetic field information, which mainly includes three parts: heading estimation, gait recognition and step length estimation. The pedestrian heading information is corrected by magnetic field information, the time of peak and valley in the acceleration mode value is used as the key variable for pedestrian gait detection, and the step length estimation is performed by the trained pedestrian step length model. The pedestrian location correction is performed using particle filtering combined with digital map, feature matching of WiFi and magnetic field information at the current moment, and secondary correction of pedestrian location based on the matching results. Finally, the floor ID determination is performed and the final localization result is given. The system block diagram of the location estimation part is shown in Fig.2.

