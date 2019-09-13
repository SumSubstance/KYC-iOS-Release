# KYC-iOS-Release 2.9.1

## Liveness3D module

### Installation
This framework ment to be installed via [cocoapods](https://cocoapods.org/).

* Add to your `Podfile` specs repositories: `SumSubstance/Specs`, and public one - `CocoaPods/Specs`
* Specify `use_frameworks!` option
* Add dependency `SumSubstanceKYC/Liveness3D` to your target

Resulting `Podfile` could look as follows:
```ruby
platform :ios, '9.3'

source 'https://github.com/CocoaPods/Specs.git'
source 'https://github.com/SumSubstance/Specs.git'

use_frameworks!

target 'MyAwesomeApp' do

  pod 'SumSubstanceKYC/Liveness3D'

  # any other dependencies
end
```
* Run `pod install --repo-update`

### Usage 
Instantiate the module and pass handlers
```objc
SSLiveness3D *liveness3D =
[SSLiveness3D.alloc initWithBaseUrl:baseUrl
                              token:token
                             locale:locale
             tokenExpirationHandler:^(void (^ _Nonnull completionHandler)(NSString * _Nullable))
 {
     // get new token then call completionHandler
     getNewToken(^(NSString *token) {
     	completionHandler(token);
     };
     
 } completionHandler:^(UIViewController * _Nonnull controller, SSLiveness3DStatus status) {
     
     // process status then update UI accordingly

     // possible statuses are:
     // SSLiveness3DStatus_Cancelled,
     // SSLiveness3DStatus_InitializationFailed,
     // SSLiveness3DStatus_CameraPermissionDenied,
     // SSLiveness3DStatus_TokenIsInvalid,
     // SSLiveness3DStatus_VerificationPassedSuccessfully,

     [controller dismissViewControllerAnimated:YES completion:nil];
 }];
``` 
Where 
* `baseUrl` - `test-msdk.sumsub.com` for test environment or `msdk.sumsub.com` for production one
* `token` - your Sum&Sub auth token
* `locale` - user locale (preferably `NSLocale.currentLocale.localeIdentifier`, but you can use any)

Then create and display UI
```objc
UIViewController *vc = [liveness3D getController];

vc.modalTransitionStyle = UIModalTransitionStyleCrossDissolve;

[self.navigationController presentViewController:vc animated:YES completion:nil];
```

For usage example refer to [demo project](https://github.com/SumSubstance/KYC-iOS-Demo).
