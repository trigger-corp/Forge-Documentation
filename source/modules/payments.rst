.. _modules-payments:

``payments``: In-app payments
================================================================================

.. warning:: In-app payments is a premium module that is fee while in beta. Contact support@trigger.io to be notified about pricing.

Config
------

The ``payments`` module must be enabled in ``config.json``

.. parsed-literal::
    {
        "modules": {
            "payments": {
                "androidPublicKey": "BASE64\KEY=="
            }
        }
    }

API
---

The ``forge.payments`` namespace allows access to native in-app payment processing.

``transactionReceived.addListener``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Triggered for all payment transaction events, if the payments module is used this listener must be add on all pages to handle transaction events.

The callback for this event will be invoked with two arguments, the first is an object containing the following keys:

 * ``orderId``: A unique order ID returned from iTunes or Google Play, use this to match refunds or cancellations to purchases.
 * ``productId``: The product involved in this transaction
 * ``purchaseTime``: The date and time of purchase
 * ``purchaseState``: One of ``PURCHASED``, ``REFUNDED`` or ``CANCELED``. Gives the state of the transaction, only ``PURCHASED`` exists on iOS.
 * ``notificationId``: An internal identifier used by Forge when confirming transactions.
 * ``receipt``: Receipt information which can be sent to a server and verified with iTunes or Google Play. See the guide for more details.
 
The 2nd argument is a function used to confirm the transaction has been processed, this is required by both iOS and Android to confirm the transaction has been both recieved and correctly processed.

Example::

  forge.payments.transactionReceived.addListener(function (data, confirm) {
    if (data.purchaseState == "PURCHASED") {
        alert("Thanks for buying: "+data.productId);
        confirm();
    } else {
        alert("Your product '"+productId+"' has been removed");
        confirm();
    }
  });

``purchaseProduct``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

Purchase an in-app product identified by ``productId``. The ``success`` callback will be called when the purchase has been approved by the user; after this the transaction information will be returned via the ``transactionReceived`` listener.

.. js:function:: payments.purchaseProduct(productId, success, error)

    :param string productId: product id registered with iTunes or Google Play.
    :param function() success: Purchase approved
    :param function(content) error: called with details of any error which may occur

``restoreTransactions``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
**Platforms: Mobile**

If in-app products are managed by iTunes or Google Play, previous transactions may be requested at any time. This allows transactions to be restored on a new device or if the app has been reinstalled. The ``success`` callback will be called once the request is made; after this the transaction information will be returned via the ``transactionReceived`` listener.

.. js:function:: payments.restoreTransactions(success, error)

    :param function() success: Request sent
    :param function(content) error: called with details of any error which may occur
	
Guide
-----

Using in-app payments
~~~~~~~~~~~~~~~~~~~~~

Javascript
##########

 * In order to receive asynchronous transaction details you must register a ``transactionReceived`` listener on all pages in your app: this must deal with incoming transactions and call the confirmation function when they are dealt with. Not calling the confirm function will cause transactions events to be emitted again at a later time as iTunes/Google Play will assume your app has not handled them successfully.
 * To purchase a product use ``forge.payments.purchaseProduct``. When calling ``purchaseProduct`` pass the ID of your product as created on iTunes/Google Play.

Android
#############################################################################

When developing your app and not signing with a release key, you can use the following special product IDs to test in-app payments:
 * ``android.test.purchased``: This product will return a successful ``PURCHASED`` transaction if the user presses "Buy". It is not managed and so will not be restorable.
 * ``android.test.canceled``: This product will return a ``CANCELED`` transaction immediately if the user presses "Buy".
 * ``android.test.refunded``: This product acts the same as ``android.test.canceled`` but is marked as ``REFUNDED``.
 * ``android.test.item_unavailable``: This product cannot be bought and will display an error to the user.

.. important:: In a real purchase, a ``CANCELED`` transaction may be returned after a ``PURCHASED`` transaction: in this situation, your app should be able to deal with revoking any features enabled by a previously ``PURCHASED`` transaction. If a transaction is cancelled it will have the same ``orderId`` as the original purchase.

Test products are a close simulation to actual products bought through in-app payments, but they do act in subtly different ways: it is important you also test your app with real purchases before deploying it to users.

In order to test your actual products you will need to make sure you have done the following things:
 * Add your in-app products on the Google Play Developer Console. To do this you will need to sign up for a merchant account through the console.
 * Make sure your in-app products are marked as published: unpublished products will not appear for test users in unpublished APKs
 * Add test accounts in your profile on the Google Play Developer Console. As a developer you cannot purchase your own products, they must be purchased by a test account, who must be the primary user on the device you are testing on. If you (the developer) are the primary user on your device you will need to perform a factory reset and sign in with a test account to test your app.
 * Copy the public key from your profile on the Google Play Developer Console into your payments module config.
 * Package your app through Forge and upload the APK you wish to test to Google Play. You do not need to publish the app to test it as one of the test users you previously created, but you do need to upload it to enable in-app purchases.
 * Install the APK you uploaded to Google Play to the device you wish to test on (and make sure your primary account on the device is a test user who has been added on Google Play).
 * You should now be able to perform in-app purchase actions in your app. Test user purchases will be charged if you allow them to go through: you can manually cancel or refund purchases through the merchant account section of Google Play.

.. important:: You cannot buy your own products: test users must have a different ID to your merchant ID, and the test user must be the **primary** user account on the testing device.

.. note:: You cannot use the emulator to test in-app payments: it must be a real device.

.. note:: When uploading APKs and adding test users, we've found there can sometimes be a delay for the changes to take effect. If you see unexpectedly see messages like **this app is not configured for billing** or **this item is not available**, try waiting for 10 minutes.

iOS
################################################################################

When developing on iOS, there are no test product IDs - only actual products created for your app in iTunes Connect can be tested. However, apps signed with a "iPhone Developer" certificate will run in the iTunes sandbox and any purchases will be simulated (no charge will be made).

In order to test in-app payments on iOS you must make sure you have completed the following steps:
 * Create a specific app ID for your app in the iOS provisioning portal, and create development and distribution provisioning profiles for that app. Wildcard provisioning profiles will not work with in-app purchases.
 * Add your app to iTunes Connect and add any in-app products you want to sell. Currently the payments module support consumable and non-consumable products only, not subscriptions.
 * :ref:`Package your app <releasing-ios-ipa>` with the *distribution* provisioning profile into an IPA and submit it to iTunes Connect; if you do not wish you submit your app for approval yet you can submit it then immediately reject the binary through iTunes Connect.
 * Run the app on a device using the *development* provisioning profile to be able to test in the sandbox with dummy transactions.
 * You cannot buy apps using a real iTunes account while testing: in order to test, you must sign out of the App Store on your device, and when using your app and prompted to login, sign in with a test user created through iTunes Connect.
 * You may need to wait several hours between submitting your app and in-app items and them being available for you to test with. If you have followed all of the above steps and still have problems you may just need to wait for the changes you have made to become active.

.. note:: You can configure the provisioning profile and developer certificate to use in your ``local_config.json`` file, see :ref:`parameters-in-a-file`. Being able to switch between development and distribution environments with :ref:`Profiles <local_conf-profiles>` is a time saver.

Managed products / ``restoreTransactions``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If you create "managed" items on Google Play or "Non-Consumable" items on iTunes Connect then you can restore purchases the user has made at a later date, if they have reinstalled your app or moved to another device.

To restore transactions made on another install or another device use ``forge.payments.restoreTransactions``, calling this may cause the user to be prompted for login details, so it is best to only call it when first setting up an application, or if a user specifically requests it. Any restored transactions will be returned through the ``transactionReceived`` listener.

Receipts
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In order to confirm a purchase has been legitimately made through iTunes or Google Play it is best to forward details of the transaction to your server and verify the transaction there. To allow this both iTunes and Google Play provide signed receipts for the transactions.

Android
#######

On Android, the ``receipt`` property of the transaction contains the ``type`` as ``android``, as well as a ``data`` property containing a JSON string with the receipt data, a ``signature`` property containing a base64 encoded signature and a ``signed`` property which is a boolean indicating whether or not the signature matches. Details on how to verify the signature can be found in the Android documentation: http://developer.android.com/guide/market/billing/billing_integrate.html#billing-signatures.

The ``signature`` property is determined on the device in Java and should not be trusted if the data can be sent to a server to be verified.

iOS
################################################################################

On iOS the ``receipt`` property of the transaction contains the ``type`` as ``iOS`` and a ``data`` property which is a base64 encoded receipt. You can forward the receipt to iTunes in order to verify it by following the instructions provided by Apple: http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/StoreKitGuide/VerifyingStoreReceipts/VerifyingStoreReceipts.html
