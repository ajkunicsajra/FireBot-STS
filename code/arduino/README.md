#include<Servo.h>

Servo myServo1;
int pos1 = 90;

Servo myServo2;
int pos2 = 90;

int motorA = 2;
int motorB = 4;
int motora = 3;
int motorb = 5;
int pwm1 = 9;
int pwm2 = 10;

const int relayPin1 = 6;
const int relayPin2 = 11;
const int relayPin3 = 12;

const int reflektor = 13;

const int trigPinFront = 14;
const int echoPinFront = 15;
const int trigPinLeft = 16;
const int echoPinLeft = 17;
const int trigPinRight = 18;
const int echoPinRight = 19;
long duration;
int distanceFront, distanceLeft, distanceRight;


void setup() {
  pinMode(motorA, OUTPUT);
  pinMode(motorB, OUTPUT);
  pinMode(motora, OUTPUT);
  pinMode(motorb, OUTPUT);

  pinMode(pwm1, OUTPUT);
  pinMode(pwm2, OUTPUT);

  pinMode(relayPin1, OUTPUT);
  pinMode(relayPin2, OUTPUT);
  pinMode(relayPin3, OUTPUT);

  pinMode(reflektor, OUTPUT);

  myServo1.attach(7); //Povezivanje
  myServo2.attach(8); //Povezivanje

  pinMode(trigPinFront, OUTPUT);
  pinMode(echoPinFront, INPUT);
  pinMode(trigPinLeft, OUTPUT);
  pinMode(echoPinLeft, INPUT);
  pinMode(trigPinRight, OUTPUT);
  pinMode(echoPinRight, INPUT);
  Serial.begin(9600);

}

//funkcija za senzore
int getDistance(int trigPin, int echoPin){
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  
  duration = pulseIn(echoPin, HIGH);
  return duration * 0,034 / 2;
}


void loop() {

  if (Serial.available()) {
  char komanda = Serial.read();

    if (komanda == 'S') {  //autic nazad
      digitalWrite(motorA, LOW);
      digitalWrite(motorB, HIGH);
      digitalWrite(motora, LOW);
      digitalWrite(motorb, HIGH);
      analogWrite(pwm1, 150);
      analogWrite(pwm2, 150);
    }
 
    else if (komanda == 'W'){ //autic naprijed
      distanceFront = getDistance(trigPinFront, echoPinFront);

      if(distanceFront <= 20){
        digitalWrite(motorA, LOW);
        digitalWrite(motorB, LOW);
        digitalWrite(motora, LOW);
        digitalWrite(motorb, LOW);
      }

      else{
        digitalWrite(motorA, HIGH);
        digitalWrite(motorB, LOW);
        digitalWrite(motora, HIGH);
        digitalWrite(motorb, LOW);
        analogWrite(pwm1, 150);
        analogWrite(pwm2, 150);
      }
    }
 
    else if (komanda == 'D') {  //autic desno
      distanceRight = getDistance(trigPinRight, echoPinRight);

      if(distanceRight <= 20){
        digitalWrite(motorA, LOW);
        digitalWrite(motorB, LOW);
        digitalWrite(motora, LOW);
        digitalWrite(motorb, LOW);
      }

      else{
        digitalWrite(motorA, HIGH);
        digitalWrite(motorB, LOW);
        digitalWrite(motora, HIGH);
        digitalWrite(motorb, LOW);
        analogWrite(pwm1, 50);
        analogWrite(pwm2, 150);
      }
    }

    else if (komanda == 'A') {  //autic lijevo
      distanceLeft = getDistance(trigPinLeft, echoPinLeft);

      if(distanceLeft <= 20){
        digitalWrite(motorA, LOW);
        digitalWrite(motorB, LOW);
        digitalWrite(motora, LOW);
        digitalWrite(motorb, LOW);
      }
  
      else{
        digitalWrite(motorA, HIGH);
        digitalWrite(motorB, LOW);
        digitalWrite(motora, HIGH);
        digitalWrite(motorb, LOW);
        analogWrite(pwm1, 150);
        analogWrite(pwm2, 50);
      }
    }

    else if(komanda == 'G'){//pumpa se gasi
      digitalWrite(relayPin1, HIGH);
    }

    else if(komanda == 'H'){//pumpa se pali
      digitalWrite(relayPin1, LOW);
    }

    else if(komanda == 'I'){//ide gore prskalica
      for(int pos1 = pos1; pos1 <= 150; pos1++){
        myServo1.write(pos1);
      }
    }

    else if(komanda == 'K'){//ide dolje prskalica
      for(int pos1 = pos1; pos1 >= 30; pos1--){
        myServo1.write(pos1);
      }
    }

    else if(komanda == 'L'){//ide desno
      for(int pos2 = pos2; pos2 <= 150; pos2++){
        myServo2.write(pos2);
      }
    }

    else if(komanda == 'J'){//ide lijevo
      for(int pos2 = pos2; pos2 >= 30; pos2--){
        myServo2.write(pos2);
      }
    }

    else if(komanda == 'T'){//aktuator relej 1 se pali
      digitalWrite(relayPin2, HIGH);
      digitalWrite(relayPin3, LOW);
    }

    else if(komanda == 'Z'){//aktuator relej 2 se pali
      digitalWrite(relayPin2, LOW);
      digitalWrite(relayPin3, HIGH);
    }
  
    else if(komanda == 'R' ){//reflektor se pali
      digitalWrite(reflektor, LOW);
    }

    else if(komanda == 'E' ){//reflektor se gasi
      digitalWrite(reflektor, HIGH);
    }

    else{
      digitalWrite(motorA, LOW);
      digitalWrite(motorB, LOW);
      digitalWrite(motora, LOW);
      digitalWrite(motorb, LOW);

      //gasi aktuator
      digitalWrite(relayPin2, HIGH);
      digitalWrite(relayPin3, HIGH);
    }
  }
}
 
 
