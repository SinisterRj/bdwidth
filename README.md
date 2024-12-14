# bdwidth
bdwidth sensor is a optical width and motion sensor for 3D printer.

> [!TIP]
> with the width and motion data of the filament, we can adjust the flow rate in real time
> 
> and pause the printer if the filament jams and runout


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
extruder:extruder
runout_delay_length : 4.0
pause_on_runout: True
read_interval:0.3
#  in seconds
sensor_to_nozzle_length: 70
#   The distance from sensor to the melting chamber/hot-end in
#   millimeters (mm). The filament between the sensor and the hot-end
#   will be treated as the default_nominal_filament_diameter. Host
#   module works with FIFO logic. It keeps each sensor value and
#   position in an array and POP them back in correct position. This
#   parameter must be provided.

default_nominal_filament_diameter: 1.75 # (mm)

enable: True
#   Sensor enabled or disabled after power on. The default is to
#   disable.
min_diameter: 1.0
#   Minimal allowed diameter for flow rate adjust and runout.
max_diameter: 1.9
#   Maximum allowed diameter for flow rate adjust and runout.
#   The default is default_nominal_filament_diameter + max_difference.
logging: True
#   Out diameter to terminal and klipper.log can be turn on|of by
#   command.


```
