>>> u1 = User.objects.create_user(username='Semyon')
>>> u1
<User: Semyon>
>>> u2 = User.objects.create_user(username='Sam')
>>> u2
<User: Sam>
>>> Author.objects.create(authorUser=u1)
<Author: Author object (1)>
>>> Author.objects.create(authorUser=u2)
<Author: Author object (2)>
>>> Category.objects.create(name='IT')
<Category: Category object (1)>
>>> Category.objects.create(name='US')
<Category: Category object (2)>
>>> Category.objects.create(name='SKILL')
<Category: Category object (3)>
>>> Category.objects.create(name='FACTORY')
<Category: Category object (4)>
>>> author = Author.objects.get(id=1)
>>> author
<Author: Author object (1)>
>>> Post.objects.create(author=author, categoryType='NW', title='sometitle', text='somebigtext')
<Post: Post object (1)>
>>> Post.objects.get(id=1)
<Post: Post object (1)>
>>> author = Author.objects.get(id=2)
>>> author
<Author: Author object (2)>
>>> Post.objects.create(author=author, categoryType='AR', title='sometitle', text='sometext') 
<Post: Post object (2)>
>>> Post.objects.get(id=1).title
'sometitle'
>>> Post.objects.get(id=1).postCategory.add(Category.objects.get(id=1))
>>> Comment.objects.create(commentPost=Post.objects.get(id=1), commentUser=Author.objects.get(id=1).authorUser, text='anytextbyauthor')
<Comment: Comment object (1)>
>>> Comment.objects.create(commentPost=Post.objects.get(id=2), commentUser=Author.objects.get(id=2).authorUser, text='textbyauthor')
<Comment: Comment object (2)>
>>> Comment.objects.get(id=1).like()
>>> Comment.objects.get(id=1).rating
1
>>> Comment.objects.get(id=1).dislike()
>>> Comment.objects.get(id=1).dislike()
>>> Comment.objects.get(id=1).dislike()
>>> Comment.objects.get(id=1).rating
-2
>>> Author.objects.get(id=1)
<Author: Author object (1)>
>>> a = Author.objects.get(id=1)
>>> a.update_rating()
>>> a.retingAuthor
-2
>>> Post.objects.get(id=1).like()
>>> a.update_rating()
>>> a.retingAuthor
1
>>> a = Author.objects.order_by('-retingAuthor')[:1]
>>> a
<QuerySet [<Author: Author object (1)>]>
>>> c = User.objects.create_user(username='Din')
>>> Author.objects.create(authorUser=c)
<Author: Author object (3)>
>>> a = Author.objects.order_by('-retingAuthor')[:1]
>>> a
<QuerySet [<Author: Author object (1)>]>
>>> a = Author.objects.order_by('-retingAuthor')
>>> a
<QuerySet [<Author: Author object (1)>, <Author: Author object (2)>, <Author: Author object (3)>]>
>>> for i in a:
...     i.retingAuthor
...     i.authorUser.username
... 
1
'Semyon'
0
'Sam'
0
'Din'

