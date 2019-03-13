# Forms, CRUD and Active Record Associations

Take 30 minutes and discuss the following with your table group. Try whiteboarding out different solutions and ideas!

1. Map the CRUD actions (create, read, update, delete) to their matching Sinatra routes and HTTP verbs. For example: In a blog app, displaying the content of one particular blog post corresponds to the "Read" CRUD action and the *show* RESTful route. The matching route would be an HTTP Get request to '/posts/:id' where the id is that particular post's id i.e. '/posts/6' .

Create 
     -request type:GET
     -route '/posts/new'   #grab the page create page first
     -view new.erb

     -request type:POST 
     -route '/posts'        #create action happen
     -redirect '/posts'(index.erb)

  Read
     -request type:GET    #display all the posts
     -route '/posts'
     -view index.erb


     -request type:GET
     -route '/posts/:id'  #display single post
     -view show.erb

  Update
     -request type:GET
     -route '/posts/:id/edit'   #grab/open the edit page for the particular post
     -view edit.erb

     -request type:PATCH
     -route '/posts/:id'  #it's updating this particular post
     -redirect '/posts/:id' 

  Delete 
     -request type:delete
     -route '/posts/:id'
     -redirect '/posts'

2. Build an HTML form to create a new blog post. Then, build a form to edit a post. What are the differences between the two? What routes do they send requests to? What type of requests should each form make?
###### Create
  <html>
    <form method = "POST" action = "/posts">
    <div>
      <label>Title:</label>
      <input type="text" name="post[title]" />
   </div>
      
    <div>
      <label>Content:</label>
      <input type="text" name="post[content]" />
      </div>

       <input type = "submit" id = "Submit"/>
    </form>
  </html>


#### Edit
  <html>
    <form method = "POST" action = "/posts/<%= post.id %>">
    <input type = "hidden" name="_method" value = "PATCH" />
    <div>
      <label>Title:</label>
      <input type="text" name="post[title]" value = "<%= post.title %>" />
   </div>
      
    <div>
      <label>Content:</label>
      <input type="text" name="post[content]" value = "<%= post.content %>" />
      </div>

      <input type = "submit" id = "Submit"/>
    </form>
  </html>

  Differences: 1. where to update(all the <%= %> parts)
  Create form route action = "/posts"
  Edit form route action = "/posts/<%= post.id %>"

  Create form request type :POST
  Edit form request type :PATCH

3. Revisit your CRUD action-to-route map. What view files, if any, does each action/route correspond to?
  
  Refer to Q1 

4. Write out the Active Record code to preform CRUD actions on a Post model.

  Create:   @post = Post.create(parmas[:post])
  Read:     @post = Post.find(params[:id])

  Update:   1. @post = Post.find(params[:id])
            2. @post.update(params[:post])

  Delete:   1. @post = Post.find(params[:id])   
            2. @post.delete    

5. Let's think about the domain model for a To-Do list application. Let's say you have a List model and an Item model.
  * What is the relationship between a list and an item?

  A list has many items
  An item belongs to a list

  * A user needs to be able to visit your app, create a new list and then add items to that list. What route would bring the user to the the page to make a new list? What route would take them to the page to make a new item?

    create list route '/lists/new'
    make new item route '/items/new'

  * How and where would you write the code that associates a new item to its list?
  In the Model
  class Item
   belongs_to :list
  end

  class list
   has_many :items
  end
<p class='util--hide'>View <a href='https://learn.co/lessons/week-4-day-2-discussion'>Forms, CRUD and Active Record Associations</a> on Learn.co and start learning to code for free.</p>
