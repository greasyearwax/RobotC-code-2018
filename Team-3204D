#pragma config(I2C_Usage, I2C1, i2cSensors)
#pragma config(Sensor, in1,    flippot,        sensorPotentiometer)
#pragma config(Sensor, in3,    PE,             sensorAnalog)
#pragma config(Sensor, I2C_1,  ,               sensorQuadEncoderOnI2CPort,    , AutoAssign )
#pragma config(Sensor, I2C_2,  ,               sensorQuadEncoderOnI2CPort,    , AutoAssign )
#pragma config(Sensor, I2C_3,  ,               sensorQuadEncoderOnI2CPort,    , AutoAssign )
#pragma config(Motor,  port1,           bdl,           tmotorVex393_HBridge, openLoop)
#pragma config(Motor,  port2,           fdr,           tmotorVex393_MC29, openLoop, reversed)
#pragma config(Motor,  port3,           mml,           tmotorVex393_MC29, openLoop, encoderPort, I2C_1)
#pragma config(Motor,  port4,           capflip,       tmotorVex393_MC29, openLoop)
#pragma config(Motor,  port5,           cata,          tmotorVex393_MC29, openLoop, encoderPort, I2C_3)
#pragma config(Motor,  port6,           intake,        tmotorVex393_MC29, openLoop)
#pragma config(Motor,  port7,           mmr,           tmotorVex393_MC29, openLoop, reversed, encoderPort, I2C_2)
#pragma config(Motor,  port8,           fdl,           tmotorVex393_MC29, openLoop)
#pragma config(Motor,  port9,           bdr,           tmotorVex393_MC29, openLoop, reversed)
/*
			Setting up all the motors and sensors
*/




/*
			Calling external files
*/
#pragma competitionControl(Competition)
#include "Vex_Competition_Includes.c"
#pragma platform(VEX2)

/*
			Asigning Variables
*/
int vartb = 1;
int count = 0;
int intakevar = 0;
float drvdiv = 1.2;
const short leftButton = 1;
const short centerButton = 2;
const short rightButton = 4;

/*
			Placing the drive motors in a callable function
*/

void drive(int drvspd){
	motor[fdr] = drvspd;
	motor[fdl] = drvspd/1.22;
	motor[bdr] = drvspd;
	motor[bdl] = drvspd/1.22;
	motor[mml] = drvspd/1.22;
	motor[mmr] = drvspd;

}
/*
			Fucntion for left point turn
*/
void pointleft(int drvspd){
	motor[fdr] = drvspd;
	motor[fdl] = -drvspd/1.2;
	motor[bdr] = drvspd;
	motor[bdl] = -drvspd/1.2;
	motor[mml] = -drvspd/1.2;
	motor[mmr] = drvspd;
}
/*
			Fucntion for right point turn
*/
void pointright(int drvspd){
	motor[fdr] = -drvspd;
	motor[fdl] = drvspd/1.2;
	motor[bdr] = -drvspd;
	motor[bdl] = drvspd/1.2;
	motor[mml] = drvspd/1.2;
	motor[mmr] = -drvspd;
}
/*
			Fucntion for right swing turn
*/
void swingright(int drvspd){
	motor[fdr] = drvspd;
	motor[bdr] = drvspd;
	motor[mmr] = drvspd;
}

/*
			Function for left swing turn
*/
void swingleft(int drvspd){
	motor[fdl] = drvspd/1.2;
	motor[bdl] = drvspd/1.2;
	motor[mml] = drvspd/1.2;
}
/*
			Function to reset encoders
*/
void resetsnsr(){

	nMotorEncoder[mmr] = 0;
	nMotorEncoder[mml] = 0;
}
/*
			Fucntion for Reversing drive direction
*/
void driverev(int onoff){
	if ((onoff) == 1){
		//Drive Tank
		motor[fdr] = vexRT[Ch2]/drvdiv;
		motor[fdl] = vexRT[Ch3]/drvdiv;
		motor[bdr] = vexRT[Ch2]/drvdiv;
		motor[bdl] = vexRT[Ch3]/drvdiv;
		motor[mml] = vexRT[Ch3]/drvdiv;
		motor[mmr] = vexRT[Ch2]/drvdiv;

	}
	if ((onoff) == 2){
		//Drive Tank Reversed
		motor[fdr] = -vexRT[Ch3]/drvdiv;
		motor[fdl] = -vexRT[Ch2]/drvdiv;
		motor[bdr] = -vexRT[Ch3]/drvdiv;
		motor[bdl] = -vexRT[Ch2]/drvdiv;
		motor[mml] = -vexRT[Ch2]/drvdiv;
		motor[mmr] = -vexRT[Ch3]/drvdiv;
	}
}
/*
			Function for using LCD as code chooser
*/

void waitForPress()
{
	while(nLCDButtons == 0){} //Wait for button press
	wait1Msec(5);
}

void waitForRelease()
{
	while(nLCDButtons != 0){} //wait for button release
	wait1Msec(5);
}
task lcd()
{

	string mainBattery, backupBattery, battery2Level;
	while (true)
	{
		bLCDBacklight = true;
		clearLCDLine(0);
		clearLCDLine(1);
		displayLCDString(0, 0, "Primary: ");
		sprintf(mainBattery, "%1.2f%c", nImmediateBatteryLevel/1000.0,'V');
		displayNextLCDString(mainBattery);
		displayLCDString(1, 0, "expander: ");
		battery2Level = (int)((float)SensorValue[PE] * 5.48);
		displayNextLCDString(battery2Level);
		wait1Msec(3000);
	}
}
/*
			Task for Cap flipper
*/
task capflipper()
{
	while(true){
		if(vexRT[Btn5U] == 1){

			motor[capflip] = 127;
		}
		else if (vexRT[Btn5D] == 1){

			motor[capflip] = -127;
		}
		else{
			motor[capflip] = 0;
		}
	}
}
/*
			Task for intake
*/
task intaker()
{
while(true){
	if (vexRT[Btn7U] == 1 && (intakevar == 0)){
		motor[intake]	= 127;
		wait1Msec(100);
		intakevar = 1;
}
	else if (vexRT[Btn7U] == 1 && (intakevar == 1)){
		motor[intake]	= -127;
		wait1Msec(100);
		intakevar = 2;
	}
else if (vexRT[Btn7U] == 1 && (intakevar == 2)){
		motor[intake]	= 0;
		wait1Msec(100);
		intakevar = 0;
	}
}
}
/*
			Default function for  setting up pre autonomous
*/
void pre_auton()
{
	bLCDBacklight = true;
	bStopTasksBetweenModes = true;
	clearLCDLine(0); // Clearing LCD line 1
	clearLCDLine(1); // Clearinh LCD line 2
	/*
			While loop for detection button press
	*/
	while(nLCDButtons != centerButton)
	{
		//Switch case that allows the user to choose from 4 different options
		switch(count){
		case 0:
			//Display first choice
			displayLCDCenteredString(0, "Ballcann Red");
			displayLCDCenteredString(1, "<		 Enter		>");
			waitForPress();
			//Increment or decrement "count" based on button press
			if(nLCDButtons == leftButton)
			{
				waitForRelease();
				count = 3;
			}
			else if(nLCDButtons == rightButton)
			{
				waitForRelease();
				count++;
			}
			break;
		case 1:
			//Display second choice
			displayLCDCenteredString(0, "Ballcann Blue");
			displayLCDCenteredString(1, "<		 Enter		>");
			waitForPress();
			//Increment or decrement "count" based on button press
			if(nLCDButtons == leftButton)
			{
				waitForRelease();
				count--;
			}
			else if(nLCDButtons == rightButton)
			{
				waitForRelease();
				count++;
			}
			break;
		case 2:
			//Display third choice
			displayLCDCenteredString(0, "World skills");
			displayLCDCenteredString(1, "<		 Enter		>");
			waitForPress();
			//Increment or decrement "count" based on button press
			if(nLCDButtons == leftButton)
			{
				waitForRelease();
				count--;
			}
			else if(nLCDButtons == rightButton)
			{
				waitForRelease();
				count++;
			}
			break;
		case 3:
			//Display fourth choice
			displayLCDCenteredString(0, "Nothing");
			displayLCDCenteredString(1, "<		 Enter		>");
			waitForPress();
			//Increment or decrement "count" based on button press
			if(nLCDButtons == leftButton)
			{
				waitForRelease();
				count--;
			}
			else if(nLCDButtons == rightButton)
			{
				waitForRelease();
				count = 0;
			}
			break;
		default:
			count = 0;
			break;
		}
	}
}


/*
		Task for autonomous	
*/

task autonomous()
{

	resetsnsr();

	clearLCDLine(0);
	clearLCDLine(1);
	//Switch Case that actually runs the user choice
	switch(count){
	case 0:
		//If count = 0, run the code correspoinding with choice 1
		displayLCDCenteredString(0, "Ballcann Red"); // Red alliance code
		displayLCDCenteredString(1, "is running!");
		wait1Msec(500);
		motor[fdr] = 110;
		motor[fdl] = 110;
		motor[bdr] = 110; // Drives forward
		motor[bdl] = 110;
		motor[mml] = 110;
		motor[mmr] = 110;
		wait1Msec(1500);
		motor[fdr] = 0;
		motor[fdl] = 0;
		motor[bdr] = 0;
		motor[bdl] = 0; // Stop all motors
		motor[mml] = 0;
		motor[mmr] = 0;
		wait1Msec(150);
		motor[fdr] = -110;
		motor[fdl] = -110;
		motor[bdr] = -110;
		motor[bdl] = -110; // Drive backwards
		motor[mml] = -110;
		motor[mmr] = -110;
		wait1Msec(800);
		motor[fdr] = 0;
		motor[fdl] = 0;
		motor[bdr] = 0; // Stops all motors
		motor[bdl] = 0;
		motor[mml] = 0;
		motor[mmr] = 0;
		wait1Msec(1000);							// Robot runs previous code for 1000 milliseconds before moving on
		break;
	case 1:
		//If count = 1, run the code correspoinding with choice 2
		displayLCDCenteredString(0, "Ballcann Blue");// Blue alliance code
		displayLCDCenteredString(1, "is running!");
		wait1Msec(100);
		wait1Msec(2000);
		motor[fdr] = 110;
		motor[fdl] = 110;
		motor[bdr] = 110; // Drives forward
		motor[bdl] = 110;
		motor[mml] = 110;
		motor[mmr] = 110;
		wait1Msec(1500);
		motor[fdr] = 0;
		motor[fdl] = 0;
		motor[bdr] = 0;
		motor[bdl] = 0; // Stop all motors
		motor[mml] = 0;
		motor[mmr] = 0;
		wait1Msec(150);
		motor[fdr] = -110;
		motor[fdl] = -110;
		motor[bdr] = -110;// Drive backwards
		motor[bdl] = -110;
		motor[mml] = -110;
		motor[mmr] = -110;
		wait1Msec(800);
		motor[fdr] = 0;
		motor[fdl] = 0;
		motor[bdr] = 0; // Stop all motors
		motor[bdl] = 0;
		motor[mml] = 0;
		motor[mmr] = 0;
		wait1Msec(1000);							// Robot runs previous code for 1000 milliseconds before moving on
		break;
	case 2:
		//If count = 2, run the code correspoinding with choice 3
		displayLCDCenteredString(0, "World skills"); // Word skills code
		displayLCDCenteredString(1, "is running!");
		wait1Msec(500);
		while(nMotorEncoder[mmr] < 950 && (nMotorEncoder[mml] < 950)){//Drive forward
			drive(40);
		}
		drive(0);
		resetsnsr();
		wait1Msec(500);
		while(nMotorEncoder[mmr] > -2070 && (nMotorEncoder[mml] > -2070)){//Drive backward
			drive(-40);
		}
		drive(0);
		resetsnsr();
		wait1Msec(500);
		while(nMotorEncoder[mmr] < 270 && (nMotorEncoder[mml] > -270)){//Left point turn
			pointleft(70);
		}
		drive(0);
		resetsnsr(); // Reset sensors
		wait1Msec(500);
		drive(60); // Drive forward 
		wait1Msec(2000);
		drive(0); // Stop all motors
		resetsnsr();
		wait1Msec(500);
		while(nMotorEncoder[mmr] > -670 && (nMotorEncoder[mml] > -670)){//Drive backward
			drive(-40);
		}
		drive(0);
		resetsnsr(); // Reset sensors
		wait1Msec(50);
		motor[capflip] = -127;// flip cap
		wait1Msec(350);
		motor[capflip] = -40; // Reset cap flipper
		wait1Msec(500);														//Swing Right && Pull down cap flipper
		while(nMotorEncoder[mmr] > -250){
			swingright(-40);
		}
		drive(0); // Stops all motors
		resetsnsr(); // Reset sensors
		wait1Msec(500);
		motor[capflip] = 127; 
		wait1Msec(200);
		motor[capflip] = -127;
		wait1Msec(350);							//Swing Right && Pull up cap flipper
		motor[capflip] = -40;
		wait1Msec(100);
		while(nMotorEncoder[mmr] < 250){ //Right swing turn
			swingright(40);
		}
		drive(0);
		resetsnsr();
		wait1Msec(500);
		motor[capflip] = -127;
		wait1Msec(350);
		motor[capflip] = -40;				//Swing Left && Pull down cap flipper
		wait1Msec(100);
		while(nMotorEncoder[mml] > -250){
			swingleft(-40);
		}
		drive(0);
		resetsnsr();
		wait1Msec(500);
		motor[capflip] = 127;
		wait1Msec(200);
		motor[capflip] = -127;
		wait1Msec(350);
		motor[capflip] = -40;
		wait1Msec(100);				//Swing left && Pull up cap flipper
		while(nMotorEncoder[mml] < 250){
			swingleft(40);
		}
		drive(0);
		resetsnsr();
		wait1Msec(500);
		while(nMotorEncoder[mmr] > -460 && (nMotorEncoder[mml] > -460)){//Drive backward
			drive(-40);
		}
		drive(0);
		resetsnsr();
		wait1Msec(500);
		motor[capflip] = -127;
		wait1Msec(350);
		motor[capflip] = -40;
		wait1Msec(500);							//Swing Right && Pull down cap flipper
		while(nMotorEncoder[mmr] > -250){
			swingright(-40);
		}
		drive(0);
		resetsnsr();
		wait1Msec(500);
		motor[capflip] = 127;
		wait1Msec(200);
		motor[capflip] = -127;
		wait1Msec(350);					//Swing Right && Pull up cap flipper
		motor[capflip] = -40;
		wait1Msec(100);
		while(nMotorEncoder[mmr] < 250){
			swingright(40);
		}
		drive(0);
		resetsnsr();
		wait1Msec(500);
		motor[capflip] = -127;
		wait1Msec(350);
		motor[capflip] = -40;		//Swing Left && Pull down cap flipper
		wait1Msec(100);
		while(nMotorEncoder[mml] > -250){
			swingleft(-40);
		}
		drive(0);
		resetsnsr();
		wait1Msec(500);
		motor[capflip] = 127;
		wait1Msec(200);
		motor[capflip] = -127;
		wait1Msec(350);
		motor[capflip] = -40;
		wait1Msec(100);				//Swing left && Pull up cap flipper
		while(nMotorEncoder[mml] < 250){
			swingleft(40);
		}
		drive(0);
		resetsnsr();
		wait1Msec(500);
		while(nMotorEncoder[mmr] < 1050 && (nMotorEncoder[mml] < 1050)){//Drive forward
			drive(40);
		}
		drive(0);
		resetsnsr();
		wait1Msec(500);
		while(nMotorEncoder[mmr] > -300 && (nMotorEncoder[mml] < 300)){//Right point turn
			pointright(40);
		}
		drive(0);
		resetsnsr();
		wait1Msec(500);
		while(nMotorEncoder[mmr] < 700 && (nMotorEncoder[mml] < 700)){//Drive forward
			drive(40);
		}
		drive(0);
		resetsnsr();
		wait1Msec(500);
		while(nMotorEncoder[mmr] > -300 && (nMotorEncoder[mml] < 300)){//Right point turn
			pointright(40);
		}
		drive(0);
		resetsnsr();
		wait1Msec(500); //Drive forward
		drive(127);
		wait1Msec(7000);
		drive(0);
		resetsnsr();
		wait1Msec(100);							// Robot runs previous code for 100 milliseconds before moving on
		break;
	case 3:
		//If count = 3, run the code correspoinding with choice 4
		displayLCDCenteredString(0, "Nothing"); //Code for if we want the bot to do nothing
		displayLCDCenteredString(1, "is running!");
		wait1Msec(500);

		break;
	default:
		displayLCDCenteredString(0, "No valid choice"); // Error correcting
		displayLCDCenteredString(1, "was made!");
		break;
	}
}

task usercontrol()//User control start
{
	driverev(2);
	startTask(lcd); // Start task for LCD
	startTask(intaker);// Start task for intake
	startTask(capflipper); // Start task for Cap flipper
	//	startTask(camFlipp2000);
	while (true)
	{
		if (vexRT[Btn8L] == 1  && (vartb == 0)){ // Using one button for reversing drive
			vartb = 1;
			wait1Msec(250);
		}
		if (vexRT[Btn8L] == 1  && (vartb == 1)){ // Reversing drive back to normal
			vartb = 0;
			wait1Msec(250);
		}
		if (vartb == 1){ // Drive mode 1
			driverev(1);
		}
		else if (vartb == 0){ // Drive mode 2
			driverev(2);
		}
		if (vexRT[Btn7U] == 1){// Resetting incase of error
			drvdiv = 1;
		}
	}
}
