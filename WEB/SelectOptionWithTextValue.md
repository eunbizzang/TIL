https://www.darklaunch.com/jquery-select-option-using-text-value-text.html

this saved me!
```
var selectOptionText = "wobble";
$("#select-2").find("option").filter(function(index) {
    return selectOptionText === $(this).text();
}).prop("selected", "selected");
```