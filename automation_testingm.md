<h1> Automation test cases </h1>	

I chose **Selenium Webdriver** as an an automation testing framework for the website

<br/>


<h3>Scenario 1: User Registration and Login</h3>

<h4>Happy path - user registration</h4>

```
public class RegistrationTest {

    private WebDriver driver;
    private String baseUrl = "https://automationteststore.com/index.php?rt=account/login";
    private String firstName = "Hannah";
    private String lastName = "James"
    private String email = "hannah.jones@gmail.com";
    private String address1 = "Radićeva ulica 35";
    private String city = "Zagreb";
    private String zipCode = "10000";
    private String loginName = "HannahJames";
    private String password = "FQqJL@7E6t3J";
    private String passwordConfirm = "FQqJL@7E6t3J";


    @BeforeClass
    public void setUp() {
        System.setProperty("webdriver.chrome.driver", "path_to_chromedriver_executable");
        driver = new ChromeDriver();
        driver.get(baseUrl);
    }

    @Test
    public void testUserRegistrationWithValidInformation() {
        // Navigate to register page by clicking on Continue button
        WebElement continueButton = driver.findElement(By.cssSelector("input[title='Continue']"));
        continueButton.click();

        // Register a new user
        register(firstName, lastName, email, address1, city, zipCode, loginName, password, passwordConfirm);
        
        // Verify if registration was successful
        WebElement registerSuccess = driver.findElement(By.xpath("//*[text()='Your Account Has Been Created!']"));
        Assert.assertTrue(registerSuccess.isDisplayed(), "The registration failed");
    }

    private void register(String firstName, String lastName, String email, String address1, String city, String zipCode, String loginName, String password, String                                     passwordConfirm) {
        WebElement firstNameInput = driver.findElement(By.id("AccountFrm_firstname"));
        WebElement lastNameInput = driver.findElement(By.id("AccountFrm_lastname"));
        WebElement emailInput = driver.findElement(By.id("AccountFrm_email"));
        WebElement address1Input = driver.findElement(By.id("AccountFrm_address_1"));
        WebElement cityInput = driver.findElement(By.id("AccountFrm_city"));
        WebElement postcodeInput = driver.findElement(By.id("AccountFrm_postcode"));
        WebElement loginNameInput = driver.findElement(By.id("AccountFrm_loginname"));
        WebElement passwordInput = driver.findElement(By.id("AccountFrm_password"));
        WebElement passwordConfirmInput = driver.findElement(By.id("AccountFrm_confirm"));
        WebElement agreePrivacy = driver.findElement(By.id("AccountFrm_agree"));

        firstNameInput.sendKeys(firstName);
        lastNameInput.sendKeys(lastName);
        emailInput.sendKeys(email);
        address1Input.sendKeys(address1);
        cityInput.sendKeys(city);
        postcodeInput.sendKeys(zipCode);
        loginNameInput.sendKeys(loginName);
        passwordInput.sendKeys(password);
        passwordConfirmInput.sendKeys(passwordConfirm);
        agreePrivacy.click();

        // Choose region from dropdown menu
        Select region = new Select(driver.findElement(By.id("AccountFrm_zone_id")));
        region.selectByVisibleText("Zagreb");

        // Click on Continue button
        WebElement continueButton = driver.findElement(By.cssSelector("input[title='Continue']"));
        continueButton.click();
    }

        @AfterClass
        public void tearDownClass() {
        // Close the WebDriver instance after all tests in the class
        if (driver != null) {
        driver.quit();
        }
    }
}

```


<h4>Happy path - user login</h4>

```

public class LoginTest {

    private WebDriver driver;
    private String baseUrl = "https://automationteststore.com/index.php?rt=account/login";
    private String loginName = "HannahJames";
    private String password = "FQqJL@7E6t3J";


    @BeforeClass
    public void setUp() {
        System.setProperty("webdriver.chrome.driver", "path_to_chromedriver_executable");
        driver = new ChromeDriver();
        driver.get(baseUrl);
    }

    @Test
    public void testUserLoginWithValidCredentials() {
        // Perform the login action
        login(loginName, password);

        // Verify if login was successful
        WebElement loginSuccess = driver.findElement(By.xpath("//a[text()='My Account']"));
        Assert.assertTrue(loginSuccess.isDisplayed(), "The login failed");
    }

    private void login(String loginName, String password) {
        WebElement loginNameInput = driver.findElement(By.id("loginFrm_loginname"));
        WebElement passwordInput = driver.findElement(By.id("loginFrm_password"));
        WebElement loginButton = driver.findElement(By.cssSelector("input[title='Login']"));

        loginNameInput.sendKeys(loginName);
        passwordInput.sendKeys(password);
        loginButton.click();
    }

    @AfterClass
    public void tearDownClass() {
        // Close the WebDriver instance after all tests in the class
        if (driver != null) {
            driver.quit();
        }
    }
}

```


