## CSS coordinate
x increase to the right
y increase to the bottom


## creating a section with image exceeding into next section
* Apply top section margin-bottom: x pixel
* Apply a protruding section with top: x pixel
* using top in relative position, will shift element in y direction
* using top in absolute, will position element at the edge of the parent container

![section protrusion](https://res.cloudinary.com/db80dscth/image/upload/v1569922702/Screenshot_2019-10-01_at_5.32.30_PM_wu6hit.png "Logo Title Text 1")


## Animate on scroll
1. Use AOS library 
2. do yourself.
The idea is to add a class 'animated-object' to the element block you want to animate.
use javascript or jquery to get the animated object and cache them.
Create a function to check if the animated object fits within the height of view window. if it does, add class "in-view", else remove it. Then use transform: translate3d and transition to make the animation. 
See below

Javascript
```
var $window = $(window);
var $animateObjects = $('.animate-section');



function check_if_in_view(){
	// get current view height 
	var window_height = $window.height();
	var window_top = $window.scrollTop();
	var window_bottom = window_top + window_height;



	//get animate object height
	//outer height includes padding, border and margin
	$.each($animateObjects, function(){
		var $element = $(this);
		var elementHeight = $element.outerHeight();
		var	elementTop = $element.offset().top;
		var elementBottom = elementTop + elementHeight;

	//check if animate object in in current view
	if( (elementTop <= window_bottom)  && (elementBottom >= window_top)){
		console.log('inview');
		$element.addClass('in-view');
	}else{
		// console.log('outview');
		$element.removeClass('in-view');
	}

	});
}

//on scroll or resize, check if in view
$window.on('scroll resize', check_if_in_view);
// trigger scroll on page load
$window.trigger('scroll');
```

CSS
```
/* animation on scroll */
.animate-section{
   position: relative;
}

.bottom-up{
  opacity: 0;
  transition: all 500ms ease-out;
  transform: translate3d(0px, 100px, 0px);

}

.in-view .bottom-up{
  opacity: 1;
  transform: translate3d(0px, 0px, 0px);
}
```
HTML
```
      <section class="animate-section animate-block">
        <h1 class="bottom-up">This is section2</h1>
      </section>
           
      <section class="animate-section animate-block">
        <h1 class="bottom-up">This is section2</h1>
      </section>
       
      <section class="animate-section animate-block">
        <div class="bottom-up">
          <h1>This is section2</h1>
          <img src="https://images.unsplash.com/44/MIbCzcvxQdahamZSNQ26_12082014-IMG_3526.jpg?ixlib=rb-0.3.5&amp;q=80&amp;fm=jpg&amp;crop=entropy&amp;w=1080&amp;fit=max&amp;s=49dab7a5e4b2e28b5707bc2db974c94b">
        </div>
      </section>
```
