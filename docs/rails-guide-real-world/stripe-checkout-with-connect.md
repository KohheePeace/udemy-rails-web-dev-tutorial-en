We are using **"direct-charges"**
https://stripe.com/docs/payments/checkout/connect#direct-charges


## Edit controller
`app/controllers/stripe_controller.rb`
```ruby
def checkout
  post = Post.find(params[:id])

  session = Stripe::Checkout::Session.create({
    payment_method_types: ['card'],
    line_items: [{
      name: post.title,
      description: post.title,
      images: [post.thumbnail.service_url],
      amount: post.price_cents,
      currency: 'usd',
      quantity: 1,
    }],
    payment_intent_data: {
      application_fee_amount: (post.price_cents * 0.1),
    },
    success_url: 'https://example.com/success?session_id={CHECKOUT_SESSION_ID}',
    cancel_url: 'https://example.com/cancel',
  }, {
    stripe_account: post.user.stripe_account_id,
  })

  # This is a key point
  render json: { sessionId: session[:id] }
end
```

`show.html.erb`
```js
<script>
var stripe = Stripe('pk_test_HW5Th5fsCXhRBncUo4M2GMZE00JT91FpkZ', {
  stripeAccount: "<%= @post.user.stripe_user_id %>"
});

$("#pay-by-stripe-button").click(function() {
  $.post('/stripe_checkout', { id: "<%= @post.id %>"  }, function(data) {
    sessionId = data.sessionId;

    stripe.redirectToCheckout({
      // Make the id field from the Checkout Session creation API response
      // available to this file, so you can provide it as parameter here
      // instead of the {{CHECKOUT_SESSION_ID}} placeholder.
      sessionId: sessionId
    }).then(function (result) {
      // If `redirectToCheckout` fails due to a browser or network
      // error, display the localized error message to your customer
      // using `result.error.message`.
    });
  });
});
</script>
```


## Test it
1. You see the price is post price
2. You see post id is sent in terminal logs
3. we don't set success_url and cancel_url