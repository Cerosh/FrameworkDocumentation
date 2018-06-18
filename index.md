### Framework Documentation
## Annotations
There are three built annotations in Java and they are there `@Deprecated`, `@Override`, `@SuppressWarnngs`. Annotations can be applied to class, interface, method and field. Custom annotation can be created using the `@interface` followd by the class name. Custom annotation can have elements but should not provide implementations but can provide default values. While using the annotation in a class those elements which has default value can be excluded or updated for new values. Array elements are also allowed in annotations.Custom annotation can use four type of annotations they are
`@Documented`, annotation indicates that element using this annotation should be documentd by Java Doc.
`@Target`, annotation specifies where this can be used and since this is an optional one if its not mentioned then the annotation would be applied to all elements.
`@Inherited`, annotation signals that the all elements of base class which is inherting from the parent class should also inherit this.
`@Retention`, annotation indicates how long annotations are to be retained using the Retention policy.
## Exceptions
## PageFactory
## Enumerations
Enum is a special type of data type which is basically a collection of constants.
```Java
public class EnumDemo {
    public enum Oceans{
        Pacific  ("P"), 
        Atlantic  ("A"), 
        Indian  ("I"), 
        Arctic  ("Ar"),
        Southern ("S"); 
        private final String shortCode;
	
	    Oceans(String code) {
            this.shortCode = code;
        }
	  
        public String getOceansShortCode() {
            return this.shortCode;
        }
    }
    public static void main(String[] args) {
    	Oceans oceanName = Oceans.Pacific;
    	System.out.println(oceanName.getOceansShortCode());
    }
}
```
## Drivers
## PropertyFiles
## BaseTest
## PageObjects
## TestListeners
Listeners are interfaces used in Selenium WebDriver scripts. Listners allow customising TestNG reports or logs. There are many Listeners `ITestListner` is one among them. various methods are available in ITestListner one is: `onTestFailure()`. Using this method we can capture the screen shots of the failed cases and log the failed methods.
## TestPages
## Logs
## Screenshot
## Inheritance
## Interface
## HtmlElements
This framework is designed by a third party called yandex to provide an easy-to-use way of interacting with web-page elements in tests. This framework can be considered to be an extension of WebDriver Page Object. With the help of the Html Elements framework we can group web-page elements into blocks, encapsulate logic of interaction within them and then easily use created blocks in page objects. 
To use the HtmlElements library, just needed to add the dependency to the `POM.xml`.
```xml
<dependency>
    <groupId>ru.yandex.qatools.htmlelements</groupId>
    <artifactId>htmlelements-java</artifactId>
    <version>1.19</version>
</dependency>
```
Run the mvn clean compile command to test that your project is being compiled.
### Example of using HtmlElements
As an example, take the main page of Yandex (http://www.yandex.ru). Let's describe for the beginning a simple element, for example a search string:

```Java
public class SearchArrow extends HtmlElement {

    @FindBy(xpath = ".//input[@class='search2__input']")
    public TextInput requestInput;

    @FindBy(xpath = ".//input[@class='search2__button']")
    public Button searchButton;

    public void searchFor(String request) {
        requestInput.clear();
        requestInput.sendKeys(request);
        searchButton.click();
    }
}
```
The `searchFor()` method uses 2 elements, requestInput and searchButton. They dont use the WebElement type but new ones (TextInput and Button). The `@FindBy` annotations is used not only by the elements of the `SearchArrow` class but also by the class itself.The framework  define a class for each type of HTML element (TextInput, Button). The `@FindBy` annotation can be used not only for elements but also for the classes. The `@FindBy` annotation can be used for objects with the TextInput and Button classes.  There is a class for each type of html element which are the TestInput and Button class. All these classes extend another class called `TypifiedElement`. Because of the inheritance, TextInput can use all protected/public methods of TypifiedElement. In addition, it defines methods for getting text and clearing value. Since there is no `driver` or `By locator` passed as parameter It implements the `WebDriver` interface .
The `PageFactory.initElements()` can initialize TextInput and Button elements.This class describes the structure of the search string and the logic of interaction with it. Next, you need to create a MainPage class that contains the search string:
```Java
public class MainPage {

    private WebDriver driver;

    @FindBy(className = "home-arrow__search")
    private SearchArrow searchArrow;

    public MainPage(final WebDriver driver) {
        PageFactory.initElements(new HtmlElementDecorator(driver), this);
        this.driver = driver;
    }

    public SearchPage searchFor(String request) {
        this.searchArrow.searchFor(request);
        return new SearchPage(driver);
    }

}
```
As you can see, the initialization of internal staple elements MainPage is invoked in the constructor is used by the custom decorator of the class fields: `HtmlElementDecorator()`. Since the field 'searchArrow' is the successor of HtmlElements, its initialization occurs recursively. Thus, the internal elements of the search string are also initialized:

protected WebElement requestInput;
protected WebElement searchButton;
As you can see from the description, the searchFor method returns an instance of the search page. We describe it:
```Java
public class SearchPage {

    private WebDriver driver;

    @FindBy(className = "b-serp-list")
    private SearchResults searchResults;

    @FindBy(className = "b-morda-search-form")
    private SearchArrow searchArrow;

    public SearchPage(WebDriver driver) {
        PageFactory.initElements(new HtmlElementDecorator(driver), this);
        this.driver = driver;
    }

    public SearchPage searchFor(String request) {
        this.searchArrow.searchFor(request);
        return this;
    }

    public SearchResults getSearchResults() {
        return this.searchResults;
    }
}
```
The searchFor() method uses a SearchArrow class object for executing search. it does not declare any web element fields and annotations (like a standard page factory implementation). it declares a searchArrow field for the SearchArrow class which is then initialized in the class’s constructor; the standard page factory implementation does this only for web elements.
In order to check this, we create a simple test to check the search results, in which we create a copy of our page:
```Java
public class SearchingByRequestTest {

    private final int DEFAULT_RESULTS_COUNT;

    public WebDriver driver = new FirefoxDriver();

    public SearchingByRequestTest() {
        DEFAULT_RESULTS_COUNT = 10;
    }

    @Before
    public void loadStartPage() {
        driver.get("http://www.yandex.ru");
    }

    @Test
    public void afterSearchingUserShouldSeSearchResults() {
        MainPage mainPage = new MainPage(driver);
        SearchPage page = mainPage.searchFor("Yandex");
        assertThat(page.getSearchResults(), exists());
        assertThat(page.getSearchResults().getSearchItems(), hasSize(DEFAULT_RESULTS_COUNT));
    }

    @After
    public void killWebDriver() {
        driver.quit();
    }
}
```
The test uses an object of the SearchPage page class and interacts with it through its methods.
In this example, you see that after initializing the MainPage itself, the internal elements were initialized.

```markdown
Syntax highlighted code block
## HashMap
HashMap basically designates unique keys to corresponding values and those values can be stored in a map by forming a key-value pair. The value can be retrieved using the key by passing it to the correct method.
```Java
public void HashMap_Example(){
	    Map<String, String> objMap = new HashMap<String, String>();
	    objMap.put("Name", "Suzuki");
	    objMap.put("Power", "220");
	    objMap.put("Type", "2-wheeler");
	    objMap.put("Price", "85000");
	    System.out.println("Elements of the Map:"+ objMap);
	    System.out.println("Is there a Power Key: " + objMap.containsKey("Name"));
	    System.out.println("Is there a 2-wheeler Value: " + objMap.containsValue("2-wheeler"));
	    System.out.println("Name key : " + objMap.get("Name"));
	    System.out.println("All the available keys: " + objMap.keySet());
	    System.out.println("All the available values : " + objMap.values());
	  }
```

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/Cerosh/FrameworkDocumentation/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
