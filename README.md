
<img width="1929" height="1216" alt="Screenshot 2025-11-06 194755" src="https://github.com/user-attachments/assets/6427abdf-ae17-4753-8465-288240991620" />
[CSC170-main.zip](https://github.com/user-attachments/files/23482890/CSC170-main.zip)

# CSC170
Smashing dots is a game where you try to avoid the red big balls and get to the blue balloons to raise your health and continue the game
Code for MyWorld:
import greenfoot.*;  // (World, Actor, GreenfootImage, Greenfoot and MouseInfo)

/**
 * Write a description of class MyWorld here.
 * 
 * @author (your name) 
 * @version (a version number or a date)
 */
public class MyWorld extends World
{
       private GreenfootSound backgroundMusic;
    /**
     * Constructor for objects of class MyWorld.
     * 
     */
    
   
    public MyWorld()
    {    
       
        // Create a new world with 600x400 cells with a cell size of 1x1 pixels.
        super(600, 400, 1); 
        
         backgroundMusic = new GreenfootSound("Yameii.wav");
        backgroundMusic.setVolume(25);
        backgroundMusic.playLoop();
    }
        public void stopped() {
        if (backgroundMusic != null && backgroundMusic.isPlaying()) {
            backgroundMusic.stop();
        }
    } 
        public void started() {
        if (backgroundMusic != null && !backgroundMusic.isPlaying()) {
            backgroundMusic.playLoop();
        }
    }
      public void nextLevel()
    {
        // Minimal implementation - just so the method exists
        System.out.println("Next level called!");
    }
    }








   code for realDot:

   import greenfoot.*;  // (World, Actor, GreenfootImage, Greenfoot and MouseInfo)

/**
 * Write a description of class realDot here.
 * 
 * @author (your name) 
 * @version (a version number or a date)
 */
public class realDot extends Actor
{
    /**
     * Act - do whatever the realDot wants to do. This method is called whenever
     * the 'Act' or 'Run' button gets pressed in the environment.
     */
    private int health = 3;
    
 private GreenfootSound backgroundMusic;  
    public void act()
    {
                
        // Add your action code here.
        if (Greenfoot.isKeyDown("up")){
        setLocation(getX(), getY() - 5);
        }
        if (Greenfoot.isKeyDown("down")){
        setLocation(getX(), getY() + 5);
    }
     if (Greenfoot.isKeyDown("left")){
        setLocation(getX() - 5, getY());
        }
        if (Greenfoot.isKeyDown("right")){
        setLocation(getX() + 5, getY());
    }

    checkCollision();
    checkCollision1();
   checkHealth();

    }
    
    
    public void checkCollision(){
    Actor otherDot = getOneIntersectingObject(EvilDots.class);
    
    if (otherDot != null){
    loseHealth(1);
    setLocation(getX() - 30, getY() - 30);
    }
}

public void checkCollision1(){
    Actor otherDot = getOneIntersectingObject(HealthPickup.class);
    
    if (otherDot != null){
    gainHealth(1);
    setLocation(getX() - 30, getY() - 30);
    }
}

    public void checkHealth(){
    if (health <= 0 ){
    getWorld().removeObject(this);
}
}


public void loseHealth(int amount){
health = health - amount;

System.out.println(health + "  ");
System.out.println("Ouch!");

}

public void gainHealth(int amount){
health = health + amount;

System.out.println(health + "  ");
System.out.println("Wandava!");

}

public int getHealth(){
return health + 1;
}
public void addHealth(int amount)
{
    health = health + amount;
    System.out.println("Health gained! Current Health is " + health);
 
}
}








code for EvilDots:      
import greenfoot.*;  // (World, Actor, GreenfootImage, Greenfoot and MouseInfo)

/**
 * Write a description of class EvilDots here.
 * 
 * @author (your name) 
 * @version (a version number or a date)
 */
public class EvilDots extends Actor
{
    /**
     * Act - do whatever the EvilDots wants to do. This method is called whenever
     * the 'Act' or 'Run' button gets pressed in the environment.
     */
    private int direction = 1;
    private int speed = 2;
    
    public void act()
    {
        // Add your action code here.
      setLocation(getX() + (direction * speed), getY());
      
      if (getX() <= 0 || getX() >= getWorld().getWidth() -1){
        direction *= -1;
        }
        if(isTouching(realDot.class)){
        Greenfoot.playSound("CollideSound.wav");
        }
}
}








code for HealthPicksUp:

import greenfoot.*;

public class HealthPickup extends Actor
{
    
    
    //Constructor
   
    
    public void act()
    {
       
    }
   

        
    }




