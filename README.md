# OWN-VERSION-OF-MEMORY-GAME
**Overview of the project.**:
The original Atari game had four colored panels, each with an LED that lit up in a particular pattern that players had to repeat back
When you press the correct corresponding button, the lights
flash again in a longer sequence. Each time you repeat the sequence
back correctly, the game adds an extra step to make the sequence
more challenging for you. When you make an error, the game resets
itself.I have personally made the game upto level 20,which implies it will show a pattern upto where the LEDs will glow 20 times maximum.

**Components used :-**
Arduino board
• Breadboard
• Jumper wires
• 4 momentary tactile four-pin
pushbuttons
• 4 LEDs,1 RGB LED
• 4 220-ohm resistors


**CODE:**

const int buttonPin_green = 2;  **// Pin connected to the push button GREEN**
const int ledPin_green = 13;    **// Pin connected to the LED GREEN**
const int buttonPin_red = 3;    **// Pin connected to pushbutton RED**
const int ledPin_red = 12;      **// Pin connected to LED RED**
const int buttonPin_blue = 4;  ** // Pin connected to pushbutton BLUE**
const int ledPin_blue = 11;     **// Pin connected to LED BLUE**
const int buttonPin_yellow = 5; **// Pin connected to pushbutton YELLOW**
const int ledPin_yellow = 10;   **// Pin connected to LED YELLOW**
int generate[20];
int a=A5;// **Indicator For Giving Input**
int b=A4;//  **Indicator For Giving Input**

void setup() {
  pinMode(buttonPin_green, INPUT_PULLUP);  **// Use internal pull-up resistor**
  pinMode(ledPin_green, OUTPUT);
  pinMode(buttonPin_red, INPUT_PULLUP); 
  pinMode(ledPin_red, OUTPUT);
  pinMode(buttonPin_blue, INPUT_PULLUP); 
  pinMode(ledPin_blue, OUTPUT);
  pinMode(buttonPin_yellow, INPUT_PULLUP); 
  pinMode(ledPin_yellow, OUTPUT);
 pinMode(a,OUTPUT);
pinMode(b,OUTPUT);
  
  Serial.begin(9600);
  
  

  randomSeed(111);      **// Use as seed**
}

void loop() {
  int i=0, a = 0,k=1;
  while(i!=20&&k==1){
    a = random(10, 14);**//Generating Random Colors**
    generate[i] = a;
    Serial.println("---------------------------------------------------------------------------------------------");
    input(i); **//Display the LED pattern**
    delay(3000);**//Giving A Delay 3 seconds**
    k=output(i);**//Taking the Input from the user**
    i++;
  }
  if(i==20)**//If The User  Reaches 20 LEVEL i.e The Last Level**
  {
    analogWrite(b,255);
    delay(500);
    analogWrite(b,0);
    delay(500);
    analogWrite(b,255);
    delay(500);
    analogWrite(b,0);
    delay(500);
    analogWrite(b,255);
    delay(500);
    analogWrite(b,0);
    delay(500);
   analogWrite(b,255);
    delay(500);
    analogWrite(b,0);
    delay(500);
  }
  else **//The User Fails At a Level Before 20**
  {
analogWrite(a,255);
      delay(500);
      analogWrite(a,0);
      delay(500);
      analogWrite(a,255);
      delay(500);
      analogWrite(a,0);
      delay(500);
      analogWrite(a,255);
      delay(500);
      analogWrite(a,0);
      delay(500);
      }
  analogWrite(a,0);
  analogWrite(b,0);
  exit(0);
}

void input(int i) {
  Serial.print("LEVEL :- ");
  Serial.println(i + 1);

      
  for (int k = 0; k <= i; k++) {
    if (generate[k] == 10) {
      Serial.print(k + 1);
      Serial.println("- YELLOW");
      digitalWrite(ledPin_yellow, HIGH); **// Set Yellow High**
     
    } else if (generate[k] == 11) {
      Serial.print(k + 1);
      Serial.println("- BLUE");
      digitalWrite(ledPin_blue, HIGH); **// Set Blue High**
      
    } else if (generate[k] == 12) {
      Serial.print(k + 1);
      Serial.println("- RED");
      digitalWrite(ledPin_red, HIGH); **// Set Red High**
     
    } else {
      Serial.print(k + 1);
      Serial.println("- GREEN");
      digitalWrite(ledPin_green, HIGH); **//Set Green High**
      
    }

    delay(1000);

    **// Turn off all LEDs**
    digitalWrite(ledPin_yellow, LOW);
    digitalWrite(ledPin_green, LOW);
    digitalWrite(ledPin_blue, LOW);
    digitalWrite(ledPin_red, LOW);
    delay(1000);
  }
}
int output(int i)
{
  int q,w=0,e,buttonState_red,buttonState_blue,buttonState_green,buttonState_yellow;
  analogWrite(b,255); **//Indicator LED for Input Turned on**
  for(q=0;q<=i;q++){
     buttonState_green= digitalRead(buttonPin_green); **//Reading the state of green button pin**
   buttonState_red=digitalRead(buttonPin_red);**//Reading the state of red button pin**
   buttonState_blue=digitalRead(buttonPin_blue);**//Reading the state of blue button pin**
   buttonState_yellow=digitalRead(buttonPin_yellow);**//Reading the state of yellow button pin**
   if (buttonState_green == LOW) { **// Buttonpin of Green is pressed**
    digitalWrite(ledPin_green, HIGH); **// Turn on Green LED**
    w=13;
  } 
  else if (buttonState_red == LOW) { **// Buttonpin of Red is pressed**
    digitalWrite(ledPin_red, HIGH); **// Turn on Red LED**
    w=12;
  }
  else if (buttonState_blue == LOW) {** // Buttonpin of Blue is pressed**
    digitalWrite(ledPin_blue, HIGH); **// Turn on Blue LED**
    w=11;
  } 
  else if (buttonState_yellow == LOW) { **// Buttonpin of Yellow  is pressed**
    digitalWrite(ledPin_yellow, HIGH); **// Turn on yellow LED**
    w=10;
    }
    if(w==0){ //** A loop if the User has not pressed any button **
      q--;
    continue;
    }
   delay(1000);

    // Turn off all LEDs
    digitalWrite(ledPin_yellow, LOW);
    digitalWrite(ledPin_green, LOW);
    digitalWrite(ledPin_blue, LOW);
    digitalWrite(ledPin_red, LOW);
    delay(1000);
    if(w==generate[q]){
      w=0;
    
    }
    else{ **// If The User Input Pattern  Does Not Match With The Generated Pattern**
      analogWrite(a,255);
      delay(500);
      analogWrite(a,0);
      delay(500);
      analogWrite(a,255);
      delay(500);
      analogWrite(a,0);
      delay(500);
      analogWrite(a,255);
      delay(500);
      analogWrite(a,0);
      delay(500);
      analogWrite(a,255);
      delay(500);
      analogWrite(a,0);
      delay(500);
      analogWrite(a,255);
      delay(500);
      analogWrite(a,0);
      delay(500);
      return 0;
    }

  }
  analogWrite(a,0); **//Turn Off The Indicator LED**
  analogWrite(b,0);**//Turn Off The Indicator LED**
      
  return 1;
}
