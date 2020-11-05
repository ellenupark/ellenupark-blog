---
layout: post
title:      "Delving into Rails"
date:       2020-11-05 23:41:47 +0000
permalink:  delving_into_rails
---


For my third project at Flatiron I was tasked with creating a Rails applications. I recently got a pomsky puppy. So, my head has been filled with nothing but dog related ideas. Naturally, I geared my app towards dog owners. My app allows users to create an account, add pets to their account and arrange play dates with other dog owners. 

To begin, I spent a lot of time figuring out the associations. I knew right off the bat that I would have a User and Pet model. Users would ` have_many :pets`, pets would `belong_to :user`. That part was simple. The tricky part was how to introduce the Event element. After much thinking and drawing out many diagrams, I created a join table (invites) to connect pets to events. The end result was:


```
class User
   has_many :pets
end

class Pet
   belongs_to :user
   has_many :invites
   has_many :events, through: :invites
end

class Invite
   belongs_to :pet
   belongs_to :event
end

class Event
   has_many :invites
   has_many :pets, through: :invites
end
```

Once my associations were set up I was able to start laying out my routes, controller actions and corresponding views. Coming from Sinatra, this was the most familiar part. One unfamiliar element that I implemented was scope methods. Scope methods are queries that you define and customize inside a model. I created a scope method `past_events` for my Event model. 

```
class Event
   scope :past_events, lambda { where('date <= ?', Time.now ).where('accepted = ?', true) }
end
```

My method `Event.past_events` can be understood as "retrieve all events where the date is less than or equal to now (in other words, in the past) and where accepted equals true". The fact that you can easily understand what a scope method will return by the syntax appealed to me right away. There's nothing better than easy to read code.



