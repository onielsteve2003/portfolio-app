* First, do python manage.py startapp blog
* Then, do python manage.py startapp jobs

* We first went to the models.py in the jobs and then created a class called Job and to do that we had to pass in the models.Model for the class to be able to be created..... Then the image = models.imageField is because we want the job to have an Image and this is like a syntax or so, we want to save images connected with a job to the images directory.. Next we pass the summary = models.charField(i.e This is for the for the boxes )

* Next we went to the settings.py and added our Job.apps and co.... Under the installed apps
* Next, we did _MEDIA__ROOT = os.path.join(BASE_DIR, 'media') in the settings.py at the bottom meaning anytime the user is saving a file that is connected with the model, It should go inside of a new folder in the same space with the db.sqlite3
* you have to install pillow inside of your newvenv and do python manage.py makemigrations and do python manage.py migrate and it will create a migration  something 001...
* Next we did a python manage.py createsuperuser which will ask for a username and password that you will use to login to the /admin in your website

* We want whenever we go to the /admin and login, It should show us the list of jobs and co and the way to do that is to go under the jobs folder and open up the admin.py and add this: from .models import Job to import the job from models and to see the space for where the jobs will be shown, you have to do admin.site.register(Job)..... Then we went to add job, once u click add job the models.py then loads the image code and the summary code!

* Next, we went to the urls.py and imported settings from django.conf in order for static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT) to execute and then next we imported from django.conf.urls.static import static
static is the whole app that allows us to serve up images, etc

* Next we downloaded postgreSQL coz we wanted to change the database we are using so after downloading it, You go to the settings.url and then go to database and change the engine to django.db.backends.postgresql and then the name of the database we created was portfoliodb so we gave the name to be that and then the user to be postgres then we gave the password to be django123 and so on..... All this, We already created them in the postgres DB

* Next step was for us to open the models.py in blogs and created a class for title, publication date, body and image for the users then next step was to add the blog to settings.py under installed_apps then we created a migrations which gave us the folder called migrations and then we did python manage.py migrate and the last thing we did for the blog was to add the blog to the admin by simply going into the admin.py and importing blog from .models and also doing a admin.site.register(blog) so that data for those models can be created , deleted and so on through the user interface.

* Next was to create the home url by going to the url.py and then adding a path for the home page and also importing job.views in the url.py.... Then next is going into the views.py and defining a function called home for the homepage
We did this: jobs/templates/jobs/home.html because both the jobs and the blog is going to have a home.html so something like that sha and we have views.py in different folder

* After creating the home.html, we then Added code with bootstrap inside of the file to beautify the home page

* Next, We Went to the views.py and imported Job from models and then we passed in Job.objects and this simply means it will go get all job objects from the database and turn them into python objects, Then we went to the return render and passed in a dictionary like: {'jobs':jobs}

* Next, We went to the home.html and then above the code for showing the jobs, we had to pass in a loop there coz we don't know how much Jobs the user will have, so its depending. Then we passed in job.summary so that whatever job that is passed in the database will be displayed

* Next, we want a situation where by ths user can click on a blog and it takes them to the recent blog posts and stuffs like that.... So we started by going into the urls.py and specifying the path for the blog and then we went to the blogs folder and created a file names urls.py and passed in this path: path('', views.allblogs, name='allblogs') and also went to the views.py for blog and defined a function for allblogs and rendered the request and the html file
N/B: That blog.urls simply means when the user requests for the blog page, it looks at that include blog.urls and it goes under the blog folder and looks for the urls.py under blogs and finds the url path for blog... The reason we did not put the blog url in the same file as the main url is because for example if you are working on a big project, the urls file might get messy so the best way is to add the include and put the url in the folder

* Next, we went to the views.py for the blog and imported blog from models and then we wanted all the blogs to show up in the blogs page, so we simply did a for loop in the allblogs.html that shows up all the amount of blogs that is in the database.... So, We passed the blog.title first, then next was the blog.pub_date and so on...... Then we went to the models.py to adddef summary(self):return self.body[:100] meaning if a text or sentence is more than 100 characters, Summarize it into just 100 texts for me Thats all, Then if you want it to work effectively, You have to pass it in as blog.summary rather than blog.title but i left mine as .title so you can you anyone..... We also went to the models.py and passed in def __str__(self): return self.title meaning in the admin page, It shows you the title of your blog and the you can click it and edit if you want to.

* Next, we want something like, when the user clicks the link on each blog, It should show the url in the url on the web broser Like the blog/the id something like that so in the urls.py we passed in <int:blog_id> and gave the name to be detail and we now went inside the views.py to pass in the function called detail which has a request and thr blog_id... The int there means for example, out Id is 1 so it should be like blog/1 thats why the int is there then the blog_id means the number which is either 1 or 2 or whatsoever, Next we imported get_object_or_404 meaning it either gets an object from the DB or it throws back a 404 error, Then we passed in get_object_or_404(Blog, pk=blog_id) where pk means the primary key which is equal to the blog id then we saved it into a variable called detailblog and returned render request and a new file called detail.html then we passed in a dictionary

<!-- Short summary on how the detail came into the project -->
N/B: It first starts in the main urls.py and sees the path as blog/, include.... so it then redirects to the blog folder and goes into the blog/urls.py and see that after the first url path the next has something called an int so it saves it as a blog id and then we called it views.detail and passed the name as detail and then we went to the views.py and defined a function as detail where we passed in the request and blog id and return render detail.html and we also passed in a dictionary, so then it redirects to the detail.html and then looks into that file and sees what to print out

* We went to the settings.py and added STATIC_ROOT = os.path.join(BASE_DIR, 'static')
MEDIA_URL = '/static/' on separate lines because we created a folder called static and then we want to save our images there and our resume. Then we ran a command such as python manage.py collectstatic.... It collects everything about static, Then we went to the home.html and added a load static at the top of the page and then we went down to where we have something called resume to put our picture there and we also put an image in the home page 

* Next we went to the allblogs and added <a href="{% url 'detail' blog.id %}"><h3>{{blog.title}}</h3></a> so that when we click a blog it shows the full detail  

* So Finally, The detail page is something like when you click a blog then is elaborates, It expands So We put in some code in the detail.html where by if u click on a blog post is shows you everything about it...
