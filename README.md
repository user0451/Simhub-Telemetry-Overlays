## Simhub-Telemetry-Overlays
A set of racing tools using Simhub overlays.

## Pedal Tracer
![Pedal Tracer](https://github.com/user0451/Simhub-Telemetry-Overlays/blob/main/media/tracer.gif)

An overlay that shows the current position of the pedal inputs in your racing simulator. It can be used to analyze pedal inputs and improve driving technique. As my example above shows, I need to work on braking...

## Steering Wheel
![Wheel Tracer](https://github.com/user0451/Simhub-Telemetry-Overlays/blob/main/media/wheel.gif)

An overlay that shows the current position of the steering wheel. Modelled on the Moza CS2 Pro and the FSR2 wheels.

## These overlays have two modes:
- **Game Input**: Shows the current position of the pedals and steering wheel as they are being reported by the game telemetry. Only available when a game is running and Simhub is receiving telemetry from that game.
- **Direct Input**: Shows the current position of the pedals and steering wheel directly from the hardware. This mode has a few requirements:
  - You must have the Simhub Control Mapper plugin enabled
  - You need to tell the overlays which inputs to use. 

I've made use of Simhub variables to make this a little easier. I shall use my settings for a Moza R5 wheelbase as an example. The following variables are available in the overlay:

### Steering Wheel Overlay
Edit the overlay. The overlay has the following dashboard variables:

| Variable | Description | NCalc Example Value |
|----------|-------------|---------|
| **Wheelbase_Steering_Axis** | The Simhub property value representing the steering axis | [JoystickPlugin.MOZA_R5_Base_X] |
| **DIRECT_Max** | The maximum value the above axis can report | 65535 |
| **DIRECT_Steering_Angle** | The maximum steering angle you have set in your wheel controller (ie, Moza Pithouse) | 1080 |
| **GAME_Steering_Angle** | The steering angle of your current vehicle | 360 |

If you want to use the **Direct Input Mode** for steering, you need to set the top three variables above in the overlay dashboard variables screen. Your wheel will then match the different soft-locks on all cars when you have that option set up in your simulator.

The final variable, **GAME_Steering_Angle**, is used only by **Game Output Mode** to match the in-game steering angle for a specific vehicle. Most games have different steering soft-locks for different vehicles, so this variable is used to scale the steering input to match the in-game steering angle, as games do not return the steering angle compensated with their soft-lock. This is why the steering wheel overlay will not match the in-game steering angle unless you set this variable to match the vehicle you are driving.

### Pedal Tracer Overlay
The Pedal tracer overlay works slightly differently. Our variables are not attached to the dashboard this time, but instead are attached to some widgets.

- edit the overlay
- There are two screens in this overlay; select the ***Direct Input*** screen from the dropdown at the top of the overlay settings.
- The screen contains two widgets, HorzMeters and VertMeters. Select one of these widgets
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

### Which mode am I in?
OK, one small customization to go, and then we are done! To show you which mode you are in, both overlays need to know which button you have set to switch modes for that overlay. So, we need to add one more variable value to the dashboard variables for each overlay.

### Pedal Tracer Overlay & Steering Wheel Overlay

Edit each overlay; view the dashboard variables on EACH overlay: <TO IMPLEMENT FOR PEDAL TRACER OVERLAY AND STEERING WHEEL OVERLAY>
| Variable | Description | NCalc Example Value |
|----------|-------------|---------|
| **nextKey** | The key you have set for the next screen | [InputStatus.KeyboardReaderPlugin.Ctrl+Shift+Up] |

Once you have added unique keys to this variable on each of the overlays, you will see a label appear on the overlay when you switch modes. The label will show the current mode for 2 seconds or so, and then disappear.

## The cost...
Well, the overlays are free monetarily, but will cost a little bit of your patience and time to customise them to your specific hardware. Easy for some, a little more difficult for others. I have tried to make the Simhub overlays as easy to customise as possible.

### Forget about it...
All but one of the values you will need to customise are 'fire and forget'; do it once and then forget about them. The **GAME_Steering_Angle** variable should be changed to match the vehicle you are currently driving, if you want to use the **Game Input mode** on the Steering Wheel.

The **Direct Input Mode** is a great way to practice your pedal inputs without having to load up a sim. You can use this mode to practice hitting exact pedal pressures, and to get used to the feel of your pedals. While driving, this is the better mode to use. Take the time to set up your variables correctly, as this mode will give you a more accurate representation of your pedal and steering inputs. 

The **Game Input Mode** is ideal for using with your Simhub replays. It can certainly be used while driving, but remember you need to set the **GAME_Steering_Angle** variable to match each vehicle's steering angle.



