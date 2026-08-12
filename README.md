## Simhub-Telemetry-Overlays
A set of racing tools using Simhub overlays.

## Pedal Tracer
![Pedal Tracer](https://github.com/user0451/Simhub-Telemetry-Overlays/blob/main/media/tracer.gif)

An overlay that shows the current position of the pedal inputs in your racing simulator. It can be used to analyze pedal inputs and improve driving technique. As my example above shows, I need to work on braking...

## Steering Wheel
An overlay that shows the current position of the steering wheel. Modelled on the Moza CS2 Pro and the FSR2 wheels.

## These overlays have two modes:
- **Game Input**: Shows the current position of the pedals and steering wheel as they are being reported by the game telemetry.
- **Direct Input**: Shows the current position of the pedals and steering wheel directly from the hardware. This can be a very useful mode for practising hitting exact pedal pressures, without loading up a sim. This mode has a few requirements:
  - You must have the Simhub Control Mapper plugin enabled
  - You need to tell the overlay which input device to use. 

I've made use of Simhub variables to make this a little easier. I shall use my settings for a Moza R5 wheel as an example. The following variables are available in the overlay:

### Steering Wheel Overlay
The overlay has the following dashboard variables:

| Variable | Description | NCalc Example Value |
|----------|-------------|---------|
| **Wheelbase_Steering_Axis** | The Simhub property value representing the steering axis | [JoystickPlugin.MOZA_R5_Base_X] |
| **DIRECT_Max** | The maximum value the above axis can report | 65535 |
| **DIRECT_Steering_Angle** | The maximum steering angle you have set in your wheel controller (ie, Moza Pithouse) | 1080 |
| **GAME_Steering_Angle** | The steering angle of your current vehicle | 360 |

I'll add more info on the wiki pages soon, but for now, if you want to use the **Direct Input Mode**, you need to set the top three variables above in the overlay dashboard variables screen. Your wheel will then match the different soft-locks on all cars when you have that option set up in your simulator.

The final variable, **GAME_Steering_Angle**, is used only by **Game Output Mode** to match the in-game steering angle for a specific vehicle. Most games have different steering soft-locks for different vehicles, so this variable is used to scale the steering input to match the in-game steering angle, as games do not return the steering angle compensated with their soft-lock. This is why the steering wheel overlay will not match the in-game steering angle unless you set this variable to match the vehicle you are driving.

### Pedal Tracer Overlay
The Pedal tracer overlay works slightly differently. Our variables are not attached to the dashboard this time, but instead are attached to some widgets.

- There are two screens in this overlay; select the Direct Input screen
- The control contains two widgets, HorzMeters and VertMeters. Select one of these widgets
- Scroll down to the bottom of the properties list and find the Variables field for this widget.

Clicking the Edit Variables button will allow you to add the following variables:
| Variable | Description | NCalc Example Value |
|----------|-------------|---------|
| **accel** | The Simhub property value representing the accelerator axis | [JoystickPlugin.MOZA_R5_Base_Y] |
| **brake** | The Simhub property value representing the brake axis | [JoystickPlugin.MOZA_R5_Base_RZ] |
| **clutch** | The Simhub property value representing the clutch axis | [JoystickPlugin.MOZA_R5_Base_Z] |
| **max** | The maximum value your pedal can report when you fully press one of them. | 65535 |

So, to use the Direct Input mode, you need to set all four variables to match your pedal's axes on BOTH widgets.

Game Input Mode does not require any variables to be set, as it uses the game telemetry to report the pedal positions.

## Switch Modes
When you set up your simhub overlay screen, use the settings icon on each overlay to view the settings. Override controls for the overlay, and bind any key you want to Next. Pressing this key then allows you to switch between the modes.
