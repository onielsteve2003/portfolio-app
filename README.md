# Word-Count
Django...

* First, we created a file named views.py and imported it into the Urls.py because Views is a url.... 

* So once the user does not enter a url after the home page, It takes them to the views.home that we created in the views.py file.

* We then imported the django shortcuts from render so that we will be able to send the user to the home.html if they ask for a request on the homepage.

<!-- Under the urls.py, You have to go there and declare any new Url that was added to your project and there must be a comma at the end of each -->

<!-- The first url in the urls.py was an empty string because it was the homepage....that the user requested -->

<!-- Home.html is like the output..... where things will be displayed -->

* Next, We create the form and then textarea in the home.html where the user can pass in their text....and then the input:type:submit where the users can submit whatever text that have been passed into the textarea

* Next step is to listen so that when the user hits the count button it goes to the count page.... and to do this, We created a function for count whereby when the user seeks a request, it takes them to the count.html the place where the output for the count is...and we added a url for the count to the url.py and this time the Url looks different because in the form in home.html..... that action, we had to specify where it should take us to when the user clicks the form button so that's why we have name to be equal to string count....  N/B: Whatever u pass in the url must be what u will pass in the form action

* Next step is: taking the name of that textarea which is fulltext and then in order to get whatever the user passed or typed in the form, u have to use a request.GET then inside the square bracket u put the fulltext in string and then assign the whole line or request.Get to a variable called fulltext e.g fulltext = request.GET ['fulltext]..... and then under the return render, u pass the dictionary there which is 'fulltext':fulltext and to access this dictionary, you need to go to the count.html and pass in the fulltext with double Curly braces like this: {{fulltext}}  N/B: The first fulltext with string is the key and the other is the value

* Next step: we declared another variable as wordlist in the view.py and the reason is so that it can take whatever text the user passed inside the textarea and then split e.g wordlist = fulltext.split() this means anywhere there is space, It counts up till the end so then the next step is in the return render, You have to pass len(wordlist), This is to get the total number of letters in the word u passed in and the final step is to go into the count.html and then pass the count in your h1 text e.g There are {{count}} words in your text

Next, We used a for loop to check for which number appears the most amongst the whole text.....  We did this by declaring worddictionary/sortedwords and using a for loop to check how many times a word appears in the text and if it is the highest, increment the word.... Something like that

Next, we passed worddictionary as a list in the return render by adding .item() and then in the count.html, we used a for loop to check the word and count how many times it occurred and then we passed the key as word and the value as counttotal

The last step is to sort the number of the words.... Bringing them from highest to lowest so we passed a variable called sortedwords and passed in the necessary params
