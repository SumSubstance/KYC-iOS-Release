# KYC-iOS-Release 1.1

### Installation
This framework ment to be installed via [cocoapods](https://cocoapods.org/).

* Add to your Podfile new specs repository:
`source 'https://github.com/SumSubstance/Specs.git'`
* Add dependency to your target 
`pod 'SumSubstanceKYC'`  
* Run `pod install --repo-update`

### Usage 
To instantiate framework call 
```objc
SSEngine *engine = [SSFacade setupForApplicant:applicantID
                                     withToken:authToken
                                        locale:locale
                                  supportEmail:supportEmail
                                       baseUrl:baseUrl];
``` 
Where 
* `applicantID` - your applicant identifier
* `authToken` - your Sum&Sub auth token
* `locale`  -  user language (preferably, NSLocale.currentLocale.localeIdentifier, but you can use any)

Then, you should:
* Connect to remote - `[engine connectWithExpirationHandler:verificationResultHandler:]; `
* Create KYC UI - `[SSFacade getChatControllerWithAttributedTitle:titleOrNil]` 
* Refrest auth token (when needed) - `engine.refreshToken = newToken;`

For more usage examples refer to [demo project](https://github.com/SumSubstance/KYC-iOS-Demo).
