# Pakistan Mobile Number Validator
RegEx for validating mobile numbers of Pakistan. To change it to work for your country just change `92` and `3` with your country code. Also you can change length of numbers by changing last `{9}`

    ^((\+92)?(0092)?(92)?(0)?)(3)([0-9]{9})$/gm
     
Test it online on [RegExr](https://regexr.com/62e7a) or [RegEx101](https://regex101.com/r/h7LIjZ/2) 
    
## Explanation:  
There are `three` groups: 

|Group|Description|
|--|--|
|92 \| +92 \| 0092 \| 0  | Allow any integer at beginning  |
| 3 | Must be having `3` |
|001234567| Allow any integers between 0-9 but of length `9`|


Breakdown:  
`(\92)`? Allow `92` and is optional  
`((\+92)?` Allow `+92` and is optional  
`(0092)?` Allow `0092` and is optional  
`(0)?)` Allow only `0` and is optional  
`(3)` `3` is mandatory because Pakistani numbers starts with `3xx`  
`([0-9]{9})` Allow any numbers from 0 to 9, but length should be exactly `9`  




## Above RegEx will Validate



    +923001234567
    00923001234567
    923001234567
    03001234567
    3001234567




## Doesn't Validate 
    +3001234567 (92 is missing)
    +933001234567 (Country code is 92)
    +924001234567 (Because of missing 3)
    +92300123456720 (Too many numbers)
    030012345672  (Too many numbers)
    30012345673 (Too many numbers)
    0030012345673 (Too many numbers)





To use it in code use as mentioned by [John](https://stackoverflow.com/a/22344145/5737774):

      public static boolean isSingaporeMobileNo(String str) {
          Pattern mobNO = Pattern.compile("^((\\+92)?(0092)?(92)?(0)?)(3)([0-9]{9})$");
          Matcher matcher = mobNO.matcher(str);
          if (matcher.find()) {
              return true;
          } else {
              return false;
          }
      }


or


    import java.util.regex.Matcher;
    import java.util.regex.Pattern;

    public class Example {
        public static void main(String[] args) {
            final String regex = "^((\\+92)?(0092)?(92)?(0)?)(3)([0-9]{9})$";
            final String string = "// Validate it\n\n"
                                   + "+923001234567\n"
                                   + "00923001234567\n"
                                   + "923001234567\n"
                                   + "03001234567\n"
                                   + "3001234567\n\n\n"
                                   + "// Don't Validate \n"
                                   + "+3001234567\n"
                                   + "+933001234567\n"
                                   + "+9230012345672\n"
                                   + "+923001234567200\n"
                                   + "030012345672\n"
                                   + "30012345673";

        final Pattern pattern = Pattern.compile(regex, Pattern.MULTILINE);
        final Matcher matcher = pattern.matcher(string);
        
        while (matcher.find()) {
            System.out.println("Full match: " + matcher.group(0));
            
            for (int i = 1; i <= matcher.groupCount(); i++) {
                System.out.println("Group " + i + ": " + matcher.group(i));
                    }
                }
            }
        }

# To allow Dash (-) and White Space

If you want it to allow dash `-` or `space` you can use this one:  

        /^((\+92)?(0092)?(92)?(0)?)(3)([0-9]{2})((-?)|( ?))([0-9]{7})$/gm
        
Test it online on [RegExr](https://regexr.com/62e63)  
        
it will pass these two formats (along with above mentioned): 

        0300 1234567
        0300-1234567
        
And will reject `0300- 1234567` because it has both white space and dash. 



# Another Solution  
Another solution can be found [here](https://stackoverflow.com/a/24101520/5737774) by Giacomo1968 on StackOverflow as:  

        ^((\+92)|(0092))-{0,1}\d{3}-{0,1}\d{7}$|^\d{11}$|^\d{4}-\d{7}$




