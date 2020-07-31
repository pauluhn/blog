# Why is it looking for a `Mac App Distribution` for a fastlane iPhone build?

Are you trying to build an iPhone app with an `iPhone Distribution` certificate but getting an error because it can't find the `Mac App Distribution` signing certificate?

Is this the error you get?
```
Error Domain=IDECodesignResolverErrorDomain Code=1 "No signing certificate "Mac App Distribution" found"
 UserInfo={IDEDistributionIssueSeverity=3, 
  NSLocalizedRecoverySuggestion=No "Mac App Distribution" signing certificate matching team ID "<REDACTED>" with a private key was found., 
  IDEProvisioningError_UserInfoKey_IDEProvisioningErrorSpecifier=Mac App Distribution, 
  NSLocalizedDescription=No signing certificate "Mac App Distribution" found, 
  IDEProvisioningError_UserInfoKey_IDEProvisioningErrorPlatform=com.apple.platform.macosx, 
  IDEProvisioningError_UserInfoKey_IDEProvisioningErrorAction=5, 
  IDEProvisioningError_UserInfoKey_IDEProvisioningErrorTeam=<IDEProvisioningBasicTeam: 0x<REDACTED>; teamID='<REDACTED>', 
  teamName='(null)'>}
** EXPORT FAILED **
[14:35:21]: Exit status: 70
```

Did you double and triple check your `CODE_SIGN_IDENTITY` to make sure they are all set to `iPhone *`a?

Did you double and triple confirm it on fastlane like below?

```
+---------------------------------------------------------------+---------------------------------------------------------+
|                                                 Summary for gym x.xxx.x                                                 |
+---------------------------------------------------------------+---------------------------------------------------------+
| export_options.signingCertificate                             | iPhone Distribution                                     |
```

Do you have `Automatically manage signing` turned off?

Did you just add `Firebase` to your project?

...

Welcome back to that last corner of the Internet!

If you are still here, your journey requires one more step into the void: https://github.com/firebase/firebase-ios-sdk/issues/5403.

TLDR: Remove `run` and `upload-symbols` from `Copy Bundle Resources`
