#include <max6675.h>  // Include the MAX6675 library for reading thermocouple temperature
#include <Wire.h>     // Include the Wire library for I2C communication
#include <LiquidCrystal_I2C.h> // Include the LiquidCrystal_I2C library for controlling LCD display

int relayPin = 9;     // Define the pin number for the relay that controls power to the Peltier
int ledPin1 = 11;     // Define the pin number for the LED indicator on the HOT side
int ledPin2 = 10;     // Define the pin number for the LED indicator on the COLD side

int csPin1 = 4;       // Define the chip select pin for the first thermocouple for the hot side 
int soPin1 = 7;       // Define the data out pin for the first thermocouple for the hot side
int sckPin1 = 8 ;     // Define the clock pin for the first thermocouple for the hot side 

int csPin2 = 2;       // Define the chip select pin for the second thermocouple for the cold side
int soPin2 = 12;      // Define the data out pin for the second thermocouple for the cold side 
int sckPin2 = 13;     // Define the clock pin for the second thermocouple for the cold side 

LiquidCrystal_I2C lcd1(0x27, 16, 2); // Initialize the first LCD display with the I2C address and dimensions for the hotside
LiquidCrystal_I2C lcd2(0x25, 16, 2); // Initialize the second LCD display with the I2C address and dimensions for the cold side 

MAX6675 thermocouple1(sckPin1, csPin1, soPin1); // Initialize the first thermocouple object with the pins defined above
MAX6675 thermocouple2(sckPin2, csPin2, soPin2); // Initialize the second thermocouple object with the pins defined above

void setup() { 
  pinMode(ledPin1, OUTPUT);  // Set the LED pin on the HOT side as an output        
  pinMode(ledPin2, OUTPUT);  // Set the LED pin on the COLD side as an output       
  pinMode(relayPin, OUTPUT);// Set the relay pin as an output for the peltier
  digitalWrite(relayPin, HIGH); // Turn on the relay to initialize power
  delay(7000);              // Wait for 7 seconds to allow the system to initialize the temperature in both sides 
  
  lcd1.init();      // Initialize the first LCD display
  lcd1.backlight(); // Turn on the backlight on the first LCD display
  lcd2.init();      // Initialize the second LCD display
  lcd2.backlight(); // Turn on the backlight on the second LCD display
   
  lcd1.print("Food Container"); // Print the title on the first LCD display
  lcd1.setCursor(0,1);           // Set the cursor position to the second row
  lcd1.print("HOT SIDE");        // Print the subtitle on the first LCD display      
      
  lcd2.print("Food Container"); // Print the title on the second LCD display
  lcd2.setCursor(0,1);           // Set the cursor position to the second row
  lcd2.print("COLD SIDE");       // Print the subtitle on the second LCD display 
      
  Serial.begin(9600);  // Initialize serial communication at 9600 baud
  Serial.println("Food Container"); // Print a message to the serial monitor
  
  delay(5000);  // Wait for 5 seconds to allow the user to read the display at the beginning for both lcd 
}

void loop() {
  
  // Read temperature from two thermocouples and store the values
  float temp1 = thermocouple1.readFahrenheit();
  float temp2 = thermocouple2.readFahrenheit();
  
  // Print temperature readings to the serial monitor
  Serial.print("C_1 = "); 
  Serial.println(thermocouple1.readCelsius());
  Serial.print("F_1 =_1");
  Serial.println(thermocouple1.readFahrenheit());
  Serial.print("C_2 = "); 
  Serial.println(thermocouple2.readCelsius());
  Serial.print("F_2 =_2");
  Serial.println(thermocouple2.readFahrenheit());
  
  // Clear previous values from two LCD screens
  lcd1.clear();
  lcd2.clear();
  
  // Set cursor and print "HOT SIDE" to the first LCD screen
  lcd1.setCursor(0,0);      
  lcd1.print("HOT SIDE");
  
  // Set cursor and print temperature readings in Celsius and Fahrenheit to the first LCD screen
  lcd1.setCursor(0,1);
  lcd1.print(thermocouple1.readCelsius()); 
  lcd1.setCursor(5,1);
  lcd1.print((char)223); 
  lcd1.setCursor(6,1);
  lcd1.print("C");    
  lcd1.setCursor(7,1);
  lcd1.print(" ");       
  lcd1.setCursor(8,1);
  lcd1.print(thermocouple1.readFahrenheit()); 
  lcd1.setCursor(14,1);    
  lcd1.print((char)223); 
  lcd1.setCursor(15,1);
  lcd1.print("F");
  
  // Check if temperature reading from thermocouple 1 is less than or equal to 120 Fahrenheit
  if (temp1 <= 120) {  
    // Turn on the red LED connected to ledPin1
    digitalWrite(ledPin1, HIGH);
   
  } else {
    // Otherwise turn off LED connected to ledPin1
    digitalWrite(ledPin1, LOW);
    
  }
  
  // Set cursor and print "COLD SIDE" to the second LCD screen
  lcd2.setCursor(0,0);     
  lcd2.print("COLD SIDE");
  
  // Set cursor and print temperature readings in Celsius and Fahrenheit to the second LCD screen
  lcd2.setCursor(0,1);
  lcd2.print(thermocouple2.readCelsius()); 
  lcd2.setCursor(5,1);
  lcd2.print((char)223); 
  lcd2.setCursor(6,1);
  lcd2.print("C");    
  lcd2.setCursor(7,1);
  lcd2.print(" ");       
  lcd2.setCursor(8,1);
  lcd2.print(thermocouple2.readFahrenheit()); 
  lcd2.setCursor(14,1);      
  lcd2.print((char)223); 
  lcd2.setCursor(15,1);
  lcd2.print("F"); 
  
  // Check if temperature reading from thermocouple 2 is greater than or equal to 45 Fahrenheit 
    // Turn on LED connected to ledPin2
    digitalWrite(ledPin2, HIGH);
    // Turn on relay connected to relayPin
    digitalWrite(relayPin, HIGH);
  } else {
    // Otherwise turn off
