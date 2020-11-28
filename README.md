public class LoginPage {

    WebDriver webDriver;
    WebDriverWait webDriverWait;

    public LoginPage(WebDriver webDriver)
    {
        this.webDriver=webDriver;
        this.webDriverWait=new WebDriverWait(webDriver,30,150);
    }

    public void login(String username,String password)
    {
        //1
        webDriver.get("https://www.n11.com/");
        Assert.assertEquals("n11.com - Hayat Sana Gelir",webDriver.getTitle());
        webDriver.findElement(By.cssSelector(".btn.btnBlack")).click();
        webDriverWait.until(ExpectedConditions.elementToBeClickable(By.className("btnSignIn"))).click();

        JavascriptExecutor executor = (JavascriptExecutor)webDriver;
        executor.executeScript("document.body.style.zoom = '0.98'");

        //2
        webDriver.findElement(By.id("email")).clear();
        webDriver.findElement(By.id("email")).sendKeys(username);
        webDriver.findElement(By.id("password")).clear();
        webDriver.findElement(By.id("password")).sendKeys(password);
        webDriver.manage().timeouts().implicitlyWait(20, TimeUnit.SECONDS);
        webDriver.findElement(By.xpath("/html/body/div[1]/div[2]/div/div[1]/div/div/div[1]/div/form/div[4]")).click();
        Assert.assertEquals("n11.com - Hayat Sana Gelir",webDriver.getTitle());

        //3
        WebElement searchData=webDriver.findElement(By.id("searchData"));
        searchData.clear();
        searchData.sendKeys("Samsung");
        searchData.sendKeys(Keys.ENTER);

        //4
        Assert.assertEquals("Samsung - n11.com",webDriver.getTitle());

        //5
        webDriverWait.until(ExpectedConditions.elementToBeClickable(By.xpath("//*[@id=\"contentListing\"]/div/div/div[2]/div[5]/a[2]"))).click();
        Assert.assertEquals("https://www.n11.com/arama?q=Samsung&pg=2",webDriver.getCurrentUrl());

        //6
        webDriverWait.until(ExpectedConditions.elementToBeClickable(By.xpath("//*[@id=\"p-440132201\"]/div[1]/span"))).click();
        //7
        webDriverWait.until(ExpectedConditions.elementToBeClickable(By.xpath("//*[@id=\"header\"]/div/div/div[2]/div[2]/div[2]/div[2]/div/a[2]"))).click();
        webDriverWait.until(ExpectedConditions.elementToBeClickable(By.xpath("//*[@id=\"myAccount\"]/div[3]/ul/li[1]/div/a"))).click();
        //8
        Assert.assertEquals("Samsung Galaxy S20 128 GB (Samsung Türkiye Garantili)",webDriver.findElement(By.xpath("//*[text()='Samsung Galaxy S20 128 GB (Samsung Türkiye Garantili)']")));
        //9
        webDriverWait.until(ExpectedConditions.elementToBeClickable((By.xpath("//*[@id=\"p-440132201\"]/div[3]/span")))).click();

        //10
        Assert.assertEquals("message",webDriver.findElement(By.className("message")));
        webDriver.findElement(By.cssSelector(".btn.btnBlack.confirm")).click();
    }
}
