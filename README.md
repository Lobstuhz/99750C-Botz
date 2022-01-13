# 99750C-Botz
Back-up code in case I am gone.
Transcript of code:

#include "vex.h"
using namespace vex;
competition Competition;
vex::controller Controller1 = vex::controller(vex::controllerType::primary);
vex::brain RobotBrain;
vex::triport ThreeWirePort = vex::triport(vex::PORT22);
vex::digital_out Piston1 = vex::digital_out(RobotBrain.ThreeWirePort.G);
vex::digital_out Plunger = vex::digital_out(RobotBrain.ThreeWirePort.H);
vex::motor RightFront = vex::motor(vex::PORT20,true);
vex::motor RightBack = vex::motor(vex::PORT6,true);
vex::motor LeftFront = vex::motor(vex::PORT12);
vex::motor LeftBack = vex::motor(vex::PORT5);
vex::motor LiftRight = vex::motor(vex::PORT10,vex::gearSetting::ratio36_1,true);
vex::motor LiftLeft = vex::motor(vex::PORT1,vex::gearSetting::ratio36_1);
vex::motor Backlift1 = vex::motor(vex::PORT7);
vex::motor Backlift2 = vex::motor(vex::PORT18,true);
vex::motor HDrive = vex::motor(vex::PORT13,true);
vex::motor_group Backlift(Backlift1,Backlift2);
vex::motor_group Right(RightFront,RightBack);
vex::motor_group Left(LeftFront,LeftBack);
vex::motor_group DriveTrain(RightFront,RightBack,LeftFront,LeftBack);
vex::motor_group Lift(LiftRight,LiftLeft);
vex::motor_group LDiagonal(LeftFront,RightBack);
vex::motor_group RDiagonal(RightFront,LeftBack);
vex::motor_group ForwardRight(LeftFront,RightFront,RightBack);
vex::motor_group BackwardRight(LeftBack,RightFront,RightBack);
vex::motor_group ForwardLeft(RightFront,LeftFront,LeftBack);
vex::motor_group BackwardLeft(LeftBack,RightFront,RightBack); 
int a=1;
int b=1;
void pre_auton(void){
vexcodeInit();}
void autonomous(void){
RightFront.setVelocity(90,pct);
RightBack.setVelocity(90,pct);
LeftFront.setVelocity(90,pct);
LeftBack.setVelocity(90,pct); 
Backlift.setVelocity(100,pct);
RightFront.startRotateFor(vex::directionType::fwd,1300,degrees);
RightBack.startRotateFor(vex::directionType::fwd,1300,degrees);
LeftFront.startRotateFor(vex::directionType::fwd,1300,degrees);
LeftBack.rotateFor(vex::directionType::fwd,1300,degrees);
Piston1.set(true);
Lift.rotateFor(vex::directionType::rev,90,degrees);
//back
RightFront.startRotateFor(vex::directionType::rev,1000,degrees);
RightBack.startRotateFor(vex::directionType::rev,1000,degrees);
LeftFront.startRotateFor(vex::directionType::rev,1000,degrees);
LeftBack.rotateFor(vex::directionType::rev,1000,degrees);
Backlift.rotateFor(vex::directionType::fwd,600,degrees,false);
//turn and release goal//
RightFront.startRotateFor(vex::directionType::fwd,600,degrees);
RightBack.startRotateFor(vex::directionType::fwd,600,degrees);
LeftFront.startRotateFor(vex::directionType::rev,600,degrees);
LeftBack.rotateFor(vex::directionType::rev,600,degrees);
Piston1.set(false);

}
// Lol you guys kinda stink, stnky boys
void usercontrol(void){
 bool toggle = false;
 bool latch = false;
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
if(toggle){
Right.spin(vex::forward, Controller1.Axis2.position(vex::percent),vex::percentUnits::pct);
Left.spin(vex::forward, Controller1.Axis3.position(vex::percent), vex::percentUnits::pct);
}
else{
latch = false;
} 
if(Controller1.ButtonUp.pressing()){
  if(!latch){
    toggle = !toggle;
    latch = true;}} 
else {
 latch = false; 
Right.spin(vex::forward, Controller1.Axis2.position(vex::percent),vex::percentUnits::pct);
Left.spin(vex::forward, Controller1.Axis3.position(vex::percent), vex::percentUnits::pct);
}
if(Controller1.ButtonX.pressing()){
a++;}
if(Controller1.ButtonB.pressing()){
b++;}
if(b==2){
Plunger.set(true);
wait(.1,seconds);}
else if(b==3){
Plunger.set(false);
b=1;}
if(a==2){
Piston1.set(true);
wait(.1,seconds);}
else if(a==3){
Piston1.set(false);
a=1;}
if(Controller1.ButtonR2.pressing()){
Lift.spin(vex::directionType::fwd,1000,vex::velocityUnits::pct);}
else if(Controller1.ButtonR1.pressing()){  
Lift.spin(vex::directionType::rev,1000,vex::velocityUnits::pct);}
else{
Lift.stop(vex::brakeType::hold);
if(Controller1.ButtonL1.pressing()){
Backlift.spin(vex::directionType::rev,60,vex::velocityUnits::pct);}
else if(Controller1.ButtonL2.pressing()){
Backlift.spin(vex::directionType::fwd,60,vex::velocityUnits::pct);}
else{
Backlift.stop(vex::brakeType::hold);}
if(Controller1.ButtonA.pressing()){
HDrive.spin(vex::directionType::fwd,1000,vex::velocityUnits::pct);}
else if(Controller1.ButtonY.pressing()){
HDrive.spin(vex::directionType::rev,1000,vex::velocityUnits::pct);}
else{
HDrive.stop(vex::brakeType::brake);}
wait(20,msec);
task::sleep(100);}}}
int main(){
Competition.autonomous(autonomous);
Competition.drivercontrol(usercontrol);
pre_auton();
while(true){
wait(100, msec);}}

Change log: 1/13/2022 - Page Creation
