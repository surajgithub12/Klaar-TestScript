# Klaar-TestScript

public class KlaarLoginTest {

    public static void main(String[] args) {
        // Set ChromeDriver path
        System.setProperty("webdriver.chrome.driver", "/path/to/chromedriver");

        // Initialize WebDriver
        WebDriver driver = new ChromeDriver();

        // Test Case 1: Verify Klaar company logo is present on the login page at the right place
        driver.get("https://dev.klaarhq.com");
        WebElement logo = driver.findElement(By.xpath("//img[@alt='Klaar']"));
        if (logo.isDisplayed()) {
            System.out.println("Test Case 1 Passed: Klaar company logo is present on the login page.");
        } else {
            System.out.println("Test Case 1 Failed: Klaar company logo is not present on the login page.");
        }

        // TC2 
        driver.findElement(By.xpath("(//div[@class='ant-row md:tw-justify-center'])[3]")).click();

        Thread.sleep(2000);
        driver.findElement(By.xpath(" //input[@placeholder='Enter your email or phone number here']")).sendkeys("klaar@gmail.com");
        
        driver.findElement(By.xpath(" //input[@placeholder='Enter your password here']")).sendkeys("Klaar2021");
        driver.findElement(By.xpath("//button[@type='submit']")).click();

        // Verify for wrong credentials .Check if Error message is displayed
        WebElement errorMessage = driver.findElement(By.xpath("//app-alerts[@data-cy='login-page-alert-error-message']")).gettext();
        if (errorMessage.isDisplayed()) {
            System.out.println("Test Passed: Error message displayed for wrong credentials.");
        } else {
            System.out.println("Test Failed: Error message not displayed for wrong credentials.");
        }

         
        // Verify for Successful login
        
        driver.findElement(By.xpath(" //input[@placeholder='Enter your email or phone number here']")).sendkeys(" deepa.nayak@gamma.klaar.team");
        
        driver.findElement(By.xpath(" //input[@placeholder='Enter your password here']")).sendkeys("Klaar2021");
        driver.findElement(By.xpath("//button[@type='submit']")).click();

        //Enter on Workspace page by clicking on setting button
        driver.findElement(By.xpath("(//button[@tabindex='0'])[7]")).click();

        Thread.sleep(2000);

        
          
       

        
