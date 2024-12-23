# bdwidth
#### bdwidth sensor is an optical width and motion sensor for 3D printer.
We have developed a unique algorithm that automatically compensates for the filament shadow on the CCD sensor as the filament moves at different heights and angles

1. Adjust the flow rate in real time

2. Pause the printer while jam or runout (Built-in one laser motion sensor chip PAT9125)
 
3. Width accuracy: +/- 0.015mm (Built-in one high resolution 0.005mm ccd sensor chip TCD1254)
 
4. Connection: USB or I2C

5. No Need to do calibration

> [!NOTE]
> Transparent filament: It cannot measure the width of fully transparent filaments, but it can still measure movement. This means that the jam and runout detection functions still work


## Quick start

#### 1.Plug the bdwidth sensor into the USB port or I2C port(it can be any two gpios) on the 3D printer mainboard 


#### 2.Install software module
```
cd  ~
git clone https://github.com/markniu/bdwidth.git
chmod 777 ~/bdwidth/klipper/install.sh
~/bdwidth/klipper/install.sh
```

#### 3.Configure Klipper

add the following section into your klipper config file,

here we connect the bdwidth to the usb port

```
[bdwidth]
port:usb
#   usb or i2c 
#i2c_software_scl_pin:PB10
#i2c_software_sda_pin:PB11
#   needed if the port is i2c
serial:/dev/serial/by-id/usb-1a86_USB_Serial-if00-port0
#   needed if the port is usb
default_nominal_filament_diameter: 1.75 # (mm)
enable: all
#  disable or enable the sensor after power on.
#   the value should be one of width/motion/all/disable 
#   width(only enable the width function)
#   motion(only enable the motion function)
#   all(enable both the width and motion)
#   disable(disable both the width and motion)
min_diameter: 1.0
#   Minimal allowed diameter for flow rate adjust and runout.
max_diameter: 1.9
#   Maximum allowed diameter for flow rate adjust and runout.
#   The default is default_nominal_filament_diameter + max_difference.
extruder:extruder
runout_delay_length : 4.0  # (mm)
flowrate_adjust_length : 5  # (mm)
pause_on_runout: True
sample_time:2
#  in seconds
sensor_to_nozzle_length: 70
#   The distance from sensor to the melting chamber/hot-end in
#   millimeters (mm). The filament between the sensor and the hot-end
#   will be treated as the default_nominal_filament_diameter. Host
#   module works with FIFO logic. It keeps each sensor value and
#   position in an array and POP them back in correct position. This
#   parameter must be provided.


logging: True
#   Out diameter to terminal and klipper.log can be turn on|of by
#   command.



```

#### Where to buy: [https://www.pandapi3d.com/product-page/bdwidth-sensor](https://www.pandapi3d.com/product-page/bdwidth-sensor)


