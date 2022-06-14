Link : https://developer.mozilla.org/en-US/docs/Web/API/Event/preventDefault

Event.preventDefault()

calling preventDefault() for a non-cancelable event, such as one dispatched via EventTarget.dispatchEvent(), without specifying cancelable: true has no effect.


```ex.js
function checkName(evt) {
  var charCode = evt.charCode;
  if (charCode != 0) {
    if (charCode < 97 || charCode > 122) {
      evt.preventDefault();
      displayWarning(
        "Please use lowercase letters only."
        + "\n" + "charCode: " + charCode + "\n"
      );
    }
  }
}
```