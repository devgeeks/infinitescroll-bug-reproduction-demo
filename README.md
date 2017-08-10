# infinitescroll-bug-reproduction-demo

Framework7/Vue Webpack app to demo Infinite Scroll bug on iOS

## Bug description

NOTE: this only happens in iOS when in an actual Cordova app or "Add to Homescreen".

When loading content into an infinite scroll from an async source like an API 
call, the infinite scroll possibly has an incorrect height initially, so scrolling 
isn't available.

Once another gesture is performed (presumably then reloading the scroll 
container or page) scrolling again becomes possible.


# Bug reproduction steps using this repo

## Build Project

``` bash
# install dependencies
npm install

# build for production with minification
npm run build
```

## Create a cordova app

```bash
# create a blank app
cordova create infinitescroll

# use the built version of this app
rm infinitescroll/www

cp -r dist infinitescroll/www

cd infinitescroll

cordova platform add ios
```

## Run the app on iOS (the simulator is fine, usually)

```bash
cordova run ios
```

## Test the bug

When the app has lunched on the simulator, click the "About" link.

Once the placeholder content has finished loading, try scrolling down the page. 

It should fail to scroll.

Now try beginning a "swipe to go back" gesture, but don't complete it and 
remain on this page.

Now try scrolling the page.

It should scroll.
