# Shop-Webapp

Shop-webapp is a single page progressive web app created - in the first place - for an artisan selling handmade soaps.

You can see the live version running here : [https://ptitcoinsavonnerie.fr](https://ptitcoinsavonnerie.fr).
*Please note that the running app is only in french (but the whole code is in english), and it delivers only in France.*
  *We are not responsible for color choices.*

It is build with polymer, rely on firebase, and goes with its own [backend API](https://github.com/cursed-duo/backend-shop-webapp).
As an e-shop, it presents all the features for selling online goods :

#### Customers can :
- browse products
- place orders, manage their cart and pay (cards or paypal)
- find or contact the store

#### Admins can :
- create or update products, manage stocks, and prices
- manage orders (mark as sent, refund)
- see some analytics

## Stack

* [**Polymer**](https://www.polymer-project.org/1.0/) (1.8.0, with no plan to upgrade later)
* [**Polymer-starter-kit**](https://developers.google.com/web/tools/polymer-starter-kit/)
* [**Firebase**](https://firebase.google.com/)

## Progressive

#### Mobile ready

The app is responsive. Every display or control has been made for rendering / working on mobile as well as on desktop. You can add the app to your homescreen and run it in standalone mode.

#### Offline capable

This app works offline (recent firefox and chrome) ! Most data are cached locally, so even if you run the application without internet or lose network, you can still browse products you crossed before, or see your orders. Some functionalities are disabled (payment and other stuff), but the whole thing keeps running.

This is done by :
- [data-source component](https://github.com/cursed-duo/shop-webapp/blob/master/src/components/data-source.component.html) which gather the requested data from cache first, and then check the network (if available) to update them. Local caching is relying on IndexedDB.
- service-worker which cache the app files to be able to serve them even without network. Polymer-CLI generates it on build from [polymer.json](https://github.com/cursed-duo/shop-webapp/blob/master/polymer.json) and [sw-precache-config.js](https://github.com/cursed-duo/shop-webapp/blob/master/sw-precache-config.js).

#### PRPL

The app follows the [PRPL pattern](https://developers.google.com/web/fundamentals/performance/prpl-pattern/) :
- Push : [firebase.json](https://github.com/cursed-duo/shop-webapp/blob/master/firebase.json) (rel=import),
- Render : [my-app.html](https://github.com/cursed-duo/shop-webapp/blob/master/src/my-app.html) (app shell),
- Pre-cache : [firebase.json](https://github.com/cursed-duo/shop-webapp/blob/master/firebase.json) (rel=preload),
- Lazy-load : [page-transition.behavior.html](https://github.com/cursed-duo/shop-webapp/blob/master/src/behaviors/page-transition.behavior.html), [modal-container.component.html](https://github.com/cursed-duo/shop-webapp/blob/master/src/components/modal-container.component.html).

#### Push notification

Upon user agreement, the app can delivers notifications to desktop and/or mobile when specific events occurs (order is sent, or refunded), using Firebase Cloud Messaging. See [notification-registerer.component.html](https://github.com/cursed-duo/shop-webapp/blob/master/src/components/notification-registerer.component.html).
For further details about endpoints handling, see [backend-shop-webapp](https://github.com/cursed-duo/backend-shop-webapp).

## Other Notables Features

Aside from the expected set of features that powers an e-shop (create / manage products, navigate through orders, etc.), there are less visible features that are worth mentioning :

#### Firebase

This app rests on Firebase for all its data, user authentication, files storage and hosting. All the informations displayed are updated as soon as modifications occurs in Firebase, without refresh or any other action, keeping the app interactive and dynamic.

#### 60 FPS

We tried our best to make the app smooth and animated when navigating, when elements appear or things pop. The effects are handled through behaviors. Two good examples are : [page transitions](https://github.com/cursed-duo/shop-webapp/blob/master/src/behaviors/page-transition.behavior.html) or [list animations](https://github.com/cursed-duo/shop-webapp/blob/master/src/behaviors/list-animation.behavior.html).

#### Parallel uploads
The app allows to upload pictures (straight to firebase storage) for products. It is possible to send many pictures at the same time, or even to start uploading on different products. The [upload behavior](https://github.com/cursed-duo/shop-webapp/blob/master/src/behaviors/upload.behavior.html) handles them through a common state. You can find more explanations in the file comments.

#### Other components
And with all this, there is also a whole lot of components, ranging from inputs to carousel. Some are based on the polymer catalog, and others are hand-crafted. You can find them in the [components source folder](https://github.com/cursed-duo/shop-webapp/tree/master/src/components) (you got it already).

## Support

![Google Chrome][logo_chrome] ![Safari][logo_safari] ![Firefox][logo_firefox] ![Edge][logo_edge]

## License

This app uses a BSD-like license that is available [here](https://github.com/cursed-duo/shop-webapp/blob/master/license.txt).

## Special thanks

Thanks to the Polymer Authors, and a special shoutout for the [Polymer Shop](https://github.com/Polymer/shop) which was a good help and source of inspiration.

[logo_chrome]: https://firebasestorage.googleapis.com/v0/b/savon-1df9a.appspot.com/o/internal%2Fchrome_64x64.png?alt=media&token=e5fe8e0c-b136-46b1-9b94-0dc39c2d10c5 "Google chrome"
[logo_safari]: https://firebasestorage.googleapis.com/v0/b/savon-1df9a.appspot.com/o/internal%2Fsafari_64x64.png?alt=media&token=50839dd0-2fe2-4d41-be25-a44889d6a78f "Safari"
[logo_firefox]: https://firebasestorage.googleapis.com/v0/b/savon-1df9a.appspot.com/o/internal%2Ffirefox_64x64.png?alt=media&token=c2a20811-8257-404a-8b16-d1c19e7adf27 "Firefox"
[logo_edge]: https://firebasestorage.googleapis.com/v0/b/savon-1df9a.appspot.com/o/internal%2Fedge_64x64.png?alt=media&token=32c863a5-595a-4eab-9fa5-2382fc4d5a4b "Edge"
