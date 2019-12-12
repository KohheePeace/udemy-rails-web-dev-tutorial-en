In this part, we will ==learn the basics of Rails==.

We will follow the **official rails "Getting Started" guide** but a little bit different way.

https://guides.rubyonrails.org/getting_started.html

## 1 Goal of this part

!!! success "Goal of this part"
    1. Become able to make **CRUD**
    2. Understand the below diagram
    ![rails-flow-diagram.png](../img/rails-guide-basics/rails-flow-diagram.png)

## 2 What is Rails?
I just highlighted important part.

https://guides.rubyonrails.org/getting_started.html#what-is-rails-questionmark

Rails is a web application development framework written in the Ruby programming language. It is designed to ==**make programming web applications easier**== by making assumptions about what every developer needs to get started. It allows you to write less code while accomplishing more than many other languages and frameworks. Experienced Rails developers also report that ==**it makes web application development more fun**==.

Rails is opinionated software. It makes the assumption that ==**there is a "best" way to do things, and it's designed to encourage that way**== - and in some cases to discourage alternatives. If you learn "The Rails Way" you'll probably discover a tremendous increase in productivity. If you persist in bringing old habits from other languages to your Rails development, and trying to use patterns you learned elsewhere, you may have a less happy experience.

The Rails philosophy includes two major guiding principles:

- Don't Repeat Yourself: DRY is a principle of software development which states that "Every piece of knowledge must have a single, unambiguous, authoritative representation within a system." By not writing the same information over and over again, our code is more maintainable, more extensible, and less buggy.

- Convention Over Configuration: Rails has opinions about the best way to do many things in a web application, and defaults to this set of conventions, rather than require that you specify minutiae through endless configuration files.

## 3 CRUD
**CRUD** is "Create, read, update and delete".

This concept is **==very very very important==** because every website includes this function.

For example...

### Twitter
1. create tweet
2. read tweet
3. update tweet (we cannot this ...)
4. delete tweet

### Airbnb
1. create listing
2. read listing
3. update listing
4. delete listing

### Youtube
1. create(upload) video
2. read video
3. update video
4. delete video

etc...

## 4 What we will make in this part