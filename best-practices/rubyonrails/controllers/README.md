# Ruby on Rails Controllers

## Be RESTful as possible

Ruby on Rails supports RESTful and creating other actions that are outside the standard makes the understanding and maintenance, so it's a good idea to create specific controllers and use the REST methods. For example: An approval routine for a comment.

```ruby
# Instead of this...
class CommentsController < ApplicationController
  def approve
    @comment.approve!
  end
end

# ...You should do this.
class ApproveCommentsController < ApplicationController
  def update
    @comment.approve!
  end
end
```

And, configure routes to `ApproveCommentsController` be nested of `CommentsController`. For details see the [Ruby on Rails Guides](http://guides.rubyonrails.org/routing.html).

If it won't be possible for some reason, write a good methods's documentation for these actions and use `member` or `collection` in the `routes.rb`:

```ruby
# ...You should do this.
resources :comments, only: [:index, :show] do
  member do
    put :approve
    put :disapprove
  end
end
```

## Keep clear and simple

* Use [plataformatec/responders](https://github.com/plataformatec/responders) gem to dry up your Rails app (3.2+).
* Set `respond_to` in the `ApplicationController`.
* Use `respond_with` in actions.
* Set the flash messages in the Flash Responder's. For details see [Flash Responder Manual](https://github.com/plataformatec/responders#flashresponder).
* Use private methods and `before_action` to help to mantain controllers clean
* Use before filter to ensure access of users, or similar.
* Use the `:show` action only if you need to show some important information that does not fit in the `index`. Or if you need something more complex to be displayed.
* Escape from actions `show` that show the same thing as the `:index`.
