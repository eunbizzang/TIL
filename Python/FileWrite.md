https://www.w3schools.com/python/python_file_write.asp



File Handling

The key function for working with files in Python is the open() function.

The open() function takes two parameters; filename, and mode.

There are four different methods (modes) for opening a file:

* "r" - Read - Default value. Opens a file for reading, error if the file does not exist

* "a" - Append - Opens a file for appending, creates the file if it does not exist

* "w" - Write - Opens a file for writing, creates the file if it does not exist

* "x" - Create - Creates the specified file, returns an error if the file exists

In addition you can specify if the file should be handled as binary or text mode

* "t" - Text - Default value. Text mode

* "b" - Binary - Binary mode (e.g. images)

Write to an Existing File

To write to an existing file, you must add a parameter to the open() function:

* "a" - Append - will append to the end of the file

* "w" - Write - will overwrite any existing content


Delete a File

To delete a file, you must import the OS module, and run its os.remove() function:

Example
Remove the file "demofile.txt":
```
import os
os.remove("demofile.txt")
```

Check if File exist:

To avoid getting an error, you might want to check if the file exists before you try to delete it:

Example
Check if file exists, then delete it:
```
import os
if os.path.exists("demofile.txt"):
  os.remove("demofile.txt")
else:
  print("The file does not exist")
```

Delete Folder

To delete an entire folder, use the os.rmdir() method:

Example
Remove the folder "myfolder":
```
import os
os.rmdir("myfolder")
```


