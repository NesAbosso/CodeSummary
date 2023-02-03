# CodeSummary
C# Live Project Code Summary

# Introduction

For the last two weeks of my time at the tech academy, I worked with my peers in a team developing a full scale MVC/MVVM Web Application in C# for a local theatre/acting company's website. Working on a codebase with a team was a great learning oppertunity for fixing bugs, cleaning up code, and adding requested features. This was a large project and working in a team allowed us to accomplish all our goals by the deadline. For this project we utilized an Agile work environment in Azure DevOps and SCRUM processes, which involved daily standups and weekly code retrospectives during the two week sprint. I worked on several front-end and back-end stories that I am very proud of.

Below are descriptions of the stories I worked on, along with code snippets.


## Table of Contents
* Create and Style About Page
* Create Comment Model & CRUD Pages
* Comments Partial View
* Styling the Comments
* Like/Dislike Implementation
* Conclusion and Skills Learned


# Create and Style About Page

For this story, I was assigned the task of designing the About page for the Vertigo Theatre web application. This about page is going to show the Mission Statement, Ensemble (including the images), Company History, and Board. I utilized Bootstrap cards for the display of images. 

I also added a nice theatre seat background and Broadway font in CSS for styling.  
      
            
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

# Update-Database

I then scaffold the CRUD pages, by right-clicking on the Controllers folder, selecting Add > New Scaffolded Item, and selecting Razor Pages using Entity Framework. You would then select the Comment model and the required pages (Index, Edit, Create, Details, and Delete).
After scaffolding, you would be able to access the CRUD pages for the Comment model and perform operations such as creating, editing, and deleting comments. The pages would use Entity Framework to interact with the database and display information about comments.

![image](https://user-images.githubusercontent.com/117785546/216729713-93e254cf-5198-4d83-abbb-9ccb38399516.png)



# Comments Partial View

For this story I had to create a partial view for the comments section. To display comments on the BlogPosts Index page, you would first create a partial view in the Comments View folder named "_Comments". This partial view would be responsible for displaying the comments and should have the capability to be used on other pages.
Next, you would replace the table on the Comments Index page with a method that calls the "_Comments" partial view. The method would pass the comments to the partial view as a model and render the partial view.

@Html.Partial("_Comments")


