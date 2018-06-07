## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/Cerosh/FrameworkDocumentation/edit/master/index.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown
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

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block


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
