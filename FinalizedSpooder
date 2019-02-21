const int motor1 = 9; //backward
const int motor2 = 10; //forward
const int motor3 = 11; //right
const int motor4 = 12; //left
#include <IRremote.h>
#define down 0xFF22DD
#define right 0xFFC23D
#define left 0xFFE01F
#define up 0xFF906F
#define self 0xFFE21D
#define turnOff 0xFFA25D

int ir = 13;

IRrecv irrecv(ir);

decode_results results;


#define MAX_TIME 150 // max ms between codes
int state = LOW;

long lastPressTime = 0;
unsigned long lastState;

boolean lockout = true;

#define trigPin 4
#define echoPin 2


void setup() {
  Serial.begin (9600);
 Serial.println("Enabling IRin");
  irrecv.enableIRIn(); // Start the receiver
  Serial.println("Enabled IRin");
  
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  pinMode(motor1, OUTPUT);
  pinMode(motor2, OUTPUT);
  pinMode(motor3, OUTPUT);
  pinMode(motor4, OUTPUT);

}
long duration, distance;

void loop() {
if (irrecv.decode(&results)) {
       Serial.println(results.value, HEX);
       delay(200);
       if (lockout == false){
        sonar();
       } 
        
       if(results.value !=0xFFFFFFFF){
              lastState = results.value;
        }
        if (lastState == down){
          lockout = true;
               if (state == LOW) { 
                        state = HIGH;  // Button pressed, so set state to HIGH
                        digitalWrite(motor1, HIGH);
               }
                lastPressTime = millis();
         }
         if (lastState == up) {
                lockout = true;
               if (state == LOW) { 
                        state = HIGH;  // Button pressed, so set state to HIGH
                        digitalWrite(motor2, HIGH);
               }
                lastPressTime = millis();
         }
         if (lastState == left) {
                    lockout = true;
               if (state == LOW) { 
                        state = HIGH;  // Button pressed, so set state to HIGH
                        digitalWrite(motor3, HIGH);
               }
                lastPressTime = millis();
         }
          if (lastState == right) {
                  lockout = true;
               if (state == LOW) { 
                        state = HIGH;  // Button pressed, so set state to HIGH
                        digitalWrite(motor4, HIGH);
               }
               lastPressTime = millis();
          }
       
       if (results.value == self) {
        lockout = false;
        }
        
        irrecv.resume(); // Receive the next value
}
  if (state == HIGH && millis() - lastPressTime > MAX_TIME) {
           state = LOW; // Haven't heard from the button for a while, so not pressed
           digitalWrite(motor1, LOW);
           digitalWrite(motor2, LOW);
           digitalWrite(motor3, LOW);
           digitalWrite(motor4, LOW);
  }
}

void sonar(){
               // long duration, distance;
  digitalWrite(trigPin, LOW);  // Added this line
  delayMicroseconds(2); // Added this line
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10); // Added this line
  digitalWrite(trigPin, LOW);
  duration = pulseIn(echoPin, HIGH);
  distance = (duration/2) / 29.1;
  Serial.print(distance);
  Serial.println(" cm");
  delay (200);
  if (distance >= 200 || distance <= 0){
    digitalWrite(motor1, LOW);  // Added this line
   }

  if(distance<=20){
   avoid();
  }
  else if (distance >=21){
    movement();
   }
}

void avoid(){
  digitalWrite(motor1, LOW);     
  digitalWrite(motor2, LOW);  
  digitalWrite(motor3, LOW);      
  digitalWrite(motor4, HIGH);
}

void movement(){
   digitalWrite(motor1, LOW);  // Added this line
   digitalWrite(motor2, HIGH);  // Added this line
   digitalWrite(motor3, LOW);  // Added this line    
   digitalWrite(motor4, LOW);  // Added this line
}

