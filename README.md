# 99750C-Botz
Back-up code in case I am gone.
Transcript of code:

#include "vex.h"

// ---- START VEXCODE CONFIGURED DEVICES ----
// Robot Configuration:
// [Name]               [Type]        [Port(s)]
// Smile                inertial      15              
// ---- END VEXCODE CONFIGURED DEVICES ----
using namespace vex;
competition Competition;
vex::controller Controller1 = vex::controller(vex::controllerType::primary);
vex::controller Controller2 = vex::controller(vex::controllerType::partner);
vex::brain RobotBrain;
vex::triport ThreeWirePort = vex::triport(vex::PORT22);
vex::digital_out Piston1 = vex::digital_out(RobotBrain.ThreeWirePort.G);
vex::digital_out UnderPiston = vex::digital_out(RobotBrain.ThreeWirePort.F);
vex::motor RightFront = vex::motor(vex::PORT20,true);
vex::motor RightBack = vex::motor(vex::PORT6,true);
vex::motor LeftFront = vex::motor(vex::PORT5);
vex::motor LeftBack = vex::motor(vex::PORT12);
vex::motor LiftRight = vex::motor(vex::PORT10,vex::gearSetting::ratio36_1,true);
vex::motor LiftLeft = vex::motor(vex::PORT1,vex::gearSetting::ratio36_1);
vex::motor Backlift2 = vex::motor(vex::PORT7);
vex::motor Backlift1 = vex::motor(vex::PORT18,true);
vex::motor_group Backlift(Backlift1,Backlift2);
vex::motor_group Right(RightFront,RightBack);
vex::motor_group Left(LeftFront,LeftBack);
vex::motor_group Lift(LiftRight,LiftLeft);
vex::motor_group LDiagonal(LeftFront,RightBack);
vex::motor_group RDiagonal(RightFront,LeftBack);
vex::motor_group ForwardRight(LeftFront,RightFront,RightBack);
vex::motor_group BackwardRight(LeftBack,RightFront,RightBack);
vex::motor_group ForwardLeft(RightFront,LeftFront,LeftBack);
vex::motor_group BackwardLeft(LeftBack,RightFront,RightBack); 
vex::smartdrive DriveTrain(Right,Left,Smile,12.56,17.25,17.5, distanceUnits::in);
//Declare Variables//
int PlatCount = 1;
bool PlatToggle = false;
int FrontLiftCount=0;
int BackLiftCount=0;
bool FrontLock = false;
bool BackLock = false;


//Begin Pre_Auton
void pre_auton(void){

vexcodeInit();
Smile.calibrate();}

void autonomous(void){  
//start auto (usually by setting motor speeds,etc)//
RightFront.setVelocity(90,pct);
RightBack.setVelocity(90,pct);
LeftFront.setVelocity(90,pct);
LeftBack.setVelocity(90,pct); 
//
RightFront.startRotateFor(vex::directionType::fwd,1320,degrees);
RightBack.startRotateFor(vex::directionType::fwd,1320,degrees);
LeftFront.startRotateFor(vex::directionType::fwd,1320,degrees);
LeftBack.rotateFor(vex::directionType::fwd,1320,degrees);
Piston1.set(true);
Lift.rotateFor(vex::directionType::rev,90,degrees);
//back
RightFront.startRotateFor(vex::directionType::rev,800,degrees);
RightBack.startRotateFor(vex::directionType::rev,800,degrees);
LeftFront.startRotateFor(vex::directionType::rev,800,degrees);
LeftBack.rotateFor(vex::directionType::rev,700,degrees);
//turn and release goal//
RightFront.startRotateFor(vex::directionType::fwd,600,degrees);
RightBack.startRotateFor(vex::directionType::fwd,600,degrees);
LeftFront.startRotateFor(vex::directionType::rev,600,degrees);
LeftBack.rotateFor(vex::directionType::rev,600,degrees,false);
wait(1.5,seconds);
Piston1.set(false);
RightFront.setVelocity(50,pct);
RightBack.setVelocity(50,pct);
LeftFront.setVelocity(50,pct);
LeftBack.setVelocity(50,pct); 
RightFront.startRotateFor(vex::directionType::rev,100,degrees);
RightBack.startRotateFor(vex::directionType::rev,100,degrees);
LeftFront.startRotateFor(vex::directionType::rev,100,degrees);
LeftBack.rotateFor(vex::directionType::rev,100,degrees);
wait(.4,seconds);
//first turn
RightFront.startRotateFor(vex::directionType::fwd,200,degrees);
RightBack.startRotateFor(vex::directionType::fwd,200,degrees);
LeftFront.startRotateFor(vex::directionType::rev,200,degrees);
LeftBack.rotateFor(vex::directionType::rev,200,degrees);
wait(.5,seconds);
RightFront.startRotateFor(vex::directionType::rev,500,degrees);
RightBack.startRotateFor(vex::directionType::rev,500,degrees);
LeftFront.startRotateFor(vex::directionType::rev,500,degrees);
LeftBack.rotateFor(vex::directionType::rev,500,degrees);
//2nd turn now
RightFront.startRotateFor(vex::directionType::rev,290,degrees);
RightBack.startRotateFor(vex::directionType::rev,290,degrees);
LeftFront.startRotateFor(vex::directionType::fwd,290,degrees);
LeftBack.rotateFor(vex::directionType::fwd,290,degrees);
wait(.6,seconds);
RightFront.startRotateFor(vex::directionType::rev,1200,degrees);
RightBack.startRotateFor(vex::directionType::rev,1200,degrees);
LeftFront.startRotateFor(vex::directionType::rev,1200,degrees);
LeftBack.rotateFor(vex::directionType::rev,1200,degrees);
//
wait(.3,seconds);
RightFront.startRotateFor(vex::directionType::fwd,70,degrees);
RightBack.startRotateFor(vex::directionType::fwd,70,degrees);
LeftFront.startRotateFor(vex::directionType::rev,70,degrees);
LeftBack.rotateFor(vex::directionType::rev,70,degrees);
//go forward to our alliance zone
RightFront.startRotateFor(vex::directionType::fwd,1300,degrees);
RightBack.startRotateFor(vex::directionType::fwd,1300,degrees);
LeftFront.startRotateFor(vex::directionType::fwd,1300,degrees);
LeftBack.rotateFor(vex::directionType::fwd,1300,degrees);
}


void usercontrol(void){
//Logo//
//brain is 480x240 resolution//
Brain.Screen.setPenColor(red);
Brain.Screen.setFillColor(black);
Brain.Screen.setPenWidth(15);
Brain.Screen.drawCircle(240,120,80);
Brain.Screen.setPenWidth(30);
Brain.Screen.drawLine(160,120,130,120);
Brain.Screen.drawLine(320,120,350,120);
Brain.Screen.drawLine(240,200,240,230);
Brain.Screen.drawLine(240,40,240,10);
Brain.Screen.drawLine(180,60,160,40);
Brain.Screen.drawLine(300,60,320,40);
Brain.Screen.drawLine(180,180,160,200);
Brain.Screen.drawLine(300,180,320,200);
Brain.Screen.setCursor(6,20);
Brain.Screen.setFont(mono20);
Brain.Screen.print(" SPARTAS'S");
Brain.Screen.setCursor(7,22);
Brain.Screen.print(" BOTZ");
Brain.Screen.setCursor(5,22);
Brain.Screen.print("99750C");
while(true){
//Begin While Loop//

//Pneumatic Front Lift//

if (Controller1.ButtonX.pressing()){
FrontLiftCount++;}
if (FrontLiftCount == 2){
Piston1.set(true);}
else if (FrontLiftCount == 4){
Piston1.set(false);
FrontLiftCount = 0;}

//Pneumatic Back Lift//

if (Controller2.ButtonB.pressing()){
BackLiftCount++;}
if (BackLiftCount == 2){
UnderPiston.set(true);}
else if (BackLiftCount == 4){
UnderPiston.set(false);
BackLiftCount = 0;}

//Tank Control DriveTrain//  
if(Controller2.ButtonUp.pressing()){
      PlatCount++;
    }
    if(PlatCount == 3){
      PlatToggle = true;
    }
    else if(PlatCount == 5){
      PlatToggle = false;
      PlatCount = 1;
    }

if(PlatToggle == false){
Right.spin(vex::forward, Controller1.Axis2.position(vex::percent),vex::percentUnits::pct);
Left.spin(vex::forward, Controller1.Axis3.position(vex::percent), vex::percentUnits::pct);}
else if(PlatToggle == true){
  Right.stop(vex::brakeType::hold);
  Left.stop(vex::brakeType::hold);
  RobotBrain.Screen.clearScreen();
  RobotBrain.Screen.setFont(mono40);
  RobotBrain.Screen.print("BRAKES TOGGLED");
  
}
//Front and Back Lift//
if(Controller2.ButtonR2.pressing()){
Lift.spin(vex::directionType::fwd,1000,vex::velocityUnits::pct);}
else if(Controller2.ButtonR1.pressing()){  
Lift.spin(vex::directionType::rev,1000,vex::velocityUnits::pct);}
else{
Lift.stop(vex::brakeType::hold);}
if(Controller2.ButtonL2.pressing()){
Backlift.spin(vex::directionType::fwd,1000,vex::velocityUnits::pct);}
else if(Controller2.ButtonL1.pressing()){  
Backlift.spin(vex::directionType::rev,1000,vex::velocityUnits::pct);}
else{
Backlift.stop(vex::brakeType::hold);}


task::sleep(100);
} //End While Loop//
} //End Driver Control//

int main(){
Competition.autonomous(autonomous);
Competition.drivercontrol(usercontrol);
pre_auton();
while(true){
wait(100, msec);}}
        /*----*/
        //    //
        //    //
//------//----//-------//
//------//----//-------//
        //    //
        //----//

Change log: 1/13/2022 - Page Creation
            2/8/2022 - Updated Code
