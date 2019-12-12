## Home page
https://stackoverflow.com/a/11003820

`terminal`
```
docker-compose run web rails g controller Pages home
```

```
create  app/controllers/pages_controller.rb
  route  get 'pages/home'
invoke  erb
create    app/views/pages
create    app/views/pages/home.html.erb
invoke  test_unit
create    test/controllers/pages_controller_test.rb
invoke  helper
create    app/helpers/pages_helper.rb
invoke    test_unit
invoke  assets
invoke    scss
create      app/assets/stylesheets/pages.scss
```

`routes.rb`
```ruby
Rails.application.routes.draw do
  get 'pages/home'
  root 'pages#home'
end
```

## Edit home page
### Step1 Copy existing code

### Step2 Move images asset
move images under `app/assets/images`


### Step3 Use image_tag
```erb
<%= image_tag "jumbotron.svg", alt: "jumbotron", class: "img-fluid" %>
```


`app/views/pages/home.html.erb`
```erb
<!-- Navbar -->
<nav class="navbar navbar-expand-lg navbar-light">
  <a class="navbar-brand font-weight-bold" href="#">Logo</a>
  <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
    <span class="navbar-toggler-icon"></span>
  </button>

  <div class="collapse navbar-collapse" id="navbarSupportedContent">
    <ul class="navbar-nav mr-auto">
      <li class="nav-item active">
        <a class="nav-link" href="#">Home <span class="sr-only">(current)</span></a>
      </li>
      <li class="nav-item">
        <a class="nav-link" href="#">Link</a>
      </li>
      <li class="nav-item dropdown">
        <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
          Dropdown
        </a>
        <div class="dropdown-menu" aria-labelledby="navbarDropdown">
          <a class="dropdown-item" href="#">Action</a>
          <a class="dropdown-item" href="#">Another action</a>
          <div class="dropdown-divider"></div>
          <a class="dropdown-item" href="#">Something else here</a>
        </div>
      </li>
      <li class="nav-item">
        <a class="nav-link disabled" href="#" tabindex="-1" aria-disabled="true">Disabled</a>
      </li>
    </ul>
    <button class="btn btn-warning my-2 my-sm-0" type="submit">Sign Up</button>
  </div>
</nav>
<!-- # Navbar -->

<!-- Jumbotron -->
<div class="jumbotron bg-primary" style="padding-bottom: 5rem; border-bottom-left-radius: 30% 10%; border-bottom-right-radius: 30% 10%;">
  <div class="row">
    <div class="col-md-6 mb-5">
      <h1 class="display-4 font-weight-bold">Hello, world!</h1>
      <p class="lead">This is a simple hero unit, a simple jumbotron-style component for calling extra attention to featured content or information.</p>
      <hr class="my-4">
      <p>It uses utility classes for typography and spacing to space content out within the larger container.</p>
      <a class="btn btn-warning btn-lg rounded-pill" href="#" role="button">Get Started</a>
    </div>
    <div class="col-md-6">
      <%= image_tag "jumbotron.svg", alt: "jumbotron", class: "img-fluid" %>
    </div>
  </div>
</div>
<!-- # Jumbotron -->

<!-- About Us -->
<section id="about">
  <div class="container">
    <header class="pb-5">
      <h1 class="text-center font-weight-bold">About Us</h1>
      <p class="text-center w-50 mx-auto">Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>
    </header>

    <div class="container">
      <div class="row">
        <div class="col-lg-6 order-1 order-lg-2">
          <%= image_tag "about-easy-collaboration.svg", alt: "about-easy-collaboration", class: "img-fluid" %>
        </div>

        <div class="col-lg-6 pt-4 pt-lg-0 order-2 order-lg-1">
          <h2 class="font-weight-bold">Easy Collaboration</h2>
          <p>
            Delectus alias ut incidunt delectus nam placeat in consequatur. Sed cupiditate quia ea quis. Voluptas nemo qui aut distinctio. Cumque fugit earum est quam officiis numquam. Ducimus corporis autem at blanditiis beatae incidunt sunt. 
          </p>
          <p>
            Voluptas saepe natus quidem blanditiis. Non sunt impedit voluptas mollitia beatae. Qui esse molestias. Laudantium libero nisi vitae debitis. Dolorem cupiditate est perferendis iusto.
          </p>
          <p>
            Eum quia in. Magni quas ipsum a. Quis ex voluptatem inventore sint quia modi. Numquam est aut fuga mollitia exercitationem nam accusantium provident quia.
          </p>
        </div>
      </div>

      <div class="row pt-5">
        <div class="col-lg-6">
          <%= image_tag "about-knowledge-bases.svg", alt: "about-knowledge-bases", class: "img-fluid" %>
        </div>
        <div class="col-lg-6 pt-5 pt-lg-0">
          <h2 class="font-weight-bold">Knowledge Bases</h2>
          <p>
            Ipsum in aspernatur ut possimus sint. Quia omnis est occaecati possimus ea. Quas molestiae perspiciatis occaecati qui rerum. Deleniti quod porro sed quisquam saepe. Numquam mollitia recusandae non ad at et a.
          </p>
          <p>
            Ad vitae recusandae odit possimus. Quaerat cum ipsum corrupti. Odit qui asperiores ea corporis deserunt veritatis quidem expedita perferendis. Qui rerum eligendi ex doloribus quia sit. Porro rerum eum eum.
          </p>
        </div>
      </div>

      <div class="row pt-5">
        <div class="col-lg-6 order-1 order-lg-2">
          <%= image_tag "about-interaction-design.svg", alt: "about-interaction-design", class: "img-fluid" %>
        </div>

        <div class="col-lg-6 pt-4 pt-lg-0 order-2 order-lg-1">
          <h2 class="font-weight-bold">Interaction Design</h2>
          <p>
            Delectus alias ut incidunt delectus nam placeat in consequatur. Sed cupiditate quia ea quis. Voluptas nemo qui aut distinctio. Cumque fugit earum est quam officiis numquam. Ducimus corporis autem at blanditiis beatae incidunt sunt. 
          </p>
          <p>
            Voluptas saepe natus quidem blanditiis. Non sunt impedit voluptas mollitia beatae. Qui esse molestias. Laudantium libero nisi vitae debitis. Dolorem cupiditate est perferendis iusto.
          </p>
          <p>
            Eum quia in. Magni quas ipsum a. Quis ex voluptatem inventore sint quia modi. Numquam est aut fuga mollitia exercitationem nam accusantium provident quia.
          </p>
        </div>
      </div>
    </div>
  </div>
</section>
<!-- # About Us -->

<!-- Carousel -->
<div id="carouselExampleIndicators" class="carousel slide bg-primary" data-ride="carousel" style="height: 350px;">
  <header class="section-header pt-4 pb-3">
    <h1 class="text-center text-white font-weight-bold">Testimonials</h1>
  </header>
  <ol class="carousel-indicators">
    <li data-target="#carouselExampleIndicators" data-slide-to="0" class="active"></li>
    <li data-target="#carouselExampleIndicators" data-slide-to="1"></li>
    <li data-target="#carouselExampleIndicators" data-slide-to="2"></li>
  </ol>
  <div class="carousel-inner px-4 text-white">
    <div class="carousel-item text-center active">
      <%= image_tag "portrait-1.jpg", alt: "portrait-1", class: "mb-3 rounded-circle border border-white", style: "width: 90px;" %>
      <h5 class="mt-0">Jimmy Donaldson</h5>
      <p>
        Cras sit amet nibh libero, in gravida nulla.
      </p>
    </div>
    <div class="carousel-item text-center">
      <%= image_tag "portrait-2.jpg", alt: "portrait-2", class: "mb-3 rounded-circle border border-white", style: "width: 90px;" %>
      <h5 class="mt-0">Morgan Adams</h5>
      <p>
        Cras sit amet nibh libero, in gravida nulla.
      </p>
    </div>
    <div class="carousel-item text-center">
      <%= image_tag "portrait-3.jpg", alt: "portrait-3", class: "mb-3 rounded-circle border border-white", style: "width: 90px;" %>
      <h5 class="mt-0">Chandler Hallow</h5>
      <p>
        Cras sit amet nibh libero, in gravida nulla.
      </p>
    </div>
  </div>
  <a class="carousel-control-prev" href="#carouselExampleIndicators" role="button" data-slide="prev">
    <span class="carousel-control-prev-icon" aria-hidden="true"></span>
    <span class="sr-only">Previous</span>
  </a>
  <a class="carousel-control-next" href="#carouselExampleIndicators" role="button" data-slide="next">
    <span class="carousel-control-next-icon" aria-hidden="true"></span>
    <span class="sr-only">Next</span>
  </a>
</div>
<!-- # Carousel -->

<!-- Clients -->
<section class="py-5 border-bottom">
  <div class="container">
    <div class="row">
      <div class="col-md-3 col-sm-6">
        <a href="#">
          <img class="img-fluid d-block mx-auto" src="https://blackrockdigital.github.io/startbootstrap-agency/img/logos/envato.jpg" alt="">
        </a>
      </div>
      <div class="col-md-3 col-sm-6">
        <a href="#">
          <img class="img-fluid d-block mx-auto" src="https://blackrockdigital.github.io/startbootstrap-agency/img/logos/designmodo.jpg" alt="">
        </a>
      </div>
      <div class="col-md-3 col-sm-6">
        <a href="#">
          <img class="img-fluid d-block mx-auto" src="https://blackrockdigital.github.io/startbootstrap-agency/img/logos/themeforest.jpg" alt="">
        </a>
      </div>
      <div class="col-md-3 col-sm-6">
        <a href="#">
          <img class="img-fluid d-block mx-auto" src="https://blackrockdigital.github.io/startbootstrap-agency/img/logos/creative-market.jpg" alt="">
        </a>
      </div>
    </div>
  </div>
</section>
<!-- # Clients -->

<!-- Footer -->
<footer class="container py-5">
  <div class="row">
    <div class="col-12 col-md">
      <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" class="d-block mb-2" role="img" viewBox="0 0 24 24" focusable="false"><title>Product</title><circle cx="12" cy="12" r="10"></circle><path d="M14.31 8l5.74 9.94M9.69 8h11.48M7.38 12l5.74-9.94M9.69 16L3.95 6.06M14.31 16H2.83m13.79-4l-5.74 9.94"></path></svg>
      <small class="d-block mb-3 text-muted">© 2017-2019</small>
    </div>
    <div class="col-6 col-md">
      <h5>Features</h5>
      <ul class="list-unstyled text-small">
        <li><a class="text-muted" href="#">Cool stuff</a></li>
        <li><a class="text-muted" href="#">Random feature</a></li>
        <li><a class="text-muted" href="#">Team feature</a></li>
        <li><a class="text-muted" href="#">Stuff for developers</a></li>
        <li><a class="text-muted" href="#">Another one</a></li>
        <li><a class="text-muted" href="#">Last time</a></li>
      </ul>
    </div>
    <div class="col-6 col-md">
      <h5>Resources</h5>
      <ul class="list-unstyled text-small">
        <li><a class="text-muted" href="#">Resource</a></li>
        <li><a class="text-muted" href="#">Resource name</a></li>
        <li><a class="text-muted" href="#">Another resource</a></li>
        <li><a class="text-muted" href="#">Final resource</a></li>
      </ul>
    </div>
    <div class="col-6 col-md">
      <h5>Resources</h5>
      <ul class="list-unstyled text-small">
        <li><a class="text-muted" href="#">Business</a></li>
        <li><a class="text-muted" href="#">Education</a></li>
        <li><a class="text-muted" href="#">Government</a></li>
        <li><a class="text-muted" href="#">Gaming</a></li>
      </ul>
    </div>
    <div class="col-6 col-md">
      <h5>About</h5>
      <ul class="list-unstyled text-small">
        <li><a class="text-muted" href="#">Team</a></li>
        <li><a class="text-muted" href="#">Locations</a></li>
        <li><a class="text-muted" href="#">Privacy</a></li>
        <li><a class="text-muted" href="#">Terms</a></li>
      </ul>
    </div>
  </div>
</footer>
<!-- # Footer -->

<!-- Back to Top Button -->
<div id="back-to-top-btn" class="btn btn-warning rounded-circle">
  <i class="fas fa-chevron-up"></i>
</div>
<!-- # Back to Top Button -->
```