import greenfoot.*;  // (World, Actor, GreenfootImage, Greenfoot and MouseInfo)

public class MyWorld extends World
{
    private int timer = 0;
    private int spawnDelay = 100;
    private GreenfootSound backgroundMusic;
    private int playerHealth = 3;
    private realDot player; // This is your instance variable

    public MyWorld()
    {
        super(600, 400, 1); 
        prepare();
        
        backgroundMusic = new GreenfootSound("Yameii.wav");
        backgroundMusic.setVolume(75);
        backgroundMusic.playLoop();
    }

    private void prepare(){
        // FIX: Remove "realDot" to use the instance variable, not create a local one
        player = new realDot();
        addObject(player, getWidth()/2, getHeight()/2);
        
        // Spawn some initial objects
        spawnInitialObjects();
        updateHealthDisplay(); // Initialize health display
    }
    
    public void act()
    {
        spawnObjects();
        updateHealthFromPlayer(); // Update health display each act cycle
    }
    
    private void updateHealthFromPlayer() {
        if (player != null && player.getWorld() != null) {
            int currentHealth = player.getHealth();
            if (currentHealth != playerHealth) {
                playerHealth = currentHealth;
                updateHealthDisplay();
            }
        }
    }
    
    private void updateHealthDisplay() {
        // Display health in top-left corner
        showText("Health: " + playerHealth, 60, 20);
    }
    
    private void spawnInitialObjects(){
        for (int i = 0; i < 3; i++) {
            spawnEvilDot();
        }
        // Spawn some health pickups at start
        for (int i = 0; i < 2; i++) {
            spawnHealthPickup();
        }
    }
    
    private void spawnObjects(){
        timer++;
        
        if (timer % spawnDelay == 0) {
            spawnEvilDot();
        }
        
        // Spawn health pickups less frequently
        if (timer % (spawnDelay * 3) == 0) {
            spawnHealthPickup();
        }
        
        // Reset timer if it gets too large
        if (timer > 1000) { 
            timer = 0;
        }
    }
    
    private void spawnEvilDot(){
        EvilDots evilDot = new EvilDots();
        
        int edge = Greenfoot.getRandomNumber(4); // 0-3
        int x = 0, y = 0;
        
        switch (edge){
            case 0: 
                x = Greenfoot.getRandomNumber(getWidth());
                y = 0;
                break;
            case 1: 
                x = getWidth();
                y = Greenfoot.getRandomNumber(getHeight());
                break;
            case 2: 
                x = Greenfoot.getRandomNumber(getWidth());
                y = getHeight();
                break;
            case 3: 
                x = 0;
                y = Greenfoot.getRandomNumber(getHeight());
                break;
        }
        addObject(evilDot, x, y);
    }
    
    private void spawnHealthPickup() {
        if (getObjects(HealthPickup.class).size() < 3){
            HealthPickup health = new HealthPickup();
            int x = Greenfoot.getRandomNumber(getWidth());
            int y = Greenfoot.getRandomNumber(getHeight());
            addObject(health, x, y);
        }
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
}


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


import greenfoot.*;

public class HealthPickup extends Actor
{
    
    
    
    // Constructor
   
    
    public void act()
    {
       
    }
   

        
    }


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
    private int maxHealth = 5;
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


private void loseHealth(int amount){
health = health - amount;


}

private void gainHealth(int amount){
health = health + amount;



}

 

public int getHealth(){
    if(health == 1){
    health = health - 1;
    
    }
return health;
}
public void addHealth(int amount)
{
    health = health + amount;
   
 
}
 
}
    


    






