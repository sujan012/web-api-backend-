# Gharbeti Application
Name: Sujan Basnet
CollegeID: 170327


Batch:23A

Brief description of the domain of My project!
Gharbeti (Rental Management) application reduces problem faced by both buyer and seller while buying and selling property.    Most of the people are worried about the long process of searching property. Gharbeti (Rental Management) Application is a meeting point where buyer and seller of property from different places find each other. Gharbeti (Rental Management) Application deals with Property buy/sell/rent which helps to find buyer and seller of the property. Gharbeti (Rental Management) Application will automate all the facilities provided by broker to buyer and seller.

## List of Main Features
Main Techinal Feature of my project are as given below:
a) User can add Post of available rooms.
b) User can add comment on particular post upload by other users. 
c) User can delete and update their own post.
d) User can update thier own profile with image. 
e) User can contact to the admin with out login into the site.
f) Admin can delete the user ,post and feedback.
g) Admin can update his/her own profile with image.

## API Documentation
List out your main APIs and its sample input and output!

I have used nodejs ,MongoDb express and mongoose to develop the API for the project. The main work of the api is to post the GET,POST,DELETE and PUT
Here are the some sample input and output of my api 

Code for addding post:

router.post('/post', (req, res) => {
    User.findOne({
        _id: req.body._id
    }, function(err, user) {
        if (err) {
            res.json({ 'Success': 'Post Failed Something is wrong. Log in first!!' });
        } else if (!user) {
            res.json({ 'Success': 'Not user' });
        } else if (user) {
            console.log(user.username);
            console.log(req.body.username);
            if (user._id == req.body.user) {
                var post = new Post();

                post.title = req.body.title;
                post.location = req.body.location;
                post.image = req.body.image;
                post.description = req.body.description;
                post.user = req.body.user;
                post.save((err, doc) => {
                    if (err) {
                        console.log('Error during record insertion : ' + err);
                    } else {
                        res.json({ 'Success': 'Post successfully Placed!!!' });
                    }
                });
                console.log(post);
            } else {
                res.json({ 'Success': 'Authentication Failed!!' });
            }
        }

    });

});

If user input the data of the post then the output would be 'Success': 'Post successfully Placed!!!' which would be printed on console.
 
 Another main api I have used is through populate.
  
  Code for veiwing comment and post
  router.post('/postDetail/:id', (req, res) => {
    var locals = {};
    async.parallel([
        function(callback) {
            Post.findById(req.params.id).populate('user').sort({ '_id': -1 }).exec(function(err, post) {
                if (err) return callback(err);
                locals.post = post;
                callback();
            });
        },
        function(callback) {
            Comment.find({ post_id: req.params.id }).populate('user').sort({ '_id': -1 }).exec(function(err, comments) {

                console.log(comments.comment);

                if (err) return callback(err);
                locals.comments = comments;

                callback();
            });
        }
    ], function(err) {
        if (err) return ("asds");
        res.json({
            post: locals.post,
            comments: locals.comments

        });
    });

    console.log(locals.comments);

});

To get details the of comment on particular post  about post method is applied while retriveing the data it shows the data of post with the user and 
the comment on the post with specific user.








