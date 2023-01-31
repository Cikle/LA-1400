```java
package LutzigerCyril;
import robocode.*;

/**
 * //Egg - a robot by (Lutziger Cyril)
 */
public class Egg extends JuniorRobot
{

	public void run() {
	
		setColors(white, white, white, white, white);
		
		//Turns and goes to the under part of the map
		int i = 10;
		turnTo(0);
		back(fieldHeight);
		turnRight(90);


		while(true) {
			
		 ahead(100);
		 turnGunRight(360);
		 ahead(100);
			if(i % 10 == 0){
				turnGunRight(360);
				
		
				
			}
		}
	}

	
	public void onScannedRobot() {
	
		//int for scanning
		int scannedDistance_ = scannedDistance;
		int scannedVelocity_ = scannedVelocity;
		turnGunTo(scannedAngle);
		int gunHeading_ = gunHeading;
		int scannedAngle_ = gunHeading_;
		int scannedHeading_ = scannedHeading;
		
		//Cheking, if everything is scanned right
		out.println("ScannedDistance: " + scannedDistance_);
		out.println("ScannedVelocity: " + scannedVelocity_);
		out.println("gunHeading: "  + gunHeading_);
		
		//Calculating the bullet travel time
		int timeForBullet = scannedDistance_ / 14;
		int distanceTraveled = scannedVelocity_ * timeForBullet;
		
		//Calculating the distance that could be traveled by the target
		int angleForCalc = scannedAngle_ - 180;
		int beta = angleForCalc - scannedHeading_;
		
		//Calculates the lenght of the shooting path
		double Path =  Math.sqrt(Math.pow(scannedDistance_, 2) + Math.pow(distanceTraveled, 2) - 2 * scannedDistance_ * distanceTraveled * Math.cos(beta));
	
		double preAimAngle = Math.acos((Math.pow(scannedDistance_, 2) + Math.pow(Path, 2) - Math.pow(distanceTraveled, 2)) / 2*scannedDistance_*Path);
	
		int AimedAngle = (int)preAimAngle;
		int PreAimed = 0;
		
		//Checks if Angle is under 360 degrees 
		if(scannedAngle_ + preAimAngle > 360){
			PreAimed = scannedAngle_ + AimedAngle - 360;
		}
		else{
			PreAimed = scannedAngle_ + AimedAngle;
		}
				
	
		out.println("Path: " + Path);
		out.println("PreAimAngle: " + preAimAngle);
		out.println("gunHeading: " + gunHeading);
		out.println("After" + PreAimed);
		
		//Firing to the calculated Angle
		turnGunTo(PreAimed);
		fire(3);
		


	
			
		
	   
		
	}

	public void onHitByBullet() {
		
		turnRight(30);
		ahead(30);
		turnLeft(30);
		ahead(70);
		
	}
	

	public void onHitWall() {
	
		turnRight(90);
		turnGunRight(90);
		ahead(50);
	}	
}
```
