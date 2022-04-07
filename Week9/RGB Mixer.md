# RGB Colour Mixer - Part 2 Assignment 2
## using Arduino 

![Arduino Circuit - Tinkercad](https://user-images.githubusercontent.com/38569809/162177369-d7a11a30-ba59-4782-bbf5-ab154219a9d9.png)


### Objective 

To work with digitalRead, digitalWrite, analogRead, analogWrite and input and output in hardware. 

### Components Used

  - Arduino Uno 
  - Breakboard mini
  - Potentiometer
  - RGB LED
  - Red LED, Green LED, Blue LED
  - Push Button
  - Resistors

### Development Process  

This was a really fun activity to work on. The fact that the RGB LED could produce multiple colours with the right ratio of Red, Blue and Green fascinated me. The initial idea required the use of multiple potentiometers and LEDs, but to be more resourceful I optimized it by using a button switch which allows the potentiometer to control the brightness of all three RGB LED colours. 

Then, I thought of giving the user a way to know which colour they are controlling (R, G or B), and this led to me adding the three LEDs . So, I connected the three LED's to the digital pin and the button switches between the LED's. 

Changing the potentiometer value while moving between the LED's allows the user to control the RGB LED and produce any colour of their choice!

### Challenges

The biggest problem I came upon was the button making it difficult to switch between the 3 LEDs and RGB modes in an order. A simpler fix to this would be using a three way switch, with a connection to each mode. But, since I didn't have the component, I had to implement a debounce code which will add a delay to button press. This would allow the user to switch between the modes reliably. 

### Future Improvements

I think the project can further be improved by turning the hardware into a more interactive game where an LCD screen will display a colour and the user will try to get to the colour by experimenting with the RGB values. 

