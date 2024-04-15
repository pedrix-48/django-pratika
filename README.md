Atu kria database sira

(envs) C:\Users\HP\Desktop\my_project>python manage.py makemigrations
Migrations for 'blog':
blog\migrations\0001_initial.py - Create model Post

(envs) C:\Users\HP\Desktop\my_project>python manage.py sqlmigrate blog 0001
BEGIN;
--
-- Create model Post
--
CREATE TABLE "blog_post" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "title" varchar(100) NOT NULL, "content" text NOT NULL, "date_post" datetime NOT NULL, "author_id" integer NOT NULL REFERENCES "auth_user" ("id") DEFERRABLE INITIALLY DEFERRED);
CREATE INDEX "blog_post_author_id_dd7a8485" ON "blog_post" ("author_id");
COMMIT;

(envs) C:\Users\HP\Desktop\my_project>python manage.py migrate
Operations to perform:
Apply all migrations: admin, auth, blog, contenttypes, sessions
Running migrations:
Applying blog.0001_initial... OK

(envs) C:\Users\HP\Desktop\my_project>python manage.py shell

> > > from blog.models import Post
> > > from django.contrib.auth.models import User
> > > User.objects.all()
> > > <QuerySet [<User: jessuabelo>, <User: cania>]>
> > > User.objects.first()
> > > <User: jessuabelo>
> > > User.objects.filter(username = 'jessuabelo')
> > > <QuerySet [<User: jessuabelo>]>
> > > User.objects.filter(username = 'jessuabelo').first()
> > > <User: jessuabelo>
> > > user = User.objects.filter(username = 'jessuabelo').first()
> > > user
> > > <User: jessuabelo>
> > > cls
> > > Traceback (most recent call last):
> > > File "<console>", line 1, in <module>
> > > NameError: name 'cls' is not defined
> > > user
> > > <User: jessuabelo>
> > > user.id
> > > 1
> > > user.pk
> > > 1
> > > Post.objects.all()
> > > <QuerySet []>
> > > post_1 = Post(title = 'Blog 1', content = 'First Post Content!', author = user)
> > > Post.objects.all()
> > > <QuerySet []>
> > > post_1.save()
> > > Post.objects.all()
> > > <QuerySet [<Post: Post object (1)>]>
> > > exit()

(envs) C:\Users\HP\Desktop\my_project>python manage.py shell
Python 3.11.2 (tags/v3.11.2:878ead1, Feb 7 2023, 16:38:35) [MSC v.1934 64 bit (AMD64)] on win32
Type "help", "copyright", "credits" or "license" for more information.
(InteractiveConsole)

> > > from blog.models import Post
> > > from django.contrib.auth.models import User
> > > Post.obejcts.all()
> > > Traceback (most recent call last):
> > > File "<console>", line 1, in <module>
> > > AttributeError: type object 'Post' has no attribute 'obejcts'
> > > Post.objects.all()
> > > <QuerySet [<Post: Blog 1>]>
> > > user = User.objects.filter(username = 'jessuabelo').first()
> > > user
> > > <User: jessuabelo>
> > > post_2 = Post(title = 'Blog 2', content = 'Second Post Content', author_id = user.id )
> > > post_2.save()
> > > Post.objects.all()
> > > <QuerySet [<Post: Blog 1>, <Post: Blog 2>]>
> > > post = Post.objects.first()
> > > post
> > > <Post: Blog 1>
> > > post.content
> > > 'First Post Content!'
> > > post.date_posted
> > > Traceback (most recent call last):
> > > File "<console>", line 1, in <module>
> > > AttributeError: 'Post' object has no attribute 'date_posted'
> > > post.date_post
> > > datetime.datetime(2024, 4, 9, 14, 8, 26, 652652, tzinfo=datetime.timezone.utc)
