The `CurrentSE` function in your code is already being used to convert the raw current measurement into a distance measurement for the ultrasonic sensor. However, it's currently set up to output the distance in inches, as indicated by the line `Units Ultrasonic=in`.

If you want to convert the output to millimeters, you'll need to adjust the gain and offset parameters in the `CurrentSE` function and change the units declaration for the `Ultrasonic` variable.

First, change the units declaration for `Ultrasonic` to millimeters:

```cr-basic
Units Ultrasonic=mm
```

Next, you'll need to adjust the gain and offset parameters in the `CurrentSE` function. The exact values will depend on the specific characteristics of your sensor, but the general idea is that you'll need to multiply the gain by 25.4 (since there are 25.4 millimeters in an inch) and do the same for the offset.

For example, if your sensor outputs a current of 4 mA for 0 mm and 20 mA for a certain maximum distance (let's say 10668mm = 35ft), you could calculate the gain and offset as follows:

- Gain = (35 ft - 0.5 ft) / (20 mA - 4 mA) = 2.15625 ft/mA
- Offset = 0.5 ft - (Gain * 4 mA) = -8.575 ft

So your `CurrentSE` function would look like this:

```cr-basic
CurrentSE(Ultrasonic,1,Autorange,RG1,True,0,50,Gain,Offset)	' Freq = 50Hz
```

Please note that these are just example values. You'll need to replace them with the actual values for your specific sensor.