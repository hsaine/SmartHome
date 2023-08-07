<h1 align="center"> SmartHome Project</h1>
<p align="center">
  <img src="sm.jpg" title=" SmartHome"  height="400"><br>
</p>


<h1 align="center">Abstract</h1>
The concept of a smart home, in which various appliances and systems can be controlled
and monitored remotely, has become increasingly popular in recent years. One popular method
for implementing a smart home is to use an Arduino microcontroller. The Arduino is a small,
affordable, and easy-to-use microcontroller that can be programmed to control and interact with
a variety of sensors and actuators.
In this projet, we present a smart home system that uses an Arduino Mega microcontroller to
control and monitor various appliances and systems. The system includes temperature and light
sensors, which are used to adjust the temperature and lighting in the home, as well as motion
sensors, which are used to detect movement and trigger alarms. Additionally, we also explore
the use of actuators, such as LED lights and motors, to control various aspects of the home,
such as opening and closing blinds.
The system is designed to be easy to use and requires minimal programming knowledge.
The code for the system is open-source and can be easily modified to suit the needs of the user.
The system is also designed to be expandable, meaning that additional sensors and actuators can
be added as needed. Overall, this projet demonstrates the feasibility of using an Arduino Mega
microcontroller to control and monitor various appliances and systems in a smart home. The
system is easy to use, affordable, and expandable, making it a suitable option for those looking
to implement a smart home.


<h1 align="center">The Design and Modeling of RoverBot</h1>

<h2 align="center">3D Printing</h2>
<p>
In our project, we created the basic structure of our robot using the SolidWorks CAD software. We utilized this software to design the shape of the robot's base and ensure that all parts fit together correctly. For the wheels, we used an existing model of mecanum wheels to ensure a reliable and efficient design.

Next, we employed 3D printing to manufacture all the necessary parts for the wheels in our university laboratory. This allowed us to create precise and high-quality components for our robot, which is crucial for ensuring optimal performance and durability.

By using SolidWorks and 3D printing, we successfully developed a reliable and efficient robot that fulfills all the requirements of our project. We take pride in our creation and look forward to seeing it in action.

The figures below illustrate the machines constructing different pieces of our robot:</p>
<table>
    <tr>
      <td><img src="photo1674556183 (1).jpeg" alt="Image 1" width="200"></td>
      <td><img src="photo1674556183 (2).jpeg" alt="Image 2" width="200"></td>
      <td><img src="photo1674556183 (3).jpeg" alt="Image 3" width="200"></td>
      <td><img src="photo1674556183 (4).jpeg" alt="Image 4" width="200"></td>
    </tr>
 
  </table>

<h1 align="center">HARDWARE</h1>
<p>We will use stepper motors, an A4988 driver, and an Arduino Mega board to build a holonomic mobile robot. Stepper motors are electric motors that can be controlled step by step, allowing for extremely precise control. The A4988 driver is a microstepping driver that simplifies the control of stepper motors by integrating a translator for easy use. The Arduino Mega board is a popular development board with enough output pins to connect the stepper motors and sufficient memory to store the control code. By combining these components, we will be able to construct a holonomic mobile robot capable of precise and controlled movements</p>

<h3>Arduino Mega</h3>
An Arduino Mega board can be used to drive 4 stepper motors for a mobile robot as it provides enough output pins to connect all 4 motors. Additionally, it has sufficient memory to store the necessary code for motor control. By using a stepper motor driver like A4988, which can be connected to the Arduino Mega, it becomes easy to control the stepper motors with simple high-level commands. Lastly, the Arduino Mega is a popular platform for robotics projects due to its user-friendliness and a large community of developers.
<p align="center">
  <img src="arduino.jpeg" alt="Image 2" width="200">
</p>

<h3>The A4988 Stepper Motor Driver</h3>
The A4988 is a micro-stepping driver designed to control bipolar stepper motors and features a built-in translator for easy use. This means we can control the stepper motor with just 2 pins from our controller: one for controlling the direction of rotation and the other for controlling the steps. The driver offers five different step resolutions: full step, half-step, quarter-step, eighth-step, and sixteenth-step. Additionally, it includes a potentiometer for adjusting the output current, thermal shutdown protection in case of overheating, and protection against cross-currents.
Its logic voltage ranges from 3 to 5.5V, and the maximum current per phase is 2A if proper additional cooling is provided or 1A of continuous current per phase without a heatsink or cooling.
<p align="center">
<img  src="driver.jpg" alt="Image 2" width="200"></td>
</p>

<h3>Stepper Motor</h3>
A stepper motor is an electric motor whose main characteristic is that its shaft rotates by taking steps, which means it moves a fixed amount of degrees with each step. This feature is achieved through the internal structure of the motor and allows for knowing the exact angular position of the shaft by simply counting the number of steps taken, without the need for a sensor. This characteristic also makes it suitable for a wide range of applications.
<p align="center">
<img src="moteur.jpg" alt="Image 2" width="200"></td>
</p>
<h1 align="center">Realization</h1>
<h3>Algorithm explantion</h3>
Our algorithm for this mobile robot project involves using a matrix to represent the maze, where each cell is numbered based on its distance to the destination. The destination itself is marked with "0", adjacent cells are marked with "1", cells next to the "1" marked cells are marked with "2", and so on until all cells are filled. Then, the robot is placed in a random cell and uses this matrix to plan the shortest path to reach the destination while avoiding obstacles, which are defined as cells with high values in the matrix. In our example, we have a 5*5 maze, and we provide the robot with the destination (4,3).

<h3>Code</h3>
<p>The code of our project is presented below for your reference :</p>

```
// CNC Shield Stepper  Control Demo
// Superb Tech
// www.youtube.com/superbtech

#include<stdlib.h>
#include<time.h>

#define INT_MAX 1000

#define row 5
#define col 5

// object coordinates
#define objrow 1
#define objcol 1
//destination coordinates
#define destrow 3
#define destcol 3

const int StepX = 2;
const int DirX = 5;
const int StepY = 3;
const int DirY = 6;
const int StepZ = 4;
const int DirZ = 7;
const int StepA = 12;
const int DirA = 13;

void afficherMatrice(int m[row][col]){
	// afficher matrice.
   
	for (int i = 0; i < row; i++) {
		for (int j = 0; j < col; j++){
            if(m[i][j]==404){
                Serial.print("X");
        Serial.print("  ");
            }else if(m[i][j]==100){
				Serial.print("R");
        Serial.print("  ");
        
			}else{
                Serial.print(m[i][j]);
        Serial.print("  ");
            }
            }

		Serial.println(" ");
	}

}

void forward(){
 digitalWrite(DirX, HIGH); // set direction, HIGH for clockwise, LOW for anticlockwise
 digitalWrite(DirY, HIGH);
 digitalWrite(DirZ, LOW);
 digitalWrite(DirA, LOW);
 
 for(int x = 0; x<700; x++) { // loop for 200 steps
  digitalWrite(StepX,HIGH);
  digitalWrite(StepY,HIGH);
  digitalWrite(StepZ,HIGH);
  digitalWrite(StepA,HIGH);
  delayMicroseconds(3000);
  digitalWrite(StepX,LOW); 
  digitalWrite(StepY,LOW);
  digitalWrite(StepZ,LOW);
  digitalWrite(StepA,LOW);
  delayMicroseconds(3000);
 
  
}
}
void right(){
 digitalWrite(DirX, LOW); // set direction, HIGH for clockwise, LOW for anticlockwise
 digitalWrite(DirY, HIGH);
 digitalWrite(DirZ, LOW);
 digitalWrite(DirA, HIGH);
 
 for(int x = 0; x<200; x++) { // loop for 200 steps
  digitalWrite(StepX,HIGH);
  digitalWrite(StepY,HIGH);
  digitalWrite(StepZ,HIGH);
  digitalWrite(StepA,HIGH);
  delayMicroseconds(3000);
  digitalWrite(StepX,LOW); 
  digitalWrite(StepY,LOW);
  digitalWrite(StepZ,LOW);
  digitalWrite(StepA,LOW);
  delayMicroseconds(3000);
 
  
}
}
void left(){
 digitalWrite(DirX, HIGH); // set direction, HIGH for clockwise, LOW for anticlockwise
 digitalWrite(DirY, LOW);
 digitalWrite(DirZ, HIGH);
 digitalWrite(DirA, LOW);
 
 for(int x = 0; x<200; x++) { // loop for 200 steps
  digitalWrite(StepX,HIGH);
  digitalWrite(StepY,HIGH);
  digitalWrite(StepZ,HIGH);
  digitalWrite(StepA,HIGH);
  delayMicroseconds(3000);
  digitalWrite(StepX,LOW); 
  digitalWrite(StepY,LOW);
  digitalWrite(StepZ,LOW);
  digitalWrite(StepA,LOW);
  delayMicroseconds(3000);
 
  
}
}
void backward(){
 digitalWrite(DirX, LOW); // set direction, HIGH for clockwise, LOW for anticlockwise
 digitalWrite(DirY, LOW);
 digitalWrite(DirZ, HIGH);
 digitalWrite(DirA, HIGH);
 
 for(int x = 0; x<200; x++) { // loop for 200 steps
  digitalWrite(StepX,HIGH);
  digitalWrite(StepY,HIGH);
  digitalWrite(StepZ,HIGH);
  digitalWrite(StepA,HIGH);
  delayMicroseconds(3000);
  digitalWrite(StepX,LOW); 
  digitalWrite(StepY,LOW);
  digitalWrite(StepZ,LOW);
  digitalWrite(StepA,LOW);
  delayMicroseconds(3000);
 
  
}
}
void backright(){
 digitalWrite(DirX, LOW); // set direction, HIGH for clockwise, LOW for anticlockwise
 digitalWrite(DirY, LOW);
 digitalWrite(DirZ, LOW);
 digitalWrite(DirA, LOW);
 
 for(int x = 0; x<575; x++) { // loop for 200 steps
  digitalWrite(StepZ,HIGH);
  digitalWrite(StepA,HIGH);
  delayMicroseconds(500);
  digitalWrite(StepX,HIGH);
  digitalWrite(StepY,HIGH);
  delayMicroseconds(1000);
  digitalWrite(StepZ,LOW); 
  digitalWrite(StepA,LOW);
  delayMicroseconds(500);
  digitalWrite(StepX,LOW);
  digitalWrite(StepY,LOW);
  delayMicroseconds(1000);
 
  
}
}
void backleft(){
 digitalWrite(DirX, HIGH); // set direction, HIGH for clockwise, LOW for anticlockwise
 digitalWrite(DirY, HIGH);
 digitalWrite(DirZ, HIGH);
 digitalWrite(DirA, HIGH);
 
 for(int x = 0; x<500; x++) { // loop for 200 steps
  digitalWrite(StepZ,HIGH);
  digitalWrite(StepA,HIGH);
  delayMicroseconds(500);
  digitalWrite(StepX,HIGH);
  digitalWrite(StepY,HIGH);
  delayMicroseconds(1000);
  digitalWrite(StepZ,LOW); 
  digitalWrite(StepA,LOW);
  delayMicroseconds(500);
  digitalWrite(StepX,LOW);
  digitalWrite(StepY,LOW);
  delayMicroseconds(1000);
 
  
}
}

void stop(){
 digitalWrite(DirX, LOW); // set direction, HIGH for clockwise, LOW for anticlockwise
 digitalWrite(DirY, LOW);
 digitalWrite(DirZ, HIGH);
 digitalWrite(DirA, HIGH);
 
 for(int x = 0; x<200; x++) { // loop for 200 steps
  digitalWrite(StepX,LOW); 
  digitalWrite(StepY,LOW);
  digitalWrite(StepZ,LOW);
  digitalWrite(StepA,LOW);
  delayMicroseconds(3000);
 
  
}
}


void setup() {
  pinMode(StepX,OUTPUT);
  pinMode(DirX,OUTPUT);
  pinMode(StepY,OUTPUT);
  pinMode(DirY,OUTPUT);
  pinMode(StepZ,OUTPUT);
  pinMode( DirZ,OUTPUT);
  pinMode(StepA,OUTPUT);
  pinMode( DirA,OUTPUT);
  Serial.begin(9600);

}

void loop() {
  delay(1000);
 forward();
 
 delay(1000);
 backright();
 delay(1000);
 forward();
 
 

/*
// initiation des variables

	srand(time(0));

//matrice initial

	int mat[row][col];

	for( int i = 0; i < row; ++i)
	{for( int j = 0;  j < col; ++j)
	    {mat[i][j] = 0;}
	}

// on met le 1 pour notre distination

	mat[destrow][destcol] = 1;

// matrice des distances

	int ans[row][col];

	// remplire la matrice resultante avec INT_MAX pour resoudre le problem de overwrite avec zeroes
	for (int i = 0; i < row; i++)
		for (int j = 0; j < col; j++){
			ans[i][j] = INT_MAX;}


	// remplissage avec distances
	for (int i = 0; i < row; i++)
		for (int j = 0; j < col; j++) {
			// traverser la matrice pour trouver la distance minimale
			for (int k = 0; k < row; k++)
				for (int l = 0; l < col; l++) {
					// si cellule = 1 , on pose distance minimal
					if (mat[k][l] == 1)
						ans[i][j] = min(ans[i][j],abs(i - k) + abs(j - l));
				}
		}
  // definir un object qui doit arriver a la destination, on lui donne la value 100 et le symbol @

	int distance = ans[objrow][objcol];
	
	int originalobjrow = objrow;
	int originalobjcol = objcol;

	ans[originalobjrow][originalobjcol]=100;
  afficherMatrice(ans);
	Serial.println(" ");

  int min = INT_MAX;

	int tempobjrow = objrow;
	int tempobjcol = objcol;
	int oldobjrow = 0;
	int oldobjcol= 0;
  int move=0;

  while(distance!=0){

		if(ans[originalobjrow][originalobjcol-1]<min){
			min = ans[tempobjrow][tempobjcol-1];
			oldobjcol = tempobjcol;
			tempobjcol = tempobjcol - 1;
			move = 1;
      left();
		}
		if(ans[originalobjrow-1][originalobjcol]<min){
			min = ans[tempobjrow-1][tempobjcol];
			oldobjrow = tempobjrow;
			tempobjrow = tempobjrow-1;
			move = 1;
      forward();
		}
		if(ans[originalobjrow+1][originalobjcol]<min){
			min = ans[tempobjrow+1][tempobjcol];
			oldobjrow = tempobjrow;
			tempobjrow = tempobjrow+1;
			move = 1;
      backward();
		}
		if(ans[originalobjrow][originalobjcol+1]<min){
			min = ans[tempobjrow][tempobjcol+1];
			oldobjcol = tempobjcol;
			tempobjcol = tempobjcol+1;
			move = 1;
      right();
    
		}

  ans[tempobjrow][tempobjcol]=100;
	originalobjrow = tempobjrow;
	originalobjcol = tempobjcol;
	distance--;


	
afficherMatrice(ans);
	Serial.println(" ");

	move = 0;
  }
 */

}
```

<h1 align="center">Simulation</h1>
<p>You can find the video demonstrating the project:</p>
[https://www.youtube.com/embed/zyvgy9-6oCM?start=52
](https://drive.google.com/file/d/1IrPB5lr-Z72NIShX7uRKxQu5Tsus6s-f/view?usp=sharing)
<h1 align="center">Team</h1>
<ul>
	<li> Ayoub Hsaine</li>
	<li> Achraf Rachid</li>
	<li> Mohamed Mouad Ouhasni </li>
	<li> Aymane Baddou</li>
	<li> Ilhame Soufi</li>

</ul>


