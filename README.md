# iKB-1 block package for iKB-1 Baord

powered by micro:bit

![iKB-1](https://raw.githubusercontent.com/jcubuntu/pxt-iKB1/master/icon.png)

The package adds support for the [i-BIT](https://inex.co.th/shop/ibit.html) conroller board from Innovative Experiment [INEX](https://inex.co.th).

### micro:bit Pin Assignment

The following micro:bit pins are used for communication to iKB-1 to use analog and digital sensors, DC motor drivers and servo motors:
* ``GND`` -- GND connected to iKB-1 GND
* ``3V `` -- 3V  connected to iKB-1 +3.3
* ``P19`` -- SCL connected to iKB-1 SCL
* ``P20`` -- SDA connected to iKB-1 SDA

### Motor control Block

Use iBIT's motor block to drives motor forward and backward. The speed motor is adjustable between 0 to 100.

* The dirrection must be select either `Forward` or `Backward`
* Speed is an integer value between `0 - 100`


```blocks
iBIT.Motor(ibitMotor.Forward, 100)

iBIT.Motor(ibitMotor.Backward, 100)
```

### Spin Block

Spin block is used to control both motors separately. For example, choose one motor spin with forward direction another one spin with backward direction.

* The Spin select direction must be either `Left` or `Right`
* Speed is an integer value between `0 - 100`

```blocks
iBIT.Spin(ibitSpin.Left, 100)

iBIT.Spin(ibitSpin.Right, 100)
```

### Turn Block

The Turn block is used to to control the robot movment by turning. The one motor will stop, another one is moving. The vipot point is a center of the robot body.

* The Turn select direction must be either `Left` or `Right`
* Speed is an integer value between `0 - 100`

```blocks
iBIT.Turn(ibitTurn.Left, 100)

iBIT.Turn(ibitTurn.Right, 100)
```

### Motor Stop Block 

The Motor Stop block is used to stop both motors. The speed is set to `0` automatic.

```blocks
iBIT.MotorStop()
```

### Servo Block

Use this block for control the servo's moving degree from 0 to 180

* Degree is an integer value between `0 - 180`

```blocks
iBIT.Servo(ibitServo.SV1, 90)
```

### ReadAD Block

This block is used to read the analog input data from the I2C-based ADC integrated circuit, ADS7828. The resolution of conversion is 12-bit. Data will be 0 to 4095. iBIT have 8-ch analog inputs. The pinout voltage range is 0 to +3.3V

* Analog sensor port are `ADC0 - ADC7`
* Select analog channel from `ADC0 - ADC7` for reading the analog sensor.
* Get the analog value to set the conditions for the robot's mission.

### Example

* Read the analog input 0 and display the conversion data on micro:bit. User can change the analog channel any time.

```blocks
basic.showNumber(iBIT.ReadADC(ibitReadADC.ADC0))
```

* Drive the motors with Forward and Backward by counting speed `0 - 100`

```blocks
let speed = 0
basic.forever(() => {
    for (let speed = 0; speed <= 100; speed++) {
        iBIT.Motor(ibitMotor.Forward, speed)
        basic.pause(50)
    }
    for (let speed = 0; speed <= 100; speed++) {
        iBIT.Motor(ibitMotor.Backward, speed)
        basic.pause(50)
    }
})
```

* Drive the motors by pressing button `A` and `B`. Turn Left by speed 50 when pressed button `A` and Turn Right by speed 50 when pressed button `B`.

```blocks
input.onButtonPressed(Button.A, () => {
    iBIT.Turn(ibitTurn.Left, 50)
})
input.onButtonPressed(Button.B, () => {
    iBIT.Turn(ibitTurn.Right, 50)
})
```

* Spin the motors by pressing button `A` and `B`. Spin Left by speed 50 when pressed button `A` and Spin Right by speed 50 when pressed button `B`.

```blocks
input.onButtonPressed(Button.A, () => {
    iBIT.Spin(ibitSpin.Left, 50)
})
input.onButtonPressed(Button.B, () => {
    iBIT.Spin(ibitSpin.Right, 50)
})
```

* Example for Servo, drive the servo motor's movement angle at Servo output 1 and 2 from `0 - 180` and back to 0 to restart again. 

```blocks
basic.forever(() => {
    for (let Degree = 0; Degree <= 180; Degree++) {
        iBIT.Servo(ibitServo.SV1, Degree)
        iBIT.Servo(ibitServo.SV2, Degree)
        basic.pause(10)
        while (Degree == 180) {
            Degree = 0
        }
    }
})
```

* Example for set Servo Stop or set freedom servo.

```blocks
input.onButtonPressed(Button.A, () => {
    iBIT.Servo(ibitServo.SV1, 90)
})
input.onButtonPressed(Button.B, () => {
    iBIT.ServoStop(ibitServo.SV1)
})
```



## License

MIT

## Supported targets

* for PXT/microbit
