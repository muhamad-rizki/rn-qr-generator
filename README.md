
# rn-qr-generator

https://www.npmjs.com/package/rn-qr-generator

## Getting started

`$ npm install rn-qr-generator --save`

### Mostly automatic installation

`$ react-native link rn-qr-generator`

---

#### Important:
Linking is not needed anymore. ``react-native@0.60.0+`` supports dependencies auto linking.
For iOS you also need additional step to install auto linked Pods (Cocoapods should be installed):
``` 
cd ios && pod install && cd ../
```
___

### Manual installation


#### iOS

1. In XCode, in the project navigator, right click `Libraries` ➜ `Add Files to [your project's name]`
2. Go to `node_modules` ➜ `rn-qr-generator` and add `RNQrGenerator.xcodeproj`
3. In XCode, in the project navigator, select your project. Add `libRNQrGenerator.a` to your project's `Build Phases` ➜ `Link Binary With Libraries`
4. Run your project (`Cmd+R`)<

#### Android

1. Open up `android/app/src/main/java/[...]/MainActivity.java`
  - Add `import com.gevorg.reactlibrary.RNQrGeneratorPackage;` to the imports at the top of the file
  - Add `new RNQrGeneratorPackage()` to the list returned by the `getPackages()` method
2. Append the following lines to `android/settings.gradle`:
  	```
  	include ':rn-qr-generator'
  	project(':rn-qr-generator').projectDir = new File(rootProject.projectDir, 	'../node_modules/rn-qr-generator/android')
  	```
3. Insert the following lines inside the dependencies block in `android/app/build.gradle`:
  	```
      compile project(':rn-qr-generator')
  	```


## Usage
```javascript
import RNQRGenerator from 'rn-qr-generator';

RNQRGenerator.generate({
  value: 'https://github.com/gevgasparyan/rn-qr-generator', // required
  height: 100,
  width: 100,
  base64: false,            // default 'false'
  backgroundColor: 'black', // default 'white'
  color: 'white',           // default 'black'
})
  .then(response => {
    const { uri, width, height, base64 } = response;
    this.setState({ imageUri: uri });
  })
  .catch(error => console.log('Cannot create QR code', error));
```

Example of 2FA QR code with Time Based (TOTP) or Counter Based (HOTP)

```
RNQRGenerator.generate({
  ...
  value: 'otpauth://totp/Example:google@google.com?secret=HKSWY3RNEHPK3PXP&issuer=Issuer',
})
```

More information about totp can be found [here](https://github.com/google/google-authenticator/wiki/Key-Uri-Format).

# Note
Some simulators may not generate qr code properly. Use real device if you get an error.
