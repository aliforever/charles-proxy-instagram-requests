# Charles Proxy Instagram Requests
Instagram Private API Requests Exported From Charles Proxy

Requests are separated by Instagram's Android versions


# How to Contibute:

### Note: You should have a Facebook account and an Instagram account associated with it. (Login to Instagram with Facebook)

1. [Go to Researcher Settings on Facebook](https://www.facebook.com/whitehat/researcher-settings/)

2. Check "Enable user installed Certificate Authorities (CAs) for your Facebook account" and "Enable user installed CAs for your Whitehat Test Accounts."

3. Choose Instagram in "Select on which apps you want to enable the Mobile Settings."

4. Force Stop Instagram and Clear Data.

5. Login to Instagram with Your Facebook Account.

6. Go to Instagram's Settings -> Internal -> Whitehat Settings

7. Check "Allow user installed certificates" and "Do not use TLS 1.3"

8. Force Stop Instagram and Clear Data

9. Set WIFI's proxy to Charles Proxy Address

10. Open Instagram and Export Requests in Charles Session File Format (.chls) (note: Give it a Suitable Name)

11. Move the exported file to its related Instagram android version.

#### Pull Request!

Cheers 🥳

# How to Find Version, VersionCode and Signature Key?

Check User-Agent Header in Requests for version and version code:

![Check User-Agent Header in Requests for version and version code](https://i.ibb.co/grTDTGD/version-code.png)

## To Find out Signature
1. Install Frida using `pip install frida`
2. Run [frida-server](https://github.com/frida/frida/releases) on your device using adb.
3. Run Instagram on Your Phone or Emulator
4. Put Below Code in a File Name `script.js` and Run Using Python (`python script.py`):
```python
import frida, sys

def on_message(message, data):
    print(message)

process = frida.get_usb_device().attach('com.instagram.android')

jscode = """
Interceptor.attach(Module.findExportByName("libscrambler.so", "_ZN9Scrambler9getStringESs"), {
    onLeave: function (retval) {
        console.log(Memory.readCString(retval));
    }
});
"""

script = process.create_script(jscode)
script.on('message', on_message)
print('[*] Running sniffer')
script.load()
sys.stdin.read()
```
5. Make a Request in Instagram to Get Signature Printed:

![Signature](https://i.ibb.co/2kqDpcy/signature.png)
