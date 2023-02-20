# CodeSummary
C# Live Project Code Summary

# Introduction

For the last two weeks of my time at the tech academy I was an intern for Prosper IT Consulting, I worked in a team developing a full scale MVC/MVVM Web Application in C# for a local theatre/acting company's website. Working on a codebase with a team was a great learning oppertunity for fixing bugs, cleaning up code, and adding requested features. This was a large project and working in a team allowed us to accomplish all our goals by the deadline. For this project we utilized an Agile work environment in Azure DevOps and SCRUM processes, which involved daily standups and weekly code retrospectives during the two week sprint. I worked on several front-end and back-end stories that I am very proud of.

Below are descriptions of the stories I worked on, along with code snippets.


## Table of Contents
* Create and Style About Page
* Create Comment Model & CRUD Pages
* Comments Partial View
* Styling the Comments
* Like/Dislike Implementation
* Conclusion and Skills Learned


# Create and Style About Page

For this story, I was assigned the task of designing the About page for the Vertigo Theatre web application. This about page is to show the Mission Statement, Ensemble (including the images), Company History, and Board. I utilized Bootstrap cards for the display of images. 

I also added a nice theatre seat background and Broadway font for styling.  
      
            
    body {
        background: url(https://media.istockphoto.com/id/1295114854/photo/empty-red-armchairs-of-a-theater-ready-for-a-show.jpg?b=1&s=170667a&w=0&k=20&c=W__8iZMDp4XtPAMPRuTPPYzszc1A4fdajYGn0ox9kG4=) no-repeat center center fixed;
        font-family: 'Broadway', sans-serif;
        background-size: cover;
    }

![image](https://user-images.githubusercontent.com/117785546/216728182-fa715d16-dff5-4b79-967a-d4643b6dca0f.png)


# Create Comment Model & CRUD Pages

For this story I was tasked with creating a Comment Model & CRUD Pages. Here I created a Comment model in the blog area and first defined the model with properties. 

    public class Comment
    {
        public int CommentId { get; set; }
        public string Author { get; set; }
        public string Message { get; set; }
        public DateTime CommentDate { get; set; }
        public int Likes { get; set; }
        public int Dislikes { get; set; }

Next, I created a database context class to manage the database connection.

    public DbSet<Comment> Comments { get; set; }

To add the model to the database, you would run the following command in the Package Manager Console.

## Update-Database

I then scaffold the CRUD pages, by right-clicking on the Controllers folder, selecting Add > New Scaffolded Item, and selecting Razor Pages using Entity Framework. I then select the Comment model and the required pages (Index, Edit, Create, Details, and Delete).
After scaffolding, I was able to access the CRUD pages for the Comment model and perform operations such as creating, editing, and deleting comments. The pages would use Entity Framework to interact with the database and display information about comments.

![image](https://user-images.githubusercontent.com/117785546/216729713-93e254cf-5198-4d83-abbb-9ccb38399516.png)



# Comments Partial View

For this story I had to create a partial view for the comments section. To display comments on the BlogPosts Index page, I first created a partial view in the Comments View folder named "_Comments". This partial view would be responsible for displaying the comments and should have the capability to be used on other pages.
Next, replace the table on the Comments Index page with a method that calls the "_Comments" partial view. The method would pass the comments to the partial view as a model and render the partial view.

    @Html.Partial("_Comments")
      
With this setup, I was able to display the comments on the BlogPosts Index page by calling the "_Comments" partial view and passing it the comments as a model. This would allow for code reusability and maintainability, as you would only need to make changes in one place (the partial view) if there are updates to the way comments are displayed.
      
# Styling the Comments
      
For this story I was tasked with styling the comment section. Instead of using tables to show Comments, we want the Comments to look more like Comments you might see on other popular websites. I redesigned the comments so that the Author that wrote the Comment is displayed, the time that has passed since the comment was uploaded, the text for the Comment, the Like/Dislike (or Upvote/Downvote) buttons (and the number of Likes/Dislikes beside those buttons), and a Reply button and add a trashcan button using a font-awesome icon.
      
    <span class="comment-author">@comment.Author</span>
            <span class="comment-time">@comment.CommentDate.ToString("g")</span> 

    <span class="delete-button">
        <i class="fa fa-trash"></i>
    </span>

In my code, the author, text, time, and Like/Dislike buttons are displayed for each comment. The time is calculated as the difference between the current time and the time the comment was uploaded. The number of Likes and Dislikes are also displayed next to the respective buttons. Additionally, a trashcan icon has been added as a font-awesome icon to represent the "delete" functionality that Admins will have.
      
![image](https://user-images.githubusercontent.com/117785546/216731304-286822dc-be4b-40eb-9bde-46d65833735c.png)
      
# Like/Dislike Implementation
      
In my last story I implemented the Like/Dislike or Upvote/Downvote functionality.
      
I created action methods in the Comment controller for incrementing the Like and Dislike properties.
 
    [HttpPost]
        public JsonResult Like(int commentId)
        {
            Comment comment = db.Comments.Find(commentId);
            comment.Likes++;
            db.SaveChanges();
            return Json(new { likes = comment.Likes });
        }   
      
      
 In the view, I added buttons for each action and use jQuery to bind an AJAX call to each button's click event.
      
     <button id="dislike-button-@comment.CommentId" class="btn btn-danger btn-sm dislike-button">Dislike</button>
        <span id="dislikes-@comment.CommentId">@comment.Dislikes</span>
      
    $(".dislike-button").click(function () {
                var commentId = $(this).attr("id").split("-")[2];
                $.ajax({
                    type: "POST",
                    url: "/Blog/Comments/Dislike",
                    data: { commentId: commentId },
                    success: function (data) {
                        $("#dislikes-" + commentId).text(data.dislikes);
      
This allowed for each like and dislike button to increment by 1 when clicked.
      
      
![image](https://user-images.githubusercontent.com/117785546/216734112-bc8052cc-cd45-4930-b351-431ca2cdff67.png)

      
      
# Conclusion and Skills Learned
      
This live project was an invaluable opportunity to really test myself, my skills and gain experience working in an Agile team environment. The skills I gained working in a collaborative development including:
      
    * Communication
    * Problem–Solving Skills
    * Time Management
    * Team Building Skills
    * Able to revise, update and debug code
    * Can design the backend database for the web-based application
    * Create web-based applications and test them by running the MVC Framework-based Applications
    * Code-first or db-first approach
      
  Overall, I really relished the real world experience that this Live Project provided me and look forward to applying what I have learned in my future projects.
