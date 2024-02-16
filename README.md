# Klaar-TestScript
# Test 1 - Workspace setting

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
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

 
        // Close the browser
        driver.quit();
    }
}


 # Test script for Test 3 - User custom fields

 public class UserCustomFields {
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

        // Navigate to custom field page
	driver.findElement(By.xpath( "//div[@class='ant-tabs-tab ng-star-inserted ant-tabs-tab-active']]")).click();

	// Add new custom field of type "date"
 	driver.findElement(By.xpath( " //input[@placeholder='Enter field name...']")).sendkeys("Klaar");
        
 	 WebElement dropdown = driver.findElement(By.xpath("//input[@autocomplete='off']"));
         
        Select d = new Select(dropdown);
        d.selectByVisibleText("Date");

 	driver.findElement(By.xpath("//button[@data-cy='modal-submit-button']")).click();

        // Verify that the added custom field is reflected in the custom field page
   	
        webelement custom = driver.findElement(By.xpath("(//tr[@class='row ng-star-inserted']/descendant::td)[10]"));
	if (custom.isDisplayed()) {
            System.out.println("Test Passed:  Klaar is added successfully on custom field list ");
        } else {
            System.out.println("Test Failed:  Klaar is not added successfully on custom field list");
        }


       // Add a new custom field of type List with 3 list options

       driver.findElement(By.xpath( " //input[@placeholder='Enter field name...']")).sendkeys("Best Klaar");
        
 	 WebElement dropdown = driver.findElement(By.xpath("//input[@autocomplete='off']"));
         
        Select d = new Select(dropdown);
        d.selectByVisibleText("list");
	driver.findElement(By.xpath( "//input[@placeholder='Option List']")).sendkeys("K1");
        webelement Add =  driver.findElement(By.xpath("(//div[@class='modal footer-available']/descendant::button)[2]"));
        Add.click();
	driver.findElement(By.xpath( "(//input[@placeholder='Option List'])[2]")).sendkeys("K2");
        Add.click();
	driver.findElement(By.xpath( "(//input[@placeholder='Option List'])[3]")).sendkeys("K3");

 	driver.findElement(By.xpath("//button[@data-cy='modal-submit-button']")).click();

  	// Verify that Best Klaar name is dispalayed on custom field list

        webelement userlist = driver.findElement(By.xpath("(//tr[@class='row ng-star-inserted']/descendant::td)[2]"));
	 if (userlist.isDisplayed()) {
            System.out.println("Test Passed: Best Klaar is added successfully on custom field list ");
        } else {
            System.out.println("Test Failed: Best Klaar is not added successfully on custom field list");
        }

        // Test the custom field switch on/off toggle and verify changes are reflected respectively in the user company details page

 	// Locate the toggle button element
        WebElement toggleButton = driver.findElement(By.xpath("//button[@class='ant-switch ant-switch-checked']"));

        // Get the initial state of the toggle button
        boolean isToggleButtonEnabled = toggleButton.isSelected();
        System.out.println("Toggle button is enabled: " + isToggleButtonEnabled);

         // Switch off the toggle button if it's currently on
        if (isToggleButtonEnabled) {
            toggleButton.click();
        }

        // Get the new state of the toggle button
        isToggleButtonDisabled = toggleButton.isSelected();
        System.out.println("Toggle button is disabled: " + isToggleButtonDisabled);

         // Switch on the toggle button if it's currently off
        if (!isToggleButtonDisabled) {
            toggleButton.click();
        }

       // Get the new state of the toggle button
        isToggleButtonEnabled = toggleButton.isSelected();
        System.out.println("Toggle button is enabled: " + isToggleButtonEnabled);

       //  Delete the added custom field (Deleting Klaar)

       driver.findElement(By.xpath(" (//span[@nztype='delete'])[3]")).click();

      // Verify that deleted Klaar custom field is not dispalyed on custom field table
       
       Thread.sleep(2000);

       List<WebElement> deletedElements = driver.findElements(By.xpath("(//tr[@class='row ng-star-inserted']/descendant::td)[10]"));

      // Verify if the element is deleted
      if (deletedElements.size() == 0) 
      {
     System.out.println("Element successfully deleted");
     } else {
              System.out.println("Element deletion failed");
            }
    
     // Close the browser
        driver.quit();
    }
}
       

      
  

       

 



      
        



        
        




       
        

        




       


        

        

        

      
          
	   



    








        
