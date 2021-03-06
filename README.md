# Otp Reader

OTP (One-Time Password)  Reader Library for Android helping easily implement listening of SMS messages and using the callback methods to perform password verification etc.

### Gradle Dependencies

> build.gradle (module)
```
compile 'swarajsaaj:otpreader:1.1'
```

### Usage

To implement the Otp reader in the application:-

1. Implement the following service in AndroidManifest.xml

```
 <receiver android:name="swarajsaaj.smscodereader.receivers.OtpReader">
        <intent-filter>
            <action android:name="android.provider.Telephony.SMS_RECEIVED"/>
        </intent-filter>
</receiver>
```

2. Add SMS reading permissions in AndroidManifes.xml
```
    <uses-permission android:name="android.permission.RECEIVE_SMS" />
    <uses-permission android:name="android.permission.READ_SMS" />

```

3. Implement the OTPListener Interface in your activity
```
public class MainActivity extends ActionBarActivity implements OTPListener {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        OtpReader.bind(this,"SENDER_NUM_HERE");
    }

    
    @Override
    public void otpReceived(String smsText) {
        //Do whatever you want to do with the text
        Toast.makeText(this,"Got "+smsText,Toast.LENGTH_LONG).show();
        Log.d("Otp",smsText);
    }
}
```

4. Bind the current Activity (or OTPListener) to OtpReader with second argument as the sender number (e.g. if it might be like BM-BIZY, DM-BIZY you can give this argument as "BIZY" or some constant like 9898982222 , enter any extract substring of the expected number here or leave it blank to read all incoming messages. If not left blank the numbers containing the string will be considered for listening).

```
OtpReader.bind(this,"SENDER_NUM_HERE");
```

Override the otpReceived method
```
  @Override
    public void otpReceived(String smsText) {
        //Do whatever you want to do with the text
        Toast.makeText(this,"Got "+smsText,Toast.LENGTH_LONG).show();
        Log.d("Otp",smsText);
    }
```

#### Thats it. otpReceived will be called when the message is received.