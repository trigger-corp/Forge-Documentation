.. _best-practice-wireless-distribution:

Wireless distribution on iOS
============================

If you are using Adhoc or Enterprise distribution certificates when packaging your iOS app, you are able to wirelessly distribute the resulting IPA file. To help you do this, a wireless distribution plist template will be generated and output alongside your IPA file in the ``release/ios`` folder.

In order to use this plist you will need to modify 3 URLs: all URLs must be absolute and point to a downloadable file. Once you have modified these URLs you can host the plist file and access it from the device to install the app.

The URLs that need to be modified in the plist are:

 * ``http://www.example.com/app.ipa``: is a download URL for the IPA just generated
 * ``http://www.example.com/image.57x57.png``: is a 57x57 pixel PNG icon for your app which will be displayed while it downloads
 * ``http://www.example.com/image.512x512.jpg``: is a high resolution image for your app

More information on wireless app distribution can be found in Apple's documentation: http://developer.apple.com/library/ios/#featuredarticles/FA_Wireless_Enterprise_App_Distribution/Introduction/Introduction.html
