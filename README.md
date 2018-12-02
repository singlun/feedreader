# Feed Reader And Testing

## Overview

This project is a web-based application that reads RSS feeds. The aim of this project is to test the application by using Jasmine JavaScript Testing Tool. In Order to test the application, all the test condition will be specify in the `feedreader.js` file. The test condition will run against the application which is base on the `app.js ` source code. The testing will be divided into 4 parts namely `'RRS Feeds'`, `'The Menu'`, `'Initial Entries'` and the `'New Feed Selection'`. Fully testing of each part will be describe below. One thing to mention, no tests is dependent on the results of one and another.

## Installation

The project runs on any browser, web-server is required. To install it on the web server. You just need to copy and paste the `'feedreader'` folder to the root directory your web server. Inorder to access the web site for example `localhost`: you just need to type in `http://localhost/feedreader/index.html`.


## Testing Strategy

1. The First part let's begin to Tests `'RSS Feeds'`. This part we will write a test that loops through each feed in the `allFeeds` object and ensures it has a **URL** defined _and_ that the **URL** is not empty. Next, we will Write a test that loops through each feed in the `allFeeds` object and ensures it has a **Name** defined and that the **Name** is not empty.

    * To achieve this tasks, we use a `for...of` loop to loop through the `allFeeds` object and check whether the URL of each item in the `allFeeds` object is empty or not. Three conditions will be encountered :

        * undefined
        * null
        * empty string
        
        The first two conditions we can use the Jasmine Funtion to test:

            `expect(feedUrl.url).toEqual(jasmine.anything())`

        The 'jasmine.anything()' will return 'TRUE' if the actual value is not null or undefined.
    
        Then for the last condition we can use the 'Not Equal to' operator to test:

            `expect(feedUrl.url).not.toEqual('');`

        For the 'Name' this also applies the same.

2. The second part we will test `'The Menu'`. This part we will test two things. First we will test whether the `'Menu Element'` is hidden by default. Next we ensures the `'Menu changes visibility'` when the menu icon is clicked.

    * To test whether the menu element is hidden by default we can check the `body` tag whether it contains the class element `'menu-hidden'` on the first load.
       
            `expect(document.querySelector('body').classList.contains('menu-hidden')).toBe(true);`

    * To ensures the `'Menu changes visibility'` when the menu icon is clicked, we can test by removing and adding the `'menu-hidden'` class element to the `body` tag on the first load. Two conditions will be encountered :
        
        * Removing the `'menu-hidden'` class element from the `body` tag on the first load.
        * Adding `'menu-hidden'` class element to the `body` tag on the first load.

        For the first conditon when removing the class element. The menu element must be visible on the first load. You can use the DOM function remove() method to handle.

            `document.querySelector('body').classList.remove('menu-hidden');

            expect(document.querySelector('body').classList.contain('menu-hidden')).toBe(false);`

        For the second conditon when adding the class element. The menu element must not be visible on the first load. You can use the DOM function add() method to handle.

            `document.querySelector('body').classList.add('menu-hidden');
            
            expect(document.querySelector('body').classList.contains('menu-hidden')).toBe(true);`

3. The third part we will test `'Initial Entries'`. This part we will write a test that ensures  the `'loadFeed()'` function is called and completes its work. The `'loadFeed()'` is a asynchronous `'AJAX'` function which loads the RSSFeed using the Google Feed Reader API. It will then perform all of the DOM operations required to display feed entries on the page. Feeds are referenced by their index position within the allFeeds array. This function all supports a callback as the second parameter which will be called after everything has run successfully.  

    * To acheive this tasks. We must use Jasmine's `'beforeEach'` and asynchronous `'done()'` function to test the `'loadFeed()'` ajax.

           `beforeEach(function(done) {
                 setTimeout(function() {
                    loadFeed(0, done);
                 }, 1);    
            });`  

        In the above snipplet we pass the `'done()'` funtion as a callback to the `'loadFeed()'` method. The `'loadFeed()'` method will execute the `'done()'` function. The `'loadFeed()'` will not complete until its `'done()'` is called from the `'describe'` spec.

            `it('method LoadFeed() is called and completes its work', function(done) {
                done();
                expect(entriesLen).toBeGreaterThan(0);
            });`

        As you can see, inorder to check the `'loadFeed()'` method successfully completed it's tasks, we can check the vairable `'entriesLen'`. This variable stores the total number of feeds that retrieved from the RSSFeed results. The variable must be greater than 0 inorder to pass the test.

4. The fourth part we will test `'New Feed Selection'`. This part we will write a test that ensures when a new feed is loaded by the `'loadFeed()'` function the content will actually changes.

    * To acomplish this tasks. we need to load two different feeds for a given article. Due to the complexity of comparing the contents of the two feeds, we just compare the total number of feeds for each article (Two feeds must be carefully selected as the total number of feeds must not be the same). If the total number of feeds for a given article are not the same we assume we have pass the test. 
        
        * The article we are going to test is `'Linear Digressions'`

            * First load the feed [Html 5 Rocks](http://feeds.feedburner.com/html5rocks)
                
                The total number of feeds for this article is 10 (**total no of feeds might change due to updates**).
                
            * Second load the feed [Udacity Linear Digressions](http://feeds.feedburner.com/udacity-linear-digressions)

                The total number of feeds for this article is 203 (**total no of feeds might change due to updates**).

            * Compare the results 10 not equal to 203.
    
        The methodology of retrieving and counting the number of feeds is quite similar to the test `'Number 3'`.As the feeds is loaded by the ajax `'loadFeed()'` method. We apply the `'beforeEach()'` and `'done()'` technique. Please refer to `'Test Number 3'` for detail description.

## References

* Plug-Ins
    * [Jasmine](https://jasmine.github.io/)
    * [eslint](https://eslint.org/)
    * [visual studio code editor for window](https://code.visualstudio.com/)
* Code References
    * [volare - Testing async calls with jasmine](https://volaresystems.com/blog/post/2014/12/09/Testing-async-calls-with-Jasmine)
    * [Stack OverFlow](https://stackoverflow.com/)
    * [w3schools](https://www.w3schools.com)
    * [Udacity](https://www.udacity.com/)
    * [GitHub](https://github.com/)
    