# Klaar-TestScript
import org.openqa.selenium.support.ui.Select;
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
        driver.findElement(By.xpath("//input[@placeholder='Organization name']")).sendkeys("Klaar");
        driver.findElement(By.xpath("//button[@class='ant-btn ant-btn-primary']")).click();

        // Verify for Organization chart configuration

        WebElement dropdown = driver.findElement(By.xpath("//nz-select[@nzplaceholder='Select head of Org Chart']"));
         
        Select d = new Select(dropdown);
        d.selectByVisibleText("Akshay(akshat)");

        d.selectByVisibleText("A(asas)");
          
        d.deselectByVisibleText("Akshay(akshat)");
        driver.findElement(By.xpath("(//button[@class='ant-btn ant-btn-primary'])[2]")).click();

        // Wait for the popup message to appear
        WebDriverWait wait = new WebDriverWait(driver, 5);
        Alert popup = wait.until(ExpectedConditions.alertIsPresent());

        // Get the text of the popup message
        String popMessage = popup.getText();
        System.out.println("Popup message: " + message);
        if (popupMessage.isDisplayed()) {
            System.out.println("Test Passed: Org chart configuration saved ");
        } else {
            System.out.println("Test Failed: Org chart configuration not saved ");
        }

        // Verify for uploading new Workspace logo

        driver.findElement(By.xpath("//button[@nzsize='large']")).sendkeys("C:\\Users\\SURAJ\\Downloads\\Klaar.png");
         driver.findElement(By.xpath("//button[@class='ant-btn ant-btn-link']")).click();
        Webelement workspaceLogo =  driver.findElement(By.xpath("//img[@class='orgShortLogo']"));

        if (workspaceLogo.isDisplayed()) {
            System.out.println("Test Passed: Logo uploaded ");
        } else {
            System.out.println("Test Failed: logo not uploaded ");
        }
        
        // Verify for editing Workspace logo
         driver.findElement(By.xpath("//button[@data-cy='settings-workspace-logo-edit-button']")).sendkeys("C:\\Users\\SURAJ\\Downloads\\Klaar.png");
         driver.findElement(By.xpath("//button[@class='ant-btn ant-btn-link']")).click();
        Webelement workspaceLogo =  driver.findElement(By.xpath("//img[@class='orgShortLogo']"));

        if (workspaceLogo.isDisplayed()) {
            System.out.println("Test Passed: Logo is edited ");
        } else {
            System.out.println("Test Failed: logo not not edited ");
        }

        //Verify for deleting uploaded Workspace logo

        driver.findElement(By.xpath("//button[@data-cy=' settings-workspace-logo-delete-button']")).click();
        Thread.sleep(2000);
        
       Webelemet Deletelogo = driver.findElement(By.xpath("//button[@class='ant-btn']")).click();

        // Verify the successful removal by checking if the logo element is no longer present
        boolean isLogoPresent = driver.findElements(By.id("//div[@class='ant-spin-container ng-star-inserted']")).isEmpty();
        if (isLogoPresent) {
            System.out.println("Workspace logo successfully deleted.");
        } else {
            System.out.println("Failed to delete workspace logo.");
        }

        // Close the browser
        driver.quit();
    }
}
         
      
# Test script for Test 2 - Add a New User 
     public class AddUser {

	    public static void main(String[] args) throws
     {
        System.setProperty("webdriver.chrome.driver", "/path/to/chromedriver");

        // Initialize WebDriver
        WebDriver driver = new ChromeDriver();

        driver.get("https://dev.klaarhq.com");
        
        driver.findElement(By.xpath(" //input[@placeholder='Enter your password here']")).sendkeys("Klaar2021");
        driver.findElement(By.xpath("//button[@type='submit']")).click();

        // Click on settings button

        driver.findElement(By.xpath("(//button[@tabindex='0'])[7]")).click();
        webelement userlist = driver.findElement(By.xpath("//a[@href='/settings/workspace/User-List']")).click();
        if (userlist.isDisplayed()) {
            System.out.println("Test Passed: Landed on All Users page ");
        } else {
            System.out.println("Test Failed: Not landed on All Users page");
        }

        // Verify for adding new user

        Thread.sleep(2000);
	    
	   WebElement Add = driver.findElement(By.xpath("//button[@data-cy='settings-user-list-add-user-button']"));
	    
	   Actions act=new Actions(driver);
	   
	   act.moveToElement(Add).perform();
	   
	   Thread.sleep(2000);
	   
	   driver.findElement(By.xpath("//li[@data-cy='settings-user-list-add-single-user-button']")).click();

        // Check for error handling message by giving invalid email id
       driver.findElement(By.xpath("//nz-input-group[@class='ng-tns-c282-3564 ant-input-affix-wrapper']")).sendkeys("Deepa");
       webelement errormessage = driver.findElement(By.xpath("//nz-input-group[@class='ng-tns-c282-3565 ant-input-affix-wrapper']")).sendkeys("df@.com");
         if (errorMessage.isDisplayed()) {
            System.out.println("Error handling testing passed");
        } else {
            System.out.println("Error handling testing passed");
        }

        // Verify with valid email id
         driver.findElement(By.xpath("//nz-input-group[@class='ng-tns-c282-3564 ant-input-affix-wrapper']")).sendkeys("Deepa");
         driver.findElement(By.xpath("//nz-input-group[@class='ng-tns-c282-3565 ant-input-affix-wrapper']")).sendkeys("df@gmail.com");

        
       // Department dropdown

       WebElement dropdown = driver.findElement(By.xpath("//input[@autocomplete='off']"));
         
        Select d = new Select(dropdown);
        d.selectByVisibleText("Engineering");

        // Title dropdown
         WebElement dropdown = driver.findElement(By.xpath("(//input[@autocomplete='off'])[2]"));
         
        Select d = new Select(dropdown);
        d.selectByVisibleText("QA");

        // Manager dropdown
         WebElement dropdown = driver.findElement(By.xpath("(//input[@autocomplete='off'])[3]"));
         
        Select d = new Select(dropdown);
        d.selectByVisibleText("A(asas@gmail.com");

        // Verify User ID input box
        driver.findElement(By.xpath("//input[@formcontrolname='user_id']")).sendkeys("K0123");

        // Verify Location input box
         driver.findElement(By.xpath("//input[@formcontrolname='location']")).sendkeys("Pune");

        // Check user checkbox
        driver.findElement(By.xpath("//input[@type='checkbox']")).click();

        // Verify for HRBP dropdown
        WebElement dropdown = driver.findElement(By.xpath("(//input[@autocomplete='off'])[4]"));
         
        Select d = new Select(dropdown);
        d.selectByVisibleText("A(asas@gmail.com");

        // Submit by clicking add now button
        webelement Edituser = driver.findElement(By.xpath(" //button[@data-cy='modal-submit-button']")).click();
        if (Edituser.isDisplayed()) {
            System.out.println("Landed on Edit user page");
        } else {
            System.out.println("Not landed on Edit user page");
        }
        
        Thread.sleep(2000);

        // Click on save button on Edit user page
        driver.findElement(By.xpath("//button[@data-cy='settings-edit-user-save-button']")).click();

        // Return to the All Users page and confirm visibility in the user list table.

        driver.navigate().back();

        webelement userDeepa = driver.findElement(By.xpath(" //input[@data-cy='user-list-search-text-field']")).sendkeys("Deepa");

         if (userDeepa.isDisplayed()) {
            System.out.println("New user name Deepa is successfully added");
        } else {
            System.out.println("New user name Deepa is not added");
        }

        
        




       
        

        




       


        

        

        

      
          
	   



    








        
