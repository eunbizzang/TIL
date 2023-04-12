https://www.javacodeexamples.com/java-regex-not-operator/3641


1. Using a character class
In Java regex, we can specify the character class with a “^” sign. Inside a character class, it means a NOT operator.
```
package com.javacodeexamples.regex;
 
public class RegExNotOperator {
 
    public static void main(String[] args) {
        
        String str = "There are total 12 files";
        str = str.replaceAll("[^0-9]", "");
        
        System.out.println(str);
    }
}
```
Output
: 12


2. Using a negative lookahead
The below given example searches a number in the string that is not followed by the word “out”.
```
String str = "1 out of 10 files processed";
 
Pattern pattern = Pattern.compile("(\\d+)\\s(?!out)");
Matcher matcher = pattern.matcher(str);
 
while(matcher.find()) {
    System.out.println(matcher.group(1));
}
```
Output
: 10


3. Using the negative lookbehind
For example, we want to search a number in a string that is not preceded by the start of the string as give in the below example.

```
String str = "1 out of 10 files processed";
 
Pattern pattern = Pattern.compile("(?<!^)(\\d+)");
Matcher matcher = pattern.matcher(str);
 
while(matcher.find()) {
    System.out.println(matcher.group(1));
}
```
Output
: 10


The pattern “(?<!^)(\\d+)” means that any digit one or more times that is not preceded by the start of the string. The “^” character outside a character class means the start of the string. Since we do not want to match a number at the start, the only number our pattern matches is “10” which is in the middle of the string.