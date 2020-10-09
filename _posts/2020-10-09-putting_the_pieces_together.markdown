---
layout: post
title:      "Putting the Pieces Together"
date:       2020-10-09 23:30:20 +0000
permalink:  putting_the_pieces_together
---


For my second project at Flatiron I created a Sinatra application. Sinatra is a DSL (domain specific language) and web application library.  It is a simple, yet effective framework designed to quickly create web applications with Ruby. 

One challenge I had while working on this project was implementing error messages. After some googling, I stumbled across a fellow Flatiron student's blog post about using sessions for error messages. That's where I started for my first attempt. I began by creating a key called “error_message” in the session hash. Then, in my create route I assigned the appropriate value to session[:error_message] depending on the validity of user inputs.

```
session[:error_message] = "Successfully created story."
```

In my show route, I assigned the value of session[:error_message] to a variable @error_message. This would allow it to be accessed and rendered by my view file. I then immediately reassigned the value of @error_message to nil  to ensure the message would only show up once. 

```
@error_message = session[:error_message]
session[:error_message] = nil
```

This process did work. However, I wanted a more efficient solution, one that did not require me to assign and reassign values over and over. This is where flash error messages came in. A flash message allows you to save specific information then render it in the next full-page reload only. I used a gem called Sinatra::Flash to implement flash messages into my application. After setting up the gem, I could insert error messages simply by assigning value in my create route,

```
flash[error_message] = "This is the error message"
```

and by adding the below into my HTML code.

```
<%= styled_flash %>
```

Because the data only persists for the next page reload, it eliminates any need for extra code (e.g. assigning session[:error_message] to variable, reassigning session[:error_message] to nil) in the show route.

This project was challenging. But once my class relationships and CRUD routes were set up, I actually really enjoyed tinkering with the code and improving what I could. After finishing the CLI project, being able to work in an actual web browser felt like a huge step forward. I feel that now, I’m finally putting the pieces together and understanding how everything I’ve learned so far comes together to create the actual web pages I use everyday. 
