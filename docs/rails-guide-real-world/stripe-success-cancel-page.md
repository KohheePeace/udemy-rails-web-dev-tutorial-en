## Cancel page
Just back to the post page is enough
`cancel_url`
```ruby
def checkout
  post = Post.find(params[:id])

  session = Stripe::Checkout::Session.create(
    payment_method_types: ['card'],
    line_items: [{
      name: post.title,
      description: post.title,
      images: [post.thumbnail.service_url],
      amount: post.price_cents,
      currency: 'usd',
      quantity: 1,
    }],
    success_url: 'https://example.com/success?session_id={CHECKOUT_SESSION_ID}',
    cancel_url: post_url(post),
  )

  # This is a key point
  render json: { sessionId: session[:id] }
end
```

## Success page
未定。
`success_url`
```ruby
def checkout
  post = Post.find(params[:id])

  session = Stripe::Checkout::Session.create(
    payment_method_types: ['card'],
    line_items: [{
      name: post.title,
      description: post.title,
      images: [post.thumbnail.service_url],
      amount: post.price_cents,
      currency: 'usd',
      quantity: 1,
    }],
    success_url: 'https://example.com/success?session_id={CHECKOUT_SESSION_ID}',
    cancel_url: post_url(post),
  )

  # This is a key point
  render json: { sessionId: session[:id] }
end
```